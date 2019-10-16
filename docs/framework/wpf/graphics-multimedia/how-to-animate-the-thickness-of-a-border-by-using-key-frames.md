---
title: '방법: 키 프레임을 사용하여 테두리 두께에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], border thickness with key frames
- key frames [WPF], animating border thickness with
- border thickness [WPF], animating with key frames
ms.assetid: 3a9cb463-0a63-407d-aae7-3fbb1a559947
ms.openlocfilehash: 101fd077bf125faadbd9a0186c2282e4b20ee78f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699034"
---
# <a name="how-to-animate-the-thickness-of-a-border-by-using-key-frames"></a>방법: 키 프레임을 사용하여 테두리 두께에 애니메이션 효과 주기
애니메이션을 적용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Control.BorderThickness%2A> 의 속성을 <xref:System.Windows.Controls.Border>입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.ThicknessAnimationUsingKeyFrames> 클래스에 애니메이션 효과를 <xref:System.Windows.Controls.Control.BorderThickness%2A> 의 속성을 <xref:System.Windows.Controls.Border>합니다. 이 애니메이션은 다음과 같은 방식으로 세 가지 키 프레임을 사용합니다.  
  
1. 처음 1/2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame> 클래스를 테두리의 두께 점차적으로 늘립니다. 이 예제에서는 사용 <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame> 값 사이 매끄러운 선형 증가 만들려고 합니다.  
  
2. 0.5 초가 고 끝에 다음의 인스턴스를 사용 하 여 <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame> 테두리의 두께 갑자기 늘립니다 클래스입니다. 파생 된 것과 같은 불연속 키 프레임 <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame> 애니메이션의 이동을 매끄럽지는, 즉 값 간에 갑작스러운 이동을 만듭니다.  
  
3. 마지막 2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame> 클래스 테두리의 두께를 줄입니다. 파생 된 것과 같은 스플라인 키 프레임 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame> 의 값에 따라 값 사이 가변 전환을 만듭니다는 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame.KeySpline%2A> 속성입니다. 이 키 프레임에서 애니메이션은 느리게 시작하다가 시간 세그먼트의 끝에 다가가면 기하급수적으로 빨라집니다.  
  
 [!code-xaml[keyframes_snip#ThicknessAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ThicknessAnimationUsingKeyFramesExample.xaml#thicknessanimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame>
- <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame>
- <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
- [BorderThickness 값에 애니메이션 효과 주기](../controls/how-to-animate-a-borderthickness-value.md)
