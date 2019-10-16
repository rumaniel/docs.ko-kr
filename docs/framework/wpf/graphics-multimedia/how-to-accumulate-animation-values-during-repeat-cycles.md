---
title: '방법: 반복 주기 동안 애니메이션 값 누적'
ms.date: 03/30/2017
helpviewer_keywords:
- accumulating animation values across repeating cycles [WPF]
- animation [WPF], accumulating values across repeating cycles
ms.assetid: 548df369-c7cc-4dab-b569-08b95ced2e7e
ms.openlocfilehash: bccdc9b7bf2d5a0ea476e39e8d54107854db7ae3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591465"
---
# <a name="how-to-accumulate-animation-values-during-repeat-cycles"></a>방법: 반복 주기 동안 애니메이션 값 누적
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 반복 주기에 대해 애니메이션 값 누적 하는 속성입니다.  
  
## <a name="example"></a>예제  
 사용 된 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 반복 주기에 대해 애니메이션의 기본 값을 누적 하는 속성입니다. 예를 들어 애니메이션 9 번 반복을 설정 하는 경우 (<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> = "9 x") 10 월 15 일 까지의 애니메이션 효과를 주는 속성을 설정 (10 = = 15), 속성에 애니메이션 효과 10에서 15 15 두 번째 주기 동안 20에서 첫 번째 주기 동안 세 번째 주기 등에 중 25 20에서입니다. 따라서 각 애니메이션 주기는 기준 값으로 이전 애니메이션 주기에서 끝 값을 사용합니다.  
  
 사용할 수는 `IsCumulative` 가장 기본적인 애니메이션 및 대부분의 키 프레임 애니메이션을 사용 하 여 속성입니다. 자세한 내용은 [애니메이션 개요](animation-overview.md) 하 고 [키 프레임 애니메이션 개요](key-frame-animations-overview.md)합니다.  
  
 다음 예제에서는 네 개의 사각형의 너비를 애니메이션으로이 동작을 보여 줍니다. 예제:  
  
- 사용 하 여 첫 번째 사각형에 애니메이션을 적용 <xref:System.Windows.Media.Animation.DoubleAnimation> 가져오거나 설정 합니다 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 속성을 `true`입니다.  
  
- 사용 하 여 두 번째 사각형에 애니메이션을 적용 <xref:System.Windows.Media.Animation.DoubleAnimation> 가져오거나 설정 합니다 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 속성의 기본값을 `false`입니다.  
  
- 사용 하 여 세 번째 사각형에 애니메이션을 적용 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 가져오거나 설정 합니다 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> 속성을 `true`입니다.  
  
- 사용 하 여 마지막 사각형에 애니메이션을 적용 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 가져오거나 설정 합니다 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> 속성을 `false`입니다.  
  
 [!code-xaml[timingbehaviors_snip#IsCumulativeWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsCumulativeExample.xaml#iscumulativewholepage)]  
  
## <a name="see-also"></a>참고자료

- [애니메이션 시작 값에 애니메이션 출력 값 추가](how-to-add-an-animation-output-value-to-an-animation-starting-value.md)
- [애니메이션 반복](how-to-repeat-an-animation.md)
- [애니메이션 개요](animation-overview.md)
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [방법 항목](animation-and-timing-how-to-topics.md)
