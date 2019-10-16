---
title: '방법: MediaElement 제어(재생, 일시 중지, 정지, 볼륨 및 속도)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- playback of media [WPF], controlling
- controlling playback of media [WPF]
- multimedia [WPF], controlling playback of media
- media [WPF], controlling playback of
ms.assetid: 6885a730-e054-4c16-8c1e-ffe17b1f7c32
ms.openlocfilehash: cde7c32b48dff3d6d054e700b2f95771ba3b3773
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930157"
---
# <a name="how-to-control-a-mediaelement-play-pause-stop-volume-and-speed"></a>방법: MediaElement 제어(재생, 일시 중지, 정지, 볼륨 및 속도)
다음 예제에서는를 <xref:System.Windows.Controls.MediaElement>사용 하 여 미디어 재생을 제어 하는 방법을 보여 줍니다. 이 예에서는 미디어에서 재생, 일시 중지, 중지 및 건너뛰기를 수행할 뿐만 아니라 볼륨 및 속도 비율을 조정할 수 있는 간단한 미디어 플레이어를 만듭니다.  
  
## <a name="example"></a>예제  
 아래 코드는 UI를 만듭니다.  
  
> [!NOTE]
> 미디어 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 를 대화형 <xref:System.Windows.Controls.MediaElement> 으로 중지, 일시 `Manual` 중지 및 재생할 수 있도록의 속성은로 설정 되어야 합니다.  
  
 [!code-xaml[MediaGallery_snip#MediaElementExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml#mediaelementexamplewholepage)]  
  
## <a name="example"></a>예제  
 아래 코드는 샘플 UI 컨트롤의 기능을 구현 합니다. <xref:System.Windows.Controls.MediaElement.Play%2A>, 및메서드<xref:System.Windows.Controls.MediaElement.Stop%2A> 는 각각 미디어를 재생, 일시 중지 및 중지 하는 데 사용 됩니다. <xref:System.Windows.Controls.MediaElement.Pause%2A> 의 속성 <xref:System.Windows.Controls.MediaElement.Position%2A> 을 변경 하면 미디어를 건너뛸 수있습니다.<xref:System.Windows.Controls.MediaElement> 마지막으로 <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> 및 속성은 미디어의 볼륨 및 재생 속도를 조정 하는 데 사용 됩니다. <xref:System.Windows.Controls.MediaElement.Volume%2A>  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaElementExample.xaml.cs#codebehindmediaelementexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml.vb#codebehindmediaelementexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- [Storyboard를 사용하여 MediaElement 제어](how-to-control-a-mediaelement-by-using-a-storyboard.md)
