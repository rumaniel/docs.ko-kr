---
title: '연습: Async 및 Wait (Visual Basic)를 사용 하 여 웹에 액세스'
ms.date: 07/20/2015
ms.assetid: 84fd047f-fab8-4d89-8ced-104fb7310a91
ms.openlocfilehash: 2d9d3ea3d55fcd3a59039f4b8b93f37df35bf86d
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71351912"
---
# <a name="walkthrough-accessing-the-web-by-using-async-and-await-visual-basic"></a>연습: Async 및 Wait (Visual Basic)를 사용 하 여 웹에 액세스

async/await 기능을 사용하여 비동기 프로그램을 보다 쉽고 직관적인 방식으로 작성할 수 있습니다. 동기 코드처럼 보이는 비동기 코드를 작성하고 일반적으로 비동기 코드에 수반되는 어려운 콜백 함수 및 연속 작업을 컴파일러에서 처리하도록 할 수 있습니다.

비동기 기능에 대 한 자세한 내용은 [async And wait (Visual Basic)를 사용한 비동기 프로그래밍](../../../../visual-basic/programming-guide/concepts/async/index.md)을 참조 하세요.

이 연습은 웹 사이트 목록에 있는 바이트 수의 합계를 계산하는 동기 WPF(Windows Presentation Foundation) 애플리케이션에서 시작합니다. 그런 다음 새로운 기능을 사용하여 애플리케이션을 비동기 솔루션으로 변환합니다.

응용 프로그램을 직접 빌드하지 않으려는 경우 "Async 샘플: [개발자 코드 샘플](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)에서 웹C# 연습 (및 Visual Basic)에 액세스 합니다.

이 연습에서는 다음 작업을 완료합니다.

> [!div class="checklist"]
>
> - [WPF 응용 프로그램 만들기](#create-a-wpf-application)
> - [간단한 WPF Mainwindow.xaml 디자인](#design-a-simple-wpf-mainwindow)
> - [참조 추가](#add-a-reference)
> - [필요한 Imports 문 추가](#add-necessary-imports-statements)
> - [동기 응용 프로그램 만들기](#create-a-synchronous-application)
> - [동기 솔루션 테스트](#test-the-synchronous-solution)
> - [GetURLContents를 비동기 메서드로 변환](#convert-geturlcontents-to-an-asynchronous-method)
> - [SumPageSizes을 비동기 메서드로 변환](#convert-sumpagesizes-to-an-asynchronous-method)
> - [StartButton_Click을 비동기 메서드로 변환](#convert-startbutton_click-to-an-asynchronous-method)
> - [비동기 솔루션 테스트](#test-the-asynchronous-solution)
> - [GetURLContentsAsync 메서드를 .NET Framework 메서드로 바꿉니다.](#replace-the-geturlcontentsasync-method-with-a-net-framework-method)

전체 비동기 예제는 [예제](#example) 섹션을 참조 하세요.

## <a name="prerequisites"></a>전제 조건

Visual Studio 2012 이상이 컴퓨터에 설치되어 있어야 합니다. 자세한 내용은 Visual Studio [다운로드](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 페이지를 참조 하세요.

## <a name="create-a-wpf-application"></a>WPF 애플리케이션 만들기

1. Visual Studio를 시작합니다.

2. 메뉴 모음에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.

    **새 프로젝트** 대화 상자가 열립니다.

3. **설치 된 템플릿** 창에서 Visual Basic을 선택한 다음 프로젝트 형식 목록에서 **WPF 응용 프로그램** 을 선택 합니다.

4. **이름** 텍스트 상자에 `AsyncExampleWPF`를 입력하고 **확인** 단추를 선택합니다.

    **솔루션 탐색기**에 새 프로젝트가 표시됩니다.

## <a name="design-a-simple-wpf-mainwindow"></a>간단한 WPF MainWindow 디자인

1. Visual Studio 코드 편집기에서 **MainWindow.xaml** 탭을 선택합니다.

2. **도구 상자** 창이 표시되지 않으면 **보기** 메뉴를 열고 **도구 상자**를 선택합니다.

3. **Button** 컨트롤 및 **TextBox** 컨트롤을 **MainWindow** 창에 추가합니다.

4. **TextBox** 컨트롤을 강조 표시하고 **속성** 창에서 다음 값을 설정합니다.

    - **Name** 속성을 `resultsTextBox`로 설정합니다.

    - **Height** 속성을 250으로 설정합니다.

    - **Width** 속성을 500으로 설정합니다.

    - **Text** 탭에서 Lucida Console 또는 Global Monospace 같은 고정 폭 글꼴을 지정합니다.

5. **Button** 컨트롤을 강조 표시하고 **속성** 창에서 다음 값을 설정합니다.

    - **Name** 속성을 `startButton`으로 설정합니다.

    - **Content** 속성 값을 **Button**에서 **Start**로 변경합니다.

6. 텍스트 상자와 단추가 둘 다 **MainWindow** 창에 나타나도록 위치를 지정합니다.

    WPF XAML 디자이너에 대한 자세한 내용은 [XAML 디자이너를 사용하여 UI 만들기](/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio)를 참조하세요.

## <a name="add-a-reference"></a>참조 추가

1. **솔루션 탐색기**에서 프로젝트의 이름을 강조 표시합니다.

2. 메뉴 모음에서 **프로젝트**, **참조 추가**를 선택합니다.

    **참조 관리자** 대화 상자가 나타납니다.

3. 대화 상자 맨 위에서 프로젝트가 .NET Framework 4.5 이상을 대상으로 하는지 확인합니다.

4. **어셈블리** 영역에서 **프레임워크**가 선택되지 않은 경우 선택합니다.

5. 이름 목록에서 **System.Net.Http** 확인란을 선택합니다.

6. **확인** 단추를 선택하여 대화 상자를 닫습니다.

## <a name="add-necessary-imports-statements"></a>필요한 Imports 문 추가

1. **솔루션 탐색기**에서 mainwindow.xaml의 바로 가기 메뉴를 열고 **코드 보기**를 선택 합니다.

2. 아직 없는 경우 `Imports` 코드 파일의 맨 위에 다음 문을 추가 합니다.

    ```vb
    Imports System.Net.Http
    Imports System.Net
    Imports System.IO
    ```

## <a name="create-a-synchronous-application"></a>동기 응용 프로그램 만들기

1. 디자인 창 mainwindow.xaml에서 **시작** 단추를 두 번 클릭 하 여 mainwindow.xaml에 `startButton_Click` 이벤트 처리기를 만듭니다.

2. Mainwindow.xaml에서 다음 코드를의 `startButton_Click`본문에 복사 합니다.

    ```vb
    resultsTextBox.Clear()
    SumPageSizes()
    resultsTextBox.Text &= vbCrLf & "Control returned to startButton_Click."
    ```

    이 코드는 애플리케이션 `SumPageSizes`를 구동하는 메서드를 호출하고 컨트롤이 `startButton_Click`으로 반환될 때 메시지를 표시합니다.

3. 동기 솔루션에 대한 코드에는 다음 네 가지 메서드가 포함되어 있습니다.

    - `SumPageSizes` - `SetUpURLList`에서 웹 페이지 URL 목록을 가져온 다음 `GetURLContents` 및 `DisplayResults`를 호출하여 각 URL을 처리합니다.

    - `SetUpURLList` - 웹 주소 목록을 만들어 반환합니다.

    - `GetURLContents` - 각 웹 사이트의 콘텐츠를 다운로드하고 해당 콘텐츠를 바이트 배열로 반환합니다.

    - `DisplayResults`- 각 URL에 대한 바이트 배열의 바이트 수를 표시합니다.

    다음 네 가지 메서드를 복사한 다음 mainwindow.xaml의 `startButton_Click` 이벤트 처리기 아래에 붙여 넣습니다.

    ```vb
    Private Sub SumPageSizes()

        ' Make a list of web addresses.
        Dim urlList As List(Of String) = SetUpURLList()

        Dim total = 0
        For Each url In urlList
            ' GetURLContents returns the contents of url as a byte array.
            Dim urlContents As Byte() = GetURLContents(url)

            DisplayResults(url, urlContents)

            ' Update the total.
            total += urlContents.Length
        Next

        ' Display the total count for all of the web addresses.
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "Total bytes returned:  {0}" & vbCrLf, total)
    End Sub

    Private Function SetUpURLList() As List(Of String)

        Dim urls = New List(Of String) From
            {
                "https://msdn.microsoft.com/library/windows/apps/br211380.aspx",
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290136.aspx",
                "https://msdn.microsoft.com/library/ee256749.aspx",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            }
        Return urls
    End Function

    Private Function GetURLContents(url As String) As Byte()

        ' The downloaded resource ends up in the variable named content.
        Dim content = New MemoryStream()

        ' Initialize an HttpWebRequest for the current URL.
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)

        ' Send the request to the Internet resource and wait for
        ' the response.
        ' Note: you can't use HttpWebRequest.GetResponse in a Windows Store app.
        Using response As WebResponse = webReq.GetResponse()
            ' Get the data stream that is associated with the specified URL.
            Using responseStream As Stream = response.GetResponseStream()
                ' Read the bytes in responseStream and copy them to content.
                responseStream.CopyTo(content)
            End Using
        End Using

        ' Return the result as a byte array.
        Return content.ToArray()
    End Function

    Private Sub DisplayResults(url As String, content As Byte())

        ' Display the length of each website. The string format
        ' is designed to be used with a monospaced font, such as
        ' Lucida Console or Global Monospace.
        Dim bytes = content.Length
        ' Strip off the "https://".
        Dim displayURL = url.Replace("https://", "")
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)
    End Sub
    ```

## <a name="test-the-synchronous-solution"></a>동기 솔루션 테스트

1. F5 키를 선택하여 프로그램을 실행한 다음 **시작** 단추를 선택합니다.

    다음 목록과 유사한 출력이 표시되어야 합니다.

    ```console
    msdn.microsoft.com/library/windows/apps/br211380.aspx        383832
    msdn.microsoft.com                                            33964
    msdn.microsoft.com/library/hh290136.aspx               225793
    msdn.microsoft.com/library/ee256749.aspx               143577
    msdn.microsoft.com/library/hh290138.aspx               237372
    msdn.microsoft.com/library/hh290140.aspx               128279
    msdn.microsoft.com/library/dd470362.aspx               157649
    msdn.microsoft.com/library/aa578028.aspx               204457
    msdn.microsoft.com/library/ms404677.aspx               176405
    msdn.microsoft.com/library/ff730837.aspx               143474

    Total bytes returned:  1834802

    Control returned to startButton_Click.
    ```

    개수를 표시하려면 몇 초 정도 걸릴 수 있습니다. 이 시간 동안 UI 스레드는 차단되어 요청한 리소스가 다운로드될 때까지 기다립니다. 따라서 **시작** 단추를 선택한 후에도 표시 창을 이동, 최대화, 최소화할 수 없으며 닫을 수도 없습니다. 이러한 작업은 바이트 개수가 나타나기 시작할 때까지 실패합니다. 웹 사이트가 응답하지 않는 경우 실패한 사이트를 표시하지 않아도 됩니다. 대기를 중지하고 프로그램을 닫는 것도 어렵습니다.

## <a name="convert-geturlcontents-to-an-asynchronous-method"></a>GetURLContents를 비동기 메서드로 변환

1. 동기 솔루션을 비동기 솔루션으로 변환 하려면 `GetURLContents` <xref:System.Net.HttpWebRequest.GetResponse%2A?displayProperty=nameWithType> 메서드를 호출 하 고 <xref:System.IO.Stream.CopyTo%2A?displayProperty=nameWithType> 메서드를 호출 하는 것이 응용 프로그램에서 웹에 액세스 하는 위치 이기 때문에를 시작 하는 것이 가장 좋습니다. .NET Framework는 두 메서드의 비동기 버전을 제공하여 변환을 쉽게 만듭니다.

    `GetURLContents`에서 사용되는 메서드에 대한 자세한 내용은 <xref:System.Net.WebRequest>를 참조하세요.

    > [!NOTE]
    > 이 연습 단계를 수행하면 여러 가지 컴파일러 오류가 표시됩니다. 이러한 오류는 무시하고 연습을 진행할 수 있습니다.

    `GetURLContents`의 셋째 줄에서 호출되는 메서드를 `GetResponse`에서 비동기 작업 기반 <xref:System.Net.WebRequest.GetResponseAsync%2A> 메서드로 변경합니다.

    ```vb
    Using response As WebResponse = webReq.GetResponseAsync()
    ```

2. `GetResponseAsync`는 <xref:System.Threading.Tasks.Task%601>를 반환합니다. 이 경우 *작업 반환 변수* `TResult`는 <xref:System.Net.WebResponse> 형식입니다. 작업은 요청한 데이터를 다운로드하고 작업을 실행하여 완료한 후 실제 `WebResponse` 개체를 생성한다는 약속입니다.

    작업에서 `WebResponse`값을 검색 하려면 다음 코드에 표시된 것 처럼에 대한 호출에 [wait](../../../../visual-basic/language-reference/operators/await-operator.md) 연산자를 적용 합니다.`GetResponseAsync`

    ```vb
    Using response As WebResponse = Await webReq.GetResponseAsync()
    ```

    `GetURLContents` 연산자는 대기 중인 작업이 완료될 때까지 현재 메서드 `Await`의 실행을 일시 중단합니다. 반면, 컨트롤은 현재 메서드의 호출자에게 반환됩니다. 이 예제에서 현재 메서드는 `GetURLContents`이고 호출자는 `SumPageSizes`입니다. 작업이 완료되면 약속된 `WebResponse` 개체가 대기 중인 작업의 값으로 생성되고 `response` 변수에 할당됩니다.

    위의 문을 다음과 같은 두 개의 문으로 구분하여 수행되는 작업을 명확하게 나타낼 수 있습니다.

    ```vb
    Dim responseTask As Task(Of WebResponse) = webReq.GetResponseAsync()
    Using response As WebResponse = Await responseTask
    ```

    `webReq.GetResponseAsync`를 호출하면 `Task(Of WebResponse)` 또는 `Task<WebResponse>`가 반환됩니다. 그런 다음 `WebResponse` 연산자를 작업에 적용 하 여 값을 검색 합니다. `Await`

    비동기 메서드가 작업의 완료에 따라 달라지지 않는 작업을 수행해야 하는 경우 메서드는 비동기 메서드를 호출한 후와 await 연산자가 적용되기 전의 두 문 사이에서 해당 작업을 계속할 수 있습니다. 예제는 [방법: Async 및 wait (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md) 를 사용 하 여 여러 웹 요청을 병렬로 수행 하 고 [다음을 수행 합니다. 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)을 사용 하 여 비동기 연습을 확장 합니다.

3. 이전 단계에서 `Await` 연산자를 추가했으므로 컴파일러 오류가 발생합니다. 연산자는 [Async](../../../../visual-basic/language-reference/modifiers/async.md) 한정자로 표시 된 메서드에서만 사용할 수 있습니다. `CopyTo` 호출을 `CopyToAsync` 호출로 바꾸는 변환 단계를 반복하는 동안에는 오류를 무시합니다.

    - 호출되는 메서드의 이름을 <xref:System.IO.Stream.CopyToAsync%2A>로 변경합니다.

    - `CopyTo` 또는 `CopyToAsync` 메서드는 바이트를 해당 인수 `content`에 복사하고 의미 있는 값을 반환하지 않습니다. 동기 버전에서 `CopyTo` 호출은 값을 반환하지 않는 단순 문입니다. 비동기 버전 `CopyToAsync`는 <xref:System.Threading.Tasks.Task>를 반환합니다. 작업은 "Task(void)"처럼 작동하고 메서드를 대기하도록 합니다. 다음 코드에 표시된 대로 `Await` 또는 `await`를 `CopyToAsync` 호출에 적용합니다.

        ```vb
        Await responseStream.CopyToAsync(content)
        ```

         위의 문은 다음 두 줄의 코드를 줄여서 표시한 것입니다.

        ```vb
        ' CopyToAsync returns a Task, not a Task<T>.
        Dim copyTask As Task = responseStream.CopyToAsync(content)

        ' When copyTask is completed, content contains a copy of
        ' responseStream.
        Await copyTask
        ```

4. `GetURLContents`에서 수행해야 할 나머지 작업은 메서드 시그니처를 조정하는 것입니다. 연산자는 `Await` [Async](../../../../visual-basic/language-reference/modifiers/async.md) 한정자로 표시 된 메서드에서만 사용할 수 있습니다. 다음 코드에 표시된 대로 한정자를 추가하여 메서드를 *비동기 메서드*로 표시합니다.

    ```vb
    Private Async Function GetURLContents(url As String) As Byte()
    ```

5. 비동기 메서드의 반환 형식은, <xref:System.Threading.Tasks.Task> <xref:System.Threading.Tasks.Task%601>만 될 수 있습니다. Visual Basic에서 메서드는 `Task` 또는 `Task(Of T)`를 반환하는 `Function`이거나 `Sub`여야 합니다. 일반적으로 메서드 `Sub` 는 `Sub` 가 필요한 비동기 이벤트 처리기 에서만 사용 됩니다. 다른 경우에는 completed 메서드에 `Task(T)` T 형식의 값을 반환 하는 [Return](../../../../visual-basic/language-reference/statements/return-statement.md) 문이 있는 경우를 사용 하 고, 완료 된 메서드에서 `Task` 의미 있는 값을 반환 하지 않는 경우를 사용 합니다.

    자세한 내용은 [비동기 반환 형식 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)을 참조 하세요.

    `GetURLContents` 메서드에는 return 문이 있고 이 문은 바이트 배열을 반환합니다. 따라서 비동기 버전의 반환 형식은 Task(T)이며, 여기서 T는 바이트 배열입니다. 다음과 같이 메서드 시그니처를 변경합니다.

    - 반환 형식을 `Task(Of Byte())`로 변경합니다.

    - 규칙에 따라 비동기 메서드에는 "Async"로 끝나는 이름이 있으므로 `GetURLContentsAsync` 메서드의 이름을 바꿉니다.

    다음 코드에서는 이러한 변경을 보여 줍니다.

    ```vb
    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())
    ```

    몇 가지 변경 작업을 통해 `GetURLContents`가 비동기 메서드로 변환되었습니다.

## <a name="convert-sumpagesizes-to-an-asynchronous-method"></a>SumPageSizes를 비동기 메서드로 변환

1. `SumPageSizes`에 대한 이전 절차의 단계를 반복합니다. 먼저 `GetURLContents` 호출을 비동기 호출로 변경합니다.

    - 호출되는 메서드의 이름을 `GetURLContents`에서 `GetURLContentsAsync`로 변경하지 않은 경우 지금 변경합니다.

    - `GetURLContentsAsync`에서 반환하는 작업에 `Await`를 적용하여 바이트 배열 값을 가져옵니다.

    다음 코드에서는 이러한 변경을 보여 줍니다.

    ```vb
    Dim urlContents As Byte() = Await GetURLContentsAsync(url)
    ```

    위의 할당은 다음 두 줄의 코드를 줄여서 표시한 것입니다.

    ```vb
    ' GetURLContentsAsync returns a task. At completion, the task
    ' produces a byte array.
    Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)
    Dim urlContents As Byte() = Await getContentsTask
    ```

2. 메서드의 시그니처를 다음과 같이 변경합니다.

    - `Async` 한정자를 사용하여 메서드를 표시합니다.

    - 메서드 이름에 "Async"를 추가합니다.

    - `SumPageSizesAsync`는 T에 대한 값을 반환하지 않으므로 이번에는 작업 반환 변수 T가 없습니다. 메서드에 `Return` 문이 없습니다. 그러나 메서드는 대기 가능하도록 `Task`를 반환해야 합니다. 따라서 메서드 형식을에서 `Sub` 로 `Function`변경 합니다. 함수의 반환 형식은 `Task`입니다.

    다음 코드에서는 이러한 변경을 보여 줍니다.

    ```vb
    Private Async Function SumPageSizesAsync() As Task
    ```

    `SumPageSizes`가 `SumPageSizesAsync`로 변환되었습니다.

## <a name="convert-startbutton_click-to-an-asynchronous-method"></a>startButton_Click을 비동기 메서드로 변환

1. 이벤트 처리기에서 호출된 메서드의 이름을 `SumPageSizes`에서 `SumPageSizesAsync`로 변경하지 않은 경우 지금 변경합니다.

2. `SumPageSizesAsync`는 비동기 메서드이므로 이벤트 처리기에서 코드를 변경하여 결과를 대기합니다.

    `SumPageSizesAsync` 호출은 `GetURLContentsAsync`에서 `CopyToAsync` 호출을 미러링합니다. 이 호출에서는 `Task(T)`가 아니라 `Task`를 반환합니다.

    이전 절차에서처럼 한 개 또는 두 개의 문을 사용하여 호출을 변환할 수 있습니다. 다음 코드에서는 이러한 변경을 보여 줍니다.

    ```vb
    ' One-step async call.
    Await SumPageSizesAsync()

    ' Two-step async call.
    Dim sumTask As Task = SumPageSizesAsync()
    Await sumTask
    ```

3. 실수로 작업을 다시 입력하지 않도록 하려면 `startButton_Click`의 맨 위에 다음 문을 추가하여 **시작** 단추를 사용하지 않도록 설정합니다.

    ```vb
    ' Disable the button until the operation is complete.
    startButton.IsEnabled = False
    ```

    이벤트 처리기의 끝에서 단추를 다시 사용하도록 설정할 수 있습니다.

    ```vb
    ' Reenable the button in case you want to run the operation again.
    startButton.IsEnabled = True
    ```

    재입력에 대 한 자세한 내용은 [비동기 앱에서 재입력 처리 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/handling-reentrancy-in-async-apps.md)를 참조 하세요.

4. 마지막으로 `Async` 한정자를 선언에 추가하여 이벤트 처리기에서 `SumPagSizesAsync`를 기다릴 수 있도록 합니다.

    ```vb
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click
    ```

    일반적으로 이벤트 처리기의 이름은 변경되지 않습니다. 이벤트 처리기 `Task` `Sub` 가 Visual Basic의 프로시저 여야 하므로 반환 형식은로 변경 되지 않습니다.

    동기에서 비동기 처리로 프로젝트 변환이 완료되었습니다.

## <a name="test-the-asynchronous-solution"></a>비동기 솔루션 테스트

1. F5 키를 선택하여 프로그램을 실행한 다음 **시작** 단추를 선택합니다.

2. 동기 솔루션의 출력과 유사한 출력이 표시되어야 합니다. 그러나 다음과 같은 차이가 있습니다.

    - 처리가 완료된 후 결과가 모두 동시에 발생하지는 않습니다. 예를 들어 두 프로그램 모두 텍스트 상자를 지우는 줄을 `startButton_Click`에 포함할 수 있습니다. 의도는 하나의 결과 집합이 나타난 후 몇 초 동안 **시작** 단추를 선택하면 실행 사이에 텍스트 상자를 지우는 것입니다. 동기 버전에서는 다운로드가 완료되고 UI 스레드에서 자유롭게 다른 작업을 수행할 수 있게 되면 두 번째로 개수가 표시되기 직전에 텍스트 상자가 지워집니다. 비동기 버전에서는 **시작** 단추를 선택한 직후에 텍스트 상자가 지워집니다.

    - 가장 중요한 점은 다운로드하는 동안 UI 스레드가 차단되지 않는다는 것입니다. 웹 리소스를 다운로드하고, 개수를 계산하고, 표시하는 동안 창을 이동하거나 크기를 조정할 수 있습니다. 웹 사이트 중 하나가 속도가 느리거나 응답하지 않는 경우 **닫기** 단추(오른쪽 위 모서리에 있는 빨간색 필드의 x)를 선택하여 작업을 취소할 수 있습니다.

## <a name="replace-the-geturlcontentsasync-method-with-a-net-framework-method"></a>GetURLContentsAsync 메서드를 .NET Framework 메서드로 바꿉니다.

1. .NET Framework는 사용할 수 있는 여러 비동기 메서드를 제공 합니다. <xref:System.Net.Http.HttpClient.GetByteArrayAsync%28System.String%29?displayProperty=nameWithType> 이러한 메서드 중 하나는이 연습에 필요한 작업을 수행 하는 것입니다. 이전 절차에서 만든 `GetURLContentsAsync` 메서드 대신 사용할 수도 있습니다.

    첫 번째 단계는 <xref:System.Net.Http.HttpClient> `SumPageSizesAsync` 메서드에 개체를 만드는 것입니다. 메서드의 시작 부분에 다음 선언을 추가합니다.

    ```vb
    ' Declare an HttpClient object and increase the buffer size. The
    ' default buffer size is 65,536.
    Dim client As HttpClient =
        New HttpClient() With {.MaxResponseContentBufferSize = 1000000}
    ```

2. `SumPageSizesAsync,`에서 `GetURLContentsAsync` 메서드 호출을 `HttpClient` 메서드 호출로 바꿉니다.

    ```vb
    Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)
    ```

3. 작성한 `GetURLContentsAsync` 메서드를 제거하거나 주석 처리합니다.

4. F5 키를 선택하여 프로그램을 실행한 다음 **시작** 단추를 선택합니다.

    이 버전의 프로젝트 동작은 "비동기 솔루션을 테스트하려면" 절차에서 설명한 동작과 일치해야 하지만 사용자의 노력은 훨씬 줄어듭니다.

## <a name="example"></a>예제

다음은 비동기 `GetURLContentsAsync` 메서드를 사용 하는 변환 된 비동기 솔루션의 전체 예제입니다. 원래의 동기 솔루션과 매우 유사해야 합니다.

```vb
' Add the following Imports statements, and add a reference for System.Net.Http.
Imports System.Net.Http
Imports System.Net
Imports System.IO

Class MainWindow

    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click

        ' Disable the button until the operation is complete.
        startButton.IsEnabled = False

        resultsTextBox.Clear()

        '' One-step async call.
        Await SumPageSizesAsync()

        ' Two-step async call.
        'Dim sumTask As Task = SumPageSizesAsync()
        'Await sumTask

        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."

        ' Reenable the button in case you want to run the operation again.
        startButton.IsEnabled = True
    End Sub

    Private Async Function SumPageSizesAsync() As Task

        ' Make a list of web addresses.
        Dim urlList As List(Of String) = SetUpURLList()

        Dim total = 0
        For Each url In urlList
            Dim urlContents As Byte() = Await GetURLContentsAsync(url)

            ' The previous line abbreviates the following two assignment statements.

            '//<snippet21>
            ' GetURLContentsAsync returns a task. At completion, the task
            ' produces a byte array.
            'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)
            'Dim urlContents As Byte() = Await getContentsTask

            DisplayResults(url, urlContents)

            ' Update the total.
            total += urlContents.Length
        Next

        ' Display the total count for all of the websites.
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &
                                             "Total bytes returned:  {0}" & vbCrLf, total)
    End Function

    Private Function SetUpURLList() As List(Of String)

        Dim urls = New List(Of String) From
            {
                "https://msdn.microsoft.com/library/windows/apps/br211380.aspx",
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290136.aspx",
                "https://msdn.microsoft.com/library/ee256749.aspx",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            }
        Return urls
    End Function

    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())

        ' The downloaded resource ends up in the variable named content.
        Dim content = New MemoryStream()

        ' Initialize an HttpWebRequest for the current URL.
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)

        ' Send the request to the Internet resource and wait for
        ' the response.
        Using response As WebResponse = Await webReq.GetResponseAsync()

            ' The previous statement abbreviates the following two statements.

            'Dim responseTask As Task(Of WebResponse) = webReq.GetResponseAsync()
            'Using response As WebResponse = Await responseTask

            ' Get the data stream that is associated with the specified URL.
            Using responseStream As Stream = response.GetResponseStream()
                ' Read the bytes in responseStream and copy them to content.
                Await responseStream.CopyToAsync(content)

                ' The previous statement abbreviates the following two statements.

                ' CopyToAsync returns a Task, not a Task<T>.
                'Dim copyTask As Task = responseStream.CopyToAsync(content)

                ' When copyTask is completed, content contains a copy of
                ' responseStream.
                'Await copyTask
            End Using
        End Using

        ' Return the result as a byte array.
        Return content.ToArray()
    End Function

    Private Sub DisplayResults(url As String, content As Byte())

        ' Display the length of each website. The string format
        ' is designed to be used with a monospaced font, such as
        ' Lucida Console or Global Monospace.
        Dim bytes = content.Length
        ' Strip off the "https://".
        Dim displayURL = url.Replace("https://", "")
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)
    End Sub

End Class
```

다음 코드는 `HttpClient` 메서드 `GetByteArrayAsync`를 사용하는 솔루션에 대한 전체 예제입니다.

```vb
' Add the following Imports statements, and add a reference for System.Net.Http.
Imports System.Net.Http
Imports System.Net
Imports System.IO

Class MainWindow

    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click

        resultsTextBox.Clear()

        ' Disable the button until the operation is complete.
        startButton.IsEnabled = False

        ' One-step async call.
        Await SumPageSizesAsync()

        ' Two-step async call.
        'Dim sumTask As Task = SumPageSizesAsync()
        'Await sumTask

        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."

        ' Reenable the button in case you want to run the operation again.
        startButton.IsEnabled = True
    End Sub

    Private Async Function SumPageSizesAsync() As Task

        ' Declare an HttpClient object and increase the buffer size. The
        ' default buffer size is 65,536.
        Dim client As HttpClient =
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}

        ' Make a list of web addresses.
        Dim urlList As List(Of String) = SetUpURLList()

        Dim total = 0
        For Each url In urlList
            ' GetByteArrayAsync returns a task. At completion, the task
            ' produces a byte array.
            Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)

            ' The following two lines can replace the previous assignment statement.
            'Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)
            'Dim urlContents As Byte() = Await getContentsTask

            DisplayResults(url, urlContents)

            ' Update the total.
            total += urlContents.Length
        Next

        ' Display the total count for all of the websites.
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &
                                             "Total bytes returned:  {0}" & vbCrLf, total)
    End Function

    Private Function SetUpURLList() As List(Of String)

        Dim urls = New List(Of String) From
            {
                "https://msdn.microsoft.com/library/windows/apps/br211380.aspx",
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290136.aspx",
                "https://msdn.microsoft.com/library/ee256749.aspx",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            }
        Return urls
    End Function

    Private Sub DisplayResults(url As String, content As Byte())

        ' Display the length of each website. The string format
        ' is designed to be used with a monospaced font, such as
        ' Lucida Console or Global Monospace.
        Dim bytes = content.Length
        ' Strip off the "https://".
        Dim displayURL = url.Replace("https://", "")
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)
    End Sub

End Class
```

## <a name="see-also"></a>참고자료

- [비동기 샘플: 웹 연습에 액세스(C# 및 Visual Basic)](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)
- [Await 연산자](../../../../visual-basic/language-reference/operators/await-operator.md)
- [비동기](../../../../visual-basic/language-reference/modifiers/async.md)
- [Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
- [비동기 반환 형식(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)
- [TAP(작업 기반 비동기 프로그래밍)](https://go.microsoft.com/fwlink/?LinkId=204847)
- [방법: 작업을 사용 하 여 비동기 연습 확장 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)
- [방법: Async 및 Wait (Visual Basic)를 사용 하 여 여러 웹 요청을 병렬로 수행](../../../../visual-basic/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)
