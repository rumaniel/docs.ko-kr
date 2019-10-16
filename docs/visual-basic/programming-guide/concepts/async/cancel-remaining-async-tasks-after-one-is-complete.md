---
title: 하나가 (Visual Basic) 완료 되 면 남은 비동기 작업 취소
ms.date: 07/20/2015
ms.assetid: c928b5a1-622f-4441-8baf-adca1dde197f
ms.openlocfilehash: 587c863ba110f035ace5207d8404fd70b3befe37
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64755824"
---
# <a name="cancel-remaining-async-tasks-after-one-is-complete-visual-basic"></a>하나가 (Visual Basic) 완료 되 면 남은 비동기 작업 취소

<xref:System.Threading.CancellationToken>과 함께 <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 메서드를 사용하면 한 작업이 완료될 때 나머지 작업을 모두 취소할 수 있습니다. `WhenAny` 메서드는 작업의 컬렉션인 인수를 사용합니다. 메서드는 모든 작업을 시작하고 단일 작업을 반환합니다. 컬렉션의 임의 작업이 완료되면 단일 작업이 완료됩니다.

이 예제에서는 취소 토큰을 `WhenAny`와 함께 사용하여 작업 컬렉션에서 완료될 첫 번째 작업을 유지하고 나머지 작업을 취소하는 방법을 보여 줍니다. 각 작업은 웹 사이트의 콘텐츠를 다운로드합니다. 예제에서는 완료할 첫 번째 다운로드의 콘텐츠 길이를 표시하고 기타 다운로드를 취소합니다.

> [!NOTE]
> 예제를 실행하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치되어 있어야 합니다.

## <a name="downloading-the-example"></a>예제 다운로드

[Async 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 WPF(Windows Presentation Foundation) 프로젝트를 다운로드한 후, 다음 단계를 수행합니다.

1. 다운로드한 파일의 압축을 푼 다음 Visual Studio를 시작합니다.

2. 메뉴 모음에서 **파일**, **열기**, **프로젝트/솔루션**을 선택합니다.

3. **프로젝트 열기** 대화 상자에서 압축을 해제한 샘플 코드가 포함된 폴더를 열고 AsyncFineTuningVB에 대한 솔루션(.sln) 파일을 엽니다.

4. **솔루션 탐색기**에서 **CancelAfterOneTask** 프로젝트에 대한 바로 가기 메뉴를 열고 **시작 프로젝트로 설정**을 선택합니다.

5. F5 키를 선택하여 프로젝트를 실행합니다.

    디버그하지 않고 프로젝트를 실행하려면 Ctrl+F5를 선택합니다.

6. 프로그램을 여러 번 실행하여 다른 다운로드가 먼저 완료되는지 확인합니다.

프로젝트를 다운로드하지 않으려는 경우 이 항목의 끝에 있는 MainWindow.xaml.vb 파일을 검토할 수 있습니다.

## <a name="building-the-example"></a>예제 빌드

이 항목의 예제에서 개발 된 프로젝트에 추가 [비동기 작업 또는 작업 목록 취소](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md) 작업 목록을 취소 합니다. **취소** 단추는 명시적으로 사용되지 않지만 예제에서는 같은 UI를 사용합니다.

직접 예제를 빌드하려면 "예제 다운로드" 섹션의 지침을 단계별로 따르되, **CancelAListOfTasks**를 **시작 프로젝트**로 선택합니다. 이 항목의 변경 내용을 해당 프로젝트에 추가합니다.

MainWindow.xaml.vb 파일에는 **CancelAListOfTasks** 프로젝트를에서 루프의 각 웹 사이트에 대 한 처리 단계를 이동 하 여 전환을 시작 `AccessTheWebAsync` 다음 비동기 메서드로 합니다.

```vb
' ***Bundle the processing steps for a website into one async method.
Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)

    ' GetAsync returns a Task(Of HttpResponseMessage).
    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)

    ' Retrieve the website contents from the HttpResponseMessage.
    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

    Return urlContents.Length
End Function
```

`AccessTheWebAsync`에서 이 예제는 쿼리, <xref:System.Linq.Enumerable.ToArray%2A> 메서드 및 `WhenAny` 메서드를 사용하여 작업 배열을 만들고 시작합니다. 배열에 `WhenAny`를 적용하면 대기할 때 작업 배열에서 완료에 도달할 첫 번째 작업으로 계산되는 단일 작업이 반환됩니다.

`AccessTheWebAsync`에서 다음과 같이 변경합니다. 코드 파일에서 변경 내용에는 별표가 표시됩니다.

1. 루프를 주석으로 처리하거나 삭제합니다.

2. 실행될 때 제네릭 작업의 컬렉션을 생성하는 쿼리를 만듭니다. `ProcessURLAsync`를 호출할 때마다 <xref:System.Threading.Tasks.Task%601>가 반환됩니다. 여기서 `TResult`는 정수입니다.

    ```vb
    ' ***Create a query that, when executed, returns a collection of tasks.
    Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =
        From url In urlList Select ProcessURLAsync(url, client, ct)
    ```

3. `ToArray`를 호출하여 쿼리를 실행하고 작업을 시작합니다. 다음 단계에서 `WhenAny` 메서드를 적용하면 `ToArray`를 사용하지 않고 쿼리가 실행되고 작업이 시작되지만 다른 메서드는 시작되지 않을 수 있습니다. 가장 안전한 방법은 쿼리를 명시적으로 강제 실행하는 것입니다.

    ```vb
    ' ***Use ToArray to execute the query and start the download tasks.
    Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()
    ```

4. 작업 컬렉션에서 `WhenAny`를 호출합니다. `WhenAny`는 `Task(Of Task(Of Integer))` 또는 `Task<Task<int>>`를 반환합니다.  즉, `WhenAny`는 대기 시 단일 `Task(Of Integer)` 또는 `Task<int>`로 계산되는 작업을 반환합니다. 이 단일 작업은 컬렉션에서 완료될 첫 번째 작업입니다. 첫 번째로 완료된 작업은 `firstFinishedTask`에 할당됩니다. `firstFinishedTask`의 형식은 <xref:System.Threading.Tasks.Task%601>입니다. 여기서 `TResult`는 `ProcessURLAsync`의 반환 형식이므로 정수입니다.

    ```vb
    ' ***Call WhenAny and then await the result. The task that finishes
    ' first is assigned to firstFinishedTask.
    Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)
    ```

5. 이 예제에서는 첫 번째로 완료되는 작업에만 초점을 맞춥니다. 따라서 <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=nameWithType>을 사용하여 나머지 작업을 취소합니다.

    ```vb
    ' ***Cancel the rest of the downloads. You just want the first one.
    cts.Cancel()
    ```

6. 마지막으로 다운로드된 콘텐츠의 길이를 검색할 때까지 `firstFinishedTask`를 대기하게 합니다.

    ```vb
    Dim length = Await firstFinishedTask
    resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)
    ```

프로그램을 여러 번 실행하여 다른 다운로드가 먼저 완료되는지 확인합니다.

## <a name="complete-example"></a>완성된 예제

다음 코드는 예제의 전체 MainWindow.xaml.vb 또는 MainWindow.xaml.cs 파일입니다. 별표는 이 예제에 대해 추가된 요소를 표시합니다.

<xref:System.Net.Http>에 대한 참조를 추가해야 합니다.

[비동기 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 프로젝트를 다운로드할 수 있습니다.

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
            Await AccessTheWebAsync(cts.Token)
            resultsTextBox.Text &= vbCrLf & "Download complete."

        Catch ex As OperationCanceledException
            resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf

        Catch ex As Exception
            resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf
        End Try

        ' Set the CancellationTokenSource to Nothing when the download is complete.
        cts = Nothing
    End Sub

    ' You can still include a Cancel button if you want to.
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)

        If cts IsNot Nothing Then
            cts.Cancel()
        End If
    End Sub

    ' Provide a parameter for the CancellationToken.
    ' Change the return type to Task because the method has no return statement.
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task

        Dim client As HttpClient = New HttpClient()

        ' Call SetUpURLList to make a list of web addresses.
        Dim urlList As List(Of String) = SetUpURLList()

        '' Comment out or delete the loop.
        ''For Each url In urlList
        ''    ' GetAsync returns a Task(Of HttpResponseMessage).
        ''    ' Argument ct carries the message if the Cancel button is chosen.
        ''    ' Note that the Cancel button can cancel all remaining downloads.
        ''    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)

        ''    ' Retrieve the website contents from the HttpResponseMessage.
        ''    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

        ''    resultsTextBox.Text &=
        ''        String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)
        ''Next

        ' ***Create a query that, when executed, returns a collection of tasks.
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =
            From url In urlList Select ProcessURLAsync(url, client, ct)

        ' ***Use ToArray to execute the query and start the download tasks.
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()

        ' ***Call WhenAny and then await the result. The task that finishes
        ' first is assigned to firstFinishedTask.
        Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)

        ' ***Cancel the rest of the downloads. You just want the first one.
        cts.Cancel()

        ' ***Await the first completed task and display the results
        ' Run the program several times to demonstrate that different
        ' websites can finish first.
        Dim length = Await firstFinishedTask
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)
    End Function

    ' ***Bundle the processing steps for a website into one async method.
    Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)

        ' GetAsync returns a Task(Of HttpResponseMessage).
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)

        ' Retrieve the website contents from the HttpResponseMessage.
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

        Return urlContents.Length
    End Function

    ' Add a method that creates a list of web addresses.
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

' Sample output:

' Length of the downloaded website:  158856

' Download complete.
```

## <a name="see-also"></a>참고자료

- <xref:System.Threading.Tasks.Task.WhenAny%2A>
- [Async 응용 프로그램 미세 조정(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)
- [Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
- [비동기 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)
