---
title: 클라이언트 소켓 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- receiving data, sockets
- Socket class, client sockets
- protocols, sockets
- Internet, sockets
- sockets, client sockets
- client sockets
ms.assetid: 81de9f59-8177-4d98-b25d-43fc32a98383
ms.openlocfilehash: fe2ad55c3f60347369c0e92bc834d81d98f3870e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046953"
---
# <a name="using-client-sockets"></a>클라이언트 소켓 사용
<xref:System.Net.Sockets.Socket>을 통해 대화를 시작하려면 먼저 애플리케이션과 원격 디바이스 간에 데이터 파이프를 만들어야 합니다. 다른 네트워크 주소 패밀리 및 프로토콜이 있어도 이 예제에서는 원격 서비스에 대한 TCP/IP 연결을 만드는 방법을 보여 줍니다.  
  
 TCP/IP는 네트워크 주소와 서비스 포트 번호를 사용하여 서비스를 고유하게 식별합니다. 네트워크 주소는 네트워크에서 특정 디바이스를 식별하고, 포트 번호는 연결할 해당 디바이스의 특정 서비스를 식별합니다. 네트워크 주소와 서비스 포트의 조합을 엔드포인트가라고 하며, .NET Framework에서는 <xref:System.Net.EndPoint> 클래스로 표현됩니다. **EndPoint**의 하위 항목이 지원되는 각 주소 패밀리에 대해 정의되고, IP 주소 패밀리에 대한 클래스는 <xref:System.Net.IPEndPoint>입니다.  
  
 <xref:System.Net.Dns> 클래스는 TCP/IP 인터넷 서비스를 사용하는 애플리케이션에 도메인 이름 서비스를 제공합니다. <xref:System.Net.Dns.Resolve%2A> 메서드는 DNS 서버를 쿼리하여 친숙한 도메인 이름(예: “host.contoso.com”)을 숫자 인터넷 주소(예: 192.168.1.1)에 매핑합니다. **Resolve**는 요청된 이름에 대한 주소 및 별칭 목록이 들어 있는 <xref:System.Net.IPHostEntry>를 반환합니다. 대부분의 경우 <xref:System.Net.IPHostEntry.AddressList%2A> 배열에 반환된 첫 번째 주소를 사용할 수 있습니다. 다음 코드에서는 host.contoso.com 서버의 IP 주소가 포함된 <xref:System.Net.IPAddress>를 가져옵니다.  
  
```vb  
Dim ipHostInfo As IPHostEntry = Dns.Resolve("host.contoso.com")  
Dim ipAddress As IPAddress = ipHostInfo.AddressList(0)  
```  
  
```csharp  
IPHostEntry ipHostInfo = Dns.Resolve("host.contoso.com");  
IPAddress ipAddress = ipHostInfo.AddressList[0];  
```  
  
 IANA(Internet Assigned Numbers Authority)는 공통 서비스의 포트 번호를 정의합니다. 자세한 내용은 [Service Name and Transport Protocol Port Number Registry](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)(서비스 이름 및 전송 프로토콜 포트 번호 레지스트리)를 참조하세요. 다른 서비스에는 1,024 ~ 65,535 범위의 등록된 포트 번호가 있을 수 있습니다. 다음 코드에서는 host.contoso.com의 IP 주소를 포트 번호와 결합하여 연결에 대한 원격 엔드포인트를 만듭니다.  
  
```vb  
Dim ipe As New IPEndPoint(ipAddress, 11000)  
```  
  
```csharp  
IPEndPoint ipe = new IPEndPoint(ipAddress,11000);  
```  
  
 원격 디바이스의 주소를 결정하고 연결에 사용할 포트를 선택하면 애플리케이션이 원격 디바이스에 대한 연결을 시도할 수 있습니다. 다음 예제에서는 기존 **IPEndPoint**를 사용하여 원격 디바이스에 연결하고 throw되는 예외를 catch합니다.  
  
```vb  
Try  
    s.Connect(ipe)  
Catch ae As ArgumentNullException  
    Console.WriteLine("ArgumentNullException : {0}", _  
        ae.ToString())  
Catch se As SocketException  
    Console.WriteLine("SocketException : {0}", se.ToString())  
Catch e As Exception  
    Console.WriteLine("Unexpected exception : {0}", e.ToString())  
End Try  
```  
  
```csharp  
try {  
    s.Connect(ipe);  
} catch(ArgumentNullException ae) {  
    Console.WriteLine("ArgumentNullException : {0}", ae.ToString());  
} catch(SocketException se) {  
    Console.WriteLine("SocketException : {0}", se.ToString());  
} catch(Exception e) {  
    Console.WriteLine("Unexpected exception : {0}", e.ToString());  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [동기 클라이언트 소켓 사용](using-a-synchronous-client-socket.md)
- [비동기 클라이언트 소켓 사용](using-an-asynchronous-client-socket.md)
- [방법: 소켓 만들기](how-to-create-a-socket.md)
- [소켓](sockets.md)
