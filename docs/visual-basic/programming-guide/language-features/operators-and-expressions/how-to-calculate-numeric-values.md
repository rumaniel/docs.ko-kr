---
title: '방법: 숫자 값 (Visual Basic)를 계산 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- operator precedence
- operators [Visual Basic]
- expressions [Visual Basic], numeric
- calculations [Visual Basic], numeric expressions
- precedence [Visual Basic], of operators
- Visual Basic code, operators
- Visual Basic code, expressions
- numeric expressions
ms.assetid: ba6bf43d-bd96-49b8-b1de-4a7797551372
ms.openlocfilehash: 3e367a10a3e703241c7417d3ea17068018becb5a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649730"
---
# <a name="how-to-calculate-numeric-values-visual-basic"></a>방법: 숫자 값 (Visual Basic)를 계산 합니다.
숫자 식 사용 하 여 숫자 값을 계산할 수 있습니다. A *숫자 식* 리터럴, 상수 및 숫자 값을 나타내는 변수를 포함 하는 식과 해당 값에 대해 작동 하는 연산자가 있습니다.  
  
## <a name="calculating-numeric-values"></a>숫자 값 계산  
  
#### <a name="to-calculate-a-numeric-value"></a>숫자 값을 계산 하기  
  
- 숫자 식에 하나 이상의 숫자 리터럴, 상수 및 변수를 결합 합니다. 다음 예에서는 유효한 숫자 식을 보여 줍니다.  
  
     `93.217`  
  
     `System.Math.PI`  
  
     `counter`  
  
     `4 * (67 + i)`  
  
     처음 세 줄에는 리터럴, 상수 및 변수를 보여 줍니다. 각각 자체는 유효한 숫자 식을 형성합니다. 마지막 줄에는 두 개의 리터럴을 사용 하 여 변수 조합을 보여 줍니다.  
  
     숫자 식이 자체적으로 전체 Visual Basic 문을 구성 하지 않는 참고 합니다. 식 문이 종결의 일부로 사용 해야 합니다.  
  
#### <a name="to-store-a-numeric-value"></a>숫자 값을 저장 하려면  
  
- 다음 예제에서는 숫자 식에 변수를 나타내는 값을 할당 하는 대입문을 사용할 수 있습니다.  
  
     [!code-vb[VbVbalrOperators#82](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#82)]  
  
     이전 예제에서는 같음 연산자의 오른쪽에 있는 식의 값 (`=`)를 변수에 할당 됩니다 `j` 연산자의 좌 변에 있는 하므로 `j` 276으로 계산 합니다.  
  
     자세한 내용은 [문](../../../../visual-basic/language-reference/statements/index.md)을 참조하세요.  
  
## <a name="multiple-operators"></a>여러 연산자  
 숫자 식 이상의 연산자를 포함 하는 경우 평가 되는 순서는 연산자 우선 순위 규칙에 따라 결정 됩니다. 식을 위의 예와; 괄호로 묶습니다 있습니다 연산자 우선 순위 규칙을 재정의 하려면 괄호 안의 식이 먼저 계산 됩니다.  
  
#### <a name="to-override-normal-operator-precedence"></a>일반 연산자 우선 순위를 재정의 하려면  
  
- 괄호를 사용 하 여 먼저 수행 하려는 작업을 묶습니다. 다음 예제에서는 피연산자와 연산자를 사용 하 여 두 개의 서로 다른 결과 보여 줍니다.  
  
     [!code-vb[VbVbalrOperators#83](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#83)]  
  
     앞의 예제에 대 한 계산에 `j` 더하기 연산자를 수행 합니다. (`+`) 첫 번째 때문에 괄호로 `(67 + i)` 일반 우선 순위 및 할당 된 값을 재정의 `j` 은 276 (4 회 69). 에 대 한 계산 `k` 일반 우선 순위 연산자 수행 (`*` 하기 전에 `+`), 및 할당 된 값 `k` 은 270 (268 + 2).  
  
     자세한 내용은 [Visual Basic의 연산자 우선 순위](../../../../visual-basic/language-reference/operators/operator-precedence.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [연산자 및 식](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [값 비교](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)
- [문(C++)](../../../../visual-basic/language-reference/statements/index.md)
- [Visual Basic에서의 연산자 우선 순위](../../../../visual-basic/language-reference/operators/operator-precedence.md)
- [산술 연산자](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [연산자의 효율적 결합](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
