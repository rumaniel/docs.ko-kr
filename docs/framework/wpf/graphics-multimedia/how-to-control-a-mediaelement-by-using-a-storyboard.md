---
title: '방법: 스토리보드를 사용하여 MediaElement 제어'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- multimedia [WPF], controlling playback of media with Storyboards
- controlling playback of media [WPF], with Storyboards
- Storyboards [WPF], controlling playback of media with
- media [WPF], controlling playback with Storyboards
- playback of media [WPF], controlling with Storyboards
ms.assetid: 6128ca77-b826-4e36-b968-6f237157c543
ms.openlocfilehash: ae785e11b1da0f2c408b24021ad46ab071419378
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62032237"
---
# <a name="how-to-control-a-mediaelement-by-using-a-storyboard"></a>방법: 스토리보드를 사용하여 MediaElement 제어
제어 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.MediaElement> 를 사용 하 여는 <xref:System.Windows.Media.MediaTimeline> 에 <xref:System.Windows.Media.Animation.Storyboard>합니다.  
  
## <a name="example"></a>예제  
 사용 하는 경우를 <xref:System.Windows.Media.MediaTimeline> 에 <xref:System.Windows.Media.Animation.Storyboard> 의 타이밍을 제어 하는 <xref:System.Windows.Controls.MediaElement>, 기능은 다른 기능과 동일한 <xref:System.Windows.Media.Animation.Timeline> 애니메이션 등의 개체입니다. 예를 들어,를 <xref:System.Windows.Media.MediaTimeline> 사용 하 여 <xref:System.Windows.Media.Animation.Timeline> 등의 속성을 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 시작 하는 시기를 지정 하는 속성을 <xref:System.Windows.Controls.MediaElement> (미디어 재생을 시작 합니다.). 또한 사용 하 여는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 속성을 통해 지정 시간 <xref:System.Windows.Controls.MediaElement> 활성 (미디어 재생 기간). 사용에 대 한 자세한 내용은 <xref:System.Windows.Media.Animation.Timeline> 사용 하 여 개체를 <xref:System.Windows.Media.Animation.Storyboard>를 참조 하세요 [Storyboard 개요](storyboards-overview.md)합니다.  
  
 이 예제에 사용 하는 간단한 미디어 플레이어를 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.MediaTimeline> 재생을 제어할 수 있습니다. Media player에는 재생, 일시 중지, 재개 및 중지 단추입니다. 플레이어가 있습니다를 <xref:System.Windows.Controls.Slider> 역할 진행률 표시줄을 컨트롤입니다.  
  
 다음 예제에서는 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] media player에 대 한 합니다.  
  
 [!code-xaml[MediaGallery_snip#MediaTimelineExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml#mediatimelineexamplewholepage)]  
  
 다음 예제에서는 진행률 표시줄에 대 한 기능을 만듭니다.  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaTimelineExample.xaml.cs#codebehindmediatimelineexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml.vb#codebehindmediatimelineexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.MediaElement>
- <xref:System.Windows.Media.MediaTimeline>
- <xref:System.Windows.Media.Animation.Storyboard>
- [MediaElement 제어(재생, 일시 중지, 정지, 볼륨 및 속도)](how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)
- [Storyboard 개요](storyboards-overview.md)
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [애니메이션 개요](animation-overview.md)
- [방법 항목](audio-and-video-how-to-topics.md)
- [그래픽 및 멀티미디어](index.md)
