---
title: 비트 및 시프트 연산자 - C# 참조
description: 정수 형식의 피연산자를 사용하여 비트 논리 또는 시프트 연산을 수행하는 C# 연산자에 대해 알아봅니다.
ms.date: 04/18/2019
author: pkulikov
f1_keywords:
- ~_CSharpKeyword
- <<_CSharpKeyword
- '>>_CSharpKeyword'
- '&_CSharpKeyword'
- ^_CSharpKeyword
- '|_CSharpKeyword'
helpviewer_keywords:
- bitwise logical operators [C#]
- shift operators [C#]
- tilde operator [C#]
- one's complement operator [C#]
- bitwise complement operator [C#]
- ~ operator [C#]
- left shift operator [C#]
- << operator [C#]
- right shift operator [C#]
- '>> operator [C#]'
- bitwise logical AND operator [C#]
- ampersand operator [C#]
- '& operator [C#]'
- bitwise logical exclusive OR operator [C#]
- bitwise logical XOR operator [C#]
- ^ operator [C#]
- bitwise logical OR operator [C#]
- '| operator [C#]'
ms.openlocfilehash: c18a06971887049a443f0bd1af7c77610a787a27
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67609950"
---
# <a name="bitwise-and-shift-operators-c-reference"></a>비트 및 시프트 연산자(C# 참조)

다음 연산자는 [정수 형식](../builtin-types/integral-numeric-types.md)의 피연산자를 사용하여 비트 논리 또는 시프트 연산을 수행합니다.

- 단항 [`~`(비트 보수)](#bitwise-complement-operator-) 연산자
- 이진 [`<<`(왼쪽 시프트)](#left-shift-operator-) 및 [`>>`(오른쪽 시프트)](#right-shift-operator-) 시프트 연산자
- 이진 [`&`(논리 AND)](#logical-and-operator-), [`|`(논리 OR)](#logical-or-operator-) 및 [`^`(논리 배타적 OR)](#logical-exclusive-or-operator-) 연산자

이러한 연산자는 `int`, `uint`, `long` 및 `ulong` 형식에 대해 정의되어 있습니다. 두 피연산자가 모두 다른 정수 형식(`sbyte`, `byte`, `short`, `ushort` 또는 `char`)인 경우, 해당 값은 작업의 결과 형식이기도 한 `int` 유형으로 변환됩니다. 피연산자가 다른 정수 형식인 경우 해당 값은 가장 가까운 정수 형식으로 변환됩니다. 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [숫자 승격](~/_csharplang/spec/expressions.md#numeric-promotions) 섹션을 참조하세요.

`bool` 유형의 피연산자에 대한 `&`, `|` 및 `^` 연산자도 정의되어 있습니다. 자세한 내용은 [부울 논리 연산자](boolean-logical-operators.md)를 참조하세요.

비트 및 시프트 작업으로 인해 오버플로가 발생하지 않고 [Checked 및 Unchecked](../keywords/checked-and-unchecked.md) 컨텍스트에서 동일한 결과가 생성되지 않습니다.

## <a name="bitwise-complement-operator-"></a>비트 보수 연산자 ~

`~` 연산자는 각 비트를 반대로 하여 해당 피연산자의 비트 보수를 생성합니다.

[!code-csharp-interactive[bitwise NOT](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseComplement)]

`~` 기호를 사용하여 종료자를 선언할 수도 있습니다. 자세한 내용은 [종료자](../../programming-guide/classes-and-structs/destructors.md)를 참조하세요.

## <a name="left-shift-operator-"></a>왼쪽 시프트 연산자 \<\<

`<<` 연산자는 왼쪽 피연산자를 오른쪽 피연산자로 정의된 비트 수만큼 왼쪽으로 이동합니다.

왼쪽 시프트 연산은 결과 형식의 범위를 벗어나는 상위 비트를 삭제하고 다음 예제와 같이 빈 하위 비트 위치를 0으로 설정합니다.

[!code-csharp-interactive[left shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LeftShift)]

시프트 연산자는 `int`, `uint`, `long` 및 `ulong` 유형에 대해서만 정의되므로 작업 결과에는 항상 32비트 이상이 포함됩니다. 왼쪽 피연산자가 다른 정수 형식(`sbyte`, `byte`, `short`, `ushort` 또는 `char`)인 경우, 다음 예제와 같이 해당 값이 `int` 유형으로 변환됩니다.

[!code-csharp-interactive[left shift with promotion](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LeftShiftPromoted)]

`<<` 연산자의 오른쪽 피연산자가 시프트 수를 정의하는 방법에 대한 자세한 내용은 [시프트 연산자의 시프트 수](#shift-count-of-the-shift-operators) 섹션을 참조하세요.

## <a name="right-shift-operator-"></a>오른쪽 시프트 연산자 >>

`>>` 연산자는 왼쪽 피연산자를 오른쪽 피연산자로 정의된 비트 수만큼 오른쪽으로 이동합니다.

오른쪽 시프트 연산은 다음 예제와 같이 하위 비트를 삭제합니다.

[!code-csharp-interactive[right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#RightShift)]

빈 상위 공백 비트 위치는 다음과 같이 왼쪽 피연산자 형식에 따라 설정됩니다.

- 왼쪽 피연산자가 [int](../builtin-types/integral-numeric-types.md) 또는 [long](../builtin-types/integral-numeric-types.md) 형식인 경우 오른쪽 시프트 연산자는 *산술* 시프트를 수행합니다. 왼쪽 피연산자의 최상위 비트(부호 비트) 값이 빈 상위 비트 위치로 전파됩니다. 즉, 빈 상위 비트 위치는 왼쪽 피연산자가 음수가 아닌 경우 0으로 설정되고, 음수인 경우 1로 설정됩니다.

  [!code-csharp-interactive[arithmetic right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#ArithmeticRightShift)]

- 왼쪽 피연산자가 [uint](../builtin-types/integral-numeric-types.md) 또는 [ulong](../builtin-types/integral-numeric-types.md) 형식이면 오른쪽 시프트 피연산자는 *논리적* 시프트를 수행합니다. 빈 상위 비트 위치가 항상 0으로 설정됩니다.

  [!code-csharp-interactive[logical right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LogicalRightShift)]

`>>` 연산자의 오른쪽 피연산자가 시프트 수를 정의하는 방법에 대한 자세한 내용은 [시프트 연산자의 시프트 수](#shift-count-of-the-shift-operators) 섹션을 참조하세요.

## <a name="logical-and-operator-"></a> 논리 AND 연산자 &amp;

`&` 연산자는 해당 피연산자의 비트 논리 AND를 컴퓨팅합니다.

[!code-csharp-interactive[bitwise AND](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseAnd)]

`bool` 유형의 피연산자의 경우 `&` 연산자는 해당 피연산자의 [논리 AND](boolean-logical-operators.md#logical-and-operator-)를 컴퓨팅합니다. 단항 `&` 연산자는 [address-of 연산자](pointer-related-operators.md#address-of-operator-)입니다.

## <a name="logical-exclusive-or-operator-"></a>논리 배타적 OR 연산자 ^

`^` 연산자는 해당 피연산자의 비트 논리 XOR이라고도 하는 비트 논리 배타적 OR을 컴퓨팅합니다.

[!code-csharp-interactive[bitwise XOR](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseXor)]

`bool` 유형의 피연산자의 경우 `^` 연산자는 해당 피연산자의 [논리 배타적 OR](boolean-logical-operators.md#logical-exclusive-or-operator-)을 컴퓨팅합니다.

## <a name="logical-or-operator-"></a>논리 OR 연산자 |

`|` 연산자는 해당 피연산자의 비트 논리 OR을 컴퓨팅합니다.

[!code-csharp-interactive[bitwise OR](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseOr)]

`bool` 유형의 피연산자의 경우 `|` 연산자는 해당 피연산자의 [논리 OR](boolean-logical-operators.md#logical-or-operator-)을 컴퓨팅합니다.

## <a name="compound-assignment"></a>복합 할당

이진 연산자(`op`)의 경우 양식의 복합 할당 식

```csharp
x op= y
```

위의 식은 아래의 식과 동일합니다.

```csharp
x = x op y
```

단, `x`가 한 번만 계산됩니다.

다음 예제에서는 비트 및 시프트 연산자를 사용하는 복합 할당의 사용법을 보여줍니다.

[!code-csharp-interactive[compound assignment](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#CompoundAssignment)]

[숫자 승격](~/_csharplang/spec/expressions.md#numeric-promotions)으로 인해 `op` 연산의 결과가 암시적으로 `x`의 `T` 형식으로 변환되지 못할 수 있습니다. 이 경우 `op`가 미리 정의된 연산자이고 연산의 결과가 명시적으로 `x`의 `T` 형식으로 변환 가능하다면 `x op= y` 양식의 복합 할당 식이 `x = (T)(x op y)`에 해당합니다. 단 `x`는 한 번만 평가됩니다. 다음 예제에서는 해당 동작을 보여줍니다.

[!code-csharp-interactive[compound assignment with cast](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#CompoundAssignmentWithCast)]

## <a name="operator-precedence"></a>연산자 우선 순위

다음 목록에서는 비트 및 시프트 연산자를 가장 높은 우선순위부터 가장 낮은 것으로 정렬합니다.

- 비트 보수 연산자 `~`
- 시프트 연산자 `<<` 및 `>>`
- 논리 AND 연산자 `&`
- 논리 배타적 OR 연산자 `^`
- 논리 OR 연산자 `|`

괄호(`()`)를 사용하여 연산자 우선 순위에 따라 주어진 평가 순서를 변경합니다.

[!code-csharp-interactive[operator precedence](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#Precedence)]

우선 순위 수준에 따라 정렬된 전체 연산자 목록은 [C# 연산자](index.md)를 참조하세요.

## <a name="shift-count-of-the-shift-operators"></a>시프트 연산자의 시프트 수

시트프 연산자 `<<` 및 `>>`의 경우 오른쪽 피연산자의 형식은 [int](../builtin-types/integral-numeric-types.md)이거나 `int`로의 [미리 정의된 암시적 숫자 변환](../keywords/implicit-numeric-conversions-table.md)이 있는 형식이어야 합니다.

`x << count` 및 `x >> count`식의 경우 실제 시프트 수는 다음과 같이 `x` 형식에 따라 달라집니다.

- `x`의 형식이 [int](../builtin-types/integral-numeric-types.md) 또는 [uint](../builtin-types/integral-numeric-types.md)이면 시프트 수는 오른쪽 피연산자의 하위 *5*비트로 정의됩니다. 즉, 시프트 수는 `count & 0x1F`(또는 `count & 0b_1_1111`)에서 계산됩니다.

- `x`의 형식이 [long](../builtin-types/integral-numeric-types.md) 또는 [ulong](../builtin-types/integral-numeric-types.md)이면 시프트 수는 오른쪽 피연산자의 하위 *6*비트로 정의됩니다. 즉, 시프트 수는 `count & 0x3F`(또는 `count & 0b_11_1111`)에서 계산됩니다.

다음 예제에서는 해당 동작을 보여줍니다.

[!code-csharp-interactive[shift count example](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#ShiftCount)]

## <a name="enumeration-logical-operators"></a>열거형 논리 연산자

`~`, `&`, `|` 및 `^` 연산자도 [열거형](../keywords/enum.md) 형식에 대해 정의됩니다. 동일한 열거형 형식의 피연산자인 경우, 기본 정수 형식의 해당 값에 대해 논리 연산을 수행됩니다. 예를 들어 기본 형식이 `U`인 열거형 형식 `T`의 `x` 및 `y`에 대해 `x & y` 식은 `(T)((U)x & (U)y)` 식과 동일한 결과를 생성합니다.

일반적으로 [Flags](xref:System.FlagsAttribute) 특성으로 정의된 열거형 형식을 가진 비트 논리 연산자를 사용합니다. 자세한 내용은 [열거형 형식](../../programming-guide/enumeration-types.md) 문서의 [비트 플래그로서 열거형 형식](../../programming-guide/enumeration-types.md#enumeration-types-as-bit-flags)을 참조하세요.

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

사용자 정의 형식은 `~`, `<<`, `>>`, `&`, `|` 및 `^` 연산자를 [오버로드](operator-overloading.md)할 수 있습니다. 이항 연산자가 오버로드되면 해당하는 복합 대입 연산자도 암시적으로 오버로드됩니다. 사용자 정의 형식은 복합 대입 연산자를 명시적으로 오버로드할 수 없습니다.

사용자 정의 형식 `T`가 `<<` 또는 `>>` 연산자를 오버로드하는 경우 첫 번째 피연산자의 형식은 `T`여야 하고, 두 번째 피연산자의 형식은 `int`여야 합니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 다음 섹션을 참조하세요.

- [비트 보수 연산자](~/_csharplang/spec/expressions.md#bitwise-complement-operator)
- [시프트 연산자](~/_csharplang/spec/expressions.md#shift-operators)
- [논리 연산자](~/_csharplang/spec/expressions.md#logical-operators)
- [복합 할당](~/_csharplang/spec/expressions.md#compound-assignment)
- [숫자 승격](~/_csharplang/spec/expressions.md#numeric-promotions)

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [부울 논리 연산자](boolean-logical-operators.md)
