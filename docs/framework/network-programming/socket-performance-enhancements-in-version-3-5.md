---
title: 버전 3.5의 소켓 성능 향상
ms.date: 03/30/2017
ms.assetid: 225aa5f9-c54b-4620-ab64-5cd100cfd54c
ms.openlocfilehash: 588edc35f1b0fb39beb9be9a71573a1727ffeab8
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50193450"
---
# <a name="socket-performance-enhancements-in-version-35"></a>버전 3.5의 소켓 성능 향상
<xref:System.Net.Sockets.Socket?displayProperty=nameWithType> 클래스는 비동기 네트워크 I/O를 통해 성능을 최적화하는 응용 프로그램에서 사용하기 위해 버전 3.5에서 개선되었습니다. 특수화된 고성능 소켓 응용 프로그램에서 사용할 수 있는 대체 비동기 패턴을 제공하는 <xref:System.Net.Sockets.Socket> 클래스에 대한 향상된 기능 집합의 일부로 일련의 새로운 클래스가 추가되었습니다. 이러한 개선 사항은 특히 높은 성능이 필요한 네트워크 서버 응용 프로그램용으로 설계되었습니다. 응용 프로그램은 향상된 비동기 패턴을 단독으로 사용하거나, 응용 프로그램의 대상 핫 영역에서만 사용할 수 있습니다(예: 많은 양의 데이터를 수신하는 경우).  
  
## <a name="class-enhancements"></a>클래스 개선 사항  
 이러한 개선 사항의 주요 기능은 대량 비동기 소켓 I/O 중 개체의 반복 할당 및 동기화를 방지할 수 있습니다. 현재 비동기 소켓 I/O에 대해 <xref:System.Net.Sockets.Socket> 클래스에서 구현되는 Begin/End 디자인 패턴에서는 각 비동기 소켓 작업에 대해 <xref:System.IAsyncResult?displayProperty=nameWithType> 개체가 할당되어야 합니다.  
  
 새 <xref:System.Net.Sockets.Socket> 클래스 개선 사항에서 비동기 소켓 작업은 응용 프로그램에서 할당하고 유지 관리하는 다시 사용할 수 있는 <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=nameWithType> 클래스 개체를 통해 설명됩니다. 고성능 소켓 응용 프로그램은 유지해야 하는 겹쳐진 소켓 작업량을 가장 잘 알고 있습니다. 응용 프로그램은 <xref:System.Net.Sockets.SocketAsyncEventArgs> 개체를 필요한 개수만큼 만들 수 있습니다. 예를 들어 서버 응용 프로그램이 들어오는 클라이언트 연결 속도를 지원하기 위해 항상 15개의 소켓 허용 작업을 처리 중이어야 하는 경우 해당 용도로 다시 사용할 수 있는 <xref:System.Net.Sockets.SocketAsyncEventArgs> 개체 15개를 미리 할당할 수 있습니다.  
  
 이 클래스를 사용하여 비동기 소켓 작업을 수행하기 위한 패턴은 다음 단계로 구성됩니다.  
  
1.  새 <xref:System.Net.Sockets.SocketAsyncEventArgs> 컨텍스트 개체를 할당하거나 응용 프로그램 풀에서 무료 개체를 가져옵니다.  
  
2.  컨텍스트 개체의 속성을 수행할 작업으로 설정합니다(예: 콜백 대리자 메서드 및 데이터 버퍼).  
  
3.  적절한 소켓 메서드(xxxAsync)를 호출하여 비동기 작업을 시작합니다.  
  
4.  비동기 소켓 메서드(xxxAsync)가 콜백에서 true를 반환하는 경우 컨텍스트 속성에서 완료 상태를 쿼리합니다.  
  
5.  비동기 소켓 메서드(xxxAsync)가 콜백에서 false를 반환하는 경우 작업이 동기적으로 완료됩니다. 컨텍스트 속성에서 작업 결과를 쿼리할 수 있습니다.  
  
6.  컨텍스트를 다른 작업에 다시 사용하거나, 풀에 다시 넣거나, 삭제합니다.  
  
 새 비동기 소켓 작업 컨텍스트 개체의 수명은 응용 프로그램 코드와 비동기 I/O 참조에서 참조를 통해 결정됩니다. 비동기 소켓 작업 방법 중 하나에 매개 변수로 제출된 후 응용 프로그램이 비동기 소켓 작업 컨텍스트 개체에 대한 참조를 유지할 필요는 없습니다. 완료 콜백이 반환될 때까지 참조된 상태로 유지됩니다. 그러나 이후 비동기 소켓 작업에 다시 사용할 수 있도록 응용 프로그램에서 컨텍스트 개체에 대한 참조를 유지하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.Sockets.Socket?displayProperty=nameWithType>  
 <xref:System.Net.Sockets.SendPacketsElement?displayProperty=nameWithType>  
 <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=nameWithType>  
 <xref:System.Net.Sockets.SocketAsyncOperation?displayProperty=nameWithType>  
 [네트워크 프로그래밍 샘플](../../../docs/framework/network-programming/network-programming-samples.md)  
 [소켓 코드 예제](socket-code-examples.md)
