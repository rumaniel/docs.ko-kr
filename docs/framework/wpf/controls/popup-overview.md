---
title: Popup 개요
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], Popup
- Popup control [WPF], about Popup control
ms.assetid: 774f53ca-bff8-470e-9ce9-3928b4cf3d4c
ms.openlocfilehash: 7e6977737d362fd0df6321702bb8a1ac6cad66e0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951438"
---
# <a name="popup-overview"></a>Popup 개요
컨트롤 <xref:System.Windows.Controls.Primitives.Popup> 은 지정 된 요소 또는 화면 좌표를 기준으로 현재 응용 프로그램 창에 표시 되는 별도의 창에 콘텐츠를 표시 하는 방법을 제공 합니다. 이 항목에서는 <xref:System.Windows.Controls.Primitives.Popup> 컨트롤을 소개 하 고 사용에 대 한 정보를 제공 합니다.  

<a name="What_Is_a_Popup_"></a>   
## <a name="what-is-a-popup"></a>Popup이란?  
 컨트롤 <xref:System.Windows.Controls.Primitives.Popup> 은 화면의 요소나 요소에 상대적인 별도의 창에 콘텐츠를 표시 합니다. 이 표시 되 면 속성은로 `true`설정 됩니다. <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> <xref:System.Windows.Controls.Primitives.Popup>  
  
> [!NOTE]
> 는 <xref:System.Windows.Controls.Primitives.Popup> 마우스 포인터가 부모 개체 위로 이동할 때 자동으로 열리지 않습니다. 가 <xref:System.Windows.Controls.Primitives.Popup> 자동으로 열리도록 하려면 <xref:System.Windows.Controls.ToolTip> 또는 <xref:System.Windows.Controls.ToolTipService> 클래스를 사용 합니다. 자세한 내용은 [ToolTip 개요](tooltip-overview.md)를 참조하세요.  
  
<a name="APopupExample"></a>   
## <a name="creating-a-popup"></a>팝업 만들기  
 다음 예제에서는 <xref:System.Windows.Controls.Button> 컨트롤의 자식 요소인 컨트롤 <xref:System.Windows.Controls.Primitives.Popup> 을 정의 하는 방법을 보여 줍니다. 에 <xref:System.Windows.Controls.Button> 는 자식 요소가 하나만 있을 수 있기 때문에이 예제에서는 <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.StackPanel>및 <xref:System.Windows.Controls.Primitives.Popup> 컨트롤에 대 한 텍스트를에 배치 합니다. 의 콘텐츠 <xref:System.Windows.Controls.Primitives.Popup> 는 <xref:System.Windows.Controls.TextBlock> 컨트롤에 표시 됩니다 .이 컨트롤은 관련 <xref:System.Windows.Controls.Button> 컨트롤 근처의 응용 프로그램 창에 표시 되는 별도의 창에 텍스트를 표시 합니다.  
  
 [!code-xaml[PopupSimple#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#1)]  
  
 [!code-xaml[PopupSimple#CreatePopupCodeXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#createpopupcodexaml)]  
  
<a name="PopupUses"></a>   
## <a name="controls-that-implement-a-popup"></a>Popup을 구현하는 컨트롤  
 다른 컨트롤에 <xref:System.Windows.Controls.Primitives.Popup> 컨트롤을 빌드할 수 있습니다. 다음 컨트롤은 특정 용도 <xref:System.Windows.Controls.Primitives.Popup> 에 맞게 컨트롤을 구현 합니다.  
  
- <xref:System.Windows.Controls.ToolTip>. 요소에 대 한 도구 설명을 만들려는 경우 <xref:System.Windows.Controls.ToolTip> 및 <xref:System.Windows.Controls.ToolTipService> 클래스를 사용 합니다. 자세한 내용은 [ToolTip 개요](tooltip-overview.md)를 참조하세요.  
  
- <xref:System.Windows.Controls.ContextMenu>. 요소에 대 한 상황에 맞는 메뉴를 만들려면 <xref:System.Windows.Controls.ContextMenu> 컨트롤을 사용 합니다. 자세한 내용은 [ContextMenu 개요](contextmenu-overview.md)를 참조하세요.  
  
- <xref:System.Windows.Controls.ComboBox>. 표시 하거나 숨길 수 있는 드롭다운 목록 상자를 포함 하는 선택 컨트롤을 만들려면 <xref:System.Windows.Controls.ComboBox> 컨트롤을 사용 합니다.  
  
- <xref:System.Windows.Controls.Expander>. 콘텐츠를 표시 하는 축소 가능한 영역을 포함 하는 머리글을 표시 하는 컨트롤을 만들려면 <xref:System.Windows.Controls.Expander> 컨트롤을 사용 합니다. 자세한 내용은 [Expander 개요](expander-overview.md)를 참조하세요.  
  
<a name="PopupBehaviorandAppearance"></a>   
## <a name="popup-behavior-and-appearance"></a>Popup 동작 및 모양  
 컨트롤 <xref:System.Windows.Controls.Primitives.Popup> 은 동작 및 모양을 사용자 지정할 수 있는 기능을 제공 합니다. 예를 들어 열기 및 닫기 동작, 애니메이션, 불투명도 및 비트맵 효과, <xref:System.Windows.Controls.Primitives.Popup> 크기 및 위치를 설정할 수 있습니다.  
  
<a name="OpenandCloseBehavior"></a>   
### <a name="open-and-close-behavior"></a>열기 및 닫기 동작  
 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> <xref:System.Windows.Controls.Primitives.Popup> 속성이 로`true`설정 된 경우 컨트롤은 해당 내용을 표시 합니다. 기본적 <xref:System.Windows.Controls.Primitives.Popup> 으로는 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> 속성이로 `false`설정 될 때까지 열린 상태로 유지 됩니다. 그러나 <xref:System.Windows.Controls.Primitives.Popup.StaysOpen%2A> 속성을로 `false`설정 하 여 기본 동작을 변경할 수 있습니다. 이 속성을로 `false` <xref:System.Windows.Controls.Primitives.Popup> 설정 하면 내용 창에 마우스 캡처가 있습니다. <xref:System.Windows.Controls.Primitives.Popup> 마우스 캡처가 <xref:System.Windows.Controls.Primitives.Popup> 손실 되 고 창 외부에서 마우스 이벤트가 발생할 때 창이 닫힙니다.  
  
 <xref:System.Windows.Controls.Primitives.Popup.Opened> 및<xref:System.Windows.Controls.Primitives.Popup.Closed>이벤트는 콘텐츠창이열리거나닫힐<xref:System.Windows.Controls.Primitives.Popup> 때 발생 합니다.  
  
<a name="Animation"></a>   
### <a name="animation"></a>애니메이션  
 <xref:System.Windows.Controls.Primitives.Popup> 컨트롤에는 일반적으로 페이드 인 및 슬라이드와 같은 동작과 연결 되는 애니메이션에 대 한 지원이 기본적으로 제공 됩니다. <xref:System.Windows.Controls.Primitives.Popup.PopupAnimation%2A> 속성을 <xref:System.Windows.Controls.Primitives.PopupAnimation> 열거형 값으로 설정 하 여 이러한 애니메이션을 켤 수 있습니다. 애니메이션이 제대로 작동 하려면 <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> 속성을로 `true`설정 해야 합니다. <xref:System.Windows.Controls.Primitives.Popup>  
  
 컨트롤에 같은 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션을 적용할 수도 있습니다. <xref:System.Windows.Controls.Primitives.Popup>  
  
<a name="OpacityandBitmapEffects"></a>   
### <a name="opacity-and-bitmap-effects"></a>불투명도 및 비트맵 효과  
 컨트롤의 속성은 <xref:System.Windows.UIElement.Opacity%2A> 내용에 영향을 주지 않습니다. <xref:System.Windows.Controls.Primitives.Popup> 기본적 <xref:System.Windows.Controls.Primitives.Popup> 으로 콘텐츠 창은 불투명 합니다. 투명 <xref:System.Windows.Controls.Primitives.Popup>을 만들려면 <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> 속성을로 `true`설정 합니다.  
  
 의 <xref:System.Windows.Controls.Primitives.Popup> 콘텐츠는 <xref:System.Windows.Controls.Primitives.Popup> 컨트롤 또는 부모 창에 있는 다른 요소에 <xref:System.Windows.Media.Effects.DropShadowBitmapEffect>직접 설정 하는 등의 비트맵 효과를 상속 하지 않습니다. 비트맵 효과가의 <xref:System.Windows.Controls.Primitives.Popup>내용에 표시 되 게 하려면 해당 콘텐츠에 직접 비트맵 효과를 설정 해야 합니다. 예를 들어의 <xref:System.Windows.Controls.Primitives.Popup> 자식이 <xref:System.Windows.Controls.StackPanel>인 경우에 <xref:System.Windows.Controls.StackPanel>비트맵 효과를 설정 합니다.  
  
<a name="PopupSize"></a>   
### <a name="popup-size"></a>Popup 크기  
 기본적으로는 <xref:System.Windows.Controls.Primitives.Popup> 내용에 맞게 자동으로 크기가 조정 됩니다. 자동 크기 조정을 수행 하는 경우 <xref:System.Windows.Controls.Primitives.Popup> 콘텐츠에 대해 정의 된 화면 영역의 기본 크기에서 비트맵 효과를 표시 하는 데 충분 한 공간을 제공 하지 않기 때문에 일부 비트맵 효과를 숨길 수 있습니다.  
  
 <xref:System.Windows.Controls.Primitives.Popup>콘텐츠에를 설정 하는 경우에 <xref:System.Windows.UIElement.RenderTransform%2A> 도 콘텐츠가 가려져 있을 수 있습니다. 이 시나리오에서는 변환 <xref:System.Windows.Controls.Primitives.Popup> 된 내용이 원래 <xref:System.Windows.Controls.Primitives.Popup>영역을 벗어나 확장 되는 경우 일부 콘텐츠가 숨겨져 있을 수 있습니다. 비트맵 효과 또는 변환에 더 많은 공간이 필요한 경우 컨트롤에 더 많은 영역을 제공 <xref:System.Windows.Controls.Primitives.Popup> 하기 위해 콘텐츠 주위에 여백을 정의할 수 있습니다.  
  
<a name="DefiningPopupPosition"></a>   
## <a name="defining-the-popup-position"></a>Popup 위치 정의  
 설정 하 여 팝업을 배치할 수는 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>, <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>, <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>, <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>, 및 <xref:System.Windows.Controls.Primitives.Popup.VerticalOffsetProperty> 속성입니다. 자세한 내용은 [Popup 배치 동작](popup-placement-behavior.md)을 참조하세요. 때 <xref:System.Windows.Controls.Primitives.Popup> 표시 되는 화면에서 이전 위치를 자체 나면 부모가 재배치 된 경우.  
  
<a name="CustomizingPopupPlacement"></a>   
### <a name="customizing-popup-placement"></a>Popup 배치 사용자 지정  
 을 표시할에 상대적인 <xref:System.Windows.Controls.Primitives.Popup> <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> <xref:System.Windows.Controls.Primitives.Popup> 좌표 집합을 지정 하 여 컨트롤의 배치를 사용자 지정할 수 있습니다.  
  
 배치를 사용자 지정 하려면 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성을로 <xref:System.Windows.Controls.Primitives.PlacementMode.Custom>설정 합니다. 그런 다음 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> <xref:System.Windows.Controls.Primitives.Popup>에 대 한 가능한 배치 지점과 기본 축 (기본 설정 순서 대로) 집합을 반환 하는 대리자를 정의 합니다. 의 가장 큰 부분을 표시 하는 점이 <xref:System.Windows.Controls.Primitives.Popup> 자동으로 선택 됩니다. 예제를 보려면 [사용자 지정 팝업 위치 지정](how-to-specify-a-custom-popup-position.md)을 참조하세요.  
  
<a name="PopupandtheVisualTree"></a>   
## <a name="popup-and-the-visual-tree"></a>Popup 및 시각적 트리  
 컨트롤에는 고유한 시각적 트리가 없으며,에 대 한 <xref:System.Windows.Controls.Primitives.Popup.MeasureOverride%2A> <xref:System.Windows.Controls.Primitives.Popup> 메서드가 호출 되 면 대신 크기가 0으로 반환 됩니다. <xref:System.Windows.Controls.Primitives.Popup> 그러나의 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> <xref:System.Windows.Controls.Primitives.Popup> 속성을로 `true`설정 하면 고유한 시각적 트리가 있는 새 창이 만들어집니다. 새 창에는의 <xref:System.Windows.Controls.Primitives.Popup.Child%2A> <xref:System.Windows.Controls.Primitives.Popup>내용이 포함 되어 있습니다. 새 창의 너비와 높이는 화면 너비 또는 높이의 75%를 초과할 수 없습니다.  
  
 컨트롤 <xref:System.Windows.Controls.Primitives.Popup> 은 해당 <xref:System.Windows.Controls.Primitives.Popup.Child%2A> 콘텐츠에 대 한 참조를 논리 자식으로 유지 관리 합니다. 새 창이 만들어지면의 <xref:System.Windows.Controls.Primitives.Popup> 콘텐츠는 창의 시각적 자식이 되 고의 <xref:System.Windows.Controls.Primitives.Popup>논리적 자식으로 유지 됩니다. 반대로는 해당 <xref:System.Windows.Controls.Primitives.Popup.Child%2A> 콘텐츠의 논리적 부모를 유지합니다.<xref:System.Windows.Controls.Primitives.Popup>  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Primitives.Popup>
- <xref:System.Windows.Controls.Primitives.PopupPrimaryAxis>
- <xref:System.Windows.Controls.Primitives.PlacementMode>
- <xref:System.Windows.Controls.Primitives.CustomPopupPlacement>
- <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>
- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipService>
- [방법 항목](popup-how-to-topics.md)
- [방법 항목](tooltip-how-to-topics.md)
