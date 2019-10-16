---
title: 형식 테스트 및 캐스트 연산자 - C# 참조
description: 식 결과의 형식을 검사하고, 필요한 경우 다른 형식으로 변환하는 데 사용할 수 있는 C# 연산자에 대해 알아봅니다.
ms.date: 06/21/2019
author: pkulikov
f1_keywords:
- is_CSharpKeyword
- as_CSharpKeyword
- ()_CSharpKeyword
- typeof_CSharpKeyword
helpviewer_keywords:
- type-testing operators [C#]
- conversion operators [C#]
- type conversion [C#]
- is operator [C#]
- as operator [C#]
- cast operator [C#]
- cast expression [C#]
- () operator [C#]
- typeof operator [C#]
ms.openlocfilehash: 62186409fdc1abb2275af535be3ae939a1e63323
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922289"
---
# <a name="type-testing-and-cast-operators-c-reference"></a>형식 테스트 및 캐스트 연산자(C# 참조)

다음 연산자를 사용하여 형식 검사 또는 형식 변환을 수행할 수 있습니다.

- [is 연산자](#is-operator): 식의 런타임 형식이 지정된 형식과 호환되는지 확인합니다.
- [as 연산자](#as-operator): 런타임 형식이 지정된 형식과 호환되는 경우 식을 해당 형식으로 명시적으로 변환합니다.
- [캐스트 연산자 ()](#cast-operator-): 명시적 변환을 수행합니다.
- [typeof 연산자](#typeof-operator): 형식의 <xref:System.Type?displayProperty=nameWithType> 인스턴스를 가져옵니다.

## <a name="is-operator"></a>is 연산자

`is` 연산자는 식 결과의 런타임 형식이 지정된 형식과 호환되는지 확인합니다. C# 7.0부터, `is` 연산자는 식 결과에 패턴이 있는지도 테스트합니다.

형식 테스트 `is` 연산자가 포함된 식의 양식은 다음과 같습니다.

```csharp
E is T
```

여기서 `E`는 값을 반환하는 식이고, `T`는 형식 또는 형식 매개 변수의 이름입니다. `E`은 무명 메서드 또는 람다 식일 수 없습니다.

`E is T` 식은 `E`의 결과가 null이 아니고 참조 변환, boxing 변환 또는 unboxing 변환을 통해 `T` 형식으로 변환될 수 있는 경우 `true`를 반환하고, 변환될 수 없으면 `false`를 반환합니다. `is` 연산자는 사용자 정의 변환을 고려하지 않습니다.

다음 예제에서는 식 결과의 런타임 형식이 지정된 형식에서 파생되는 경우, 즉 형식 간에 참조 변환이 있는 경우 `is` 연산자가 `true`를 반환하는 것을 보여 줍니다.

[!code-csharp[is with reference conversion](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#IsWithReferenceConversion)]

다음 예제에서는 `is` 연산자가 boxing 및 unboxing 변환은 고려하지만 숫자 변환을 고려하지 않는 것을 보여 줍니다.

[!code-csharp-interactive[is with int](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#IsWithInt)]

C# 변환에 대한 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [변환](~/_csharplang/spec/conversions.md) 장을 참조하세요.

### <a name="type-testing-with-pattern-matching"></a>패턴 일치를 사용한 형식 테스트

C# 7.0부터, `is` 연산자는 식 결과에 패턴이 있는지도 테스트합니다. 특히, 다음 형태의 양식 패턴을 지원합니다.

```csharp
E is T v
```

여기서 `E`는 값을 반환하는 식이고, `T`는 형식 또는 형식 매개 변수의 이름이며, `v`는 `T` 형식의 새 로컬 변수입니다. `E`의 결과가 null이 아니고 참조, boxing 또는 unboxing 변환을 통해 `T`로 변환될 수 있는 경우 `E is T v` 식이 `true`를 반환하고 `E` 결과의 변환된 값이 `v` 변수에 할당됩니다.

다음 예제에서는 형식 패턴과 `is` 연산자를 사용하는 방법을 보여 줍니다.

[!code-csharp-interactive[is with type pattern](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#IsTypePattern)]

형식 패턴 및 기타 지원되는 패턴에 대한 자세한 내용은 [is를 사용한 패턴 일치](../keywords/is.md#pattern-matching-with-is)를 참조하세요.

## <a name="as-operator"></a>as 연산자

`as` 연산자는 식의 결과를 지정된 참조 또는 nullable 값 형식으로 명시적으로 변환합니다. 변환할 수 없는 경우 `as` 연산자가 `null`을 반환합니다. [캐스트 연산자 ()](#cast-operator-)와 달리, `as` 연산자는 예외를 throw하지 않습니다.

다음 형태의 식이 있다고 가정합니다.

```csharp
E as T
```

여기서 `E`는 값을 반환하는 식이고, `T`는 형식 또는 형식 매개 변수의 이름입니다. 이 식은 다음과 동일한 결과를 생성합니다.

```csharp
E is T ? (T)(E) : (T)null
```

단, `E`가 한 번만 계산됩니다.

`as` 연산자는 참조, nullable, boxing 및 unboxing 변환만 고려합니다. `as` 연산자를 사용하여 사용자 정의 변환을 수행할 수는 없습니다. 사용자 정의 변환을 수행하려면 [캐스트 연산자 ()](#cast-operator-)를 사용합니다.

다음 예제에서는 `as` 연산자의 사용법을 보여 줍니다.

[!code-csharp-interactive[as operator](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#AsOperator)]

> [!NOTE]
> 앞의 예제와 같이, `as` 식의 결과를 `null`과 비교하여 변환에 성공했는지 확인해야 합니다. C# 7.0부터, [is 연산자](#type-testing-with-pattern-matching)를 사용하여 변환에 성공하는지 테스트하고, 성공한 경우 해당 결과를 새 변수에 할당할 수 있습니다.

## <a name="cast-operator-"></a>캐스트 연산자 ()

`(T)E` 형태의 캐스트 식은 `E` 식의 결과를 `T` 형식으로 명시적으로 변환합니다. `E` 형식에서 `T` 형식으로의 명시적 변환이 없는 경우 컴파일 시간 오류가 발생합니다. 런타임에 명시적 변환이 실패하고 캐스트 식이 예외를 throw할 수도 있습니다.

다음 예제에서는 명시적 숫자 및 참조 변환을 보여 줍니다.

[!code-csharp-interactive[cast expression](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#Cast)]

지원되는 명시적 변환에 대한 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [명시적 변환](~/_csharplang/spec/conversions.md#explicit-conversions) 섹션을 참조하세요. 사용자 지정 명시적 또는 암시적 형식 변환을 정의하는 방법에 대한 자세한 내용은 [사용자 정의 변환 연산자](user-defined-conversion-operators.md)를 참조하세요.

### <a name="other-usages-of-"></a>다른 () 용도

[메서드 또는 대리자를 호출](member-access-operators.md#invocation-operator-)하는 경우에도 괄호를 사용합니다.

괄호를 사용하여 식에서 연산을 계산하는 순서를 조정하기도 합니다. 자세한 내용은 [C# 연산자](index.md)를 참조하세요.

## <a name="typeof-operator"></a>typeof 연산자

`typeof` 연산자는 형식의 <xref:System.Type?displayProperty=nameWithType> 인스턴스를 가져옵니다. `typeof` 연산자의 인수는 다음 예제와 같이 형식 또는 형식 매개 변수의 이름이어야 합니다.

[!code-csharp-interactive[typeof operator](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#TypeOf)]

바인딩되지 않은 제네릭 형식과 `typeof` 연산자를 사용할 수도 있습니다. 바인딩되지 않은 제네릭 형식의 이름에는 형식 매개 변수 개수보다 하나 더 적은 적절한 개수의 쉼표가 포함되어야 합니다. 다음 예제에서는 바인딩되지 않은 제네릭 형식과 `typeof` 연산자를 사용하는 방법을 보여 줍니다.

[!code-csharp-interactive[typeof unbound generic](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#TypeOfUnboundGeneric)]

식은 `typeof` 연산자의 인수가 될 수 없습니다. 식 결과의 런타임 형식에 대한 <xref:System.Type?displayProperty=nameWithType> 인스턴스를 가져오려면 <xref:System.Object.GetType%2A?displayProperty=nameWithType> 메서드를 사용합니다.

### <a name="type-testing-with-the-typeof-operator"></a>`typeof` 연산자를 사용한 형식 테스트

`typeof` 연산자를 사용하여 식 결과의 런타임 형식이 지정된 형식과 정확히 일치하는지 확인합니다. 다음 예제에서는 `typeof` 연산자와 [is 연산자](#is-operator)를 사용한 형식 검사의 차이점을 보여 줍니다.

[!code-csharp[typeof vs is](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#TypeCheckWithTypeOf)]

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

`is`, `as` 및 `typeof` 연산자는 오버로드할 수 없습니다.

사용자 정의 형식은 `()` 연산자를 오버로드할 수 없지만, 캐스트 식에서 수행할 수 있는 사용자 지정 형식 변환을 정의할 수 있습니다. 자세한 내용은 [사용자 정의 변환 연산자](user-defined-conversion-operators.md)를 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 다음 섹션을 참조하세요.

- [is 연산자](~/_csharplang/spec/expressions.md#the-is-operator)
- [as 연산자](~/_csharplang/spec/expressions.md#the-as-operator)
- [캐스트 식](~/_csharplang/spec/expressions.md#cast-expressions)
- [typeof 연산자](~/_csharplang/spec/expressions.md#the-typeof-operator)

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [방법: 패턴 일치와 is 및 as 연산자를 사용하여 안전하게 캐스트](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)
