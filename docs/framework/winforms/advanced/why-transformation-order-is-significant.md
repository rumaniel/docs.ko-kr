---
title: 변형 순서의 중요성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- transformations [Windows Forms], order significance
ms.assetid: 37d5f9dc-a5cf-4475-aa5d-34d714e808a9
ms.openlocfilehash: 08927ebaa460e19e558dce22f39c13c31f0e49d0
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504912"
---
# <a name="why-transformation-order-is-significant"></a>변형 순서의 중요성
단일 <xref:System.Drawing.Drawing2D.Matrix> 개체는 단일 변환 또는 변환의 시퀀스에 저장할 수 있습니다. 후자 보다 복합 변환을 이라고 합니다. 개별 변환의 매트릭스를 곱하여 복합 변환의 매트릭스를 가져옵니다.  
  
## <a name="composite-transform-examples"></a>복합 변환 예제  
 복합 변환에서 개별 변환의 순서가 중요 합니다. 예를 들어 경우 먼저 회전 다음 크기 조정, 변환, 결과 얻게 다른 보다 먼저 변환 하는 경우 다음 회전 하 고 확장 합니다. GDI +에서 복합 변환 왼쪽에서 오른쪽으로 작성 됩니다. S, R 및 T 인 경우 크기 조정, 회전 및 변환 행렬 각각 다음 제품 SRT (해당 순서 대로)은 복합 변환의 매트릭스는 첫 번째 눈금, 회전, 그런 변환 합니다. 제품에 의해 생성 되는 매트릭스 SRT TR 제품에 의해 생성 되는 매트릭스와에서 다릅니다.  
  
 순서는 중요 한 이유 등 회전 및 배율 조정 변환 좌표계의 원점을 기준으로 수행 되는 경우 원점에서 이동 된 개체 크기 조정 결과 서로 다르게 생성 원점에 중점을 두는 개체를 확장 합니다. 마찬가지로, 개체를 회전 하면 원점에 중점을 두는 원본에서 이동 된 개체를 회전 다른 결과 생성 합니다.  
  
 다음 예제에서는 복합 변환을 형성 하기 위해 크기 조정, 회전 및 변환 (지정 된 순서로)를 결합 합니다. 인수 <xref:System.Drawing.Drawing2D.MatrixOrder.Append> 에 전달 되는 <xref:System.Drawing.Graphics.RotateTransform%2A> 회전 크기 조정은 도메인이 메서드를 나타냅니다. 마찬가지로, 인수 <xref:System.Drawing.Drawing2D.MatrixOrder.Append> 에 전달 되는 <xref:System.Drawing.Graphics.TranslateTransform%2A> 메서드 변환 회전 따르는지를 나타냅니다. <xref:System.Drawing.Drawing2D.MatrixOrder.Append> 및 <xref:System.Drawing.Drawing2D.MatrixOrder.Prepend> 의 멤버는 <xref:System.Drawing.Drawing2D.MatrixOrder> 열거형입니다.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.MiscLegacyTopics#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#21)]  
  
 다음 예에서는 이전 예와 동일한 메서드를 호출 하지만 호출의 순서는 반대입니다. 작업의 결과 순서 회전, 첫 번째 눈금 보다 매우 다른 결과 생성 하는 눈금으로 회전, 차례로 변환 먼저 변환 됩니다.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.MiscLegacyTopics#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#22)]  
  
 복합 변환에서 개별 변환의 순서를 반대로 하는 한 방법은 메서드 호출의 시퀀스의 순서를 반대로 하려면 것입니다. 작업의 순서를 제어 하는 두 번째 방법은 경우 행렬 order 인수를 변경 하려면 다음 예제는 점을 제외 하면 앞의 예제에서와 동일 <xref:System.Drawing.Drawing2D.MatrixOrder.Append> 로 변경 되었습니다 <xref:System.Drawing.Drawing2D.MatrixOrder.Prepend>합니다. 행렬 곱셈 SRT, S, R 및 T 있는 확장에 대 한 행렬 순서로 수행 됩니다, 회전 하 고 각각 변환 합니다. 복합 변환의 순서가 첫 번째 소수 자릿수를 회전 차례로 변환 합니다.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.MiscLegacyTopics#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#23)]  
  
 바로 앞의 예제 결과가 같습니다이 항목의 첫 번째 예의 결과입니다. 메서드 호출의 순서와 행렬 곱셈의 순서를 바꾸었기 때문입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Drawing2D.Matrix>
- [좌표계 및 변형](coordinate-systems-and-transformations.md)
- [관리 GDI+에서 변형 사용](using-transformations-in-managed-gdi.md)
