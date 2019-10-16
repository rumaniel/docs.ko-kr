---
title: true 및 false 연산자 - C# 참조
ms.custom: seodec18
ms.date: 12/10/2018
helpviewer_keywords:
- false operator [C#]
- true operator [C#]
ms.assetid: 81a888fd-011e-4589-b242-6c261fea505e
ms.openlocfilehash: 7cbfca932b5f9f8a6f658e84204da5005da5ffb8
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67609833"
---
# <a name="true-and-false-operators-c-reference"></a>true 및 false 연산자(C# 참조)

`true` 연산자는 [부울](../keywords/bool.md) 값을 반환하여 `true` 피연산자가 확실히 true임을 나타냅니다. `false` 연산자는 `bool` 값을 반환하여 `true` 피연산자가 확실히 false임을 나타냅니다. `true` 및 `false` 연산자는 서로를 보완한다고 보장되지 않습니다. 즉, `true` 및 `false` 연산자는 모두 `bool` 값을 동일한 `false` 피연산자에 반환할 수도 있습니다. 형식이 두 연산자 중 하나를 정의하는 경우 나머지 연산자도 정의해야 합니다.

> [!TIP]
> 예를 들어 값이 세 개인 논리를 지원해야 하는 경우(예: 값이 세 개인 부울 형식을 지원하는 데이터베이스에서 작업하는 경우) `bool?` 형식을 사용합니다. C#은 `bool?` 피연산자를 사용하여 값이 세 개인 논리를 지원하는 `&` 및 `|` 연산자를 제공합니다. 자세한 내용은 [부울 논리 연산자](boolean-logical-operators.md) 문서의 [Nullable 부울 논리 연산자](boolean-logical-operators.md#nullable-boolean-logical-operators) 섹션을 참조하세요.

## <a name="boolean-expressions"></a>부울 식

정의된 `true` 연산자가 있는 형식은 [if](../keywords/if-else.md), [do](../keywords/do.md), [while](../keywords/while.md) 및 [for](../keywords/for.md) 문과 [조건부 연산자`?:`](conditional-operator.md)에서 제어하는 조건식의 결과 형식일 수 있습니다. 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [부울 식](~/_csharplang/spec/expressions.md#boolean-expressions) 섹션을 참조하세요.

## <a name="user-defined-conditional-logical-operators"></a>사용자 지정 조건부 논리 연산자

정의된 `true` 및 `false` 연산자가 있는 형식이 특정 방식으로 [논리적 OR 연산자](boolean-logical-operators.md#logical-or-operator-) `|` 또는 [논리적 AND 연산자](boolean-logical-operators.md#logical-and-operator-) `&`를 [오버로드](operator-overloading.md)하는 경우, [조건부 논리적 OR 연산자](boolean-logical-operators.md#conditional-logical-or-operator-) `||` 또는 [조건부 논리적 AND 연산자](boolean-logical-operators.md#conditional-logical-and-operator-) `&&`가 해당 형식의 피연산자에 대해 각각 계산될 수 있습니다. 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [사용자 정의 조건부 논리 연산자](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators) 섹션을 참조하세요.

## <a name="example"></a>예

다음 예제는 `true` 및 `false` 연산자를 둘 다 정의하는 형식을 제공합니다. `&&` 연산자도 해당 형식의 피연산자에 대해 계산될 수 있는 방식으로 논리적 AND 연산자 `&`를 오버로드합니다.

[!code-csharp[true and false operators example](~/samples/csharp/language-reference/operators/TrueFalseOperators.cs)]

`&&` 연산자의 단락 동작을 확인합니다. `GetFuelLaunchStatus` 메서드가 `LaunchStatus.Red`를 반환하면 `&&` 연산자의 오른쪽 피연산자는 계산되지 않습니다. `LaunchStatus.Red`가 확실히 false이기 때문입니다. 따라서 논리적 AND의 결과가 오른쪽 피연산자의 값에 종속되지 않습니다. 예제 출력은 다음과 같습니다.

```console
Getting fuel launch status...
Wait!
```

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [true 리터럴](../keywords/true-literal.md)
- [false 리터럴](../keywords/false-literal.md)
