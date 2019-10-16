---
title: '방법: SolidColorBrush의 색 또는 불투명도에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- SolidColorBrush [WPF], animating color of
- colors [WPF], animating
- opacity [WPF], animating
- animation [WPF], color of SolidColorBrush
- animation [WPF], opacity of SolidColorBrush
- SolidColorBrush [WPF], animating opacity of
ms.assetid: d9154354-843f-4713-bad1-35bb0ba6eaeb
ms.openlocfilehash: 610a7c4879b4ffe54940e8bc744dcca0711e84d2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593393"
---
# <a name="how-to-animate-the-color-or-opacity-of-a-solidcolorbrush"></a>방법: SolidColorBrush의 색 또는 불투명도에 애니메이션 효과 주기
애니메이션을 적용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 하 고 <xref:System.Windows.Media.Brush.Opacity%2A> 의 <xref:System.Windows.Media.SolidColorBrush>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 3 개의 애니메이션을 사용 하 여 애니메이션 효과를 주는 합니다 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 하 고 <xref:System.Windows.Media.Brush.Opacity%2A> 의 <xref:System.Windows.Media.SolidColorBrush>.  
  
- 첫 번째 애니메이션을 <xref:System.Windows.Media.Animation.ColorAnimation>, 브러시의 색을 변경 <xref:System.Windows.Media.Colors.Gray%2A> 마우스 사각형 안으로 이동할 때.  
  
- 다음 애니메이션 다른 <xref:System.Windows.Media.Animation.ColorAnimation>, 브러시의 색을 변경 <xref:System.Windows.Media.Colors.Orange%2A> 마우스가 사각형을 벗어날 때입니다.  
  
- 마지막 애니메이션을 <xref:System.Windows.Media.Animation.DoubleAnimation>, 마우스 왼쪽된 단추를 누를 때 브러시의 불투명도 0.0으로 변경 합니다.  
  
 [!code-csharp[brushanimations_snip#SolidColorBrushAnimationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/brushanimations_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushanimationexample)]  
  
 다양 한 유형의 브러시에 애니메이션을 적용 하는 방법을 보여주는 전체 샘플을 보려면 합니다 [브러시 샘플](https://go.microsoft.com/fwlink/?LinkID=159973)합니다. 애니메이션에 대 한 자세한 내용은 참조는 [애니메이션 개요](animation-overview.md)합니다.  
  
 다른 애니메이션 예제를 사용 하 여 일관성을 위해이 예제의 코드 버전 사용을 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션을 적용 하는 개체입니다. 그러나 코드에서 단일 애니메이션을 적용할 때 간단 하 게 사용 합니다 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 사용 하는 대신 메서드를 <xref:System.Windows.Media.Animation.Storyboard>입니다. 예제를 보려면 [Storyboard를 사용하지 않고 속성에 애니메이션 효과 주기](how-to-animate-a-property-without-using-a-storyboard.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [애니메이션 개요](animation-overview.md)
- [Storyboard 개요](storyboards-overview.md)
- [브러시 샘플](https://go.microsoft.com/fwlink/?LinkID=159973)
