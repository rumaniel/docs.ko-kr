---
title: C# for 문
ms.date: 06/13/2018
f1_keywords:
- for
- for_CSharpKeyword
helpviewer_keywords:
- for keyword [C#]
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
ms.openlocfilehash: 61315a04ca8d5a619a3dcaf43b15a309919d3c42
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70167878"
---
# <a name="for-c-reference"></a>for(C# 참조)

`for` 문은 지정된 부울 식이 `true`로 계산되는 동안 문 또는 문 블록을 실행합니다.

`for` 문 블록 내 원하는 지점에서 [break](break.md) 문을 사용하여 루프를 중단하거나 [continue](continue.md) 문을 사용하여 루프의 다음 반복을 한 단계 실행할 수 있습니다. [goto](goto.md), [return](return.md) 또는 [throw](throw.md) 문으로 `for` 루프를 종료할 수도 있습니다.

## <a name="structure-of-the-for-statement"></a>`for` 문의 구조

`for` 문은 *initializer*, *condition* 및 *iterator* 섹션을 정의합니다.

```csharp
for (initializer; condition; iterator)
    body
```

세 개의 섹션은 모두 선택 사항입니다. 루프의 본문은 명령문 또는 명령문 블록입니다.

다음 예제에서는 모든 섹션이 정의된 `for` 문을 보여 줍니다.

[!code-csharp-interactive[for loop example](~/samples/snippets/csharp/keywords/IterationKeywordsExamples.cs#5)]

### <a name="the-initializer-section"></a>*initializer* 섹션

*initializer* 섹션의 명령문은 루프로 유입되기 전에 한 번만 실행됩니다. *initializer* 섹션은 다음 중 하나입니다.

- 루프 외부에서 액세스할 수 없는 로컬 루프 변수의 선언 및 초기화

- 쉼표로 구분된 다음 목록의 0개 이상의 명령문 식:

  - [assignment](../operators/assignment-operator.md) 문

  - 메서드 호출

  - 접두사 또는 후위 [increment](../operators/arithmetic-operators.md#increment-operator-) 식(예: `++i` 또는`i++`)

  - 접두사 또는 후위 [decrement](../operators/arithmetic-operators.md#decrement-operator---) 식(예: `--i` 또는`i--`)

  - [new](../operators/new-operator.md) 연산자를 사용하여 개체 만들기

  - [await](../operators/await.md) 식

위의 예제에서 *initializer* 섹션은 로컬 루프 변수 `i`를 선언하고 초기화합니다.

```csharp
int i = 0
```

### <a name="the-condition-section"></a>*condition* 섹션

*condition* 섹션이 있으면 부울 식이어야 합니다. 이 식은 모든 루프 반복 전에 평가됩니다. *condition* 섹션이 없거나 부울 식이 `true`로 평가되는 경우, 다음 루프 반복이 실행되고 그렇지 않으면 루프가 종료됩니다.

위의 예제에서 *condition* 섹션은 로컬 루프 변수의 값에 따라 루프가 종료되는지 여부를 결정합니다.

```csharp
i < 5
```

### <a name="the-iterator-section"></a>*iterator* 섹션

*iterator* 섹션은 루프의 본문을 반복할 때마다 수행되는 작업을 정의합니다. *iterator* 섹션에는 쉼표로 구분된 다음 명령문 식이 0개 이상 포함됩니다.

- [assignment](../operators/assignment-operator.md) 문

- 메서드 호출

- 접두사 또는 후위 [increment](../operators/arithmetic-operators.md#increment-operator-) 식(예: `++i` 또는`i++`)

- 접두사 또는 후위 [decrement](../operators/arithmetic-operators.md#decrement-operator---) 식(예: `--i` 또는`i--`)

- [new](../operators/new-operator.md) 연산자를 사용하여 개체 만들기

- [await](../operators/await.md) 식

위 예제의 *iterator* 섹션은 로컬 루프 변수를 증가시킵니다.

```csharp
i++
```

## <a name="examples"></a>예제

다음 예제에서는 *initializer* 섹션에서 외부 루프 변수에 값 할당, *initializer* 및 *iterator* 섹션에서 메서드 호출, *iterator* 섹션에서 두 변수의 값 변경과 같이 `for` 문 섹션의 여러 가지 덜 일반적인 사용법을 보여 줍니다. **Run**을 선택하여 예제 코드를 실행합니다. 그런 다음, 코드를 수정하고 다시 실행할 수 있습니다.

[!code-csharp-interactive[not typical for loop example](~/samples/snippets/csharp/keywords/IterationKeywordsExamples.cs#6)]

다음 예제에서는 무한 `for` 루프를 정의합니다.

[!code-csharp[infinite for loop example](~/samples/snippets/csharp/keywords/IterationKeywordsExamples.cs#7)]

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [for 문](~/_csharplang/spec/statements.md#the-for-statement) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [foreach, in](foreach-in.md)
