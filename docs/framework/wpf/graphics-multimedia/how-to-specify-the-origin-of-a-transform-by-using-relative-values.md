---
title: '방법: 상대 값을 사용하여 변환 원점 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- origins of Transforms [WPF]
- Transforms [WPF], origins of
- graphics [WPF], origins of Transforms
ms.assetid: f4dbc29d-93c7-41cd-96d8-5cfd8624b470
ms.openlocfilehash: 48b3b0df8dab8516873495a996074eae57ffe00f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651144"
---
# <a name="how-to-specify-the-origin-of-a-transform-by-using-relative-values"></a>방법: 상대 값을 사용하여 변환 원점 지정
이 예제에서는 상대 값의 출처를 지정 하는 데는 <xref:System.Windows.UIElement.RenderTransform%2A> 에 적용 되는 한 <xref:System.Windows.FrameworkElement>합니다.  
  
 회전, 크기 조정 또는 기울일 때를 <xref:System.Windows.FrameworkElement> 를 사용 하 여는 <xref:System.Windows.UIElement.RenderTransform%2A> 요소의 왼쪽 위 모퉁이에 변환을 적용 하는 속성을 기본 설정 합니다. 요소 중심에서 회전, 크기 조정 또는 기울이기를 수행하려면 변환의 중심을 요소의 중심으로 설정하여 보완할 수 있습니다. 그러나 해당 솔루션에서는 요소의 크기를 알고 있어야 합니다. 요소 중심에 변환을 적용 하는 보다 손쉬운 방법을 설정 하는 것의 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 속성을 (0.5, 0.5) 변환 자체에 대해 중심 값을 설정 하는 대신 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 <xref:System.Windows.Media.RotateTransform> 회전 하는 <xref:System.Windows.Controls.Button> 시계 방향으로 45도 합니다. 이 예제에서는 중심을 지정하지 않으므로 단추는 왼쪽 위 구석에 해당하는 점 (0,0)에 대해 회전합니다. 합니다 <xref:System.Windows.Media.RotateTransform> 에 적용 되는 <xref:System.Windows.UIElement.RenderTransform%2A> 속성입니다.  
  
 다음 그림에서는 이어지는 예제의 변환 결과를 보여 줍니다.  
  
 ![RenderTransform을 사용 하 여 변형 된 단추](./media/graphicsmm-rendertransformwithdefaultcenter.png "graphicsmm_RenderTransformWithDefaultCenter")  
RenderTransform 속성을 사용한 45도 시계 방향 회전  
  
 [!code-xaml[Transforms_snip#GraphicsMMRotateButtonExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample1)]  
  
 다음 예제에서는 또한 사용 하 여는 <xref:System.Windows.Media.RotateTransform> 회전 하는 <xref:System.Windows.Controls.Button> 45도 시계 방향으로, 단,이 예제에서는 설정는 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 단추 (0.5, 0.5). 결과적으로, 회전은 왼쪽 위 구석 대신 단추의 중심에 적용됩니다.  
  
 다음 그림에서는 이어지는 예제의 변환 결과를 보여 줍니다.  
  
 ![가운데를 중심으로 변형 된 단추](./media/graphicsmm-rendertransformrelativecenter.png "graphicsmm_RenderTransformRelativeCenter")  
RenderTransformOrigin (0.5, 0.5)의 RenderTransform 속성을 사용하여 45도 회전  
  
 [!code-xaml[Transforms_snip#GraphicsMMRotateButtonExample2](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample2)]  
  
 변환 하는 방법에 대 한 자세한 내용은 <xref:System.Windows.FrameworkElement> 개체를 참조 합니다 [변환 개요](transforms-overview.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Transform>
- [Transform 개요](transforms-overview.md)
- [방법 항목](transformations-how-to-topics.md)
