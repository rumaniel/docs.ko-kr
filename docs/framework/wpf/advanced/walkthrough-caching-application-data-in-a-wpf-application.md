---
title: '연습: WPF 애플리케이션에서 애플리케이션 데이터 캐싱'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthroughs [WPF], caching
- caching [.NET Framework]
- caching [WPF]
ms.assetid: dac2c9ce-042b-4d23-91eb-28f584415cef
ms.openlocfilehash: 2609a54ce8ba2076c35567fe5bc1d9961f6fef3f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69942056"
---
# <a name="walkthrough-caching-application-data-in-a-wpf-application"></a>연습: WPF 애플리케이션에서 애플리케이션 데이터 캐싱
캐싱을 사용하면 빠른 액세스를 위해 데이터를 메모리에 저장할 수 있습니다. 데이터에 다시 액세스할 때 애플리케이션은 원래 소스에서 검색하는 대신 캐시에서 데이터를 가져올 수 있습니다. 이 경우 성능과 확장성이 향상됩니다. 또한 캐싱을 사용하면 데이터 소스를 일시적으로 사용할 수 없는 경우에도 데이터를 사용할 수 있습니다.

 .NET Framework는 .NET Framework 응용 프로그램에서 캐싱을 사용할 수 있도록 하는 클래스를 제공 합니다. 이러한 클래스는 <xref:System.Runtime.Caching> 네임 스페이스에 있습니다.

> [!NOTE]
> <xref:System.Runtime.Caching> 네임 스페이스는 .NET Framework 4의 새로운입니다. 이 네임 스페이스는 모든 .NET Framework 응용 프로그램에서 캐싱을 사용할 수 있도록 합니다. 이전 버전의 .NET Framework에서 캐싱은 <xref:System.Web> 네임 스페이스 에서만 사용할 수 있으므로 ASP.NET 클래스에 대 한 종속성이 필요 했습니다.

 이 연습에서는 .NET Framework에서 사용할 수 있는 캐싱 기능을 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램의 일부로 사용 하는 방법을 보여 줍니다. 이 연습에서는 텍스트 파일의 내용을 캐시 합니다.

 이 연습에서 수행할 작업은 다음과 같습니다.

- WPF 응용 프로그램 프로젝트 만들기

- .NET Framework 4에 대 한 참조 추가

- 캐시를 초기화 하는 중입니다.

- 텍스트 파일의 내용을 포함 하는 캐시 엔트리 추가

- 캐시 엔트리에 대 한 제거 정책을 제공 합니다.

- 캐시 된 파일의 경로를 모니터링 하 고 모니터링 되는 항목에 대 한 변경 내용을 캐시 인스턴스에 알립니다.

## <a name="prerequisites"></a>필수 구성 요소
 이 연습을 완료하려면 다음 사항이 필요합니다.

- Microsoft Visual Studio 2010

- 적은 양의 텍스트를 포함 하는 텍스트 파일입니다. 텍스트 파일의 내용은 메시지 상자에 표시 됩니다. 이 연습에서 설명 하는 코드는 사용자가 다음 파일을 사용 하 고 있다고 가정 합니다.

     `c:\cache\cacheText.txt`

     그러나이 연습에서는 모든 텍스트 파일을 사용 하 고 코드를 약간만 변경할 수 있습니다.

## <a name="creating-a-wpf-application-project"></a>WPF 응용 프로그램 프로젝트 만들기
 먼저 WPF 응용 프로그램 프로젝트를 만듭니다.

#### <a name="to-create-a-wpf-application"></a>WPF 애플리케이션을 만들려면

1. Visual Studio를 시작합니다.

2. **파일** 메뉴에서 **새로 만들기**를 클릭 한 다음 **새 프로젝트**를 클릭 합니다.

     **새 프로젝트** 대화 상자가 표시됩니다.

3. **설치 된 템플릿**에서 사용 하려는 프로그래밍 언어 (**Visual Basic** 또는 **C#시각적 개체**)를 선택 합니다.

4. **새 프로젝트** 대화 상자에서 **WPF 응용 프로그램**을 선택 합니다.

    > [!NOTE]
    > **Wpf 응용 프로그램** 템플릿이 표시 되지 않는 경우 wpf를 지 원하는 .NET Framework 버전을 대상으로 하는지 확인 합니다. **새 프로젝트** 대화 상자의 목록에서 .NET Framework 4를 선택 합니다.

5. **이름** 텍스트 상자에 프로젝트의 이름을 입력 합니다. 예를 들어 **WPFCaching**를 입력할 수 있습니다.

6. **솔루션용 디렉터리 만들기** 확인란을 선택합니다.

7. **확인**을 클릭합니다.

     WPF 디자이너가 **디자인** 뷰에서 열리고 mainwindow.xaml 파일이 표시 됩니다. Visual Studio에서 **My Project** 폴더, 응용 프로그램 .xaml 파일 및 mainwindow.xaml 파일을 만듭니다.

## <a name="targeting-the-net-framework-and-adding-a-reference-to-the-caching-assemblies"></a>.NET Framework 대상 지정 및 캐싱 어셈블리에 대 한 참조 추가
 기본적으로 WPF 응용 프로그램은를 [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]대상으로 합니다. WPF 응용 프로그램 <xref:System.Runtime.Caching> 에서 네임 스페이스를 사용 하려면 응용 프로그램이 .NET Framework 4 (가 [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]아님)를 대상으로 하 고 네임 스페이스에 대 한 참조를 포함 해야 합니다.

 따라서 다음 단계는 .NET Framework 대상을 변경 하 고 <xref:System.Runtime.Caching> 네임 스페이스에 대 한 참조를 추가 하는 것입니다.

> [!NOTE]
> .NET Framework 대상을 변경 하는 절차는 Visual Basic 프로젝트와 Visual C# 프로젝트에서 다릅니다.

#### <a name="to-change-the-target-net-framework-in-visual-basic"></a>Visual Basic에서 대상 .NET Framework를 변경 하려면

1. **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.

     응용 프로그램에 대 한 속성 창이 표시 됩니다.

2. **컴파일** 탭을 클릭합니다.

3. 창 맨 아래에서 **고급 컴파일 옵션 ...** 을 클릭 합니다.

     **고급 컴파일러 설정** 대화 상자가 표시 됩니다.

4. **대상 프레임 워크 (모든 구성)** 목록에서 .NET Framework 4를 선택 합니다. 선택 [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]하지 마십시오.

5. **확인**을 클릭합니다.

     **대상 프레임워크 변경** 대화 상자가 표시됩니다.

6. **대상 프레임 워크 변경** 대화 상자에서 **예**를 클릭 합니다.

     프로젝트가 닫힌 후 다시 열립니다.

7. 다음 단계를 수행 하 여 캐싱 어셈블리에 대 한 참조를 추가 합니다.

    1. **솔루션 탐색기**에서 프로젝트의 이름을 마우스 오른쪽 단추로 클릭 한 다음 **참조 추가**를 클릭 합니다.

    2. **.Net** 탭을 선택 하 고 `System.Runtime.Caching`를 선택한 다음 **확인**을 클릭 합니다.

#### <a name="to-change-the-target-net-framework-in-a-visual-c-project"></a>시각적 C# 프로젝트에서 대상 .NET Framework를 변경 하려면

1. **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.

     응용 프로그램에 대 한 속성 창이 표시 됩니다.

2. **응용 프로그램** 탭을 클릭합니다.

3. **대상 프레임 워크** 목록에서 .NET Framework 4를 선택 합니다. **.NET Framework 4 클라이언트 프로필**을 선택 하지 마십시오.

4. 다음 단계를 수행 하 여 캐싱 어셈블리에 대 한 참조를 추가 합니다.

    1. **참조** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **참조 추가**를 클릭 합니다.

    2. **.Net** 탭을 선택 하 고 `System.Runtime.Caching`를 선택한 다음 **확인**을 클릭 합니다.

## <a name="adding-a-button-to-the-wpf-window"></a>WPF 창에 단추 추가
 다음에는 단추 컨트롤을 추가 하 고 단추의 `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다. 나중에이 단추를 클릭할 때 텍스트 파일의 내용이 캐시 되 고 표시 되는 코드를에 추가 합니다.

#### <a name="to-add-a-button-control"></a>단추 컨트롤을 추가 하려면

1. **솔루션 탐색기**에서 mainwindow.xaml 파일을 두 번 클릭 하 여 엽니다.

2. **일반 WPF 컨트롤**의 `Button` **도구 상자**에서 컨트롤을 `MainWindow` 창으로 끌어 옵니다.

3. **속성** 창에서 `Content` `Button` 컨트롤의 속성을 설정 하 여 캐시를 **가져옵니다**.

## <a name="initializing-the-cache-and-caching-an-entry"></a>캐시 초기화 및 항목 캐싱
 다음으로 다음 작업을 수행 하는 코드를 추가 합니다.

- Cache 클래스의 인스턴스를 만듭니다. 즉, 새 <xref:System.Runtime.Caching.MemoryCache> 개체를 인스턴스화합니다.

- 캐시에서 개체를 <xref:System.Runtime.Caching.HostFileChangeMonitor> 사용 하 여 텍스트 파일의 변경 내용을 모니터링 하도록 지정 합니다.

- 텍스트 파일을 읽고 해당 내용을 캐시 항목으로 캐시 합니다.

- 캐시 된 텍스트 파일의 내용을 표시 합니다.

#### <a name="to-create-the-cache-object"></a>Cache 개체를 만들려면

1. MainWindow.xaml.cs 또는 Mainwindow.xaml 파일에서 이벤트 처리기를 만들기 위해 방금 추가한 단추를 두 번 클릭 합니다.

2. 파일의 맨 위에 클래스 선언 앞에 다음 `Imports` (Visual Basic) 또는 `using` (C#) 문을 추가 합니다.

    ```csharp
    using System.Runtime.Caching;
    using System.IO;
    ```

    ```vb
    Imports System.Runtime.Caching
    Imports System.IO
    ```

3. 이벤트 처리기에서 다음 코드를 추가 하 여 cache 개체를 인스턴스화합니다.

    ```csharp
    ObjectCache cache = MemoryCache.Default;
    ```

    ```vb
    Dim cache As ObjectCache = MemoryCache.Default
    ```

     <xref:System.Runtime.Caching.ObjectCache> 클래스는 메모리 내 개체 캐시를 제공 하는 기본 제공 클래스입니다.

4. 다음 코드를 추가 하 여 라는 `filecontents`캐시 항목의 내용을 읽습니다.

    ```vb
    Dim fileContents As String = TryCast(cache("filecontents"), String)
    ```

    ```csharp
    string fileContents = cache["filecontents"] as string;
    ```

5. 다음 코드를 추가 하 여 라는 `filecontents` 캐시 항목이 있는지 여부를 확인 합니다.

    ```vb
    If fileContents Is Nothing Then

    End If
    ```

    ```csharp
    if (fileContents == null)
    {

    }
    ```

     지정 된 캐시 엔트리가 없으면 텍스트 파일을 읽고 캐시에 캐시 항목으로 추가 해야 합니다.

6. 블록에 다음 코드를 추가 하 여 10 초 후에 <xref:System.Runtime.Caching.CacheItemPolicy> 캐시 엔트리가 만료 되도록 지정 하는 새 개체를 만듭니다. `if/then`

    ```vb
    Dim policy As New CacheItemPolicy()
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0)
    ```

    ```csharp
    CacheItemPolicy policy = new CacheItemPolicy();
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0);
    ```

     제거 또는 만료 정보를 제공 하지 않는 경우 기본값은입니다 <xref:System.Runtime.Caching.ObjectCache.InfiniteAbsoluteExpiration>. 즉, 캐시 항목이 절대 시간에 따라 만료 되지 않습니다. 대신 캐시 항목은 메모리가 부족할 때만 만료 됩니다. 가장 좋은 방법은 항상 절대 또는 상대 (sliding) 만료를 명시적으로 제공 하는 것입니다.

7. `if/then` 블록 내에서 이전 단계에서 추가한 코드 뒤에 다음 코드를 추가 하 여 모니터링 하려는 파일 경로에 대 한 컬렉션을 만들고 텍스트 파일의 경로를 컬렉션에 추가 합니다.

    ```vb
    Dim filePaths As New List(Of String)()
    filePaths.Add("c:\cache\cacheText.txt")
    ```

    ```csharp
    List<string> filePaths = new List<string>();
    filePaths.Add("c:\\cache\\cacheText.txt");
    ```

    > [!NOTE]
    > 사용할 텍스트 파일을 사용할 수 없는 `c:\cache\cacheText.txt`경우 텍스트 파일을 사용할 경로를 지정 합니다.

8. 이전 단계에서 추가한 코드 뒤에 다음 코드를 추가 하 여 캐시 항목에 대 한 변경 <xref:System.Runtime.Caching.HostFileChangeMonitor> 모니터의 컬렉션에 새 개체를 추가 합니다.

    ```vb
    policy.ChangeMonitors.Add(New HostFileChangeMonitor(filePaths))
    ```

    ```csharp
    policy.ChangeMonitors.Add(new HostFileChangeMonitor(filePaths));
    ```

     개체 <xref:System.Runtime.Caching.HostFileChangeMonitor> 는 텍스트 파일의 경로를 모니터링 하 고 변경 내용이 발생 하는 경우 캐시에 알립니다. 이 예에서는 파일의 내용이 변경 되 면 캐시 항목이 만료 됩니다.

9. 이전 단계에서 추가한 코드 뒤에 다음 코드를 추가 하 여 텍스트 파일의 내용을 읽습니다.

    ```vb
    fileContents = File.ReadAllText("c:\cache\cacheText.txt") & vbCrLf & DateTime.Now.ToString()
    ```

    ```csharp
    fileContents = File.ReadAllText("c:\\cache\\cacheText.txt") + "\n" + DateTime.Now;
    ```

     캐시 엔트리가 만료 되는 시점을 확인할 수 있도록 날짜 및 시간 타임 스탬프가 추가 됩니다.

10. 이전 단계에서 추가한 코드 뒤에 다음 코드를 추가 하 여 파일 내용을 캐시 개체 <xref:System.Runtime.Caching.CacheItem> 에 인스턴스로 삽입 합니다.

    ```vb
    cache.Set("filecontents", fileContents, policy)
    ```

    ```csharp
    cache.Set("filecontents", fileContents, policy);
    ```

     이전에 만든 개체를 <xref:System.Runtime.Caching.CacheItemPolicy> 매개 변수로 전달 하 여 캐시 엔트리를 제거 하는 방법에 대 한 정보를 지정 합니다.

11. `if/then` 블록 뒤에 다음 코드를 추가 하 여 캐시 된 파일 콘텐츠를 메시지 상자에 표시 합니다.

    ```vb
    MessageBox.Show(fileContents)
    ```

    ```csharp
    MessageBox.Show(fileContents);
    ```

12. **빌드** 메뉴에서 **WPFCaching 빌드** 를 클릭 하 여 프로젝트를 빌드합니다.

## <a name="testing-caching-in-the-wpf-application"></a>WPF 응용 프로그램에서 캐싱 테스트
 이제 응용 프로그램을 테스트할 수 있습니다.

#### <a name="to-test-caching-in-the-wpf-application"></a>WPF 응용 프로그램에서 캐싱을 테스트 하려면

1. Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

     `MainWindow` 창이 표시 됩니다.

2. **캐시 가져오기**를 클릭 합니다.

     텍스트 파일의 캐시 된 내용이 메시지 상자에 표시 됩니다. 파일의 타임 스탬프를 확인 합니다.

3. 메시지 상자를 닫고 **캐시 가져오기** 를 다시 클릭 합니다.

     타임 스탬프는 변경 되지 않습니다. 이는 캐시 된 내용이 표시 됨을 나타냅니다.

4. 10 초 이상 기다렸다가 **캐시 가져오기** 를 다시 클릭 합니다.

     이번에는 새 타임 스탬프가 표시 됩니다. 이는 정책에 의해 캐시 항목이 만료 되 고 새 캐시 된 콘텐츠가 표시 됨을 나타냅니다.

5. 텍스트 편집기에서 사용자가 만든 텍스트 파일을 엽니다. 아직 변경 하지 마십시오.

6. 메시지 상자를 닫고 **캐시 가져오기** 를 다시 클릭 합니다.

     타임 스탬프를 다시 확인 합니다.

7. 텍스트 파일을 변경한 다음 파일을 저장 합니다.

8. 메시지 상자를 닫고 **캐시 가져오기** 를 다시 클릭 합니다.

     이 메시지 상자에는 텍스트 파일의 업데이트 된 콘텐츠와 새 타임 스탬프가 포함 됩니다. 이는 절대 시간 제한 기간이 만료 되지 않았더라도 파일을 변경 하는 즉시 호스트 파일 변경 모니터가 캐시 항목을 제거 했음을 나타냅니다.

    > [!NOTE]
    > 파일을 변경 하는 데 더 많은 시간을 허용 하려면 제거 시간을 20 초 이상으로 늘릴 수 있습니다.

## <a name="code-example"></a>코드 예
 이 연습을 완료 한 후에는 만든 프로젝트에 대 한 코드는 다음 예제와 유사 합니다.

 [!code-csharp[CachingWPFApplications#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CachingWPFApplications/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[CachingWPFApplications#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CachingWPFApplications/VisualBasic/MainWindow.xaml.vb#1)]

## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Caching.MemoryCache>
- <xref:System.Runtime.Caching.ObjectCache>
- <xref:System.Runtime.Caching>
- [.NET Framework 애플리케이션에서 캐시](../../performance/caching-in-net-framework-applications.md)
