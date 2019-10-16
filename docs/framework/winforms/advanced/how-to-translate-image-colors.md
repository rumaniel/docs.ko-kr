---
title: '방법: 이미지 색 변환'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- bitmaps [Windows Forms], changing colors
- images [Windows Forms], changing colors
- image colors [Windows Forms]
ms.assetid: 2106fb9a-4d60-4dcf-9220-9f189a6c4d19
ms.openlocfilehash: fb9ec30c06740214b8dc6b65d32eba4e2920c89b
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592938"
---
# <a name="how-to-translate-image-colors"></a>방법: 이미지 색 변환
번역 네 가지 구성 요소 중 하나 이상에 값을 추가합니다. 번역을 나타내는 색 매트릭스 항목은 다음 표에 제공 됩니다.  
  
|변환 구성 요소|행렬 항목|  
|--------------------------------|------------------|  
|빨강|[4][0]|  
|녹색|[4][1]|  
|파랑|[4][2]|  
|알파|[4][3]|  
  
## <a name="example"></a>예제  
 다음 예제에서는 생성 된 <xref:System.Drawing.Image> ColorBars.bmp 파일에서 개체입니다. 다음 코드는 이미지의 각 픽셀의 빨강 구성 요소를 0.75를 추가합니다. 변환 된 이미지와 함께 원본 이미지를 그립니다.  
  
 다음 그림에서는 오른쪽에서 왼쪽의 원래 이미지와 변환 된 이미지를 보여 줍니다.  
  
 ![원본 및 변환 된 이미지의 스크린샷입니다.](./media/how-to-translate-image-colors/original-image-translate-colors.png)  
  
 다음 표에서 빨간색 번역 전후 4 개 막대에 대 한 색 벡터를 나열합니다. Note 색 구성 요소에 대 한 최대값은 1 이므로 두 번째 행의 빨강 구성 요소 변경 되지 않습니다. (마찬가지로 색 구성 요소에 대 한 최소값은 0입니다.)  
  
|원래 색|번역 언어|  
|--------------|----------------|  
|검은색 (0, 0, 0, 1)|(0.75, 0, 0, 1)|  
|빨강 (1, 0, 0, 1)|(1, 0, 0, 1)|  
|녹색 (0, 1, 0, 1)|(0.75, 1, 0, 1)|  
|(0, 0, 1, 1) 파랑|(0.75, 0, 1, 1)|  
  
 [!code-csharp[System.Drawing.RecoloringImages#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.RecoloringImages#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다. 대체 `ColorBars.bmp` 있는 이미지 파일 이름 및 경로 시스템에서 사용할 수 있는 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Imaging.ColorMatrix>
- <xref:System.Drawing.Imaging.ImageAttributes>
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [이미지 다시 칠하기](recoloring-images.md)
