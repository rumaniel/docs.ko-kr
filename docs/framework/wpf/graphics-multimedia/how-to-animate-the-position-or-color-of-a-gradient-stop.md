---
title: '방법: 그라데이션 중지점의 위치 또는 색에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- position [WPF], animating
- animation [WPF], position of GradientStop objects
- GradientStop objects [WPF], animating color of
- colors [WPF], animating
- animation [WPF], color of GradientStop objects
- GradientStop objects [WPF], animating position of
ms.assetid: 6f5b8b47-6c32-4b8e-98ee-fdf6515ec843
ms.openlocfilehash: 4762233cace895c9d492fb426f3f6be14498ad53
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593352"
---
# <a name="how-to-animate-the-position-or-color-of-a-gradient-stop"></a>방법: 그라데이션 중지점의 위치 또는 색에 애니메이션 효과 주기
애니메이션을 적용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.GradientStop.Color%2A> 하 고 <xref:System.Windows.Media.GradientStop.Offset%2A> 의 <xref:System.Windows.Media.GradientStop> 개체입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 세 그라데이션 내에서 애니메이션을 <xref:System.Windows.Media.LinearGradientBrush>입니다. 이 예제에서는 다양 한 그라데이션 중지점에 애니메이션을 적용 하는 각 세 가지 애니메이션을 사용 합니다.  
  
- 첫 번째 애니메이션을 <xref:System.Windows.Media.Animation.DoubleAnimation>, 첫 번째 그라데이션 중지점의 애니메이션 <xref:System.Windows.Media.GradientStop.Offset%2A> 0.0에서 1.0의 0.0으로 다시 합니다. 결과적으로, 첫 번째 사각형의 왼쪽에서 오른쪽으로 왼쪽에서 그라데이션 만큼의 색을 왼쪽으로 다시 합니다.  
  
- 두 번째 애니메이션을 <xref:System.Windows.Media.Animation.ColorAnimation>, 두 번째 그라데이션 중지점의 애니메이션 효과 줍니다 <xref:System.Windows.Media.GradientStop.Color%2A> 에서 <xref:System.Windows.Media.Colors.Purple%2A> 에 <xref:System.Windows.Media.Colors.Yellow%2A> 다시 <xref:System.Windows.Media.Colors.Purple%2A>입니다. 결과적으로, 노란색, 보라색으로 다시로 자주색에서 그라데이션의 중간 색을 변경합니다.  
  
- 세 번째 애니메이션 다른 <xref:System.Windows.Media.Animation.ColorAnimation>, 세 번째 그라데이션 중지점의 불투명도 애니메이션을 적용 <xref:System.Windows.Media.GradientStop.Color%2A> -1로 다시 합니다. 결과적으로, 세 번째 그라데이션 색 희미해 및 다시 불투명해 집니다.  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/GradientStopAnimationExample.cs#graphicsmmgradientanimationexampleswholepage)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/gradientstopanimationexample.vb#graphicsmmgradientanimationexampleswholepage)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/GradientStopAnimationExample.xaml#graphicsmmgradientanimationexampleswholepage)]  
  
 이 예제에서는 <xref:System.Windows.Media.LinearGradientBrush>, 프로세스에 애니메이션 효과를 동일 <xref:System.Windows.Media.GradientStop> 내에서 개체를 <xref:System.Windows.Media.RadialGradientBrush>입니다.  
  
 추가 예제를 보려면 합니다 [브러시 샘플](https://go.microsoft.com/fwlink/?LinkID=159973)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.GradientStop>
- [애니메이션 개요](animation-overview.md)
- [Storyboard 개요](storyboards-overview.md)
