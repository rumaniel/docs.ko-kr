---
title: '방법: 색 전단'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [Windows Forms], transforming with color matrices
- colors [Windows Forms], shearing
ms.assetid: 0a424171-5b8b-45c4-afef-e9720a6c3e22
ms.openlocfilehash: b390caf644b86de0001387b2c3f41503fd34759a
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593199"
---
# <a name="how-to-shear-colors"></a>방법: 색 전단
기울이기 증가 또는 색 구성 요소를 다른 색 구성 요소에 비례 하는 양을 감소 합니다. 예를 들어 빨강 구성 요소를 0.5 파랑 구성 요소 값 만큼 늘리는 변환입니다. 이러한 변환에서 (0.2, 0.5, 1) 색 (0.7, 0.5, 1) 될 것입니다. 새 빨강 구성 요소는 0.2 + (1/2)(1) 0.7입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 생성 된 <xref:System.Drawing.Image> ColorBars4.bmp 파일에서 개체입니다. 다음 코드는 각 픽셀 이미지에 이전 단락에 설명 된 기울이기 변환을 적용 됩니다.  
  
 다음 그림에서는 오른쪽에서 왼쪽의 원래 이미지와 기울이기가 적용 된 이미지를 보여 줍니다. 
  
 ![색이 지정 된 줄무늬-side-by-side 원본 이미지와 기울이기가 적용 된 이미지를 보여 주는 사용 하 여 두 개의 사각형입니다.](./media/how-to-shear-colors/original-image-sheared-image.png)  
  
 다음 표에서 전과 기울이기 변환 후 4 개 막대에 대 한 색 벡터를 나열합니다.  
  
|원래 색|전단|  
|--------------|-------------|  
|(0, 0, 1, 1)|(0.5, 0, 1, 1)|  
|(0.5, 1, 0.5, 1)|(0.75, 1, 0.5, 1)|  
|(1, 1, 0, 1)|(1, 1, 0, 1)|  
|(0.4, 0.4, 0.4, 1)|(0.6, 0.4, 0.4, 1)|  
  
 [!code-csharp[System.Drawing.Misc3#9](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Misc3/CS/Form1.cs#9)]
 [!code-vb[System.Drawing.Misc3#9](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Misc3/VB/Form1.vb#9)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다. 대체 `ColorBars.bmp` 있는 이미지 이름 및 경로 시스템에서 사용할 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Imaging.ColorMatrix>
- <xref:System.Drawing.Imaging.ImageAttributes>
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [이미지 다시 칠하기](recoloring-images.md)
