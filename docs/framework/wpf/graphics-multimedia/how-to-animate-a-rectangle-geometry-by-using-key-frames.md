---
title: '방법: 키 프레임을 사용하여 사각형에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- key frames [WPF], animating RectangleGeometry objects with
- RectangleGeometry objects [WPF], animating with key frames
- animation [WPF], RectangleGeometry objects with key frames
ms.assetid: a8b45ceb-0e32-4ba1-928f-df6d30db17c6
ms.openlocfilehash: 03953b79127ffceeb49e4ece2070d09f382448a5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010100"
---
# <a name="how-to-animate-a-rectangle-geometry-by-using-key-frames"></a>방법: 키 프레임을 사용하여 사각형에 애니메이션 효과 주기
애니메이션을 적용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.RectangleGeometry.Rect%2A> 의 속성을 <xref:System.Windows.Media.RectangleGeometry> 키 프레임을 사용 하 여 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames> 클래스에 애니메이션 효과를 <xref:System.Windows.Media.RectangleGeometry.Rect%2A> 의 속성을 <xref:System.Windows.Media.RectangleGeometry>합니다. 이 애니메이션은 다음과 같은 방식으로 세 가지 키 프레임을 사용합니다.  
  
1. 처음 2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.LinearRectKeyFrame> 위치, 너비 및 사각형의 높이의 점진적 변화에 애니메이션 효과를 주는 클래스입니다. 과 같은 선형 키 프레임 <xref:System.Windows.Media.Animation.LinearRectKeyFrame> 값 사이 매끄러운 선형 전환을 만듭니다.  
  
2. 0.5 초가 고 다음의 끝 중의 인스턴스를 사용 하 여 <xref:System.Windows.Media.Animation.DiscreteRectKeyFrame> 클래스를 사각형의 높이 갑자기 줄입니다. 과 같은 불연속 키 프레임 <xref:System.Windows.Media.Animation.DiscreteRectKeyFrame> 값 간에 급격 한 변화를 만듭니다, 높이 감소 신속 하 게 발생 하 고는 미묘 하지 않습니다.  
  
3. 마지막 2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.SplineRectKeyFrame> 사각형을 다시 원래 크기와 위치를 변경 하는 클래스입니다. 과 같은 스플라인 키 프레임 <xref:System.Windows.Media.Animation.SplineRectKeyFrame> 의 값에 따라 값 사이 가변 전환을 만듭니다는 <xref:System.Windows.Media.Animation.SplineRectKeyFrame.KeySpline%2A> 속성입니다. 이 예제에서 변화는 느리게 시작하다가 시간 세그먼트의 끝에 다가가면 기하급수적으로 빨라집니다.  
  
 [!code-csharp[keyframes_snip#RectAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/RectAnimationUsingKeyFramesExample.cs#rectanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#RectAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/rectanimationusingkeyframesexample.vb#rectanimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#RectAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/RectAnimationUsingKeyFramesExample.xaml#rectanimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.RectangleGeometry>
- <xref:System.Windows.Media.RectangleGeometry.Rect%2A>
- <xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
