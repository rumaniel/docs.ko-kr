---
title: 동기 메서드를 비동기 방식으로 호출
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- asynchronous programming, delegates
- asynchronous delegates
- AsyncWaitHandle property
- callback methods
- calling synchronous methods in asynchronous manner
- WaitHandle class, code examples
- asynchronous programming, status polling
- polling asynchronous operation status
- delegates [.NET Framework], asynchronous
- synchronous calling in asynchronous manner
- waiting for asynchronous calls
- status information [.NET Framework], asynchronous operations
ms.assetid: 41972034-92ed-450a-9664-ab93fcc6f1fb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 342af20b78ae996bb61c6b563ecf42137ee51022
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64629098"
---
# <a name="calling-synchronous-methods-asynchronously"></a>동기 메서드를 비동기 방식으로 호출

.NET Framework에서는 모든 메서드를 비동기 방식으로 호출할 수 있습니다. 이렇게 하려면 호출하려는 메서드와 같은 시그니처를 사용하여 대리자를 정의합니다. 그러면 공용 언어 런타임은 이 대리자에 대해 `BeginInvoke` 및 `EndInvoke` 메서드를 해당 시그니처와 함께 자동으로 정의합니다.

> [!NOTE]
> 특히 `BeginInvoke` 및 `EndInvoke` 메서드와 같은 비동기 대리자는 .NET Compact Framework에서 호출할 수 없습니다.

`BeginInvoke` 메서드는 비동기 호출을 시작합니다. 이 메서드의 매개 변수는 비동기 방식으로 실행하려는 메서드의 매개 변수와 같으며 두 개의 선택적인 매개 변수가 추가로 사용됩니다. 첫 번째 매개 변수는 비동기 호출이 완료될 때 호출될 메서드를 참조하는 <xref:System.AsyncCallback> 대리자이고 두 번째 매개 변수는 콜백 메서드에 정보를 전달하는 사용자 정의 개체입니다. `BeginInvoke` 는 비동기 호출이 완료되기를 기다리지 않고 즉시 반환합니다. `BeginInvoke` 는 비동기 호출의 진행률을 모니터링하는 데 사용할 수 있는 <xref:System.IAsyncResult>를 반환합니다.

`EndInvoke` 메서드는 비동기 호출의 결과를 검색합니다. 이 메서드는 `BeginInvoke`를 호출한 후 언제든지 호출할 수 있습니다. 비동기 호출이 완료되지 않은 경우 `EndInvoke` 는 호출이 완료될 때까지 호출하는 스레드를 차단합니다. `EndInvoke`의 매개 변수에는 비동기 방식으로 실행하려는 메서드의 `out` 및 `ref` 매개 변수(Visual Basic의 경우 `<Out>` `ByRef` 및 `ByRef`)와 `BeginInvoke`에서 반환하는 <xref:System.IAsyncResult>가 포함됩니다.

> [!NOTE]
> Visual Studio의 IntelliSense 기능은 `BeginInvoke` 및 `EndInvoke`의 매개 변수를 표시합니다. Visual Studio 또는 이와 유사한 도구를 사용하지 않거나 Visual Studio와 C#을 함께 사용하는 경우 이러한 메서드에 대해 정의된 매개 변수 설명을 보려면 [APM(비동기 프로그래밍 모델)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md)을 참조하세요.

이 항목의 코드 예제에서는 `BeginInvoke` 및 `EndInvoke` 를 사용하여 비동기 호출을 수행하는 네 가지 일반적인 방법을 보여 줍니다. `BeginInvoke` 를 호출한 후 다음과 같은 작업을 수행할 수 있습니다.

- 작업을 수행한 다음 `EndInvoke` 를 호출하여 호출이 완료될 때까지 실행을 차단합니다.

- <xref:System.Threading.WaitHandle> 속성을 사용하여 <xref:System.IAsyncResult.AsyncWaitHandle%2A?displayProperty=nameWithType> 을 가져오고 해당 <xref:System.Threading.WaitHandle.WaitOne%2A> 메서드를 사용하여 <xref:System.Threading.WaitHandle> 이 신호를 받을 때까지 실행을 차단한 다음 `EndInvoke`를 호출합니다.

- <xref:System.IAsyncResult> 에서 반환한 `BeginInvoke` 를 폴링하여 비동기 호출이 완료되는 시점을 확인한 다음 `EndInvoke`를 호출합니다.

- 콜백 메서드의 대리자를 `BeginInvoke`에 전달합니다. 이 메서드는 비동기 호출이 완료될 때 <xref:System.Threading.ThreadPool> 스레드에서 실행됩니다. 콜백 메서드는 `EndInvoke`를 호출합니다.

> [!IMPORTANT]
> 사용하는 방법에 관계없이 항상 `EndInvoke` 를 호출하여 비동기 호출을 완료해야 합니다.

## <a name="defining-the-test-method-and-asynchronous-delegate"></a>테스트 메서드 및 비동기 대리자 정의
 다음 코드 예제에서는 동일한 장기 실행 메서드인 `TestMethod`를 비동기 방식으로 호출하는 다양한 방법을 보여 줍니다. `TestMethod` 메서드는 처리를 시작했음을 나타내는 콘솔 메시지를 표시하고 몇 초간 대기한 후 종료됩니다. `TestMethod` 에는 `out` 및 `BeginInvoke` 의 시그니처에 해당 매개 변수가 추가되는 방식을 보여 주는 `EndInvoke`매개 변수가 있습니다. `ref` 매개 변수도 마찬가지로 처리할 수 있습니다.

 다음 코드 예제에서는 `TestMethod` 의 정의와 `AsyncMethodCaller` 를 비동기식으로 호출하는 데 사용할 수 있는 `TestMethod` 라는 대리자를 보여 줍니다. 코드 예제를 컴파일하려면 `TestMethod` 및 `AsyncMethodCaller` 대리자의 정의를 포함해야 합니다.

 [!code-cpp[AsyncDelegateExamples#1](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/TestMethod.cpp#1)]
 [!code-csharp[AsyncDelegateExamples#1](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/TestMethod.cs#1)]
 [!code-vb[AsyncDelegateExamples#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/TestMethod.vb#1)]

## <a name="waiting-for-an-asynchronous-call-with-endinvoke"></a>EndInvoke로 비동기 호출 대기
 메서드를 비동기 방식으로 실행하는 가장 간단한 방법은 대리자의 `BeginInvoke` 메서드를 호출하여 메서드 실행을 시작하고 주 스레드에서 작업을 수행한 다음 대리자의 `EndInvoke` 메서드를 호출하는 것입니다. `EndInvoke` 는 비동기 호출이 완료될 때까지 반환되지 않으므로 호출하는 스레드를 차단할 수도 있습니다. 이 방법은 파일 또는 네트워크 작업에 적합합니다.

> [!IMPORTANT]
> `EndInvoke` 는 실행을 차단할 수 있으므로 사용자 인터페이스를 제공하는 스레드에서는 호출하지 말아야 합니다.

 [!code-cpp[AsyncDelegateExamples#2](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/EndInvoke.cpp#2)]
 [!code-csharp[AsyncDelegateExamples#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/EndInvoke.cs#2)]
 [!code-vb[AsyncDelegateExamples#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/EndInvoke.vb#2)]

## <a name="waiting-for-an-asynchronous-call-with-waithandle"></a>WaitHandle로 비동기 호출 대기
 <xref:System.Threading.WaitHandle> 에서 반환하는 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 의 <xref:System.IAsyncResult> 속성을 사용하여 `BeginInvoke`을 가져올 수 있습니다. 비동기 호출이 완료되면 <xref:System.Threading.WaitHandle> 은 신호를 받으며 <xref:System.Threading.WaitHandle.WaitOne%2A> 메서드를 호출하여 대기할 수 있습니다.

 <xref:System.Threading.WaitHandle>을 사용하는 경우 비동기 호출이 완료되기 전이나 후에 추가 작업을 처리한 다음 `EndInvoke` 를 호출하여 결과를 검색할 수 있습니다.

> [!NOTE]
> 대기 핸들은 `EndInvoke`를 호출할 때 자동으로 닫히지 않습니다. 대기 핸들에 대한 모든 참조를 해제하면 가비지 수집에서 대기 핸들을 회수할 때 시스템 리소스가 확보됩니다. 대기 핸들 사용을 마친 후 시스템 리소스를 즉시 확보하려면 <xref:System.Threading.WaitHandle.Close%2A?displayProperty=nameWithType> 메서드를 호출하여 핸들을 삭제합니다. 삭제 가능한 개체를 명시적으로 삭제하면 가비지 수집의 효율성이 향상됩니다.

 [!code-cpp[AsyncDelegateExamples#3](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/waithandle.cpp#3)]
 [!code-csharp[AsyncDelegateExamples#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/waithandle.cs#3)]
 [!code-vb[AsyncDelegateExamples#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/WaitHandle.vb#3)]

## <a name="polling-for-asynchronous-call-completion"></a>비동기 호출 완료에 대한 폴링
 <xref:System.IAsyncResult.IsCompleted%2A> 에서 반환하는 <xref:System.IAsyncResult> 의 `BeginInvoke` 속성을 사용하여 비동기 호출이 완료되는 시점을 확인할 수 있습니다. 사용자 인터페이스를 제공하는 스레드에서 비동기 호출을 수행하는 경우 이 동작을 수행할 수 있습니다. 완료에 대해 폴링하면 비동기 호출이 <xref:System.Threading.ThreadPool> 스레드에서 실행되는 동안 호출 스레드가 계속 실행될 수 있습니다.

 [!code-cpp[AsyncDelegateExamples#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/polling.cpp#4)]
 [!code-csharp[AsyncDelegateExamples#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/polling.cs#4)]
 [!code-vb[AsyncDelegateExamples#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/polling.vb#4)]

## <a name="executing-a-callback-method-when-an-asynchronous-call-completes"></a>비동기 호출이 완료될 때 콜백 메서드 실행
 비동기 호출을 시작하는 스레드와 결과를 처리하는 스레드가 서로 다를 수 있는 경우에는 호출이 완료될 때 콜백 메서드를 실행할 수 있습니다. 콜백 메서드는 <xref:System.Threading.ThreadPool> 스레드에서 실행됩니다.

 콜백 메서드를 사용하려면 `BeginInvoke` 에 콜백 메서드를 나타내는 <xref:System.AsyncCallback> 대리자를 전달해야 합니다. 콜백 메서드에서 사용할 정보가 들어 있는 개체를 전달할 수도 있습니다. 콜백 메서드에서는 콜백 메서드의 유일한 매개 변수인 <xref:System.IAsyncResult>를 <xref:System.Runtime.Remoting.Messaging.AsyncResult> 개체로 캐스팅할 수 있습니다. 그런 다음 <xref:System.Runtime.Remoting.Messaging.AsyncResult.AsyncDelegate%2A?displayProperty=nameWithType> 속성을 사용하여 호출을 시작하는 데 사용된 대리자를 가져오면 `EndInvoke`를 호출할 수 있습니다.

 예제 관련 참고 사항:

- `TestMethod`의 `threadId` 매개 변수는 `out` 매개 변수(Visual Basic의 경우 [`<Out>` `ByRef`)이므로 입력 값은 `TestMethod`에서 사용되지 않습니다. `BeginInvoke` 를 호출할 때는 더미 변수가 전달됩니다. `threadId` 매개 변수가 `ref` 매개 변수(Visual Basic의 경우`ByRef` )인 경우에는 변수가 `BeginInvoke` 및 `EndInvoke`에 전달 가능한 클래스 수준 필드여야 합니다.

- `BeginInvoke` 에 전달되는 상태 정보는 콜백 메서드에서 출력 메시지의 형식을 지정하는 데 사용하는 형식 문자열입니다. 이 문자열은 <xref:System.Object>형식으로 전달되므로 상태 정보를 적절한 형식으로 캐스팅해야 사용할 수 있습니다.

- 콜백은 <xref:System.Threading.ThreadPool> 스레드에서 수행됩니다. <xref:System.Threading.ThreadPool> 스레드는 주 스레드가 종료된 경우 애플리케이션 실행을 유지하지 않는 배경 스레드이므로 예제의 주 스레드는 콜백이 완료될 때까지 충분히 대기해야 합니다.

 [!code-cpp[AsyncDelegateExamples#5](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/callback.cpp#5)]
 [!code-csharp[AsyncDelegateExamples#5](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/callback.cs#5)]
 [!code-vb[AsyncDelegateExamples#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/callback.vb#5)]

## <a name="see-also"></a>참고 항목

- <xref:System.Delegate>
- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
