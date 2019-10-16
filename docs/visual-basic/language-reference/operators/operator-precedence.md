---
title: Visual Basic에서의 연산자 우선 순위
ms.date: 07/20/2015
helpviewer_keywords:
- arithmetic operators [Visual Basic], precedence
- operator precedence
- logical operators [Visual Basic], precedence
- operators [Visual Basic], associativity
- operators [Visual Basic], resolution
- associativity of operators [Visual Basic]
- operators [Visual Basic], precedence
- precedence [Visual Basic], of operators
- comparison operators [Visual Basic], precedence
- math operators [Visual Basic]
- order of precedence
ms.assetid: cbbdb282-f572-458e-a520-008a675f8063
ms.openlocfilehash: df40aced45442c9c7895c8d10ece64b21e292508
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659919"
---
# <a name="operator-precedence-in-visual-basic"></a>Visual Basic에서의 연산자 우선 순위
식에서 여러 연산이 수행 될 때 각 부분은 *연산자 우선 순위*라는 미리 결정 된 순서에 따라 평가 되 고 해결 됩니다.

## <a name="precedence-rules"></a>선행 규칙
 식이 둘 이상의 범주에 있는 연산자를 포함 하는 경우 다음 규칙에 따라 평가 됩니다.

- 산술 및 연결 연산자는 다음 섹션에서 설명 하는 우선 순위를 가지 며 모두 비교, 논리 및 비트 연산자 보다 우선 순위가 높습니다.

- 모든 비교 연산자는 동일한 우선 순위를 가지 며 모든 비교 연산자는 논리 및 비트 연산자 보다 우선 순위가 크므로 산술 연산자와 연결 연산자 보다 우선 순위가 낮습니다.

- 논리 및 비트 연산자는 다음 섹션에서 설명 하는 우선 순위를 가지 며 모두 산술, 연결 및 비교 연산자 보다 우선 순위가 낮습니다.

- 우선 순위가 같은 연산자는 식에 표시 되는 순서 대로 왼쪽에서 오른쪽으로 계산 됩니다.

## <a name="precedence-order"></a>우선 순위
 연산자는 다음과 같은 우선 순위에 따라 평가 됩니다.

### <a name="await-operator"></a>Await 연산자
 W

### <a name="arithmetic-and-concatenation-operators"></a>산술 및 연결 연산자
 지 각`^`()

 단항 id 및 부정 (`+`, `–`)

 곱하기 및 부동 소수점 나누기 (`*`,) `/`

 정수 나누기 (`\`)

 모듈식 산술 (`Mod`)

 더하기 및 빼기 (`+`, `–`)

 문자열 연결 (`&`)

 산술 비트 시프트 (`<<`, `>>`)

### <a name="comparison-operators"></a>비교 연산자
 모든 비교 연산자 (`=`, `<>`, `<`, `<=`, `>` ,`>=`, ,,`Is`, ...`TypeOf` `IsNot` `Like` `Is`)

### <a name="logical-and-bitwise-operators"></a>논리 및 비트 연산자
 부정 (`Not`)

 결합 (`And`, `AndAlso`)

 포함 분리 (`Or`, `OrElse`)

 배타적 분리 (`Xor`)

### <a name="comments"></a>주석
 `=` 연산자는 대입 연산자가 아닌 같음 비교 연산자입니다.

 문자열 연결 연산자 (`&`)는 산술 연산자가 아니지만 우선 순위는 산술 연산자와 함께 그룹화 됩니다.

 `Is` 및`IsNot` 연산자는 개체 참조 비교 연산자입니다. 두 개체의 값을 비교 하지 않습니다. 두 개체 변수가 동일한 개체 인스턴스를 참조 하는지 확인 합니다.

## <a name="associativity"></a>associativity
 곱하기 및 나누기와 같이 우선 순위가 같은 연산자가 식에 함께 표시 되는 경우 컴파일러는 각 작업을 왼쪽에서 오른쪽으로 발견할 때 각 작업을 평가 합니다. 다음은 이에 대한 예입니다.

```vb
Dim n1 As Integer = 96 / 8 / 4
Dim n2 As Integer = (96 / 8) / 4
Dim n3 As Integer = 96 / (8 / 4)
```

 첫 번째 식은 나누기 96/8 (결과 12)을 평가한 다음 나누기 12/4를 계산 하 여 3을 반환 합니다. 컴파일러는에 대 한 `n1` 작업을 왼쪽에서 오른쪽으로 평가 하기 때문에에 대 한 `n2`순서가 명시적으로 지정 된 경우에도 계산이 동일 합니다. `n1` 및`n2` 는 모두 3의 결과를 가집니다. 이와 대조적 `n3` 으로 괄호를 적용 하면 컴파일러가 8/4를 먼저 평가 하기 때문에 48이 발생 합니다.

 이 동작으로 인해 연산자는 Visual Basic에서 *왼쪽 결합성* 이라고 합니다.

## <a name="overriding-precedence-and-associativity"></a>우선 순위 및 결합성 재정의
 괄호를 사용 하 여 식의 일부 부분이 다른 식 보다 먼저 계산 되도록 할 수 있습니다. 이는 우선 순위와 왼쪽 결합성의 순서를 모두 재정의할 수 있습니다. Visual Basic는 항상 괄호 안에 포함 된 작업을 외부에서 수행 합니다. 그러나 괄호 안에 괄호를 사용 하지 않으면 괄호 안에 일반적인 우선 순위와 결합성이 유지 됩니다. 다음은 이에 대한 예입니다.

```vb
Dim a, b, c, d, e, f, g As Double
a = 8.0
b = 3.0
c = 4.0
d = 2.0
e = 1.0
f = a - b + c / d * e
' The preceding line sets f to 7.0. Because of natural operator
' precedence and associativity, it is exactly equivalent to the
' following line.
f = (a - b) + ((c / d) * e)
' The following line overrides the natural operator precedence
' and left associativity.
g = (a - (b + c)) / (d * e)
' The preceding line sets g to 0.5.
```

## <a name="see-also"></a>참고자료

- [= 연산자](../../../visual-basic/language-reference/operators/assignment-operator.md)
- [Is 연산자](../../../visual-basic/language-reference/operators/is-operator.md)
- [IsNot 연산자](../../../visual-basic/language-reference/operators/isnot-operator.md)
- [Like 연산자](../../../visual-basic/language-reference/operators/like-operator.md)
- [TypeOf 연산자](../../../visual-basic/language-reference/operators/typeof-operator.md)
- [Await 연산자](../../../visual-basic/language-reference/operators/await-operator.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [연산자 및 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
