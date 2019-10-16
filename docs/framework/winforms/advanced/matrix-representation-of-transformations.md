---
title: 변환에 대한 매트릭스 표현
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- composite transformations
- transformations [Windows Forms], linear
- matrices
- translations in matrix representation
- transformations [Windows Forms], composite
- vectors
- linear transformations
- transformations [Windows Forms], matrix representation of
- transformations [Windows Forms], translation
- affine transformations
ms.assetid: 0659fe00-9e0c-41c4-9118-016f2404c905
ms.openlocfilehash: 24da407de24a924a68466e4301cc3f4a74cb2e94
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044247"
---
# <a name="matrix-representation-of-transformations"></a>변환에 대한 매트릭스 표현
M × n 행렬은 m 행과 n 개의 열로 정렬 된 숫자 집합입니다. 다음 그림에서는 여러 행렬을 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art04.gif "AboutGdip05_art04")  
  
 개별 요소를 추가 하 여 동일한 크기의 두 행렬을 추가할 수 있습니다. 다음 그림에서는 행렬 추가의 두 가지 예를 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art05.gif "AboutGdip05_art05")  
  
 M × n 매트릭스는 n × p 매트릭스를 곱할 수 있으며 결과는 m × p 매트릭스입니다. 첫 번째 행렬의 열 수는 두 번째 행렬의 행 수와 같아야 합니다. 예를 들어 4 × 2 행렬을 2 × 3 매트릭스에 곱하여 4 × 3 행렬을 생성할 수 있습니다.  
  
 평면의 점과 행렬의 행 및 열을 벡터로 간주할 수 있습니다. 예를 들어 (2, 5)는 두 개의 구성 요소가 있는 벡터이 고 (3, 7, 1)는 세 가지 구성 요소가 포함 된 벡터입니다. 두 벡터의 내적은 다음과 같이 정의 됩니다.  
  
 (a, b) • (c, d) = ac + bd  
  
 (a, b, c) • (d, e, f) = ad + be + cf  
  
 예를 들어 (2, 3) 및 (5, 4)의 도트 제품은 (2) (5) + (3) (4) = 22입니다. (2, 5, 1) 및 (4, 3, 1)의 도트 제품은 (2) (4) + (5) (3) + (1) (1) = 24입니다. 두 벡터의 점 곱을 다른 벡터가 아닌 숫자입니다. 또한 두 벡터의 구성 요소 수가 동일한 경우에만 도트 곱을 계산할 수 있습니다.  
  
 (I, j)는 i 번째 행과 jth 열의 행렬 A에 있는 항목입니다. 예를 들어 (3, 2)는 세 번째 행과 두 번째 열에 있는 행렬 A의 항목입니다. A, B 및 C는 매트릭스가 고 AB = C 라고 가정 합니다. C의 항목은 다음과 같이 계산 됩니다.  
  
 C (i, j) = (행 i의 i) • (B의 열 j)  
  
 다음 그림에서는 행렬 곱셈의 몇 가지 예를 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art06.gif "AboutGdip05_art06")  
  
 평면의 점을 1 × 2 행렬로 간주 하는 경우 2 × 2 매트릭스를 곱하여 해당 점을 변형할 수 있습니다. 다음 그림에서는 점 (2, 1)에 적용 되는 여러 변환을 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art07.gif "AboutGdip05_art07")  
  
 위의 그림에 표시 된 모든 변환은 선형 변환입니다. 변환과 같은 다른 변환은 선형이 아니므로 2 × 2 × 2 × 2 × 2 × 2 행렬로 표현할 수 없습니다. Point (2, 1)로 시작 하 고, 90도 회전 하 고, x 방향으로 3 단위를 변환 하 고, y 방향으로 4 단위를 변환 한다고 가정 합니다. 행렬 곱하기를 사용 하 고 행렬 추가를 사용 하 여이를 수행할 수 있습니다.  
  
 ![Transformations](./media/aboutgdip05-art08.gif "AboutGdip05_art08")  
  
 선형 변환 (2 × 2 매트릭스가 곱하기) 다음에 변환 (1 × 2 행렬 추가)을 수행 하는 것을 상관 변환 이라고 합니다. 행렬 쌍 (선형 부분에 대해 1 개, 변환에 대해 하나)에 상관 변환을 저장 하는 대신 3 × 3 행렬에 전체 변환을 저장 합니다. 이 작업을 수행 하려면 평면의 점이 더미 3 좌표를 사용 하 여 1 × 3 행렬에 저장 되어야 합니다. 일반적인 방법은 세 번째 좌표를 모두 1로 설정 하는 것입니다. 예를 들어 점 (2, 1)은 행렬 [2 1 1]로 표시 됩니다. 다음 그림에서는 단일 3 × 3 매트릭스의 곱셈으로 표현 되는 관계 변환 (90도 회전, y 방향으로 4 개 단위)을 표시 합니다.  
  
 ![Transformations](./media/aboutgdip05-art09.gif "AboutGdip05_art09")  
  
 앞의 예제에서 point (2, 1)는 점 (2, 6)에 매핑됩니다. 3 × 3 행렬의 세 번째 열에는 숫자 0, 0, 1이 포함 됩니다. 이는 항상 상관 변환의 3 × 3 행렬의 경우입니다. 중요 한 숫자는 열 1과 2에 있는 6 개의 숫자입니다. 행렬의 왼쪽 위 2 × 2 부분은 변환의 선형 부분을 나타내고 세 번째 행의 처음 두 항목은 변환을 나타냅니다.  
  
 ![Transformations](./media/aboutgdip05-art10.gif "AboutGdip05_art10")  
  
 Gdi +에서 <xref:System.Drawing.Drawing2D.Matrix> 개체에 상관 변환을 저장할 수 있습니다. 나타내는 3x3 유사 변형 매트릭스의 세 번째 열은 항상 때문에 (0, 0, 1)을 생성 하는 경우 처음 두 열에 있는 6 개의 숫자만 지정를 <xref:System.Drawing.Drawing2D.Matrix> 개체입니다. 문은 `Matrix myMatrix = new Matrix(0, 1, -1, 0, 3, 4)` 앞의 그림에 표시 된 행렬을 생성 합니다.  
  
## <a name="composite-transformations"></a>합성 변형  
 복합 변환에는 뒤에 다른 하나는 변환의 시퀀스입니다. 행렬 및 다음과 같은 변환을 고려 합니다.  
  
|||  
|-|-|  
|행렬|90도 회전|  
|행렬 B|X 방향으로 2 배 확장|  
|행렬 C|Y 방향의 3 단위|  
  
 점 (2, 1)부터 시작 하는 경우-행렬 [1 1 2]로 표시-및 C, 점 (2, 1)에 나열 된 순서로 세 가지 변환 될 예정 후 A, B로 곱합니다.  
  
 [2 1 1]ABC = [-2 5 1]  
  
 대신 복합 변환의 세 부분에서 세 가지 별도 행렬을 저장 하는 보다에 곱할 수 B 및 C 함께 전체 복합 변환을 저장 하는 단일 3 × 3 행렬을 가져옵니다. ABC 가정 = 4. 그런 다음, D를 곱하면 A, B, C 곱하면와 동일한 결과 제공  
  
 [2 1 1]D = [-2 5 1]  
  
 다음 그림에서는 A, B, C 및 D. 행렬을 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art12.gif "AboutGdip05_art12")  
  
 개별 변환 행렬을 곱하여 복합 변환의 매트릭스를 구성할 수는 팩트 관계 변형 시퀀스는 단일에서 저장할 수 있다는 의미 <xref:System.Drawing.Drawing2D.Matrix> 개체입니다.  
  
> [!CAUTION]
> 복합 변환의 순서가 중요 합니다. 일반적으로 회전, 크기 조정을 차례로 다릅니다 변환으로 크기 조정, 회전, 그런 다음 변환 합니다. 마찬가지로 행렬 곱셈의 순서가 중요 합니다. 일반적으로 ABC 아닙니다 백업와 동일 합니다.  
  
 <xref:System.Drawing.Drawing2D.Matrix> 클래스는 복합 변환을 구성 하는 여러 가지 방법을 제공: <xref:System.Drawing.Drawing2D.Matrix.Multiply%2A>를 <xref:System.Drawing.Drawing2D.Matrix.Rotate%2A>, <xref:System.Drawing.Drawing2D.Matrix.RotateAt%2A>를 <xref:System.Drawing.Drawing2D.Matrix.Scale%2A>를 <xref:System.Drawing.Drawing2D.Matrix.Shear%2A>, 및 <xref:System.Drawing.Drawing2D.Matrix.Translate%2A>합니다. 다음 예제에서는 먼저 30도 회전 하 고 2 y 방향의 배율을 5 개 단위 x 방향으로 변환 하는 복합 변환의 행렬을 만듭니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.CoordinateSystems#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#11)]  
  
 다음 그림에서는 행렬을 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art13.gif "AboutGdip05_art13")  
  
## <a name="see-also"></a>참고자료

- [좌표계 및 변형](coordinate-systems-and-transformations.md)
- [관리 GDI+에서 변형 사용](using-transformations-in-managed-gdi.md)
