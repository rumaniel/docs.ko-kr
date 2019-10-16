---
title: 값 비교(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], comparing values
- Visual Basic code, operators
- Visual Basic code, expressions
- comparison operators [Visual Basic], comparing expressions
- numeric expressions
- operators [Visual Basic], comparison
- expressions [Visual Basic], comparing
ms.assetid: 60da0c76-9458-4afc-97e9-44a7939c064c
ms.openlocfilehash: 270b226d0a1aa7d08721e6f9ed36d68492685af3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61864393"
---
# <a name="value-comparisons-visual-basic"></a>값 비교(Visual Basic)
숫자 변수 값을 비교 하는 식을 생성 하려면 비교 연산자를 사용할 수 있습니다. 이러한 식은 반환을 `Boolean` 비교가 true 인지에 따라 값 false입니다. 이러한 식의 예는 다음과 같습니다.  
  
 `45 > 26`  
  
 `26 > 45`  
  
 첫 번째 식의 결과가 `True`이므로 45 26 보다 큽니다. 두 번째 예에서는 `False`이므로 26 45 보다 크지 않습니다.  
  
 또한이 방식으로 숫자 식을 비교할 수 있습니다. 비교 식 자체는 다음 예제와 같이 복잡 한 식 수 있습니다.  
  
 `x / 45 * (y +17) >= System.Math.Sqrt(z) / (p - (x * 16))`  
  
 이전 복잡 한 식에는 리터럴, 변수 및 함수 호출이 포함 됩니다. 비교 연산자의 양쪽에 있는 식을 평가 하 고 결과 값을 사용 하 여 그런 비교는 `>=` 비교 연산자입니다. 왼쪽에 있는 식의 값 보다 크면 이거나 오른쪽 식의 값과 같으면는 전체 식을 계산 하는 경우 `True`이 고, 그렇지 않으면 결과가 `False`합니다.  
  
 값을 비교 하는 식에서 가장 흔히 사용 됩니다 `If...Then` 다음 예제와 같이 생성 합니다.  
  
 [!code-vb[VbVbalrOperators#84](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#84)]  
  
 `=` 기호는 대입 연산자 뿐만 아니라 비교 연산자입니다. 비교 연산자로 사용 하는 다음 예제에서와 같이 왼쪽의 값이 오른쪽의 값과 같으면 여부를 평가 합니다.  
  
 [!code-vb[VbVbalrOperators#85](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#85)]  
  
 비교 식을 어디서 나 사용할 수도 있습니다는 `Boolean` 값이 필요한, 예:는 `If`, `While`, `Loop`, 또는 `ElseIf` 문을에 할당 하거나 값을 전달 하는 경우 또는 `Boolean` 변수입니다. 다음 예제에서는 비교 식에서 반환 된 값에 할당 되는 `Boolean` 변수입니다.  
  
 [!code-vb[VbVbalrOperators#86](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#86)]  
  
## <a name="see-also"></a>참고자료

- [부울 식](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)
- [연산자 및 식](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [방법: 숫자 값 계산](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-calculate-numeric-values.md)
- [Visual Basic에서의 연산자 우선 순위](../../../../visual-basic/language-reference/operators/operator-precedence.md)
