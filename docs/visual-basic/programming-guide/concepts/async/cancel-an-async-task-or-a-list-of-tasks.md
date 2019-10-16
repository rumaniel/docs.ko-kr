---
title: 비동기 작업 또는 작업 목록 취소 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: a9ee1b71-5bec-4736-a1e9-448042dd7215
ms.openlocfilehash: 73627455b1f4460edfe165126a388e961e98921f
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353134"
---
# <a name="cancel-an-async-task-or-a-list-of-tasks-visual-basic"></a>비동기 작업 또는 작업 목록 취소 (Visual Basic)

작업이 완료될 때까지 기다리지 않으려면 비동기 애플리케이션을 취소할 때 사용하는 단추를 설정할 수 있습니다. 이 항목의 예제에 따라 한 웹 사이트 또는 웹 사이트 목록의 콘텐츠를 다운로드하는 애플리케이션에 취소 단추를 추가할 수 있습니다.

이 예제에서는 [비동기 응용 프로그램 (Visual Basic)을 미세 조정](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md) 하는 UI를 사용 합니다.

> [!NOTE]
> 예제를 실행하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치되어 있어야 합니다.

## <a name="BKMK_CancelaTask"></a> 작업 취소

첫 번째 예제에서는 **취소** 단추를 단일 다운로드 작업에 연결합니다. 애플리케이션이 콘텐츠를 다운로드하는 동안 단추를 선택하면 다운로드가 취소됩니다.

### <a name="downloading-the-example"></a>예제 다운로드

[Async 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 WPF(Windows Presentation Foundation) 프로젝트를 다운로드한 후, 다음 단계를 수행합니다.

1. 다운로드한 파일의 압축을 푼 다음 Visual Studio를 시작합니다.

2. 메뉴 모음에서 **파일**, **열기**, **프로젝트/솔루션**을 선택합니다.

3. **프로젝트 열기** 대화 상자에서 압축을 해제한 샘플 코드가 포함된 폴더를 열고 AsyncFineTuningVB에 대한 솔루션(.sln) 파일을 엽니다.

4. **솔루션 탐색기**에서 **CancelATask** 프로젝트에 대한 바로 가기 메뉴를 열고 **시작 프로젝트로 설정**을 선택합니다.

5. F5 키를 선택하여 프로젝트를 실행합니다.

     디버그하지 않고 프로젝트를 실행하려면 Ctrl+F5를 선택합니다.

 프로젝트를 다운로드 하지 않으려는 경우이 항목의 끝에 있는 Mainwindow.xaml 파일을 검토할 수 있습니다.

### <a name="building-the-example"></a>예제 빌드

다음 변경 내용은 웹 사이트를 다운로드하는 애플리케이션에 **취소** 단추를 추가합니다. 예제를 다운로드하거나 빌드하지 않으려면 이 항목의 끝에 있는 “전체 예제” 섹션에서 최종 결과를 검토할 수 있습니다. 코드에서 변경 내용에는 별표가 표시됩니다.

직접 예제를 빌드하려면 "예제 다운로드" 섹션의 지침을 단계별로 따르지만 **시작 프로젝트**로 **CancelATask** 대신 **StarterCode**를 선택합니다.

그런 다음, 해당 프로젝트의 Mainwindow.xaml 파일에 다음 변경 내용을 추가 합니다.

1. 액세스하는 모든 메서드에 대한 범위 내에 있는 `CancellationTokenSource` 변수 `cts`를 선언합니다.

    ```vb
    Class MainWindow

        ' ***Declare a System.Threading.CancellationTokenSource.
        Dim cts As CancellationTokenSource
    ```

2. **취소** 단추에 대한 다음 이벤트 처리기를 추가합니다. 이벤트 처리기는 <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=nameWithType> 메서드를 사용하여 사용자가 취소를 요청할 때 `cts`에 알려줍니다.

    ```vb
    ' ***Add an event handler for the Cancel button.
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)

        If cts IsNot Nothing Then
            cts.Cancel()
        End If
    End Sub
    ```

3. 이벤트 처리기에서 **시작** 단추 `startButton_Click`을 다음과 같이 변경합니다.

    - `CancellationTokenSource`, `cts`를 인스턴스화합니다.

      ```vb
      ' ***Instantiate the CancellationTokenSource.
      cts = New CancellationTokenSource()
      ```

    - 지정된 웹 사이트의 콘텐츠를 다운로드하는 `AccessTheWebAsync` 호출에서 `cts`의 <xref:System.Threading.CancellationTokenSource.Token%2A?displayProperty=nameWithType> 속성을 인수로 전송합니다. 취소가 요청되면 `Token` 속성은 메시지를 전파합니다. 사용자가 다운로드 작업을 취소하도록 선택할 경우 메시지를 표시하는 catch 블록을 추가합니다. 다음 코드는 변경 내용을 보여 줍니다.

      ```vb
      Try
          ' ***Send a token to carry the message if cancellation is requested.
          Dim contentLength As Integer = Await AccessTheWebAsync(cts.Token)

          resultsTextBox.Text &=
              String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)

          ' *** If cancellation is requested, an OperationCanceledException results.
      Catch ex As OperationCanceledException
          resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf

      Catch ex As Exception
          resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf
      End Try
      ```

4. `AccessTheWebAsync`에서 <xref:System.Net.Http.HttpClient> 형식에 있는 `GetAsync` 메서드의 <xref:System.Net.Http.HttpClient.GetAsync%28System.String%2CSystem.Threading.CancellationToken%29?displayProperty=nameWithType> 오버로드를 사용하여 웹 사이트의 콘텐츠를 다운로드합니다. `AccessTheWebAsync`의 <xref:System.Threading.CancellationToken> 매개 변수인 `ct`를 두 번째 인수로 전달합니다. 사용자가 **취소** 단추를 선택하면 토큰이 메시지를 전달합니다.

    다음 코드는 `AccessTheWebAsync`의 변경 내용을 보여 줍니다.

    ```vb
    ' ***Provide a parameter for the CancellationToken.
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task(Of Integer)

        Dim client As HttpClient = New HttpClient()

        resultsTextBox.Text &=
            String.Format(vbCrLf & "Ready to download." & vbCrLf)

        ' You might need to slow things down to have a chance to cancel.
        Await Task.Delay(250)

        ' GetAsync returns a Task(Of HttpResponseMessage).
        ' ***The ct argument carries the message if the Cancel button is chosen.
        Dim response As HttpResponseMessage = Await client.GetAsync("https://msdn.microsoft.com/library/dd470362.aspx", ct)

        ' Retrieve the website contents from the HttpResponseMessage.
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

        ' The result of the method is the length of the downloaded website.
        Return urlContents.Length
    End Function
    ```

5. 프로그램을 취소 하지 않으면 다음과 같은 출력이 생성 됩니다.

    ```console
    Ready to download.
    Length of the downloaded string: 158125.
    ```

    프로그램이 콘텐츠 다운로드를 완료 하기 전에 **취소** 단추를 선택 하면 프로그램에서 다음과 같은 출력을 생성 합니다.

    ```console
    Ready to download.
    Download canceled.
    ```

## <a name="BKMK_CancelaListofTasks"></a> 작업 목록 취소

이전 예제를 확장하여 같은 `CancellationTokenSource` 인스턴스를 각 작업과 연결하는 방식으로 여러 작업을 취소할 수 있습니다. **취소** 단추를 선택하면 아직 완료되지 않은 모든 작업이 취소됩니다.

### <a name="downloading-the-example"></a>예제 다운로드

[Async 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 WPF(Windows Presentation Foundation) 프로젝트를 다운로드한 후, 다음 단계를 수행합니다.

1. 다운로드한 파일의 압축을 푼 다음 Visual Studio를 시작합니다.

2. 메뉴 모음에서 **파일**, **열기**, **프로젝트/솔루션**을 선택합니다.

3. **프로젝트 열기** 대화 상자에서 압축을 해제한 샘플 코드가 포함된 폴더를 열고 AsyncFineTuningVB에 대한 솔루션(.sln) 파일을 엽니다.

4. **솔루션 탐색기**에서 **CancelAListOfTasks** 프로젝트에 대한 바로 가기 메뉴를 열고 **시작 프로젝트로 설정**을 선택합니다.

5. F5 키를 선택하여 프로젝트를 실행합니다.

     디버그하지 않고 프로젝트를 실행하려면 Ctrl+F5를 선택합니다.

 프로젝트를 다운로드 하지 않으려는 경우이 항목의 끝에 있는 Mainwindow.xaml 파일을 검토할 수 있습니다.

### <a name="building-the-example"></a>예제 빌드

직접 예제를 확장하려면 "예제 다운로드" 섹션의 지침을 단계별로 따르되, **CancelATask**를 **시작 프로젝트**로 선택합니다. 해당 프로젝트에 다음 변경 내용을 추가합니다. 프로그램에서 변경 내용에는 별표가 표시됩니다.

1. 웹 주소 목록에 메서드를 추가합니다.

    ```vb
    ' ***Add a method that creates a list of web addresses.
    Private Function SetUpURLList() As List(Of String)

        Dim urls = New List(Of String) From
            {
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            }
        Return urls
    End Function
    ```

2. `AccessTheWebAsync`에서 메서드를 호출합니다.

    ```vb
    ' ***Call SetUpURLList to make a list of web addresses.
    Dim urlList As List(Of String) = SetUpURLList()
    ```

3. `AccessTheWebAsync`에서 다음 루프를 추가하여 목록에 있는 각 웹 주소를 처리합니다.

    ```vb
    ' ***Add a loop to process the list of web addresses.
    For Each url In urlList
        ' GetAsync returns a Task(Of HttpResponseMessage).
        ' Argument ct carries the message if the Cancel button is chosen.
        ' ***Note that the Cancel button can cancel all remaining downloads.
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)

        ' Retrieve the website contents from the HttpResponseMessage.
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

        resultsTextBox.Text &=
            String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)
    Next
    ```

4. `AccessTheWebAsync`는 길이를 표시하므로 메서드가 아무것도 반환할 필요가 없습니다. return 문을 제거하고 메서드의 반환 형식을 <xref:System.Threading.Tasks.Task%601> 대신 <xref:System.Threading.Tasks.Task>로 변경합니다.

    ```vb
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task
    ```

    식 대신 문을 사용하여 `startButton_Click`에서 메서드를 호출합니다.

    ```vb
    Await AccessTheWebAsync(cts.Token)
    ```

5. 프로그램을 취소 하지 않으면 다음과 같은 출력이 생성 됩니다.

    ```console
    Length of the downloaded string: 35939.

    Length of the downloaded string: 237682.

    Length of the downloaded string: 128607.

    Length of the downloaded string: 158124.

    Length of the downloaded string: 204890.

    Length of the downloaded string: 175488.

    Length of the downloaded string: 145790.

    Downloads complete.
    ```

    다운로드가 완료되기 전에 **취소** 단추를 선택하면 취소하기 전에 완료된 다운로드의 길이가 출력에 포함됩니다.

    ```console
    Length of the downloaded string: 35939.

    Length of the downloaded string: 237682.

    Length of the downloaded string: 128607.

    Downloads canceled.
    ```

## <a name="BKMK_CompleteExamples"></a> 전체 예제

다음 섹션에는 각각의 이전 예제에 대한 코드가 있습니다. <xref:System.Net.Http>에 대한 참조를 추가해야 합니다.

[비동기 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 프로젝트를 다운로드할 수 있습니다.

### <a name="cancel-a-task-example"></a>작업 취소 예제

다음 코드는 단일 작업을 취소 하는 예제에 대 한 전체 Mainwindow.xaml 파일입니다.

```vb
' Add an Imports directive and a reference for System.Net.Http.
Imports System.Net.Http

' Add the following Imports directive for System.Threading.
Imports System.Threading

Class MainWindow

    ' ***Declare a System.Threading.CancellationTokenSource.
    Dim cts As CancellationTokenSource

    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)
        ' ***Instantiate the CancellationTokenSource.
        cts = New CancellationTokenSource()

        resultsTextBox.Clear()

        Try
            ' ***Send a token to carry the message if cancellation is requested.
            Dim contentLength As Integer = Await AccessTheWebAsync(cts.Token)

            resultsTextBox.Text &=
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)

            ' *** If cancellation is requested, an OperationCanceledException results.
        Catch ex As OperationCanceledException
            resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf

        Catch ex As Exception
            resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf
        End Try

        ' ***Set the CancellationTokenSource to Nothing when the download is complete.
        cts = Nothing
    End Sub

    ' ***Add an event handler for the Cancel button.
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)

        If cts IsNot Nothing Then
            cts.Cancel()
        End If
    End Sub

    ' ***Provide a parameter for the CancellationToken.
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task(Of Integer)

        Dim client As HttpClient = New HttpClient()

        resultsTextBox.Text &=
            String.Format(vbCrLf & "Ready to download." & vbCrLf)

        ' You might need to slow things down to have a chance to cancel.
        Await Task.Delay(250)

        ' GetAsync returns a Task(Of HttpResponseMessage).
        ' ***The ct argument carries the message if the Cancel button is chosen.
        Dim response As HttpResponseMessage = Await client.GetAsync("https://msdn.microsoft.com/library/dd470362.aspx", ct)

        ' Retrieve the website contents from the HttpResponseMessage.
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

        ' The result of the method is the length of the downloaded website.
        Return urlContents.Length
    End Function
End Class

' Output for a successful download:

' Ready to download.

' Length of the downloaded string: 158125.

' Or, if you cancel:

' Ready to download.

' Download canceled.
```

### <a name="cancel-a-list-of-tasks-example"></a>작업 목록 취소 예제

다음 코드는 작업 목록을 취소 하는 예제에 대 한 전체 Mainwindow.xaml 파일입니다.

```vb
' Add an Imports directive and a reference for System.Net.Http.
Imports System.Net.Http

' Add the following Imports directive for System.Threading.
Imports System.Threading

Class MainWindow

    ' Declare a System.Threading.CancellationTokenSource.
    Dim cts As CancellationTokenSource

    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)

        ' Instantiate the CancellationTokenSource.
        cts = New CancellationTokenSource()

        resultsTextBox.Clear()

        Try
            ' ***AccessTheWebAsync returns a Task, not a Task(Of Integer).
            Await AccessTheWebAsync(cts.Token)
            '  ***Small change in the display lines.
            resultsTextBox.Text &= vbCrLf & "Downloads complete."

        Catch ex As OperationCanceledException
            resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf

        Catch ex As Exception
            resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf
        End Try

        ' Set the CancellationTokenSource to Nothing when the download is complete.
        cts = Nothing
    End Sub

    ' Add an event handler for the Cancel button.
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)

        If cts IsNot Nothing Then
            cts.Cancel()
        End If
    End Sub

    ' Provide a parameter for the CancellationToken.
    ' ***Change the return type to Task because the method has no return statement.
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task

        Dim client As HttpClient = New HttpClient()

        ' ***Call SetUpURLList to make a list of web addresses.
        Dim urlList As List(Of String) = SetUpURLList()

        ' ***Add a loop to process the list of web addresses.
        For Each url In urlList
            ' GetAsync returns a Task(Of HttpResponseMessage).
            ' Argument ct carries the message if the Cancel button is chosen.
            ' ***Note that the Cancel button can cancel all remaining downloads.
            Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)

            ' Retrieve the website contents from the HttpResponseMessage.
            Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

            resultsTextBox.Text &=
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)
        Next
    End Function

    ' ***Add a method that creates a list of web addresses.
    Private Function SetUpURLList() As List(Of String)

        Dim urls = New List(Of String) From
            {
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            }
        Return urls
    End Function

End Class

' Output if you do not choose to cancel:

' Length of the downloaded string: 35939.

' Length of the downloaded string: 237682.

' Length of the downloaded string: 128607.

' Length of the downloaded string: 158124.

' Length of the downloaded string: 204890.

' Length of the downloaded string: 175488.

' Length of the downloaded string: 145790.

' Downloads complete.

'  Sample output if you choose to cancel:

' Length of the downloaded string: 35939.

' Length of the downloaded string: 237682.

' Length of the downloaded string: 128607.

' Downloads canceled.
```

## <a name="see-also"></a>참조

- <xref:System.Threading.CancellationTokenSource>
- <xref:System.Threading.CancellationToken>
- [Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
- [Async 애플리케이션 미세 조정(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)
- [비동기 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)
