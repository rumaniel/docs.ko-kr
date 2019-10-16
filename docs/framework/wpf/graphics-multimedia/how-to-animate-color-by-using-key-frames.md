---
title: '방법: 키 프레임을 사용하여 색에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [WPF], animating with key frames
- animation [WPF], colors with key frames
- key frames [WPF], animating colors with
ms.assetid: ab04ffa6-4de9-4d5b-a3b4-4e35d5b2ef35
ms.openlocfilehash: e579c4beb757ccf58eb1b9ca1f3852a5b96cac1a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010031"
---
# <a name="how-to-animate-color-by-using-key-frames"></a>방법: 키 프레임을 사용하여 색에 애니메이션 효과 주기
애니메이션을 적용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 의 한 <xref:System.Windows.Media.SolidColorBrush> 키 프레임을 사용 하 여 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames> 클래스에 애니메이션 효과를 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 의 속성을 <xref:System.Windows.Media.SolidColorBrush>합니다. 이 애니메이션은 다음과 같은 방식으로 세 가지 키 프레임을 사용합니다.  
  
1. 처음 2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.LinearColorKeyFrame> 점진적으로 녹색에서 빨간색으로 색을 변경 하는 클래스입니다. 과 같은 선형 키 프레임 <xref:System.Windows.Media.Animation.LinearColorKeyFrame> 값 사이 매끄러운 선형 전환을 만듭니다.  
  
2. 0.5 초가 고 다음의 끝 중의 인스턴스를 사용 하 여 <xref:System.Windows.Media.Animation.DiscreteColorKeyFrame> 신속 하 게 색을 빨간색에서 노란색으로 변경 하는 클래스입니다. 과 같은 불연속 키 프레임 <xref:System.Windows.Media.Animation.DiscreteColorKeyFrame> 값 간에 급격 한 변화를 만듭니다, 애니메이션의이 부분에서 색 변경 신속 하 게 발생 하 고는 미묘 하지 않습니다.  
  
3. 마지막 2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.SplineColorKeyFrame> 다시 색을 변경 하는 클래스-이 시간 노란색에서 녹색입니다. 과 같은 스플라인 키 프레임 <xref:System.Windows.Media.Animation.SplineColorKeyFrame> 의 값에 따라 값 사이 가변 전환을 만듭니다는 <xref:System.Windows.Media.Animation.SplineColorKeyFrame.KeySpline%2A> 속성입니다. 이 예제에서 색 변화는 느리게 시작하다가 시간 세그먼트의 끝에 다가가면 기하급수적으로 빨라집니다.  
  
 [!code-csharp[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/ColorAnimationUsingKeyFramesExample.cs#coloranimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/coloranimationusingkeyframesexample.vb#coloranimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ColorAnimationUsingKeyFramesExample.xaml#coloranimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.SolidColorBrush.Color%2A>
- <xref:System.Windows.Media.SolidColorBrush>
- <xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
