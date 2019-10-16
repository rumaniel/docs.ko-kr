---
title: GDI+에서 이미지 자르기 및 배율 조정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- GDI+, scaling images
- GDI+, cropping images
- images [Windows Forms], cropping
- compressing data [Windows Forms], images
- images [Windows Forms], expansion
- images [Windows Forms], scaling
- rectangles [Windows Forms], source
- rectangles [Windows Forms], destination
- images [Windows Forms], compression
ms.assetid: ad5daf26-005f-45bc-a2af-e0e97777a21a
ms.openlocfilehash: c3cdb06e99770808461f9266fb5f07df9074149b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769501"
---
# <a name="cropping-and-scaling-images-in-gdi"></a>GDI+에서 이미지 자르기 및 배율 조정
사용할 수는 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드는 <xref:System.Drawing.Graphics> 그리고 이미지 벡터 및 래스터 이미지를 배치 하는 클래스입니다. <xref:System.Drawing.Graphics.DrawImage%2A> 오버 로드 된 메서드인 이므로 여러 가지 인수를 사용 하 여 제공할 수 있습니다.  
  
## <a name="drawimage-variations"></a>DrawImage 변형  
 변형 된 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드는 수신를 <xref:System.Drawing.Bitmap> 및 <xref:System.Drawing.Rectangle>합니다. 사각형 그리기 작업에 대 한 대상을 지정합니다. 즉, 이미지를 그릴 사각형을 지정 합니다. 대상 사각형의 크기는 원본 이미지의 크기와 다른 경우 대상 사각형에 맞게 이미지 크기가 조정 됩니다. 다음 코드 예제에는 세 번 동일한 이미지를 그리는 방법을 보여 줍니다: 크기 조정 없음 번, 확장을 사용 하 여 한 번 및 압축을 사용 하 여 한 번:  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#31)]  
  
 다음 그림에서는 세 가지 그림을 보여 줍니다.  
  
 ![Scaling](./media/aboutgdip03-art06.gif "AboutGdip03_Art06")  
  
 일부 변형 된 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드는 대상 사각형 매개 변수 뿐 아니라 소스 사각형 매개 변수입니다. 그릴 원본 이미지의 부분을 지정 하는 소스 사각형 매개 변수입니다. 대상 사각형에는 이미지의 해당 부분을 그릴 사각형을 지정 합니다. 대상 사각형의 크기가 소스 사각형의 크기와 다른 경우에 그림 대상 사각형에 맞게 크기가 조정 됩니다.  
  
 다음 코드 예제를 생성 하는 방법을 보여 줍니다는 <xref:System.Drawing.Bitmap> Runner.jpg 파일에서 합니다. 확장에서 사용 하 여 전체 이미지를 그릴 (0, 0). 다음 이미지의 작은 부분을 두 번 그려집니다: 압축을 사용 하 여 한 번 및 확장을 사용 하 여 한 번입니다.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#32)]  
  
 다음 그림에는 실제 크기의 이미지 및 압축 및 확장 된 이미지 부분을 보여 줍니다.  
  
 ![자르기 및 배율 조정](./media/aboutgdip03-art07.gif "AboutGdip03_Art07")  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
