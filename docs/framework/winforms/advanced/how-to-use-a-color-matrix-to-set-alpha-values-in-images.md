---
title: '방법: 색 매트릭스를 사용하여 이미지에 알파 값 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], using color matrices for semi-transparent
- transparency [Windows Forms], color matrices
- matrices [Windows Forms], alpha values
- bitmaps [Windows Forms], using color matrices for semi-transparent
ms.assetid: a27121e6-f7e9-4c09-84e2-f05aa9d2a1bb
ms.openlocfilehash: fd63380e04eeb4b7ec7ed7d59032309ea7446507
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593163"
---
# <a name="how-to-use-a-color-matrix-to-set-alpha-values-in-images"></a>방법: 색 매트릭스를 사용하여 이미지에 알파 값 설정
합니다 <xref:System.Drawing.Bitmap> 클래스 (에서 상속 되는 <xref:System.Drawing.Image> 클래스) 및 <xref:System.Drawing.Imaging.ImageAttributes> 가져오고 픽셀 값을 설정 하기 위한 기능을 제공 하는 클래스입니다. 사용할 수는 <xref:System.Drawing.Imaging.ImageAttributes> 알파를 수정 하는 클래스는 전체 이미지에 대 한 값 또는 호출할 수 있습니다 합니다 <xref:System.Drawing.Bitmap.SetPixel%2A> 메서드의 <xref:System.Drawing.Bitmap> 개별 픽셀 값을 수정 하는 클래스입니다.  
  
## <a name="example"></a>예제  
 <xref:System.Drawing.Imaging.ImageAttributes> 클래스에 렌더링 하는 동안 이미지를 수정 하는 데 사용할 수 있는 많은 속성이 있습니다. 다음 예제에서는 <xref:System.Drawing.Imaging.ImageAttributes> 개체 어떤의 80%로 모든 알파 값을 설정 하는 합니다. 색 매트릭스를 초기화 하 고 alpha 행렬 0.8에 있는 값을 크기 조정에 설정 하면 됩니다. 색 매트릭스의 주소에 전달 되는 <xref:System.Drawing.Imaging.ImageAttributes.SetColorMatrix%2A> 메서드를 <xref:System.Drawing.Imaging.ImageAttributes> 개체 및 <xref:System.Drawing.Imaging.ImageAttributes> 개체를 전달 하는 <xref:System.Drawing.Graphics.DrawString%2A> 메서드의 <xref:System.Drawing.Graphics> 개체.  
  
 비트맵의 알파 값은 렌더링 하는 동안 어떤의 80%로 변환 됩니다. 이 인해 이미지는 배경색과 혼합 됩니다. 다음 그림에서 알 수 있듯이, 비트맵 이미지가 찾습니다 투명 합니다. 통해 검은 실선이 표시 됩니다.  
  
 ![행렬을 사용 하 여 알파 혼합](./media/image2.png "이미지 2")  
  
 이미지는 배경의 흰색 부분에 이미지를 흰색으로 혼합 되 합니다. 이미지는 검은색 줄과 교차 검은색 이미지 혼합 됩니다.  
  
 [!code-csharp[System.Drawing.AlphaBlending#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.AlphaBlending#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [선 및 채우기 알파 혼합](alpha-blending-lines-and-fills.md)
