---
title: '방법: 사각형에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], rectangles
- rectangles [WPF], animating
ms.assetid: 572ffb95-790d-4ace-adbf-b2ea8a90e75b
ms.openlocfilehash: 7f7cf24f7883553329de3761ff0670e8e3a09463
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61760911"
---
# <a name="how-to-animate-a-rectangle"></a>방법: 사각형에 애니메이션 효과 주기
이 예제에서는 사각형의 위치 및 크기 변화에 애니메이션 효과를 주는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 인스턴스를 사용 하 여 다음 예제에서는 <xref:System.Windows.Media.Animation.RectAnimation> 클래스에 애니메이션 효과를 <xref:System.Windows.Media.RectangleGeometry.Rect%2A> 의 속성은 <xref:System.Windows.Media.RectangleGeometry>, 크기 및 사각형의 위치 변경 애니메이션 효과 적용 합니다.  
  
 [!code-csharp[BasicAnimations_snip#RectAnimationWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/RectAnimationExample.cs#rectanimationwholepage)]
 [!code-vb[BasicAnimations_snip#RectAnimationWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/RectAnimationExample.vb#rectanimationwholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.RectAnimation>
- <xref:System.Windows.Media.RectangleGeometry.Rect%2A>
- <xref:System.Windows.Media.RectangleGeometry>
- [애니메이션 개요](animation-overview.md)
- [그래픽 및 멀티미디어](index.md)
- [그래픽 방법 항목](graphics-how-to-topics.md)
- [애니메이션 및 타이밍 방법 항목](animation-and-timing-how-to-topics.md)
