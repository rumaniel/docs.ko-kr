---
title: ^ 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.^
helpviewer_keywords:
- raising numbers to powers
- ^ operator [Visual Basic], exponentiation
- square operator [Visual Basic]
- ^ operator [Visual Basic]
- exponentiation operator [Visual Basic]
- exponent
- numbers [Visual Basic], rasing
- powers
- arithmetic operators [Visual Basic], exponentiation
ms.assetid: d89a1ca8-83da-4784-a87b-a9d7dceb3f62
ms.openlocfilehash: 8cdfbec917608211e19c39eb37bd12dbc7c4d33f
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592217"
---
# <a name="-operator-visual-basic"></a>^ 연산자(Visual Basic)

숫자를 다른 숫자의 승수로 거듭제곱 합니다.

## <a name="syntax"></a>구문

```vb
number ^ exponent
```

## <a name="parts"></a>요소

`number`\
필수 요소. 임의의 숫자 식입니다.

`exponent`\
필수. 임의의 숫자 식입니다.

## <a name="result"></a>결과

결과는 항상 `Double` 값으로 `exponent`의 거듭제곱으로 발생 @no__t 됩니다.

## <a name="supported-types"></a>지원 형식

`Double`. 다른 형식의 피연산자는 `Double`으로 변환 됩니다.

## <a name="remarks"></a>설명

Visual Basic는 [Double 데이터 형식](../../../visual-basic/language-reference/data-types/double-data-type.md)에서 항상 지 각 연산을 수행 합니다.

@No__t-0의 값은 소수 자릿수, 음수 또는 둘 다 일 수 있습니다.

단일 식에서 두 개 이상의 지 수를 수행 하는 경우 `^` 연산자는 왼쪽에서 오른쪽으로 발견 될 때 계산 됩니다.

> [!NOTE]
> 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `^` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.

## <a name="example"></a>예제

다음 예에서는 `^` 연산자를 사용 하 여 숫자를 지 수의 거듭제곱으로 거듭제곱 합니다. 결과는 첫 번째 피연산자가 두 번째 피연산자의 거듭제곱으로 발생 합니다.

[!code-vb[VbVbalrOperators#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#20)]

앞의 예제에서는 다음과 같은 결과를 생성 합니다.

`exp1`은 4 (4 제곱)로 설정 됩니다.

`exp2`이 19683 (3 제곱으로 설정 된 후 해당 값이 3 제곱)로 설정 됩니다.

`exp3`은-125 (-5의 3 제곱)로 설정 됩니다.

`exp4`은 625 (-5에서 4 제곱으로)로 설정 됩니다.

`exp5`은 2 (큐브 루트 8)로 설정 됩니다.

`exp6`은 0.5 (1.0을 8의 큐브 루트로 나눈 값)으로 설정 됩니다.

앞의 예제에서 식의 괄호의 중요도를 확인 합니다. *연산자 우선 순위로*인해 Visual Basic은 일반적으로 단항 `–` 연산자를 포함 하 여 다른 모든 이전에 `^` 연산자를 수행 합니다. @No__t-0과 `exp6`이 괄호 없이 계산 된 경우 다음과 같은 결과가 생성 됩니다.

`exp4 = -5 ^ 4`은 – (5에서 4 제곱)로 계산 되므로-625이 발생 합니다.

`exp6 = 8 ^ -1.0 / 3.0`은 (8에서 – 1 제곱 또는 0.125)로 구분 되어 3.0로 구분 됩니다. 그러면 0.041666666666666666666666666666667이 발생 합니다.

## <a name="see-also"></a>참조

- [^= 연산자](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic의 산술 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
