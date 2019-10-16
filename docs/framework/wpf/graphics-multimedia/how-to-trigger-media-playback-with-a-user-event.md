---
title: '방법: 사용자 이벤트를 사용하여 미디어 재생 트리거'
ms.date: 03/30/2017
helpviewer_keywords:
- synchronizing media playback with events [WPF]
- playback of media [WPF], synchronizing with events
- media [WPF], synchronizing playback with events
- multimedia [WPF], synchronizing media playback with events
ms.assetid: c4dbe632-6e7f-4d7f-9df5-98737a758bc3
ms.openlocfilehash: ae8ba54cc852bb85350492c95e3e890aebf6534f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769280"
---
# <a name="how-to-trigger-media-playback-with-a-user-event"></a>방법: 사용자 이벤트를 사용하여 미디어 재생 트리거
이 예제에서는 미디어 재생을 이벤트와 동기화하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.Controls.MediaElement> 컨트롤 및 <xref:System.Windows.Media.MediaTimeline> 를 클릭할 때 발생 하는 사운드를 재생 하는 클래스는 <xref:System.Windows.Controls.Button>합니다.  
  
 [!code-xaml[MediaGallery_snippet#SoundFromUserEventExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snippet/CSharp/SoundFromUserEventExample.xaml#soundfromusereventexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.MediaElement>
- <xref:System.Windows.Media.MediaTimeline>
- <xref:System.Windows.EventTrigger.RoutedEvent%2A>
- <xref:System.Windows.Media.Animation.Storyboard>
- [방법 항목](audio-and-video-how-to-topics.md)
- [그래픽 및 멀티미디어](index.md)
