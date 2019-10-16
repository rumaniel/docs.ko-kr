---
title: '방법: 스토리보드를 사용하여 애니메이션 효과를 적용한 후 속성 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], changing property values after
ms.assetid: 79466556-4dbf-40bd-9c1e-a77613b07077
ms.openlocfilehash: 593d3fcefe3bb81518d0886afde82f9a172874ba
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64912381"
---
# <a name="how-to-set-a-property-after-animating-it-with-a-storyboard"></a>방법: 스토리보드를 사용하여 애니메이션 효과를 적용한 후 속성 설정
경우에 따라 애니메이션이 적용 된 후에 속성의 값을 변경할 수 없습니다 나타날 것입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.Animation.Storyboard> 색에 애니메이션을 적용 하는 데 사용 되는 <xref:System.Windows.Media.SolidColorBrush>. 스토리 보드는 단추를 클릭할 때 트리거됩니다. 합니다 <xref:System.Windows.Media.Animation.Timeline.Completed> 프로그램 알림을 받을 수 있도록 이벤트를 처리 때는 <xref:System.Windows.Media.Animation.ColorAnimation> 완료 합니다.  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton1Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton1declaration)]  
  
## <a name="example"></a>예제  
 이후에 <xref:System.Windows.Media.Animation.ColorAnimation> 완료 되 면 프로그램 하려고 브러시의 색을 파란색을 변경 합니다.  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton1Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton1handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton1Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton1handler)]  
  
 이전 코드는 작업을 수행할 나타나지: 값인 yellow, 브러시 유지가 제공한는 <xref:System.Windows.Media.Animation.ColorAnimation> 작업도 합니다. 기본 속성 값 (기본값)는 실제로 파란색으로 변경 됩니다. 효과적으로 또는 현재 값은 노란색으로 남아 있지만 때문에 <xref:System.Windows.Media.Animation.ColorAnimation> 여전히 기본 값을 재정의 합니다. 유효한 값을 다시 되도록 기본 값을 원하는 경우 속성에 영향을 주지 애니메이션을 중지 해야 합니다. Storyboard 애니메이션을 사용 하 여이 작업을 수행 하는 방법은 세 가지가 있습니다.  
  
- 애니메이션의 설정 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 속성 <xref:System.Windows.Media.Animation.FillBehavior.Stop>  
  
- 전체 스토리 보드를 제거 합니다.  
  
- 개별 속성에서 애니메이션을 제거 합니다.  
  
## <a name="set-the-animations-fillbehavior-property-to-stop"></a>애니메이션의 FillBehavior 속성 Stop으로 설정  
 설정 하 여 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 에 <xref:System.Windows.Media.Animation.FillBehavior.Stop>을 활성 기간의 끝에 도달한 후 대상 속성에 영향을 주지 않으려면 애니메이션을 알려줍니다.  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton2Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton2declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton2Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton2handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton2Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton2handler)]  
  
## <a name="remove-the-entire-storyboard"></a>전체 스토리 보드를 제거 합니다.  
 사용 하 여는 <xref:System.Windows.Media.Animation.RemoveStoryboard> 트리거 또는 <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=nameWithType> 메서드를 알리는 해당 대상 속성에 영향을 주지 않으려면 storyboard 애니메이션 합니다. 이 접근 방식 및 설정 간의 차이 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 속성은 스토리 보드를 제거할 수 있습니다 있는 동안 언제 든 지는 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 속성에만 효과가 애니메이션 활성 기간의 끝에 도달 합니다.  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton3Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton3declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton3Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton3handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton3Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton3handler)]  
  
## <a name="remove-an-animation-from-an-individual-property"></a>개별 속성에서 애니메이션을 제거 합니다.  
 애니메이션 속성에 영향을 주지 않으려면 다른 기술을 사용 하는 것은 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> 애니메이션 효과 줄 개체의 메서드. 첫 번째 매개 변수로 애니메이션 효과가 적용 되는 속성을 지정 하 고 `null` 두 번째입니다.  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton4Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton4declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton4Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton4handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton4Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton4handler)]  
  
 이 기술은 비 storyboard 애니메이션 에서도 작동합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>
- <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=nameWithType>
- <xref:System.Windows.Media.Animation.RemoveStoryboard>
- [애니메이션 개요](animation-overview.md)
- [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)
