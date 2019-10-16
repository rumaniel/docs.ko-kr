---
title: '방법: 요소 또는 브러시의 불투명도에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- opacity [WPF], animating
- animation [WPF], Opacity property
ms.assetid: 572af23b-39dd-48d1-9db5-4bca56a4b3d3
ms.openlocfilehash: 2f18861eb18f81b631245d1d933b7acb1b3e0e42
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950507"
---
# <a name="how-to-animate-the-opacity-of-an-element-or-brush"></a>방법: 요소 또는 브러시의 불투명도에 애니메이션 효과 주기
프레임 워크 요소를 뷰에서 페이드 인 하거나 축소 하려면 해당 <xref:System.Windows.UIElement.Opacity%2A> 속성에 애니메이션 효과를 주거나 그리기에 사용 되는 <xref:System.Windows.Media.Brush.Opacity%2A> <xref:System.Windows.Media.Brush> (또는 브러시)의 속성에 애니메이션 효과를 적용할 수 있습니다. 요소의 불투명도에 애니메이션 효과를 적용 하면 해당 개체와 해당 자식이 뷰에서 페이드 인 및 출력을 페이드 아웃 하지만 요소를 그리는 데 사용 되는 브러시에 애니메이션 효과를 적용 하면 요소의 어느 부분이 페이드 인하는 것을 보다 쉽게 선택할 수 있습니다. 예를 들어, 단추의 배경을 그리는 데 사용 되는 브러시의 불투명도에 애니메이션 효과를 적용할 수 있습니다. 이로 인해 단추의 배경이 화면에서 페이드 인 및 페이드 아웃 되는 동안 텍스트는 완전히 불투명 하 게 됩니다.  
  
> [!NOTE]
> 의에 <xref:System.Windows.Media.Brush.Opacity%2A> 애니메이션 효과를 적용 하면 요소의 속성에 <xref:System.Windows.UIElement.Opacity%2A> 애니메이션 효과를 주는것보다성능이향상됩니다.<xref:System.Windows.Media.Brush>  
  
 다음 예제에서는 두 단추에 애니메이션 효과를 적용 하 여 뷰에서 페이드 인 및 페이드 아웃 합니다. 첫 번째 <xref:System.Windows.Controls.Button> 의 불투명도는 5 초 이상 `1.0` <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 에서 `0.0` 까지 애니메이션 효과를 적용 합니다. 두 번째 단추도 애니메이션으로 적용 되지만,를 그리는 <xref:System.Windows.Controls.Control.Background%2A> 데 사용 되는 system.windows.media.solidcolorbrush>의 불투명도는 전체 단추의 불투명도가 아닌 애니메이션 효과가 적용 됩니다. 예제가 실행 되 면 첫 번째 단추는 뷰에서 완전히 페이드 인 되 고 표시 되지 않습니다. 반면 두 번째 단추의 배경은 뷰에서 페이드 인 및 페이드 아웃 됩니다. 텍스트와 테두리는 완전히 불투명 하 게 유지 됩니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[timingbehaviors_snip#10](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/OpacityAnimationExample.xaml#10)]  
  
 이 예제에서는 코드를 생략 했습니다. 전체 샘플은 <xref:System.Windows.Media.Color> <xref:System.Windows.Media.LinearGradientBrush>내에서의 불투명도에 애니메이션 효과를 주는 방법을 보여 줍니다.  전체 샘플은 [요소의 불투명도에 애니메이션 효과 적용 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/OpacityAnimation)을 참조 하세요.
