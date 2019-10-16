---
title: 변형을 사용하여 색의 비율 조정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- transformations [Windows Forms], for scaling colors
- colors [Windows Forms], scaling
ms.assetid: df23c887-7fd6-4b15-ad94-e30b5bd4b849
ms.openlocfilehash: 81c0ddf5b937d604559a9eb1a8b598885546c97f
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504953"
---
# <a name="using-transformations-to-scale-colors"></a>변형을 사용하여 색의 비율 조정
배율 조정 변환 이상의 숫자로 된 네 가지 구성 요소를 곱합니다. 크기 조정 여부를 나타내는 색 매트릭스 항목은 다음 표에 제공 됩니다.  
  
|확장 구성 요소|행렬 항목|  
|----------------------------|------------------|  
|빨강|[0][0]|  
|녹색|[1][1]|  
|파랑|[2][2]|  
|알파|[3][3]|  
  
## <a name="scaling-one-color"></a>한 가지 색을 크기 조정  
 다음 예제에서는 생성 된 <xref:System.Drawing.Image> ColorBars2.bmp 파일에서 개체입니다. 다음 코드를 배율을 각 픽셀의 파랑 구성 요소 이미지에는 2입니다. 변환 된 이미지와 함께 원본 이미지를 그립니다.  
  
 [!code-csharp[System.Drawing.RecoloringImages#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.RecoloringImages#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#41)]  
  
 다음 그림에서는 오른쪽에서 왼쪽의 원본 이미지와 조정 된 이미지를 보여 줍니다.  
  
 ![원래 및 배율 조정 된 색을 비교 하는 스크린샷.](./media/using-transformations-to-scale-colors/four-bar-scale-one-color.png)  
  
 다음 표에서 파란색 크기 조정 전과 후 4 개 막대에 대 한 색 벡터를 나열합니다. 네 번째 색 막대의 파랑 구성 요소에서 0.8 0.6을 참고 합니다. GDI + 결과의 소수 부분에만 유지 때문입니다. 예를 들어 (2)(0.8) 1.6 = 1.6의 소수 부분은 0.6 및 합니다. 소수 부분에만 유지 하 고 결과 [0, 1] 간격에서 항상 확인 합니다.  
  
|원래 색|확장|  
|--------------|------------|  
|(0.4, 0.4, 0.4, 1)|(0.4, 0.4, 0.8, 1)|  
|(0.4, 0.2, 0.2, 1)|(0.4, 0.2, 0.4, 1)|  
|(0.2, 0.4, 0.2, 1)|(0.2, 0.4, 0.4, 1)|  
|(0.4, 0.4, 0.8, 1)|(0.4, 0.4, 0.6, 1)|  
  
## <a name="scaling-multiple-colors"></a>여러 색 비율 조정  
 다음 예제에서는 생성 된 <xref:System.Drawing.Image> ColorBars2.bmp 파일에서 개체입니다. 다음 코드는 이미지의 각 픽셀의 빨강, 녹색 및 파랑 구성 요소를 조정합니다. 빨강 구성 요소는 25%를 축소 하 고, 35%, 녹색 구성 요소는 확장 한 다음 파란색 구성 요소는 50%를 축소 합니다.  
  
 [!code-csharp[System.Drawing.RecoloringImages#42](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#42)]
 [!code-vb[System.Drawing.RecoloringImages#42](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#42)]  
  
 다음 그림에서는 오른쪽에서 왼쪽의 원본 이미지와 조정 된 이미지를 보여 줍니다.  
  
 ![원래 및 배율 조정 된 색을 비교 하는 스크린샷.](./media/using-transformations-to-scale-colors/four-bar-scale-multiple-colors.png)  
  
 다음 표에서 빨강, 녹색 및 파랑 크기 조정 전과 후 4 개 막대에 대 한 색 벡터를 나열합니다.  
  
|원래 색|확장|  
|--------------|------------|  
|(0.6, 0.6, 0.6, 1)|(0.45, 0.39, 0.3, 1)|  
|(0, 1, 1, 1)|(0, 0.65, 0.5, 1)|  
|(1, 1, 0, 1)|(0.75, 0.65, 0, 1)|  
|(1, 0, 1, 1)|(0.75, 0, 0.5, 1)|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Imaging.ColorMatrix>
- <xref:System.Drawing.Imaging.ImageAttributes>
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [이미지 다시 칠하기](recoloring-images.md)
