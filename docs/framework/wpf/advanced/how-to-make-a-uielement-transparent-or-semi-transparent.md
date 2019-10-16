---
title: '방법: UIElement를 투명하거나 반투명하게 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- UIElements [WPF], transparency
- opacity [WPF], of UIElements
- transparency of UIElements [WPF]
- UIElements [WPF], opacity
ms.assetid: a49fc8d6-7b32-4f28-9122-39b632a19b4b
ms.openlocfilehash: 1de9a7e11fee241ecb71242e9808e77b7e5e63b0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942872"
---
# <a name="how-to-make-a-uielement-transparent-or-semi-transparent"></a>방법: UIElement를 투명하거나 반투명하게 만들기
이 예제에서는 있도록는 <xref:System.Windows.UIElement> 투명 하거나 반투명 하 게 합니다. 설정 요소를 투명 하거나 반투명 하 게, 해당 <xref:System.Windows.UIElement.Opacity%2A> 속성입니다. 값이 `0.0` 요소를 완전히 투명 해지고 값을 사용 하면 `1.0` 요소를 완전히 불투명 하 게 만듭니다. 값 `0.5` 요소 50% 불투명 해지고 0.725 만듭니다. 요소의 <xref:System.Windows.UIElement.Opacity%2A> 로 설정 된 `1.0` 기본적으로 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.UIElement.Opacity%2A> 단추에 `0.25`, 하 고 해당 콘텐츠 (이 예제의 경우 단추 텍스트)에 25% 불투명 하 게 만들기.  
  
 [!code-xaml[brushsamples_snip#2](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#2)]  
  
 [!code-csharp[brushsamples_procedural_snip#2](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#2)]  
  
 요소의 콘텐츠에 자체적인 하는 경우 <xref:System.Windows.UIElement.Opacity%2A> 포함 된 요소에 대해 설정을, 해당 값 곱할 <xref:System.Windows.UIElement.Opacity%2A>합니다.  
  
 다음 예제에서는 단추의 <xref:System.Windows.UIElement.Opacity%2A> 하 `0.25`, 및 <xref:System.Windows.UIElement.Opacity%2A> 의 <xref:System.Windows.Controls.Image> 단추를 사용 하 여 포함 된 컨트롤 `0.5`. 결과적으로, 이미지 12.5% 불투명 하 게 나타납니다. 0.25 * 0.5 = 0.125.  
  
 [!code-xaml[brushsamples_snip#3](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#3)]  
  
 [!code-csharp[brushsamples_procedural_snip#3](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#3)]  
  
 요소의 불투명도 제어 하는 방법의 불투명도 설정 하는 것은 <xref:System.Windows.Media.Brush> 요소를 칠하는 합니다. 이 방법은 선택적으로 요소를 일부의 불투명도 변경할 수 있습니다 및 요소를 사용 하 여 보다 성능상 이점이 <xref:System.Windows.UIElement.Opacity%2A> 속성입니다. 다음 예제에서는 합니다 <xref:System.Windows.Media.Brush.Opacity%2A> 의 <xref:System.Windows.Media.SolidColorBrush> 단추의 그리는 데 <xref:System.Windows.Controls.Control.Background%2A> 로 설정 된 `0.25`합니다. 결과적으로 브러시의 백그라운드 25% 불투명 하 게 되었지만 내용이 (단추의 텍스트) 100% 불투명 하 게 유지 됩니다.  
  
 [!code-xaml[brushsamples_snip#4](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#4)]  
  
 [!code-csharp[brushsamples_procedural_snip#4](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#4)]  
  
 브러시 내의 개별 색의 불투명도 제어할 수도 있습니다. 색상 및 브러시에 대 한 자세한 내용은 참조 하세요. [단색 및 그라데이션 개요 그리기](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)합니다. 요소의 불투명도 애니메이션을 적용 하는 방법을 보여주는 예제를 참조 하세요 [요소 또는 브러시의 불투명도 애니메이션 효과 주기](../graphics-multimedia/how-to-animate-the-opacity-of-an-element-or-brush.md)합니다.
