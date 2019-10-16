---
title: '\ 연산자(Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.\
- '\'
helpviewer_keywords:
- division operator [Visual Basic], integer
- integer division operator [Visual Basic]
- zero, division by zero
- arithmetic operators [Visual Basic], division
- division [Visual Basic], by zero
- backslash (\) [Visual Basic]
- '\ operator [Visual Basic]'
- integer quotient
- math operators [Visual Basic]
- quotients, integer
- truncation [Visual Basic], integer division
ms.assetid: 4b0ee347-950c-45c9-8e23-54bc85df208e
ms.openlocfilehash: d1a46f99c21be007d33361ba095a3f0c52fe906c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701141"
---
# <a name="-operator-visual-basic"></a>\ 연산자(Visual Basic)
두 숫자를 나누고 정수 결과를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
expression1 \ expression2  
```  
  
## <a name="parts"></a>요소  
 `expression1`  
 필수 요소. 임의의 숫자 식입니다.  
  
 `expression2`  
 필수. 임의의 숫자 식입니다.  
  
## <a name="supported-types"></a>지원 형식  
 부호 없는 형식 및 부동 소수점 형식 및 `Decimal`를 포함 하는 모든 숫자 형식입니다.  
  
## <a name="result"></a>결과  
 결과는로 `expression1` `expression2`나눈 정수 몫으로, 나머지는 무시 하 고 정수 부분만 유지 합니다. 이를 *잘림*이라고 합니다.  
  
 결과 데이터 형식은 및 `expression1` `expression2`의 데이터 형식에 적합 한 숫자 형식입니다. [연산자 결과의 데이터 형식](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)에서 "정수 산술 연산" 표를 참조 하세요.  
  
 [/연산자 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) 는 나머지를 소수 부분으로 유지 하는 전체 몫을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 나누기를 수행 하기 전에 Visual Basic 부동 소수점 숫자 식을로 `Long`변환 하려고 합니다. `Option Strict` 가`On`이면 컴파일러 오류가 발생 합니다. 이 `Option Strict` 인 `Off` 경우, 값이 [Long 데이터 형식](../../../visual-basic/language-reference/data-types/long-data-type.md)의 범위를 벗어나면<xref:System.OverflowException>이 가능합니다. 로 `Long` 의 변환에는 *은행원의 반올림*도 적용 됩니다. 자세한 내용은 [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)에서 "소수 부분"을 참조 하세요.  
  
 또는 `expression1` 가`expression2` [Nothing](../../../visual-basic/language-reference/nothing.md)으로 계산 되 면 0으로 처리 됩니다.  
  
## <a name="attempted-division-by-zero"></a>0으로 나누기 시도  
 가 `expression2` 0으로 계산 되는 `\` 경우 연산자는 <xref:System.DivideByZeroException> 예외를 throw 합니다. 피연산자의 모든 숫자 데이터 형식에 적용 됩니다.  
  
> [!NOTE]
> 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `\` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `\` 연산자를 사용 하 여 정수 나누기를 수행 합니다. 결과는 두 피연산자의 정수 몫을 나타내며 나머지는 삭제 된 정수입니다.  
  
 [!code-vb[VbVbalrOperators#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#18)]  
  
 앞의 예제에서 식은 각각 2, 3, 33 및-22의 값을 반환 합니다.  
  
## <a name="see-also"></a>참고자료

- [\\= 연산자](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)
- [/연산자 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic의 산술 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
