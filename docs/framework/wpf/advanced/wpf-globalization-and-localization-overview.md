---
title: WPF 전역화 및 지역화 개요
ms.date: 03/30/2017
helpviewer_keywords:
- globalization [WPF], about globalization
- localization [WPF], about localization
ms.assetid: 56e5a5c8-6c96-4d19-b8e1-a5be1dc564af
ms.openlocfilehash: e9a9e9295425efaadff4ac1f0b796b2c9a889543
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200955"
---
# <a name="wpf-globalization-and-localization-overview"></a>WPF 전역화 및 지역화 개요

제품을 한 언어로만 제공하면 잠재적 고객 기반이 전 세계 65억 인구의 극히 일부로만 제한됩니다. 전 세계를 대상으로 하는 응용 프로그램을 만들려는 경우 가장 뛰어나고 경제적으로 고객에게 다가갈 수 있는 방법 중 하나는 바로 제품의 비용 효율적인 지역화입니다.  
  
 이 개요에서는 전역화 및 지역화 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]합니다. 전역화는 여러 위치에서 수행되는 응용 프로그램의 디자인 및 개발 작업입니다. 예를 들어 전역화는 여러 문화권의 사용자를 위해 지역화된 사용자 인터페이스와 국가별 데이터를 지원합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 주석 달기 및 자동 레이아웃, 위성 어셈블리 및 지역화 된 특성을 포함 하 여 전역화 된 디자인 기능을 제공 합니다.
  
 지역화는 응용 프로그램 리소스를 응용 프로그램에서 지원할 각 문화권에 맞는 지역화된 버전으로 번역하는 작업입니다. 지역화 하는 경우 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 Api를 사용 하는 <xref:System.Windows.Markup.Localizer> 네임 스페이스입니다. 이러한 Api power 합니다 [LocBaml 도구 샘플](https://go.microsoft.com/fwlink/?LinkID=160016) 명령줄 도구입니다. 빌드 LocBaml을 사용 하는 방법에 대 한 정보를 참조 하세요 [응용 프로그램 지역화](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)합니다.
  
## <a name="best-practices-for-globalization-and-localization-in-wpf"></a>WPF를 위한 최선의 전역화 및 지역화 방법

 로 빌드되는 전역화 및 지역화 기능을 최대한 활용할 수 있게 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] UI 디자인 및이 섹션에서는 제공 되는 지역화 관련 팁에 따라 합니다.  
  
### <a name="best-practices-for-wpf-ui-design"></a>최선의 WPF UI 디자인 방법

 디자인할 때를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]– 기반 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], 모범 사례를 구현 하는 것이 좋습니다.  
  
-   작성 하 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; 만들지 않도록 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 코드에서. 만들 때 사용자 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 를 사용 하 여 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], 기본 제공 지역화 Api 통해 노출 합니다.  
  
-   절대 위치와 고정된 크기를 사용 하 여 콘텐츠를 레이아웃할 수 방지 대신 상대적 크기나 자동 크기 조정 합니다.
  
    -   사용 하 여 <xref:System.Windows.Window.SizeToContent%2A> 너비와 높이 설정 하 고 `Auto`입니다.  
  
    -   사용 하지 마세요 <xref:System.Windows.Controls.Canvas> 레이아웃 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]s입니다.  
  
    -   사용 하 여 <xref:System.Windows.Controls.Grid> 및 해당 크기 공유 기능입니다.  
  
-   지역화된 텍스트는 공간을 더 많이 필요로 하는 경우가 많으므로 여분의 공간을 여백으로 남겨 둡니다. 여분의 공간을 통해 여분의 문자를 표현할 수 있습니다.  
  
-   사용 하도록 설정 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 에서 <xref:System.Windows.Controls.TextBlock> 클리핑을 피하기 위해.
  
-   `xml:lang` 특성을 설정합니다. 이 특성에는 특정 요소 및 해당 자식 요소의 문화권을을 설명합니다. 이 속성의 값에서 몇 가지 기능의 동작 변경 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다. 예를 들어 하이픈 넣기, 맞춤법 검사, 숫자 대체, 복잡한 스크립트 셰이핑 및 글꼴 대체의 동작을 변경합니다. 참조 [WPF의 전역화](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md) 설정에 대 한 자세한 내용은 합니다 [xml: lang XAML 처리](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md)합니다.  
  
-   다른 언어에 사용 되는 글꼴을 더욱 효과적으로 제어할를 사용자 지정된 합성 글꼴을 만듭니다. 기본적으로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Windows\Fonts 디렉터리에서 GlobalUserInterface.composite 글꼴을 사용 합니다.  
  
-   텍스트를 오른쪽에서 왼쪽 형식으로 표시 하는 문화권에서 지역화 될 수 있는 탐색 응용 프로그램을 만들 때, 명시적으로 설정 합니다 <xref:System.Windows.FlowDirection> 페이지를 상속 하지 않는 되도록 모든 페이지의 <xref:System.Windows.FlowDirection> 에서 <xref:System.Windows.Navigation.NavigationWindow>합니다.  
  
-   브라우저 외부에서 호스팅되는 독립 실행형 탐색 응용 프로그램을 만들 때 설정 합니다 <xref:System.Windows.Application.StartupUri%2A> 초기 응용 프로그램에 대 한는 <xref:System.Windows.Navigation.NavigationWindow> 대신 페이지 (예를 들어 `<Application StartupUri="NavigationWindow.xaml">`). 이 디자인을 사용 하면 변경할 수 있습니다는 <xref:System.Windows.FlowDirection> 창 및 탐색 모음입니다. 자세한 내용 및 예제를 참조 하세요 [Globalization Homepage 샘플](https://go.microsoft.com/fwlink/?LinkID=159990)합니다.  
  
### <a name="best-practices-for-wpf-localization"></a>WPF 지역화 모범 사례

 지역화할 때는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]– 기반된 응용 프로그램 모범 사례를 구현 하는 것이 좋습니다.  
  
-   지역화 주석을 사용 하 여 지역화 담당자에 대 한 추가 컨텍스트를 제공 합니다.  
  
-   지역화 특성을 사용 하 여 컨트롤을 선택적으로 생략 하는 대신 지역화 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 요소 속성입니다. 참조 [지역화 특성과 주석을](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md) 자세한 내용은 합니다.  
  
-   사용 하 여 `msbuild -t:updateuid` 및 `-t:checkuid` 추가 하 고 검사 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 의 속성에 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]입니다. 사용 하 여 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성 개발 및 지역화 간의 변경 내용을 추적 합니다. <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성에 새 개발 변경 내용을 지역화할 수 있습니다. 수동으로 추가한 경우 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성을 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], 작업은 지루할 정확도 낮아집니다.  
  
    -   편집 하거나 변경 하지 않는 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 지역화를 시작한 후에 속성입니다.  
  
    -   중복을 사용 하지 않는 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성 (복사 및 붙여넣기 명령을 사용 하는 경우이 팁 기억).  
  
    -   설정 된 `UltimateResourceFallback` AssemblyInfo.* 대체 (fallback)에 대 한 적절 한 언어를 지정한 위치 (예를 들어 `[assembly: NeutralResourcesLanguage("en-US",   UltimateResourceFallbackLocation.Satellite)]`).  
  
         생략 하 여 주 어셈블리에서 소스 언어를 포함 하려는 경우는 `<UICulture>` 프로젝트 파일의 태그를 설정 합니다 `UltimateResourceFallback` 위성이 아닌 주 어셈블리와 위치 (예를 들어 `[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.MainAssembly)]`).  
  
## <a name="localize-a-wpf-application"></a>WPF 응용 프로그램 지역화

지역화 하는 경우는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 몇 가지 옵션이 있습니다. 예를 들어, 응용 프로그램의 지역화 가능한 리소스를 바인딩할 수 있습니다는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 파일, 지역화 가능 텍스트를 resx 테이블에에서 저장 또는 사용 하 여 지역화 담당자가 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 파일입니다. 이 섹션에서는 몇 가지 이점을 제공 하는 XAML의 BAML 양식을 사용 하는 지역화 워크플로를 설명 합니다.  
  
-   구성한 후에 지역화할 수 있습니다.  
  
-   이전 버전의 BAML 양식의 XAML을 지역화된 새 버전의 BAML 양식의 XAML로 업데이트할 수 있으므로 개발과 동시에 지역화를 수행할 수 있습니다.  
  
-   확인할 수 있습니다 원래 소스 요소와 의미 체계 컴파일 타임에 BAML 양식의 XAML의 컴파일된 형태 이므로 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]합니다.  
  
### <a name="localization-build-process"></a>지역화 빌드 프로세스  

개발 하는 경우는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 지역화를 위한 빌드 프로세스는 다음과 같습니다.  
  
-   개발자가 만들고 전역화 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램입니다. 프로젝트 파일에서 개발자 설정 `<UICulture>en-US</UICulture>` 응용 프로그램을 컴파일할 때 있도록 언어 중립적 주 어셈블리가 생성 됩니다. 이 어셈블리에는 지역화 가능한 모든 리소스가 포함된 위성 .resources.dll 파일이 있습니다. 필요에 따라 있습니다 수 소스 언어를 유지할 주 어셈블리에 있으므로 지역화 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 주 어셈블리에서의 추출을 지원 합니다.  
  
-   파일을 빌드, 컴파일될 때는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] XAML의 BAML 양식으로 변환 됩니다. 문화권에 중립적인 `MyDialog.exe` 와 문화권에 종속적인 (영어) `MyDialog.resources.dll` 파일이 영어권 고객에 게 릴리스됩니다.  
  
### <a name="localization-workflow"></a>지역화 워크플로

지역화 프로세스 시작 되지 않은 후 `MyDialog.resources.dll` 파일이 만들어집니다. [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 요소 및 속성의 원래 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 를 사용 하 여 키-값 쌍으로 BAML 양식의 XAML에서 추출 된 합니다 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 에서 <xref:System.Windows.Markup.Localizer>합니다. 지역화 담당자는 키/값 쌍을 사용하여 응용 프로그램을 지역화합니다. 지역화가 완료된 후 새 값에서 새 .resource.dll을 생성할 수 있습니다.
  
 키-값 쌍의 키는 `x:Uid` 원래에서 개발자가 배치 되는 값 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]합니다. 이러한 `x:Uid` 값을 사용 합니다 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 추적 하 고 지역화 도중 개발자와 지역화 담당자 간에 발생 하는 변경 내용을 병합 합니다. 예를 들어 개발자가 변경 된 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 지역화 담당자가 지역화를 시작한 후 손실 되는 최소한의 변환 작업을 이미 완료 된 지역화 작업과 개발 변경 내용을 병합할 수 있습니다.  
  
 다음 그래픽은 BAML 양식의 XAML을 기반으로 하는 일반적인 지역화 워크플로를 보여 줍니다. 이 다이어그램 개발자 응용 프로그램을 영어로 작성 하는 것으로 가정 합니다. 개발자가 WPF 응용 프로그램을 만들고 전역화합니다. 프로젝트 파일에서 개발자 설정 `<UICulture>en-US</UICulture>` , 빌드 시 언어 중립적 주 어셈블리의 위성을 사용 하 여 생성 되도록 합니다. resources.dll 모든 지역화 가능 리소스를 포함 합니다. 또는 WPF 지역화 API가 주 어셈블리에서의 추출을 지원하므로 주 어셈블리에서 소스 언어를 유지할 수 있습니다. 빌드 프로세스 후 XAML이 BAML로 컴파일됩니다. 문화권에 중립적인 MyDialog.exe.resources.dll이 영어권 고객에게 제공됩니다.  
  
 ![지역화 워크플로](../../../../docs/framework/wpf/advanced/media/localizationworkflow.png "LocalizationWorkflow")  
  
 ![지역화되지 않은 워크플로](../../../../docs/framework/wpf/advanced/media/localizationworkflow2.png "LocalizationWorkflow2")  
  
## <a name="examples-of-wpf-localization"></a>WPF 지역화 예제

 이 섹션에는 지역화 된 응용 프로그램을 빌드하고 지역화 하는 방법을 이해할 수 있도록 예가 포함 되어 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램입니다.  
  
#### <a name="run-dialog-box-example"></a>실행 대화 상자 예제

 다음 그래픽의 출력을 표시 합니다 **실행** 대화 상자 샘플입니다.  
  
 **영어:**  
  
 ![실행 대화 상자](../../../../docs/framework/wpf/advanced/media/rundialogenglish.PNG "RunDialogEnglish")  
  
 **독일어:**  
  
 ![독일어 실행 대화 상자](../../../../docs/framework/wpf/advanced/media/rundialoggerman.PNG "RunDialogGerman")  
  
 **전역 실행 대화 상자 디자인**  
  
 이 예제의 결과 **실행** 대화 상자를 사용 하 여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 고 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]합니다. 이 대화 상자는 해당 하는 **실행** 에서 사용할 수 있는 대화 상자는 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 시작 메뉴.  
  
 전역 대화 상자를 만들 때 주의해야 할 점은 다음과 같습니다.  
  
 **자동 레이아웃**  
  
 *Window1.xaml:*  
  
 `<Window SizeToContent="WidthAndHeight">`  
  
 이전 Window 속성이 창의 크기를 콘텐츠 크기에 맞게 자동으로 조정합니다. 이 속성은 지역화한 후 크기가 증가한 콘텐츠가 창에서 잘리는 것을 방지하며, 지역화한 후 콘텐츠 크기가 줄어들 때 생기는 불필요한 공간도 제거합니다.  
  
 `<Grid x:Uid="Grid_1">`  
  
 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성에 대 한 순서에 필요한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 지역화 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 올바르게 작동 합니다.  
  
 사용할 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 지역화 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 개발 및 지역화 간의 변경 내용을 추적 합니다 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]합니다. <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성을 사용 하면 최신 버전의 병합 된 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 의 이전 지역화와는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]합니다. 추가 하는 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 실행 하 여 속성 `msbuild -t:updateuid RunDialog.csproj` 명령 셸에서 합니다. 추가 하는 권장 방법은 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 속성 이므로 수동으로 추가한 일반적으로 시간이 많이 걸리고 정확도 낮아집니다. 하는지 검사할 수 있습니다 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 실행 하 여 속성이 올바르게 설정 되어 `msbuild -t:checkuid RunDialog.csproj`입니다.
  
 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 를 사용 하 여 구조화 된 합니다 <xref:System.Windows.Controls.Grid> 자동 레이아웃의 이점을 활용 하는 유용한 컨트롤인 제어에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다. 대화 상자는 세 개의 행과 다섯 개의 열로 나뉩니다. 행 및 열 정의 크기가 고정; 따라서는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 각 셀에 배치 하는 요소 수 증가 맞게 지역화 하는 동안 크기가 감소 합니다.  
  
 [!code-xaml[GlobalizationRunDialog#GridColumnDef](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef)]  
  
 처음 두 열 위치를 **열기:** 레이블 및 <xref:System.Windows.Controls.ComboBox> 사항이의 10%를 사용 하 여는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 전체 너비.  
  
 [!code-xaml[GlobalizationRunDialog#GridColumnDef2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef2)]  
  
 공유 크기 조정 기능을 사용 하는 예제 <xref:System.Windows.Controls.Grid>합니다. 마지막 세 열은 동일한 자체를 배치 하 여이 활용 하기 위해 <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A>합니다. 속성의 이름에서 알 수 있듯이 이 속성을 통해 열은 같은 크기를 공유할 수 있습니다. 따라서 더 긴 문자열인 "찾아보기..."를 "찾아보기..." 가져옵니다 지역화 하는 경우 모든 단추 대신 작은 "확인" 단추 및 커집니다 "찾아보기..." 단추 너비에서 증가 합니다.  
  
 **Xml:lang**
  
 `Xml:lang="en-US"`  
  
 알림 합니다 [xml: lang XAML 처리](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md) 의 루트 요소에 배치 합니다 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]합니다. 이 속성은 해당 요소 및 자식의 문화권을 설명합니다. 이 값은 사용의 몇 가지 기능 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이며 지역화 하는 동안 적절 하 게 변경 해야 합니다. 이 값은 단어 하이픈 넣기와 맞춤법 검사에 사용할 언어 사전을 변경합니다. 또한 숫자의 표시 및 글꼴 대체 시스템에서 사용할 글꼴을 선택하는 방법에도 영향을 줍니다. 마지막으로, 속성은 숫자 표시 방식과 복잡한 스크립트에 포함된 텍스트의 모양이 지정되는 방식에 영향을 줍니다. 기본값은 "en-US"입니다.  
  
 **위성 리소스 어셈블리 빌드**  
  
 *.csproj:*  

 편집 된 `.csproj` 파일을 다음 태그를 무조건 추가 `<PropertyGroup>`:
 
 `<UICulture>en-US</UICulture>`  
  
 추가 확인을 `UICulture` 값입니다. 유효한로 설정 하면이 <xref:System.Globalization.CultureInfo> 값 예: EN-US, 프로젝트를 빌드할에 모든 지역화 가능 리소스를 사용 하 여 위성 어셈블리를 생성 합니다.  
  
 `<Resource Include="RunIcon.JPG">`  
  
 `<Localizable>False</Localizable>`  
  
 `</Resource>`  
  
 `RunIcon.JPG` 모든 문화권에 대해 동일 하 게 나타나야 하므로 지역화할 필요가 없습니다. `Localizable` 로 설정 된 `false` 위성 어셈블리 대신 언어 중립적 주 어셈블리에 유지 되도록 합니다. 모든 컴파일할 리소스의 기본값은 `Localizable` 로 `true`합니다.  
  
 **실행 대화 상자 지역화**  
  
 **구문 분석**  
  
 응용 프로그램을 빌드한 후 지역화의 첫 번째 단계는 위성 어셈블리에서 지역화할 수 있는 리소스를 구문 분석하는 것입니다. 이 항목의 목적에서 찾을 수 있는 샘플 LocBaml 도구를 사용 하 여 [LocBaml 도구 샘플](https://go.microsoft.com/fwlink/?LinkID=160016)합니다. LocBaml은 지역화 프로세스에 적합한 지역화 도구의 빌드에 도움을 주기 위한 샘플 도구입니다. 구문 분석 하려면 다음 LocBaml을 사용 하 여 실행: **LocBaml RunDialog.resources.dll 구문 분석/out:** "고 RunDialog.resources.dll.CSV" 파일을 생성 합니다.  
  
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
  
 응용 프로그램을 독일어로 지역화하려면 다음과 같이 번역해야 합니다.  
  
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
  
 독일어 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)],이 resources.dll이 주 어셈블리 옆의 DE-DE 폴더에 배치 되 면이 리소스 대신 EN-US 폴더에 자동으로 로드 됩니다. 독일어 버전이 없는 경우 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 이 테스트 하려면 문화권의 문화권으로 설정 합니다 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 사용 하는 (예를 들어 `en-US`), 원래 리소스 DLL을 바꿉니다.  
  
 **위성 리소스 로드**  
  
|MyDialog.exe|en-US\MyDialog.resources.dll|de-DE\MyDialog.resources.dll|  
|------------------|------------------------------------|------------------------------------|  
|코드|원본 영어 BAML|지역화된 BAML|  
|문화권에 중립적인 리소스|영어로 된 기타 리소스|독일어로 지역화된 기타 리소스|  
  
 .NET framework 응용 프로그램에 따라 로드할 위성 리소스 어셈블리를 자동으로 선택 `Thread.CurrentThread.CurrentUICulture`합니다. 문화권을 기본값으로 프로그램 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] OS입니다. 독일어를 사용 하는 경우 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]을 영어를 사용 하는 경우는 de-DE\MyDialog.resources.dll 로드 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]에 en-US\MyDialog.resources.dll이 로드 합니다. 프로젝트의 AssemblyInfo.*에 NeutralResourcesLanguage를 지정하여 응용 프로그램에 대한 최종 대체 리소스를 설정할 수 있습니다. 예를 들면 다음과 같이 지정할 수 있습니다.  
  
 `[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]`  
  
 그러면 de-DE\MyDialog.resources.dll 또는 de\MyDialog.resources.dll을 모두 사용할 수 없는 경우 en-US\MyDialog.resources.dll이 독일어 Windows에 사용됩니다.  
  
### <a name="microsoft-saudi-arabia-homepage"></a>Microsoft 사우디아라비아 홈페이지  
 다음 그래픽에서는 영어 및 아랍어 홈페이지를 보여 줍니다. 이러한 그래픽을 생성 하는 전체 샘플을 참조 하세요 [Globalization Homepage 샘플](https://go.microsoft.com/fwlink/?LinkID=159990)합니다.  
  
 **영어:**  
  
 ![영어 페이지](../../../../docs/framework/wpf/advanced/media/englishhomepage.jpg "EnglishHomepage")  
  
 **아랍어:**  
  
 ![아랍어 페이지](../../../../docs/framework/wpf/advanced/media/arabichomepage.jpg "ArabicHomepage")  
  
### <a name="designing-a-global-microsoft-homepage"></a>글로벌 Microsoft 홈페이지 디자인  
 이 Microsoft 사우디아라비아 웹 사이트 샘플에서는 RightToLeft 언어를 위해 제공되는 전역화 기능을 보여 줍니다. 히브리어 및 아랍어 같은 언어에는 오른쪽에서 왼쪽 읽기 순서를 따라서 레이아웃 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 배치 종종 해야 영어 등의 왼쪽에서 오른쪽 언어로 것 보다 상당히 다릅니다. 왼쪽에서 오른쪽으로 읽는 언어를 오른쪽에서 왼쪽으로 읽는 언어로 또는 그 반대로 지역화하는 작업은 꽤 까다로울 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 이러한 지역화를 훨씬 쉽게 수행할 수 있도록 디자인되었습니다.  
  
 **FlowDirection**  
  
 *Homepage.xaml:*  
  
 [!code-xaml[GlobalizationHomepage#Homepage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#homepage)]  
  
 알림 합니다 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 속성을 <xref:System.Windows.Controls.Page>입니다. 이 속성을 변경 <xref:System.Windows.FlowDirection.RightToLeft> 바뀝니다 합니다 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 의 <xref:System.Windows.Controls.Page> 및 해당 자식 요소의 있도록이 레이아웃 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 대칭 이동 됩니다 오른쪽에서 왼쪽 아랍인 사용자 예상한 대로입니다. 명시적 지정 하 여 상속 동작을 재정의할 수 있습니다 하나 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 모든 요소입니다. 합니다 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 속성은에서 사용 가능한 <xref:System.Windows.FrameworkElement> 또는 문서 관련된 요소 및 암시적 값 <xref:System.Windows.FlowDirection.LeftToRight>합니다.  
  
 배경 그라데이션 브러시도 제대로 대칭 이동 됩니다 때 관찰 루트 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 변경 됩니다.  
  
 **FlowDirection="LeftToRight"**  
  
 ![왼쪽에서 오른쪽으로 흐름](../../../../docs/framework/wpf/advanced/media/lefttoright.PNG "LeftToRight")  
  
 **FlowDirection="RightToLeft"**  
  
 ![오른쪽에서 왼쪽으로 흐름](../../../../docs/framework/wpf/advanced/media/righttoleft.PNG "RightToLeft")  
  
 **패널 및 컨트롤에 고정 크기 사용 피하기**  
  
 Homepage.xaml 살펴보세요에서 고정된 너비와 높이 전체에 대해 지정 하는 것 외 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 위쪽 <xref:System.Windows.Controls.DockPanel>, 가지 다른 고정된 차원이 없습니다. 지역화된 텍스트가 소스 텍스트보다 길어서 잘리는 것을 방지하기 위해 고정된 크기를 사용하지 않도록 하세요. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 패널 및 컨트롤은 포함된 콘텐츠에 따라 자동으로 크기가 조정됩니다. 또한 대부분의 컨트롤에는 더 많은 제어를 설정할 수 있는 최소 및 최대 크기 (예: MinWidth = "20"). 사용 하 여 <xref:System.Windows.Controls.Grid>를 사용 하 여 상대적 너비와 높이 설정할 수도 있습니다 '\*' (예를 들어 `Width="0.25*"`) 하거나 해당 셀 크기 공유 기능을 사용 합니다.  
  
 **지역화 주석**  
  
 콘텐츠가 모호하여 번역하기 어려운 경우도 많이 있습니다. 개발자나 디자이너는 지역화 주석을 통해 지역화 담당자에게 추가적인 컨텍스트 및 주석을 제공할 수 있습니다. 예를 들어 아래의 Localization.Comments에서는 문자 ‘&#124;’의 사용을 명확하게 설명합니다.  
  
 [!code-xaml[GlobalizationHomepage#LocalizationComment](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcomment)]  
  
 이 주석은 TextBlock_1의 콘텐츠와 LocBaml 도구의 연결 됩니다 (참조 [응용 프로그램 지역화](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)), 출력.csv 파일에서 TextBlock_1 행의 여섯 번째 열에서 볼 수 있습니다.  
  
|리소스 키|범주|가독성|수정 가능성|주석|값|  
|-|-|-|-|-|-|  
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|텍스트|true|true|이 문자는 장식 규칙으로 사용됩니다.|&#124;|  
  
 다음 구문을 사용하여 주석을 요소의 속성 또는 콘텐츠에 배치할 수 있습니다.  
  
 [!code-xaml[GlobalizationHomepage#LocalizationCommentsProp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcommentsprop)]  
  
 **지역화 특성**  
  
 개발자 또는 지역화 관리자는 지역화 담당자가 읽고 수정할 수 있는 컨트롤을 필요로 할 수 있습니다. 예를 들어 회사 이름이나 법적 고지문은 번역하지 않아야 할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 지역화 도구가 요소를 잠그거나, 숨기거나, 정렬할 때 사용할 수 있는 요소의 콘텐츠나 속성의 가독성, 수정 가능 여부 및 범주를 설정할 수 있는 특성을 제공합니다. 자세한 내용은 <xref:System.Windows.Localization.Attributes%2A>을 참조하세요. 이 샘플의 목적상 LocBaml 도구는 이러한 특성의 값만 출력합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤은 모두 이러한 특성에 대해 기본값을 사용하지만 이를 재정의할 수 있습니다. 다음 예제에서는 기본 지역화 특성을 재정의 하는 예를 들어 `TextBlock_1` 지역화 담당자가 콘텐츠를 읽을 수 있지만 수정할 수 없도록 설정 합니다.  
  
 [!code-xaml[LocalizationComAtt#LocalizationAttributes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributes)]  
  
 가독성 및 수정 가능 여부 특성 외에도 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 일반적인 UI 범주의 열거형을 제공 (<xref:System.Windows.LocalizationCategory>)는 지역화 담당자에 게 더 많은 컨텍스트를 제공 하는 데 사용할 수 있는 합니다. 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 플랫폼 컨트롤에 대 한 기본 범주에서 재정의할 수 있습니다 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 도:  
  
 [!code-xaml[LocalizationComAtt#LocalizationAttributesOverridden](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributesoverridden)]  
  
 기본 지역화 특성을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 제공 사용자 지정 컨트롤에 대 한 기본값을 올바르게 설정할 수 있는 코드를 통해 재정의할 수 있습니다. 예를 들어:  

```csharp 
[Localizability(Readability = Readability.Readable, Modifiability=Modifiability.Unmodifiable, LocalizationCategory.None)] 
public class CorporateLogo : TextBlock
{
    // ...
}
``` 
 
 설정 된 인스턴스별 특성 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 사용자 지정 컨트롤에서 코드에 설정 된 값 보다 우선적으로 적용 됩니다. 특성 및 주석에 대 한 자세한 내용은 참조 하세요. [지역화 특성과 주석을](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md)합니다.  
  
 **글꼴 대체 및 복합 글꼴**  
  
 지정 된 코드 포인트 범위를 지원 하지 않는 글꼴을 지정 하는 경우 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Windows\Fonts 디렉터리에 있는 전역 사용자 Interface.compositefont를 사용 하 여 수행 하는 자동으로 대체 됩니다. 복합 글꼴 것은 다른 글꼴 처럼 작동 하 고 요소를 설정 하 여 명시적으로 사용할 수 있습니다 `FontFamily` (예를 들어 `FontFamily="Global User Interface"`). 복합 글꼴을 직접 만들고 특정 코드 포인트 범위와 언어에 사용할 글꼴을 지정하여 글꼴 대체 기본 설정을 직접 지정할 수 있습니다.  
  
 복합 글꼴에 대 한 자세한 내용은 참조 하세요. <xref:System.Windows.Media.FontFamily>합니다.  
  
 **Microsoft 홈페이지 지역화**  
  
 실행 대화 상자와 동일한 단계를 사용하여 이 응용 프로그램을 지역화할 수 있습니다. 아랍어에 대 한 지역화 된.csv 파일에서 제공 되는 [Globalization Homepage 샘플](https://go.microsoft.com/fwlink/?LinkID=159990)합니다.
