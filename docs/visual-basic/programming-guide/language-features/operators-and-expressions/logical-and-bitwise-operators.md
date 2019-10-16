---
title: Visual Basic의 논리 및 비트 연산자
ms.date: 07/20/2015
helpviewer_keywords:
- short-circuiting
- Boolean expressions
- logical operators [Visual Basic], Boolean expressions
- operators [Visual Basic], logical
- AndAlso operator [Visual Basic]
- Not operator [Visual Basic], Boolean expressions
- Xor operator [Visual Basic], Boolean expressions
- And operator [Visual Basic], logical operators
- logical operators [Visual Basic]
- expressions [Visual Basic], Boolean
- Or operator [Visual Basic], logical operators
- Visual Basic code, operators
- short-circuiting [Visual Basic], logical operators
- logical operators [Visual Basic], short-circuiting
- Visual Basic code, expressions
- logical operators [Visual Basic], binary
- OrElse operator [Visual Basic]
- logical operators [Visual Basic], unary
ms.assetid: ca474e13-567d-4b1d-a18b-301433705e57
ms.openlocfilehash: 40076b2ad6606b4c565bcd39dbeea9e55da47211
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963313"
---
# <a name="logical-and-bitwise-operators-in-visual-basic"></a>Visual Basic의 논리 및 비트 연산자
논리 연산자는 `Boolean` 식을 비교 하 고 `Boolean` 결과를 반환 합니다. `And` ,`Or`, `Not` , 및`OrElse`연산자는 두 개의 피연산자를 사용 하는 반면 *이항* 는 단일 피연산자를 사용 하기 때문에 단항 연산자입니다. `AndAlso` `Xor` 이러한 연산자 중 일부는 정수 값에 대해 비트 논리적 연산을 수행할 수도 있습니다.  
  
## <a name="unary-logical-operator"></a>단항 논리 연산자  
 [Not 연산자](../../../../visual-basic/language-reference/operators/not-operator.md) 는 `Boolean` 식에 논리 *부정을* 수행 합니다. 피연산자와 반대 되는 논리를 생성 합니다. 식이로 `True`계산 `False` `False` `Not` 되 면를 반환 하 고, 식이로 계산 되 `Not` `True`면를 반환 합니다. 다음은 이에 대한 예입니다.  
  
 [!code-vb[VbVbalrOperators#77](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#77)]  
  
## <a name="binary-logical-operators"></a>이항 논리 연산자  
 [And 연산자](../../../../visual-basic/language-reference/operators/and-operator.md) 는 두 `Boolean` 식에 논리 *결합* 을 수행 합니다. 두 식이 모두로 `True`계산 `And` 되 면를 `True`반환 합니다. 식 중 하나 이상이로 `False`평가 `And` 되 면를 반환 `False`합니다.  
  
 [Or 연산자](../../../../visual-basic/language-reference/operators/or-operator.md) 는 두 `Boolean` 식에 *논리합* 연산을 수행 합니다. 두 식이 모두 `True`로 계산 되거나 모두로 `True`계산 되 면이 `Or` 반환 `True`됩니다. 식이로 `True`계산 되지 않는 경우는 `False`을 `Or` 반환 합니다.  
  
 [Xor 연산자](../../../../visual-basic/language-reference/operators/xor-operator.md) 는 두 `Boolean` 식에 대해 논리적 *제외* 를 수행 합니다. 정확히 하나의 식이로 계산 되지만 `True`둘 다로 계산 되지 `Xor` 않는 `True`경우는를 반환 합니다. 두 식이 `True` 모두로 계산 되거나 모두로 `False`계산 되 `Xor` 는 `False`경우는를 반환 합니다.  
  
 다음 예에서는 `And`, `Or`및 `Xor` 연산자를 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#78)]  
  
## <a name="short-circuiting-logical-operations"></a>순환이 짧은 논리 작업  
 [AndAlso 연산자](../../../../visual-basic/language-reference/operators/andalso-operator.md) 는 두 `Boolean` 식에서 논리적 결합 `And` 도 수행 한다는 점에서 연산자와 매우 비슷합니다. 둘 사이의 주요 차이점은 *단락* 동작을 `AndAlso` 보여 주는 것입니다. `AndAlso` 식의 첫 번째 식이로 `False`계산 되는 경우 최종 결과를 `AndAlso` 변경할 수 없고를 반환할 `False`수 없으므로 두 번째 식이 계산 되지 않습니다.  
  
 마찬가지로 [OrElse 연산자](../../../../visual-basic/language-reference/operators/orelse-operator.md) 는 두 `Boolean` 식에 순환이 짧은 논리 분리를 수행 합니다. `OrElse` 식의 첫 번째 식이로 `True`계산 되는 경우 최종 결과를 `OrElse` 변경할 수 없고를 반환할 `True`수 없으므로 두 번째 식이 계산 되지 않습니다.  
  
### <a name="short-circuiting-trade-offs"></a>단락 장단점  
 단락을 통해 논리 연산의 결과를 변경할 수 없는 식을 계산 하지 않고 성능을 향상 시킬 수 있습니다. 그러나 해당 식에서 추가 작업을 수행 하는 경우 단락에서는 이러한 작업을 건너뜁니다. 예를 들어 식에 `Function` 프로시저에 대 한 호출이 포함 된 경우 식이 short short-circuit 경우 해당 프로시저는 호출 되지 않으며 `Function` 에 포함 된 추가 코드는 실행 되지 않습니다. 따라서 함수는 가끔씩만 실행 될 수 있으며 제대로 테스트 되지 않을 수도 있습니다. 또는 프로그램 논리는의 코드 `Function`에 따라 달라질 수 있습니다.  
  
 다음 예제에서는 `And`, `Or`및의 단락에 대 한 차이점을 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#81](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#81)]  
  
 [!code-vb[VbVbalrOperators#80](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#80)]  
  
 [!code-vb[VbVbalrOperators#79](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#79)]  
  
 앞의 예제에서 내부의 `checkIfValid()` 일부 중요 한 코드는 호출이 단기 short-circuit 때 실행 되지 않습니다. 가 short `If` 회로를 `checkIfValid()` 포함 `12 > 45` 하지 않기 `False`때문에 `And` 첫 번째 문은를 반환 합니다. 두 번째 `If` 문은가를 반환할 `checkIfValid()` `12 > 45` `False`때 두 번째 식을 `AndAlso` short 회로 하므로를 호출 하지 않습니다. 이 짧은 `If` 회로를 `checkIfValid()` 포함 `12 < 45` 하지 않으므로 `True` 세`Or` 번째 문은를 반환 하지만를 호출 합니다. 가를 `If` 반환 `12 < 45` `OrElse` `checkIfValid()` 하면두번째식을short회로하므로네번째문은를호출하지않습니다.`True`  
  
## <a name="bitwise-operations"></a>비트 연산  
 비트 연산은 이진 (기본 2) 형식으로 두 개의 정수 값을 평가 합니다. 해당 위치의 비트를 비교한 다음 비교에 따라 값을 할당 합니다. 다음 예에서는 연산자를 `And` 보여 줍니다.  
  
 [!code-vb[VbVbalrConcepts#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConcepts/VB/Class1.vb#2)]  
  
 앞의 예제에서는의 `x` 값을 1로 설정 합니다. 이 문제는 다음과 같은 이유로 발생 합니다.  
  
- 값은 binary로 처리 됩니다.  
  
     3 이진 형식 = 011  
  
     5 이진 형식 = 101  
  
- 연산자 `And` 는 한 번에 하나의 이진 위치 (비트)를 비교 합니다. 지정 된 위치에 있는 두 비트가 모두 1 이면 결과의 해당 위치에 1이 배치 됩니다. 두 비트가 모두 0 인 경우 결과의 해당 위치에 0이 배치 됩니다. 위의 예제에서는 다음과 같이 작동 합니다.  
  
     011 (이진 형식의 경우 3)  
  
     101 (이진 형식의 5)  
  
     001 (이진 형식으로 된 결과)  
  
- 결과는 10 진수로 처리 됩니다. 값 001은 1의 이진 표현 이므로 `x` = 1입니다.  
  
 비교 하 `Or` 는 비트 중 하나 또는 둘 다가 1 이면 결과 비트에 1이 할당 된다는 점을 제외 하 고 비트 연산은 비슷합니다. `Xor`비교 된 비트 (둘 다) 중 정확히 하나가 1 이면 결과 비트에 1을 할당 합니다. `Not`단일 피연산자를 사용 하 고 부호 비트를 포함 하 여 모든 비트를 반전 하 고 결과에 해당 값을 할당 합니다. 즉, `Not` 부호 있는 양수의 경우 항상 음수 값을 반환 하 고 음수 `Not` 에 대해는 항상 양수 또는 0 값을 반환 합니다.  
  
 `AndAlso` 및`OrElse` 연산자는 비트 연산을 지원 하지 않습니다.  
  
> [!NOTE]
> 비트 연산은 정수 계열 형식에 대해서만 수행할 수 있습니다. 비트 연산을 계속 하려면 부동 소수점 값을 정수 계열 형식으로 변환 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [논리/비트 연산자 (Visual Basic)](../../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [부울 식](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)
- [Visual Basic의 산술 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
- [Visual Basic의 비교 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic의 연결 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)
- [연산자의 효율적 결합](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
