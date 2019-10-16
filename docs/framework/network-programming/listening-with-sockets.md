---
title: 소켓으로 수신
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- sockets, listening with sockets
- data requests, sockets
- requesting data from Internet, sockets
- receiving data, sockets
- protocols, sockets
- listening with sockets
- Internet, sockets
ms.assetid: 40e426cc-13db-4371-95eb-f7388bd23ebf
ms.openlocfilehash: d8db8cc6157ef0b03c90d00804696c7e660f08a3
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736786"
---
# <a name="listening-with-sockets"></a>소켓으로 수신
수신기 또는 서버 소켓에서 네트워크의 포트를 열고 클라이언트가 해당 포트에 연결할 때까지 기다립니다. 다른 네트워크 주소 패밀리 및 프로토콜이 있어도 이 예제에서는 TCP/IP 네트워크에 대한 원격 서비스를 만드는 방법을 보여 줍니다.  
  
 TCP/IP 서비스의 고유 주소는 서비스에 대한 엔드포인트를 만드는 서비스의 포트 번호와 호스트의 IP 주소를 결합하여 정의합니다. <xref:System.Net.Dns> 클래스에서는 로컬 네트워크 디바이스에서 지원하는 네트워크 주소에 대한 정보를 반환하는 메서드를 제공합니다. 로컬 네트워크 디바이스에 두 개 이상의 네트워크 주소가 있거나 로컬 시스템에서 두 개 이상의 네트워크 디바이스를 지원하는 경우 **Dns** 클래스에서 모든 네트워크 주소에 대한 정보를 반환하고 애플리케이션에서 서비스의 적절한 주소를 선택해야 합니다. Iana(Internet Assigned Numbers Authority)는 공통 서비스의 포트 번호를 정의합니다. 자세한 내용은 [서비스 이름 및 전송 프로토콜 포트 번호 레지스트리](https://www.iana.org/assignments/port-numbers)를 참조하세요. 다른 서비스에는 1,024 ~ 65,535 범위의 등록된 포트 번호가 있을 수 있습니다.  
  
 다음 예에서는 등록된 포트 번호 범위에서 선택된 포트 번호를 사용하는 호스트 컴퓨터의 **Dns**에서 반환한 첫 번째 IP 주소를 결합하여 서버의 <xref:System.Net.IPEndPoint>를 만듭니다.  
  
```vb  
Dim ipHostInfo As IPHostEntry = Dns.GetHostEntry(Dns.GetHostName())  
Dim ipAddress As IPAddress = ipHostInfo.AddressList(0)  
Dim localEndPoint As New IPEndPoint(ipAddress, 11000)  
```  
  
```csharp  
IPHostEntry ipHostInfo = Dns.GetHostEntry(Dns.GetHostName());  
IPAddress ipAddress = ipHostInfo.AddressList[0];  
IPEndPoint localEndPoint = new IPEndPoint(ipAddress, 11000);  
```  
  
 로컬 엔드포인트가 판별되고 나면 <xref:System.Net.Sockets.Socket.Bind%2A> 메서드를 사용하여 해당 엔드포인트와 <xref:System.Net.Sockets.Socket>을 연결해야 하며, <xref:System.Net.Sockets.Socket.Listen%2A> 메서드를 사용하여 엔드포인트에서 수신 대기하도록 설정해야 합니다. 특정 주소와 포트 조합이 이미 사용 중인 경우 **Bind**에서 예외가 throw됩니다. 다음 예에서는 **Socket**과 **IPEndPoint**의 연결을 보여 줍니다.  
  
```vb  
Dim listener As New Socket(ipAddress.AddressFamily, _  
    SocketType.Stream, ProtocolType.Tcp) 
listener.Bind(localEndPoint)  
listener.Listen(100)  
```  
  
```csharp  
Socket listener = new Socket(ipAddress.AddressFamily,
    SocketType.Stream, ProtocolType.Tcp);
listener.Bind(localEndPoint);  
listener.Listen(100);  
```  
  
 **Listen** 메서드는 연결 중인 클라이언트에 서버 사용 중 오류가 반환되기 전에 **Socket**에 대해 허용되는 보류 연결 수를 지정하는 단일 매개 변수를 사용합니다. 이 경우 클라이언트 번호 101에 서버 사용 중 응답이 반환되기 전에 최대 100개의 클라이언트를 연결 큐에 둡니다.  
  
## <a name="see-also"></a>참고 항목

- [동기 서버 소켓 사용](using-a-synchronous-server-socket.md)
- [비동기 서버 소켓 사용](using-an-asynchronous-server-socket.md)
- [클라이언트 소켓 사용](using-client-sockets.md)
- [방법: 소켓 만들기](how-to-create-a-socket.md)
- [소켓](sockets.md)
