---
title: C# 문 - C# 언어 둘러보기
description: 문을 사용하여 C# 프로그램 동작 만들기
ms.date: 11/06/2016
ms.assetid: 5409c379-5622-4fae-88b5-1654276ea8d4
ms.openlocfilehash: 26b151bc116dde9120757f954bdcf3aee041c5f5
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65634538"
---
# <a name="statements"></a>문

프로그램의 동작은 *문*을 사용하여 표현됩니다. C#은 여러 다른 종류의 문을 지원하며 이중 많은 문이 포함 문에 대해 정의됩니다.

*블록*은 단일 문이 허용되는 컨텍스트에서 여러 문을 쓸 수 있도록 허용합니다. 블록은 구분 기호 `{`와 `}` 사이에 쓴 문 목록으로 구성됩니다.

*선언 문*은 지역 변수 및 상수를 선언하는 데 사용됩니다.

*식 문*은 식을 평가하는 데 사용됩니다. 문으로 사용할 수 있는 식에는 메서드 호출, `new` 연산자를 사용하는 개체 할당, `=` 및 복합 할당 연산자를 사용하는 대입, `++` 및 `--` 연산자를 사용하는 증가 및 감소 연산, `await` 식이 포함됩니다.

*선택 문*은 일부 식 값에 따라 실행할 수 있는 다양한 문 중에서 하나를 선택하는 데 사용됩니다. 이 그룹에는 `if` 및 `switch` 문이 포함됩니다.

*반복 문*은 포함 문을 반복해서 실행하는 데 사용됩니다. 이 그룹에는 `while`, `do`, `for` 및 `foreach` 문이 포함됩니다.

*점프 문*은 제어를 전달하는 데 사용됩니다. 이 그룹에는 `break`, `continue`, `goto`, `throw`, `return` 및 `yield` 문이 포함됩니다.

`try`... `catch` 문은 블록 실행 중에 발생하는 예외를 catch하는 데 사용되고 `try`... `finally` 문은 예외 발생 여부에 관계 없이 항상 실행되는 종료 코드를 지정하는 데 사용됩니다.

`checked` 및 `unchecked` 문은 정수 계열 형식 산술 연산 및 변환에 대한 오버플로 검사 컨텍스트를 제어하는 데 사용됩니다.

`lock` 문은 지정된 개체에 대한 상호 배타적 잠금을 획득하고, 문을 실행한 후 잠금을 해제하는 데 사용됩니다.

`using` 문은 리소스를 획득하고, 문을 실행한 후 해당 리소스를 삭제하는 데 사용됩니다.

다음은 사용할 수 있는 문 종류와 각각에 대한 예제입니다.

* 지역 변수 선언:

 [!code-csharp[Declarations](../../../samples/snippets/csharp/tour/statements/Program.cs#L9-L15)]

* 지역 상수 선언:

 [!code-csharp[ConstantDeclarations](../../../samples/snippets/csharp/tour/statements/Program.cs#L17-L22)]

* 식 문

 [!code-csharp[Expressions](../../../samples/snippets/csharp/tour/statements/Program.cs#L24-L31)]

* `if` 문:

 [!code-csharp[IfStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L33-L43)]

* `switch` 문:

 [!code-csharp[SwitchStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L45-L60)]

* `while` 문:

 [!code-csharp[WhileStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L62-L70)]

* `do` 문:

 [!code-csharp[DoStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L72-L81)]

* `for` 문:

 [!code-csharp[ForStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L83-L89)]

* `foreach` 문:

 [!code-csharp[ForEachStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L91-L97)]

* `break` 문:

 [!code-csharp[BreakStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L99-L108)]

* `continue` 문:

 [!code-csharp[ContinueStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L110-L118)]

* `goto` 문:

 [!code-csharp[GotoStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L120-L129)]

* `return` 문:

 [!code-csharp[ReturnStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L131-L139)]

* `yield` 문:

 [!code-csharp[YieldStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L141-L155)]

* `throw`문 및 `try` 문:

 [!code-csharp[TryThrow](../../../samples/snippets/csharp/tour/statements/Program.cs#L157-L183)]

* `checked` 및 `unchecked` 문:

 [!code-csharp[CheckedUncheckedStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L185-L196)]

* `lock` 문:

 [!code-csharp[LockStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L257-L273)]

* `using` 문:

 [!code-csharp[UsingStatement](../../../samples/snippets/csharp/tour/statements/Program.cs#L198-L206)]

>[!div class="step-by-step"]
>[이전](expressions.md)
>[다음](classes-and-objects.md)
