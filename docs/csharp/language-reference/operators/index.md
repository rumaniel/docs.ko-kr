---
title: C# 연산자 - C# 참조
ms.date: 08/20/2019
f1_keywords:
- cs.operators
helpviewer_keywords:
- operators [C#]
- operator precedence [C#]
- operator associativity [C#]
- expressions [C#]
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
ms.openlocfilehash: 766da517d247361f747591c3758e8610927866a9
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71116106"
---
# <a name="c-operators-c-reference"></a>C# 연산자(C# 참조)

C#은 기본 제공 형식에서 지원되는 여러 연산자를 제공합니다. 예를 들어 [산술 연산자](arithmetic-operators.md)는 숫자 피연산자를 사용하여 산술 연산을 수행하고 [부울 논리 연산자](boolean-logical-operators.md)는 [bool](../keywords/bool.md) 피연산자를 사용하여 논리 연산을 수행합니다. 특정 연산자는 [오버로드](operator-overloading.md)할 수 있습니다. 연산자 오버로드를 사용하여 사용자 정의 형식의 피연산자에 대해 연산자 동작을 지정할 수 있습니다.

[식](../../programming-guide/statements-expressions-operators/expressions.md)에서 연산자 우선 순위 및 결합성은 연산이 수행되는 순서를 결정합니다. 괄호를 사용하여 연산자 우선 순위 및 결합성에 따라 주어진 계산 순서를 변경할 수 있습니다.

## <a name="operator-precedence"></a>연산자 우선 순위

여러 연산자가 있는 식에서 우선 순위가 높은 연산자는 연산자가 우선 순위가 낮은 연산자보다 먼저 계산됩니다. 다음 예제에서는 곱하기가 더하기보다 높은 우선 순위를 가지므로 곱하기가 먼저 수행됩니다.

```csharp-interactive
var a = 2 + 2 * 2;
Console.WriteLine(a); //  output: 6
```

괄호를 사용하여 연산자 우선 순위에 따라 주어진 계산 순서를 변경합니다.

```csharp-interactive
var a = (2 + 2) * 2;
Console.WriteLine(a); //  output: 8
```

다음 표에서는 우선순위가 가장 높은 것부터 시작하여 순서대로 C# 연산자를 나열합니다. 각 행 내의 연산자는 우선 순위가 같습니다.

| 연산자 | 범주 또는 이름 |
| --------- | ---------------- |
| [x.y](member-access-operators.md#member-access-operator-), [x?.y](member-access-operators.md#null-conditional-operators--and-), [x?[y]](member-access-operators.md#null-conditional-operators--and-), [f(x)](member-access-operators.md#invocation-operator-), [a&#91;i&#93;](member-access-operators.md#indexer-operator-), [x++](arithmetic-operators.md#increment-operator-), [x--](arithmetic-operators.md#decrement-operator---), [new](new-operator.md), [typeof](type-testing-and-cast.md#typeof-operator), [checked](../keywords/checked.md), [unchecked](../keywords/unchecked.md), [default](default.md), [nameof](nameof.md), [delegate](delegate-operator.md), [sizeof](sizeof.md), [stackalloc](stackalloc.md), [x->y](pointer-related-operators.md#pointer-member-access-operator--) | 기본 연산자 |
| [+x](arithmetic-operators.md#unary-plus-and-minus-operators), [-x](arithmetic-operators.md#unary-plus-and-minus-operators), [\!x](boolean-logical-operators.md#logical-negation-operator-), [~x](bitwise-and-shift-operators.md#bitwise-complement-operator-), [++x](arithmetic-operators.md#increment-operator-), [--x](arithmetic-operators.md#decrement-operator---), [^x](member-access-operators.md#index-from-end-operator-), [(T)x](type-testing-and-cast.md#cast-operator-), [await](await.md), [&x](pointer-related-operators.md#address-of-operator-), [*x](pointer-related-operators.md#pointer-indirection-operator-), [true 및 false](true-false-operators.md) | 단항 |
| [x..y](member-access-operators.md#range-operator-) | 범위 |
| [x * y](arithmetic-operators.md#multiplication-operator-), [x / y](arithmetic-operators.md#division-operator-), [x % y](arithmetic-operators.md#remainder-operator-) | 곱하기|
| [x + y](arithmetic-operators.md#addition-operator-), [x – y](arithmetic-operators.md#subtraction-operator--) | 더하기 |
| [x \<\<  y](bitwise-and-shift-operators.md#left-shift-operator-), [x >> y](bitwise-and-shift-operators.md#right-shift-operator-) | 시프트 |
| [x \< y](comparison-operators.md#less-than-operator-), [x > y](comparison-operators.md#greater-than-operator-), [x \<= y](comparison-operators.md#less-than-or-equal-operator-), [x >= y](comparison-operators.md#greater-than-or-equal-operator-), [is](type-testing-and-cast.md#is-operator), [as](type-testing-and-cast.md#as-operator) | 관계형 및 형식 테스트 |
| [x == y](equality-operators.md#equality-operator-), [x != y](equality-operators.md#inequality-operator-) | 같음 |
| `x & y` | [부울 논리 AND](boolean-logical-operators.md#logical-and-operator-) 또는 [비트 논리 AND](bitwise-and-shift-operators.md#logical-and-operator-) |
| `x ^ y` | [부울 논리 XOR](boolean-logical-operators.md#logical-exclusive-or-operator-) 또는 [비트 논리 XOR](bitwise-and-shift-operators.md#logical-exclusive-or-operator-) |
| <code>x &#124; y</code> | [ OR](boolean-logical-operators.md#logical-or-operator-) 또는 [비트 논리 OR](bitwise-and-shift-operators.md#logical-or-operator-) |
| [x && y](boolean-logical-operators.md#conditional-logical-and-operator-) | 조건부 AND |
| [x &#124;&#124; y](boolean-logical-operators.md#conditional-logical-or-operator-) | 조건부 OR |
| [x ?? y](null-coalescing-operator.md) | Null 병합 연산자 |
| [c ? t : f](conditional-operator.md) | 조건 연산자 |
| [x = y](assignment-operator.md), [x += y](arithmetic-operators.md#compound-assignment), [x -= y](arithmetic-operators.md#compound-assignment), [x *= y](arithmetic-operators.md#compound-assignment), [x /= y](arithmetic-operators.md#compound-assignment), [x %= y](arithmetic-operators.md#compound-assignment), [x &= y](boolean-logical-operators.md#compound-assignment), [x &#124;= y](boolean-logical-operators.md#compound-assignment), [x ^= y](boolean-logical-operators.md#compound-assignment), [x <<= y](bitwise-and-shift-operators.md#compound-assignment), [x >>= y](bitwise-and-shift-operators.md#compound-assignment), [x ??= y](null-coalescing-operator.md), [=>](lambda-operator.md) | 할당 및 람다 선언 |

## <a name="operator-associativity"></a>연산자 결합성

연산자의 우선 순위가 같은 경우 연산자의 결합성이 연산이 수행되는 순서를 결정합니다.

- ‘왼쪽 결합성이 있는’ 연산자는 왼쪽에서 오른쪽으로 계산됩니다.  [대입 연산자](assignment-operator.md) 및 [null 병합 연산자 `??`](null-coalescing-operator.md)를 제외하고, 모든 이진 연산자는 왼쪽 결합성이 있습니다. 예를 들어, `a + b - c`는 `(a + b) - c`로 계산됩니다.
- ‘오른쪽 결합성이 있는’ 연산자는 오른쪽에서 왼쪽으로 계산됩니다.  대입 연산자, null 병합 연산자 `??` 및 [조건 연산자 `?:`](conditional-operator.md)은 오른쪽 결합성이 있습니다. 예를 들어, `x = y = z`는 `x = (y = z)`로 계산됩니다.

괄호를 사용하여 연산자 결합성에 따라 주어진 계산 순서를 변경합니다.

```csharp-interactive
int a = 13 / 5 / 2;
int b = 13 / (5 / 2);
Console.WriteLine($"a = {a}, b = {b}");  // output: a = 1, b = 6
```

## <a name="operand-evaluation"></a>피연산자 계산

연산자 우선 순위 및 결합성과 관계없이 식의 피연산자는 왼쪽에서 오른쪽으로 계산됩니다. 다음 예제는 연산자와 피연산자가 계산되는 순서를 보여 줍니다.

| 식 | 계산 순서 |
| ---------- | ------------------- |
|`a + b`|a, b, +|
|`a + b * c`|a, b, c, *, +|
|`a / b + c * d`|a, b, /, c, d, *, +|
|`a / (b + c) * d`|a, b, c, +, /, d, *|

일반적으로 모든 연산자 피연산자가 계산됩니다. 일부 연산자는 조건부로 피연산자를 계산합니다. 즉, 이와 같은 연산자의 첫 번째 피연산자 값이 다른 피연산자를 계산해야 할지 여부 또는 계산해야 할 다른 피연산자를 정의합니다. 이에 해당하는 연산자는 조건부 논리 [AND(`&&`)](boolean-logical-operators.md#conditional-logical-and-operator-) 및 [OR(`||`)](boolean-logical-operators.md#conditional-logical-or-operator-) 연산자, [null 병합 연산자 `??`](null-coalescing-operator.md), [null 조건부 연산자 `?.` 및 `?[]`](member-access-operators.md#null-conditional-operators--and-), [조건 연산자 `?:`](conditional-operator.md)입니다. 자세한 내용은 각 연산자의 설명을 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [연산자](~/_csharplang/spec/expressions.md#operators) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [식](../../programming-guide/statements-expressions-operators/expressions.md)
