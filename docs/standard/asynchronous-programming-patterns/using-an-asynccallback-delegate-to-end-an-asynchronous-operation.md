---
title: AsyncCallback 대리자를 사용하여 비동기 작업 종료
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ending asynchronous operations
- asynchronous programming, ending operations
- AsyncCallback delegate
- stopping asynchronous operations
ms.assetid: 9d97206c-8917-406c-8961-7d0909d84eeb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9e53634cea4ab3d260247ce645956c68ea7e2e80
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623535"
---
# <a name="using-an-asynccallback-delegate-to-end-an-asynchronous-operation"></a>AsyncCallback 대리자를 사용하여 비동기 작업 종료
비동기 작업의 결과를 기다리는 동안 다른 작업을 수행할 수 있는 애플리케이션은 작업이 완료될 때까지 차단되면 안 됩니다. 다음 옵션 중 하나를 사용하여 비동기 작업이 완료될 때까지 대기하는 동안 명령을 계속 실행합니다.  
  
- <xref:System.AsyncCallback> 대리자를 사용하여 비동기 작업 결과를 별도의 스레드에서 처리합니다. 이 항목에서 이 방법을 설명합니다.  
  
- 비동기 작업의 **Begin**_OperationName_ 메서드에서 반환된 <xref:System.IAsyncResult>의 <xref:System.IAsyncResult.IsCompleted%2A> 속성을 사용하여 작업이 완료되었는지 확인합니다. 이 방법을 설명하는 예제는 [비동기 작업의 상태에 대한 폴링](../../../docs/standard/asynchronous-programming-patterns/polling-for-the-status-of-an-asynchronous-operation.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 <xref:System.Net.Dns> 클래스에서 비동기 메서드를 사용하여 사용자가 지정한 컴퓨터의 DNS(Domain Name System) 정보를 검색하는 방법을 보여줍니다. 이 예제에서는 `ProcessDnsInformation` 메서드를 참조하는 <xref:System.AsyncCallback> 대리자를 만듭니다. 이 메서드는 DNS 정보에 대한 각 비동기 요청에 대해 한 번 호출됩니다.  
  
 사용자 지정 호스트는 <xref:System.Net.Dns.BeginGetHostByName%2A> <xref:System.Object> 매개 변수에 전달됩니다. 보다 복잡한 상태 개체를 정의하고 사용하는 방법을 보여주는 예제는 [AsyncCallback 대리자 및 상태 개체 사용](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)을 참조하세요.  
  
 [!code-csharp[AsyncDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateNoStateObject.cs#4)]
 [!code-vb[AsyncDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateNoState.vb#4)]  
  
## <a name="see-also"></a>참고 항목

- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
- [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
- [IAsyncResult를 사용하는 비동기 메서드 호출](../../../docs/standard/asynchronous-programming-patterns/calling-asynchronous-methods-using-iasyncresult.md)
- [AsyncCallback 대리자 및 상태 개체 사용](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)
