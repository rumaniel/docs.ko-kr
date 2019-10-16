---
title: C# 7.1의 새로운 기능
description: C# 7.1의 새로운 기능에 대한 개요입니다.
ms.date: 04/09/2019
ms.openlocfilehash: ee68cbf129d02fc58155a603d6a3f63cfb182cd0
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70105547"
---
# <a name="whats-new-in-c-71"></a>C# 7.1의 새로운 기능

C# 7.1은 C# 언어에 대한 첫 번째 포인트 릴리스입니다. 언어에 대한 증가된 릴리스 일정을 표시합니다. 새로운 각 기능이 준비될 때 이상적으로 새 기능을 빨리 사용할 수 있습니다. C# 7.1은 지정된 버전의 언어와 일치하도록 컴파일러를 구성하는 기능을 추가합니다. 이를 통해 도구를 업그레이드하는 결정을 언어 버전을 업그레이드하는 결정에서 구분할 수 있습니다.

C# 7.1은 [언어 버전 선택](../language-reference/configure-language-version.md) 구성 요소, 세 개의 새로운 언어 기능 및 새로운 컴파일러 동작을 추가합니다.

이 릴리스의 새로운 언어 기능은 다음과 같습니다.

- [`async` `Main`메서드](#async-main)
  - 애플리케이션에 대한 진입점은 `async` 한정자를 가질 수 있습니다.
- [`default` 리터럴 식](#default-literal-expressions)
  - 대상 형식을 유추할 수 있는 경우 기본 값 식에서 기본 리터럴 식을 사용할 수 있습니다.
- [유추된 튜플 요소 이름](#inferred-tuple-element-names)
  - 튜플 요소의 이름은 대부분의 경우에 튜플 초기화에서 유추할 수 있습니다.
- [제네릭 형식 매개 변수의 패턴 일치](#pattern-matching-on-generic-type-parameters)
  - 형식이 제네릭 형식 매개 변수인 변수에서 패턴 일치 식을 사용할 수 있습니다.

마지막으로 컴파일러에는 [참조 어셈블리 생성](#reference-assembly-generation)을 제어하는 두 가지 옵션 `-refout` 및 `-refonly`가 있습니다.

포인트 릴리스에서 최신 기능을 사용하려면 [컴파일러 언어 버전을 구성](../language-reference/configure-language-version.md)하고 해당 버전을 선택해야 합니다.

이 문서의 나머지 부분에서는 해당 기능에 대한 개요를 제공합니다. 각 기능의 배경과 원리를 알아봅니다. 구문을 알아봅니다. `dotnet try` 글로벌 도구를 사용하여 환경에서 다음과 같은 기능을 탐색할 수 있습니다.

1. [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) 글로벌 도구를 설치합니다.
1. [dotnet/try-samples](https://github.com/dotnet/try-samples) 리포지토리를 복제합니다.
1. 현재 디렉터리를 *try-samples* 리포지토리의 *csharp7* 하위 디렉터리로 설정합니다.
1. `dotnet try`를 실행합니다.

## <a name="async-main"></a>비동기 기본

*비동기 기본* 메서드를 통해 `Main` 메서드에서 `await`를 사용할 수 있습니다.
이전에 다음을 작성해야 했습니다.

```csharp
static int Main()
{
    return DoAsyncWork().GetAwaiter().GetResult();
}
```

이제 다음을 작성할 수 있습니다.

```csharp
static async Task<int> Main()
{
    // This could also be replaced with the body
    // DoAsyncWork, including its await expressions:
    return await DoAsyncWork();
}
```

프로그램이 종료 코드를 반환하지 않는 경우 <xref:System.Threading.Tasks.Task>를 반환하는 `Main` 메서드를 선언할 수 있습니다.

```csharp
static async Task Main()
{
    await SomeAsyncMethod();
}
```

프로그래밍 가이드의 [비동기 기본](../programming-guide/main-and-command-args/index.md) 문서에서 세부 정보에 대해 자세히 읽어볼 수 있습니다.

## <a name="default-literal-expressions"></a>기본 리터럴 식

기본 리터럴 식은 기본값 식에 대한 향상된 기능입니다.
이러한 식은 변수를 기본 값으로 초기화합니다. 여기서 이전에 다음을 작성했습니다.

```csharp
Func<string, bool> whereClause = default(Func<string, bool>);
```

이제 초기화의 오른쪽에서 형식을 생략할 수 있습니다.

```csharp
Func<string, bool> whereClause = default;
```

자세한 내용은 [기본 연산자](../language-reference/operators/default.md) 문서의 [기본 리터럴](../language-reference/operators/default.md#default-literal) 섹션을 참조하세요.

## <a name="inferred-tuple-element-names"></a>유추된 튜플 요소 이름

이 기능은 C# 7.0에 도입된 튜플 기능에 대한 작은 향상된 기능입니다. 여러 번 튜플을 초기화할 때 할당의 오른쪽에 사용되는 변수는 튜플 요소에 대해 원하는 이름과 동일합니다.

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count: count, label: label);
```

튜플 요소의 이름은 C# 7.1에서 튜플을 초기화하는 데 사용되는 변수에서 유추할 수 있습니다.

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```

[튜플](../tuples.md) 문서에서 이 기능에 대해 자세히 알아볼 수 있습니다.

## <a name="pattern-matching-on-generic-type-parameters"></a>제네릭 형식 매개 변수의 패턴 일치

C# 7.1부터 `is` 및 `switch` 형식 패턴의 패턴 식에는 제네릭 형식 매개 변수의 형식이 포함될 수 있습니다. 이 방법은 `struct` 또는 `class` 형식 중 하나일 수 있는 형식을 확인하고 boxing을 방지하려는 경우에 가장 유용합니다.

## <a name="reference-assembly-generation"></a>참조 어셈블리 생성

*참조 전용 어셈블리*인 [-refout](../language-reference/compiler-options/refout-compiler-option.md) 및 [-refonly](../language-reference/compiler-options/refonly-compiler-option.md)를 생성하는 두 개의 새로운 컴파일러 옵션이 있습니다.
연결된 문서에서는 이러한 옵션과 참조 어셈블리를 보다 자세히 설명합니다.
