---
title: '방법: BorderThickness 값에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- border thickness [WPF], animating changes to
- animation [WPF], changes to border thickness
ms.assetid: fd021978-f74b-4e7b-a7f7-3987dcad9e0f
ms.openlocfilehash: 10e177d1f6d6add4638ce14af900e75d7e363890
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911247"
---
# <a name="how-to-animate-a-borderthickness-value"></a>방법: BorderThickness 값에 애니메이션 효과 주기
사용 하 여 테두리의 두께에 대 한 변경을 애니메이션화 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.ThicknessAnimation> 클래스입니다.  
  
## <a name="example"></a>예제  
 다음 예제를 사용 하 여 테두리의 두께 애니메이션을 적용 <xref:System.Windows.Media.Animation.ThicknessAnimation>합니다. 이 예제에서는 사용 합니다 <xref:System.Windows.Controls.Border.BorderThickness%2A> 속성의 <xref:System.Windows.Controls.Border>합니다.  
  
 [!code-csharp[BasicAnimations_snip#ThicknessAnimationWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/ThicknessAnimationExample.cs#thicknessanimationwholepage)]
 [!code-vb[BasicAnimations_snip#ThicknessAnimationWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/ThicknessAnimationExample.vb#thicknessanimationwholepage)]  
  
 전체 샘플을 참조 하세요 [애니메이션 예제 갤러리](https://go.microsoft.com/fwlink/?LinkID=159969)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.ThicknessAnimation>
- <xref:System.Windows.Controls.Border.BorderThickness%2A>
- <xref:System.Windows.Controls.Border>
- [애니메이션 개요](../graphics-multimedia/animation-overview.md)
- [애니메이션 및 타이밍 방법 항목](../graphics-multimedia/animation-and-timing-how-to-topics.md)
- [키 프레임을 사용하여 테두리 두께에 애니메이션 효과 주기](../graphics-multimedia/how-to-animate-the-thickness-of-a-border-by-using-key-frames.md)
