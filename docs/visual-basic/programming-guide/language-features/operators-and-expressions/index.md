---
title: Visual Basic의 연산자 및 식
ms.date: 07/20/2015
helpviewer_keywords:
- operators [Visual Basic], operands
- operators [Visual Basic]
- operands [Visual Basic], definition
- Visual Basic code, operators
- Visual Basic code, expressions
- operands
- expressions [Visual Basic]
ms.assetid: b86f3131-94ee-448f-96cd-79611e028b26
ms.openlocfilehash: 40d71c5231b8d278f4ca8d9352e6e3cba5104f9b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649704"
---
# <a name="operators-and-expressions-in-visual-basic"></a>Visual Basic의 연산자 및 식
*연산자*는 값을 가지는 하나 이상의 코드 요소에서 작업을 수행하는 코드 요소입니다. 값 요소는 변수, 상수, 리터럴, 속성을 포함하고 `Function` 및 `Operator` 프로시저와 식에서 반환됩니다.  
  
 *식*은 연산자와 결합된 일련의 값 요소로서, 새 값을 생성합니다. 연산자는 계산, 비교 또는 기타 작업을 수행하여 값 요소에 적용됩니다.  
  
## <a name="types-of-operators"></a>연산자 형식  
 Visual Basic는 다음과 같은 유형의 연산자를 제공합니다.  
  
- [산술 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)는 비트 패턴 이동을 포함하여 숫자 값에서 친숙한 계산을 수행합니다.  
  
- [비교 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)는 두 개의 식을 비교하고 비교 결과를 나타내는 `Boolean` 값을 반환합니다.  
  
- [연결 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)는 여러 문자열을 단일 문자열로 조인합니다.  
  
- [Visual Basic의 논리 및 비트 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)는 `Boolean` 또는 숫자 값을 결합하고 값과 같은 데이터 형식의 결과를 반환합니다.  
  
 연산자와 결합된 값 요소를 해당 연산자의 *피연산자*라고 합니다. *문*을 구성하는 대입 연산자를 제외하고 값 요소와 결합된 연산자는 식을 구성합니다. 자세한 내용은 [문](../../../../visual-basic/programming-guide/language-features/statements.md)을 참조하세요.  
  
## <a name="evaluation-of-expressions"></a>식 평가  
 식의 최종 결과는 값을 나타냅니다. 값은 일반적으로 `Boolean`, `String` 또는 숫자 형식과 같은 친숙한 데이터 형식입니다.  
  
 식의 예제는 다음과 같습니다.  
  
 `5 + 4`  
  
 `' The preceding expression evaluates to 9.`  
  
 `15 * System.Math.Sqrt(9) + x`  
  
 `' The preceding expression evaluates to 45 plus the value of x.`  
  
 `"Concat" & "ena" & "tion"`  
  
 `' The preceding expression evaluates to "Concatenation".`  
  
 `763 < 23`  
  
 `' The preceding expression evaluates to False.`  
  
 다음 예제와 같은 단일 식 또는 문에서 여러 가지 연산자가 작업을 수행할 수 있습니다.  
  
 [!code-vb[VbVbalrOperators#56](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#56)]  
  
 앞의 예제에서 Visual Basic 대입 연산자의 오른쪽 식의 작업을 수행 (`=`), 변수에 결과 값을 할당 한 다음 `x` 왼쪽에 있습니다. 식에 결합할 수 있는 연산자 수에는 실제로 제한이 없지만 예상하는 결과를 얻으려면 [Visual Basic의 연산자 우선 순위](../../../../visual-basic/language-reference/operators/operator-precedence.md)를 이해해야 합니다.  

## <a name="see-also"></a>참고자료

- [연산자](../../../../visual-basic/language-reference/operators/index.md)
- [연산자의 효율적 결합](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
- [문(C++)](../../../../visual-basic/language-reference/statements/index.md)
