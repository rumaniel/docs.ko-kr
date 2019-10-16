---
title: '방법: 색 매트릭스를 사용하여 단색으로 변환'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- image colors [Windows Forms], transforming
- color matrices [Windows Forms], using
ms.assetid: 44df4556-a433-49c0-ac0f-9a12063a5860
ms.openlocfilehash: 2df74e022b842f7e5c9ff80f6aeddfce51af5eab
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505831"
---
# <a name="how-to-use-a-color-matrix-to-transform-a-single-color"></a>방법: 색 매트릭스를 사용하여 단색으로 변환
GDI +를 제공 합니다 <xref:System.Drawing.Image> 고 <xref:System.Drawing.Bitmap> 저장 및 이미지 조작을 위한 클래스입니다. <xref:System.Drawing.Image> 및 <xref:System.Drawing.Bitmap> 개체는 32 비트 숫자도 각 픽셀의 색을 저장 합니다. 각각 8 비트가 빨간색, 녹색, 파랑 및 알파에 대 한 합니다. 각 네 가지 구성 요소에는 0부터 농도가 없음을 나타내고 255 전체 강도 나타내는 0부터 255 까지의 숫자입니다. 색의 투명도 지정 하는 알파 구성 요소: 0은 완전히 투명 하 고 255는 완전히 불투명 한 합니다.  
  
 색 벡터는 (빨강, 녹색, 파란색, 알파) 형식의 4 중 튜플입니다. 예를 들어 색 벡터 (0, 255, 0, 255)를 빨강 및 파랑, 녹색 농도가 불투명 한 색을 나타냅니다.  
  
 색을 나타내는 다른 규칙에 대 한 전체 강도로 돌아가는 숫자 1을 사용 합니다. 해당 규칙을 사용 하 여 이전 단락에서 설명한 색을 표시 벡터 (0, 1, 0, 1). GDI + 1의 규칙으로 사용 전체 강도로 돌아가는 색 변환을 수행 하는 경우.  
  
 4x4 행렬으로 색 벡터를 곱하여 색 벡터로 선형 변환 (회전, 크기 조정 등)를 적용할 수 있습니다. 그러나 비선형 변환을 수행 하는 4x4 행렬을 사용할 수 없습니다. 각 색 벡터에 더미 다섯 번째 좌표 (예를 들어, 숫자 1)을 추가 하는 경우 변환이 선형 조합을 적용할 5 × 5 행렬을 사용할 수 있습니다. 선형 번역 뒤에 변환으로 구성 된 변환에는 3x3 유사 변형을 라고 합니다.  
  
 예를 들어, (0.2, 0.0, 0.4, 1.0) 색을 사용 하 여 시작한 다음 변환을 적용 하려면:  
  
1. Double 빨강 구성 요소  
  
2. 0\.2 빨강, 녹색 및 파랑 구성 요소에 추가  
  
 나열 된 순서로 다음 행렬 곱셈 변환이 수행 합니다.  
  
 ![곱하기 변환 행렬의 스크린샷입니다.](./media/how-to-use-a-color-matrix-to-transform-a-single-color/multiplication-color-matrix.gif)
  
 색 매트릭스의 요소는 행과 열으로 (0부터 시작) 인덱싱됩니다. 예를 들어, 다섯 번째 행과 M 행렬의 세 번째 열에 있는 항목은 M [4] [2]에 의해 표시 됩니다.  
  
 (다음 그림에 표시) 5 × 5 항등 매트릭스 대각선에는 1 및 0으로 다른 곳에 있습니다. 항등 매트릭스를 색 벡터를 곱하면 색 벡터 변경 되지 않습니다. 색 변환 행렬을 형성 하는 편리한 방법을 항등 매트릭스로 시작 하 여 필요한 변환을 생성 하는 약간 변경 됩니다.  
  
 ![색 변환에 대 한 5x5 항등 매트릭스의 스크린샷.](./media/how-to-use-a-color-matrix-to-transform-a-single-color/5x5-identity-matrix-color-transformation.gif)  
  
 행렬 및 변환의 자세한 내용은 참조 하세요. [좌표계 및 변형](coordinate-systems-and-transformations.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 모든 하나의 색 (예: 0.2, 0.0, 0.4, 1.0)이 고 이전 단락에 설명 된 변환을 적용 하는 이미지입니다.  
  
 다음 그림에서는 오른쪽에서 왼쪽의 원래 이미지와 변환 된 이미지를 보여 줍니다.  
  
 ![왼쪽 및 오른쪽에 밝은 자홍 사각형에 자주색 사각형입니다.](./media/how-to-use-a-color-matrix-to-transform-a-single-color/color-transformation.png)  
  
 다음 예제 코드에서는 다음 단계를 사용 하 여 다시 칠하기는 수행:  
  
1. 초기화는 <xref:System.Drawing.Imaging.ColorMatrix> 개체입니다.  
  
2. 만들기는 <xref:System.Drawing.Imaging.ImageAttributes> 개체를 전달 합니다 <xref:System.Drawing.Imaging.ColorMatrix> 개체를 <xref:System.Drawing.Imaging.ImageAttributes.SetColorMatrix%2A> 메서드의 <xref:System.Drawing.Imaging.ImageAttributes> 개체입니다.  
  
3. 전달 합니다 <xref:System.Drawing.Imaging.ImageAttributes> 개체를 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드의 <xref:System.Drawing.Graphics> 개체입니다.  
  
 [!code-csharp[System.Drawing.RecoloringImages#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.RecoloringImages#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [이미지 다시 칠하기](recoloring-images.md)
- [좌표계 및 변형](coordinate-systems-and-transformations.md)
