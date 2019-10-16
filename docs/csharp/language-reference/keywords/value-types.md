---
title: 값 형식 - C# 참조
ms.custom: seodec18
ms.date: 11/26/2018
f1_keywords:
- cs.valuetypes
helpviewer_keywords:
- value types [C#]
- types [C#], value types
- C# language, value types
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
ms.openlocfilehash: 2a3e7f02ee9d210acae881edd170edbced82dab6
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353757"
---
# <a name="value-types-c-reference"></a>값 형식(C# 참조)

다음 두 가지 종류의 값 형식이 있습니다.

- [구조체](struct.md)

- [열거형](enum.md)

## <a name="main-features-of-value-types"></a>값 형식의 주요 기능

값 형식의 변수에는 형식의 값이 포함되어 있습니다. 예를 들어 `int` 형식의 변수에는 `42` 값이 포함될 수 있습니다. 이는 개체라고도 하는 형식 인스턴스에 대한 참조를 포함하는 참조 형식의 변수와 다릅니다. 값 형식의 변수에 새 값을 할당하면 해당 값이 복사됩니다. 참조 형식의 변수에 새 값을 할당하면 개체 자체가 아니라 참조가 복사됩니다.

모든 값 형식은 <xref:System.ValueType?displayProperty=nameWithType>에서 암시적으로 파생됩니다.

참조 형식과 달리 값 형식에서는 새 형식을 파생할 수 없습니다. 그러나 참조 형식과 마찬가지로 구조체가 인터페이스를 구현할 수 있습니다.

값 형식 변수는 기본적으로 `null`일 수 없습니다. 그러나 해당 [nullable 값 형식](../../programming-guide/nullable-types/index.md)의 변수는 `null`일 수 있습니다.

각 값 형식에는 해당 형식의 기본값을 초기화하는 암시적 매개 변수 없는 생성자가 있습니다. 값 형식의 기본값에 대한 자세한 내용은 [기본값 표](default-values-table.md)를 참조하세요.

## <a name="simple-types"></a>단순 형식

*단순 형식*은 C#에서 제공하는 미리 정의된 구조체 형식 세트이며, 다음과 같은 형식으로 구성됩니다.

- [정수 형식](../builtin-types/integral-numeric-types.md): 정수 숫자 형식 및 [char](char.md) 형식
- [부동 소수점 형식](../builtin-types/floating-point-numeric-types.md)
- [bool](bool.md)

단순 형식은 키워드를 통해 식별되지만, 이러한 키워드는 단순히 <xref:System> 네임스페이스에 미리 정의된 구조체 형식의 별칭입니다. 예를 들어 [int](../builtin-types/integral-numeric-types.md)는 <xref:System.Int32?displayProperty=nameWithType>의 별칭입니다. 별칭의 전체 목록은 [기본 제공 형식 표](built-in-types-table.md)를 참조하세요.

단순 형식은 특정 추가 작업을 허용한다는 점에서 다른 구조체 형식과는 다릅니다.

- 리터럴을 사용하여 단순 형식을 초기화할 수 있습니다. 예를 들어 `'A'`는 `char` 형식의 리터럴이고, `2001`은 `int` 형식의 리터럴입니다.

- [const](const.md) 키워드를 사용하여 단순 형식의 상수를 선언할 수 있습니다. 다른 구조체 형식의 상수는 사용할 수 없습니다.

- 해당 피연산자가 모두 단순 형식 상수인 상수 식은 컴파일 시간에 계산됩니다.

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [단순 형식](~/_csharplang/spec/types.md#simple-types) 섹션을 참조하세요.

## <a name="initializing-value-types"></a>값 형식 초기화

C#의 지역 변수는 사용하기 전에 초기화해야 합니다. 예를 들어 다음 예제와 같이 초기화하지 않고 지역 변수를 선언할 수 있습니다.

```csharp
int myInt;
```

초기화하기 전에는 사용할 수 없습니다. 다음 문을 사용하여 초기화할 수 있습니다.

```csharp
myInt = new int();  // Invoke parameterless constructor for int type.
```

이 문은 다음 문과 같습니다.

```csharp
myInt = 0;         // Assign an initial value, 0 in this example.
```

물론, 다음 예제와 같이 선언과 초기화를 동일한 문에 포함할 수 있습니다.

```csharp
int myInt = new int();
```

– 또는 –

```csharp
int myInt = 0;
```

[new](../operators/new-operator.md) 연산자를 사용하면 특정 형식의 매개 변수 없는 생성자가 호출되고 변수에 기본값이 할당됩니다. 앞의 예제에서는 매개 변수 없는 생성자가 `0` 값을 `myInt`에 할당했습니다. 매개 변수가 없는 생성자를 호출하여 할당된 값에 대한 자세한 내용은 [기본값 표](default-values-table.md)를 참조하세요.

사용자 정의 형식의 경우 [new](../operators/new-operator.md)를 사용하여 매개 변수 없는 생성자를 호출합니다. 예를 들어 다음 명령문은 `Point` 구조체의 매개 변수 없는 생성자를 호출합니다.

```csharp
var p = new Point(); // Invoke parameterless constructor for the struct.
```

이 호출 후에는 구조체가 한정적으로 할당된 것으로 간주됩니다. 즉, 모든 멤버가 기본값으로 초기화됩니다.

`new` 연산자에 대한 자세한 내용은 [new](../operators/new-operator.md)를 참조하세요.

숫자 형식의 출력에 서식을 지정하는 방법에 대한 자세한 내용은 [숫자 결과 형식 지정 표](formatting-numeric-results-table.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [유형](types.md)
- [참조 형식](reference-types.md)
- [Nullable 값 형식](../../programming-guide/nullable-types/index.md)
