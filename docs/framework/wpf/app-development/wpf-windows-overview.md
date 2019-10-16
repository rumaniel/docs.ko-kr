---
title: WPF 창 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XAML [WPF], displaying content via
- XAML pages [WPF], displaying
- content [WPF], displaying via XAML
- window objects [WPF]
- hosting [WPF], applications
- managing windows [WPF]
- dialog boxes [WPF]
- Page object [WPF]
- NavigationWindow objects [WPF]
- applications [WPF], hosting
- content [WPF], displaying
- events [WPF]
- content [WPF], displaying via procedural code
- modal windows [WPF]
- procedural code [WPF], displaying content via
- displaying content via procedural code [WPF]
- window management [WPF]
- displaying content [WPF]
- window events [WPF]
- windows [WPF]
- modal dialog boxes [WPF]
- displaying XAML pages [WPF]
ms.assetid: 737d04ec-8861-46c3-8d44-fa11d3528d23
ms.openlocfilehash: 16f4155cefea20868185febb3d2a566dc1524cc4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956279"
---
# <a name="wpf-windows-overview"></a>WPF 창 개요
사용자는 Windows를 통해 Windows Presentation Foundation (WPF) 독립 실행형 응용 프로그램과 상호 작용 합니다. 창의 기본 용도는 데이터를 시각화하는 콘텐츠를 호스트하고 사용자가 데이터와 상호 작용할 수 있도록 하는 것입니다. 독립 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 실행형 응용 프로그램은 클래스를 <xref:System.Windows.Window> 사용 하 여 자체 창을 제공 합니다. 이 항목에서는 <xref:System.Windows.Window> 독립 실행형 응용 프로그램에서 windows를 만들고 관리 하는 기본 사항을 다루기 전에 소개 합니다.  
  
> [!NOTE]
> 및 느슨한 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 페이지[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 를 포함 하 여 브라우저에서 호스팅되는 응용 프로그램은 자체 창을 제공 하지 않습니다. 대신 Windows Internet Explorer에서 제공 하는 windows에서 호스팅됩니다. [WPF XAML 브라우저 응용 프로그램 개요](wpf-xaml-browser-applications-overview.md)를 참조 하세요.  

<a name="TheWindowClass"></a>   
## <a name="the-window-class"></a>Window 클래스  
 다음 그림에서는 창의 구성 요소를 보여 줍니다.  
  
 ![창 요소를 보여 주는 스크린샷](./media/wpf-windows-overview/window-constituent-elements.png)  
  
 창은 비클라이언트 영역과 클라이언트 영역의 두 영역으로 나뉩니다.  
  
 창의 *비클라이언트 영역은* 에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 구현 되며, 다음을 포함 하 여 대부분의 창에 공통적인 창 부분을 포함 합니다.  
  
- 테두리.  
  
- 제목 표시줄.  
  
- 아이콘.  
  
- 최소화, 최대화 및 복원 단추.  
  
- 닫기 단추.  
  
- 사용자가 창을 최소화, 최대화, 복원, 이동, 크기 조정 및 닫을 수 있는 메뉴 항목이 들어 있는 시스템 메뉴.  
  
 창의 *클라이언트 영역은* 창의 비클라이언트 영역에 있는 영역이 며 개발자가 메뉴 모음, 도구 모음 및 컨트롤과 같은 응용 프로그램 관련 콘텐츠를 추가 하는 데 사용 됩니다.  
  
 에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]창은 다음을 수행 하는 데 <xref:System.Windows.Window> 사용 하는 클래스에 의해 캡슐화 됩니다.  
  
- 창을 표시합니다.  
  
- 창의 크기, 위치 및 모양을 구성합니다.  
  
- 애플리케이션별 콘텐츠를 호스팅합니다.  
  
- 창의 수명을 관리합니다.  
  
<a name="DefiningAWindow"></a>   
## <a name="implementing-a-window"></a>창 구현  
 일반적인 창의 구현은 모양과 동작으로 구성 되며, *모양은* 창이 사용자에 게 표시 되는 방식을 정의 하 고 *동작은* 사용자가 상호 작용할 때 창이 작동 하는 방식을 정의 합니다. 에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]코드 또는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 태그를 사용 하 여 창의 모양 및 동작을 구현할 수 있습니다.  
  
 그러나 일반적으로 창의 모양은 태그를 사용 하 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 여 구현 되며, 해당 동작은 다음 예제와 같이 코드를 사용 하 여 구현 됩니다.  
  
 [!code-xaml[WindowsOverviewSnippets#MarkupAndCodeBehindWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 태그 파일 및 코드 숨김이 함께 작동 하도록 설정 하려면 다음이 필요 합니다.  
  
- 태그에서 요소는 `Window` `x:Class` 특성을 포함 해야 합니다. 응용 프로그램을 빌드할 때 `x:Class` 태그 파일에가 있으면 MSBuild (Microsoft build engine)가에서 <xref:System.Windows.Window> 파생 되 고 `x:Class` 특성으로 `partial` 지정 된 이름을 가진 클래스를 만듭니다. 이렇게 하려면 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 스키마에 대 한 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 네임 스페이스 선언을 추가 해야 합니다 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"` (). 생성 `partial` 된 클래스는 이벤트 `InitializeComponent` 를 등록 하 고 태그에 구현 된 속성을 설정 하기 위해 호출 하는 메서드를 구현 합니다.  
  
- 코드를 사용할 `partial` 때 클래스는 태그의 `x:Class` 특성으로 지정 되는 동일한 이름의 클래스 여야 하며에서 <xref:System.Windows.Window>파생 되어야 합니다. 이렇게 하면 응용 프로그램을 빌드할 때 태그 파일에 대해 생성 `partial` 되는 클래스와 코드 숨김이 연결 될 수 있습니다 ( [WPF 응용 프로그램 빌드](building-a-wpf-application-wpf.md)참조).  
  
- 코드 숨김으로 클래스는 <xref:System.Windows.Window> `InitializeComponent` 메서드를 호출 하는 생성자를 구현 해야 합니다. `InitializeComponent`는 태그 파일의 생성 `partial` 된 클래스에 의해 구현 되어 이벤트를 등록 하 고 태그에 정의 된 속성을 설정 합니다.  
  
> [!NOTE]
> 를 사용 <xref:System.Windows.Window> [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]하 여 프로젝트에 새를 추가 하는 경우 <xref:System.Windows.Window> 는 태그와 코드 숨김으로 모두 사용 하 여 구현 되며, 태그와 코드 숨김으로 연결을 만드는 데 필요한 구성을 포함 합니다. 여기에서 설명 합니다.  
  
 이 구성을 적용 하면 창의 모양을 태그에 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 정의 하 고 코드 숨김으로 동작을 구현 하는 데 집중할 수 있습니다. 다음 예제에서는 태그에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 구현 된 단추와 코드 숨김으로 구현 된 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 단추의 이벤트에 대 한 이벤트 처리기가 있는 창을 보여 줍니다.  
  
 [!code-xaml[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
<a name="ConfiguringWindowForMSBuild"></a>   
## <a name="configuring-a-window-definition-for-msbuild"></a>MSBuild에 대해 창 정의 구성  
 창을 구현 하는 방법에 따라 MSBuild에 대해 구성 되는 방식이 결정 됩니다. 태그와 코드 숨김으로 모두 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 사용 하 여 정의 된 창의 경우:  
  
- XAML 태그 파일은 MSBuild `Page` 항목으로 구성 됩니다.  
  
- 코드 숨겨진 파일은 MSBuild `Compile` 항목으로 구성 됩니다.  
  
 이는 다음 MSBuild 프로젝트 파일에 표시 됩니다.  
  
```xml  
<Project ...  
                xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    ...  
    <Page Include="MarkupAndCodeBehindWindow.xaml" />  
    <Compile Include=" MarkupAndCodeBehindWindow.xaml.cs" />  
    ...  
</Project>  
```  
  
 응용 프로그램 빌드 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 에 대 한 자세한 내용은 [WPF 응용 프로그램 빌드](building-a-wpf-application-wpf.md)를 참조 하세요.  
  
<a name="WindowLifetime"></a>   
## <a name="window-lifetime"></a>창 수명  
 다른 클래스와 마찬가지로 창에는 창이 열린 후 처음 인스턴스화될 때 시작하여, 열린 후 활성화 및 비활성화되고 최종적으로 닫힐 때까지의 기간인 수명이 있습니다.  

<a name="Opening_a_Window"></a>   
### <a name="opening-a-window"></a>창 열기  
 창을 열려면 먼저 다음 예제에서 설명하는 것처럼 창의 인스턴스를 만듭니다.  
  
 [!code-xaml[WindowsOverviewStartupEventSnippets#AppMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml#appmarkup)]  
  
 [!code-csharp[WindowsOverviewStartupEventSnippets#AppCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml.cs#appcodebehind)]  
  
 이 예제 `MarkupAndCodeBehindWindow` 에서는 <xref:System.Windows.Application.Startup> 이벤트가 발생할 때 발생 하는 응용 프로그램이 시작 될 때가 인스턴스화됩니다.  
  
 창이 인스턴스화될 때이에 대 한 참조가 <xref:System.Windows.Application> 개체에 의해 관리 되는 창 목록에 자동으로 추가 됩니다 (참조 <xref:System.Windows.Application.Windows%2A?displayProperty=nameWithType>). 또한 인스턴스화될 첫 번째 창은 기본적으로 주 응용 프로그램 창 <xref:System.Windows.Application> 으로 설정 됩니다 (참조 <xref:System.Windows.Application.MainWindow%2A?displayProperty=nameWithType>).  
  
 마지막으로 메서드를 <xref:System.Windows.Window.Show%2A> 호출 하 여 창을 엽니다. 결과는 다음 그림에 나와 있습니다.  
  
 ![창을 호출 하 여 열린 창입니다. Show](./media/wpf-windows-overview//window-opened-show-method.png)  
  
 를 호출 <xref:System.Windows.Window.Show%2A> 하 여 연 창은 모덜리스 창이 며,이 창은 응용 프로그램이 동일한 응용 프로그램에서 다른 창을 활성화할 수 있도록 하는 모드에서 작동 함을 의미 합니다.  
  
> [!NOTE]
> <xref:System.Windows.Window.ShowDialog%2A>대화 상자와 같은 창을 모달로 열기 위해가 호출 됩니다. 자세한 내용은 [대화 상자 개요](dialog-boxes-overview.md) 를 참조 하세요.  
  
 가 <xref:System.Windows.Window.Show%2A> 호출 되 면 창에서 사용자 입력을 받을 수 있도록 하는 인프라를 설정 하기 전에 초기화 작업을 수행 합니다. 창이 초기화 <xref:System.Windows.Window.SourceInitialized> 되 면 이벤트가 발생 하 고 창이 표시 됩니다.  
  
 바로 가기로를 <xref:System.Windows.Application.StartupUri%2A> 설정 하 여 응용 프로그램이 시작 될 때 자동으로 열리는 첫 번째 창을 지정할 수 있습니다.  
  
 [!code-xaml[WindowsOverviewSnippets#ApplicationStartupUriMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/App.xaml#applicationstartupurimarkup)]  
  
 응용 프로그램이 시작 되 면의 <xref:System.Windows.Application.StartupUri%2A> 값으로 지정 된 창이 모덜리스 창으로으로 열리고 내부적으로 해당 <xref:System.Windows.Window.Show%2A> 메서드를 호출 하 여 창이 열립니다.  
  
<a name="Ownership"></a>   
#### <a name="window-ownership"></a>창 소유권  
 메서드를 <xref:System.Windows.Window.Show%2A> 사용 하 여 연 창에는 해당 창을 만든 창과의 암시적 관계가 없습니다. 사용자가 다른 창에 독립적으로 상호 작용할 수 있습니다. 즉, 두 창에서 모두 다음 작업을 수행할 수 있습니다.  
  
- 창 중 하나에 <xref:System.Windows.Window.Topmost%2A> 속성이로 `true`설정 되어 있지 않은 경우 다른를 포함 합니다.  
  
- 다른 창에 영향을 주지 않고 최소화, 최대화 및 복원합니다.  
  
 일부 창은 해당 창을 여는 창과의 관계를 필요로 합니다. 예를 들어 IDE (통합 개발 환경) 응용 프로그램은 속성 창 및 도구 창을 열 수 있습니다 .이 창에서 일반적인 동작을 통해 해당 창을 만들 수 있습니다. 또한 이러한 창은 항상 해당 창을 만든 창과 함께 닫히고, 최소화되고, 최대화되고, 복원되어야 합니다. 이러한 관계는 한 창을 다른 창으로 만들고 *소유자*창에 대 한 참조로 *소유 창의* <xref:System.Windows.Window.Owner%2A> 속성을 설정 하 여 설정할 수 있습니다. 다음 예제에서 이를 확인할 수 있습니다.  
  
 [!code-csharp[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/CSharp/MainWindow.xaml.cs#setwindowownercode)]
 [!code-vb[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/visualbasic/mainwindow.xaml.vb#setwindowownercode)]  
  
 소유권이 설정된 후:  
  
- 소유 된 창은 해당 <xref:System.Windows.Window.Owner%2A> 속성의 값을 검사 하 여 소유자 창을 참조할 수 있습니다.  
  
- 소유자 창은 해당 <xref:System.Windows.Window.OwnedWindows%2A> 속성의 값을 검사 하 여 소유 하 고 있는 모든 창을 검색할 수 있습니다.  
  
<a name="Preventing"></a>   
#### <a name="preventing-window-activation"></a>창 활성화 방지  
 인터넷 메신저 스타일 응용 프로그램의 대화 창 또는 전자 메일 응용 프로그램의 알림 창과 같이 창이 표시 될 때 활성화 되지 않아야 하는 시나리오가 있습니다.  
  
 응용 프로그램에 표시 될 때 활성화 하지 않아야 하는 창이 있는 경우 <xref:System.Windows.Window.ShowActivated%2A> <xref:System.Windows.Window.Show%2A> 메서드를 처음으로 호출 `false` 하기 전에 해당 속성을로 설정할 수 있습니다. 이렇게 하면 다음과 같은 결과가 나타납니다.  
  
- 창이 활성화되지 않습니다.  
  
- 창의 <xref:System.Windows.Window.Activated> 이벤트는 발생 하지 않습니다.  
  
- 현재 활성 창이 활성 상태로 유지됩니다.  
  
 그러나 사용자가 클라이언트 영역이나 비클라이언트 영역을 클릭하여 창을 활성화하면 해당 창이 활성화됩니다. 이 경우:  
  
- 창이 활성화됩니다.  
  
- 창의 <xref:System.Windows.Window.Activated> 이벤트가 발생 합니다.  
  
- 이전에 활성 상태였던 창이 비활성화됩니다.  
  
- 이후 창의 <xref:System.Windows.Window.Deactivated> 및 <xref:System.Windows.Window.Activated> 이벤트는 사용자 동작에 대 한 응답으로 예상 대로 발생 합니다.  
  
<a name="Window_Activation"></a>   
### <a name="window-activation"></a>창 활성화  
 창이 처음 열리면 창이 활성 창이 됩니다 (를로 <xref:System.Windows.Window.ShowActivated%2A> `false`설정 하 여 표시 되지 않은 경우). *활성 창은* 키 입력 및 마우스 클릭과 같은 사용자 입력을 현재 캡처하는 창입니다. 창이 활성화 되 면 <xref:System.Windows.Window.Activated> 이벤트가 발생 합니다.  
  
> [!NOTE]
> 창이 처음 열릴 <xref:System.Windows.FrameworkElement.Loaded> 때 및 <xref:System.Windows.Window.ContentRendered> 이벤트는 <xref:System.Windows.Window.Activated> 이벤트가 발생 한 후에만 발생 합니다. 이 점을 염두에 두면가 발생할 때 <xref:System.Windows.Window.ContentRendered> 창이 효과적으로 열린 것으로 간주 될 수 있습니다.  
  
 창이 활성 창이 되면 사용자는 같은 애플리케이션의 다른 창을 활성화하거나 다른 애플리케이션을 활성화할 수 있습니다. 이 경우 현재 활성화 된 창이 비활성화 되 고 이벤트를 <xref:System.Windows.Window.Deactivated> 발생 시킵니다. 마찬가지로 사용자가 현재 비활성화 된 창을 선택 하면 창이 다시 활성화 되 고 <xref:System.Windows.Window.Activated> 발생 합니다.  
  
 <xref:System.Windows.Window.Activated> 및<xref:System.Windows.Window.Deactivated> 를 처리 하는 일반적인 이유 중 하나는 창이 활성 상태일 때만 실행 될 수 있는 기능을 사용 하거나 사용 하지 않도록 설정 하는 것입니다. 예를 들어 일부 창은 게임 및 비디오 플레이어를 포함하여 지속적인 사용자의 입력이나 주의가 필요한 대화식 콘텐츠를 표시합니다. 다음 예제는이 동작을 처리 <xref:System.Windows.Window.Activated> 하 고 <xref:System.Windows.Window.Deactivated> 구현 하는 방법을 보여 주는 간단한 비디오 플레이어입니다.  
  
 [!code-xaml[WindowsOverviewSnippets#ActivationDeactivationMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml#activationdeactivationmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml.cs#activationdeactivationcodebehind)]
 [!code-vb[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/CustomMediaPlayerWindow.xaml.vb#activationdeactivationcodebehind)]  
  
 다른 형식의 애플리케이션은 창이 비활성화되었을 때 계속 백그라운드에서 코드를 실행할 수 있습니다. 예를 들어 메일 클라이언트는 사용자가 다른 애플리케이션을 사용하고 있을 때 메일 서버를 계속 폴링할 수 있습니다. 이러한 애플리케이션에는 기본 창이 비활성화되었을 때 다른 동작 또는 추가 동작을 제공하기도 합니다. 메일 프로그램의 경우에 이것은 새 메일 항목을 받은 편지함에 추가하고 시스템 트레이에 알림 아이콘을 추가하는 작업을 의미할 수 있습니다. 알림 아이콘은 메일 창이 활성화 되지 않은 경우에만 표시 되어야 합니다 .이는 <xref:System.Windows.Window.IsActive%2A> 속성을 검사 하 여 확인할 수 있습니다.  
  
 백그라운드 작업이 완료 되 면 메서드를 호출 <xref:System.Windows.Window.Activate%2A> 하 여 사용자에 게 더 급하게 알림을 보낼 수 있습니다. 사용자가를 호출할 때 <xref:System.Windows.Window.Activate%2A> 활성화 된 다른 응용 프로그램과 상호 작용 하는 경우 창의 작업 표시줄 단추가 깜박입니다. 사용자가 현재 응용 프로그램과 상호 작용 하는 경우를 <xref:System.Windows.Window.Activate%2A> 호출 하면 창이 포그라운드로 전환 됩니다.  
  
> [!NOTE]
> <xref:System.Windows.Application.Activated?displayProperty=nameWithType> 및<xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> 이벤트를 사용 하 여 응용 프로그램 범위 활성화를 처리할 수 있습니다.  
  
<a name="Closing_a_Window"></a>   
### <a name="closing-a-window"></a>창 닫기  
 창의 수명은 사용자가 창을 닫을 때 끝나게 됩니다. 창은 다음을 포함하여 비클라이언트 영역의 요소를 사용하여 닫을 수 있습니다.  
  
- **시스템** 메뉴의 **닫기** 항목입니다.  
  
- ALT+F4 누르기.  
  
- **닫기** 단추를 누릅니다.  
  
 클라이언트 영역에 창을 닫기 위한 추가적인 메커니즘을 제공할 수 있으며 이 메커니즘에는 일반적으로 다음이 포함됩니다.  
  
- 일반적으로 주 응용 프로그램 창에 대 한 **파일** 메뉴의 **종료** 항목입니다.  
  
- 일반적으로 보조 응용 프로그램 창에 있는 **파일** 메뉴의 **닫기** 항목입니다.  
  
- 일반적으로 모달 대화 상자에서 **취소** 단추를 클릭 합니다.  
  
- 일반적으로 모덜리스 대화 상자에 있는 **닫기** 단추  
  
 이러한 사용자 지정 메커니즘 중 하나에 대 한 응답으로 창을 닫으려면 <xref:System.Windows.Window.Close%2A> 메서드를 호출 해야 합니다. 다음 예제에서는 **파일** 메뉴에서 **끝내기** 를 선택 하 여 창을 닫는 기능을 구현 합니다.  
  
 [!code-xaml[WindowsOverviewSnippets#WindowWithFileExitMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml#windowwithfileexitmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml.cs#windowwithfileexitcodebehind)]
 [!code-vb[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/WindowWithFileExit.xaml.vb#windowwithfileexitcodebehind)]  
  
 창이 닫히면 <xref:System.Windows.Window.Closing> 및 <xref:System.Windows.Window.Closed>의 두 이벤트를 발생 시킵니다.  
  
 <xref:System.Windows.Window.Closing>은 창이 닫히기 전에 발생 하며 창 닫기를 방지할 수 있는 메커니즘을 제공 합니다. 대개 창이 닫히면 안 되는 한 가지 이유는 창 콘텐츠에 수정된 데이터가 있는 경우입니다. 이 경우 <xref:System.Windows.Window.Closing> 에는 이벤트를 처리 하 여 데이터가 변경 되었는지 여부를 확인 하 고, 데이터를 저장 하지 않고 창을 닫을지 아니면 창 닫기를 취소할지를 사용자에 게 요청할 수 있습니다. 다음 예에서는 처리 <xref:System.Windows.Window.Closing>의 주요 측면을 보여 줍니다.  
  
 [!code-csharp[WindowClosingSnippets](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowClosingSnippets/CSharp/DataWindow.xaml.cs)]
 [!code-vb[WindowClosingSnippets](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowClosingSnippets/visualbasic/datawindow.xaml.vb)]  

 <xref:System.ComponentModel.CancelEventArgs> `Boolean` <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 이벤트 처리기에 전달 되는은 창이 닫히지 않도록 하기 `true` 위해 설정 하는 속성을 구현 합니다. <xref:System.Windows.Window.Closing>  
  
 가 <xref:System.Windows.Window.Closing> 처리 되지 않거나 처리 되었지만 취소 되지 않은 경우 창이 닫힙니다. 창이 실제로 닫히기 직전에 <xref:System.Windows.Window.Closed> 이 발생 합니다. 이 시점에서는 창 닫기를 방지할 수 없습니다.  
  
> [!NOTE]
> 주 응용 프로그램 창이 닫히거나 (참조 <xref:System.Windows.Application.MainWindow%2A>) 마지막 창이 닫히면 응용 프로그램은 자동으로 종료 되도록 구성할 수 있습니다. 자세한 내용은 <xref:System.Windows.Application.ShutdownMode%2A>를 참조하세요.  
  
 비클라이언트 및 클라이언트 영역에서 제공 하는 메커니즘을 통해 창을 명시적으로 닫을 수 있지만, 다음을 포함 하 여 응용 프로그램이 나 창의 다른 부분에서 동작의 결과로 창이 암시적으로 닫힐 수도 있습니다.  
  
- 사용자가 로그 오프 하거나 Windows를 종료 합니다.  
  
- 창의 소유자가 닫힙니다 (참조 <xref:System.Windows.Window.Owner%2A>).  
  
- 주 응용 프로그램 창이 닫혀 있고 <xref:System.Windows.Application.ShutdownMode%2A> 가 <xref:System.Windows.ShutdownMode.OnMainWindowClose>입니다.  
  
- <xref:System.Windows.Application.Shutdown%2A>가 호출된 경우  
  
> [!NOTE]
> 창을 닫은 뒤에는 다시 열 수 없습니다.  
  
<a name="Window_Lifetime_Events"></a>   
### <a name="window-lifetime-events"></a>창 수명 이벤트  
 다음 그림에서는 창의 수명에서 주 이벤트의 시퀀스를 보여 줍니다.  
  
 ![창의 수명으로 이벤트를 표시 하는 다이어그램입니다.](./media/wpf-windows-overview/window-lifetime-events.png)  
  
 다음 그림에서는 활성화 없이 표시 되는 창의 수명에서 주 이벤트의 시퀀스를 보여 줍니다 (<xref:System.Windows.Window.ShowActivated%2A> 창이 표시 되기 전에로 `false` 설정 됨).  
  
 ![활성화 하지 않고 창의 수명으로 이벤트를 표시 하는 다이어그램입니다.](./media/wpf-windows-overview/window-lifetime-no-activation.png)  
  
<a name="WindowLocation"></a>   
## <a name="window-location"></a>창 위치  
 창은 열릴 때 바탕 화면에 상대적인 x 및 y 크기의 위치를 가집니다. 이 위치는 <xref:System.Windows.Window.Left%2A> 각각 및 <xref:System.Windows.Window.Top%2A> 속성을 검사 하 여 확인할 수 있습니다. 이 속성을 설정하여 창의 위치를 변경할 수 있습니다.  
  
 다음 <xref:System.Windows.Window.WindowStartupLocation%2A> <xref:System.Windows.Window> 열거형값<xref:System.Windows.WindowStartupLocation> 중 하나로 속성을 설정 하 여 처음에 표시 되는의 초기 위치를 지정할 수도 있습니다.  
  
- <xref:System.Windows.WindowStartupLocation.CenterOwner>(기본값)  
  
- <xref:System.Windows.WindowStartupLocation.CenterScreen>  
  
- <xref:System.Windows.WindowStartupLocation.Manual>  
  
 로 <xref:System.Windows.WindowStartupLocation.Manual>시작 위치를 지정 <xref:System.Windows.Window.Left%2A> 하 고 및 <xref:System.Windows.Window.Top%2A> 속성을 설정 <xref:System.Windows.Window> 하지 않은 경우에는 Windows에서에 표시 되는 위치를 확인 합니다.  
  
<a name="Topmost_Windows_and_Z_Order"></a>   
### <a name="topmost-windows-and-z-order"></a>최상위 창 및 Z 순서  
 창에는 x 및 y 위치 이외에도 다른 창과 상대적인 수직 위치를 결정하는 z 차원의 위치도 있습니다. 이를 창의 z 순서라고 하며 여기에는 일반 z 순서와 최상위 z 순서의 두 가지 유형이 있습니다. *표준 z 순서* 에서 창의 위치는 현재 활성화 되어 있는지 여부에 따라 결정 됩니다. 기본적으로 창은 일반 z 순서로 배치됩니다. *위쪽 z 순서* 에서 창의 위치도 현재 활성 상태 인지 여부에 따라 결정 됩니다. 최상위 z 수준의 창은 항상 일반 z 순서 창의 위에 위치합니다. 창은 해당 <xref:System.Windows.Window.Topmost%2A> 속성을로 `true`설정 하 여 맨 위 z 순서에 있습니다.  
  
 [!code-xaml[WindowsOverviewSnippets#TopmostWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TopmostWindow.xaml#topmostwindowmarkup1)]  
  
 각 z 순서 안에서는 현재 활성화된 창이 같은 z 순서를 가진 다른 모든 창 위에 나타납니다.  
  
<a name="WindowSize"></a>   
## <a name="window-size"></a>창 크기  
 데스크톱 위치를 포함 하는 것 외에도 창의 크기는 다양 한 너비 및 높이 속성 및 <xref:System.Windows.Window.SizeToContent%2A>를 포함 하 여 여러 속성에 의해 결정 됩니다.  
  
 <xref:System.Windows.FrameworkElement.MinWidth%2A>, <xref:System.Windows.FrameworkElement.Width%2A> 및<xref:System.Windows.FrameworkElement.MaxWidth%2A> 은 창이 수명 동안 포함할 수 있는 너비 범위를 관리 하는 데 사용 되 고 다음 예제와 같이 구성 됩니다.  
  
 [!code-xaml[WindowsOverviewSnippets#WidthWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WidthWindow.xaml#widthwindowmarkup1)]  
  
 창 높이는 <xref:System.Windows.FrameworkElement.MinHeight%2A>, <xref:System.Windows.FrameworkElement.Height%2A>및 <xref:System.Windows.FrameworkElement.MaxHeight%2A>에서 관리 하며 다음 예제와 같이 구성 됩니다.  
  
 [!code-xaml[WindowsOverviewSnippets#HeightWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/HeightWindow.xaml#heightwindowmarkup1)]  
  
 다양한 너비 값과 높이 값이 각각 범위를 지정하고 있기 때문에, 크기 조정 가능한 창의 너비와 높이는 지정한 범위 내에서 임의의 크기로 설정될 수 있습니다. 현재 너비와 높이를 검색 하려면 및 <xref:System.Windows.FrameworkElement.ActualWidth%2A> <xref:System.Windows.FrameworkElement.ActualHeight%2A>를 각각 검사 합니다.  
  
 창의 너비와 높이를 창 내용의 크기에 맞게 조정 하려는 경우 다음 값을 포함 하는 <xref:System.Windows.Window.SizeToContent%2A> 속성을 사용할 수 있습니다.  
  
- <xref:System.Windows.SizeToContent.Manual>. 아무런 영향이 없습니다(기본값).  
  
- <xref:System.Windows.SizeToContent.Width>. 콘텐츠 너비에 맞춥니다. 이러한 효과는 <xref:System.Windows.FrameworkElement.MinWidth%2A> 및를 콘텐츠 너비와 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 동일 하 게 설정 하는 것과 같습니다.  
  
- <xref:System.Windows.SizeToContent.Height>. 콘텐츠 높이에 맞게 <xref:System.Windows.FrameworkElement.MinHeight%2A> 및 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 를 콘텐츠의 높이로 설정 하는 것과 동일한 효과를 가집니다.  
  
- <xref:System.Windows.SizeToContent.WidthAndHeight>. 콘텐츠 너비와 높이에 <xref:System.Windows.FrameworkElement.MinHeight%2A> 맞게 및 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 를 <xref:System.Windows.FrameworkElement.MinWidth%2A> 콘텐츠의 높이로 설정 하 고 및 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 를 콘텐츠의 너비로 설정 하는 것과 동일한 효과를 가집니다.  
  
 다음 예는 창이 처음 표시될 때 콘텐츠에 맞도록 수직 및 수평으로 크기를 자동으로 조정하는 창을 보여 줍니다.  
  
 [!code-xaml[WindowsOverviewSnippets#SizeToContentWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/SizeToContentWindow.xaml#sizetocontentwindowmarkup1)]  
  
 다음 예제에서는 코드에서 <xref:System.Windows.Window.SizeToContent%2A> 속성을 설정 하 여 창의 크기가 콘텐츠에 맞게 조정 되는 방법을 지정 하는 방법을 보여 줍니다.
  
 [!code-csharp[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/MainWindow.xaml.cs#setwindowsizetocontentpropertycode)]
 [!code-vb[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/mainwindow.xaml.vb#setwindowsizetocontentpropertycode)]  
  
<a name="OrderOfPrecedence"></a>   
## <a name="order-of-precedence-for-sizing-properties"></a>크기 조정 속성에 대한 우선 순위 순서  
 기본적으로 창의 다양한 크기 속성이 결합되어 크기 조정 가능한 창의 너비와 높이의 범위가 정의됩니다. 유효한 범위가 유지 <xref:System.Windows.Window> 되도록 하기 위해는 다음과 같은 우선 순위 순서를 사용 하 여 size 속성의 값을 평가 합니다.  
  
 **높이 속성:**  
  
1. <xref:System.Windows.FrameworkElement.MinHeight%2A?displayProperty=nameWithType>
  
2. <xref:System.Windows.FrameworkElement.MaxHeight%2A?displayProperty=nameWithType>
  
3. <xref:System.Windows.SizeToContent.Height?displayProperty=nameWithType>/<xref:System.Windows.SizeToContent.WidthAndHeight?displayProperty=nameWithType>
  
4. <xref:System.Windows.FrameworkElement.Height%2A?displayProperty=nameWithType>  
  
 **너비 속성:**  
  
1. <xref:System.Windows.FrameworkElement.MinWidth%2A?displayProperty=nameWithType>
  
2. <xref:System.Windows.FrameworkElement.MaxWidth%2A?displayProperty=nameWithType>
  
3. <xref:System.Windows.SizeToContent.Width?displayProperty=nameWithType>/<xref:System.Windows.SizeToContent.WidthAndHeight?displayProperty=nameWithType>
  
4. <xref:System.Windows.FrameworkElement.Width%2A?displayProperty=nameWithType>  
  
 우선 순위는 <xref:System.Windows.Window.WindowState%2A> 속성으로 관리 되는 최대화 된 창의 크기를 결정할 수도 있습니다.  
  
<a name="WindowState"></a>   
## <a name="window-state"></a>창 상태  
 크기 조정 가능한 창의 수명은 표준, 최소화 및 최대화의 세 가지 상태를 가질 수 있습니다. *표준* 상태의 창은 창의 기본 상태입니다. 크기 조정 가능 창이 표준 상태인 경우 사용자는 크기 조정 그립이나 테두리를 사용하여 창을 이동하고 크기 조정할 수 있습니다.  
  
 가로 <xref:System.Windows.Window.ShowInTaskbar%2A> 설정되어있으면최소화된상태의창이작업표시줄단추로축소되고,그렇지않으면가능한가장작은크기로축소하고바탕화면왼쪽아래에자신을다시할당할수`true`있습니다. 이러한 최소화된 창 유형은 테두리나 크기 조정 그립을 사용하여 크기 조정할 수 없습니다. 하지만 작업 표시줄에 표시되지 않은 최소화된 창은 바탕 화면에서 끌 수 있습니다.  
  
 상태가 *최대화* 된 창은 최대 크기 (최대 크기)로 확장 됩니다. 즉 <xref:System.Windows.FrameworkElement.MaxWidth%2A>, <xref:System.Windows.FrameworkElement.MaxHeight%2A>, 및 <xref:System.Windows.Window.SizeToContent%2A> 속성에 따라 크기가 커질 수 있습니다. 최소화된 창과 마찬가지로 최대화된 창은 크기 조정 그립을 사용하거나 테두리를 끌어서 크기 조정할 수 없습니다.  
  
> [!NOTE]
> 창의 <xref:System.Windows.Window.Top%2A> ,<xref:System.Windows.Window.Left%2A>, 및<xref:System.Windows.FrameworkElement.Height%2A> 속성 값은 창이 현재 최대화 되거나 최소화 된 경우에도 항상 표준 상태 값을 나타냅니다. <xref:System.Windows.FrameworkElement.Width%2A>  
  
 <xref:System.Windows.Window.WindowState%2A> 다음<xref:System.Windows.WindowState> 열거형 값 중 하나를 가질 수 있는 속성을 설정 하 여 창의 상태를 구성할 수 있습니다.  
  
- <xref:System.Windows.WindowState.Normal>(기본값)  
  
- <xref:System.Windows.WindowState.Maximized>  
  
- <xref:System.Windows.WindowState.Minimized>  
  
 다음 예제에서는 열릴 때 최대화되어 표시되는 창을 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[WindowsOverviewSnippets#WindowStateWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStateWindow.xaml#windowstatewindowmarkup1)]  
  
 일반적으로를 설정 <xref:System.Windows.Window.WindowState%2A> 하 여 창의 초기 상태를 구성 해야 합니다. 크기 조정 가능한 창이 표시되면 사용자는 창의 제목 표시줄에서 최소화, 최대화 및 복원 단추를 눌러 창 상태를 변경할 수 있습니다.  
  
<a name="WindowAppearance"></a>   
## <a name="window-appearance"></a>창 모양  
 단추, 레이블 및 텍스트 상자와 같은 창 특정 콘텐츠를 창에 추가하여 창의 클라이언트 영역의 모양을 변경할 수 있습니다. 비클라이언트 영역 <xref:System.Windows.Window> 을 구성 하기 위해는 창의 아이콘을 설정 하 고 <xref:System.Windows.Window.Title%2A> 제목을 <xref:System.Windows.Window.Icon%2A> 설정 하기 위한 여러 가지 속성을 제공 합니다.  
  
 또한 창의 크기 조정 모드, 창 스타일 및 바탕 화면 작업 표시줄에 단추로 표시될 것인지 여부를 구성하여 비클라이언트 영역 테두리의 모양과 동작을 변경할 수도 있습니다.  

<a name="Resize_Mode"></a>   
### <a name="resize-mode"></a>크기 조정 모드  
 <xref:System.Windows.Window.WindowStyle%2A> 속성에 따라 사용자가 창의 크기를 조정 하는 방법을 제어할 수 있습니다. 창 스타일 선택은 사용자가 마우스를 사용 하 여 창의 테두리를 끌어 창의 크기를 조정할 수 있는지 여부, **최소화**, **최대화**및 **크기 조정** 단추가 비클라이언트 영역에 나타나는지 여부 및 표시 되는지 여부에 영향을 줍니다. 사용.  
  
 <xref:System.Windows.Window.ResizeMode%2A> 다음<xref:System.Windows.ResizeMode> 열거형 값 중 하나일 수 있는 속성을 설정 하 여 창의 크기를 조정 하는 방법을 구성할 수 있습니다.  
  
- <xref:System.Windows.ResizeMode.NoResize>  
  
- <xref:System.Windows.ResizeMode.CanMinimize>  
  
- <xref:System.Windows.ResizeMode.CanResize>(기본값)  
  
- <xref:System.Windows.ResizeMode.CanResizeWithGrip>  
  
 와 <xref:System.Windows.Window.WindowStyle%2A>마찬가지로 창의 크기 조정 모드는 수명 중에 변경 될 가능성이 거의 없기 때문에 태그에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 설정 하는 것이 가장 좋습니다.  
  
 [!code-xaml[WindowsOverviewSnippets#ResizeModeWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ResizeModeWindow.xaml#resizemodewindowmarkup1)]  
  
 속성을 <xref:System.Windows.Window.WindowState%2A> 검사 하 여 창이 최대화, 최소화 또는 복원 되는지 여부를 검색할 수 있습니다.  
  
<a name="Window_Style"></a>   
### <a name="window-style"></a>창 스타일  
 창의 비클라이언트 영역에서 노출되는 테두리는 대부분의 애플리케이션에 적합합니다. 하지만 창의 유형에 따라 다른 유형의 테두리가 필요하거나 테두리가 전혀 필요 없는 경우가 있습니다.  
  
 창이 가져오는 테두리 형식을 제어 하려면 <xref:System.Windows.Window.WindowStyle%2A> <xref:System.Windows.WindowStyle> 열거형의 다음 값 중 하나를 사용 하 여 해당 속성을 설정 합니다.  
  
- <xref:System.Windows.WindowStyle.None>  
  
- <xref:System.Windows.WindowStyle.SingleBorderWindow>(기본값)  
  
- <xref:System.Windows.WindowStyle.ThreeDBorderWindow>  
  
- <xref:System.Windows.WindowStyle.ToolWindow>  
  
 다음 그림에서는 이러한 창 스타일의 효과를 보여 줍니다.  
  
 ![창 테두리 스타일에 대 한 그림입니다.](./media/wpf-windows-overview/window-border-styles.png)  
  
 태그 또는 코드 <xref:System.Windows.Window.WindowStyle%2A> 를 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 사용 하 여를 설정할 수 있습니다. 창의 수명 중에 변경 될 가능성이 거의 없기 때문에 태그를 사용 하 여 구성 하는 것이 가장 좋습니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 [!code-xaml[WindowsOverviewSnippets#WindowStyleWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStyleWindow.xaml#windowstylewindowmarkup1)]  
  
#### <a name="non-rectangular-window-style"></a>사각형이 아닌 창 스타일  
 뿐만 아니라 테두리 스타일 <xref:System.Windows.Window.WindowStyle%2A> 을 사용 해도 충분 하지 않은 경우도 있습니다. 예를 들어,와 같이 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 사각형이 아닌 테두리를 사용 하 여 응용 프로그램을 만들 수 있습니다.  
  
 예를 들어 다음 그림에 표시 된 음성 거품형 창을 살펴보겠습니다.  
  
 ![위로 끌기 라는 음성 거품형 창이 표시 됩니다.](./media/wpf-windows-overview/non-rectangular-window-figure.png)  
  
 <xref:System.Windows.Window.WindowStyle%2A> 속성을로 <xref:System.Windows.WindowStyle.None>설정 하 고 투명도에 대 한 특수 지원을 <xref:System.Windows.Window> 사용 하 여이 유형의 창을 만들 수 있습니다.  
  
 [!code-xaml[WindowsOverviewSnippets#TransparentWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TransparentWindow.xaml#transparentwindowmarkup1)]  
  
 값을 조합하여 사용하면 창이 완전히 투명하게 렌더링됩니다. 이 상태에서는 창의 비클라이언트 영역 표시(닫기 메뉴, 최소화, 최대화 및 복원 단추 등)를 사용할 수 없습니다. 따라서 직접 제공해야 합니다.  
  
<a name="Task_Bar_Presence"></a>   
### <a name="task-bar-presence"></a>작업 표시줄 표시  

창의 기본 모양에는 다음 그림에 표시 된 것과 같은 작업 표시줄 단추가 포함 됩니다.

 ![작업 표시줄 단추가 있는 창을 보여 주는 스크린샷](./media/wpf-windows-overview/window-taskbar-button.png)  
  
 일부 유형의 창에는 메시지 상자 및 대화 상자와 같은 작업 표시줄 단추가 없습니다 ( [대화 상자 개요](dialog-boxes-overview.md)참조). 속성을 <xref:System.Windows.Window.ShowInTaskbar%2A> 설정 하 여 창에 대 한 작업 표시줄 단추를 표시할지 여부를 제어할 수`true` 있습니다 (기본값).  
  
 [!code-xaml[WindowsOverviewSnippets#ShowInTaskbarWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ShowInTaskbarWindow.xaml#showintaskbarwindowmarkup1)]  
  
<a name="SecurityConsiderations"></a>   
## <a name="security-considerations"></a>보안 고려 사항  
 <xref:System.Windows.Window>인스턴스화할 `UnmanagedCode` 보안 권한이 필요 합니다. 로컬 시스템에 설치되어 실행되는 애플리케이션의 경우에는 애플리케이션에 허용된 권한 집합에 속합니다.  
  
 그러나이는 ClickOnce를 사용 하 여 인터넷 또는 로컬 인트라넷 영역에서 시작 된 응용 프로그램에 부여 된 사용 권한 집합을 벗어납니다. 따라서 사용자는 ClickOnce 보안 경고를 받게 되며 응용 프로그램에 대 한 권한 집합을 완전 신뢰로 승격 시켜야 합니다.  
  
 또한에서는 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 기본적으로 창이 나 대화 상자를 표시할 수 없습니다. 독립 실행형 응용 프로그램 보안 고려 사항에 대 한 설명은 [WPF 보안 전략-플랫폼 보안](../wpf-security-strategy-platform-security.md)을 참조 하세요.  
  
<a name="Other_Types_of_Windows"></a>   
## <a name="other-types-of-windows"></a>다른 유형의 창  
 <xref:System.Windows.Navigation.NavigationWindow>는 탐색 가능한 콘텐츠를 호스트 하도록 설계 된 창입니다. 자세한 내용은 [탐색 개요](navigation-overview.md)를 참조 하세요.  
  
 대화 상자는 기능 수행을 위해 사용자로부터 정보를 수집할 때 많이 사용됩니다. 예를 들어 사용자가 파일을 열려고 할 때 파일 **열기** 대화 상자는 일반적으로 응용 프로그램에서 사용자 로부터 파일 이름을 가져오는 데 표시 됩니다. 자세한 내용은 [대화 상자 개요](dialog-boxes-overview.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Window>
- <xref:System.Windows.MessageBox>
- <xref:System.Windows.Navigation.NavigationWindow>
- <xref:System.Windows.Application>
- [대화 상자 개요](dialog-boxes-overview.md)
- [WPF 응용 프로그램 빌드](building-a-wpf-application-wpf.md)
