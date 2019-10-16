---
title: + 및 += 연산자 - C# 참조
ms.custom: seodec18
ms.date: 05/24/2019
f1_keywords:
- +_CSharpKeyword
- +=_CSharpKeyword
helpviewer_keywords:
- addition operator [C#]
- concatenation operator [C#]
- delegate combination [C#]
- + operator [C#]
- addition assignment operator [C#]
- event subscription [C#]
- += operator [C#]
ms.assetid: 93e56486-bb42-43c1-bd43-60af11e64e67
ms.openlocfilehash: 41355dbadd566648b45d825cdd6515bfc6d411aa
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67610034"
---
# <a name="-and--operators-c-reference"></a>+ 및 += 연산자(C# 참조)

`+` 연산자는 기본 제공 숫자 형식, [문자열](../keywords/string.md) 및 [대리자](../keywords/delegate.md) 형식에서 지원됩니다.

산술 `+` 연산자에 대한 자세한 내용은 [산술 연산자](arithmetic-operators.md) 문서의 [단항 더하기 및 빼기 연산자](arithmetic-operators.md#unary-plus-and-minus-operators) 및 [더하기 연산자 +](arithmetic-operators.md#addition-operator-) 섹션을 참조하세요.

## <a name="string-concatenation"></a>문자열 연결

피연산자 중 하나 또는 둘 다가 [문자열](../keywords/string.md) 형식이면 `+` 연산자는 피연산자의 문자열 표현을 연결합니다.

[!code-csharp-interactive[string concatenation](~/samples/csharp/language-reference/operators/AdditionOperator.cs#AddStrings)]

C# 6부터 [문자열 보간](../tokens/interpolated.md)은 문자열 형식을 지정하는 더욱 편리한 방법을 제공합니다.

[!code-csharp-interactive[string interpolation](~/samples/csharp/language-reference/operators/AdditionOperator.cs#UseStringInterpolation)]

## <a name="delegate-combination"></a>대리자 조합

동일한 [대리자](../keywords/delegate.md) 형식의 피연산자의 경우 `+` 연산자는 호출될 때 왼쪽 피연산자를 호출한 다음, 오른쪽 피연산자를 호출하는 새 대리자 인스턴스를 반환합니다. 피연산자 중 하나라도 `null`이면 `+` 연산자는 다른 피연산자(`null`일 수도 있음)의 값을 반환합니다. 다음 예제는 `+` 연산자를 사용하여 대리자를 결합하는 방법을 보여 줍니다.

[!code-csharp-interactive[delegate combination](~/samples/csharp/language-reference/operators/AdditionOperator.cs#AddDelegates)]

대리자 제거를 수행하려면 [`-` 연산자](subtraction-operator.md#delegate-removal)를 사용합니다.

대리자 형식에 대한 자세한 내용은 [대리자](../../programming-guide/delegates/index.md)를 참조하세요.

## <a name="addition-assignment-operator-"></a>더하기 할당 연산자 +=

다음과 같은 `+=` 연산자를 사용하는 식의 경우

```csharp
x += y
```

위의 식은 아래의 식과 동일합니다.

```csharp
x = x + y
```

단, `x`가 한 번만 계산됩니다.
  
다음 예제에서는 `+=` 연산자의 사용법을 보여 줍니다.

[!code-csharp-interactive[+= examples](~/samples/csharp/language-reference/operators/AdditionOperator.cs#AddAndAssign)]

또한 [이벤트](../keywords/event.md)를 구독할 때 `+=` 연산자를 사용하여 이벤트 처리기 메서드를 지정합니다. 자세한 내용은 [방법: 이벤트 구독 및 구독 취소](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)를 참조하세요.

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

사용자 정의 형식은 `+` 연산자를 [오버로드](operator-overloading.md)할 수 있습니다. 이진 `+` 연산자가 오버로드되면 `+=` 연산자도 암시적으로 오버로드됩니다. 사용자 정의 형식에는 `+=` 연산자를 명시적으로 오버로드할 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [단항 더하기 연산자](~/_csharplang/spec/expressions.md#unary-plus-operator) 및 [더하기 연산자](~/_csharplang/spec/expressions.md#addition-operator) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [문자열 보간](../tokens/interpolated.md)
- [방법: 여러 문자열 연결](../../how-to/concatenate-multiple-strings.md)
- [대리자](../../programming-guide/delegates/index.md)
- [이벤트](../../programming-guide/events/index.md)
- [산술 연산자](arithmetic-operators.md)
- [- 및 -= 연산자](subtraction-operator.md)
