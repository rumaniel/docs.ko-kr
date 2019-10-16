---
title: '방법: 키 프레임을 사용하여 문자열에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], strings with key frames
- strings [WPF], animating with key frames
- key frames [WPF], animating strings with
ms.assetid: c62bc9fd-c09a-4227-bce0-0a1ab82049dd
ms.openlocfilehash: 4a37408ad90fda12a95e66c1b44018967b376837
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651430"
---
# <a name="how-to-animate-a-string-by-using-key-frames"></a>방법: 키 프레임을 사용하여 문자열에 애니메이션 효과 주기
이 예제는 문자열에 애니메이션을 적용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.ContentControl.Content%2A> 의 속성을 <xref:System.Windows.Controls.Button> 키 프레임을 사용 하 여 컨트롤을 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames> 클래스에 애니메이션 효과를 <xref:System.Windows.Controls.ContentControl.Content%2A> 의 속성을 <xref:System.Windows.Controls.Button>합니다.  
  
 이 예제에서 모든 키 프레임의 인스턴스를 사용 합니다 <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame> 키 프레임을 사용 하 여 만든 문자열 애니메이션을 불연속 키 프레임에만 사용할 수 있으므로 클래스. 과 같은 불연속 키 프레임 <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame> 애니메이션에 변경 내용을 신속 하 게 발생 한, 즉 값 간에 갑작스러운 이동을 만듭니다.  
  
 [!code-xaml[keyframes_snip#StringAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/StringAnimationUsingKeyFramesExample.xaml#stringanimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>
- <xref:System.Windows.Controls.ContentControl.Content%2A>
- <xref:System.Windows.Controls.Button>
- <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
