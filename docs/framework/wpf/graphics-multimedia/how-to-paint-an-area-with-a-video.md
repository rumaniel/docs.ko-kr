---
title: '방법: 비디오로 영역 칠하기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- painting with a video [WPF]
- video [WPF], painting with
- brushes [WPF], painting with a video
ms.assetid: 04dd6600-4a6e-4b43-a93e-21cce7dfbcb8
ms.openlocfilehash: be09d1310847cd7214ea795a704c25d994f07b7a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61921734"
---
# <a name="how-to-paint-an-area-with-a-video"></a>방법: 비디오로 영역 칠하기
이 예제에서는 미디어를 사용 하 여 영역을 그리는 방법을 보여 줍니다. 미디어를 사용 하 여 영역을 그리는 방법 중 하나를 사용 하는 것을 <xref:System.Windows.Controls.MediaElement> 와 함께 <xref:System.Windows.Media.VisualBrush>입니다. 사용 하 여는 <xref:System.Windows.Controls.MediaElement> 로드 하 고 재생할 미디어를 사용 하 여 설정 하는 <xref:System.Windows.Media.VisualBrush.Visual%2A> 의 속성을 <xref:System.Windows.Media.VisualBrush>. 사용할 수는 <xref:System.Windows.Media.VisualBrush> 로드 된 미디어를 사용 하 여 영역을 그리는 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 <xref:System.Windows.Controls.MediaElement> 및 <xref:System.Windows.Media.VisualBrush> 그릴 합니다 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 의 <xref:System.Windows.Controls.TextBlock> 비디오를 사용 하 여 컨트롤입니다. 설정 하는이 예제는 <xref:System.Windows.Controls.MediaElement.IsMuted%2A> 의 속성을 <xref:System.Windows.Controls.MediaElement> 에 `true` 사운드가 재생 되지 않습니다 있도록 합니다.  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundinline)]
 [!code-xaml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundinline)]  
  
## <a name="example"></a>예제  
 때문에 <xref:System.Windows.Media.VisualBrush> 에서 상속 되는 <xref:System.Windows.Media.TileBrush> 클래스는 몇 가지 바둑판식 배열 모드입니다. 설정 하 여는 <xref:System.Windows.Media.TileBrush.TileMode%2A> 의 속성을 <xref:System.Windows.Media.VisualBrush> 하 <xref:System.Windows.Media.TileMode.Tile> 설정 하 고 해당 <xref:System.Windows.Media.TileBrush.Viewport%2A> 사용자가 칠하고 있는 영역 보다 작은 값으로 속성에는 바둑판식 배열된 패턴을 만들 수 있습니다.  
  
 다음 예제는 점을 제외 하면 이전 예제와 동일 합니다 <xref:System.Windows.Media.VisualBrush> 비디오에서 패턴을 생성 합니다.  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-xaml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundtiledinline)]  
  
 응용 프로그램에 미디어 파일과 같은 콘텐츠 파일을 추가 하는 방법에 대 한 정보를 참조 하세요. [WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일](../app-development/wpf-application-resource-content-and-data-files.md)합니다. 미디어 파일을 추가한 경우 리소스 파일 아니라 콘텐츠 파일로 추가 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.VisualBrush>
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
- [TileBrush 개요](tilebrush-overview.md)
- [멀티미디어 개요](multimedia-overview.md)
