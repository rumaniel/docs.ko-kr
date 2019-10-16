---
title: '방법: 키 프레임을 사용하여 개체에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], objects with key frames
- key frames [WPF], animating objects with
ms.assetid: b1f15ba9-cac7-4cea-8699-5c6b55c05c5e
ms.openlocfilehash: ffbe1845b634c8f94eb6a10dfa44fcf9903e0cd5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69933902"
---
# <a name="how-to-animate-an-object-by-using-key-frames"></a>방법: 키 프레임을 사용하여 개체에 애니메이션 효과 주기
이 예제에서는 개체에 애니메이션 효과를 주는 방법을 보여 줍니다 .이 예제 <xref:System.Windows.Controls.Page.Background%2A> 에서는 키 프레임 <xref:System.Windows.Controls.Page> 을 사용 하 여 컨트롤의 속성입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 클래스를 사용 하 여 <xref:System.Windows.Controls.Page> 컨트롤의 <xref:System.Windows.Controls.Page.Background%2A> 속성에 대 한 색 변경에 애니메이션 효과를 적용 합니다. 예제 애니메이션은 일정 한 간격으로 다른 배경 브러시로 변경 됩니다. 이 애니메이션은 <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> 클래스를 사용 하 여 세 개의 다른 키 프레임을 만듭니다. 애니메이션은 다음과 같은 방식으로 키 프레임을 사용 합니다.  
  
1. 첫 번째 초가 끝날 때 <xref:System.Windows.Media.LinearGradientBrush> 클래스의 인스턴스에 애니메이션 효과를 적용 합니다. 예제의이 섹션에서는 색이 노랑에서 주황, 빨강으로 전환 되도록 선형 그라데이션을 배경색에 적용 합니다.  
  
2. 다음 초가 끝날 때 <xref:System.Windows.Media.RadialGradientBrush> 클래스의 인스턴스에 애니메이션 효과를 적용 합니다. 예제의이 섹션에서는 색이 흰색에서 파랑으로 파랑으로 전환 되도록 방사형 그라데이션을 배경색에 적용 합니다.  
  
3. 세 번째 초가 끝날 때 <xref:System.Windows.Media.DrawingBrush> 클래스의 인스턴스에 애니메이션 효과를 적용 합니다. 예제의이 섹션에서는 배경에 바둑판 패턴을 적용 합니다.  
  
4. 애니메이션은 다시 시작 되 고 무기한 반복 됩니다.  
  
> [!NOTE]
> <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>는 클래스에서 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 사용할 수 있는 키 프레임의 유일한 형식입니다. 이 예제의 색 <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> 변경이 갑자기 발생 하는 경우와 같은 키 프레임은 값의 급격 한 변화를 만듭니다.  
  
 [!code-xaml[keyframes_snip#ObjectAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ObjectAnimationUsingKeyFramesExample.xaml#objectanimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>
- <xref:System.Windows.Controls.Page.Background%2A>
- <xref:System.Windows.Controls.Page>
- <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>
- <xref:System.Windows.Media.LinearGradientBrush>
- <xref:System.Windows.Media.RadialGradientBrush>
- <xref:System.Windows.Media.DrawingBrush>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
