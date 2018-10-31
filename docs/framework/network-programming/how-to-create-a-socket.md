---
title: '방법: 소켓 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- Networking
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- Socket class, creating sockets
- Network Resources
- receiving data, sockets
- protocols, sockets
- Internet, sockets
- sockets, creating
ms.assetid: c64a049c-5981-43bc-a2dc-1851473589c7
ms.openlocfilehash: 2c3bfb6435901ac8154bc801ae2a420b252d5849
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202265"
---
# <a name="how-to-create-a-socket"></a>방법: 소켓 만들기
소켓을 사용하여 원격 장치와 통신하려면 먼저 프로토콜 및 네트워크 주소 정보를 사용하여 소켓을 초기화해야 합니다. <xref:System.Net.Sockets.Socket> 클래스에 대한 생성자에는 소켓이 연결을 만드는 데 사용하는 주소 패밀리, 소켓 형식 및 프로토콜 형식을 지정하는 매개 변수가 있습니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 인터넷 같은 TCP/IP 기반 네트워크에서 통신하는 데 사용될 수 있는 소켓을 만듭니다.  
  
```csharp  
Socket s = new Socket(AddressFamily.InterNetwork,   
   SocketType.Stream, ProtocolType.Tcp);  
```  
  
```vb  
Dim s as New Socket(AddressFamily.InterNetwork, _  
   SocketType.Stream, ProtocolType.Tcp)  
```  
  
 TCP 대신 UDP를 사용하려면 다음 예제와 같이 프로토콜 형식을 변경합니다.  
  
```csharp  
Socket s = new Socket(AddressFamily.InterNetwork,   
   SocketType.Dgram, ProtocolType.Udp);  
```  
  
```vb  
Dim s as New Socket(AddressFamily.InterNetwork, _  
   SocketType.Dgram, ProtocolType.Udp)  
```  
  
 <xref:System.Net.Sockets.AddressFamily> 열거형은 **Socket** 클래스에서 네트워크 주소를 확인하는 데 사용되는 표준 주소 패밀리를 지정합니다. 예를 들어 **AddressFamily.InterNetwork** 멤버는 IP 버전 4 주소 패밀리를 지정합니다.  
  
 <xref:System.Net.Sockets.SocketType> 열거형은 소켓 형식을 지정합니다. 예를 들어 **SocketType.Stream** 멤버는 흐름 컨트롤을 통해 데이터를 보내고 받기 위한 표준 소켓을 나타냅니다.  
  
 <xref:System.Net.Sockets.ProtocolType> 열거형은 **소켓**에서 통신할 때 사용할 네트워크 프로토콜을 지정합니다. 예를 들어 **ProtocolType.Tcp**는 소켓이 TCP를 사용함을 나타내고 **ProtocolType.Udp**는 소켓이 UDP를 사용함을 나타냅니다.  
  
 **소켓**이 만들어진 후 원격 엔드포인트에 대한 연결을 시작하거나 원격 장치에서 연결을 수신할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 소켓 사용](../../../docs/framework/network-programming/using-client-sockets.md)  
 [소켓으로 수신](../../../docs/framework/network-programming/listening-with-sockets.md)
