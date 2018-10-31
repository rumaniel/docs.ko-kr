---
title: '방법: Task.WhenAll을 사용하여 비동기 연습 확장(C#)'
ms.date: 07/20/2015
ms.assetid: f6927ef2-dc6c-43f8-bc82-bbeac42de423
ms.openlocfilehash: e809ea3c2b2bcc0f547dd53280835a83f52e079b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188042"
---
# <a name="how-to-extend-the-async-walkthrough-by-using-taskwhenall-c"></a>방법: Task.WhenAll을 사용하여 비동기 연습 확장(C#)
<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 메서드를 사용하여 [연습: async 및 await를 사용하여 웹에 액세스(C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)에서 비동기 솔루션의 성능을 향상할 수 있습니다. 이 메서드는 작업 컬렉션으로 표시되는 여러 개의 비동기 작업을 비동기적으로 기다립니다.  
  
 연습에서 웹 사이트 다운로드 속도가 각기 다른 것을 보셨을 것입니다. 때로는 웹 사이트 중 하나가 매우 느려 나머지 다운로드가 모두 지연됩니다. 연습에서 빌드하는 비동기 솔루션을 실행하는 경우 대기하지 않으려면 프로그램을 쉽게 종료할 수 있지만, 동시에 모든 다운로드를 시작한 후 더 빠른 다운로드는 지연되는 다운로드를 기다리지 않고 계속되도록 하는 것이 더 낫습니다.  
  
 작업 컬렉션에 `Task.WhenAll` 메서드를 적용합니다. `WhenAll` 응용 프로그램은 컬렉션의 모든 작업이 완료될 때까지 완료되지 않는 단일 작업을 반환합니다. 작업이 병렬로 실행되는 것처럼 보이지만 추가 스레드는 생성되지 않습니다. 작업이 임의 순서로 완료될 수 있습니다.  
  
> [!IMPORTANT]
>  다음 절차에서는 [연습: async 및 await를 사용하여 웹에 액세스(C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)에서 개발된 비동기 응용 프로그램에 대한 확장을 설명합니다. 연습을 완료하거나 [개발자 코드 샘플](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)에서 코드를 다운로드하여 응용 프로그램을 개발할 수 있습니다.  
>   
>  예제를 실행하려면 Visual Studio 2012 이상이 컴퓨터에 설치되어 있어야 합니다.  
  
### <a name="to-add-taskwhenall-to-your-geturlcontentsasync-solution"></a>GetURLContentsAsync 솔루션에 Task.WhenAll을 추가하려면  
  
1.  [연습: async 및 await를 사용하여 웹에 액세스(C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)에서 개발된 첫 번째 응용 프로그램에 `ProcessURLAsync` 메서드를 추가합니다.  
  
    -   [개발자 코드 샘플](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)에서 코드를 다운로드한 경우 AsyncWalkthrough 프로젝트를 열고 MainWindow.xaml.cs 파일에 `ProcessURLAsync`를 추가합니다.  
  
    -   연습을 완료하여 코드를 개발한 경우 `GetURLContentsAsync` 메서드를 포함하는 응용 프로그램에 `ProcessURLAsync`를 추가합니다. 이 응용 프로그램에 대한 MainWindow.xaml.cs 파일은 "연습의 전체 코드 예제" 섹션에서 첫 번째 예제입니다.  
  
     `ProcessURLAsync` 메서드는 원래 연습의 `SumPageSizesAsync`에 `foreach` 루프 본문의 작업을 통합합니다. 이 메서드는 비동기적으로 지정된 웹 사이트의 내용을 바이트 배열로 다운로드한 다음 바이트 배열의 길이를 표시하고 반환합니다.  
  
    ```csharp  
    private async Task<int> ProcessURLAsync(string url)  
    {  
        var byteArray = await GetURLContentsAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
    ```  
  
2.  다음 코드와 같이 `SumPageSizesAsync`의 `foreach` 루프를 주석으로 처리하거나 삭제합니다.  
  
    ```csharp  
    //var total = 0;  
    //foreach (var url in urlList)  
    //{  
    //    byte[] urlContents = await GetURLContentsAsync(url);  
  
    //    // The previous line abbreviates the following two assignment statements.  
    //    // GetURLContentsAsync returns a Task<T>. At completion, the task  
    //    // produces a byte array.  
    //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
    //    //byte[] urlContents = await getContentsTask;  
  
    //    DisplayResults(url, urlContents);  
  
    //    // Update the total.            
    //    total += urlContents.Length;  
    //}  
    ```  
  
3.  작업 컬렉션을 만듭니다. 다음 코드는 <xref:System.Linq.Enumerable.ToArray%2A> 메서드가 실행할 때 각 웹 사이트의 내용을 다운로드하는 작업 컬렉션을 만드는 [쿼리](../../../../csharp/programming-guide/concepts/linq/index.md)를 정의합니다. 작업은 쿼리가 평가될 때 시작됩니다.  
  
     `SumPageSizesAsync` 메서드의 `urlList` 선언 뒤에 다음 코드를 추가합니다.  
  
    ```csharp  
    // Create a query.   
    IEnumerable<Task<int>> downloadTasksQuery =   
        from url in urlList select ProcessURLAsync(url);  
  
    // Use ToArray to execute the query and start the download tasks.  
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
    ```  
  
4.  작업 컬렉션 `downloadTasks`에서 `Task.WhenAll`을 적용합니다. `Task.WhenAll`은 작업 컬렉션의 모든 작업이 완료될 때 완료되는 단일 작업을 반환합니다.  
  
     다음 예제에서 `await` 식은 `WhenAll`이 반환하는 단일 작업이 완료될 때까지 기다립니다. 식은 각 정수가 다운로드된 웹 사이트의 길이인 정수 배열로 평가됩니다. 이전 단계에서 추가한 코드 뒤의 `SumPageSizesAsync`에 다음 코드를 추가합니다.  
  
    ```csharp  
    // Await the completion of all the running tasks.  
    int[] lengths = await Task.WhenAll(downloadTasks);  
  
    //// The previous line is equivalent to the following two statements.  
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
    //int[] lengths = await whenAllTask;  
    ```  
  
5.  마지막으로, <xref:System.Linq.Enumerable.Sum%2A> 메서드를 사용하여 모든 웹 사이트의 길이 합계를 계산합니다. `SumPageSizesAsync`에 다음 줄을 추가합니다.  
  
    ```csharp  
    int total = lengths.Sum();  
    ```  
  
### <a name="to-add-taskwhenall-to-the-httpclientgetbytearrayasync-solution"></a>HttpClient.GetByteArrayAsync 솔루션에 Task.WhenAll을 추가하려면  
  
1.  [연습: async 및 await를 사용하여 웹에 액세스(C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)에서 개발된 두 번째 응용 프로그램에 다음 버전의 `ProcessURLAsync`를 추가합니다.  
  
    -   [개발자 코드 샘플](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)에서 코드를 다운로드한 경우 AsyncWalkthrough_HttpClient 프로젝트를 열고 MainWindow.xaml.cs 파일에 `ProcessURLAsync`를 추가합니다.  
  
    -   연습을 완료하여 코드를 개발한 경우 `HttpClient.GetByteArrayAsync` 메서드를 사용하는 응용 프로그램에 `ProcessURLAsync`를 추가합니다. 이 응용 프로그램에 대한 MainWindow.xaml.cs 파일은 "연습의 전체 코드 예제" 섹션에서 두 번째 예제입니다.  
  
     `ProcessURLAsync` 메서드는 원래 연습의 `SumPageSizesAsync`에 `foreach` 루프 본문의 작업을 통합합니다. 이 메서드는 비동기적으로 지정된 웹 사이트의 내용을 바이트 배열로 다운로드한 다음 바이트 배열의 길이를 표시하고 반환합니다.  
  
     이전 절차의 `ProcessURLAsync` 메서드와 차이점은 <xref:System.Net.Http.HttpClient> 인스턴스 `client`를 사용한다는 것입니다.  
  
    ```csharp  
    async Task<int> ProcessURLAsync(string url, HttpClient client)  
    {  
        byte[] byteArray = await client.GetByteArrayAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
    ```  
  
2.  다음 코드와 같이 `SumPageSizesAsync`의 `For Each` 또는 `foreach` 루프를 주석으로 처리하거나 삭제합니다.  
  
    ```csharp  
    //var total = 0;  
    //foreach (var url in urlList)  
    //{  
    //    // GetByteArrayAsync returns a Task<T>. At completion, the task  
    //    // produces a byte array.  
    //    byte[] urlContent = await client.GetByteArrayAsync(url);  
  
    //    // The previous line abbreviates the following two assignment  
    //    // statements.  
    //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);  
    //    byte[] urlContent = await getContentTask;  
  
    //    DisplayResults(url, urlContent);  
  
    //    // Update the total.  
    //    total += urlContent.Length;  
    //}  
    ```  
  
3.  <xref:System.Linq.Enumerable.ToArray%2A> 메서드에서 실행할 때 각 웹 사이트의 내용을 다운로드하는 작업 컬렉션을 만드는 [쿼리](../../../../csharp/programming-guide/concepts/linq/index.md)를 정의합니다. 작업은 쿼리가 평가될 때 시작됩니다.  
  
     `SumPageSizesAsync` 메서드의 `client` 및 `urlList` 선언 뒤에 다음 코드를 추가합니다.  
  
    ```csharp  
    // Create a query.  
    IEnumerable<Task<int>> downloadTasksQuery =   
        from url in urlList select ProcessURLAsync(url, client);  
  
    // Use ToArray to execute the query and start the download tasks.  
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
    ```  
  
4.  작업 컬렉션 `downloadTasks`에서 `Task.WhenAll`을 적용합니다. `Task.WhenAll`은 작업 컬렉션의 모든 작업이 완료될 때 완료되는 단일 작업을 반환합니다.  
  
     다음 예제에서 `await` 식은 `WhenAll`이 반환하는 단일 작업이 완료될 때까지 기다립니다. 완료되면 `await` 식은 각 정수가 다운로드된 웹 사이트의 길이인 정수 배열로 평가됩니다. 이전 단계에서 추가한 코드 뒤의 `SumPageSizesAsync`에 다음 코드를 추가합니다.  
  
    ```csharp  
    // Await the completion of all the running tasks.  
    int[] lengths = await Task.WhenAll(downloadTasks);  
  
    //// The previous line is equivalent to the following two statements.  
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
    //int[] lengths = await whenAllTask;  
    ```  
  
5.  마지막으로, <xref:System.Linq.Enumerable.Sum%2A> 메서드를 사용하여 모든 웹 사이트의 길이 합계를 가져옵니다. `SumPageSizesAsync`에 다음 줄을 추가합니다.  
  
    ```csharp  
    int total = lengths.Sum();
    ```  
  
### <a name="to-test-the-taskwhenall-solutions"></a>Task.WhenAll 솔루션을 테스트하려면  
  
-   두 솔루션 중 하나에 대해 F5 키를 선택하여 프로그램을 실행한 다음 **시작** 단추를 선택합니다. 출력은 [연습: async 및 await를 사용하여 웹에 액세스(C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)의 비동기 솔루션 출력과 유사해야 합니다. 그러나 웹 사이트가 매번 다른 순서로 나타납니다.  
  
## <a name="example"></a>예  
 다음 코드에서는 `GetURLContentsAsync` 메서드를 사용하여 웹에서 콘텐츠를 다운로드하는 프로젝트에 대한 확장을 보여 줍니다.  
  
```csharp  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF_WhenAll  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
  
            // Two-step async call.  
            Task sumTask = SumPageSizesAsync();  
            await sumTask;  
  
            // One-step async call.  
            //await SumPageSizesAsync();  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            // Create a query.   
            IEnumerable<Task<int>> downloadTasksQuery =   
                from url in urlList select ProcessURLAsync(url);  
  
            // Use ToArray to execute the query and start the download tasks.  
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
  
            // You can do other work here before awaiting.  
  
            // Await the completion of all the running tasks.  
            int[] lengths = await Task.WhenAll(downloadTasks);  
  
            //// The previous line is equivalent to the following two statements.  
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
            //int[] lengths = await whenAllTask;  
  
            int total = lengths.Sum();  
  
            //var total = 0;  
            //foreach (var url in urlList)  
            //{  
            //    byte[] urlContents = await GetURLContentsAsync(url);  
  
            //    // The previous line abbreviates the following two assignment statements.  
            //    // GetURLContentsAsync returns a Task<T>. At completion, the task  
            //    // produces a byte array.  
            //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
            //    //byte[] urlContents = await getContentsTask;  
  
            //    DisplayResults(url, urlContents);  
  
            //    // Update the total.            
            //    total += urlContents.Length;  
            //}  
  
            // Display the total count for all of the websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "https://msdn.microsoft.com",  
                "https://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
                "https://msdn.microsoft.com/library/hh290136.aspx",  
                "https://msdn.microsoft.com/library/ee256749.aspx",  
                "https://msdn.microsoft.com/library/hh290138.aspx",  
                "https://msdn.microsoft.com/library/hh290140.aspx",  
                "https://msdn.microsoft.com/library/dd470362.aspx",  
                "https://msdn.microsoft.com/library/aa578028.aspx",  
                "https://msdn.microsoft.com/library/ms404677.aspx",  
                "https://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        // The actions from the foreach loop are moved to this async method.  
        private async Task<int> ProcessURLAsync(string url)  
        {  
            var byteArray = await GetURLContentsAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private async Task<byte[]> GetURLContentsAsync(string url)  
        {  
            // The downloaded resource ends up in the variable named content.  
            var content = new MemoryStream();  
  
            // Initialize an HttpWebRequest for the current URL.  
            var webReq = (HttpWebRequest)WebRequest.Create(url);  
  
            // Send the request to the Internet resource and wait for  
            // the response.  
            using (WebResponse response = await webReq.GetResponseAsync())  
            {  
                // Get the data stream that is associated with the specified url.  
                using (Stream responseStream = response.GetResponseStream())  
                {  
                    await responseStream.CopyToAsync(content);  
                }  
            }  
  
            // Return the result as a byte array.  
            return content.ToArray();  
  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "https://".  
            var displayURL = url.Replace("https://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
  
        }  
    }  
}  
```  
  
## <a name="example"></a>예  
 다음 코드에서는 `HttpClient.GetByteArrayAsync` 메서드를 사용하여 웹에서 콘텐츠를 다운로드하는 프로젝트에 대한 확장을 보여 줍니다.  
  
```csharp  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF_HttpClient_WhenAll  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
  
            // One-step async call.  
            await SumPageSizesAsync();  
  
            // Two-step async call.  
            //Task sumTask = SumPageSizesAsync();  
            //await sumTask;  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            // Declare an HttpClient object and increase the buffer size. The  
            // default buffer size is 65,536.  
            HttpClient client = new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
            // Create a query.  
            IEnumerable<Task<int>> downloadTasksQuery =   
                from url in urlList select ProcessURLAsync(url, client);  
  
            // Use ToArray to execute the query and start the download tasks.  
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
  
            // You can do other work here before awaiting.  
  
            // Await the completion of all the running tasks.  
            int[] lengths = await Task.WhenAll(downloadTasks);  
  
            //// The previous line is equivalent to the following two statements.  
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
            //int[] lengths = await whenAllTask;  
  
            int total = lengths.Sum();  
  
            //var total = 0;  
            //foreach (var url in urlList)  
            //{  
            //    // GetByteArrayAsync returns a Task<T>. At completion, the task  
            //    // produces a byte array.  
            //    byte[] urlContent = await client.GetByteArrayAsync(url);  
  
            //    // The previous line abbreviates the following two assignment  
            //    // statements.  
            //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);  
            //    byte[] urlContent = await getContentTask;  
  
            //    DisplayResults(url, urlContent);  
  
            //    // Update the total.  
            //    total += urlContent.Length;  
            //}  
  
            // Display the total count for all of the web addresses.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "https://msdn.microsoft.com",  
                "https://msdn.microsoft.com/library/hh290136.aspx",  
                "https://msdn.microsoft.com/library/ee256749.aspx",  
                "https://msdn.microsoft.com/library/hh290138.aspx",  
                "https://msdn.microsoft.com/library/hh290140.aspx",  
                "https://msdn.microsoft.com/library/dd470362.aspx",  
                "https://msdn.microsoft.com/library/aa578028.aspx",  
                "https://msdn.microsoft.com/library/ms404677.aspx",  
                "https://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        // The actions from the foreach loop are moved to this async method.  
        async Task<int> ProcessURLAsync(string url, HttpClient client)  
        {  
            byte[] byteArray = await client.GetByteArrayAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each web site. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "https://".  
            var displayURL = url.Replace("https://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>  
- [연습: async 및 await를 사용하여 웹에 액세스(C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
