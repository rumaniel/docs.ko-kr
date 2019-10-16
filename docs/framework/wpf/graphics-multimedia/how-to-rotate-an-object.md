---
title: '방법: 개체 회전'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rotating objects [WPF]
- rotating objects [WPF]
ms.assetid: ee3466cd-e66f-4e8f-8a5a-71d77bc1e390
ms.openlocfilehash: d1c4700a5dc8f6ed99043552999d8f014116da8f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61804166"
---
# <a name="how-to-rotate-an-object"></a>방법: 개체 회전
이 예제에서는 개체를 회전하는 방법을 보여 줍니다. 이 예에서는 먼저 만듭니다는 <xref:System.Windows.Media.RotateTransform> 만든 다음 해당 <xref:System.Windows.Media.RotateTransform.Angle%2A> 각도 (도).  
  
 다음 예제에서는 회전 된 <xref:System.Windows.Shapes.Polyline> 45도 왼쪽 위 구석에 해당 하는 방법에 대 한 개체입니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[Transforms_snip#RotatePolylineAboutTopLeft](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineabouttopleft)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineabouttopleft)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineabouttopleft)]  
  
 합니다 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 및 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 의 속성을 <xref:System.Windows.Media.RotateTransform> 개체가 회전 되는 지점을 지정 합니다. 이 중심점은 변환되는 요소의 좌표 공간으로 표현됩니다. 기본적으로 회전은 변환할 개체의 왼쪽 위 구석에 해당하는 (0,0)에 적용됩니다.  
  
 다음 예제에서는 회전을 <xref:System.Windows.Shapes.Polyline> 시계 방향으로 45도 점 (25, 50)에 대 한 개체입니다.  
  
 [!code-xaml[Transforms_snip#RotatePolylineAboutCenter](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineaboutcenter)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutCenter](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineaboutcenter)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutCenter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineaboutcenter)]  
  
 다음 그림과 적용 한 결과 <xref:System.Windows.Media.Transform> 두 개체에 있습니다.  
  
 ![여러 중심점을 사용한 45도 회전](./media/wcpsdk-graphicsmm-rotatetransform45degrees.gif "wcpsdk_graphicsmm_rotatetransform45degrees")  
서로 다른 회전 중심에서 45도로 회전하는 두 개체  
  
 합니다 <xref:System.Windows.Shapes.Polyline> 이전 예제는 <xref:System.Windows.UIElement>합니다. 적용 하는 경우를 <xref:System.Windows.Media.Transform> 에 <xref:System.Windows.UIElement.RenderTransform%2A> 의 속성을 <xref:System.Windows.UIElement>, 사용할 수 있습니다를 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 의 원본을 지정 하는 속성 모든 <xref:System.Windows.Media.Transform> 요소에 적용 되는. 때문에 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 상대 좌표를 사용 하는 속성, 해당 크기를 모르는 경우에 요소의 가운데에는 변환을 적용할 수 있습니다. 자세한 내용 및 예제를 참조 하세요 [상대 값 사용 하 여 변환 원점 지정](how-to-specify-the-origin-of-a-transform-by-using-relative-values.md)합니다.  
  
 전체 샘플을 보려면 [2차원 변환 샘플](https://go.microsoft.com/fwlink/?LinkID=158252)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Transform>
- [Transform 개요](transforms-overview.md)
- [방법 항목](transformations-how-to-topics.md)
