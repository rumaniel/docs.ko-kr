---
title: WPF 전역화 및 지역화 개요
ms.date: 03/30/2017
helpviewer_keywords:
- globalization [WPF], about globalization
- localization [WPF], about localization
ms.assetid: 56e5a5c8-6c96-4d19-b8e1-a5be1dc564af
ms.openlocfilehash: e34b61e14db1e7839173658d71a70240d63c5f8a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917574"
---
# <a name="wpf-globalization-and-localization-overview"></a>WPF 전역화 및 지역화 개요

제품을 한 언어로만 제공하면 잠재적 고객 기반이 전 세계 65억 인구의 극히 일부로만 제한됩니다. 전 세계를 대상으로 하는 애플리케이션을 만들려는 경우 가장 뛰어나고 경제적으로 고객에게 다가갈 수 있는 방법 중 하나는 바로 제품의 비용 효율적인 지역화입니다.

이 개요에서는의 세계화 및 지역화 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에 대해 소개 합니다. 전역화는 여러 위치에서 수행되는 애플리케이션의 디자인 및 개발 작업입니다. 예를 들어 전역화는 여러 문화권의 사용자를 위해 지역화된 사용자 인터페이스와 국가별 데이터를 지원합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]자동 레이아웃, 위성 어셈블리, 지역화 된 특성 및 주석 처리를 포함 하 여 세계화 된 디자인 기능을 제공 합니다.

지역화는 애플리케이션 리소스를 애플리케이션에서 지원할 각 문화권에 맞는 지역화된 버전으로 번역하는 작업입니다. 에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]지역화할 때 <xref:System.Windows.Markup.Localizer> 네임 스페이스에서 api를 사용 합니다. 이러한 Api는 [LocBaml 도구 샘플](https://go.microsoft.com/fwlink/?LinkID=160016) 명령줄 도구를 구동 합니다. LocBaml을 빌드 및 사용 하는 방법에 대 한 자세한 내용은 [응용 프로그램 지역화](how-to-localize-an-application.md)를 참조 하세요.

## <a name="best-practices-for-globalization-and-localization-in-wpf"></a>WPF를 위한 최선의 전역화 및 지역화 방법

이 단원에서 제공 하는 UI 디자인 및 지역화 관련 팁을 따라에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기본적으로 제공 되는 세계화 및 지역화 기능을 최대한 활용할 수 있습니다.

### <a name="best-practices-for-wpf-ui-design"></a>최선의 WPF UI 디자인 방법

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기반[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]을 설계할 때 다음과 같은 모범 사례를 구현 하는 것이 좋습니다.

- 에서를 작성 합니다. 코드 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 에서를 만들지 마십시오. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 를 사용 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]하 여를 만드는 경우 기본 제공 지역화 api를 통해 노출 합니다.

- 콘텐츠 레이아웃에 절대 위치 및 고정 크기를 사용 하지 마십시오. 대신 상대 또는 자동 크기 조정을 사용 합니다.

  - 너비 <xref:System.Windows.Window.SizeToContent%2A> 와 높이를 사용 하 고로 `Auto`설정 합니다.

  - 를 사용 <xref:System.Windows.Controls.Canvas> 하 여를 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]레이아웃 하지 마십시오.

  - 및 <xref:System.Windows.Controls.Grid> 크기 공유 기능을 사용 합니다.

- 지역화된 텍스트는 공간을 더 많이 필요로 하는 경우가 많으므로 여분의 공간을 여백으로 남겨 둡니다. 여분의 공간을 통해 여분의 문자를 표현할 수 있습니다.

- 클리핑을 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 방지 <xref:System.Windows.Controls.TextBlock> 하려면 on을 사용 하도록 설정 합니다.

- `xml:lang` 특성을 설정합니다. 이 특성은 특정 요소 및 해당 자식 요소의 문화권을 설명 합니다. 이 속성의 값은의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]여러 기능에 대 한 동작을 변경 합니다. 예를 들어 하이픈 넣기, 맞춤법 검사, 숫자 대체, 복잡한 스크립트 셰이핑 및 글꼴 대체의 동작을 변경합니다. [XAML에서 xml: Lang 처리](../../xaml-services/xml-lang-handling-in-xaml.md)를 설정 하는 방법에 대 한 자세한 내용은 [WPF 용 전역화](globalization-for-wpf.md) 를 참조 하세요.

- 다양 한 언어에 사용 되는 글꼴을 보다 효율적으로 제어 하기 위해 사용자 지정 된 복합 글꼴을 만듭니다. 기본적으로에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Windows\Fonts 디렉터리에 globaluserinterface. 복합 글꼴을 사용 합니다.

- 오른쪽에서 왼쪽 형식으로 텍스트를 표시 하는 문화권에서 지역화할 수 있는 탐색 응용 프로그램을 만드는 경우 페이지가에서 상속 <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection> <xref:System.Windows.Navigation.NavigationWindow>되지 않도록 모든 페이지의를 명시적으로 설정 합니다.

- 브라우저 외부에서 호스트 되는 독립 실행형 탐색 응용 프로그램을 만드는 경우 초기 응용 프로그램 <xref:System.Windows.Application.StartupUri%2A> <xref:System.Windows.Navigation.NavigationWindow> 의를 `<Application StartupUri="NavigationWindow.xaml">`페이지 대신로 설정 합니다 (예:). 이 디자인을 사용 하면 창과 탐색 <xref:System.Windows.FlowDirection> 모음의를 변경할 수 있습니다. 자세한 내용 및 예제는 [세계화 홈 페이지 샘플](https://go.microsoft.com/fwlink/?LinkID=159990)을 참조 하세요.

### <a name="best-practices-for-wpf-localization"></a>WPF 지역화 모범 사례

기반 응용 프로그램 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]을 지역화 하는 경우 다음 모범 사례를 구현 하는 것이 좋습니다.

- 지역화 주석을 사용 하 여 지역화 담당자에 게 추가 컨텍스트를 제공 합니다.

- 요소에 대 한 속성을 선택적으로 생략 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 하는 대신 지역화 특성을 사용 하 여 지역화를 제어 합니다. 자세한 내용은 [지역화 특성 및 주석](localization-attributes-and-comments.md) 을 참조 하세요.

- 및 `msbuild -t:updateuid` <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]를 사용 하 여에서 속성을 추가 하 고 확인 합니다. `-t:checkuid` 속성 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 을 사용 하 여 개발과 지역화 간의 변경 내용을 추적 합니다. <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>속성을 통해 새 개발 변경 내용을 지역화할 수 있습니다. 에 속성 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]을 수동으로 추가 하는 경우이 태스크는 일반적으로 지루한 작업이 더 정확 하지 않습니다.

  - 지역화를 시작한 후에 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 는 속성을 편집 하거나 변경 하지 마십시오.

  - 중복 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성을 사용 하지 마십시오 (복사 및 붙여넣기 명령을 사용 하는 경우이 팁을 명심).

  - AssemblyInfo. *의 `[assembly: NeutralResourcesLanguage("en-US",   UltimateResourceFallbackLocation.Satellite)]` 위치를설정하여대체(예:)에적합한언어를지정합니다.`UltimateResourceFallback`

    프로젝트 파일에서 태그를 `<UICulture>` 생략 하 여 주 어셈블리에 소스 언어를 포함 하도록 결정 한 경우 `UltimateResourceFallback` 위치를 위성이 `[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.MainAssembly)]`아닌 주 어셈블리로 설정 합니다 (예:).

## <a name="localize-a-wpf-application"></a>WPF 애플리케이션 지역화

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 지역화할 때 몇 가지 옵션을 사용할 수 있습니다. 예를 들어 응용 프로그램의 지역화할 수 있는 리소스를 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 파일에 바인딩하거나, 지역화할 수 있는 텍스트를 resx 테이블에 저장 하거나, 지역화 담당자가 파일을 사용할 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 수 있습니다. 이 섹션에서는 다양 한 이점을 제공 하는 BAML 형태의 XAML을 사용 하는 지역화 워크플로에 대해 설명 합니다.

- 빌드한 후에 지역화할 수 있습니다.

- 개발 하는 동시에 지역화할 수 있도록 이전 버전의 BAML XAML에서 지역화를 사용 하 여 최신 버전의 BAML XAML 버전으로 업데이트할 수 있습니다.

- BAML 형식의 XAML은의 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]컴파일된 형태 이기 때문에 컴파일 시간에 원래 소스 요소 및 의미 체계의 유효성을 검사할 수 있습니다.

### <a name="localization-build-process"></a>지역화 빌드 프로세스

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 개발할 때 지역화에 대 한 빌드 프로세스는 다음과 같습니다.

- 개발자는 응용 프로그램을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 만들고 전역화 합니다. 프로젝트 파일에서 개발자는 응용 프로그램 `<UICulture>en-US</UICulture>` 을 컴파일할 때 언어 중립적인 주 어셈블리가 생성 되도록를 설정 합니다. 이 어셈블리에는 지역화 가능한 모든 리소스가 포함된 위성 .resources.dll 파일이 있습니다. 지역화 Api가 주 어셈블리에서의 추출을 지원 하므로 필요에 따라 주 어셈블리에서 소스 언어를 유지할 수 있습니다.

- 파일이 빌드로 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 컴파일되면은 BAML 형식의 XAML로 변환 됩니다. 문화권 `MyDialog.exe` 및 문화권 종속 (영어) `MyDialog.resources.dll` 파일은 영어를 통해 고객에 게 릴리스됩니다.

### <a name="localization-workflow"></a>지역화 워크플로

지역화 되지 않은 `MyDialog.resources.dll` 파일이 작성 된 후 지역화 프로세스가 시작 됩니다. 원래 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] <xref:System.Windows.Markup.Localizer>의 요소와 속성은의 api를 사용 하 여 BAML 형식의 XAML에서 키-값 쌍으로 추출 됩니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 지역화 담당자는 키/값 쌍을 사용하여 애플리케이션을 지역화합니다. 지역화가 완료된 후 새 값에서 새 .resource.dll을 생성할 수 있습니다.

키-값 쌍 `x:Uid` 의 키는 개발자가 원래 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에 배치 하는 값입니다. 이러한 `x:Uid` 값을 통해 API는 지역화 중 개발자와 지역화 담당자 간에 발생 하는 변경 내용을 추적 하 고 병합할 수 있습니다. 예를 들어, 지역화 담당자가 지역화 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 를 시작한 후 개발자가를 변경 하는 경우 최소한의 번역 작업이 손실 되도록 개발 변경 내용을 이미 완료 된 지역화 작업과 병합할 수 있습니다.

다음 그래픽은 BAML 양식의 XAML을 기반으로 하는 일반적인 지역화 워크플로를 보여 줍니다. 이 다이어그램에서는 개발자가 응용 프로그램을 영어로 작성 하는 것으로 가정 합니다. 개발자가 WPF 애플리케이션을 만들고 전역화합니다. 프로젝트 파일에서 개발자 `<UICulture>en-US</UICulture>` 는 빌드 시 지역화 가능한 모든 리소스를 포함 하는 위성 .resources .dll을 사용 하 여 언어 중립 주 어셈블리를 생성 합니다. 또는 WPF 지역화 API가 주 어셈블리에서의 추출을 지원하므로 주 어셈블리에서 소스 언어를 유지할 수 있습니다. 빌드 프로세스 후 XAML이 BAML로 컴파일됩니다. 문화권에 중립적인 MyDialog.exe.resources.dll이 영어권 고객에게 제공됩니다.

![지역화 워크플로를 보여 주는 다이어그램입니다.](./media/wpf-globalization-and-localization-overview/localization-workflow.png)

![지역화 되지 않은 워크플로를 보여 주는 다이어그램입니다.](./media/wpf-globalization-and-localization-overview/unlocalized-workflow.png)

## <a name="examples-of-wpf-localization"></a>WPF 지역화 예제

이 섹션에는 응용 프로그램을 빌드하고 지역화 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하는 방법을 이해 하는 데 유용한 지역화 된 응용 프로그램의 예가 포함 되어 있습니다.

#### <a name="run-dialog-box-example"></a>실행 대화 상자 예제

다음 그림은 **실행** 대화 상자 샘플의 출력을 보여 줍니다.

**영어:**

![영어 실행 대화 상자를 보여 주는 스크린샷](./media/wpf-globalization-and-localization-overview/run-dialog-box-english.png)

**독일어:**

![독일어 실행 대화 상자를 보여 주는 스크린샷](./media/wpf-globalization-and-localization-overview/run-dialog-box-german.png)

**전역 실행 대화 상자 디자인**

이 예에서는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]및 를 사용 하 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 여 실행 대화 상자를 생성 합니다. 이 대화 상자는 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 시작 메뉴에서 사용할 수 있는 **실행** 대화 상자와 동일 합니다.

전역 대화 상자를 만들 때 주의해야 할 점은 다음과 같습니다.

**자동 레이아웃**

*Window1.xaml:*

`<Window SizeToContent="WidthAndHeight">`

이전 Window 속성이 창의 크기를 콘텐츠 크기에 맞게 자동으로 조정합니다. 이 속성은 지역화한 후 크기가 증가한 콘텐츠가 창에서 잘리는 것을 방지하며, 지역화한 후 콘텐츠 크기가 줄어들 때 생기는 불필요한 공간도 제거합니다.

`<Grid x:Uid="Grid_1">`

<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>속성은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 지역화 api가 제대로 작동 하기 위해 필요 합니다.

이러한 api는 지역화 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] api에서 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]의 개발과 지역화 간의 변경 내용을 추적 하는 데 사용 됩니다. <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>속성을 사용 하면 최신 버전 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 의를의 이전 지역화 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]와 병합할 수 있습니다. 명령 셸에서를 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 실행 `msbuild -t:updateuid RunDialog.csproj` 하 여 속성을 추가 합니다. 이 방법은 속성을 수동으로 추가 하 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 는 것이 일반적으로 시간이 많이 걸리고 정확도가 낮으므로 속성을 추가 하는 것이 좋습니다. 을 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 실행`msbuild -t:checkuid RunDialog.csproj`하 여 속성이 올바르게 설정 되었는지 확인할 수 있습니다.

는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] <xref:System.Windows.Controls.Grid> 의 자동[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]레이아웃을 활용 하는 데 유용한 컨트롤인 컨트롤을 사용 하 여 구성 됩니다. 대화 상자는 세 개의 행과 다섯 개의 열로 나뉩니다. 행 및 열 정의 중 하나의 크기가 고정 되어 있지 않습니다. 따라서 각 셀 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 에 배치 되는 요소는 지역화 중 크기를 늘리거나 줄일 수 있습니다.

[!code-xaml[GlobalizationRunDialog#GridColumnDef](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef)]

**Open:** label 및 <xref:System.Windows.Controls.ComboBox> 가 배치 되는 처음 두 열은 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 총 너비의 10%를 사용 합니다.

[!code-xaml[GlobalizationRunDialog#GridColumnDef2](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef2)]

이 예에서는의 <xref:System.Windows.Controls.Grid>공유 크기 조정 기능을 사용 합니다. 마지막 세 열은 자신을 동일한 <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A>에 배치 하 여이를 활용 합니다. 속성의 이름에서 알 수 있듯이 이 속성을 통해 열은 같은 크기를 공유할 수 있습니다. 따라서 "찾아보기 ..." 긴 문자열 "찾아보기 ..."로 지역화 된 모든 단추는 작은 "확인" 단추를 포함 하는 대신 너비가 커지고 "찾아보기 ..." 단추만.

**xml:lang**

`xml:lang="en-US"`

의[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]루트 요소에 배치 된 [XAML의 xml: lang 처리](../../xaml-services/xml-lang-handling-in-xaml.md) 를 확인 합니다. 이 속성은 해당 요소 및 자식의 문화권을 설명합니다. 이 값은의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 여러 기능에서 사용 되며 지역화 하는 동안 적절 하 게 변경 해야 합니다. 이 값은 단어 하이픈 넣기와 맞춤법 검사에 사용할 언어 사전을 변경합니다. 또한 숫자의 표시 및 글꼴 대체 시스템에서 사용할 글꼴을 선택하는 방법에도 영향을 줍니다. 마지막으로, 속성은 숫자 표시 방식과 복잡한 스크립트에 포함된 텍스트의 모양이 지정되는 방식에 영향을 줍니다. 기본값은 "en-US"입니다.

**위성 리소스 어셈블리 빌드**

*.csproj:*

파일을 편집 하 고 다음 태그를 무조건 무조건 `<PropertyGroup>`에 추가 합니다. `.csproj`

`<UICulture>en-US</UICulture>`

`UICulture` 값이 추가 된 것을 볼 수 있습니다. En-us와 같은 유효한 <xref:System.Globalization.CultureInfo> 값으로 설정 된 경우 프로젝트를 빌드하면 지역화 가능한 모든 리소스가 포함 된 위성 어셈블리가 생성 됩니다.

`<Resource Include="RunIcon.JPG">`

`<Localizable>False</Localizable>`

`</Resource>`

는 `RunIcon.JPG` 모든 문화권에서 동일 하 게 표시 되기 때문에 지역화할 필요가 없습니다. `Localizable`는 위성 어셈블리 `false` 대신 언어 중립적 주 어셈블리에 유지 되도록로 설정 됩니다. 모든 컴파일 이외의 리소스의 기본값은로 `Localizable` `true`설정 됩니다.

**실행 대화 상자 지역화**

**구문 분석**

애플리케이션을 빌드한 후 지역화의 첫 번째 단계는 위성 어셈블리에서 지역화할 수 있는 리소스를 구문 분석하는 것입니다. 이 항목에서는 [Locbaml 도구 샘플](https://go.microsoft.com/fwlink/?LinkID=160016)에서 찾을 수 있는 샘플 locbaml 도구를 사용 합니다. LocBaml은 지역화 프로세스에 적합한 지역화 도구의 빌드에 도움을 주기 위한 샘플 도구입니다. LocBaml을 사용 하 여 다음을 실행 하 여 구문 분석 합니다. **LocBaml/Parse RunDialog. .resources:** "RUNDIALOG. .csv" 파일을 생성 합니다.

**지역화**

유니코드를 지원하는 CSV 편집기 중 적절한 것을 사용하여 이 파일을 편집합니다. 지역화 범주가 “None”인 모든 항목을 필터링합니다. 다음과 같은 항목이 표시되어야 합니다.

|리소스 키|지역화 범주|값|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|단추|확인|
|Button_2:System.Windows.Controls.Button.$Content|단추|취소|
|Button_3:System.Windows.Controls.Button.$Content|단추|찾아보기...|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|ComboBox||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|텍스트|프로그램, 폴더, 문서 또는 인터넷 리소스의 이름을 입력하면 Windows에서 열립니다.|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|텍스트|열기:|
|Window_1:System.Windows.Window.Title|제목|실행|

애플리케이션을 독일어로 지역화하려면 다음과 같이 번역해야 합니다.

|리소스 키|지역화 범주|값|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|단추|확인|
|Button_2:System.Windows.Controls.Button.$Content|단추|Abbrechen|
|Button_3:System.Windows.Controls.Button.$Content|단추|Durchsuchen…|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|ComboBox||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|텍스트|Geben Sie den Namen eines Programms, Ordners, Dokuments oder einer Internetresource an.|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|텍스트|Öffnen:|
|Window_1:System.Windows.Window.Title|제목|실행|

**생성**

지역화의 마지막 단계에서는 새로 지역화된 위성 어셈블리를 만듭니다. 이렇게 하려면 다음 LocBaml 명령을 사용합니다.

**LocBaml.exe /generate RunDialog.resources.dll /trans:RunDialog.resources.dll.CSV /out: . /cul:de-DE**

독일어 창에서이 리소스 .dll이 주 어셈블리 옆의 de 폴더에 배치 되는 경우이 리소스는 en-us 폴더에 있는 대신 자동으로 로드 됩니다. 이 테스트를 위해 독일어 버전의 windows가 설치 되어 있지 않은 경우에는 사용 중인 창의 문화권 (예: `en-US`)으로 문화권을 설정 하 고 원래 리소스 DLL을 바꿉니다.

**위성 리소스 로드**

|MyDialog.exe|en-US\MyDialog.resources.dll|de-DE\MyDialog.resources.dll|
|------------------|------------------------------------|------------------------------------|
|코드|원본 영어 BAML|지역화된 BAML|
|문화권에 중립적인 리소스|영어로 된 기타 리소스|독일어로 지역화된 기타 리소스|

.NET framework는 응용 프로그램의 `Thread.CurrentThread.CurrentUICulture`을 기반으로 로드할 위성 리소스 어셈블리를 자동으로 선택 합니다. 기본값은 Windows OS의 문화권입니다. 따라서 독일어 창을 사용 하는 경우 de-DE\MyDialog.resources.dll가 로드 되 고 영어 창을 사용 하는 경우 en-US\MyDialog.resources.dll가 로드 됩니다. 프로젝트의 AssemblyInfo.*에 NeutralResourcesLanguage를 지정하여 애플리케이션에 대한 최종 대체 리소스를 설정할 수 있습니다. 예를 들면 다음과 같이 지정할 수 있습니다.

`[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]`

그러면 de-DE\MyDialog.resources.dll 또는 de\MyDialog.resources.dll을 모두 사용할 수 없는 경우 en-US\MyDialog.resources.dll이 독일어 Windows에 사용됩니다.

### <a name="microsoft-saudi-arabia-homepage"></a>Microsoft 사우디아라비아 홈페이지

다음 그래픽에서는 영어 및 아랍어 홈페이지를 보여 줍니다. 이러한 그래픽을 생성 하는 전체 샘플은 [세계화 홈 페이지 샘플](https://go.microsoft.com/fwlink/?LinkID=159990)을 참조 하세요.

**영어:**

![영어 홈 페이지를 보여 주는 스크린샷](./media/wpf-globalization-and-localization-overview/english-home-page-sample.jpg)

**아랍어:**

![아랍어 홈 페이지를 보여 주는 스크린샷](./media/wpf-globalization-and-localization-overview/arabic-home-page-sample.jpg)

### <a name="designing-a-global-microsoft-home-page"></a>글로벌 Microsoft 홈 페이지 디자인

이 Microsoft 사우디아라비아 웹 사이트 샘플에서는 RightToLeft 언어를 위해 제공되는 전역화 기능을 보여 줍니다. 히브리어 및 아랍어와 같은 언어는 오른쪽에서 왼쪽으로 읽는 순서를 가지 므로 레이아웃이 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 영어와 같이 왼쪽에서 오른쪽으로 배치 되는 언어와 매우 다르게 배치 되어야 하는 경우가 많습니다. 왼쪽에서 오른쪽으로 읽는 언어를 오른쪽에서 왼쪽으로 읽는 언어로 또는 그 반대로 지역화하는 작업은 꽤 까다로울 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 이러한 지역화를 훨씬 쉽게 수행할 수 있도록 디자인되었습니다.

**FlowDirection**

*Homepage.xaml:*

[!code-xaml[GlobalizationHomepage#Homepage](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#homepage)]

에 대 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 한 <xref:System.Windows.Controls.Page>속성을 확인 합니다. 이 속성을로 <xref:System.Windows.FlowDirection.RightToLeft> 변경 하면 <xref:System.Windows.Controls.Page> 및 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 해당 자식 요소의이 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 변경 되어 아랍어 사용자가 필요로 하는 레이아웃을 오른쪽에서 왼쪽으로 이동 합니다. 모든 요소에 대해 explicit <xref:System.Windows.FrameworkElement.FlowDirection%2A> 를 지정 하 여 상속 동작을 재정의할 수 있습니다. 속성 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 은 모든 <xref:System.Windows.FrameworkElement> 또는 문서 관련 요소에서 사용할 수 있으며의 <xref:System.Windows.FlowDirection.LeftToRight>암시적 값이 있습니다.

루트가 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 변경 될 때 배경 그라데이션 브러시도 올바르게 대칭 이동 되는지 확인 합니다.

**FlowDirection="LeftToRight"**

![왼쪽에서 오른쪽으로 그라데이션 흐름을 보여 주는 스크린샷](./media/wpf-globalization-and-localization-overview/gradient-flow-left-right.png)

**FlowDirection="RightToLeft"**

![오른쪽에서 왼쪽으로 그라데이션 흐름을 보여 주는 스크린샷](./media/wpf-globalization-and-localization-overview/gradient-flow-right-left.png)

**패널 및 컨트롤에 고정 크기 사용 피하기**

[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 위의<xref:System.Windows.Controls.DockPanel>전체에 대해 지정 된 고정 너비와 높이를 제외 하 고는 다른 고정 차원이 없습니다. 지역화된 텍스트가 소스 텍스트보다 길어서 잘리는 것을 방지하기 위해 고정된 크기를 사용하지 않도록 하세요. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 패널 및 컨트롤은 포함된 콘텐츠에 따라 자동으로 크기가 조정됩니다. 또한 대부분의 컨트롤에는 더 많은 제어를 위해 설정할 수 있는 최소 및 최대 차원이 있습니다 (예: MinWidth = "20"). 를 사용 하 여 '\*' (예:)를 `Width="0.25*"`사용 하거나 셀 크기 공유 기능을 사용 하 여 상대 너비와 높이를 설정할 수도 있습니다. <xref:System.Windows.Controls.Grid>

**지역화 주석**

콘텐츠가 모호하여 번역하기 어려운 경우도 많이 있습니다. 개발자나 디자이너는 지역화 주석을 통해 지역화 담당자에게 추가적인 컨텍스트 및 주석을 제공할 수 있습니다. 예를 들어 아래의 Localization.Comments에서는 문자 ‘&#124;’의 사용을 명확하게 설명합니다.

[!code-xaml[GlobalizationHomepage#LocalizationComment](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcomment)]

이 주석은 TextBlock_1's 콘텐츠와 연결 되며 LocBaml 도구의 경우 ( [응용 프로그램 지역화](how-to-localize-an-application.md)참조) 출력 .csv 파일의 TextBlock_1 행에 있는 6 번째 열에 표시 될 수 있습니다.

|리소스 키|범주|가독성|수정 가능성|주석|값|
|-|-|-|-|-|-|
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|텍스트|true|true|이 문자는 장식 규칙으로 사용됩니다.|&#124;|

다음 구문을 사용하여 주석을 요소의 속성 또는 콘텐츠에 배치할 수 있습니다.

[!code-xaml[GlobalizationHomepage#LocalizationCommentsProp](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcommentsprop)]

**지역화 특성**

개발자 또는 지역화 관리자는 지역화 담당자가 읽고 수정할 수 있는 컨트롤을 필요로 할 수 있습니다. 예를 들어 회사 이름이나 법적 고지문은 번역하지 않아야 할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 지역화 도구가 요소를 잠그거나, 숨기거나, 정렬할 때 사용할 수 있는 요소의 콘텐츠나 속성의 가독성, 수정 가능 여부 및 범주를 설정할 수 있는 특성을 제공합니다. 자세한 내용은 <xref:System.Windows.Localization.Attributes%2A>을 참조하세요. 이 샘플의 목적상 LocBaml 도구는 이러한 특성의 값만 출력합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤은 모두 이러한 특성에 대해 기본값을 사용하지만 이를 재정의할 수 있습니다. 예를 들어 다음 예제에서는에 대 한 `TextBlock_1` 기본 지역화 특성을 재정의 하 고 지역화 담당자에 대해 콘텐츠를 읽을 수는 있지만 수정할 수 없도록 설정 합니다.

[!code-xaml[LocalizationComAtt#LocalizationAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributes)]

가독성 및 수정 가능성 특성 외에도에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 지역화 담당자에 게 더 많은 컨텍스트를<xref:System.Windows.LocalizationCategory>제공 하는 데 사용할 수 있는 일반적인 UI 범주 ()의 열거형을 제공 합니다. 플랫폼 컨트롤의 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기본 범주도에서 재정의할 수 있습니다.

[!code-xaml[LocalizationComAtt#LocalizationAttributesOverridden](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributesoverridden)]

에서 제공 하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기본 지역화 특성은 코드를 통해 재정의할 수도 있으므로 사용자 지정 컨트롤에 대 한 올바른 기본값을 올바르게 설정할 수 있습니다. 예를 들어:

```csharp
[Localizability(Readability = Readability.Readable, Modifiability=Modifiability.Unmodifiable, LocalizationCategory.None)]
public class CorporateLogo : TextBlock
{
    // ...
}
```

에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 설정 된 인스턴스별 특성은 사용자 지정 컨트롤에 대 한 코드에 설정 된 값 보다 우선 적용 됩니다. 특성 및 주석에 대 한 자세한 내용은 [지역화 특성 및 주석](localization-attributes-and-comments.md)을 참조 하세요.

**글꼴 대체 및 복합 글꼴**

지정 된 코드 포인트 범위 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 를 지원 하지 않는 글꼴을 지정 하는 경우는 Windows\Fonts 디렉터리에 있는 전역 사용자 compositefont를 사용 하 여 수행 하는 것으로 자동으로 대체 됩니다. 복합 글꼴은 다른 글꼴과 마찬가지로 작동 하며 요소의 `FontFamily` 를 설정 하 여 명시적으로 사용할 수 있습니다 (예를 들어, `FontFamily="Global User Interface"`). 복합 글꼴을 직접 만들고 특정 코드 포인트 범위와 언어에 사용할 글꼴을 지정하여 글꼴 대체 기본 설정을 직접 지정할 수 있습니다.

복합 글꼴에 대 한 자세한 내용은 <xref:System.Windows.Media.FontFamily>을 참조 하십시오.

**Microsoft 홈페이지 지역화**

실행 대화 상자와 동일한 단계를 사용하여 이 애플리케이션을 지역화할 수 있습니다. 아랍어의 지역화 된 .csv 파일은 [세계화 홈 페이지 샘플](https://go.microsoft.com/fwlink/?LinkID=159990)에서 사용할 수 있습니다.
