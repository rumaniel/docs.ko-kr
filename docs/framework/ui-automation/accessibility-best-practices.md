---
title: 액세스 가능성에 대한 유용한 정보
ms.date: 03/30/2017
helpviewer_keywords:
- best practices for accessibility
- accessibility, best practices for
ms.assetid: e6d5cd98-21a3-4b01-999c-fb953556d0e6
ms.openlocfilehash: 92bad8b5ad556d79480a5b4da489d070545701da
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291396"
---
# <a name="accessibility-best-practices"></a>액세스 가능성에 대한 유용한 정보
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. @No__t-0에 대 한 최신 정보는 [Windows Automation API를 참조 하세요. UI 자동화 @ no__t-0.  
  
 컨트롤이 나 응용 프로그램에서 다음 모범 사례를 구현 하면 보조 기술 장치를 사용 하는 사용자에 대 한 접근성이 향상 됩니다. 이들 모범 사례는 대부분 효율적인 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 디자인에 초점을 맞춥니다. 각 모범 사례에는 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 컨트롤 또는 애플리케이션에 대한 구현 정보가 포함됩니다. 대부분 경우에 이들 모범 사례에 맞는 작업이 이미 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에 포함되어 있습니다.  
  
<a name="Programmatic_Access"></a>   
## <a name="programmatic-access"></a>프로그래밍 방식 액세스  
 프로그래밍 방식 액세스에서는 모든 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소에 레이블이 지정되고, 속성 값이 노출되고, 적절한 이벤트가 발생하는지를 확인합니다. 표준 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 컨트롤의 경우 이 작업 대부분이 <xref:System.Windows.Automation.Peers.AutomationPeer>를 통해 이미 수행되었습니다. 사용자 지정 컨트롤에는 프로그래밍 방식 액세스가 제대로 구현되었는지 확인하는 작업이 추가로 필요합니다.  
  
<a name="Enable_Programmatic_Access_to_all_UI_Elements_and_Text"></a>   
### <a name="enable-programmatic-access-to-all-ui-elements-and-text"></a>모든 UI 요소 및 텍스트에 대해 프로그래밍 방식 액세스 사용  
 UI (사용자 인터페이스) 요소는 프로그래밍 방식 액세스를 사용 하도록 설정 해야 합니다. [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 가 표준 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이면 프로그래밍 방식 액세스 지원이 컨트롤에 포함됩니다. 공용 컨트롤에서 서브클래싱된 컨트롤이나 컨트롤에서 서브클래싱된 컨트롤과 같은 사용자 지정 컨트롤이면 <xref:System.Windows.Automation.Peers.AutomationPeer> 구현에서 수정해야 할 수 있는 영역이 있는지 확인해야 합니다.  
  
 이 모범 사례를 따라 보조 기술 공급 업체에서 제품 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]의 요소를 식별 하 고 조작할 수 있습니다.  
  
<a name="Place_Names__Titles_and_Descriptions_on_UI_Objects_"></a>   
### <a name="place-names-titles-and-descriptions-on-ui-objects-frames-and-pages"></a>UI 개체, 프레임 및 페이지에 대한 위치 이름, 제목 및 설명  
 보조 기술, 특히 화면 읽기 프로그램에서는 제목을 사용하여 탐색 체계에서 프레임, 개체 또는 페이지의 위치를 인식합니다. 따라서 제목은 구체적인 설명을 포함해야 합니다. 예를 들어 사용자가 특정 영역을 자세히 탐색한 경우에는 웹 페이지 제목이 "Microsoft 웹 페이지"인 것은 도움이 되지 않습니다. 시각 장애가 있고 화면 읽기 프로그램에 의존하는 사용자에게는 구체적인 설명이 포함된 제목이 중요합니다. 마찬가지로 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 컨트롤의 경우 <xref:System.Windows.Automation.AutomationProperties.NameProperty>과 <xref:System.Windows.Automation.AutomationProperties.HelpTextProperty>는 보조 기술 장치에 중요 합니다.  
  
 이 모범 사례를 따라 보조 technologys 샘플 컨트롤 및 응용 프로그램에서 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]을 식별 하 고 조작할 수 있습니다.  
  
<a name="Ensure_Programmatic_Events_are_Triggered_by_all_UI"></a>   
### <a name="ensure-programmatic-events-are-triggered-by-all-ui-activities"></a>프로그래밍 방식 이벤트가 모든 UI 작업에서 트리거되는지 확인  
 이 모범 사례를 따라 보조 technologys는 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]의 변경 내용을 수신 대기 하 고 이러한 변경 내용을 사용자에 게 알릴 수 있습니다.  
  
<a name="User_Settings"></a>   
## <a name="user-settings"></a>사용자 설정  
 이 섹션의 모범 사례에서는 컨트롤이나 애플리케이션이 사용자 설정을 재정의하지 않도록 합니다.  
  
<a name="Respect_all_System_Wide_Settings_and_do_not_Interfere"></a>   
### <a name="respect-all-system-wide-settings-and-do-not-interfere-with-accessibility-functions"></a>모든 시스템 수준 설정 유지 및 액세스 가능성 기능 방해 안 함  
 사용자는 제어판을 사용하여 일부 시스템 수준 플래그를 설정할 수 있습니다. 다른 플래그는 프로그래밍 방식으로 설정할 수 있습니다. 이들 설정은 컨트롤이나 애플리케이션에 의해 변경되지 않아야 합니다. 또한 애플리케이션에서는 호스트 운영 체제의 액세스 가능성 설정을 지원해야 합니다.  
  
 이 모범 사례를 따르면 사용자가 액세스 가능성 설정을 지정하고 해당 설정이 애플리케이션에 의해 변경되지 않는다는 것을 알 수 있습니다.  
  
<a name="Visual_UI_Design"></a>   
## <a name="visual-ui-design"></a>시각적 UI 디자인  
 이 섹션의 모범 사례는 컨트롤이 나 응용 프로그램에서 색 및 이미지를 효과적으로 사용 하 고 보조 기술에서 사용할 수 있도록 합니다.  
  
<a name="Don_t_Hard_Code_Colors"></a>   
### <a name="dont-hard-code-colors"></a>색 하드 코드 안 함  
 색맹이거나 시력이 낮거나 흑백 화면을 사용하는 사용자는 하드 코드된 색으로 애플리케이션을 사용하지 못할 수 있습니다.  
  
 이 모범 사례를 따르면 사용자가 개별 요구 사항에 따라 색 조합을 조정할 수 있습니다.  
  
<a name="Support_High_Contrast_and_all_System_Display_Attributes"></a>   
### <a name="support-high-contrast-and-all-system-display-attributes"></a>고대비 및 모든 시스템 표시 특성 지원  
 애플리케이션은 사용자가 선택한 시스템 수준 대비 설정, 색 선택 또는 기타 시스템 수준 표시 설정과 특성을 방해하거나 비활성화하지 않아야 합니다. 사용자가 선택한 시스템 수준 설정은 애플리케이션의 액세스 가능성을 개선하므로 애플리케이션에 의해 비활성화되거나 무시되지 않아야 합니다. 적절한 대비를 제공하려면 올바른 배경 기반 전경 조합으로 색을 사용해야 합니다. 관련되지 않은 색을 혼합하지 않아야 하고 색을 반전하지 않아야 합니다.  
  
 대부분 사용자에게는 검은색 배경 기반 흰색 텍스트와 같은 특수 고대비 조합이 필요합니다. 흰색 배경 기반 검은색 텍스트처럼 이들 색을 반전해서 그리면 배경이 전경 위로 번지므로 몇몇 사용자는 텍스트를 읽기 어려울 수 있습니다.  
  
<a name="Ensure_all_UI_Correctly_Scales_by_any_DPI_Setting"></a>   
### <a name="ensure-all-ui-correctly-scales-by-any-dpi-setting"></a>DPI 설정으로 모든 UI가 올바르게 크기 조정되는지 확인  
 모든 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]이 dpi (인치당 도트 수) 설정에 따라 올바르게 조정 될 수 있는지 확인 합니다. 또한 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소가 120 dpi (인치당 도트 수)로 1024 x 768 화면에 맞도록 해야 합니다.  
  
<a name="Navigation"></a>   
## <a name="navigation"></a>탐색  
 이 섹션의 모범 사례에서는 컨트롤 및 애플리케이션에 대한 탐색이 처리되었는지 확인합니다.  
  
<a name="Provide_Keyboard_Interface_for_all_UI_Elements"></a>   
### <a name="provide-keyboard-interface-for-all-ui-elements"></a>모든 UI 요소에 대한 키보드 인터페이스 제공  
 특히 신중하게 계획된 탭 정지는 사용자에게 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]를 탐색하는 또 다른 방법을 제공합니다.  
  
 애플리케이션에서는 다음 키보드 인터페이스를 제공해야 합니다.  
  
- 단추, 링크 또는 목록 상자와 같이 사용자가 조작할 수 있는 모든 컨트롤에 대한 탭 정지  
  
- 논리적 탭 순서  
  
<a name="Show_the_Keyboard_Focus"></a>   
### <a name="show-the-keyboard-focus"></a>키보드 포커스 표시  
 사용자는 키 입력의 효과를 예상할 수 있도록 키보드 포커스가 있는 개체를 사용자가 알 수 있어야 합니다. 키보드 포커스를 강조 표시하려면 색, 글꼴 또는 그래픽(예: 사각형 또는 확대)을 사용합니다. 키보드 포커스를 청각적으로 강조하려면 볼륨, 피치 또는 음조 품질을 변경합니다.  
  
 혼동을 방지하려면 애플리케이션이 모든 시각적 포커스 표시기를 숨기고 비활성 창에 있는 선택 항목을 흐리게 표시해야 합니다.  
  
 애플리케이션에서는 키보드 포커스를 통해 다음을 수행해야 합니다.  
  
- 키보드 포커스가 항상 한 항목에 있어야 함  
  
- 키보드 포커스가 표시되고 분명해야 함  
  
- 선택 항목 및/또는 포커스가 있는 항목이 시각적으로 강조되어야 함  
  
<a name="Support_Navigation_Standards_and_Powerful_Navigation"></a>   
### <a name="support-navigation-standards-and-powerful-navigation-schemes"></a>탐색 표준 및 강력한 탐색 체계 지원  
 키보드 탐색의 다양한 측면을 통해 사용자가 다양한 방법으로 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]을(를) 탐색할 수 있습니다.  
  
 애플리케이션에서는 다음 키보드 인터페이스를 제공해야 합니다.  
  
- 모든 명령, 메뉴 및 컨트롤에 대한 바로 가기 키 및 밑줄이 표시된 액세스 키  
  
- 중요 링크에 대한 키보드 바로 가기  
  
- 모든 메뉴 항목에는 액세스 키가 있고 모든 단추와 모든 명령에는 액셀러레이터 키가 있습니다.  
  
<a name="Do_not_let_Mouse_Location_Interfere_with_Keyboard"></a>   
### <a name="do-not-let-mouse-location-interfere-with-keyboard-navigation"></a>마우스 위치가 키보드 탐색을 방해하면 안 됨  
 마우스 위치가 키보드 탐색을 방해하지 않아야 합니다. 예를 들어 마우스가 임의 위치에 있고 사용자가 키보드로 탐색할 경우 사용자가 시작하지 않은 마우스 클릭이 발생하지 않아야 합니다.  
  
<a name="Multimodal_Interface"></a>   
## <a name="multimodal-interface"></a>다중 모달 인터페이스  
 이 섹션의 모범 사례에서는 애플리케이션 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 에 시각적 요소에 대한 대안이 포함되도록 합니다.  
  
<a name="Provide_User_Selectable_Equivalents_for_Non_Text"></a>   
### <a name="provide-user-selectable-equivalents-for-non-text-elements"></a>텍스트가 아닌 요소에 대한 사용자가 선택할 수 있는 요소 제공  
 각 텍스트가 아닌 요소의 경우 텍스트, 기록 또는 오디오 설명(예: 대체 텍스트, 캡션 또는 시각적 피드백)에 대한 사용자가 선택할 수 있는 요소를 제공합니다.  
  
 텍스트가 아닌 요소는 이미지, 이미지 맵 영역, 애니메이션, 애플릿, 프레임, 스크립트, 그래픽 단추, 소리, 독립 실행형 오디오 파일 및 비디오를 포함한 광범위한 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소를 포함합니다. 텍스트가 아닌 요소는 사용자가 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]의 콘텐츠를 이해하기 위해 액세스해야 하는 시각적 정보, 음성 또는 일반 오디오 정보를 포함할 때 중요합니다.  
  
<a name="Use_Color_but_also_Provide_Alternatives_to_Color"></a>   
### <a name="use-color-but-also-provide-alternatives-to-color"></a>색을 사용하지만 색의 대안 제공  
 색을 사용하여 다른 수단으로 표시된 정보를 개선, 강조 또는 반복하지만 색만 사용해서 정보를 전달하지는 않습니다. 색맹이거나 단색 디스플레이를 사용하는 사용자는 색의 대안이 필요합니다.  
  
<a name="Use_Standard_Input_APIs_with_Devices_Independent"></a>   
### <a name="use-standard-input-apis-with-device-independent-calls"></a>디바이스 독립적 호출을 통해 표준 입력 API 사용  
 장치 독립적 호출을 사용 하면 키보드와 마우스 기능이 동일 하 게 유지 되 고, [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]에 대 한 필요한 정보가 보조 기술에 제공 됩니다.  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Automation.Peers>
- [테마 및 UI 자동화 지원 샘플이 있는 NumericUpDown 사용자 지정 컨트롤](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771573(v=vs.90))
- [키보드 사용자 인터페이스 디자인에 대한 지침](https://docs.microsoft.com/previous-versions/windows/desktop/dnacc/guidelines-for-keyboard-user-interface-design)
