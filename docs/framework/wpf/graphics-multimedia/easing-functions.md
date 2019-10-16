---
title: 감속/가속 함수
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applying mathematical formulas to animations [WPF]
- applying easing functions to animations [WPF]
- mathematical formulas [WPF], applying to animations
- animations [WPF], realistic movement
- easing functions [WPF]
- customizing easing functions [WPF]
- easing functions [WPF], definition
- easing functions [WPF], customizing
- animations [WPF], applying
ms.assetid: 075b9c2b-82c4-43fa-b3cd-de0b6236eb38
ms.openlocfilehash: 72118711dfd40ad8c665157e09f01c60085db903
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965727"
---
# <a name="easing-functions"></a>감속/가속 함수
감속/가속 함수를 사용하여 사용자 지정 수식을 애니메이션에 적용할 수 있습니다. 예를 들어 마치 스프링 위에 있는 것처럼 개체가 사실적으로 바운스되거나 동작하도록 하고 싶을 수 있습니다. 키 프레임 또는 심지어 From/To/By 애니메이션을 사용하여 이러한 효과를 대략적으로 나타낼 수 있지만 상당히 복잡한 작업이 필요하며 수식을 사용할 때보다 애니메이션이 덜 정확해집니다.  
  
 에서 <xref:System.Windows.Media.Animation.EasingFunctionBase>상속 하 여 사용자 지정 감속/가속 함수를 만드는 것 외에도 런타임에서 제공 하는 여러 감속/가속 함수 중 하나를 사용 하 여 일반적인 효과를 만들 수 있습니다.  
  
- <xref:System.Windows.Media.Animation.BackEase>: 지정 된 경로에서 애니메이션 효과를 시작 하기 전에 애니메이션의 동작을 약간 취소 합니다.  
  
- <xref:System.Windows.Media.Animation.BounceEase>: 바운스 효과를 만듭니다.  
  
- <xref:System.Windows.Media.Animation.CircleEase>: 순환 함수를 사용 하 여 가속 및/또는 감속 하는 애니메이션을 만듭니다.  
  
- <xref:System.Windows.Media.Animation.CubicEase>: *F*(*t*) = *t*<sup>3</sup>공식을 사용 하 여 가속 및/또는 감속 하는 애니메이션을 만듭니다.  
  
- <xref:System.Windows.Media.Animation.ElasticEase>: Rest로 전환 될 때까지 앞뒤로 진동 하는 스프링과 유사한 애니메이션을 만듭니다.  
  
- <xref:System.Windows.Media.Animation.ExponentialEase>: 지 수 수식을 사용 하 여 가속 및/또는 감속 하는 애니메이션을 만듭니다.  
  
- <xref:System.Windows.Media.Animation.PowerEase>: 수식 *f*(*t*) = *t*<sup>p</sup> 를 사용 하 여 가속 및/또는 감속 되는 애니메이션을 만듭니다. 여기서 p <xref:System.Windows.Media.Animation.PowerEase.Power%2A> 는 속성과 같습니다.  
  
- <xref:System.Windows.Media.Animation.QuadraticEase>: 수식 *f*(*t*) = *t*<sup>2</sup>를 사용 하 여 가속 및/또는 감속 하는 애니메이션을 만듭니다.  
  
- <xref:System.Windows.Media.Animation.QuarticEase>: 수식 *f*(*t*) = *t*<sup>4</sup>를 사용 하 여 가속 및/또는 감속 하는 애니메이션을 만듭니다.  
  
- <xref:System.Windows.Media.Animation.QuinticEase>: *F*(*t*) = *t*<sup>5</sup>수식을 사용 하 여 가속 및/또는 감속 하는 애니메이션을 만듭니다.  
  
- <xref:System.Windows.Media.Animation.SineEase>: 사인 수식을 사용 하 여 가속 및/또는 감속 하는 애니메이션을 만듭니다.  
  
 애니메이션에 감속/가속 함수를 적용 하려면 애니메이션의 `EasingFunction` 속성을 사용 하 여 애니메이션에 적용할 감속/가속 함수를 지정 합니다. 적용 하는 다음 예제는 <xref:System.Windows.Media.Animation.BounceEase> 감속/가속 함수를를 <xref:System.Windows.Media.Animation.DoubleAnimation> 바운스 효과를 만듭니다.  
  
 [!code-xaml[BounceEase_snippet#BounceEase](~/samples/snippets/csharp/VS_Snippets_Wpf/bounceease_snippet/CS/window1.xaml#bounceease)]  
  
 이전 예제에서는 감속/가속 함수를 From/To/By 애니메이션에 적용했습니다. 이러한 감속/가속 함수를 키 프레임 애니메이션에 적용할 수도 있습니다. 다음 예제에서는 키 프레임과 연결된 감속/가속 함수를 사용하여 위로 수축했다가 느려진 다음 아래로 늘어난 후(떨어지는 것처럼) 바운스되었다가 정지되는 사각형의 애니메이션을 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[EasingFunctionDoubleKeyFrame_snippet#EasingFunctionDoubleKeyFrame](~/samples/snippets/csharp/VS_Snippets_Wpf/easingfunctiondoublekeyframe_snippet/CS/window1.xaml#easingfunctiondoublekeyframe)]  
  
 <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A> 속성을 사용 하 여 감속/가속 함수가 동작 하는 방법, 즉 애니메이션이 보간 되는 방식을 변경할 수 있습니다. 다음 세 가지 가능한 값을 지정할 <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>수 있습니다.  
  
- <xref:System.Windows.Media.Animation.EasingMode.EaseIn>: 보간은 감속/가속 함수와 연결 된 수식을 따릅니다.  
  
- <xref:System.Windows.Media.Animation.EasingMode.EaseOut>: 보간은은 100% 보간에서 감속/가속 함수와 연결 된 수식의 출력을 뺀 값을 따릅니다.  
  
- <xref:System.Windows.Media.Animation.EasingMode.EaseInOut>: 보간 사용 <xref:System.Windows.Media.Animation.EasingMode.EaseIn> 애니메이션의 처음 절반에 대 한 및 <xref:System.Windows.Media.Animation.EasingMode.EaseOut> 하반기에 대 한 합니다.  
  
 다음 그래프에서는 *f*(*x*)가 <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A> 애니메이션 진행률을 나타내고 *t* 는 시간을 나타내는의 여러 값을 보여 줍니다.  
  
 <xref:System.Windows.Media.Animation.BackEase>  
  
 ![BackEase EasingMode 그래프](./media/backease-graph.png "BackEase_Graph")  
  
 <xref:System.Windows.Media.Animation.BounceEase>  
  
 ![BounceEase EasingMode 그래프](./media/bounceease-graph.png "BounceEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CircleEase>  
  
 ![CircleEase EasingMode 그래프](./media/circleease-graph.png "CircleEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CubicEase>  
  
 ![CubicEase EasingMode 그래프](./media/cubicease-graph.png "CubicEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ElasticEase>  
  
 ![다양한 easingmode 그래프로 나타낸 ElasticEase](./media/elasticease-graph.png "ElasticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ExponentialEase>  
  
 ![다양한 easingmode 그래프로 나타낸 ExponentialEase](./media/exponentialease-graph.png "ExponentialEase_Graph")  
  
 <xref:System.Windows.Media.Animation.PowerEase>  
  
 ![다양한 easingmode 그래프로 나타낸 QuarticEase](./media/quarticease-graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuadraticEase>  
  
 ![다양한 easingmode 그래프로 나타낸 QuadraticEase](./media/quadraticease-graph.png "QuadraticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuarticEase>  
  
 ![다양한 easingmode 그래프로 나타낸 QuarticEase](./media/quarticease-graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuinticEase>  
  
 ![다양한 easingmode 그래프로 나타낸 QuinticEase](./media/quinticease-graph.png "QuinticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.SineEase>  
  
 ![다양한 EasingMode 값의 SineEase](./media/sineease-graph.png "SineEase_Graph")  
  
> [!NOTE]
> 사용할 수 있습니다 <xref:System.Windows.Media.Animation.PowerEase> 와 같은 동작을 만들려면 <xref:System.Windows.Media.Animation.CubicEase>를 <xref:System.Windows.Media.Animation.QuadraticEase>, <xref:System.Windows.Media.Animation.QuarticEase>, 및 <xref:System.Windows.Media.Animation.QuinticEase> 사용 하 여는 <xref:System.Windows.Media.Animation.PowerEase.Power%2A> 속성입니다. 예를 들어 사용 하려는 <xref:System.Windows.Media.Animation.PowerEase> 를 대체할 <xref:System.Windows.Media.Animation.CubicEase>, 지정는 <xref:System.Windows.Media.Animation.PowerEase.Power%2A> 값 3입니다.  
  
 런타임에 포함 된 감속/가속 함수를 사용 하는 것 외에도 상속 하 여 사용자 고유의 사용자 지정 감속/가속 함수를 만들 수 있습니다 <xref:System.Windows.Media.Animation.EasingFunctionBase>합니다. 다음 예제에서는 단일 사용자 지정 감속/가속 함수를 만드는 방법을 보여 줍니다. 감속/가속 함수를 재정의 하 여 작동 하는 방법에 대 한 고유한 수학 논리를 추가할 수는 <xref:System.Windows.Media.Animation.EasingFunctionBase.EaseInCore%2A> 메서드.   
  
 [!code-csharp[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/customlog10easingfunction.cs#customeasingfunction)]
 [!code-vb[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/visualbasic/VS_Snippets_Wpf/customeasingfunction/visualbasic/customlog10easingfunction.vb#customeasingfunction)]
 [!code-xaml[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/window1.xaml#customeasingfunction)]
