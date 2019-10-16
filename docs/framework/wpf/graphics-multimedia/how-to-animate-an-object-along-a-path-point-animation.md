---
title: '방법: 경로를 따라 개체에 애니메이션 효과 주기(Point 애니메이션)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], objects along paths (point animation)
- point animation [WPF]
ms.assetid: 1fa3f817-35bc-41a1-b366-f5a20b70da0c
ms.openlocfilehash: 4ef28118975d02500916676ca50e0f9622c7a3e2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651456"
---
# <a name="how-to-animate-an-object-along-a-path-point-animation"></a>방법: 경로를 따라 개체에 애니메이션 효과 주기(Point 애니메이션)
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.PointAnimationUsingPath> 애니메이션을 적용할 개체는 <xref:System.Windows.Point> 곡선된 경로 따라 합니다.  
  
## <a name="example"></a>예제  
 이동 하는 다음 예제는 <xref:System.Windows.Media.EllipseGeometry> 정의한 경로 따라는 <xref:System.Windows.Media.PathGeometry>합니다. 타원 기 하 도형의 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 사용 하는 속성을 <xref:System.Windows.Point> 값에 애니메이션 효과 적용 하면 타원 기 하, 이동 하려면 해당 위치를 지정 하 고, 해당 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 속성입니다. 이 예제에서는 사용을 <xref:System.Windows.Media.Animation.PointAnimationUsingPath> 애니메이션 효과를 주는 <xref:System.Windows.Media.EllipseGeometry> 개체의 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 속성입니다.  
  
 [!code-xaml[PathAnimationGallery_snippet#PointAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/pointanimationusingpathexample.xaml#pointanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/PointAnimationUsingPathExample.cs#pointanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/PointAnimationUsingPathExample.vb#pointanimationusingpathwholepage)]  
  
 전체 샘플을 참조 하세요 [경로 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160028)합니다.  
  
 사용 하는 이전 샘플의 코드 버전을 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션 효과를 주는 <xref:System.Windows.Media.EllipseGeometry>하나만 애니메이션이 적용 된 경우에 합니다. A <xref:System.Windows.Media.Animation.Storyboard> 동일한 이러한 애니메이션을 제어할 수 있으므로 여러 애니메이션을 적용 하는 가장 쉬운 방법은 경우가 <xref:System.Windows.Media.Animation.Storyboard>합니다. 그러나 코드를 사용 하는 경우 속성에 단일 애니메이션을 적용 하는 간단한 방법인 사용 하는 것은 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 메서드. 예제를 보려면 [Storyboard를 사용하지 않고 속성에 애니메이션 효과 주기](how-to-animate-a-property-without-using-a-storyboard.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [경로 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160028)
- [애니메이션 개요](animation-overview.md)
- [경로 애니메이션 방법 항목](path-animation-how-to-topics.md)
