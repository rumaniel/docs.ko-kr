---
title: Popup 배치 동작
ms.date: 03/30/2017
helpviewer_keywords:
- popups [WPF]
- Popup control [WPF], placing
- placing popups [WPF]
- positioning popups [WPF]
ms.assetid: fbf642e9-f670-4efd-a7af-a67468a1c8e1
ms.openlocfilehash: ca984aa724cf3f076d6073aa8b8179abfb91d26c
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "69951728"
---
# <a name="popup-placement-behavior"></a>Popup 배치 동작
컨트롤 <xref:System.Windows.Controls.Primitives.Popup> 은 응용 프로그램 위에 배치 되는 별도의 창에 콘텐츠를 표시 합니다. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>, ,,<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>및속성을사용 <xref:System.Windows.Controls.Primitives.Popup> 하 여 컨트롤, 마우스 또는 화면을 기준으로의 위치를 지정할 수 있습니다. <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>  이러한 속성은 <xref:System.Windows.Controls.Primitives.Popup>함께 작동 하 여의 위치를 유연 하 게 지정할 수 있습니다.  
  
> [!NOTE]
> 또한 <xref:System.Windows.Controls.ToolTip> 및<xref:System.Windows.Controls.ContextMenu> 클래스는 이러한 다섯 가지 속성을 정의 하 고 비슷하게 동작 합니다.  

<a name="Positioning"></a>   
## <a name="positioning-the-popup"></a>Popup 위치 지정  
 의 <xref:System.Windows.Controls.Primitives.Popup> 배치는 전체 화면을 기준 <xref:System.Windows.UIElement> 으로 할 수 있습니다.  다음 예제에서는 <xref:System.Windows.UIElement>(이 <xref:System.Windows.Controls.Primitives.Popup> 경우 이미지)를 기준으로 4 개의 컨트롤을 만듭니다. 모든 컨트롤에는 `image1`로 설정 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 된 속성이 있지만 각 <xref:System.Windows.Controls.Primitives.Popup> 컨트롤에는 배치 속성에 대해 서로 다른 값이 있습니다. <xref:System.Windows.Controls.Primitives.Popup>  
  
 [!code-xaml[PopupPositionSnippet#3](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#3)]  
  
 다음 그림에서는 이미지와 <xref:System.Windows.Controls.Primitives.Popup> 컨트롤을 보여 줍니다.  
  
 ![네 개의 팝업 컨트롤이 있는 이미지](./media/popup-placement-behavior/popup-placement-intro.png "네 개의 팝업이 있는 이미지")    
  
 이 간단한 예제에서는 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 및 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>을 설정 하는 방법을 보여 주지만, <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> <xref:System.Windows.Controls.Primitives.Popup> 및 <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> 속성을 사용 하면가 배치 되는 위치를 보다 세부적으로 제어할 수 있습니다.  
  
<a name="Definitions"></a>   
## <a name="definitions-of-terms-the-anatomy-of-a-popup"></a>용어 정의: 팝업의 분석  
 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>다음 용어는 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>,, ,<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> 및<xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> 속성이 서로<xref:System.Windows.Controls.Primitives.Popup>어떻게 관련 되어 있는지 이해 하는 데 유용 합니다. <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>  
  
- 대상 개체  
  
- 대상 영역  
  
- 대상 원점  
  
- Popup 맞춤 지점  
  
 이러한 용어는 <xref:System.Windows.Controls.Primitives.Popup> 와 연결 된 컨트롤의 다양 한 측면을 쉽게 참조할 수 있는 방법을 제공 합니다.  
  
### <a name="target-object"></a>대상 개체  
 *대상 개체* 는가 연결 된 요소 <xref:System.Windows.Controls.Primitives.Popup> 입니다. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 속성이 설정 된 경우 대상 개체를 지정 합니다.  가 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 설정 되지 않은 경우에 <xref:System.Windows.Controls.Primitives.Popup> 부모가 있으면 부모는 대상 개체입니다.  값이 없고 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 부모가 없는 경우 대상 개체가 <xref:System.Windows.Controls.Primitives.Popup> 없고가 화면을 기준으로 배치 됩니다.  
  
 다음 예제에서는 <xref:System.Windows.Controls.Canvas>의 자식인 <xref:System.Windows.Controls.Primitives.Popup> 을 만듭니다.  이 예제에서는의 속성 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> <xref:System.Windows.Controls.Primitives.Popup>을 설정 하지 않습니다. 의 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 기본값은입니다 <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom?displayProperty=nameWithType>. 따라서는 아래 <xref:System.Windows.Controls.Primitives.Popup> 에 나타납니다. <xref:System.Windows.Controls.Canvas>  
  
 [!code-xaml[PopupPositionSnippet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#1)]  
  
 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup> 가에 상대적 <xref:System.Windows.Controls.Canvas>으로 배치 되어 있음을 보여 줍니다.  
  
 배치 ![대상 없는 Popup 컨트롤](./media/popup-placement-behavior/popup-placement-no-placement-target.png "대상에 없는 Popup입니다.")  

 다음 예제에서는 <xref:System.Windows.Controls.Canvas>의 자식인 <xref:System.Windows.Controls.Primitives.Popup> 를 만들지만 이번에는 <xref:System.Windows.Shapes.Ellipse>로 `ellipse1`설정 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 되어 있으므로 팝업이 아래에 나타납니다.  
  
 [!code-xaml[PopupPositionSnippet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#2)]  
  
 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup> 가에 상대적 <xref:System.Windows.Shapes.Ellipse>으로 배치 되어 있음을 보여 줍니다.  
  
 ![타원을 기준으로 위치가 지정 된 Popup] 배치 (./media/popup-placement-behavior/popup-placement-with-placement-target.png "를 대상으로 하는 Popup")    
  
> [!NOTE]
> 의 경우의 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>기본값 은입니다. <xref:System.Windows.Controls.Primitives.PlacementMode.Mouse> <xref:System.Windows.Controls.ToolTip>  의 경우의 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>기본값 은입니다. <xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint> <xref:System.Windows.Controls.ContextMenu> 이러한 값은 나중에 "속성을 함께 사용하는 방법"에서 설명합니다.  
  
### <a name="target-area"></a>대상 영역  
 *대상 영역은* 화면 <xref:System.Windows.Controls.Primitives.Popup> 에서가 기준으로 하는 영역입니다. 앞의 예제에서는 <xref:System.Windows.Controls.Primitives.Popup> 대상 개체의 경계를 기준으로 정렬 되지만 일부 경우 <xref:System.Windows.Controls.Primitives.Popup> 에는가 대상 개체를 <xref:System.Windows.Controls.Primitives.Popup> 포함 하는 경우에도 다른 범위에 정렬 됩니다.  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 속성이 설정 된 경우 대상 영역이 대상 개체의 범위와 다릅니다.  
  
 다음 예제에서는 각각 <xref:System.Windows.Controls.Canvas> <xref:System.Windows.Shapes.Rectangle> 및를 <xref:System.Windows.Controls.Primitives.Popup>포함 하는 두 개의 개체를 만듭니다.  두 경우 모두의 대상 개체 <xref:System.Windows.Controls.Primitives.Popup> <xref:System.Windows.Controls.Canvas>는입니다. <xref:System.Windows.Rect.X%2A> <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 첫번째<xref:System.Windows.Rect.Y%2A>에는, ,및<xref:System.Windows.Rect.Height%2A> 속성이 각각 50, 50, 50 및 100로 설정 된 집합이 있습니다. <xref:System.Windows.Rect.Width%2A> <xref:System.Windows.Controls.Canvas> <xref:System.Windows.Controls.Primitives.Popup> 두 번째 <xref:System.Windows.Controls.Canvas> 의에는이 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 설정 되어 있지 않습니다. <xref:System.Windows.Controls.Primitives.Popup>  결과적으로 첫 <xref:System.Windows.Controls.Primitives.Popup> 번째는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 아래에 배치 되 고 <xref:System.Windows.Controls.Canvas>두 번째 <xref:System.Windows.Controls.Primitives.Popup> 는 아래에 배치 됩니다. 각 <xref:System.Windows.Controls.Canvas> 에는 첫 <xref:System.Windows.Shapes.Rectangle> <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 번째<xref:System.Windows.Controls.Primitives.Popup>의와 동일한 범위를 갖는도 포함 됩니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 응용 프로그램에 표시 되는 요소를 만들지 않습니다 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>.이 예제에서는을 나타내는 <xref:System.Windows.Shapes.Rectangle> 을 만듭니다.  
  
 [!code-xaml[PopupPositionSnippet#4](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#4)]  
  
 다음 그림에서는 이전 예제의 결과를 보여 줍니다.  
  
 ![키가 없는 사각형의 Popup](./media/popup-placement-behavior/popup-placement-placement-rectangle.png "키가 없는 사각형의 Popup입니다.")  

### <a name="target-origin-and-popup-alignment-point"></a>대상 원점 및 Popup 맞춤 지점  
 *대상 원점* 및 *Popup 맞춤 지점*은 각각 대상 영역 및 Popup에서 위치 지정에 사용되는 참조 지점입니다. <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> 및<xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> 속성을 사용 하 여 대상 영역에서 popup을 오프셋할 수 있습니다.  <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> 및<xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> 는 대상 원점과 popup 맞춤 지점을 기준으로 합니다. <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성의 값은 대상 원점 및 popup 맞춤 지점이 있는 위치를 결정 합니다.  
  
 다음 예제에서는 <xref:System.Windows.Controls.Primitives.Popup> 가져오거나 설정 합니다 <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> 및 <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> 20 속성.  속성이 (기본값)로 <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom> 설정 되어 있으므로 대상 원점이 대상 영역의 왼쪽 아래 모퉁이가 고 팝업 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 위 모퉁이입니다. <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>  
  
 [!code-xaml[PopupPositionSnippet#5](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#5)]  
  
 다음 그림에서는 이전 예제의 결과를 보여 줍니다.  
  
 ![대상 원점 맞춤 지점을 사용한 Popup 배치](./media/popup-placement-behavior/popup-placement-target-origin-alignment-point.png "System.windows.controls.primitives.iscrollinfo.horizontaloffset 및 VerticalOffset를 사용 하는 Popup.")    
  
<a name="How"></a>   
## <a name="how-the-properties-work-together"></a>속성을 함께 사용하는 방법  
 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> ,<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>및 값<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 은 올바른 대상 영역, 대상 원점 및 팝업 맞춤 지점을 파악 하기 위해 함께 고려해 야 합니다.  예를 들어의 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 값이 <xref:System.Windows.Controls.Primitives.PlacementMode.Mouse>이면 대상 개체가 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 없고이 무시 되며 대상 영역이 마우스 포인터의 범위입니다. <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 반면,가 인 <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom>경우 또는 부모는 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 대상 개체를 결정 하 고 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 영역을 결정 합니다.  
  
 다음 표에서는 대상 개체, 대상 영역, 대상 원점 및 팝업 맞춤 지점에 대해 설명 하 고 각 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> <xref:System.Windows.Controls.Primitives.PlacementMode> 열거형 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 값에 및이 사용 되는지 여부를 나타냅니다.  
  
|PlacementMode|대상 개체|대상 영역|대상 원점|Popup 맞춤 지점|  
|-------------------|-------------------|-----------------|-------------------|---------------------------|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Absolute>|해당 사항 없음. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 무시 됩니다.|화면 또는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> (설정 된 경우)입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 화면을 기준으로 합니다.|대상 영역의 왼쪽 위 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.AbsolutePoint>|해당 사항 없음. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 무시 됩니다.|화면 또는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> (설정 된 경우)입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 화면을 기준으로 합니다.|대상 영역의 왼쪽 위 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Bottom>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|대상 영역의 왼쪽 아래 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Center>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|대상 영역의 가운데.|의 <xref:System.Windows.Controls.Primitives.Popup>중심입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Custom>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|에 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>의해 정의 됩니다.|에 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>의해 정의 됩니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Left>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|대상 영역의 왼쪽 위 모퉁이.|의 오른쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Mouse>|해당 사항 없음. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 무시 됩니다.|마우스 포인터의 경계. <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 무시 됩니다.|대상 영역의 왼쪽 아래 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint>|해당 사항 없음. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> 무시 됩니다.|마우스 포인터의 경계. <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 무시 됩니다.|대상 영역의 왼쪽 위 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Relative>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|대상 영역의 왼쪽 위 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.RelativePoint>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|대상 영역의 왼쪽 위 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Right>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|대상 영역의 오른쪽 위 모퉁이.|의 왼쪽 위 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Top>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>또는 부모입니다.|대상 개체 이거나 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> , 설정 된 경우입니다.  는 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> 대상 개체를 기준으로 합니다.|대상 영역의 왼쪽 위 모퉁이.|의 왼쪽 아래 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>입니다.|  
  
 다음 그림에서는 각 <xref:System.Windows.Controls.Primitives.Popup> <xref:System.Windows.Controls.Primitives.PlacementMode> 값에 대 한, 대상 영역, 대상 원점 및 팝업 맞춤 지점을 보여 줍니다. 각 그림에서 대상 영역은 노란색이 고는 <xref:System.Windows.Controls.Primitives.Popup> 파란색입니다.  
  
 ![Absolute 또는 AbsolutePoint 배치를 사용 하는 Popup](./media/popup-placement-behavior/popup-placement-absolute.png "배치가 Absolute 또는 AbsolutePoint입니다.")    
  
 ![아래쪽 배치의 팝업](./media/popup-placement-behavior/popup-placement-bottom.png "배치가 아래쪽입니다.")   
  
 ![가운데 배치의 팝업](./media/popup-placement-behavior/popup-placement-center.png "배치가 가운데 맞춤입니다.")    
  
 ![왼쪽 배치가 있는 Popup](./media/popup-placement-behavior/popup-placement-left.png "배치가 왼쪽입니다.")   
  
 ![마우스 배치의 팝업](./media/popup-placement-behavior/popup-placement-mouse.png "배치가 마우스입니다.")  
  
 ![MousePoint 배치의 Popup](./media/popup-placement-behavior/popup-placement-mousepoint.png "배치가 MousePoint입니다.")  
  
 ![상대 또는 RelativePoint 배치를 사용 하는 Popup](./media/popup-placement-behavior/popup-placement-relative.png "배치가 상대 또는 RelativePoint입니다.")    
  
 ![오른쪽 배치가 있는 Popup](./media/popup-placement-behavior/popup-placement-right.png "배치가 적합 합니다.")    
  
 ![Top 배치의 Popup](./media/popup-placement-behavior/popup-placement-top.png "배치가 위쪽입니다.")    
  
<a name="When"></a>   
## <a name="when-the-popup-encounters-the-edge-of-the-screen"></a>Popup이 화면 가장자리와 만나는 경우  
 보안상의 이유로는 <xref:System.Windows.Controls.Primitives.Popup> 화면의 가장자리에 의해 숨겨질 수 없습니다. 에서 <xref:System.Windows.Controls.Primitives.Popup> 화면 가장자리가 나타날 때 다음 세 가지 작업 중 하나가 발생 합니다.  
  
- 팝업은를 <xref:System.Windows.Controls.Primitives.Popup>realigns 화면 가장자리를 따라 자신에 게 있습니다.  
  
- Popup에 다른 Popup 맞춤 지점이 사용됩니다.  
  
- Popup에 다른 대상 원점 및 Popup 맞춤 지점이 사용됩니다.  
  
 이러한 옵션은 이 섹션의 뒷부분에서 설명합니다.  
  
 화면 가장자리가 나타날 <xref:System.Windows.Controls.Primitives.Popup> 때의 동작은 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성의 값과 popup이 발생 하는 화면 가장자리에 따라 다릅니다. 다음 표에는에서 <xref:System.Windows.Controls.Primitives.Popup> 각 <xref:System.Windows.Controls.Primitives.PlacementMode> 값에 대 한 화면 가장자리가 나타날 때의 동작이 요약 되어 있습니다.  
  
|PlacementMode|위쪽 가장자리|아래쪽 가장자리|왼쪽 가장자리|오른쪽 가장자리|  
|-------------------|--------------|-----------------|---------------|----------------|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Absolute>|위쪽 가장자리에 맞춥니다.|아래쪽 가장자리에 맞춥니다.|왼쪽 가장자리에 맞춥니다.|오른쪽 가장자리에 맞춥니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.AbsolutePoint>|위쪽 가장자리에 맞춥니다.|Popup 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 아래 모퉁이로 변경 됩니다.|왼쪽 가장자리에 맞춥니다.|Popup 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>오른쪽 위 모퉁이로 변경 됩니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Bottom>|위쪽 가장자리에 맞춥니다.|대상 원점이 대상 영역의 왼쪽 위 모퉁이로 변경 되 고 popup 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 아래 모퉁이로 변경 됩니다.|왼쪽 가장자리에 맞춥니다.|오른쪽 가장자리에 맞춥니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Center>|위쪽 가장자리에 맞춥니다.|아래쪽 가장자리에 맞춥니다.|왼쪽 가장자리에 맞춥니다.|오른쪽 가장자리에 맞춥니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Left>|위쪽 가장자리에 맞춥니다.|아래쪽 가장자리에 맞춥니다.|대상 원점이 대상 영역의 오른쪽 위 모퉁이로 변경 되 고 popup 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 위 모퉁이로 변경 됩니다.|오른쪽 가장자리에 맞춥니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Mouse>|위쪽 가장자리에 맞춥니다.|대상 원점이 대상 영역의 왼쪽 위 모퉁이로 변경 되 고 (마우스 포인터의 경계) 팝업 맞춤 지점은의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 아래 모퉁이로 변경 됩니다.|왼쪽 가장자리에 맞춥니다.|오른쪽 가장자리에 맞춥니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint>|위쪽 가장자리에 맞춥니다.|Popup 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 아래 모퉁이로 변경 됩니다.|왼쪽 가장자리에 맞춥니다.|Popup 맞춤 지점이 Popup의 오른쪽 위 모퉁이로 변경됩니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Relative>|위쪽 가장자리에 맞춥니다.|아래쪽 가장자리에 맞춥니다.|왼쪽 가장자리에 맞춥니다.|오른쪽 가장자리에 맞춥니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.RelativePoint>|위쪽 가장자리에 맞춥니다.|Popup 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 아래 모퉁이로 변경 됩니다.|왼쪽 가장자리에 맞춥니다.|Popup 맞춤 지점이 Popup의 오른쪽 위 모퉁이로 변경됩니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Right>|위쪽 가장자리에 맞춥니다.|아래쪽 가장자리에 맞춥니다.|왼쪽 가장자리에 맞춥니다.|대상 원점이 대상 영역의 왼쪽 위 모퉁이로 변경 되 고 popup 맞춤 지점이의 <xref:System.Windows.Controls.Primitives.Popup>오른쪽 위 모퉁이로 변경 됩니다.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Top>|대상 원점이 대상 영역의 왼쪽 아래 모퉁이로 바뀌고 팝업 맞춤 지점은의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 위 모퉁이로 변경 됩니다. 실제로이는가 인 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom>경우와 동일 합니다.|아래쪽 가장자리에 맞춥니다.|왼쪽 가장자리에 맞춥니다.|오른쪽 가장자리에 맞춥니다.|  
  
### <a name="aligning-to-the-screen-edge"></a>화면 가장자리에 맞춤  
 는 <xref:System.Windows.Controls.Primitives.Popup> 전체<xref:System.Windows.Controls.Primitives.Popup> 를 화면에 표시 되도록 자체적으로 위치를 조정 하 여 화면 가장자리에 맞출 수 있습니다.  이 경우 대상 원점과 팝업 맞춤 지점 간의 거리가 및 <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A>의 값과 다를 수 있습니다. 가 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> ,또는<xref:System.Windows.Controls.Primitives.PlacementMode.Center>인 경우 는<xref:System.Windows.Controls.Primitives.Popup> 자체를 모든 화면 가장자리에 맞춥니다. <xref:System.Windows.Controls.Primitives.PlacementMode.Relative> <xref:System.Windows.Controls.Primitives.PlacementMode.Absolute>  예를 <xref:System.Windows.Controls.Primitives.Popup> 들어,가로 <xref:System.Windows.Controls.Primitives.PlacementMode.Relative> 설정 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 되 고 <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> 가 100로 설정 되어 있다고 가정 합니다.  화면의 아래쪽 가장자리가의 전체 또는 일부 <xref:System.Windows.Controls.Primitives.Popup>를 숨기면 화면 아래쪽 가장자리를 따라 위치를 조정 하 고 대상 원점과 팝업 맞춤 지점 간의 세로 거리를 100 미만으로 표시 합니다. <xref:System.Windows.Controls.Primitives.Popup> 다음 그림에서 이 경우를 보여 줍니다.  
  
 ![화면 가장자리에 맞추는 팝업](./media/popup-placement-behavior/popup-placement-relative-screen-edge.png "Popup이 화면의 가장자리에 맞춰집니다.")    
  
### <a name="changing-the-popup-alignment-point"></a>Popup 맞춤 지점 변경  
 가 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> , <xref:System.Windows.Controls.Primitives.PlacementMode.AbsolutePoint> 또는<xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint>이면팝업이 아래쪽 또는 오른쪽 화면 가장자리를 만나면 팝업 맞춤 지점이 변경 됩니다. <xref:System.Windows.Controls.Primitives.PlacementMode.RelativePoint>  
  
 다음 그림에서는 아래쪽 화면 가장자리가의 전체 또는 일부 <xref:System.Windows.Controls.Primitives.Popup>를 숨기는 경우 팝업 맞춤 지점이의 왼쪽 아래 모퉁이 <xref:System.Windows.Controls.Primitives.Popup>임을 보여 줍니다.  
  
 ![아래쪽 화면 가장자리로 인 한 새로운 맞춤 지점](./media/popup-placement-behavior/popup-placement-relative-point-screen-edge.png "Popup이 화면의 아래쪽 가장자리를 만나면 팝업 맞춤 지점을 변경 합니다.")  

 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup> 가 오른쪽 화면 가장자리에 의해 숨겨지는 경우 popup 맞춤 지점이 <xref:System.Windows.Controls.Primitives.Popup>의 오른쪽 위 모퉁이 임을 보여 줍니다.  
  
 ![화면 가장자리로 인 한 새 팝업 맞춤 지점](./media/popup-placement-behavior/popup-placement-relative-point-right-screen-edge.png "Popup이 화면의 오른쪽 가장자리를 만나면 popup 맞춤 지점을 변경 합니다.")    
  
 에서 <xref:System.Windows.Controls.Primitives.Popup> 아래쪽 및 오른쪽 화면 가장자리를 만나면 팝업 맞춤 지점이 <xref:System.Windows.Controls.Primitives.Popup>의 오른쪽 아래 모퉁이입니다.  
  
### <a name="changing-the-target-origin-and-popup-alignment-point"></a>대상 원점 및 Popup 맞춤 지점 변경  
 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 이<xref:System.Windows.Controls.Primitives.PlacementMode.Bottom> ,,<xref:System.Windows.Controls.Primitives.PlacementMode.Top>, 또는 인 경우 특정 화면 가장자리에 도달 하면 대상 원점 및 팝업 맞춤 지점이 변경 됩니다. <xref:System.Windows.Controls.Primitives.PlacementMode.Left> <xref:System.Windows.Controls.Primitives.PlacementMode.Mouse> <xref:System.Windows.Controls.Primitives.PlacementMode.Right>  위치가 변경 되도록 하는 화면 가장자리는 <xref:System.Windows.Controls.Primitives.PlacementMode> 값에 따라 달라 집니다.  
  
 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 가이 고 <xref:System.Windows.Controls.Primitives.Popup> 가 <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom> 아래쪽 화면 가장자리를 만나면 대상 원점이 대상 영역의 왼쪽 위 모퉁이가 고 popup 맞춤 지점이의 왼쪽 아래 모퉁이 임을 보여 줍니다. <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![아래쪽 화면 가장자리로 인 한 새로운 맞춤 지점](./media/popup-placement-behavior/popup-placement-bottom-screen-edge.png "배치가 아래쪽에 있고 popup이 화면의 아래쪽 가장자리에 도달 합니다.")    
  
 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 가이 고 <xref:System.Windows.Controls.Primitives.Popup> 가 <xref:System.Windows.Controls.Primitives.PlacementMode.Left> 왼쪽 화면 가장자리를 만나면 대상 원점이 대상 영역의 오른쪽 위 모퉁이가 고 popup 맞춤 지점이의 왼쪽위모퉁이임을보여줍니다 <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![왼쪽 화면 가장자리로 인 한 새로운 맞춤 지점](./media/popup-placement-behavior/popup-placement-left-screen-edge.png "배치가 왼쪽에 있고 popup이 화면 왼쪽 가장자리에 도달 합니다.")  
  
 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 가이 고 <xref:System.Windows.Controls.Primitives.Popup> 가 <xref:System.Windows.Controls.Primitives.PlacementMode.Right> 오른쪽 화면 가장자리를 만나면 대상 원점이 대상 영역의 왼쪽 위 모퉁이가 고 popup 맞춤 지점이의 오른쪽 위 모퉁이 임을 보여 줍니다. <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![오른쪽 화면 가장자리로 인 한 새로운 맞춤 지점](./media/popup-placement-behavior/popup-placement-right-screen-edge.png "배치가 오른쪽에 있고 popup이 화면의 오른쪽 가장자리와 만나는") 경우  

 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 가이 고 <xref:System.Windows.Controls.Primitives.Popup> 가 <xref:System.Windows.Controls.Primitives.PlacementMode.Top> 위쪽 화면 가장자리를 만나면 대상 원점이 대상 영역의 왼쪽 아래 모퉁이가 고 popup 맞춤 지점이의 왼쪽 위 모퉁이 임을 보여 줍니다. <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![위쪽 화면 가장자리로 인 한 새로운 맞춤 지점](./media/popup-placement-behavior/popup-placement-top-screen-edge.png "배치가 위쪽이 고 popup이 화면의 위쪽 가장자리를 발견 합니다.")  
  
 다음 그림에서는 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 가이 고 <xref:System.Windows.Controls.Primitives.Popup> 가 <xref:System.Windows.Controls.Primitives.PlacementMode.Mouse> 아래쪽 화면 가장자리를 만나면 대상 원점이 대상 영역의 왼쪽 위 모퉁이 (마우스 포인터의 경계)와 popup 맞춤 임을 보여 줍니다. point는의 <xref:System.Windows.Controls.Primitives.Popup>왼쪽 아래 모퉁이입니다.  
  
 ![화면 가장자리 근처의 마우스로 인 한 새 맞춤 지점](./media/popup-placement-behavior/popup-placement-mouse-screen-edge.png "배치는 마우스이 고 popup은 화면의 아래쪽 가장자리가 발견 됩니다.")    
  
### <a name="customizing-popup-placement"></a>Popup 배치 사용자 지정  
 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성을로 <xref:System.Windows.Controls.Primitives.PlacementMode.Custom>설정 하 여 대상 원점 및 popup 맞춤 지점을 사용자 지정할 수 있습니다. 그런 다음 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> <xref:System.Windows.Controls.Primitives.Popup>에 대 한 가능한 배치 지점과 기본 축 (기본 설정 순서 대로) 집합을 반환 하는 대리자를 정의 합니다. 의 가장 큰 부분을 표시 하는 점이 <xref:System.Windows.Controls.Primitives.Popup> 선택 됩니다.  가 화면 가장자리에 <xref:System.Windows.Controls.Primitives.Popup> 의해 숨겨지면의 위치가 자동으로 조정 됩니다. <xref:System.Windows.Controls.Primitives.Popup> 예제를 보려면 [사용자 지정 팝업 위치 지정](how-to-specify-a-custom-popup-position.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [Popup Placement Sample](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS)(Popup 배치 샘플)
