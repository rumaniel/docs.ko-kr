---
title: await 연산자 - C# 참조
ms.custom: seodec18
ms.date: 08/30/2019
f1_keywords:
- await_CSharpKeyword
helpviewer_keywords:
- await keyword [C#]
- await [C#]
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
ms.openlocfilehash: c2172f651dd106825680de3195e26f032225a9ab
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169331"
---
# <a name="await-operator-c-reference"></a>await 연산자(C# 참조)

`await` 연산자는 피연산자가 나타내는 비동기 작업이 완료될 때까지 바깥쪽 [비동기](../keywords/async.md) 메서드의 평가를 일시 중단합니다. 비동기 작업이 완료되면 `await` 연산자는 작업 결과를 반환합니다(있는 경우). 이미 완료된 작업을 나타내는 피연산자에 `await` 연산자가 적용되면 바깥쪽 메서드를 일시 중단하지 않고 작업 결과를 반환합니다. `await` 연산자는 비동기 메서드를 평가하는 스레드를 차단하지 않습니다. `await` 연산자가 바깥쪽 메서드를 일시 중단하면 제어가 메서드 호출자에게 반환됩니다.

다음 예제에서 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A?displayProperty=nameWithType> 메서드는 완료 시 바이트 배열을 생성하는 비동기 작업을 나타내는 `Task<byte[]>` 인스턴스를 반환합니다. 작업이 완료될 때까지 `await` 연산자는 `DownloadDocsMainPageAsync` 메서드를 일시 중단합니다. `DownloadDocsMainPageAsync`가 일시 중단되면 제어는 `DownloadDocsMainPageAsync`의 호출자인 `Main` 메서드에 반환됩니다. `Main` 메서드는 `DownloadDocsMainPageAsync` 메서드가 수행한 비동기 작업의 결과가 필요할 때까지 실행됩니다. <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>가 모든 바이트를 가져오면 나머지 `DownloadDocsMainPageAsync` 메서드가 평가됩니다. 그 후에는 나머지 `Main` 메서드가 평가됩니다.

[!code-csharp[await example](~/samples/csharp/language-reference/operators/AwaitOperator.cs)]

앞의 예제에서는 C# 7.1부터 가능한 [비동기 `Main` 메서드](../../programming-guide/main-and-command-args/index.md)를 사용합니다. 자세한 내용은 [Main 메서드 섹션의 await 연산자](#await-operator-in-the-main-method)를 참조하세요.

> [!NOTE]
> 비동기 프로그래밍에 대한 소개는 [async 및 await를 사용한 비동기 프로그래밍](../../programming-guide/concepts/async/index.md)을 참조하세요. `async` 및 `await`를 사용하는 비동기 프로그래밍은 [작업 기반 비동기 패턴](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)을 따릅니다.

[async](../keywords/async.md) 키워드로 수정된 메서드, [람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md) 또는 [무명 메서드](delegate-operator.md)에는 `await` 연산자만 사용할 수 있습니다. 비동기 메서드 내의 동기 함수 본문, [lock 문](../keywords/lock-statement.md) 블록 및 [unsafe](../keywords/unsafe.md) 컨텍스트에서는 `await` 연산자를 사용할 수 없습니다.
  
`await` 연산자의 피연산자는 일반적으로 .NET 형식인 <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.ValueTask> 또는 <xref:System.Threading.Tasks.ValueTask%601> 중 하나에 해당합니다. 그러나 대기 가능한 모든 식은 `await` 연산자의 피연산자일 수 있습니다. 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [대기 가능 식](~/_csharplang/spec/expressions.md#awaitable-expressions) 섹션을 참조하세요.

`t` 식의 형식이 <xref:System.Threading.Tasks.Task%601> 또는 <xref:System.Threading.Tasks.ValueTask%601>이면 `await t` 식의 형식은 `TResult`입니다. `t` 형식이 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.ValueTask>이면 `await t` 형식은 `void`입니다. 두 경우 모두 `t`가 예외를 throw하면 `await t`는 예외를 다시 throw합니다. 예외 처리에 대한 자세한 내용은 [try-catch 문](../keywords/try-catch.md) 문서에서 [비동기 메서드의 예외](../keywords/try-catch.md#exceptions-in-async-methods) 섹션을 참조하세요.

`async` 및 `await` 키워드는 C# 5부터 사용할 수 있습니다.

## <a name="await-operator-in-the-main-method"></a>Main 메서드의 await 연산자

C# 7.1부터 애플리케이션 진입점인 [`Main` 메서드](../../programming-guide/main-and-command-args/index.md)는 `Task` 또는 `Task<int>`를 반환하여 해당 본문에서 `await` 연산자를 사용할 수 있습니다. 이전 C# 버전에서는 `Main` 메서드가 비동기 작업이 완료될 때까지 대기하는지 확인하기 위해 해당 비동기 메서드에서 반환되는 <xref:System.Threading.Tasks.Task%601> 인스턴스의 <xref:System.Threading.Tasks.Task%601.Result?displayProperty=nameWithType> 속성 값을 검색할 수 있습니다. 값을 생성하지 않는 비동기 작업의 경우 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드를 호출할 수 있습니다. 언어 버전을 선택하는 방법에 대한 자세한 내용은 [C# 언어 버전 선택](../configure-language-version.md)을 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [Await 식](~/_csharplang/spec/expressions.md#await-expressions) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [async](../keywords/async.md)
- [async 및 await를 사용한 비동기 프로그래밍](../../programming-guide/concepts/async/index.md)
- [작업 비동기 프로그래밍 모델](../../programming-guide/concepts/async/task-asynchronous-programming-model.md)
- [비동기 프로그래밍](../../async.md)
- [작업 기반 비동기 패턴](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)
- [비동기에 대한 자세한 설명](../../../standard/async-in-depth.md)
- [연습: async 및 await를 사용하여 웹에 액세스](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
