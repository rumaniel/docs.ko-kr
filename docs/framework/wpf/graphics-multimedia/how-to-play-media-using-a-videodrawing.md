---
title: '방법: VideoDrawing을 사용하여 미디어 재생'
ms.date: 03/30/2017
helpviewer_keywords:
- playback of media [WPF]
- classes [WPF], MediaPlayer
ms.assetid: 165d47ed-22ce-4ded-aa6a-aa9b7467de87
ms.openlocfilehash: 2e2007525be770186a17cf9d2d42a7c52ba93fba
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956961"
---
# <a name="how-to-play-media-using-a-videodrawing"></a>방법: VideoDrawing을 사용하여 미디어 재생
오디오 또는 비디오 파일을 재생 하려면 <xref:System.Windows.Media.VideoDrawing> 및를 <xref:System.Windows.Media.MediaPlayer>사용 합니다. 미디어를 로드하고 재생하는 방법에는 다음 두 가지가 있습니다. 첫 번째 방법은 <xref:System.Windows.Media.MediaPlayer> 및 <xref:System.Windows.Media.VideoDrawing>를 <xref:System.Windows.Media.VideoDrawing> 자체적으로 사용 하는 것이 고, 두 번째 방법은 <xref:System.Windows.Media.MediaPlayer> 및와 함께 <xref:System.Windows.Media.MediaTimeline> 사용할 고유한를 만드는 것입니다.  
  
> [!NOTE]
> 애플리케이션을 사용하여 미디어를 배포하는 경우 이미지의 경우처럼 미디어 파일을 프로젝트 리소스로 사용할 수 없습니다. 대신 프로젝트 파일에서 미디어 형식을 `Content`로 설정하고 `CopyToOutputDirectory`를 `PreserveNewest` 또는 `Always`로 설정해야 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.VideoDrawing> <xref:System.Windows.Media.MediaPlayer> 및를 사용 하 여 한 번 비디오 파일을 재생 합니다.  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 미디어에 대 한 추가 타이밍 제어를 얻으려면 <xref:System.Windows.Media.MediaTimeline> <xref:System.Windows.Media.MediaPlayer> 및 <xref:System.Windows.Media.VideoDrawing> 개체가 포함 된를 사용 합니다. 에서 <xref:System.Windows.Media.MediaTimeline> 비디오를 반복할지 여부를 지정할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.MediaTimeline> <xref:System.Windows.Media.MediaPlayer> 및 <xref:System.Windows.Media.VideoDrawing> 개체와 함께를 사용 하 여 비디오를 반복 해 서 재생 합니다.  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 을 사용 <xref:System.Windows.Media.MediaTimeline>하는 경우의 <xref:System.Windows.Media.Animation.Clock.Controller%2A> 속성 <xref:System.Windows.Media.MediaClock> 에서 반환 되는 대화형 <xref:System.Windows.Media.Animation.ClockController> 을 사용 하 여의 <xref:System.Windows.Media.MediaPlayer>대화형 메서드 대신 미디어 재생을 제어할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.VideoDrawing>
- [Drawing 개체 개요](drawing-objects-overview.md)
