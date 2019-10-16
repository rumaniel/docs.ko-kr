---
title: 비동기 작업을 여러 개 시작 하 고 완료 될 때마다 처리 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 57ffb748-af40-4794-bedd-bdb7fea062de
ms.openlocfilehash: b103f385c804061c4df99dc9d1fdd54c7876151a
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928464"
---
# <a name="start-multiple-async-tasks-and-process-them-as-they-complete-visual-basic"></a>비동기 작업을 여러 개 시작 하 고 완료 될 때마다 처리 (Visual Basic)
<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType>를 사용하면 시작된 순서대로 처리하는 대신 동시에 여러 작업을 시작하고 완료 시 하나씩 처리할 수 있습니다.  
  
 다음 예제에서는 쿼리를 사용하여 작업 컬렉션을 만듭니다. 각 작업은 지정된 웹 사이트의 콘텐츠를 다운로드합니다. while 루프의 각 반복에서 대기된 `WhenAny` 호출은 다운로드를 먼저 완료하는 작업 컬렉션의 작업을 반환합니다. 해당 작업은 컬렉션에서 제거되고 처리됩니다. 컬렉션에 더 이상 작업이 없을 때까지 루프가 반복됩니다.  
  
> [!NOTE]
> 예제를 실행하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치되어 있어야 합니다.  
  
## <a name="downloading-the-example"></a>예제 다운로드  
 [Async 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 WPF(Windows Presentation Foundation) 프로젝트를 다운로드한 후, 다음 단계를 수행합니다.  
  
1. 다운로드한 파일의 압축을 푼 다음 Visual Studio를 시작합니다.  
  
2. 메뉴 모음에서 **파일**, **열기**, **프로젝트/솔루션**을 선택합니다.  
  
3. **프로젝트 열기** 대화 상자에서 압축을 해제한 샘플 코드가 포함된 폴더를 열고 AsyncFineTuningVB에 대한 솔루션(.sln) 파일을 엽니다.  
  
4. **솔루션 탐색기**에서 **ProcessTasksAsTheyFinish** 프로젝트에 대한 바로 가기 메뉴를 열고 **시작 프로젝트로 설정**을 선택합니다.  
  
5. F5 키를 선택하여 프로젝트를 실행합니다.  
  
     디버그하지 않고 프로젝트를 실행하려면 Ctrl+F5를 선택합니다.  
  
6. 프로젝트를 여러 번 실행하여 다운로드한 길이가 항상 같은 순서로 표시되는지 확인합니다.  
  
 프로젝트를 다운로드하지 않으려는 경우 이 항목의 끝에 있는 MainWindow.xaml.vb 파일을 검토할 수 있습니다.  
  
## <a name="building-the-example"></a>예제 빌드  
 이 예제에서는 [작업 하나가 완료 된 후 남은 비동기 작업 취소 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md) 에서 개발 된 코드에를 추가 하 고 동일한 UI를 사용 합니다.  
  
 직접 예제를 빌드하려면 "예제 다운로드" 섹션의 지침을 단계별로 따르되, **CancelAfterOneTask**를 **시작 프로젝트**로 선택합니다. 이 항목의 변경 내용을 해당 프로젝트의 `AccessTheWebAsync` 메서드에 추가합니다. 변경 내용은 별표로 표시됩니다.  
  
 **CancelAfterOneTask** 프로젝트에는 실행 시 작업 컬렉션을 만드는 쿼리가 이미 포함되어 있습니다. 다음 코드에서는 `ProcessURLAsync`를 호출할 때마다 <xref:System.Threading.Tasks.Task%601>가 반환됩니다. 여기서 `TResult`는 정수입니다.  
  
```vb  
Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
    From url In urlList Select ProcessURLAsync(url, client, ct)  
```  
  
 프로젝트의 mainwindow.xaml 파일에서 `AccessTheWebAsync` 메서드를 다음과 같이 변경 합니다.  
  
- <xref:System.Linq.Enumerable.ToArray%2A> 대신 <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType>를 적용하여 쿼리를 실행합니다.  
  
    ```vb  
    Dim downloadTasks As List(Of Task(Of Integer)) = downloadTasksQuery.ToList()  
    ```  
  
- 컬렉션의 각 작업에 대해 다음 단계를 수행하는 while 루프를 추가합니다.  
  
    1. 컬렉션의 첫 번째 작업을 식별하여 다운로드를 완료하기 위해 `WhenAny` 호출을 대기합니다.  
  
        ```vb  
        Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
        ```  
  
    2. 컬렉션에서 해당 작업을 제거합니다.  
  
        ```vb  
        downloadTasks.Remove(firstFinishedTask)  
        ```  
  
    3. `ProcessURLAsync` 호출에서 반환된 `firstFinishedTask`를 대기합니다. `firstFinishedTask` 변수는 <xref:System.Threading.Tasks.Task%601>입니다. 여기서 `TReturn`은 정수입니다. 작업은 이미 완료되었지만, 다음 예제와 같이 다운로드한 웹 사이트의 길이를 검색하도록 기다립니다.  
  
        ```vb  
        Dim length = Await firstFinishedTask  
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        ```  
  
 프로젝트를 여러 번 실행하여 다운로드한 길이가 항상 같은 순서로 표시되는지 확인해야 합니다.  
  
> [!CAUTION]
> 예제에 설명된 대로 루프에서 `WhenAny`를 사용하는 것은 적은 수의 작업이 필요한 문제 해결에 적합합니다. 그러므로 많은 수의 작업을 처리해야 하는 경우에는 다른 접근 방법이 더 효율적입니다. 자세한 내용 및 예제는 [작업이 완료되었을 때 처리 방법](https://devblogs.microsoft.com/pfxteam/processing-tasks-as-they-complete/)을 참조하세요.  
  
## <a name="complete-example"></a>완성된 예제  
 다음 코드는 예제에 대한 MainWindow.xaml.vb 파일의 전체 텍스트입니다. 별표는 이 예제에 대해 추가된 요소를 표시합니다.  
  
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
            resultsTextBox.Text &= vbCrLf & "Downloads complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf  
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
  
        ' ***Create a query that, when executed, returns a collection of tasks.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client, ct)  
  
        ' ***Use ToList to execute the query and start the download tasks.   
        Dim downloadTasks As List(Of Task(Of Integer)) = downloadTasksQuery.ToList()  
  
        ' ***Add a loop to process the tasks one at a time until none remain.  
        While downloadTasks.Count > 0  
            ' ***Identify the first task that completes.  
            Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
  
            ' ***Remove the selected task from the list so that you don't  
            ' process it more than once.  
            downloadTasks.Remove(firstFinishedTask)  
  
            ' ***Await the first completed task and display the results.  
            Dim length = Await firstFinishedTask  
            resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        End While  
  
    End Function  
  
    ' Bundle the processing steps for a website into one async method.  
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
  
' Length of the download:  226093  
' Length of the download:  412588  
' Length of the download:  175490  
' Length of the download:  204890  
' Length of the download:  158855  
' Length of the download:  145790  
' Length of the download:  44908  
' Downloads complete.  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Threading.Tasks.Task.WhenAny%2A>
- [Async 응용 프로그램 미세 조정(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)
- [Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
- [비동기 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)
