---
title: '방법: Visual을 이미지 파일에 인코딩'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- image files [WPF], encoding from visuals
- encoding image formats [WPF]
- visuals [WPF], encoding to an image file
ms.assetid: 2036385b-ea47-4d54-8027-5797f52c8149
ms.openlocfilehash: 193b6a14e404d32bb49d6e0ef3cbd513166bcce2
ms.sourcegitcommit: 43761fcee10aeefcf851ea81cea3f3c691420856
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69545297"
---
# <a name="how-to-encode-a-visual-to-an-image-file"></a>방법: Visual을 이미지 파일에 인코딩
이 예제에서는 <xref:System.Windows.Media.Visual> <xref:System.Windows.Media.Imaging.RenderTargetBitmap> 및를 <xref:System.Windows.Media.Imaging.PngBitmapEncoder>사용 하 여 개체를 이미지 파일로 인코딩하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 는로 <xref:System.Windows.Media.Imaging.BitmapImage> 렌더링되<xref:System.Windows.Media.FormattedText> 는 및를 사용 하 여 만들어집니다. <xref:System.Windows.Media.Imaging.RenderTargetBitmap> <xref:System.Windows.Media.DrawingVisual> 렌더링 된 비트맵은 새 png (이동식 네트워크 <xref:System.Windows.Media.Imaging.BitmapFrame> 그래픽) 파일을 만들기 <xref:System.Windows.Media.Imaging.PngBitmapEncoder> 위해에 추가 되는를 만드는 데 사용 됩니다.  
  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample_Encode.cs#rtbencodeinline1)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample_Encode.vb#rtbencodeinline1)]  
  
 이 <xref:System.Windows.Media.Imaging.PngBitmapEncoder> 예제에서는를 사용 했지만 이미지 파일을 만드는 데 <xref:System.Windows.Media.Imaging.BitmapEncoder> 파생 된 개체를 사용 했을 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.DrawingContext>
- [이미징 개요](imaging-overview.md)
- [Drawing 개체 개요](drawing-objects-overview.md)
- [DrawingVisual 개체 사용](using-drawingvisual-objects.md)
