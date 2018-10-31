---
title: 비동기 작업 또는 작업 목록 취소(C#)
ms.date: 07/20/2015
ms.assetid: eec32dbb-70ea-4c88-bd27-fa2e34546914
ms.openlocfilehash: b4dc6aaca100008f81b55f3d853b1ccf89d50bb2
ms.sourcegitcommit: d88024e6d6d8b242feae5f4007a709379355aa24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49316495"
---
# <a name="cancel-an-async-task-or-a-list-of-tasks-c"></a>비동기 작업 또는 작업 목록 취소(C#)

작업이 완료될 때까지 기다리지 않으려면 비동기 응용 프로그램을 취소할 때 사용하는 단추를 설정할 수 있습니다. 이 항목의 예제에 따라 한 웹 사이트 또는 웹 사이트 목록의 콘텐츠를 다운로드하는 응용 프로그램에 취소 단추를 추가할 수 있습니다.

예제에서는 [비동기 응용 프로그램 미세 조정(C#)](../../../../csharp/programming-guide/concepts/async/fine-tuning-your-async-application.md)에서 설명하는 UI를 사용합니다.

> [!NOTE]
> 예제를 실행하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치되어 있어야 합니다.

## <a name="cancel-a-task"></a>작업 취소

첫 번째 예제에서는 **취소** 단추를 단일 다운로드 작업에 연결합니다. 응용 프로그램이 콘텐츠를 다운로드하는 동안 단추를 선택하면 다운로드가 취소됩니다.

### <a name="download-the-example"></a>예제 다운로드

[Async 샘플: 응용 프로그램 세부 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 전체 WPF(Windows Presentation Foundation) 프로젝트를 다운로드한 후 다음 단계를 따를 수 있습니다.

1.  다운로드한 파일의 압축을 푼 다음 Visual Studio를 시작합니다.

2.  메뉴 모음에서 **파일** > **열기** > **프로젝트/솔루션**을 선택합니다.

3.  **프로젝트 열기** 대화 상자에서 압축을 해제한 샘플 코드가 포함된 폴더를 열고 AsyncFineTuningCS에 대한 솔루션(.sln) 파일을 엽니다.

4.  **솔루션 탐색기**에서 **CancelATask** 프로젝트에 대한 바로 가기 메뉴를 열고 **시작 프로젝트로 설정**을 선택합니다.

5.  **F5** 키를 선택하여 프로젝트를 실행합니다. 또는 디버그하지 않고 프로젝트를 실행하려면 **Ctrl**+**F5**를 누릅니다.

> [!TIP]
> 프로젝트를 다운로드하지 않으려는 경우 이 항목의 끝에 있는 MainWindow.xaml.cs 파일을 검토할 수 있습니다.

### <a name="build-the-example"></a>예제 빌드
 다음 변경 내용은 웹 사이트를 다운로드하는 응용 프로그램에 **취소** 단추를 추가합니다. 예제를 다운로드하거나 빌드하지 않으려면 이 항목의 끝에 있는 “전체 예제” 섹션에서 최종 결과를 검토할 수 있습니다. 코드에서 변경 내용에는 별표가 표시됩니다.

 직접 예제를 빌드하려면 "예제 다운로드" 섹션의 지침을 단계별로 따르지만 **시작 프로젝트**로 **CancelATask** 대신 **StarterCode**를 선택합니다.

 그리고 다음 변경 내용을 해당 프로젝트의 MainWindow.xaml.cs 파일에 추가합니다.

1.  액세스하는 모든 메서드에 대한 범위 내에 있는 `CancellationTokenSource` 변수 `cts`를 선언합니다.

    ```csharp
    public partial class MainWindow : Window
    {
        // ***Declare a System.Threading.CancellationTokenSource.
        CancellationTokenSource cts;
    ```

2.  **취소** 단추에 대한 다음 이벤트 처리기를 추가합니다. 이벤트 처리기는 <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=nameWithType> 메서드를 사용하여 사용자가 취소를 요청할 때 `cts`에 알려줍니다.

    ```csharp
    // ***Add an event handler for the Cancel button.
    private void cancelButton_Click(object sender, RoutedEventArgs e)
    {
        if (cts != null)
        {
            cts.Cancel();
        }
    }
    ```

3.  이벤트 처리기에서 **시작** 단추 `startButton_Click`을 다음과 같이 변경합니다.

    -   `CancellationTokenSource`, `cts`를 인스턴스화합니다.

        ```csharp
        // ***Instantiate the CancellationTokenSource.
        cts = new CancellationTokenSource();
        ```

    -   지정된 웹 사이트의 콘텐츠를 다운로드하는 `AccessTheWebAsync` 호출에서 `cts`의 <xref:System.Threading.CancellationTokenSource.Token%2A?displayProperty=nameWithType> 속성을 인수로 전송합니다. 취소가 요청되면 `Token` 속성은 메시지를 전파합니다. 사용자가 다운로드 작업을 취소하도록 선택할 경우 메시지를 표시하는 catch 블록을 추가합니다. 다음 코드는 변경 내용을 보여 줍니다.

        ```csharp
        try
        {
            // ***Send a token to carry the message if cancellation is requested.
            int contentLength = await AccessTheWebAsync(cts.Token);
            resultsTextBox.Text +=
                String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);
        }
        // *** If cancellation is requested, an OperationCanceledException results.
        catch (OperationCanceledException)
        {
            resultsTextBox.Text += "\r\nDownload canceled.\r\n";
        }
        catch (Exception)
        {
            resultsTextBox.Text += "\r\nDownload failed.\r\n";
        }
        ```

4.  `AccessTheWebAsync`에서 <xref:System.Net.Http.HttpClient> 형식에 있는 `GetAsync` 메서드의 <xref:System.Net.Http.HttpClient.GetAsync%28System.String%2CSystem.Threading.CancellationToken%29?displayProperty=nameWithType> 오버로드를 사용하여 웹 사이트의 콘텐츠를 다운로드합니다. `AccessTheWebAsync`의 <xref:System.Threading.CancellationToken> 매개 변수인 `ct`를 두 번째 인수로 전달합니다. 사용자가 **취소** 단추를 선택하면 토큰이 메시지를 전달합니다.

     다음 코드는 `AccessTheWebAsync`의 변경 내용을 보여 줍니다.

    ```csharp
    // ***Provide a parameter for the CancellationToken.
    async Task<int> AccessTheWebAsync(CancellationToken ct)
    {
        HttpClient client = new HttpClient();

        resultsTextBox.Text +=
            String.Format("\r\nReady to download.\r\n");

        // You might need to slow things down to have a chance to cancel.
        await Task.Delay(250);

        // GetAsync returns a Task<HttpResponseMessage>.
        // ***The ct argument carries the message if the Cancel button is chosen.
        HttpResponseMessage response = await client.GetAsync("https://msdn.microsoft.com/library/dd470362.aspx", ct);

        // Retrieve the website contents from the HttpResponseMessage.
        byte[] urlContents = await response.Content.ReadAsByteArrayAsync();

        // The result of the method is the length of the downloaded website.
        return urlContents.Length;
    }
    ```

5.  프로그램을 취소하지 않으면 다음 출력이 생성됩니다.

    ```text
    Ready to download.
    Length of the downloaded string: 158125.
    ```

     프로그램이 다운로드를 완료하기 전에 **취소** 단추를 선택하면 다음 출력이 생성됩니다.

    ```text
    Ready to download.
    Download canceled.
    ```

## <a name="cancel-a-list-of-tasks"></a>작업 목록 취소

이전 예제를 확장하여 같은 `CancellationTokenSource` 인스턴스를 각 작업과 연결하는 방식으로 여러 작업을 취소할 수 있습니다. **취소** 단추를 선택하면 아직 완료되지 않은 모든 작업이 취소됩니다.

### <a name="download-the-example"></a>예제 다운로드

[Async 샘플: 응용 프로그램 세부 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 전체 WPF(Windows Presentation Foundation) 프로젝트를 다운로드한 후 다음 단계를 따를 수 있습니다.

1.  다운로드한 파일의 압축을 푼 다음 Visual Studio를 시작합니다.

2.  메뉴 모음에서 **파일** > **열기** > **프로젝트/솔루션**을 선택합니다.

3.  **프로젝트 열기** 대화 상자에서 압축을 해제한 샘플 코드가 포함된 폴더를 열고 AsyncFineTuningCS에 대한 솔루션(.sln) 파일을 엽니다.

4.  **솔루션 탐색기**에서 **CancelAListOfTasks** 프로젝트에 대한 바로 가기 메뉴를 열고 **시작 프로젝트로 설정**을 선택합니다.

5.  **F5** 키를 선택하여 프로젝트를 실행합니다.

     디버그하지 않고 프로젝트를 실행하려면 **Ctrl**+**F5**를 선택합니다.

프로젝트를 다운로드하지 않으려는 경우 이 항목의 끝에 있는 MainWindow.xaml.cs 파일을 검토할 수 있습니다.

### <a name="build-the-example"></a>예제 빌드

직접 예제를 확장하려면 "예제 다운로드" 섹션의 지침을 단계별로 따르되, **CancelATask**를 **시작 프로젝트**로 선택합니다. 해당 프로젝트에 다음 변경 내용을 추가합니다. 프로그램에서 변경 내용에는 별표가 표시됩니다.

1.  웹 주소 목록에 메서드를 추가합니다.

    ```csharp
    // ***Add a method that creates a list of web addresses.
    private List<string> SetUpURLList()
    {
        List<string> urls = new List<string>
        {
            "https://msdn.microsoft.com",
            "https://msdn.microsoft.com/library/hh290138.aspx",
            "https://msdn.microsoft.com/library/hh290140.aspx",
            "https://msdn.microsoft.com/library/dd470362.aspx",
            "https://msdn.microsoft.com/library/aa578028.aspx",
            "https://msdn.microsoft.com/library/ms404677.aspx",
            "https://msdn.microsoft.com/library/ff730837.aspx"
        };
        return urls;
    }
    ```

2.  `AccessTheWebAsync`에서 메서드를 호출합니다.

    ```csharp
    // ***Call SetUpURLList to make a list of web addresses.
    List<string> urlList = SetUpURLList();
    ```

3.  `AccessTheWebAsync`에서 다음 루프를 추가하여 목록에 있는 각 웹 주소를 처리합니다.

    ```csharp
    // ***Add a loop to process the list of web addresses.
    foreach (var url in urlList)
    {
        // GetAsync returns a Task<HttpResponseMessage>.
        // Argument ct carries the message if the Cancel button is chosen.
        // ***Note that the Cancel button can cancel all remaining downloads.
        HttpResponseMessage response = await client.GetAsync(url, ct);

        // Retrieve the website contents from the HttpResponseMessage.
        byte[] urlContents = await response.Content.ReadAsByteArrayAsync();

        resultsTextBox.Text +=
            String.Format("\r\nLength of the downloaded string: {0}.\r\n", urlContents.Length);
    }
    ```

4.  `AccessTheWebAsync`는 길이를 표시하므로 메서드가 아무것도 반환할 필요가 없습니다. return 문을 제거하고 메서드의 반환 형식을 <xref:System.Threading.Tasks.Task%601> 대신 <xref:System.Threading.Tasks.Task>로 변경합니다.

    ```csharp
    async Task AccessTheWebAsync(CancellationToken ct)
    ```

     식 대신 문을 사용하여 `startButton_Click`에서 메서드를 호출합니다.

    ```csharp
    await AccessTheWebAsync(cts.Token);
    ```

5.  프로그램을 취소하지 않으면 다음 출력이 생성됩니다.

    ```text
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

    ```text
    Length of the downloaded string: 35939.

    Length of the downloaded string: 237682.

    Length of the downloaded string: 128607.

    Downloads canceled.
    ```

## <a name="complete-examples"></a>전체 예제

다음 섹션에는 각각의 이전 예제에 대한 코드가 있습니다. <xref:System.Net.Http>에 대한 참조를 추가해야 합니다.

[Async 샘플: 응용 프로그램 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)에서 프로젝트를 다운로드할 수 있습니다.

### <a name="example---cancel-a-task"></a>예제 - 작업 취소

다음 코드는 단일 작업을 취소하는 예제에 대한 전체 MainWindow.xaml.cs 파일입니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

// Add a using directive and a reference for System.Net.Http.
using System.Net.Http;

// Add the following using directive for System.Threading.

using System.Threading;
namespace CancelATask
{
    public partial class MainWindow : Window
    {
        // ***Declare a System.Threading.CancellationTokenSource.
        CancellationTokenSource cts;

        public MainWindow()
        {
            InitializeComponent();
        }

        private async void startButton_Click(object sender, RoutedEventArgs e)
        {
            // ***Instantiate the CancellationTokenSource.
            cts = new CancellationTokenSource();

            resultsTextBox.Clear();

            try
            {
                // ***Send a token to carry the message if cancellation is requested.
                int contentLength = await AccessTheWebAsync(cts.Token);
                resultsTextBox.Text +=
                    String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);
            }
            // *** If cancellation is requested, an OperationCanceledException results.
            catch (OperationCanceledException)
            {
                resultsTextBox.Text += "\r\nDownload canceled.\r\n";
            }
            catch (Exception)
            {
                resultsTextBox.Text += "\r\nDownload failed.\r\n";
            }

            // ***Set the CancellationTokenSource to null when the download is complete.
            cts = null;
        }

        // ***Add an event handler for the Cancel button.
        private void cancelButton_Click(object sender, RoutedEventArgs e)
        {
            if (cts != null)
            {
                cts.Cancel();
            }
        }

        // ***Provide a parameter for the CancellationToken.
        async Task<int> AccessTheWebAsync(CancellationToken ct)
        {
            HttpClient client = new HttpClient();

            resultsTextBox.Text +=
                String.Format("\r\nReady to download.\r\n");

            // You might need to slow things down to have a chance to cancel.
            await Task.Delay(250);

            // GetAsync returns a Task<HttpResponseMessage>.
            // ***The ct argument carries the message if the Cancel button is chosen.
            HttpResponseMessage response = await client.GetAsync("https://msdn.microsoft.com/library/dd470362.aspx", ct);

            // Retrieve the website contents from the HttpResponseMessage.
            byte[] urlContents = await response.Content.ReadAsByteArrayAsync();

            // The result of the method is the length of the downloaded website.
            return urlContents.Length;
        }
    }

    // Output for a successful download:

    // Ready to download.

    // Length of the downloaded string: 158125.

    // Or, if you cancel:

    // Ready to download.

    // Download canceled.
}
```

### <a name="example---cancel-a-list-of-tasks"></a>예제 - 작업 목록 취소

다음 코드는 작업 목록을 취소하는 예제에 대한 전체 MainWindow.xaml.cs 파일입니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

// Add a using directive and a reference for System.Net.Http.
using System.Net.Http;

// Add the following using directive for System.Threading.
using System.Threading;

namespace CancelAListOfTasks
{
    public partial class MainWindow : Window
    {
        // Declare a System.Threading.CancellationTokenSource.
        CancellationTokenSource cts;

        public MainWindow()
        {
            InitializeComponent();
        }

        private async void startButton_Click(object sender, RoutedEventArgs e)
        {
            // Instantiate the CancellationTokenSource.
            cts = new CancellationTokenSource();

            resultsTextBox.Clear();

            try
            {
                await AccessTheWebAsync(cts.Token);
                // ***Small change in the display lines.
                resultsTextBox.Text += "\r\nDownloads complete.";
            }
            catch (OperationCanceledException)
            {
                resultsTextBox.Text += "\r\nDownloads canceled.";
            }
            catch (Exception)
            {
                resultsTextBox.Text += "\r\nDownloads failed.";
            }

            // Set the CancellationTokenSource to null when the download is complete.
            cts = null;
        }

        // Add an event handler for the Cancel button.
        private void cancelButton_Click(object sender, RoutedEventArgs e)
        {
            if (cts != null)
            {
                cts.Cancel();
            }
        }

        // Provide a parameter for the CancellationToken.
        // ***Change the return type to Task because the method has no return statement.
        async Task AccessTheWebAsync(CancellationToken ct)
        {
            // Declare an HttpClient object.
            HttpClient client = new HttpClient();

            // ***Call SetUpURLList to make a list of web addresses.
            List<string> urlList = SetUpURLList();

            // ***Add a loop to process the list of web addresses.
            foreach (var url in urlList)
            {
                // GetAsync returns a Task<HttpResponseMessage>.
                // Argument ct carries the message if the Cancel button is chosen.
                // ***Note that the Cancel button can cancel all remaining downloads.
                HttpResponseMessage response = await client.GetAsync(url, ct);

                // Retrieve the website contents from the HttpResponseMessage.
                byte[] urlContents = await response.Content.ReadAsByteArrayAsync();

                resultsTextBox.Text +=
                    String.Format("\r\nLength of the downloaded string: {0}.\r\n", urlContents.Length);
            }
        }

        // ***Add a method that creates a list of web addresses.
        private List<string> SetUpURLList()
        {
            List<string> urls = new List<string>
            {
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            };
            return urls;
        }
    }

    // Output if you do not choose to cancel:

    //Length of the downloaded string: 35939.

    //Length of the downloaded string: 237682.

    //Length of the downloaded string: 128607.

    //Length of the downloaded string: 158124.

    //Length of the downloaded string: 204890.

    //Length of the downloaded string: 175488.

    //Length of the downloaded string: 145790.

    //Downloads complete.

    // Sample output if you choose to cancel:

    //Length of the downloaded string: 35939.

    //Length of the downloaded string: 237682.

    //Length of the downloaded string: 128607.

    //Downloads canceled.
}
```

## <a name="see-also"></a>참고 항목

- <xref:System.Threading.CancellationTokenSource>
- <xref:System.Threading.CancellationToken>
- [async 및 await를 사용한 비동기 프로그래밍(C#)](../../../../csharp/programming-guide/concepts/async/index.md)
- [Async 응용 프로그램 미세 조정(C#)](../../../../csharp/programming-guide/concepts/async/fine-tuning-your-async-application.md)
- [Async 샘플: 응용 프로그램 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)
