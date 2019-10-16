---
title: '방법: 키 프레임을 사용하여 크기 변경에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- key frames [WPF], animating size changes with
- animation [WPF], size changes with key frames
- size changes [WPF], animating with key frames
ms.assetid: 86bd2950-d4c9-4ec4-aa8d-7dc3ccadded4
ms.openlocfilehash: 0629b6600444bd172af451fd7e970bff894d8047
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61789261"
---
# <a name="how-to-animate-size-changes-by-using-key-frames"></a>방법: 키 프레임을 사용하여 크기 변경에 애니메이션 효과 주기
이 예제에서는 키 프레임을 사용하여 크기 변경에 애니메이션 효과를 주는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames> 클래스에 애니메이션 효과를 합니다 <xref:System.Windows.Media.ArcSegment.Size%2A> 의 속성은 <xref:System.Windows.Media.ArcSegment>. 이 애니메이션은 다음과 같은 방식으로 세 가지 키 프레임을 사용합니다.  
  
1. 애니메이션의 처음 1/2 초 동안의 인스턴스를 사용 하 여는 <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> 클래스를 점차적으로 원호의 크기를 늘립니다. 과 같은 선형 키 프레임 <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> 값 사이 매끄러운 선형 전환을 만듭니다.  
  
2. 0.5 초가 고 끝에 다음의 인스턴스를 사용 하는 <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame> 클래스를 갑자기 원호의 크기를 늘립니다. 과 같은 불연속 키 프레임 <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame> 크기 변화를 갑자기 발생 되며 미묘 하지, 즉 값 간에 갑작스러운 이동을 만듭니다.  
  
3. 마지막 2 초 동안의 인스턴스를 사용 하는 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame> 클래스 원호의 크기를 늘립니다. 과 같은 스플라인 키 프레임 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame> 의 값에 따라 값 사이 가변 전환을 만듭니다는 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame.KeySpline%2A> 속성입니다. 이 예제에서 원호의 크기는 처음에는 느리게 증가했다가 시간 세그먼트가 끝나면서 기하급수적으로 증가합니다.  
  
 [!code-xaml[keyframes_snip#SizeAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/SizeAnimationUsingKeyFramesExample.xaml#sizeanimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames>
- <xref:System.Windows.Media.ArcSegment.Size%2A>
- <xref:System.Windows.Media.ArcSegment>
- <xref:System.Windows.Media.Animation.LinearSizeKeyFrame>
- <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame>
- <xref:System.Windows.Media.Animation.SplineSizeKeyFrame>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
