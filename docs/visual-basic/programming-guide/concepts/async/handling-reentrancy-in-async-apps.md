---
title: 비동기 앱에서 재진입 처리 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: ef3dc73d-13fb-4c5f-a686-6b84148bbffe
ms.openlocfilehash: 199b7ce2cb8b3f3b8e220f9e2bab7e9c39a8d033
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71352007"
---
# <a name="handling-reentrancy-in-async-apps-visual-basic"></a>비동기 앱에서 재진입 처리 (Visual Basic)

앱에 비동기 코드가 사용될 때, 비동기 작업이 완료되기 전에 동일한 비동기 작업을 다시 수행하는 재진입을 파악하고 방지할 수 있어야 합니다. 재진입 가능성을 식별하고 처리하지 못하면 예기치 않은 결과가 생길 수 있습니다.

> [!NOTE]
> 예제를 실행하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치되어 있어야 합니다.

## <a name="BKMK_RecognizingReentrancy"></a> 재진입 인식

이 항목의 예제에서는 사용자가 **시작** 버튼를 선택하여 일련의 웹 사이트를 다운로드하고 다운로드되는 총 바이트 수를 계산하는 비동기 앱을 시작합니다. 예제의 동기 버전은 처음 실행 후 앱 실행이 완료될 때까지 UI 스레드에서 해당 이벤트를 무시하므로 사용자가 버튼를 선택하는 횟수에 관계없이 동일한 방식으로 응답합니다. 그러나 비동기 앱에서 UI 스레드는 계속 응답하므로 완료되기 전에 비동기 작업을 다시 실행할 수 있습니다.

다음 예제에서는 사용자가 **시작** 버튼를 한 번만 선택하는 경우 예상되는 출력을 보여 줍니다. 다운로드된 웹 사이트 목록이 각 사이트의 크기(바이트)와 함께 나타납니다. 총 바이트 수는 끝에 나타납니다.

```console
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
5. msdn.microsoft.com/library/hh524395.aspx                68959
6. msdn.microsoft.com/library/ms404677.aspx               197325
7. msdn.microsoft.com                                            42972
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591
```

그러나 사용자가 버튼을 두 번 이상 클릭하면 이벤트 처리기가 반복적으로 호출되고 다운로드 프로세스가 매번 다시 실행됩니다. 따라서 여러 개의 비동기 작업이 동시에 실행되면 출력에서 결과를 인터리브하며 총 바이트 수를 파악하기 어렵게 됩니다.

```console
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
5. msdn.microsoft.com/library/hh524395.aspx                68959
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
6. msdn.microsoft.com/library/ms404677.aspx               197325
3. msdn.microsoft.com/library/jj155761.aspx                29019
7. msdn.microsoft.com                                            42972
4. msdn.microsoft.com/library/hh290140.aspx               117152
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591

5. msdn.microsoft.com/library/hh524395.aspx                68959
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
6. msdn.microsoft.com/library/ms404677.aspx               197325
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
7. msdn.microsoft.com                                            42972
5. msdn.microsoft.com/library/hh524395.aspx                68959
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591

6. msdn.microsoft.com/library/ms404677.aspx               197325
7. msdn.microsoft.com                                            42972
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591
```

이 항목의 끝으로 스크롤하면 이 출력을 생성하는 코드를 검토할 수 있습니다. 로컬 컴퓨터에 솔루션을 다운로드한 다음 WebsiteDownload 프로젝트를 실행하거나 이 항목의 끝에 있는 코드를 사용하여 고유한 프로젝트를 만들면 코드를 테스트할 수 있습니다. 자세한 내용 및 지침은 [예제 앱 검토 및 실행](#BKMD_SettingUpTheExample)을 참조하세요.

## <a name="BKMK_HandlingReentrancy"></a> 재입력 처리

앱에서 수행하려는 작업에 따라 다양한 방법으로 재진입을 처리할 수 있습니다. 이 항목에서는 다음 예제를 제공합니다.

- [시작 버튼 사용 안 함](#BKMK_DisableTheStartButton)

  작업이 실행되는 동안 **시작** 버튼을 사용할 수 없도록 설정하여 사용자가 작업을 방해할 수 없도록 합니다.

- [작업 취소 및 다시 시작](#BKMK_CancelAndRestart)

  사용자가 **시작** 버튼을 다시 클릭하는 경우 현재 실행되고 있는 작업을 취소한 다음 가장 최근에 요청한 작업이 계속해서 실행되도록 합니다.

- [여러 작업을 실행하고 출력을 큐 대기](#BKMK_RunMultipleOperations)

  요청한 모든 작업이 비동기적으로 실행되도록 허용하지만 각 작업의 결과가 함께 순서대로 나타나도록 출력의 표시를 조정합니다.

### <a name="BKMK_DisableTheStartButton"></a> 시작 버튼 사용 안 함

`StartButton_Click` 이벤트 처리기의 위쪽에 있는 버튼를 사용하지 않도록 설정하여 작업이 실행되는 동안 **시작** 버튼를 차단할 수 있습니다. 그런 다음 작업이 완료되면 `Finally` 블록 내에서 단추를 다시 사용하도록 설정하여 사용자가 앱을 다시 실행하도록 할 수 있습니다.

다음 코드에서는 이러한 변경 내용을 보여 주며, 별표로 표시되어 있습니다. 이 항목의 끝에 있는 코드에 변경 내용을 추가 하거나 [Async 샘플에서 완성 된 앱을 다운로드할 수 있습니다. .NET 데스크톱 앱의 재진입](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06)에서 완성된 앱을 다운로드할 수도 있습니다. 프로젝트 이름은 DisableStartButton입니다.

```vb
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)
    ' This line is commented out to make the results clearer in the output.
    'ResultsTextBox.Text = ""

    ' ***Disable the Start button until the downloads are complete.
    StartButton.IsEnabled = False

    Try
        Await AccessTheWebAsync()

    Catch ex As Exception
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."
    ' ***Enable the Start button in case you want to run the program again.
    Finally
        StartButton.IsEnabled = True

    End Try
End Sub
```

변경의 결과로 `AccessTheWebAsync`에서 웹 사이트를 다운로드하는 동안 단추가 응답하지 않으므로 프로세스를 다시 입력할 수 없습니다.

### <a name="BKMK_CancelAndRestart"></a> 작업 취소 및 다시 시작

**시작** 버튼을 사용하지 않도록 설정하는 대신 버튼을 활성 상태로 유지하지만 사용자가 버튼을 다시 클릭하는 경우 이미 실행되고 있는 작업을 취소하고 가장 최근에 시작한 작업이 계속되도록 합니다.

취소에 대 한 자세한 내용은 [비동기 응용 프로그램 미세 조정 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)을 참조 하세요.

이 시나리오를 설정하려면 [예제 앱 검토 및 실행](#BKMD_SettingUpTheExample)에서 제공하는 기본 코드를 다음과 같이 변경합니다. [Async Samples: .NET 데스크톱 앱의 재진입](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06)에서 완성된 앱을 다운로드할 수도 있습니다. 이 프로젝트의 이름은 CancelAndRestart입니다.

1. 모든 메서드에 대한 범위 내에 있는 <xref:System.Threading.CancellationTokenSource> 변수 `cts`를 선언합니다.

    ```vb
    Class MainWindow // Or Class MainPage

        ' *** Declare a System.Threading.CancellationTokenSource.
        Dim cts As CancellationTokenSource
    ```

2. `StartButton_Click`에서 작업이 이미 진행 중인지 확인합니다. @No__t-0의 값 @no__t이-1 이면 이미 활성화 된 작업이 없습니다. 값이-0 @no__t 아닌 경우 이미 실행 중인 작업이 취소 됩니다.

    ```vb
    ' *** If a download process is already underway, cancel it.
    If cts IsNot Nothing Then
        cts.Cancel()
    End If
    ```

3. `cts`를 현재 프로세스를 나타내는 다른 값으로 설정합니다.

    ```vb
    ' *** Now set cts to cancel the current process if the button is chosen again.
    Dim newCTS As CancellationTokenSource = New CancellationTokenSource()
    cts = newCTS
    ```

4. @No__t-0의 끝에서 현재 프로세스가 완료 되었으므로 `cts`의 값을 다시 `Nothing`로 설정 합니다.

    ```vb
    ' *** When the process completes, signal that another process can proceed.
    If cts Is newCTS Then
        cts = Nothing
    End If
    ```

다음 코드에서는 `StartButton_Click`의 모든 변경 내용을 보여 줍니다. 추가된 내용은 별표로 표시됩니다.

```vb
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)

    ' This line is commented out to make the results clearer.
    'ResultsTextBox.Text = ""

    ' *** If a download process is underway, cancel it.
    If cts IsNot Nothing Then
        cts.Cancel()
    End If

    ' *** Now set cts to cancel the current process if the button is chosen again.
    Dim newCTS As CancellationTokenSource = New CancellationTokenSource()
    cts = newCTS

    Try
        ' *** Send a token to carry the message if the operation is canceled.
        Await AccessTheWebAsync(cts.Token)

    Catch ex As OperationCanceledException
        ResultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf

    Catch ex As Exception
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."
    End Try

    ' *** When the process is complete, signal that another process can proceed.
    If cts Is newCTS Then
        cts = Nothing
    End If
End Sub
```

`AccessTheWebAsync`에서 다음과 같이 변경합니다.

- `StartButton_Click`에서 취소 토큰을 허용하도록 매개 변수를 추가합니다.

- `GetAsync`가 <xref:System.Threading.CancellationToken> 인수를 허용하므로 <xref:System.Net.Http.HttpClient.GetAsync%2A> 메서드를 사용하여 웹 사이트를 다운로드합니다.

- `DisplayResults`를 호출하여 다운로드한 각 웹 사이트에 대한 결과를 표시하려면 먼저 `ct`를 확인하여 현재 작업이 취소되었는지 확인합니다.

 다음 코드에서는 이러한 변경 내용을 보여 주며, 별표로 표시되어 있습니다.

```vb
' *** Provide a parameter for the CancellationToken from StartButton_Click.
Private Async Function AccessTheWebAsync(ct As CancellationToken) As Task

    ' Declare an HttpClient object.
    Dim client = New HttpClient()

    ' Make a list of web addresses.
    Dim urlList As List(Of String) = SetUpURLList()

    Dim total = 0
    Dim position = 0

    For Each url In urlList
        ' *** Use the HttpClient.GetAsync method because it accepts a
        ' cancellation token.
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)

        ' *** Retrieve the website contents from the HttpResponseMessage.
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

        ' *** Check for cancellations before displaying information about the
        ' latest site.
        ct.ThrowIfCancellationRequested()

        position += 1
        DisplayResults(url, urlContents, position)

        ' Update the total.
        total += urlContents.Length
    Next

    ' Display the total count for all of the websites.
    ResultsTextBox.Text &=
        String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)
End Function
```

이 앱이 실행 되는 동안 **시작** 단추를 여러 번 선택 하면 다음 출력과 유사한 결과가 생성 됩니다.

```console
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               122505
5. msdn.microsoft.com/library/hh524395.aspx                68959
6. msdn.microsoft.com/library/ms404677.aspx               197325
Download canceled.

1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
Download canceled.

1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
5. msdn.microsoft.com/library/hh524395.aspx                68959
6. msdn.microsoft.com/library/ms404677.aspx               197325
7. msdn.microsoft.com                                            42972
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591
```

부분 목록을 제거하려면 `StartButton_Click`에서 코드 첫 줄의 주석 처리를 제거하여 사용자가 작업을 다시 시작할 때마다 텍스트 상자의 내용을 지웁니다.

### <a name="BKMK_RunMultipleOperations"></a> 여러 작업을 실행하고 출력을 큐 대기

이 세 번째 예제는 사용자가 **시작** 버튼을 선택할 때마다 앱이 다른 비동기 작업을 시작하고 모든 작업이 실행되어 완료된다는 점에서 가장 복잡합니다. 요청한 모든 작업은 목록에서 비동기적으로 웹 사이트를 다운로드하지만 작업의 출력은 순차적으로 제공됩니다. 즉, 실제 다운로드 작업은 [재진입 인식](#BKMK_RecognizingReentrancy)의 출력에 표시된 대로 인터리브되지만 각 그룹에 대한 결과 목록은 별도로 제공됩니다.

작업은 표시 프로세스의 게이트키퍼 역할을 하는 전역 <xref:System.Threading.Tasks.Task>, `pendingWork`를 공유합니다.

변경 내용을 [앱 빌드](#BKMK_BuildingTheApp)의 코드에 붙여 넣어 이 예제를 실행하거나, [앱 다운로드](#BKMK_DownloadingTheApp)의 지침에 따라 샘플을 다운로드한 다음 QueueResults 프로젝트를 실행할 수 있습니다.

다음 출력은 사용자가 **시작** 단추를 한 번만 선택하는 경우의 결과를 보여 줍니다. 문제 레이블 A는 처음으로 **시작** 버튼을 선택한 경우의 결과임을 나타냅니다. 숫자는 다운로드 대상 목록에서 URL의 순서를 보여 줍니다.

```console
#Starting group A.
#Task assigned for group A.

A-1. msdn.microsoft.com/library/hh191443.aspx                87389
A-2. msdn.microsoft.com/library/aa578028.aspx               209858
A-3. msdn.microsoft.com/library/jj155761.aspx                30870
A-4. msdn.microsoft.com/library/hh290140.aspx               119027
A-5. msdn.microsoft.com/library/hh524395.aspx                71260
A-6. msdn.microsoft.com/library/ms404677.aspx               199186
A-7. msdn.microsoft.com                                            53266
A-8. msdn.microsoft.com/library/ff730837.aspx               148020

TOTAL bytes returned:  918876

#Group A is complete.
```

사용자가 **시작** 버튼을 세 번 선택하면 앱이 다음 줄과 유사한 출력을 생성합니다. 파운드 기호(#)로 시작하는 정보 줄은 애플리케이션의 진행률을 추적합니다.

```console
#Starting group A.
#Task assigned for group A.

A-1. msdn.microsoft.com/library/hh191443.aspx                87389
A-2. msdn.microsoft.com/library/aa578028.aspx               207089
A-3. msdn.microsoft.com/library/jj155761.aspx                30870
A-4. msdn.microsoft.com/library/hh290140.aspx               119027
A-5. msdn.microsoft.com/library/hh524395.aspx                71259
A-6. msdn.microsoft.com/library/ms404677.aspx               199185

#Starting group B.
#Task assigned for group B.

A-7. msdn.microsoft.com                                            53266

#Starting group C.
#Task assigned for group C.

A-8. msdn.microsoft.com/library/ff730837.aspx               148010

TOTAL bytes returned:  916095

B-1. msdn.microsoft.com/library/hh191443.aspx                87389
B-2. msdn.microsoft.com/library/aa578028.aspx               207089
B-3. msdn.microsoft.com/library/jj155761.aspx                30870
B-4. msdn.microsoft.com/library/hh290140.aspx               119027
B-5. msdn.microsoft.com/library/hh524395.aspx                71260
B-6. msdn.microsoft.com/library/ms404677.aspx               199186

#Group A is complete.

B-7. msdn.microsoft.com                                            53266
B-8. msdn.microsoft.com/library/ff730837.aspx               148010

TOTAL bytes returned:  916097

C-1. msdn.microsoft.com/library/hh191443.aspx                87389
C-2. msdn.microsoft.com/library/aa578028.aspx               207089

#Group B is complete.

C-3. msdn.microsoft.com/library/jj155761.aspx                30870
C-4. msdn.microsoft.com/library/hh290140.aspx               119027
C-5. msdn.microsoft.com/library/hh524395.aspx                72765
C-6. msdn.microsoft.com/library/ms404677.aspx               199186
C-7. msdn.microsoft.com                                            56190
C-8. msdn.microsoft.com/library/ff730837.aspx               148010

TOTAL bytes returned:  920526

#Group C is complete.
```

그룹 B와 C는 그룹 A가 완료되기 전에 시작되지만 각 그룹에 대한 출력은 별도로 나타납니다. 그룹 A에 대한 모든 출력이 먼저 나타나고 그 뒤에 그룹 B에 대한 모든 출력과 그룹 C에 대한 모든 출력이 차례로 나타납니다. 앱은 항상 순서대로 그룹을 표시하고 각 그룹에 대해 URL이 URL 목록에 나타나는 순서대로 개별 웹 사이트에 대한 정보를 항상 표시합니다.

그러나 다운로드가 실제로 수행되는 순서는 예측할 수 없습니다. 여러 그룹이 시작된 후에는 그룹이 생성하는 다운로드 작업이 모두 활성화됩니다. A-1이 B-1보다 먼저 다운로드된다고 가정할 수 없으며 A-1이 A-2보다 먼저 다운로드된다고 가정할 수 없습니다.

#### <a name="global-definitions"></a>전역 정의

샘플 코드는 모든 메서드에서 표시되는 다음과 같은 두 가지 전역 선언을 포함합니다.

```vb
Class MainWindow    ' Class MainPage in Windows Store app.

    ' ***Declare the following variables where all methods can access them.
    Private pendingWork As Task = Nothing
    Private group As Char = ChrW(AscW("A") - 1)
```

`Task` 변수 `pendingWork`는 표시 프로세스를 감독하고 모든 그룹이 다른 그룹의 표시 작업을 방해하지 않도록 합니다. 문자 변수 `group`은 다른 그룹의 출력에 레이블을 지정하여 해당 결과가 예상 순서대로 나타나는지 확인합니다.

#### <a name="the-click-event-handler"></a>Click 이벤트 처리기

이벤트 처리기 `StartButton_Click`은 사용자가 **시작** 버튼를 선택할 때마다 그룹 문자를 증가시킵니다. 그런 다음 처리기에서 `AccessTheWebAsync`를 호출하여 다운로드 중인 작업을 실행합니다.

```vb
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)
    ' ***Verify that each group's results are displayed together, and that
    ' the groups display in order, by marking each group with a letter.
    group = ChrW(AscW(group) + 1)
    ResultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "#Starting group {0}.", group)

    Try
        ' *** Pass the group value to AccessTheWebAsync.
        Dim finishedGroup As Char = Await AccessTheWebAsync(group)

        ' The following line verifies a successful return from the download and
        ' display procedures.
        ResultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "#Group {0} is complete." & vbCrLf, finishedGroup)

    Catch ex As Exception
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."

    End Try
End Sub
```

#### <a name="the-accessthewebasync-method"></a>AccessTheWebAsync 메서드

이 예제에서는 `AccessTheWebAsync`를 두 개의 메서드로 분할합니다. 첫 번째 메서드 `AccessTheWebAsync`는 그룹에 대해 모든 다운로드 작업을 시작하고 `pendingWork`를 설정하여 표시 프로세스를 제어합니다. 이 메서드는 LINQ(통합 언어 쿼리) 쿼리 및 <xref:System.Linq.Enumerable.ToArray%2A>를 사용하여 모든 다운로드 작업을 동시에 시작합니다.

그런 다음 `AccessTheWebAsync`는 `FinishOneGroupAsync`를 호출하여 각 다운로드가 완료될 때까지 대기하고 해당 길이를 표시합니다.

`FinishOneGroupAsync`는 `AccessTheWebAsync`의 `pendingWork`에 할당되는 작업을 반환합니다. 해당 값은 작업이 완료되기 전에 다른 작업에 의한 중단을 방지합니다.

```vb
Private Async Function AccessTheWebAsync(grp As Char) As Task(Of Char)

    Dim client = New HttpClient()

    ' Make a list of the web addresses to download.
    Dim urlList As List(Of String) = SetUpURLList()

    ' ***Kick off the downloads. The application of ToArray activates all the download tasks.
    Dim getContentTasks As Task(Of Byte())() =
        urlList.Select(Function(addr) client.GetByteArrayAsync(addr)).ToArray()

    ' ***Call the method that awaits the downloads and displays the results.
    ' Assign the Task that FinishOneGroupAsync returns to the gatekeeper task, pendingWork.
    pendingWork = FinishOneGroupAsync(urlList, getContentTasks, grp)

    ResultsTextBox.Text &=
        String.Format(vbCrLf & "#Task assigned for group {0}. Download tasks are active." & vbCrLf, grp)

    ' ***This task is complete when a group has finished downloading and displaying.
    Await pendingWork

    ' You can do other work here or just return.
    Return grp
End Function
```

#### <a name="the-finishonegroupasync-method"></a>FinishOneGroupAsync 메서드

이 메서드는 한 그룹의 다운로드 작업을 순환하여 각 작업을 대기하고 다운로드한 웹 사이트의 길이를 표시하고 길이를 합계에 추가합니다.

`FinishOneGroupAsync`의 첫 번째 문은 `pendingWork`를 사용하여 메서드 입력이 이미 표시 프로세스에 있거나 이미 대기 중인 작업을 방해하지 않는지 확인합니다. 이러한 작업이 진행 중인 경우 입력 작업은 해당 순서를 기다려야 합니다.

```vb
Private Async Function FinishOneGroupAsync(urls As List(Of String), contentTasks As Task(Of Byte())(), grp As Char) As Task

    ' Wait for the previous group to finish displaying results.
    If pendingWork IsNot Nothing Then
        Await pendingWork
    End If

    Dim total = 0

    ' contentTasks is the array of Tasks that was created in AccessTheWebAsync.
    For i As Integer = 0 To contentTasks.Length - 1
        ' Await the download of a particular URL, and then display the URL and
        ' its length.
        Dim content As Byte() = Await contentTasks(i)
        DisplayResults(urls(i), content, i, grp)
        total += content.Length
    Next

    ' Display the total count for all of the websites.
    ResultsTextBox.Text &=
        String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)
End Function
```

변경 내용을 [앱 빌드](#BKMK_BuildingTheApp)의 코드에 붙여 넣어 이 예제를 실행하거나, [앱 다운로드](#BKMK_DownloadingTheApp)의 지침에 따라 샘플을 다운로드한 다음 QueueResults 프로젝트를 실행할 수 있습니다.

#### <a name="points-of-interest"></a>관심 영역

출력에서 파운드 기호(#)로 시작하는 정보 줄은 이 예제의 작동 방식을 명확히 나타냅니다.

출력은 다음과 같은 패턴을 보여 줍니다.

- 이전 그룹이 출력을 표시하는 동안 그룹이 시작될 수 있지만 이전 그룹의 출력 표시가 중단되지 않습니다.

  ```console
  #Starting group A.
  #Task assigned for group A. Download tasks are active.

  A-1. msdn.microsoft.com/library/hh191443.aspx                87389
  A-2. msdn.microsoft.com/library/aa578028.aspx               207089
  A-3. msdn.microsoft.com/library/jj155761.aspx                30870
  A-4. msdn.microsoft.com/library/hh290140.aspx               119037
  A-5. msdn.microsoft.com/library/hh524395.aspx                71260

  #Starting group B.
  #Task assigned for group B. Download tasks are active.

  A-6. msdn.microsoft.com/library/ms404677.aspx               199186
  A-7. msdn.microsoft.com                                            53078
  A-8. msdn.microsoft.com/library/ff730837.aspx               148010

  TOTAL bytes returned:  915919

  B-1. msdn.microsoft.com/library/hh191443.aspx                87388
  B-2. msdn.microsoft.com/library/aa578028.aspx               207089
  B-3. msdn.microsoft.com/library/jj155761.aspx                30870

  #Group A is complete.

  B-4. msdn.microsoft.com/library/hh290140.aspx               119027
  B-5. msdn.microsoft.com/library/hh524395.aspx                71260
  B-6. msdn.microsoft.com/library/ms404677.aspx               199186
  B-7. msdn.microsoft.com                                            53078
  B-8. msdn.microsoft.com/library/ff730837.aspx               148010

  TOTAL bytes returned:  915908
  ```

- @No__t-0 작업은 먼저 시작 된 그룹 A에 대 한 `FinishOneGroupAsync`의 시작 부분에 `Nothing`입니다. 그룹 A는 `FinishOneGroupAsync`에 도달할 때 await 식을 아직 완료하지 않았습니다. 따라서 컨트롤이 `AccessTheWebAsync`로 반환되지 않았으며 `pendingWork`에 대한 첫 번째 할당이 발생되지 않았습니다.

- 다음 두 줄은 항상 출력에 함께 나타납니다. 코드는 `StartButton_Click`의 그룹 작업 시작과 `pendingWork`에 그룹에 대한 작업 할당 사이에서 중단되지 않습니다.

  ```console
  #Starting group B.
  #Task assigned for group B. Download tasks are active.
  ```

  그룹이 `StartButton_Click`을 입력한 후 작업은 `FinishOneGroupAsync`를 입력한 다음에야 await 식을 완료합니다. 따라서 코드의 해당 세그먼트 중에는 다른 작업에서 제어할 수 없습니다.

## <a name="BKMD_SettingUpTheExample"></a> 예제 앱 검토 및 실행

예제 앱을 더 잘 이해하려면 다운로드하거나, 직접 빌드하거나, 앱을 구현하지 않고 이 항목의 끝에 있는 코드를 검토할 수 있습니다.

> [!NOTE]
> 예제를 WPF(Windows Presentation Foundation) 데스크톱 앱으로 실행하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치되어 있어야 합니다.

### <a name="BKMK_DownloadingTheApp"></a> 앱 다운로드

1. [Async Samples: .NET 데스크톱 앱의 재진입](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06)에서 완성된 앱을 다운로드할 수도 있습니다.

2. 다운로드한 파일의 압축을 푼 다음 Visual Studio를 시작합니다.

3. 메뉴 모음에서 **파일**, **열기**, **프로젝트/솔루션**을 선택합니다.

4. 압축을 푼 샘플 코드가 저장된 폴더로 이동한 다음 솔루션(.sln) 파일을 엽니다.

5. **솔루션 탐색기**에서 실행하려는 프로젝트의 바로 가기 메뉴를 연 후 **StartUpProject로 설정**을 선택합니다.

6. CTRL+F5를 선택하여 프로젝트를 빌드하고 실행합니다.

### <a name="BKMK_BuildingTheApp"></a> 앱 빌드

다음 섹션에서는 예제를 WPF 앱으로 빌드하는 코드를 제공합니다.

##### <a name="to-build-a-wpf-app"></a>WPF 응용 프로그램을 빌드하려면

1. Visual Studio를 시작합니다.

2. 메뉴 모음에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.

     **새 프로젝트** 대화 상자가 열립니다.

3. **설치 된 템플릿** 창에서 **Visual Basic**을 확장 한 다음 **Windows**를 확장 합니다.

4. 프로젝트 형식 목록에서 **WPF 애플리케이션**을 선택합니다.

5. 프로젝트 이름을 `WebsiteDownloadWPF`로 지정한 다음 **확인**을 선택합니다.

     **솔루션 탐색기**에 새 프로젝트가 표시됩니다.

6. Visual Studio 코드 편집기에서 **MainWindow.xaml** 탭을 선택합니다.

     탭이 표시되지 않는 경우 **솔루션 탐색기**에서 MainWindow.xaml의 바로 가기 메뉴를 열고 **코드 보기**를 선택합니다.

7. MainWindow.xaml의 **XAML** 보기에서 코드를 다음 코드로 바꿉니다.

    ```xaml
    <Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:WebsiteDownloadWPF"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Width="517" Height="360">
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="-1,0,0,0" VerticalAlignment="Top" Click="StartButton_Click" Height="53" Background="#FFA89B9B" FontSize="36" Width="518"  />
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" Margin="-1,53,0,-36" TextWrapping="Wrap" VerticalAlignment="Top" Height="343" FontSize="10" ScrollViewer.VerticalScrollBarVisibility="Visible" Width="518" FontFamily="Lucida Console" />
        </Grid>
    </Window>
    ```

     텍스트 상자와 버튼이 포함된 간단한 창이 MainWindow.xaml의 **디자인** 보기에 나타납니다.

8. <xref:System.Net.Http>에 대한 참조를 추가합니다.

9. **솔루션 탐색기**에서 mainwindow.xaml의 바로 가기 메뉴를 열고 **코드 보기**를 선택 합니다.

10. Mainwindow.xaml에서 코드를 다음 코드로 바꿉니다.

    ```vb
    ' Add the following Imports statements, and add a reference for System.Net.Http.
    Imports System.Net.Http
    Imports System.Threading

    Class MainWindow

        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)
            ' This line is commented out to make the results clearer in the output.
            'ResultsTextBox.Text = ""

            Try
                Await AccessTheWebAsync()

            Catch ex As Exception
                ResultsTextBox.Text &= vbCrLf & "Downloads failed."

            End Try
        End Sub

        Private Async Function AccessTheWebAsync() As Task

            ' Declare an HttpClient object.
            Dim client = New HttpClient()

            ' Make a list of web addresses.
            Dim urlList As List(Of String) = SetUpURLList()

            Dim total = 0
            Dim position = 0

            For Each url In urlList
                ' GetByteArrayAsync returns a task. At completion, the task
                ' produces a byte array.
                Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)

                position += 1
                DisplayResults(url, urlContents, position)

                ' Update the total.
                total += urlContents.Length
            Next

            ' Display the total count for all of the websites.
            ResultsTextBox.Text &=
                String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)
        End Function

        Private Function SetUpURLList() As List(Of String)
            Dim urls = New List(Of String) From
            {
                "https://msdn.microsoft.com/library/hh191443.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/jj155761.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/hh524395.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            }
            Return urls
        End Function

        Private Sub DisplayResults(url As String, content As Byte(), pos As Integer)
            ' Display the length of each website. The string format is designed
            ' to be used with a monospaced font, such as Lucida Console or
            ' Global Monospace.

            ' Strip off the "http:'".
            Dim displayURL = url.Replace("https://", "")
            ' Display position in the URL list, the URL, and the number of bytes.
            ResultsTextBox.Text &= String.Format(vbCrLf & "{0}. {1,-58} {2,8}", pos, displayURL, content.Length)
        End Sub
    End Class
    ```

11. CTRL+F5 키를 선택하여 프로그램을 실행한 다음 **시작** 버튼을 여러 번 선택합니다.

12. [시작 버튼 사용 안 함](#BKMK_DisableTheStartButton), [작업 취소 및 다시 시작](#BKMK_CancelAndRestart) 또는 [여러 작업을 실행하고 출력을 큐 대기](#BKMK_RunMultipleOperations)의 내용을 변경하여 재진입을 처리합니다.

## <a name="see-also"></a>참조

- [연습: Async 및 Wait (Visual Basic)를 사용 하 여 웹에 액세스](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
