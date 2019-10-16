---
title: GDI+에서 이미지 그리기, 위치 지정 및 복제
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- raster images [Windows Forms]
- images [Windows Forms], positioning
- drawing [Windows Forms], images
- drawing [Windows Forms], raster images
- images [Windows Forms], cloning
- images [Windows Forms], drawing
- GDI+, drawing images
- GDI+, cloning images
- GDI+, positioning images
ms.assetid: 09f0c07a-19c0-43b4-90a2-862a10545ce8
ms.openlocfilehash: b5f98e7bdef9ff8ed0a4cd0e040cb92a31f30503
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61756925"
---
# <a name="drawing-positioning-and-cloning-images-in-gdi"></a>GDI+에서 이미지 그리기, 위치 지정 및 복제
사용할 수는 <xref:System.Drawing.Bitmap> 로드 래스터 이미지를 표시 하는 클래스를 사용할 수는 <xref:System.Drawing.Imaging.Metafile> 클래스를 로드 하 고 벡터 이미지를 표시 합니다. <xref:System.Drawing.Bitmap> 하 고 <xref:System.Drawing.Imaging.Metafile> 클래스에서 상속 된 <xref:System.Drawing.Image> 클래스. 인스턴스의 벡터 이미지를 표시 하려면 필요 합니다 <xref:System.Drawing.Graphics> 클래스 및 <xref:System.Drawing.Imaging.Metafile>합니다. 인스턴스의 래스터 이미지를 표시 하려면 필요 합니다 <xref:System.Drawing.Graphics> 클래스 및 <xref:System.Drawing.Bitmap>합니다. 인스턴스의 <xref:System.Drawing.Graphics> 클래스를 제공 합니다 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드를 수신 하는 합니다 <xref:System.Drawing.Imaging.Metafile> 또는 <xref:System.Drawing.Bitmap> 인수로.  
  
## <a name="file-types-and-cloning"></a>파일 형식 및 복제  
 다음 코드 예제를 생성 하는 방법을 보여 줍니다는 <xref:System.Drawing.Bitmap> Climber.jpg 파일에서 비트맵을 표시 합니다. 이미지의 왼쪽 위 모퉁이 대 한 대상 점 (10, 10)에 두 번째 및 세 번째 매개 변수를 지정 합니다.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#11)]  
  
 다음 그림에서는 이미지를 보여 줍니다.  
  
 ![샘플 이미지](./media/aboutgdip03-art04.gif "AboutGdip03_Art04")  
  
 생성할 수 있습니다 <xref:System.Drawing.Bitmap> 다양 한 그래픽 개체 파일 형식: BMP, GIF, JPEG, EXIF, PNG, TIFF 및 아이콘  
  
 다음 코드 예제를 생성 하는 방법을 보여 줍니다 <xref:System.Drawing.Bitmap> 다양 한 파일 형식에서에서 개체 및 다음 비트맵을 표시 합니다.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#12)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#12)]  
  
 <xref:System.Drawing.Bitmap> 클래스를 제공 된 <xref:System.Drawing.Bitmap.Clone%2A> 의 기존 복사본을 사용할 수 있는 메서드 <xref:System.Drawing.Bitmap>. <xref:System.Drawing.Bitmap.Clone%2A> 메서드에 복사 하려는 원본 비트맵의 일부를 지정 하는 데 사용할 수 있는 소스 사각형 매개 변수가 있습니다. 다음 코드 예제에서는 만드는 방법을 보여 줍니다.는 <xref:System.Drawing.Bitmap> 기존의 위쪽 절반을 복제 하 여 <xref:System.Drawing.Bitmap>입니다. 다음 두 이미지를 그립니다.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#13](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#13)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#13](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#13)]  
  
 다음 그림에서는 두 개의 이미지를 보여 줍니다.  
  
 ![Cropping](./media/aboutgdip03-art05.gif "AboutGdip03_Art05")  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [방법: 그리는 데 필요한 그래픽 개체 만들기](how-to-create-graphics-objects-for-drawing.md)
- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
