---
title: AsyncCallback 대리자 및 상태 개체 사용
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous programming, delegates
- AsyncCallback delegate, samples
- asynchronous programming, state objects
- IAsyncResult interface, samples
ms.assetid: e3e5475d-c5e9-43f0-928e-d18df8ca1f1d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bb62b191dc3b3246745f9f0ea3737ed74a2bf57b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54605983"
---
# <a name="using-an-asynccallback-delegate-and-state-object"></a>AsyncCallback 대리자 및 상태 개체 사용
<xref:System.AsyncCallback> 대리자를 사용하여 별도의 스레드에서 비동기 작업의 결과를 처리할 때 상태 개체를 사용하여 콜백 간에 정보를 전달하고 최종 결과를 검색할 수 있습니다. 이 항목에서는 [AsyncCallback 대리자를 사용하여 비동기 작업 종료](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)의 예를 확장하여 연습하는 방법을 보여줍니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 <xref:System.Net.Dns> 클래스에서 비동기 메서드를 사용하여 사용자가 지정한 컴퓨터의 DNS(Domain Name System) 정보를 검색하는 방법을 보여줍니다. 이 예제는 상태 정보를 저장하는 `HostRequest` 클래스를 정의하고 사용합니다. 사용자가 입력한 각 컴퓨터 이름에 대해 `HostRequest` 개체가 생성됩니다. 이 개체는 <xref:System.Net.Dns.BeginGetHostByName%2A> 메서드에 전달됩니다. 요청이 완료될 때마다 `ProcessDnsInformation` 메서드가 호출됩니다. `HostRequest` 개체는 <xref:System.IAsyncResult.AsyncState%2A> 속성을 사용하여 검색됩니다. `ProcessDnsInformation` 메서드는 `HostRequest` 개체를 사용하여 요청에서 반환한 <xref:System.Net.IPHostEntry> 또는 요청에서 throw한 <xref:System.Net.Sockets.SocketException>을 저장합니다. 모든 요청이 완료되면 애플리케이션은 `HostRequest` 개체에 대해 반복되며 DNS 정보 또는 <xref:System.Net.Sockets.SocketException> 오류 메시지를 표시합니다.  
  
 [!code-csharp[AsyncDesignPattern#5](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateWithStateObject.cs#5)]
 [!code-vb[AsyncDesignPattern#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateWithStateObject.vb#5)]  
  
## <a name="see-also"></a>참고 항목

- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
- [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
- [AsyncCallback 대리자를 사용하여 비동기 작업 종료](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)
