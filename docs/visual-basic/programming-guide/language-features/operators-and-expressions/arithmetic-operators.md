---
title: Visual Basic의 산술 연산자
ms.date: 07/20/2015
helpviewer_keywords:
- type safety
- operators [Visual Basic], bitwise
- operators [Visual Basic], bit-shift
- bitwise operators [Visual Basic]
- bit-shift operators [Visual Basic]
- zero, division by zero
- operators [Visual Basic], arithmetic
- division [Visual Basic], by zero
- Visual Basic code, operators
- arithmetic operators [Visual Basic], about arithmetic operators
ms.assetid: 325dac7a-ea4f-41d5-8b48-f6e904211569
ms.openlocfilehash: a1854e35e32a31dbf531e6705a7968434dd02e44
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593245"
---
# <a name="arithmetic-operators-in-visual-basic"></a>Visual Basic의 산술 연산자
산술 연산자는 리터럴, 변수, 다른 식, 함수 및 속성 호출 및 상수를 나타내는 숫자 값의 계산을 포함 하는 친숙 한 산술 연산을 수행 하도록 사용 됩니다. 피연산자의 개별 비트 수준에서 역할 및를 왼쪽 또는 오른쪽의 비트 패턴을 이동할 비트 시프트 연산자는 산술 연산자를 사용 하 여 분류 합니다.  
  
## <a name="arithmetic-operations"></a>산술 연산  
 와 함께 식에서 두 값을 추가할 수 있습니다는 [+ 연산자](../../../../visual-basic/language-reference/operators/addition-operator.md), 또는 빼기에서 사용 하 여 다른 합니다 [-연산자 (Visual Basic)](../../../../visual-basic/language-reference/operators/subtraction-operator.md)처럼 다음 예제에서는 합니다.  
  
 [!code-vb[VbVbalrOperators#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#57)]  
  
 부정도 사용 합니다 [-연산자 (Visual Basic)](../../../../visual-basic/language-reference/operators/subtraction-operator.md), 없지만 하나의 피연산자를 사용 하 여 다음 예제와 같이 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#58](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#58)]  
  
 곱하기와 나누기 사용 합니다 [* 연산자](../../../../visual-basic/language-reference/operators/multiplication-operator.md) 및 [/ 연산자 (Visual Basic)](../../../../visual-basic/language-reference/operators/floating-point-division-operator.md)다음 예제 처럼 각각.  
  
 [!code-vb[VbVbalrOperators#59](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#59)]  
  
 지 수 연산을 사용 하 여는 [^ 연산자](../../../../visual-basic/language-reference/operators/exponentiation-operator.md)같이 다음 예에서는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#60)]  
  
 정수 나누기가 사용 하 여 실행 합니다 [\ 연산자 (Visual Basic)](../../../../visual-basic/language-reference/operators/integer-division-operator.md)합니다. 정수 나누기 몫을 반환 합니다, 그리고 즉, 횟수를 나타내는 정수 제 분할할 수 있습니다 나머지 고려 하지 않고 피제수로 합니다. Divisor와 dividend 모두 정수 계열 형식 이어야 합니다 (`SByte`, `Byte`, `Short`, `UShort`를 `Integer`를 `UInteger`, `Long`, 및 `ULong`)이이 연산자에 대 한 합니다. 먼저 다른 모든 형식은 정수 계열 형식으로 변환 합니다. 다음 예제에서는 정수 나누기를 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#61)]  
  
 모듈러스 산술를 사용 하 여 수행 되는 [Mod 연산자](../../../../visual-basic/language-reference/operators/mod-operator.md)합니다. 이 연산자는 정수 횟수도 하 피제수를 나누는 나눈 나머지를 반환 합니다. 피제수와 제수의 정수 형식이 면 반환된 된 값은 정수입니다. Divisor와 dividend 부동 소수점 형식이 면 반환 된 값을 부동 소수점 이기도 합니다. 다음 예제에서는이 동작을 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#62)]  
  
 [!code-vb[VbVbalrOperators#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#63)]  
  
### <a name="attempted-division-by-zero"></a>0으로 나누기  
 0으로 나누기는 관련 된 데이터 형식에 따라 다른 결과입니다. 정수 계열 사업부의 (`SByte`, `Byte`, `Short`, `UShort`, `Integer`를 `UInteger`, `Long`, `ULong`),.NET Framework에서를 <xref:System.DivideByZeroException> 예외입니다. 나누기 작업에 `Decimal` 또는 `Single` 데이터 형식을.NET Framework도 throw를 <xref:System.DivideByZeroException> 예외입니다.  
  
 부동 소수점 나누기에서 합니다 `Double` 데이터 형식 예외가 throw 되지 및 결과 나타내는 클래스 멤버는 <xref:System.Double.NaN>를 <xref:System.Double.PositiveInfinity>, 또는 <xref:System.Double.NegativeInfinity>피제수에 따라 합니다. 다음 표에서 나누기의 다양 한 결과 `Double` 값을 0으로 합니다.  
  
|피제수 데이터 형식|제 수 데이터 형식|피제수 값|결과|  
|---|---|---|---|  
|`Double`|`Double`|0|<xref:System.Double.NaN> (수학적으로 정의 된 숫자가 아님)|  
|`Double`|`Double`|> 0|<xref:System.Double.PositiveInfinity>|  
|`Double`|`Double`|\< 0|<xref:System.Double.NegativeInfinity>|  
  
 Catch 하는 경우는 <xref:System.DivideByZeroException> 예외를 처리 하는 데 해당 멤버를 사용할 수 있습니다. 예를 들어를 <xref:System.Exception.Message%2A> 속성 예외에 대 한 메시지 텍스트를 저장 합니다. 자세한 내용은 [Try...Catch...Finally 문](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)을 참조하세요.  
  
## <a name="bit-shift-operations"></a>비트 시프트 작업  
 비트 시프트 작업과 비트 패턴에 산술 시프트를 수행합니다. 패턴은 오른쪽 피연산자는 패턴을 이동할 위치 수를 지정 하는 동안 왼쪽의 피연산자에 포함 됩니다. 패턴을 사용 하 여 오른쪽으로 이동할 수 있습니다 합니다 [>> 연산자](../../../../visual-basic/language-reference/operators/right-shift-operator.md) 또는 왼쪽의 [<< 연산자](../../../../visual-basic/language-reference/operators/left-shift-operator.md)합니다.  
  
 패턴 피연산자의 데이터 형식 이어야 합니다 `SByte`, `Byte`, `Short`, `UShort`를 `Integer`를 `UInteger`를 `Long`, 또는 `ULong`합니다. 시프트 크기 피연산자의 데이터 형식 이어야 합니다 `Integer` 으로 확장 해야 합니다 또는 `Integer`합니다.  
  
 산술 shifts 순환있지 않습니다 즉, 결과의 한쪽 끝에서 벗어나 이동한 비트는 반대쪽 다시 도입 되지 않습니다. 이동 하 여 비워진 비트 위치는 다음과 같이 설정 됩니다.  
  
- 산술 왼쪽된 시프트에 대 한 0  
  
- 양수의 산술 오른쪽 시프트에 대 한 0  
  
- 산술 오른쪽 시프트 연산 부호 없는 데이터 형식에 대 한 0 (`Byte`, `UShort`하십시오 `UInteger`, `ULong`)  
  
- 음수의 산술 오른쪽 시프트에 대 한 1 (`SByte`, `Short`를 `Integer`, 또는 `Long`)  
  
 다음 예에서는 이동는 `Integer` 왼쪽과 오른쪽 값입니다.  
  
 [!code-vb[VbVbalrOperators#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#64)]  
  
 산술 shifts 오버플로 예외를 생성 하지 않습니다.  
  
## <a name="bitwise-operations"></a>비트 연산  
 논리 연산자 뿐만 `Not`, `Or`, `And`, 및 `Xor` 숫자 값에 사용할 때 비트 산술을 수행할 수도 있습니다. 자세한 내용은 "비트 작업"를 참조 하세요 [논리 및 비트 Visual Basic의 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)합니다.  
  
## <a name="type-safety"></a>형식 안전성  
 피연산자는 일반적으로 동일한 형식 이어야 합니다. 예를 들어, 사용 하 여 추가 하는 경우는 `Integer` 변수를 추가 해야 다른 `Integer` 변수를 할당 해야 결과 형식의 변수에 `Integer` 도 합니다.  
  
 형식이 안전한을 확인 하는 한 가지 방법은 코딩 방법을 사용 하는 것은 [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)합니다. 설정 하는 경우 `Option Strict On`, Visual Basic에서 자동으로 수행 *형식이 안전한* 변환 합니다. 예를 들어, 추가 하려는 경우는 `Integer` 변수를 `Double` 변수를 값으로 할당을 `Double` 변수에 작업을 정상적으로 진행 되므로 `Integer` 값을 변환할 수 `Double` 데이터의 손실 없이. 안전 하지 않은 유형 변환에는 다른 한편으로 사용 하 여 컴파일러 오류가 발생 `Option Strict On`합니다. 예를 들어, 추가 하려는 경우는 `Integer` 변수를 `Double` 변수를 값으로 할당는 `Integer` 변수는 컴파일러 오류가 발생 하기 때문에 `Double` 형식으로 변수를 암시적으로 변환할 수 없습니다 `Integer`.  
  
 설정한 경우 `Option Strict Off`, 예기치 않은 데이터 또는 정밀도 손실을 초래할 수 있습니다 하지만 Visual Basic에서 암시적 축소 변환을 수행를 허용 하는 단, 합니다. 따라서이 사용 하는 권장 `Option Strict On` 프로덕션 코드를 작성할 때. 자세한 내용은 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [산술 연산자](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [비트 시프트 연산자](../../../../visual-basic/language-reference/operators/bit-shift-operators.md)
- [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic의 연결 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)
- [Visual Basic의 논리 및 비트 연산자](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
- [연산자의 효율적 결합](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
