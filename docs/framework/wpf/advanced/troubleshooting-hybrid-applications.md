---
title: 혼합 애플리케이션 문제 해결
ms.date: 03/30/2017
helpviewer_keywords:
- overlapping controls [WPF]
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- hybrid applications [WPF interoperability]
- message loops [WPF]
ms.assetid: f440c23f-fa5d-4d5a-852f-ba61150e6405
ms.openlocfilehash: 707e77ac69878c1c7fb8e975c1f90ad657228d1a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61696437"
---
# <a name="troubleshooting-hybrid-applications"></a>혼합 애플리케이션 문제 해결
<a name="introduction"></a> 이 항목에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 기술을 둘 다 사용하는 혼합 응용 프로그램을 작성할 때 발생할 수 있는 몇 가지 일반적인 문제에 대해 설명합니다.  

<a name="overlapping_controls"></a>   
## <a name="overlapping-controls"></a>컨트롤 겹침  
 컨트롤이 예상대로 겹치지 않을 수 있습니다. [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]는 각 컨트롤에 대해 별도의 HWND를 사용합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 페이지의 모든 콘텐츠에 대해 하나의 HWND를 사용합니다. 이러한 구현 차이로 인해 예기치 않은 겹치는 동작이 발생합니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 호스트되는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤은 항상 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 위에 나타납니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 호스팅되는 콘텐츠를 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤의 z 순서에 표시 되는 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤입니다. 겹칠 수 있기 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤 이지만 호스팅된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 결합 하거나 상호 작용 하지 않습니다.  
  
<a name="child_property"></a>   
## <a name="child-property"></a>자식 속성  
 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 고 <xref:System.Windows.Forms.Integration.ElementHost> 클래스는 단일 자식 컨트롤이 나 요소만 호스트할 수 있습니다. 둘 이상의 컨트롤이나 요소를 호스트하려면 컨테이너를 자식 콘텐츠로 사용해야 합니다. 예를 들어, 추가할 수 있습니다 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 단추 및 확인란 컨트롤을를 <xref:System.Windows.Forms.Panel?displayProperty=nameWithType> 컨트롤을 패널에 할당 한 다음는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤의 <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A> 속성입니다. 그러나 추가할 수 없습니다 단추 및 확인란 컨트롤을 별도로 동일한 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 제어 합니다.  
  
<a name="scaling"></a>   
## <a name="scaling"></a>배율 조정  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]는 배율 조정 모델이 서로 다릅니다. 일부 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 배율 조정 변환은 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에서 의미가 있지만 일부는 그렇지 않습니다. 예를 들어 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤의 배율을 0으로 조정할 수 있지만 동일한 컨트롤의 배율을 0이 아닌 값으로 다시 조정하려고 하면 컨트롤의 크기가 0으로 유지됩니다. 자세한 내용은 [WindowsFormsHost 요소에 대한 레이아웃 고려 사항](layout-considerations-for-the-windowsformshost-element.md)을 참조하세요.  
  
<a name="adapter"></a>   
## <a name="adapter"></a>어댑터  
 작업할 때 혼동 수는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 및 <xref:System.Windows.Forms.Integration.ElementHost> 숨겨진된 컨테이너가 포함 되어 있으므로 클래스. 모두를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 및 <xref:System.Windows.Forms.Integration.ElementHost> 클래스 라는 숨겨진된 컨테이너가는 *어댑터*, 콘텐츠를 호스트를 사용 하 여 합니다. 에 대 한 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 에서 파생 되는 요소, 어댑터는 <xref:System.Windows.Forms.ContainerControl?displayProperty=nameWithType> 클래스입니다. 에 대 한 합니다 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에서 파생 되는 어댑터는 <xref:System.Windows.Controls.DockPanel> 요소입니다. 다른 상호 운용성 항목에 어댑터에 대한 참조가 표시되는 경우 이 컨테이너에 대해 설명하는 것입니다.  
  
<a name="nesting"></a>   
## <a name="nesting"></a>중첩  
 중첩을 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 내부 요소는 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤이 지원 되지 않습니다. 중첩 된 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤 내부를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소도 지원 되지 않습니다.  
  
<a name="focus"></a>   
## <a name="focus"></a>포커스  
 포커스는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]에서 다르게 작동합니다. 즉, 혼합 애플리케이션에서는 포커스 문제가 발생할 수 있습니다. 예를 들어, 내에 포커스가 있는 경우는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소와 하거나 최소화 및 페이지를 복원 하거나 모달 대화 상자를 표시, 안의 포커스가 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소가 손실 될 수 있습니다. <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소 계속 포커스가 있지만 컨트롤 내부 없을 수 있습니다.  
  
 데이터 유효성 검사도 포커스의 영향을 받습니다. 작동 하는 유효성 검사를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 개 tab 키를 누르면 요소가 있지만 작동 하지 않는 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소 간에 또는 서로 다른 두 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소입니다.  
  
<a name="property_mapping"></a>   
## <a name="property-mapping"></a>속성 매핑  
 일부 속성 매핑에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 기술 간의 다른 구현을 연결하려면 광범위한 해석이 필요합니다. 속성 매핑을 사용하면 코드가 글꼴, 색 및 기타 속성의 변경에 반응하도록 할 수 있습니다. 일반적으로 속성 매핑은 *Property*Changed 이벤트나 On*Property*Changed 호출을 수신 대기하고 자식 컨트롤이나 해당 어댑터에서 적절한 속성을 설정하여 작동합니다. 자세한 내용은 [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)을 참조하세요.  
  
<a name="layoutrelated_properties_on_hosted_content"></a>   
## <a name="layout-related-properties-on-hosted-content"></a>호스트된 콘텐츠의 레이아웃 관련 속성  
 경우는 <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.Integration.ElementHost.Child%2A?displayProperty=nameWithType> 속성이 할당 되 면 호스트 된 콘텐츠의 여러 레이아웃 관련 속성이 자동으로 설정 됩니다. 이러한 콘텐츠 속성을 변경하면 예기치 않은 레이아웃 동작이 발생할 수 있습니다.  
  
 호스트 된 콘텐츠를 채우도록 도킹 됩니다 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 고 <xref:System.Windows.Forms.Integration.ElementHost> 부모입니다. 이 채우기 동작을 사용하려면 자식 속성을 설정할 때 여러 가지 속성을 설정합니다. 다음 표에서 콘텐츠 속성으로 설정 합니다 <xref:System.Windows.Forms.Integration.ElementHost> 및 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 클래스입니다.  
  
|호스트 클래스|콘텐츠 속성|  
|----------------|------------------------|  
|<xref:System.Windows.Forms.Integration.ElementHost>|<xref:System.Windows.FrameworkElement.Height%2A><br /><br /> <xref:System.Windows.FrameworkElement.Width%2A><br /><br /> <xref:System.Windows.FrameworkElement.Margin%2A><br /><br /> <xref:System.Windows.FrameworkElement.VerticalAlignment%2A><br /><br /> <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>|  
|<xref:System.Windows.Forms.Integration.WindowsFormsHost>|<xref:System.Windows.Forms.Control.Margin%2A><br /><br /> <xref:System.Windows.Forms.Control.Dock%2A><br /><br /> <xref:System.Windows.Forms.Control.AutoSize%2A><br /><br /> <xref:System.Windows.Forms.Control.Location%2A><br /><br /> <xref:System.Windows.Forms.Control.MaximumSize%2A>|  
  
 호스트된 콘텐츠에서 직접 이러한 속성을 설정하지 마세요. 자세한 내용은 [WindowsFormsHost 요소에 대한 레이아웃 고려 사항](layout-considerations-for-the-windowsformshost-element.md)을 참조하세요.  
  
<a name="navigation_applications"></a>   
## <a name="navigation-applications"></a>탐색 애플리케이션  
 탐색 애플리케이션에서 사용자 상태를 유지하지 않을 수 있습니다. <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소 탐색 응용 프로그램에서 사용 하는 경우 해당 컨트롤을 다시 만듭니다. 때 사용자가 호스트 하는 페이지에서 자식 컨트롤 다시 만들기는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소 및이를 반환 합니다. 사용자가 입력한 모든 콘텐츠가 손실됩니다.  
  
<a name="message_loop_interoperation"></a>   
## <a name="message-loop-interoperation"></a>메시지 루프 상호 운용성  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 메시지 루프로 작업할 때 메시지가 예상대로 처리되지 않을 수 있습니다. 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> 메서드를 호출 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 생성자입니다. 이 메서드는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 메시지 루프에 메시지 필터를 추가합니다. 이 필터를 호출 합니다 <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=nameWithType> 메서드 경우는 <xref:System.Windows.Forms.Control?displayProperty=nameWithType> 메시지의 대상이 되 고 메시지를 변환/디스패치 됩니다.  
  
 표시 하는 경우를 <xref:System.Windows.Window> 에 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 메시지 루프를 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType>를 호출 하지 않으면 아무 것도 입력할 수 없습니다는 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> 메서드. <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> 메서드를 <xref:System.Windows.Window> 추가 <xref:System.Windows.Forms.IMessageFilter?displayProperty=nameWithType>, 키 관련 메시지를 다시 라우팅하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 메시지 루프입니다. 자세한 내용은 [Windows Forms 및 WPF 상호 운용성 입력 아키텍처](windows-forms-and-wpf-interoperability-input-architecture.md)를 참조하세요.  
  
<a name="opacity_and_layering"></a>   
## <a name="opacity-and-layering"></a>불투명도 및 레이어  
 <xref:System.Windows.Interop.HwndHost> 클래스 계층을 지원 하지 않습니다. 즉, 해당 설정을 <xref:System.Windows.UIElement.Opacity%2A> 속성에는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소에 영향을 주지 않습니다 개이고 혼합이 발생 하지 다른 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 있는 windows <xref:System.Windows.Window.AllowsTransparency%2A> 로 `true`.  
  
<a name="dispose"></a>   
## <a name="dispose"></a>Dispose  
 클래스를 올바르게 삭제하지 않으면 리소스가 누출될 수 있습니다. 하이브리드 응용 프로그램에 있는지 확인 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 및 <xref:System.Windows.Forms.Integration.ElementHost> 클래스가 삭제 또는 리소스가 누출 될 수 있습니다. [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 삭제 <xref:System.Windows.Forms.Integration.ElementHost> 시기를 제어 해당 비 모달 <xref:System.Windows.Forms.Form> 부모 닫힙니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 삭제 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 응용 프로그램이 종료 될 때 요소입니다. 표시할 수는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소에는 <xref:System.Windows.Window> 에 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 메시지 루프입니다. 이 경우 코드에서 애플리케이션이 종료되고 있다는 알림을 받을 수 없습니다.  
  
<a name="enabling_visual_styles"></a>   
## <a name="enabling-visual-styles"></a>비주얼 스타일 사용  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에서 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 비주얼 스타일을 사용할 수 없습니다. 합니다 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> 에 대 한 템플릿에서 호출을 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 응용 프로그램입니다. 이 메서드는 기본적으로 호출되지 않지만 Comctl32.dll 버전 6.0을 사용할 수 있는 경우 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]를 사용하여 프로젝트를 만들면 컨트롤에 대한 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 비주얼 스타일이 제공됩니다. 호출 해야 합니다 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 메서드 핸들 스레드에서 생성 되기 전에 합니다. 자세한 내용은 [방법: 하이브리드 응용 프로그램에서 비주얼 스타일 사용](how-to-enable-visual-styles-in-a-hybrid-application.md)합니다.  
  
<a name="licensed_controls"></a>   
## <a name="licensed-controls"></a>사용이 허가된 컨트롤  
 사용자에 대한 메시지 상자에 라이선스 정보를 표시하는 사용이 허가된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤은 혼합 애플리케이션에 예기치 않은 동작을 발생시킬 수 있습니다. 일부 사용이 허가된 컨트롤은 핸들 만들기에 대한 응답으로 대화 상자를 표시합니다. 예를 들어 사용이 허가된 컨트롤은 라이선스가 필요하다거나 컨트롤의 평가판 사용이 세 개 남아 있음을 사용자에게 알릴 수 있습니다.  
  
 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소에서 파생 되는 <xref:System.Windows.Interop.HwndHost> 클래스 및 자식 컨트롤의 핸들은 내부에 생성 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A> 메서드. 합니다 <xref:System.Windows.Interop.HwndHost> 클래스에서 처리할 메시지를 허용 하지 않습니다는 <xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A> 방법 이지만 대화 상자를 표시 하면 메시지를 보낼 수 있습니다. 이 라이선스 시나리오를 사용 하려면 호출을 <xref:System.Windows.Forms.Control.CreateControl%2A?displayProperty=nameWithType> 으로 할당 하기 전에 컨트롤의 메서드는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소의 자식입니다.  
  
<a name="wpf_designer"></a>   
## <a name="wpf-designer"></a>WPF Designer  
 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]를 사용하여 WPF 콘텐츠를 디자인할 수 있습니다. 다음 섹션에서는 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]를 사용하여 혼합 애플리케이션을 작성할 때 발생할 수 있는 몇 가지 일반적인 문제에 대해 설명합니다.  
  
### <a name="backcolortransparent-is-ignored-at-design-time"></a>BackColorTransparent가 디자인 타임에 무시됨  
 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 속성에는 디자인 타임에 예상 대로 작동 하지 않을 수 있습니다.  
  
 WPF 컨트롤을 표시 되는 부모에 없는 경우 WPF 런타임에서 무시는 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 값입니다. 이유는 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 무시 될 수 있습니다 이므로 <xref:System.Windows.Forms.Integration.ElementHost> 별도의 개체를 만들 <xref:System.AppDomain>합니다. 그러나 응용 프로그램을 실행할 때 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 예상 대로 작동 합니다.  
  
### <a name="design-time-error-list-appears-when-the-obj-folder-is-deleted"></a>obj 폴더를 삭제하면 디자인 타임 오류 목록이 나타남  
 obj 폴더를 삭제하면 디자인 타임 오류 목록이 나타납니다.  
  
 사용 하 여 디자인할 때 <xref:System.Windows.Forms.Integration.ElementHost>, Windows Forms 디자이너는 프로젝트의 obj 폴더 내의 Debug 또는 Release 폴더에 생성 된 파일을 사용 합니다. 이러한 파일을 삭제하면 디자인 타임 오류 목록이 나타납니다. 이 문제를 해결하려면 프로젝트를 다시 빌드하세요. 자세한 내용은 [Windows Forms 디자이너의 디자인 타임 오류](../../winforms/controls/design-time-errors-in-the-windows-forms-designer.md)를 참조하세요.  
  
<a name="elementhost_and_ime"></a>   
## <a name="elementhost-and-ime"></a>ElementHost 및 IME  
 에 호스팅된 WPF 컨트롤을 <xref:System.Windows.Forms.Integration.ElementHost> 현재 지원 하지 않습니다는 <xref:System.Windows.Forms.Control.ImeMode%2A> 속성입니다. 변경 내용을 <xref:System.Windows.Forms.Control.ImeMode%2A> 호스트 된 컨트롤에서 무시 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [WPF Designer의 상호 운용성](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb628658(v=vs.100))
- [Windows Forms 및 WPF 상호 운용성 입력 아키텍처](windows-forms-and-wpf-interoperability-input-architecture.md)
- [방법: 하이브리드 응용 프로그램에서 비주얼 스타일 사용](how-to-enable-visual-styles-in-a-hybrid-application.md)
- [WindowsFormsHost 요소에 대한 레이아웃 고려 사항](layout-considerations-for-the-windowsformshost-element.md)
- [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)
- [Windows Forms 디자이너의 디자인 타임 오류](../../winforms/controls/design-time-errors-in-the-windows-forms-designer.md)
- [마이그레이션 및 상호 운용성](migration-and-interoperability.md)
