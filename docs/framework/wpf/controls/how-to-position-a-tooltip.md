---
title: '방법: 도구 설명 배치'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolTip control [WPF], positioning
- positioning ToolTip controls [WPF]
ms.assetid: cddf3757-9e5f-4ce3-a6eb-44489cf3804a
ms.openlocfilehash: 811818fe6e7c0d8ce9e2aa058b42bf592ada4b92
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770930"
---
# <a name="how-to-position-a-tooltip"></a>방법: 도구 설명 배치
이 예제에는 화면의 도구 설명의 위치를 지정 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 둘 다에 정의 된 5 가지 속성 집합을 사용 하 여 도구 설명을 배치할 수 있습니다 합니다 <xref:System.Windows.Controls.ToolTip> 및 <xref:System.Windows.Controls.ToolTipService> 클래스입니다. 다음 표에서 이러한 두 속성을 5 개를 표시 하 고 클래스에 따라 해당 참조 설명서에 대 한 링크를 제공 합니다.  
  
### <a name="corresponding-tooltip-properties-according-to-class"></a>클래스에 따라 해당 도구 설명 속성  
  
|<xref:System.Windows.Controls.ToolTip?displayProperty=nameWithType> 클래스 속성|<xref:System.Windows.Controls.ToolTipService?displayProperty=nameWithType> 클래스 속성|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.ToolTip.Placement%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.Placement%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementTarget%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementTarget%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementRectangle%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementRectangle%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.HorizontalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.HorizontalOffset%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.VerticalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.VerticalOffset%2A?displayProperty=nameWithType>|  
  
 사용 하 여 도구 설명의 내용을 정의 하는 경우는 <xref:System.Windows.Controls.ToolTip> 개체 클래스의 속성을 사용할 수 있지만 <xref:System.Windows.Controls.ToolTipService> 속성 보다 우선적으로 적용 합니다. 사용 된 <xref:System.Windows.Controls.ToolTipService> 속성으로 정의 되어 있지 않은 도구 설명에 <xref:System.Windows.Controls.ToolTip> 개체입니다.  
  
 다음 그림은 이러한 속성을 사용 하 여 도구 설명을 배치 하는 방법을 보여 줍니다. 하지만, [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 이러한 그림과 예제에 정의 된 속성을 설정 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.ToolTip> 클래스의 해당 속성을 <xref:System.Windows.Controls.ToolTipService> 클래스 동일한 레이아웃 규칙에 따라 합니다. 배치 속성에 대 한 가능한 값에 대 한 자세한 내용은 참조 하세요. [Popup 배치 동작](popup-placement-behavior.md)합니다.  
 
 다음 이미지는 배치 속성을 사용 하 여 tooltip 배치를 보여줍니다.  
  
 ![배치 속성을 사용 하 여 ToolTip 배치를 보여 주는 다이어그램입니다.](./media/how-to-position-a-tooltip/tooltip-placement-property.png)
 
 다음 이미지는 배치 및 PlacementRectangle 속성을 사용 하 여 tooltip 배치를 보여줍니다.   

 ![PlacementRectangle 속성을 사용 하 여 ToolTip 배치를 보여 주는 다이어그램입니다.](./media/how-to-position-a-tooltip/tooltip-placement-rectangle-property.png)  
 
 다음 이미지는 배치, PlacementRectangle, 및 오프셋 속성을 사용 하 여 tooltip 배치를 보여줍니다.   
  
 ![오프셋 속성을 사용 하 여 ToolTip 배치를 보여 주는 다이어그램입니다.](./media/how-to-position-a-tooltip/tooltip-placement-offset-property.png)

 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.ToolTip> 내용이 도구 설명의 위치를 지정 하는 속성을 <xref:System.Windows.Controls.ToolTip> 개체입니다.  
  
 [!code-xaml[ToolTipService#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
 [!code-csharp[ToolTipService#ToolTipCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#tooltipcode)]
 [!code-vb[ToolTipService#ToolTipCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#tooltipcode)]  
  
 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.ToolTipService> 내용이 아닙니다. 도구 설명의 위치를 지정 하는 속성을 <xref:System.Windows.Controls.ToolTip> 개체입니다.  
  
 [!code-xaml[ToolTipService#NoToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
 [!code-csharp[ToolTipService#NoToolTipCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#notooltipcode)]
 [!code-vb[ToolTipService#NoToolTipCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#notooltipcode)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipService>
- [방법 항목](tooltip-how-to-topics.md)
- [도구 설명 개요](tooltip-overview.md)
