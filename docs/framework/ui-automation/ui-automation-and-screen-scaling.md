---
title: UI 자동화 및 화면 크기 조정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- scaling, screens
- screens, scaling
- UI (user interface), automation
- UI Automation
ms.assetid: 4380cad7-e509-448f-b9a5-6de042605fd4
ms.openlocfilehash: e0f7bd553096be0674827aa0498a53df5247940e
ms.sourcegitcommit: 77e33b682db39955e331b8e8eda4ef1925a24e78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70133774"
---
# <a name="ui-automation-and-screen-scaling"></a>UI 자동화 및 화면 크기 조정
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
Windows Vista부터 사용자는 dpi (인치당 도트 수) 설정을 변경 하 여 화면에 있는 대부분의 UI (사용자 인터페이스) 요소를 더 크게 표시할 수 있습니다. Windows에서는이 기능을 사용할 수 있었지만 이전 버전에서는 응용 프로그램에서 크기 조정을 구현 해야 했습니다. Windows Vista부터 바탕 화면 창 관리자는 자체 크기 조정을 처리 하지 않는 모든 응용 프로그램에 대해 기본 크기 조정을 수행 합니다. UI 자동화 클라이언트 애플리케이션에서는 이 기능을 고려해야 합니다.  
  
<a name="Scaling_in_Windows_Vista"></a>   
## <a name="scaling-in-windows-vista"></a>Windows Vista에서 크기 조정  
 기본 dpi 설정은 96입니다. 즉, 96 픽셀은 1 내의 추상적인 인치 너비 또는 높이를 차지 합니다. "인치"의 정확한 측정값은 모니터의 크기와 실제 해상도에 따라 달라집니다. 예를 들어, 12인치 너비의 모니터에서 1280픽셀의 수평 해상도의 경우 96픽셀의 가로줄은 1인치의 약 9/10입니다.  
  
 Dpi 설정을 변경 하는 것은 화면 해상도를 변경 하는 것과 다릅니다. Dpi 크기 조정을 사용 하는 경우 화면의 실제 픽셀 수는 동일 하 게 유지 됩니다. 하지만 크기 조정은 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소의 크기와 위치에 적용됩니다. 크기를 조정하지 말라는 메시지가 명시적으로 표시되지 않는 데스크톱 및 애플리케이션에 대해서는 바탕 화면 창 관리자가 이 크기 조정을 자동으로 수행할 수 있습니다.  
  
 실제로 사용자가 배율 인수를 120 dpi로 설정 하면 화면의 세로 또는 가로 인치가 25% 더 커집니다. 그에 따라 모든 치수가 적절하게 조정됩니다. 화면 위쪽에서 왼쪽 가장자리까지 애플리케이션 창의 오프셋이 25% 늘어납니다. 응용 프로그램 크기 조정을 사용 하 고 응용 프로그램에서 dpi를 인식 하지 못하는 경우 창의 크기는 포함 된 모든 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소의 오프셋과 크기와 함께 동일한 비율로 늘어납니다.  
  
> [!NOTE]
> 기본적으로, 사용자가 dpi를 120로 설정 하는 경우에는 비 dpi 인식 응용 프로그램에 대 한 크기 조정을 수행 하지 않지만 dpi가 사용자 지정 값 144 이상으로 설정 된 경우에는이를 수행 합니다. 그러나 사용자는 기본 동작을 재정의할 수 있습니다.  
  
 화면 크기 조정 어떤 방식으로든 화면 좌표와 관련된 애플리케이션에 대한 새로운 문제를 만듭니다. 이제 화면에는 물리적 좌표와 논리적 좌표 두 개가 포함됩니다. 점의 물리적 좌표는 원점의 왼쪽 상단에서의 픽셀 단위의 실제 오프셋입니다. 논리적 좌표는 픽셀 자체의 크기가 조정된 경우 발생되는 오프셋입니다.  
  
 좌표 (100, 48)에서 단추가 있는 대화 상자를 설계한다고 가정해 보세요. 이 대화 상자가 기본 96 dpi로 표시 되 면 단추는 (100, 48)의 물리적 좌표에 있습니다. 120 dpi에서는 (125, 60)의 물리적 좌표에 있습니다. 그러나 논리 좌표는 모든 dpi 설정에서 동일 합니다. (100, 48).  
  
 논리 좌표는 dpi 설정에 관계 없이 운영 체제와 응용 프로그램의 동작을 일관적으로 만들기 때문에 중요 합니다. 예를 들어, <xref:System.Windows.Forms.Cursor.Position%2A?displayProperty=nameWithType> 은 일반적으로 논리적 좌표를 반환합니다. 대화 상자의 요소 위로 커서를 이동 하면 dpi 설정에 관계 없이 동일한 좌표가 반환 됩니다. (100, 100)에서 컨트롤을 그리면 해당 논리적 좌표로 그려지고 모든 dpi 설정에서 동일한 상대적 위치를 차지 하 게 됩니다.  
  
<a name="Scaling_in_UI_Automation_Clients"></a>   
## <a name="scaling-in-ui-automation-clients"></a>UI 자동화 클라이언트의 크기 조정  
 API [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 는 논리적 좌표를 사용 하지 않습니다. 다음 메서드 및 속성은 물리적 좌표를 반환하거나 매개 변수로 간주합니다.  
  
- <xref:System.Windows.Automation.AutomationElement.GetClickablePoint%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.TryGetClickablePoint%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.ClickablePointProperty>  
  
- <xref:System.Windows.Automation.AutomationElement.FromPoint%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.BoundingRectangle%2A>  
  
 기본적으로 96이 아닌 환경에서 실행 되는 UI 자동화 클라이언트 응용 프로그램은 이러한 메서드와 속성에서 올바른 결과를 얻을 수 없습니다. 예를 들어, 커서 위치는 논리적 좌표에 있기 때문에 클라이언트가 이러한 좌표를 <xref:System.Windows.Automation.AutomationElement.FromPoint%2A> 에 간단히 전달하여 커서 아래에 있는 요소를 가져올 수 없습니다. 또한 애플리케이션이 클라이언트 영역 외부에 창을 올바르게 배치할 수 없습니다.  
  
 솔루션은 두 부분으로 구성됩니다.  
  
1. 먼저 클라이언트 응용 프로그램에서 dpi를 인식 하도록 설정 합니다. 이렇게 하려면 시작 시에 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 함수 `SetProcessDPIAware` 를 호출합니다. 관리 코드에서, 다음 선언을 통해 이 함수를 사용할 수 있습니다.  
  
     [!code-csharp[Highlighter#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/Highlighter/CSharp/NativeMethods.cs#101)]
     [!code-vb[Highlighter#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Highlighter/VisualBasic/NativeMethods.vb#101)]  
  
     이 함수는 전체 프로세스 dpi를 인식 합니다. 즉, 프로세스에 속하는 모든 창이 실제 크기로 설정 됩니다. 예를 들어, [형광펜 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/Highlighter)에서 강조 표시 사각형을 구성 하는 4 개의 창은 논리적 좌표가 아니라 UI 자동화에서 가져온 물리적 좌표에 있습니다. 샘플이 dpi를 인식 하지 못하는 경우 강조 표시는 데스크톱의 논리적 좌표에 그려지며 96이 아닌 환경에서 잘못 된 배치가 발생 합니다.  
  
2. 커서 좌표를 가져오려면 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 함수 `GetPhysicalCursorPos`를 호출합니다. 다음 예제에서는 이 함수를 선언하고 사용하는 방법을 보여 줍니다.  
  
     [!code-csharp[UIAClient_snip#185](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#185)]
     [!code-vb[UIAClient_snip#185](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#185)]  
  
> [!CAUTION]
> <xref:System.Windows.Forms.Cursor.Position%2A?displayProperty=nameWithType>는 사용하지 마세요. 크기가 조정된 환경에서 클라이언트 창 외부에서의 이 속성 동작이 정의되지 않았습니다.  
  
 응용 프로그램에서 dpi를 인식 하지 않는 응용 프로그램을 사용 하 여 직접 프로세스 간 통신을 수행 하는 경우 및 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] `LogicalToPhysicalPoint`함수 `PhysicalToLogicalPoint` 를 사용 하 여 논리적 좌표와 물리적 좌표 간을 변환 했을 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Highlighter Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/Highlighter)
