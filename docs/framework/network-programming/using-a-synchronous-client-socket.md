---
title: 동기 클라이언트 소켓 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- synchronous client sockets
- Socket class, synchronous client sockets
- receiving data, sockets
- sockets, synchronous client sockets
- protocols, sockets
- Internet, sockets
- client sockets
ms.assetid: 945d00c6-7202-466c-9df9-140b84156d43
ms.openlocfilehash: 8036421f937385edbaefb8df4ee3915798084c64
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50192436"
---
# <a name="using-a-synchronous-client-socket"></a>동기 클라이언트 소켓 사용
동기 클라이언트 소켓은 네트워크 작업이 완료되는 동안 응용 프로그램을 일시 중단합니다. 동기 소켓은 네트워크를 작업에 많이 사용하는 응용 프로그램에 적합하지 않지만 다른 응용 프로그램의 네트워크 서비스에 대한 간단한 액세스를 가능하게 합니다.  
  
 데이터를 보내려면 바이트 배열을 <xref:System.Net.Sockets.Socket> 클래스의 데이터 전송 메서드(<xref:System.Net.Sockets.Socket.Send%2A> 및 <xref:System.Net.Sockets.Socket.SendTo%2A>) 중 하나에 전달합니다. 다음 예제에서는 <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType> 속성을 사용하여 문자열을 바이트 배열 버퍼로 인코드한 다음 **Send** 메서드를 사용하여 버퍼를 네트워크 장치에 전송합니다. **Send** 메서드는 네트워크 장치에 전송된 바이트 수를 반환합니다.  
  
```vb  
Dim msg As Byte() = _  
    System.Text.Encoding.ASCII.GetBytes("This is a test.")  
Dim bytesSent As Integer = s.Send(msg)  
```  
  
```csharp  
byte[] msg = System.Text.Encoding.ASCII.GetBytes("This is a test");  
int bytesSent = s.Send(msg);  
```  
  
 **Send** 메서드는 버퍼에서 바이트를 제거하고 네트워크 인터페이스를 사용하여 네트워크 장치에 전송되도록 큐에 대기시킵니다. 네트워크 인터페이스에서 데이터를 즉시 전송하지 않을 수도 있지만, 연결이 <xref:System.Net.Sockets.Socket.Shutdown%2A> 메서드를 사용하여 정상적으로 닫히기만 하면 결국 전송합니다.  
  
 네트워크 장치에서 데이터를 수신하려면 버퍼를 **Socket** 클래스의 데이터 수신 메서드(<xref:System.Net.Sockets.Socket.Receive%2A> 및 <xref:System.Net.Sockets.Socket.ReceiveFrom%2A>) 중 하나에 전달합니다. 네트워크에서 바이트가 수신되거나 소켓이 닫힐 때까지 동기 소켓이 응용 프로그램을 일시 중단합니다. 다음 예제에서는 네트워크에서 데이터를 수신한 후 콘솔에 표시합니다. 이 예제에서는 네트워크에서 들어오는 데이터가 ASCII로 인코드된 텍스트라고 가정합니다. **Receive** 메서드는 네트워크에서 받은 바이트 수를 반환합니다.  
  
```vb  
Dim bytes(1024) As Byte  
Dim bytesRec = s.Receive(bytes)  
Console.WriteLine("Echoed text = {0}", _  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec))  
```  
  
```csharp  
byte[] bytes = new byte[1024];  
int bytesRec = s.Receive(bytes);  
Console.WriteLine("Echoed text = {0}",  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec));  
```  
  
 소켓이 더 이상 필요하지 않은 경우 <xref:System.Net.Sockets.Socket.Shutdown%2A> 메서드를 호출한 다음 **Close** 메서드를 호출하여 소켓을 해제해야 합니다. 다음 예제에서는 **Socket**을 해제합니다. <xref:System.Net.Sockets.SocketShutdown> 열거형은 전송, 수신 또는 둘 다를 위해 소켓을 닫아야 하는지 여부를 나타내는 상수를 정의합니다.  
  
```vb  
s.Shutdown(SocketShutdown.Both)  
s.Close()  
```  
  
```csharp  
s.Shutdown(SocketShutdown.Both);  
s.Close();  
```  
  
## <a name="see-also"></a>참고 항목  
 [비동기 클라이언트 소켓 사용](../../../docs/framework/network-programming/using-an-asynchronous-client-socket.md)  
 [소켓으로 수신](../../../docs/framework/network-programming/listening-with-sockets.md)  
 [동기 클라이언트 소켓 예제](../../../docs/framework/network-programming/synchronous-client-socket-example.md)
