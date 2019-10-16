---
title: '방법: 색 다시 매핑 변경 테이블 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- color tables [Windows Forms], remapping colors with
- custom colors [Windows Forms], creating with color remap table
- color remap tables [Windows Forms], using
ms.assetid: 977df1ce-8665-42d4-9fb1-ef7f0ff63419
ms.openlocfilehash: 360ec30563ee5001d784dc7c4ccdb50563867c29
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505768"
---
# <a name="how-to-use-a-color-remap-table"></a>방법: 색 다시 매핑 변경 테이블 사용
다시 매핑하는 프로세스 색 다시 매핑 테이블에 따라 이미지의 색을 변환입니다. 색 다시 매핑 테이블을 배열이 <xref:System.Drawing.Imaging.ColorMap> 개체입니다. 각 <xref:System.Drawing.Imaging.ColorMap> 배열의 개체에는 <xref:System.Drawing.Imaging.ColorMap.OldColor%2A> 속성 및 <xref:System.Drawing.Imaging.ColorMap.NewColor%2A> 속성입니다.  
  
 GDI + 이미지를 그립니다, 이미지의 각 픽셀의 이전 색 배열에 비교 됩니다. 이전 색상을 픽셀의 색 일치 하는 경우 해당 새로운 색으로 변경 됩니다. 색이 렌더링에만 변경 됩니다-이미지 자체의 색상 값 (에 저장 된를 <xref:System.Drawing.Image> 또는 <xref:System.Drawing.Bitmap> 개체)는 변경 되지 않습니다.  
  
 매핑된 이미지를 그릴 배열을 초기화할 <xref:System.Drawing.Imaging.ColorMap> 개체입니다. 해당 배열을 전달 합니다 <xref:System.Drawing.Imaging.ImageAttributes.SetRemapTable%2A> 메서드의 <xref:System.Drawing.Imaging.ImageAttributes> 개체를 전달한를 <xref:System.Drawing.Imaging.ImageAttributes> 개체를 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드의 <xref:System.Drawing.Graphics> 개체.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Drawing.Image> RemapInput.bmp 파일에서 개체입니다. 코드는 단일 구성 되는 색 다시 매핑 테이블을 만듭니다 <xref:System.Drawing.Imaging.ColorMap> 개체입니다. <xref:System.Drawing.Imaging.ColorMap.OldColor%2A> 의 속성을 `ColorRemap` 개체가 빨강, 및 <xref:System.Drawing.Imaging.ColorMap.NewColor%2A> 속성이 파란색 합니다. 이미지가 그려지는 번 다시 매핑 없이 한 번 다시 매핑입니다. 다시 매핑 프로세스에서 파란색 빨간색 모든 픽셀을 변경 합니다.  
  
 다음 그림에서는 오른쪽에서 왼쪽의 원래 이미지와 매핑된 이미지를 보여 줍니다.  
  
 ![원본 이미지와 매핑된 이미지를 보여주는 스크린샷.](./media/how-to-use-a-color-remap-table/original-image-remap-colors.png)  
  
 [!code-csharp[System.Drawing.RecoloringImages#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.RecoloringImages#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#31)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [이미지 다시 칠하기](recoloring-images.md)
- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
