---
title: '방법: 애니메이션이 있는 미디어 재생'
ms.date: 03/30/2017
helpviewer_keywords:
- multimedia [WPF], playback with animations
- playback of media [WPF], with animations
- animation [WPF], media playback with
- media [WPF], playback with animations
ms.assetid: 8982b7b7-1c6c-4b24-8801-b328862975f5
ms.openlocfilehash: 200f9d62c67a02088fe5a5789cdb41a04837d430
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61921669"
---
# <a name="how-to-play-media-with-animations"></a>방법: 애니메이션이 있는 미디어 재생
사용 하 여 동시 미디어 및 애니메이션을 재생 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.MediaTimeline> 하 고 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 클래스를 같은 <xref:System.Windows.Media.Animation.Storyboard>합니다.  
  
## <a name="example"></a>예제  
 하나를 사용할 수 있습니다 <xref:System.Windows.Media.MediaTimeline> 개체를 <xref:System.Windows.Media.Animation.Storyboard> 다른 함께 <xref:System.Windows.Media.Animation.Timeline> 애니메이션 등의 개체입니다.  
  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.ParallelTimeline.SlipBehavior%2A> 의 속성을 <xref:System.Windows.Media.Animation.Storyboard> 값으로 `Slip`, 애니메이션 (이 예제의 비디오) 미디어 진행 될 때까지 진행 되지 않습니다. 지정 하는. 이 기능은 로드 시간 때문에 미디어 재생을 지연해야 할 경우에 필요할 수 있습니다.  
  
 [!code-xaml[MediaGallery_snippet#MediaTimelinePlusAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snippet/CSharp/MediaTimelinePlusAnimationExample.xaml#mediatimelineplusanimationexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.MediaTimeline>
- <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>
- <xref:System.Windows.Media.Animation.Storyboard>
- <xref:System.Windows.Media.Animation.ParallelTimeline.SlipBehavior%2A>
- [방법 항목](audio-and-video-how-to-topics.md)
- [Storyboard 개요](storyboards-overview.md)
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [애니메이션 개요](animation-overview.md)
- [그래픽 및 멀티미디어](index.md)
