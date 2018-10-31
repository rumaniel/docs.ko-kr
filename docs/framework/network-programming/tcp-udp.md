---
title: TCP-UDP
ms.date: 03/30/2017
helpviewer_keywords:
- protocols, TCP/UDP
- network resources, TCP/UDP
- sending data, TCP/UDP
- TCP/UDP
- TcpClient class, about TcpClient class
- application protocols, TCP/UDP
- receiving data, TCP/UDP
- TcpListener class, about TcpListener class
- Socket class, about Socket class
- UDP
- data requests, TCP/UDP
- requesting data from Internet, TCP/UDP
- Internet, TCP/UDP
ms.assetid: df29b4b0-49e8-4923-82b9-13150dfc40f5
ms.openlocfilehash: 987a8aa789d8c4585a58a031c9d920ee5cab45aa
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50191877"
---
# <a name="tcp-udp"></a>TCP-UDP
응용 프로그램은 <xref:System.Net.Sockets.TcpClient>, <xref:System.Net.Sockets.TcpListener> 및 <xref:System.Net.Sockets.UdpClient> 클래스와 함께 TCP(Transmission Control Protocol) 및 UDP(User Datagram Protocol) 서비스를 사용할 수 있습니다. 이러한 프로토콜 클래스는 <xref:System.Net.Sockets.Socket?displayProperty=nameWithType> 클래스를 기반으로 빌드되며 데이터 전송의 세부 사항을 처리합니다.  
  
 프로토콜 클래스는 **Socket** 클래스의 동기 메서드를 사용하여 상태 정보를 유지 관리하거나 프로토콜 관련 소켓 설정의 세부 정보를 알아야 하는 오버헤드 없이 네트워크 서비스에 대한 쉽고 간단한 액세스를 제공합니다. 비동기 **Socket** 메서드를 사용하려면 <xref:System.Net.Sockets.NetworkStream> 클래스에서 제공하는 비동기 메서드를 사용할 수 있습니다. 프로토콜 클래스에 의해 노출되지 않는 **Socket** 클래스의 기능에 액세스하려면 **Socket** 클래스를 사용해야 합니다.  
  
 **TcpClient** 및 **TcpListener**는 **NetworkStream** 클래스를 사용하여 네트워크를 나타냅니다. <xref:System.Net.Sockets.TcpClient.GetStream%2A> 메서드를 사용하여 네트워크 스트림을 반환한 다음 스트림의 <xref:System.Net.Sockets.NetworkStream.Read%2A> 및 <xref:System.Net.Sockets.NetworkStream.Write%2A> 메서드를 호출합니다. **NetworkStream**은 프로토콜 클래스의 기본 소켓을 소유하지 않으므로 닫아도 소켓에 영향을 주지 않습니다.  
  
 **UdpClient** 클래스는 바이트 배열을 사용하여 UDP 데이터그램을 보유합니다. <xref:System.Net.Sockets.UdpClient.Send%2A> 메서드를 사용하여 네트워크에 데이터를 보내고 <xref:System.Net.Sockets.UdpClient.Receive%2A> 메서드를 사용하여 들어오는 데이터그램을 받습니다.  
  
## <a name="see-also"></a>참고 항목  
 [TCP 서비스 사용](../../../docs/framework/network-programming/using-tcp-services.md)  
 [UDP 서비스 사용](../../../docs/framework/network-programming/using-udp-services.md)  
 [네트워크에서 스트림 사용](../../../docs/framework/network-programming/using-streams-on-the-network.md)  
 [비동기 서버 소켓 사용](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)  
 [비동기 클라이언트 소켓 사용](../../../docs/framework/network-programming/using-an-asynchronous-client-socket.md)  
 [응용 프로그램 프로토콜 사용](../../../docs/framework/network-programming/using-application-protocols.md)
