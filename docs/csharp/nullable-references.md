---
title: nullable 참조 형식
description: 이 문서에서는 C# 8에 추가된 nullable 참조 형식에 대해 간략하게 설명합니다. 이 기능이 신규 및 기존의 프로젝트의 null 참조 예외에 대해 어떻게 안전성을 제공하는지 알아봅니다.
ms.date: 02/19/2019
ms.openlocfilehash: 213f0e3d9ad84628dab02a1dc483513783b2ad6e
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699953"
---
# <a name="nullable-reference-types"></a>nullable 참조 형식

C# 8.0에는 참조 형식 변수의 속성에 대한 중요한 설명을 할 수 있는 **nullable 참조 형식**과 **nullable이 아닌 참조 형식**이 도입되었습니다.

- **참조에 null이 허용되지 않습니다**. 변수에 null이 허용되지 않는 경우 컴파일러는 null이 아닌지 먼저 확인하지 않고 이러한 참조를 역참조하기에 안전한지 확인하는 규칙을 적용합니다.
  - 이 변수는 null이 아닌 값으로 초기화되어야 합니다.
  - 이 변수에는 `null` 값을 절대로 할당할 수 없습니다.
- **참조에 null이 허용됩니다**. 변수에 null이 허용되는 경우 컴파일러는 null 참조 검사를 제대로 했는지 확인하는 다른 규칙을 적용합니다.
  - 컴파일러가 해당 값이 null이 아님을 보장할 수 있는 경우에만 변수를 역참조할 수 있습니다.
  - 이러한 변수는 기본 `null` 값으로 초기화할 수 있으며 다른 코드에서 `null` 값을 할당할 수 있습니다.

이 새로운 기능은 변수 선언에서 설계 의도를 파악할 수 없었던 이전 버전의 C#에 비해 참조 변수 처리에 관한 상당한 이점을 제공합니다. 기존 컴파일러는 참조 형식의 null 참조 예외에 대해 안전성을 제공하지 않았습니다.

- **참조가 null일 수 있습니다**. 참조 형식이 null로 초기화되거나 나중에 null이 할당되는 경우 경고가 발생하지 않습니다.
- **참조가 null이 아닌 것으로 간주됩니다**. 컴파일러는 참조 형식이 역참조될 때 어떠한 경고도 발생시키지 않습니다. (nullable 참조인 경우 컴파일러는 null일 수 있는 변수를 역참조할 때마다 경고를 발생시킵니다).

Nullable 참조 형식을 추가함으로써 의도를 보다 명확하게 선언할 수 있습니다. `null` 값은 변수가 값을 참조하지 않음을 나타내는 올바른 방법입니다. 코드에서 모든 `null` 값을 제거하는 데 이 기능을 사용하지 마세요. 대신, 컴파일러 및 코드를 읽는 다른 개발자에게 의도를 선언해야 합니다. 의도를 선언해 놓으면 컴파일러는 해당 의도와 일치하지 않는 코드 작성 시 이를 알려줍니다.

**nullable 참조 형식**은 [nullable 값 형식](programming-guide/nullable-types/index.md)과 동일한 구문을 사용하여 작성합니다. 변수 형식에 `?`가 추가됩니다. 예를 들어 다음 변수 선언은 nullable 문자열 변수 `name`을 나타냅니다.

```csharp
string? name;
```

형식 이름에 `?`가 추가되지 않은 모든 변수는 **nullable이 아닌 참조 형식**입니다. 여기에는 이 기능을 설정한 기존 코드에 있는 모든 참조 형식 변수가 포함됩니다.

컴파일러는 정적 분석을 사용하여 nullable 참조가 null이 아닌 것으로 알려져 있는지 확인합니다. 컴파일러는 null일 수 있는 nullable 참조를 역참조하는 경우 경고를 표시합니다. 변수 이름 뒤에 **null 허용 연산자** `!`를 사용하여 이 동작을 재정의할 수 있습니다. 예를 들어 `name` 변수가 null이 아닌 것으로 알고 있는데 컴파일러 경고가 발생하는 경우 다음 코드를 작성하여 컴파일러 분석을 재정의할 수 있습니다.

```csharp
name!.Length;
```

이 연산자에 대한 자세한 내용은 GitHub의 [nullable 참조 형식 사양 제안 초안](../../_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator)에서 확인할 수 있습니다.

## <a name="nullability-of-types"></a>형식의 Null 허용 여부

모든 참조 형식은 경고가 생성되는 경우를 설명하는 4가지 *nullabilities(Null 허용 여부)* 중 하나일 수 있습니다.

- *Nonnullable(Null 허용 안 함)* : 이 형식의 변수에는 null을 할당할 수 없습니다. 이 형식의 변수는 역참조되기 전에 null 검사가 필요하지 않습니다.
- *Nullable(Null 허용)* : 이 형식의 변수에는 null을 할당할 수 있습니다. `null`에 대한 사전 검사 없이 이 형식의 변수를 역참조하면 경고가 발생합니다.
- *Oblivious(모호한)* : C# 8 이전 상태입니다. 이 형식의 변수는 경고 없이 역참조되거나 할당될 수 있습니다.
- *Unknown(알 수 없음)* : 형식이 *nullable* 또는 *nonnullable*이어야 하는지 제약 조건으로 컴파일러에 명시하지 않은 형식 매개 변수에 일반적입니다.

변수 선언에서 형식의 null 허용 여부는 변수가 선언된 *nullable 컨텍스트*로 제어됩니다.

## <a name="nullable-contexts"></a>Nullable 컨텍스트

Nullable 컨텍스트를 통해 컴파일러가 참조 형식 변수를 해석하는 방식을 미세하게 제어할 수 있습니다. 지정된 소스 줄의 **nullable 주석 컨텍스트**는 `enabled` 또는 `disabled`입니다. C# 8 이전 컴파일러는 `disabled` nullable 컨텍스트에서 모든 코드를 컴파일하는 것으로 생각할 수 있습니다. 모든 참조 형식은 null일 수 있습니다. **nullable 경고 컨텍스트**는 `enabled` 또는 `disabled`로 설정할 수 있습니다. nullable 경고 컨텍스트는 컴파일러가 해당 흐름 분석을 사용하여 생성한 경고를 지정합니다.

*.csproj* 파일에 `Nullable` 요소를 사용하여 프로젝트에 대한 nullable 주석 컨텍스트 및 nullable 경고 컨텍스트를 설정할 수 있습니다. 이 요소는 컴파일러가 형식의 null 허용 여부를 해석하는 방법 및 생성되는 경고를 구성합니다. 유효한 설정은 다음과 같습니다.

- `enable`: nullable 주석 컨텍스트가 **enabled**입니다. nullable 경고 컨텍스트가 **enabled**입니다.
  - 예를 들어 참조 형식 변수 `string`은 null이 아닙니다.  모든 null 허용 여부 경고가 enabled입니다.
- `warnings`: nullable 주석 컨텍스트가 **disabled**입니다. nullable 경고 컨텍스트가 **enabled**입니다.
  - 참조 형식의 변수가 모호합니다. 모든 null 허용 여부 경고가 enabled입니다.
- `annotations`: nullable 주석 컨텍스트가 **enabled**입니다. nullable 경고 컨텍스트가 **disabled**입니다.
  - 참조 형식의 변수가 모호합니다. 모든 null 허용 여부 경고가 disabled입니다.
- `disable`: nullable 주석 컨텍스트가 **disabled**입니다. nullable 경고 컨텍스트가 **disabled**입니다.
  - 참조 형식의 변수는 이전 버전의 C#과 마찬가지로 모호할 수 있습니다. 모든 null 허용 여부 경고가 disabled입니다.

또한 지시문을 사용하여 프로젝트의 아무 곳에나 이러한 동일한 컨텍스트를 설정할 수도 있습니다.

- `#nullable enable`: nullable 주석 컨텍스트와 nullable 경고 컨텍스트를 **enabled**로 설정합니다.
- `#nullable disable`: nullable 주석 컨텍스트와 nullable 경고 컨텍스트를 **disabled**로 설정합니다.
- `#nullable restore`: nullable 주석 컨텍스트와 nullable 경고 컨텍스트를 프로젝트 설정으로 복원합니다.
- `#nullable disable warnings`: nullable 경고 컨텍스트를 **disabled**로 설정합니다.
- `#nullable enable warnings`: nullable 경고 컨텍스트를 **enabled**로 설정합니다.
- `#nullable restore warnings`: nullable 경고 컨텍스트를 프로젝트 설정으로 복원합니다.
- `#nullable disable annotations`: nullable 주석 컨텍스트를 **disabled**로 설정합니다.
- `#nullable enable annotations`: nullable 주석 컨텍스트를 **enabled**로 설정합니다.
- `#nullable restore annotations`: 주석 경고 컨텍스트를 프로젝트 설정으로 복원합니다.

기본 nullable 주석 및 경고 컨텍스트는 `disabled`입니다. 이 결정은 기존 코드가 변경 없이 새로운 경고를 생성하지 않고 컴파일됨을 의미합니다.

## <a name="nullable-annotation-context"></a>nullable 주석 컨텍스트

컴파일러는 disabled nullable 주석 컨텍스트에 다음 규칙을 사용합니다.

- disabled 컨텍스트에서 nullable 참조를 선언할 수 없습니다.
- 모든 참조 변수에는 null을 할당할 수 있습니다.
- 참조 형식의 변수가 역참조되면 경고가 생성되지 않습니다.
- disabled 컨텍스트에는 null 허용 연산자를 사용할 수 없습니다.

동작은 이전 버전의 C#과 같습니다.

컴파일러는 enabled nullable 주석 컨텍스트에 다음 규칙을 사용합니다.

- 모든 참조 형식의 변수는 **nullable이 아닌 참조**입니다.
- nullable이 아닌 모든 참조는 안전하게 역참조될 수 있습니다.
- 모든 nullable 참조 형식(변수 선언에서 형식 뒤에 `?` 표시)은 null일 수 있습니다. 정적 분석으로 값이 역참조될 때 null이 아닌 것으로 알려져 있는지 확인합니다. 아닌 경우 컴파일러가 경고를 생성합니다.
- null 허용 연산자를 사용하여 nullable 참조가 null이 아님을 선언할 수 있습니다.

enabled nullable 주석 컨텍스트에서 참조 형식에 추가된 `?` 문자는 **nullable 참조 형식**을 선언합니다. **null 비허용 연산자** `!`를 식 뒤에 추가하여 식이 null이 아님을 선언할 수 있습니다.

## <a name="nullable-warning-context"></a>Nullable 경고 컨텍스트

nullable 경고 컨텍스트는 nullable 주석 컨텍스트와 다릅니다. 새 주석이 해제(disabled)되어도 경고는 설정(enabled)할 수 있습니다. 컴파일러는 정적 흐름 분석을 사용하여 모든 참조에 대한 **null 상태**를 확인합니다. null 상태는 *nullable 경고 컨텍스트*가 **disabled**가 아닌 경우 **null이 아님** 또는 **null일 수 있음**입니다. 컴파일러가 **null일 수 있음**으로 확인한 경우 역참조하면 경고가 발생합니다. 참조 상태는 컴파일러가 다음 두 조건 중 하나를 확인할 수 없으면 **null일 수 있음**입니다.

1. 변수에 확실히 null이 아닌 값이 할당되었습니다.
1. 변수 또는 식이 역참조되기 전에 null 검사되었습니다.

컴파일러는 nullable 경고 컨텍스트가 `enabled`인 경우 **null일 수 있는** 상태의 변수 또는 식을 역참조할 때마다 경고를 생성합니다. 또한 nullable 주석 컨텍스트가 `enabled`인 경우 **null일 수 있는** 변수 또는 식에 null을 허용하지 않는 참조 형식이 할당되면 경고가 생성됩니다.

## <a name="learn-more"></a>자세한 정보

- [Nullable 참조 사양 초안](https://github.com/dotnet/csharplang/blob/master/proposals/csharp-8.0/nullable-reference-types-specification.md)
- [Nullable 참조 소개 자습서](tutorials/nullable-reference-types.md)
- [기존 코드베이스를 nullable 참조로 마이그레이션](tutorials/upgrade-to-nullable-references.md)
