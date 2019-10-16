---
title: '방법: 키 프레임을 사용하여 점에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- key frames [WPF], animating Points with
- Points [WPF], animating with key frames
- animation [WPF], Points with key frames
ms.assetid: d2e2ef10-0773-4133-856e-d41c09f60ded
ms.openlocfilehash: b706568a0e8221aac737780592882f728f0f9e9c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010165"
---
# <a name="how-to-animate-a-point-by-using-key-frames"></a>방법: 키 프레임을 사용하여 점에 애니메이션 효과 주기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> 애니메이션 효과를 주는 클래스를 <xref:System.Windows.Point>입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 삼각형 경로를 따라 타원을 이동합니다. 예제에서는 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> 클래스에 애니메이션 효과를 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 의 속성을 <xref:System.Windows.Media.EllipseGeometry>입니다. 이 애니메이션은 다음과 같은 방식으로 세 가지 키 프레임을 사용합니다.  
  
1. 처음 1/2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.LinearPointKeyFrame> 시작 위치부터 일정 한 속도로 경로 따라 타원을 이동 하는 클래스입니다. 과 같은 선형 키 프레임 <xref:System.Windows.Media.Animation.LinearPointKeyFrame> 값 사이 매끄러운 선형 보간을 만듭니다.  
  
2. 0.5 초가 고 다음의 끝 중의 인스턴스를 사용 하 여 <xref:System.Windows.Media.Animation.DiscretePointKeyFrame> 갑자기 다음 위치로 경로 따라 타원을 이동 하는 클래스입니다. 과 같은 불연속 키 프레임 <xref:System.Windows.Media.Animation.DiscretePointKeyFrame> 값 간에 갑작스러운 이동을 만듭니다.  
  
3. 마지막 2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.SplinePointKeyFrame> 클래스 타원을 다시 시작 위치로 이동 합니다. 과 같은 스플라인 키 프레임 <xref:System.Windows.Media.Animation.SplinePointKeyFrame> 의 값에 따라 값 사이 가변 전환을 만듭니다는 <xref:System.Windows.Media.Animation.SplinePointKeyFrame.KeySpline%2A> 속성입니다. 이 예제에서 애니메이션은 느리게 시작하다가 시간 세그먼트의 끝에 다가가면 기하급수적으로 빨라집니다.  
  
 [!code-csharp[keyframes_snip#PointAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/PointAnimationUsingKeyFramesExample.cs#pointanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#PointAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/pointanimationusingkeyframesexample.vb#pointanimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#PointAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/PointAnimationUsingKeyFramesExample.xaml#pointanimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
 다른 애니메이션 예제를 사용 하 여 일관성을 위해이 예제의 코드 버전 사용을 <xref:System.Windows.Media.Animation.Storyboard> 적용할 개체는 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>합니다. 그러나 코드에서 단일 애니메이션을 적용할 때 간단 하 게 사용 합니다 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 사용 하는 대신 메서드를 <xref:System.Windows.Media.Animation.Storyboard>입니다. 예제를 보려면 [Storyboard를 사용하지 않고 속성에 애니메이션 효과 주기](how-to-animate-a-property-without-using-a-storyboard.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>
- <xref:System.Windows.Media.EllipseGeometry.Center%2A?displayProperty=nameWithType>
- <xref:System.Windows.Media.EllipseGeometry>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
