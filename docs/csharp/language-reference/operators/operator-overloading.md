---
title: 연산자 오버로드 - C# 참조
description: C# 연산자를 오버로드하는 방법과 오버로드가 가능한 C# 연산자에 대해 알아봅니다.
ms.date: 07/05/2019
f1_keywords:
- operator_CSharpKeyword
helpviewer_keywords:
- operator keyword [C#]
- operator overloading [C#]
ms.openlocfilehash: 130eb4be66d13b43e5605ef98a647fa9f4223014
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71116086"
---
# <a name="operator-overloading-c-reference"></a>연산자 오버로드(C# 참조)

사용자 정의 형식은 미리 정의된 C# 연산자를 오버로드할 수 있습니다. 즉, 피연산자 중 하나 또는 두 개가 해당 형식일 때 형식은 작업의 사용자 정의 구현을 제공할 수 있습니다. [오버로드할 수 있는 연산자](#overloadable-operators) 섹션에는 오버로드할 수 있는 C# 연산자가 나와 있습니다.

`operator` 키워드를 사용하여 연산자를 선언합니다. 연산자 선언은 다음 규칙을 충족해야 합니다.

- `public` 및 `static` 한정자를 모두 포함합니다.
- 단항 연산자는 하나의 매개 변수를 사용합니다. 이항 연산자는 두 개의 매개 변수를 사용합니다. 각각의 경우 하나 이상의 매개 변수가 `T` 또는 `T?` 유형을 가져야 하며, 여기서 `T`는 연산자 선언이 포함된 유형입니다.

다음 예제에서는 유리수를 나타내는 간단한 구조를 정의합니다. 구조체가 [산술 연산자](arithmetic-operators.md) 중 일부를 오버로드합니다.

[!code-csharp[fraction example](~/samples/csharp/language-reference/operators/OperatorOverloading.cs)]

암시적 변환을 `int`에서 `Fraction`으로 정의하여 앞의 예제를 확장할 수 있습니다. 그런 다음, 오버로드된 연산자는 해당 두 형식의 인수를 지원합니다. 즉, 분수에 정수를 추가하고 그 결과로 분수를 얻을 수 있습니다.

또한 `operator` 키워드를 사용하여 사용자 지정 형식 변환을 정의합니다. 자세한 내용은 [사용자 정의 변환 연산자](user-defined-conversion-operators.md)를 참조하세요.

## <a name="overloadable-operators"></a>오버로드할 수 있는 연산자

다음 표는 C# 연산자의 오버로드 가능성에 대한 정보를 제공합니다.

| 연산자 | 오버로드 가능성 |
| --------- | --------------- |
|[+x](arithmetic-operators.md#unary-plus-and-minus-operators), [-x](arithmetic-operators.md#unary-plus-and-minus-operators), [!x](boolean-logical-operators.md#logical-negation-operator-), [~x](bitwise-and-shift-operators.md#bitwise-complement-operator-), [++](arithmetic-operators.md#increment-operator-), [--](arithmetic-operators.md#decrement-operator---), [true](true-false-operators.md), [false](true-false-operators.md)|이러한 단항 연산자는 오버로드할 수 있습니다.|
|[x + y](addition-operator.md), [x - y](subtraction-operator.md), [x \* y](arithmetic-operators.md#multiplication-operator-), [x / y](arithmetic-operators.md#division-operator-), [x % y](arithmetic-operators.md#remainder-operator-), [x & y](boolean-logical-operators.md#logical-and-operator-), [x &#124; y](boolean-logical-operators.md#logical-or-operator-), [x ^ y](boolean-logical-operators.md#logical-exclusive-or-operator-), [x \<\< y](bitwise-and-shift-operators.md#left-shift-operator-), [x >> y](bitwise-and-shift-operators.md#right-shift-operator-), [x == y](equality-operators.md#equality-operator-), [x != y](equality-operators.md#inequality-operator-), [x \< y](comparison-operators.md#less-than-operator-), [x > y](comparison-operators.md#greater-than-operator-), [x \<= y](comparison-operators.md#less-than-or-equal-operator-), [x >= y](comparison-operators.md#greater-than-or-equal-operator-)|이러한 이항 연산자는 오버로드할 수 있습니다. 특정 연산자는 쌍으로 오버로드되어야 합니다. 자세한 내용은 이 표 다음에 나오는 참고 사항을 참조하세요.|
|[x && y](boolean-logical-operators.md#conditional-logical-and-operator-), [x &#124;&#124; y](boolean-logical-operators.md#conditional-logical-or-operator-)|조건부 논리 연산자는 오버로드할 수 없습니다. 그러나 오버로드된 [`true` 및 `false` 연산자](true-false-operators.md)가 있는 형식도 특정 방식으로 `&` 또는 <code>&#124;</code> 연산자를 오버로드하는 경우, `&&` 또는 <code>&#124;&#124;</code> 연산자는 각각 해당 유형의 피연산자에 대해 평가될 수 있습니다. 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [사용자 정의 조건부 논리 연산자](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators) 섹션을 참조하세요.|
|[a&#91;i&#93;](member-access-operators.md#indexer-operator-)|요소 액세스는 오버로드 가능한 연산자로 간주되지 않지만 [인덱서](../../programming-guide/indexers/index.md)를 정의할 수 있습니다.|
|[(T)x](type-testing-and-cast.md#cast-operator-)|캐스트 연산자는 오버로드할 수 없지만 새 변환 연산자를 정의할 수 있습니다. 자세한 내용은 [사용자 정의 변환 연산자](user-defined-conversion-operators.md)를 참조하세요.|
|[+=](arithmetic-operators.md#compound-assignment), [-=](arithmetic-operators.md#compound-assignment), [\*=](arithmetic-operators.md#compound-assignment), [/=](arithmetic-operators.md#compound-assignment), [%=](arithmetic-operators.md#compound-assignment), [&=](boolean-logical-operators.md#compound-assignment), [&#124;=](boolean-logical-operators.md#compound-assignment), [^=](boolean-logical-operators.md#compound-assignment), [\<\<=](bitwise-and-shift-operators.md#compound-assignment), [>>=](bitwise-and-shift-operators.md#compound-assignment)|복합 할당 연산자를 명시적으로 오버로드할 수 없습니다. 그러나 이항 연산자가 오버로드되면 해당 복합 할당 연산자(있는 경우)도 암시적으로 오버로드됩니다. 예를 들어 `+=`는 오버로드될 수 있는 `+`를 사용하여 계산됩니다.|
|[^x](member-access-operators.md#index-from-end-operator-), [x = y](assignment-operator.md), [x.y](member-access-operators.md#member-access-operator-), [c ? t : f](conditional-operator.md), [x ?? y](null-coalescing-operator.md), [x ??= y](null-coalescing-operator.md), [x..y](member-access-operators.md#range-operator-), [x->y](pointer-related-operators.md#pointer-member-access-operator--), [=>](lambda-operator.md), [f(x)](member-access-operators.md#invocation-operator-), [as](type-testing-and-cast.md#as-operator), [await](await.md), [checked](../keywords/checked.md), [unchecked](../keywords/unchecked.md), [default](default.md), [delegate](delegate-operator.md), [is](type-testing-and-cast.md#is-operator), [nameof](nameof.md), [new](new-operator.md), [sizeof](sizeof.md), [stackalloc](stackalloc.md), [typeof](type-testing-and-cast.md#typeof-operator)|이러한 연산자는 오버로드할 수 없습니다.|

> [!NOTE]
> 비교 연산자는 쌍으로 오버로드되어야 합니다. 즉, 쌍 중 하나의 연산자가 오버로드되면 다른 연산자도 오버로드되어야 합니다. 이러한 쌍은 다음과 같습니다.
>
> - `==` 및 `!=` 연산자
> - `<` 및 `>` 연산자
> - `<=` 및 `>=` 연산자

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 다음 섹션을 참조하세요.

- [연산자 오버로드](~/_csharplang/spec/expressions.md#operator-overloading)
- [연산자](~/_csharplang/spec/classes.md#operators)

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [사용자 정의 전환 연산자](user-defined-conversion-operators.md)
- [Why are overloaded operators always static in C#?](https://blogs.msdn.microsoft.com/ericlippert/2007/05/14/why-are-overloaded-operators-always-static-in-c/)(오버로드된 연산자가 C#에서 항상 정적인 이유)
