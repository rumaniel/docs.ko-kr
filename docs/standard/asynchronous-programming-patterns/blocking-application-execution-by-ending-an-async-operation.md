---
title: 비동기 작업을 종료하여 애플리케이션 실행 차단
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- blocks, asynchronous operations
- AsyncWaitHandle property
- asynchronous programming, blocking applications
- blocking application execution
ms.assetid: cc5e2834-a65b-4df8-b750-7bdb79997fee
author: rpetrusha
ms.author: ronpet
dev_langs:
- csharp
- vb
ms.openlocfilehash: d457a9c22f0eaea02fe744ebb24d02558710948b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64629021"
---
# <a name="blocking-application-execution-by-ending-an-async-operation"></a>비동기 작업을 종료하여 애플리케이션 실행 차단
비동기 작업의 결과를 기다리는 동안 다른 작업을 계속 수행할 수 없는 애플리케이션은 작업이 완료될 때까지 차단되어야 합니다. 다음 옵션 중 하나를 사용하여 비동기 작업이 완료될 때까지 대기하는 동안 애플리케이션의 기본 스레드를 차단합니다.  
  
- 비동기 작업 **End**_OperationName_ 메서드를 호출합니다. 이 항목에서 이 방법을 설명합니다.  
  
- 비동기 작업의 **Begin**_OperationName_ 메서드에 의해 반환된 <xref:System.IAsyncResult>의 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 속성을 사용합니다. 이 방법을 설명하는 예제는 [AsyncWaitHandle을 사용하는 애플리케이션 실행 블로킹](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-using-an-asyncwaithandle.md)을 참조하세요.  
  
 **End**_OperationName_ 메서드를 사용하여 비동기 작업이 완료될 때까지 차단하는 애플리케이션은 일반적으로 **Begin**_OperationName_ 메서드를 호출하고, 작업 결과 없이 완료할 수 있는 작업을 수행한 다음, **End**_OperationName_을 호출합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 <xref:System.Net.Dns> 클래스에서 비동기 메서드를 사용하여 사용자가 지정한 컴퓨터의 Domain Name System 정보를 검색하는 방법을 보여줍니다. 이 방법을 사용할 경우 이러한 인수가 필요하지 않기 때문에 <xref:System.Net.Dns.BeginGetHostByName%2A>`requestCallback` 및 `stateObject` 매개 변수에 대해 `null`(Visual Basic의 `Nothing`)이 전달됩니다.  
  
 [!code-csharp[AsyncDesignPattern#1](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_EndBlock.cs#1)]
 [!code-vb[AsyncDesignPattern#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_EndBlock.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
- [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
