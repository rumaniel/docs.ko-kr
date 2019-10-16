---
title: WPF 및 Windows Forms 상호 운용성
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms [WPF], interoperability with
- nester interoperation [WPF]
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- hybrid control [WPF interoperability]
ms.assetid: 9e8aa6b6-112c-4579-98d1-c974917df499
ms.openlocfilehash: 0326f283cb271d1578e94b648e423c6f88c579f0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917396"
---
# <a name="wpf-and-windows-forms-interoperation"></a>WPF 및 Windows Forms 상호 운용성
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]에서는 응용 프로그램 인터페이스를 만들기 위한 두 개의 서로 다른 아키텍처를 제공합니다. 네임 <xref:System.Windows.Forms.Integration?displayProperty=nameWithType> 스페이스는 일반적인 상호 운용성 시나리오를 가능 하 게 하는 클래스를 제공 합니다. 상호 운용성 기능을 구현 하는 두 가지 주요 클래스는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 고 <xref:System.Windows.Forms.Integration.ElementHost>입니다. 이 항목에서는 지원되는 상호 운용성 시나리오와 지원되지 않는 시나리오를 설명합니다.  
  
> [!NOTE]
> *하이브리드 컨트롤* 시나리오에는 특별 고려 사항이 제공됩니다. 하이브리드 컨트롤에서는 한 기술의 컨트롤이 다른 기술의 컨트롤에 중첩되어 있습니다. 이 특징은 *중첩된 상호 운용성*이라고도 합니다. *다단계 하이브리드 컨트롤*에는 두 개 이상의 하이브리드 컨트롤 중첩 수준이 있습니다. 다단계 중첩 상호 운용성의 예는 다른 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 포함하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이 포함되어 있는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤입니다. 다단계 하이브리드 컨트롤은 지원되지 않습니다.  

<a name="Windows_Presentation_Foundation_Application_Hosting"></a>   
## <a name="hosting-windows-forms-controls-in-wpf"></a>WPF에서 Windows Forms 컨트롤 호스팅  
 컨트롤이 Windows Forms 컨트롤을 호스트 하 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 는 경우 다음과 같은 상호 운용 시나리오가 지원 됩니다.  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤은 XAML을 사용하여 하나 이상의 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 호스팅할 수 있습니다.  
  
- 코드를 사용하여 하나 이상의 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 호스팅할 수 있습니다.  
  
- 다른 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 포함하는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨테이너 컨트롤을 호스팅할 수 있습니다.  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 마스터 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 세부 정보를 사용하여 마스터/세부 정보 양식을 호스팅할 수 있습니다.  
  
- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 마스터 및 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 세부 정보를 사용하여 마스터/세부 정보 양식을 호스팅할 수 있습니다.  
  
- 하나 이상의 ActiveX 컨트롤을 호스팅할 수 있습니다.  
  
- 하나 이상의 복합 컨트롤을 호스팅할 수 있습니다.  
  
- [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]을 사용하여 하이브리드 컨트롤을 호스팅할 수 있습니다.  
  
- 코드를 사용하여 하이브리드 컨트롤을 호스팅할 수 있습니다.  
  
### <a name="layout-support"></a>레이아웃 지원  
 다음 목록에서는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소가 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 시스템에 통합 하려고 할 때 알려진 제한 사항을 설명 합니다.  
  
- 경우에 따라 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤은 크기를 조정할 수 없거나 특정 차원으로만 크기를 조정할 수 있습니다. 예를 들어, [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.ComboBox> 컨트롤은 컨트롤의 글꼴 크기에 따라 정의 되는 단일 높이도 지원 합니다. 요소가 세로로 확대 될 수 있다고 가정 하는 <xref:System.Windows.Forms.ComboBox> 동적레이아웃에서호스팅된컨트롤은예상대로확장되지않습니다.[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]  
  
- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 회전하거나 기울일 수 없습니다. 예를 들어, 사용자 인터페이스를 90도 회전하면 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤이 수직 위치를 유지합니다.  
  
- 대부분의 경우 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 서는 비례하여 크기 조정을 지원하지 않습니다. 컨트롤의 전체 크기는 조정할 수 있지만, 컨트롤의 구성 요소와 자식 컨트롤의 크기가 예상대로 조정되지 않을 수 있습니다. 이 제한 사항은 각 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에서 얼마나 효과적으로 크기 조정을 지원하는지에 따라 달라집니다.  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용자 인터페이스에서 겹치는 동작을 제어하기 위해 요소의 z 순서를 변경할 수 있습니다. 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤은 개별 HWND에서 그려지므로 항상 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 요소 위에 그려집니다.  
  
- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤은 컨트롤 크기에 따라 자동 크기 조정을 지원합니다. 개별 요소의 크기는 동적으로 조정할 수 있지만 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용자 인터페이스에서 글꼴 크기를 변경해도 전체 레이아웃의 크기는 조정되지 않습니다.  
  
### <a name="ambient-properties"></a>앰비언트 속성  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤의 일부 앰비언트 속성에는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]에 해당하는 속성이 있습니다. 이러한 앰비언트 속성은 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤로 전파 되 고 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤에 공용 속성으로 노출 됩니다. 컨트롤 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 은 각 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 앰비언트 속성을 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 해당 하는로 변환 합니다.  
  
 자세한 내용은 [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)을 참조하세요.  
  
### <a name="behavior"></a>동작  
 다음 테이블에서는 상호 운용성 동작을 설명합니다.  
  
|동작|지원함|지원되지 않음|  
|--------------|---------------|-------------------|  
|투명도|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤 렌더링에서는 투명도를 지원합니다. 부모 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤의 배경이 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤의 배경이 될 수 있습니다.|일부 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에서는 투명도를 지원하지 않습니다. 예를 들어, <xref:System.Windows.Forms.TextBox> 및 <xref:System.Windows.Forms.ComboBox> 컨트롤은에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]호스팅될 때 투명 하지 않습니다.|  
|탭 이동|호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤의 탭 순서는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 기반 애플리케이션에서 해당 컨트롤을 호스팅할 때와 동일합니다.<br /><br /> Tab 키와 Shift+Tab을 사용하여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에서 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤로 탭을 이동하는 기능은 정상적으로 작동합니다.<br /><br /> [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]<xref:System.Windows.Forms.Control.TabStop%2A> 속성 값이 인 `false` 컨트롤은 사용자가 컨트롤을 통해 탭 할 때 포커스를 받지 않습니다.<br /><br /> -각 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤 <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A> 에는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤이 포커스를 받는 시기를 결정 하는 값이 있습니다.<br />-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]<xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨테이너 내에 포함 된 컨트롤은 <xref:System.Windows.Forms.Control.TabIndex%2A> 속성으로 지정 된 순서를 따릅니다. 마지막 탭 인덱스에서 탭 이동하면 다음 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤(있는 경우)에 포커스를 둡니다. 기타 포커스 가능 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이 없으면, 탭 순서에서 첫 번째에 있는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 탭 이동이 반환됩니다.<br />-   <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A>내 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤의 값은 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤에 포함 된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 형제 컨트롤을 기준으로 합니다.<br />-   탭 이동은 컨트롤별 동작을 준수합니다. 예를 들어 <xref:System.Windows.Forms.TextBox> <xref:System.Windows.Forms.TextBoxBase.AcceptsTab%2A> 속성 값 `true` 이 인 컨트롤에서 tab 키를 누르면 포커스가 이동 하는 대신 텍스트 상자에 탭이 들어갑니다.|해당 사항 없음.|  
|화살표 키를 사용하여 탐색|- <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤에서 화살표 키를 사용 하는 탐색은 일반 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨테이너 컨트롤과 동일 합니다. 위쪽 화살표 및 왼쪽 화살표 키는 이전 컨트롤을 선택 하 고 아래쪽 화살표 및 오른쪽 화살표 키는 다음 컨트롤을 선택 합니다.<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤에 포함 된 첫 번째 컨트롤의 위쪽 화살표 및 왼쪽 화살표 키가 SHIFT + TAB 바로 가기 키와 동일한 작업을 수행 합니다. 포커스를 받을 수 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 있는 컨트롤이 있는 경우 포커스는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤 외부로 이동 합니다. 이 동작은 마지막 컨트롤에 대 <xref:System.Windows.Forms.ContainerControl> 한 배치가 발생 하지 않는다는 점에서 표준 동작과 다릅니다. 기타 포커스 가능 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이 없으면, 탭 순서에서 마지막에 있는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 포커스가 반환됩니다.<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤에 포함 된 마지막 컨트롤의 아래쪽 화살표 및 오른쪽 화살표 키는 TAB 키와 동일한 작업을 수행 합니다. 포커스를 받을 수 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 있는 컨트롤이 있는 경우 포커스는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤 외부로 이동 합니다. 이 동작은 첫 번째 컨트롤에 <xref:System.Windows.Forms.ContainerControl> 대 한 배치가 발생 하지 않는다는 점에서 표준 동작과 다릅니다. 기타 포커스 가능 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이 없으면 탭 순서에서 첫 번째에 있는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 포커스가 반환됩니다.|해당 사항 없음.|  
|액셀러레이터|“지원되지 않음” 열에 명시된 경우를 제외하고는 액셀러레이터가 정상적으로 작동합니다.|기술 전체에서 중복된 액셀러레이터는 일반 중복 액셀러레이터처럼 작동하지 않습니다. 액셀러레이터가 기술 전체에 걸쳐 중복되어 있어, 하나 이상이 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 있고 다른 하나는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에 있으면 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에서 항상 액셀러레이터를 받습니다. 중복 액셀러레이터를 누르면 컨트롤 간에 포커스가 전환되지 않습니다.|  
|바로 가기 키|“지원되지 않음” 열에 명시된 경우를 제외하고는 바로 가기 키가 정상적으로 작동합니다.|전처리 단계에서 처리하는 -   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 바로 가기 키는 항상 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 바로 가기 키보다 우선합니다. 예를 들어 ctrl + s 바로 <xref:System.Windows.Forms.ToolStrip> 가기 키가 정의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 된 컨트롤이 있고 <xref:System.Windows.Forms.ToolStrip> ctrl + s에 바인딩된 명령이 있는 경우 포커스에 관계 없이 항상 먼저 제어 처리기가 호출 됩니다.<br />-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]<xref:System.Windows.Forms.Control.KeyDown> 이벤트에서 처리 하는 바로 가기 키는에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]마지막으로 처리 됩니다. 컨트롤의 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.Control.IsInputKey%2A> 메서드를 재정의 하거나 이벤트를 <xref:System.Windows.Forms.Control.PreviewKeyDown> 처리 하 여이 동작을 방지할 수 있습니다. `true` <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A?displayProperty=nameWithType> 메서드에서를 반환 `true` 하거나 이벤트<xref:System.Windows.Forms.Control.PreviewKeyDown> 처리기에서 속성의 값을로 설정 합니다. <xref:System.Windows.Forms.Control.IsInputKey%2A>|  
|AcceptsReturn, AcceptsTab 및 기타 컨트롤별 동작|기본 키보드 동작을 변경 하는 속성은 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤이 메서드를 <xref:System.Windows.Forms.Control.IsInputKey%2A> 재정의 하 여를 반환 `true`한다고 가정 하 고 평소 처럼 작동 합니다.|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]이벤트를 <xref:System.Windows.Forms.Control.KeyDown> 처리 하 여 기본 키보드 동작을 변경 하는 컨트롤은 호스트 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에서 마지막으로 처리 됩니다. 이러한 컨트롤은 마지막으로 처리되므로 예기치 않은 동작이 발생할 수 있습니다.|  
|시작 및 종료 이벤트|포커스가 포함 <xref:System.Windows.Forms.Integration.ElementHost> 하는 컨트롤로 이동 하지 않는 경우 단일 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤에서 포커스가 변경 되 면 평소와 같이 Enter 및 Leave 이벤트가 발생 합니다.|다음 포커스 변경이 발생하면 시작 및 종료 이벤트는 발생하지 않습니다.<br /><br /> -내부에서 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤 바깥쪽으로<br />-외부에서 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤 내에 있습니다.<br />-컨트롤 외부 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 에 있습니다.<br />- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤<xref:System.Windows.Forms.Integration.WindowsFormsHost> 에호스팅된<xref:System.Windows.Forms.Integration.WindowsFormsHost>컨트롤에서 동일한 내에 호스팅된 컨트롤로 <xref:System.Windows.Forms.Integration.ElementHost>|  
|다중 스레딩|모든 종류의 다중 스레딩이 지원됩니다.|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기술에서는 단일 스레드 동시 모델을 가정합니다. 디버깅 중에 다른 스레드에서 프레임워크 개체를 호출하면 이 요구 사항을 적용하기 위해 예외가 발생합니다.|  
|보안|모든 상호 운용성 시나리오에는 완전 신뢰가 필요합니다.|부분 신뢰에서는 상호 운용성 시나리오가 허용되지 않습니다.|  
|액세스 가능성|모든 접근성 시나리오가 지원됩니다. [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이 모두 포함된 하이브리드 응용 프로그램에 사용될 때 보조 기술 제품이 올바르게 작동합니다.|해당 사항 없음.|  
|클립보드|모든 클립보드 작업이 정상적으로 작동합니다. 이 작업에는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 간에 잘라내기 및 붙여넣기가 포함됩니다.|해당 사항 없음.|  
|끌어서 놓기 기능|끌어서 놓기 작업이 모두 정상적으로 작동합니다. 이 작업에는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 간의 작업이 포함됩니다.|해당 사항 없음.|  
  
<a name="Windows_Forms_Application_Hosting_Windows"></a>   
## <a name="hosting-wpf-controls-in-windows-forms"></a>Windows Forms에서 WPF 컨트롤 호스팅  
 Windows Forms 컨트롤에서 컨트롤을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 호스트 하는 경우 다음과 같은 상호 운용 시나리오가 지원 됩니다.  
  
- 코드를 사용하여 하나 이상의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 호스팅.  
  
- 속성 시트를 호스팅된 하나 이상의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤과 연결.  
  
- 양식에서 하나 이상의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 페이지 호스팅.  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 창 시작.  
  
- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 마스터와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 세부 정보를 사용하여 마스터/세부 정보 호스팅.  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 마스터와 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 세부 정보를 사용하여 마스터/세부 정보 호스팅.  
  
- 사용자 지정 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 호스팅.  
  
- 하이브리드 컨트롤 호스팅.  
  
### <a name="ambient-properties"></a>앰비언트 속성  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤의 일부 앰비언트 속성에는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에 해당하는 속성이 있습니다. 이러한 앰비언트 속성은 호스팅된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤로 전파 되 고 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에 공용 속성으로 노출 됩니다. 컨트롤 <xref:System.Windows.Forms.Integration.ElementHost> 은 각 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 앰비언트 속성을 해당 하 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 는로 변환 합니다.  
  
 자세한 내용은 [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)을 참조하세요.  
  
### <a name="behavior"></a>동작  
 다음 테이블에서는 상호 운용성 동작을 설명합니다.  
  
|동작|지원함|지원되지 않음|  
|--------------|---------------|-------------------|  
|투명도|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 렌더링에서는 투명도를 지원합니다. 부모 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤의 배경이 호스팅된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤의 배경이 될 수 있습니다.|해당 사항 없음.|  
|다중 스레딩|모든 종류의 다중 스레딩이 지원됩니다.|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기술에서는 단일 스레드 동시 모델을 가정합니다. 디버깅 중에 다른 스레드에서 프레임워크 개체를 호출하면 이 요구 사항을 적용하기 위해 예외가 발생합니다.|  
|보안|모든 상호 운용성 시나리오에는 완전 신뢰가 필요합니다.|부분 신뢰에서는 상호 운용성 시나리오가 허용되지 않습니다.|  
|액세스 가능성|모든 접근성 시나리오가 지원됩니다. [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이 모두 포함된 하이브리드 응용 프로그램에 사용될 때 보조 기술 제품이 올바르게 작동합니다.|해당 사항 없음.|  
|클립보드|모든 클립보드 작업이 정상적으로 작동합니다. 이 작업에는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 간에 잘라내기 및 붙여넣기가 포함됩니다.|해당 사항 없음.|  
|끌어서 놓기 기능|끌어서 놓기 작업이 모두 정상적으로 작동합니다. 이 작업에는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 간의 작업이 포함됩니다.|이 오류에는 이 작업을 적용할 수 없습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [연습: WPF에서 Windows Forms 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
- [연습: WPF에서 Windows Forms 복합 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [연습: Windows Forms에서 WPF 복합 컨트롤 호스팅](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)
