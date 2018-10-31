---
title: AsyncWaitHandle을 사용하는 응용 프로그램 실행 블로킹
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- blocks, asynchronous operations
- ending asynchronous operations
- asynchronous programming, ending operations
- asynchronous programming, blocking applications
- stopping asynchronous operations
- blocking application execution
ms.assetid: 3e32daf2-8161-4e8f-addd-9fd9ff101b03
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 054af36987d60c8aeb752c9c711f1cce19733efc
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48033287"
---
# <a name="blocking-application-execution-using-an-asyncwaithandle"></a>AsyncWaitHandle을 사용하는 응용 프로그램 실행 블로킹
비동기 작업의 결과를 기다리는 동안 다른 작업을 계속 수행할 수 없는 응용 프로그램은 작업이 완료될 때까지 차단되어야 합니다. 다음 옵션 중 하나를 사용하여 비동기 작업이 완료될 때까지 대기하는 동안 응용 프로그램의 기본 스레드를 차단합니다.  
  
-   비동기 작업의 **Begin***OperationName* 메서드에 의해 반환된 <xref:System.IAsyncResult>의 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 속성을 사용합니다. 이 항목에서 이 방법을 설명합니다.  
  
-   비동기 작업의 **End***OperationName* 메서드를 호출합니다. 이 방법을 설명하는 예제는 [비동기 작업을 종료하여 응용 프로그램 실행 블로킹](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-by-ending-an-async-operation.md)을 참조하세요.  
  
 비동기 작업이 완료될 때까지 하나 이상의 <xref:System.Threading.WaitHandle> 개체를 사용하여 차단하는 응용 프로그램은 일반적으로 **Begin***OperationName* 메서드를 호출하고 작업의 결과 없이 완료할 수 있는 작업을 수행한 다음, 비동기 작업이 완료될 때까지 차단합니다. 응용 프로그램은 <xref:System.IAsyncResult.AsyncWaitHandle%2A>를 사용하는 <xref:System.Threading.WaitHandle.WaitOne%2A> 메서드 중 하나를 호출하여 단일 작업을 차단할 수 있습니다. 비동기 작업 집합이 완료될 때까지 대기하는 동안 차단하려면 연관된 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 개체를 배열에 저장하고 <xref:System.Threading.WaitHandle.WaitAll%2A> 메서드 중 하나를 호출합니다. 일련의 비동기 작업 중 하나가 완료될 때까지 대기하는 동안 차단하려면 연관된 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 개체를 배열에 저장하고 <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드 중 하나를 호출합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 DNS 클래스에서 비동기 메서드를 사용하여 사용자가 지정한 컴퓨터의 Domain Name System 정보를 검색하는 방법을 보여줍니다. 이 예제는 비동기 작업과 연결된 <xref:System.Threading.WaitHandle>을 사용하여 차단하는 방법을 보여줍니다. 이 방법을 사용할 경우 이러한 항목이 필요하지 않기 때문에 <xref:System.Net.Dns.BeginGetHostByName%2A>`requestCallback` 및 `stateObject` 매개 변수에 대해 `null`(Visual Basic의 `Nothing`)이 전달됩니다.  
  
 [!code-csharp[AsyncDesignPattern#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_EndBlockWait.cs#2)]
 [!code-vb[AsyncDesignPattern#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_EndBlockWait.vb#2)]  
  
## <a name="see-also"></a>참고 항목

- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
- [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
