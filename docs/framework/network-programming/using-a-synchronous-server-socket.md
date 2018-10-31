---
title: 동기 서버 소켓 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- synchronous server sockets
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- server sockets
- receiving data, sockets
- Socket class, synchronous server sockets
- protocols, sockets
- sockets, synchronous server sockets
- Internet, sockets
ms.assetid: d1ce882e-653e-41f5-9289-844ec855b804
ms.openlocfilehash: 9880766641be618a6a0f54ded501cf6f6e95e128
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50034360"
---
# <a name="using-a-synchronous-server-socket"></a>동기 서버 소켓 사용
동기 서버 소켓은 소켓에 연결 요청이 수신될 때까지 응용 프로그램 실행을 일시 중단합니다. 동기 서버 소켓은 네트워크를 작업에 많이 사용하는 응용 프로그램에 적합하지 않지만 간단한 네트워크 응용 프로그램에는 적합할 수 있습니다.  
  
 <xref:System.Net.Sockets.Socket>이 <xref:System.Net.Sockets.Socket.Bind%2A> 및 <xref:System.Net.Sockets.Socket.Listen%2A> 메서드를 사용하여 엔드포인트에서 수신 대기하도록 설정되면 <xref:System.Net.Sockets.Socket.Accept%2A> 메서드를 사용하여 들어오는 연결 요청을 허용할 수 있습니다. **Accept** 메서드를 호출하면 연결 요청이 수신될 때까지 응용 프로그램이 일시 중단됩니다.  
  
 연결 요청이 수신되면 **Accept**는 연결 중인 클라이언트와 연결된 새 **Socket** 인스턴스를 반환합니다. 다음 예제에서는 클라이언트에서 데이터를 읽고 콘솔에 표시한 다음 데이터를 클라이언트에 다시 에코합니다. **Socket**은 메시징 프로토콜을 지정하지 않으므로 “\<EOF>” 문자열은 메시지 데이터의 끝을 표시합니다. `listener`라는 **Socket**이 초기화되었으며 엔드포인트에 바인딩되었다고 가정합니다.  
  
```vb  
Console.WriteLine("Waiting for a connection...")  
Dim handler As Socket = listener.Accept()  
Dim data As String = Nothing  
  
While True  
    bytes = New Byte(1024) {}  
    Dim bytesRec As Integer = handler.Receive(bytes)  
    data += Encoding.ASCII.GetString(bytes, 0, bytesRec)  
    If data.IndexOf("<EOF>") > - 1 Then  
        Exit While  
    End If  
End While  
  
Console.WriteLine("Text received : {0}", data)  
  
Dim msg As Byte() = Encoding.ASCII.GetBytes(data)  
handler.Send(msg)  
handler.Shutdown(SocketShutdown.Both)  
handler.Close()  
```  
  
```csharp  
Console.WriteLine("Waiting for a connection...");  
Socket handler = listener.Accept();  
String data = null;  
  
while (true) {  
    bytes = new byte[1024];  
    int bytesRec = handler.Receive(bytes);  
    data += Encoding.ASCII.GetString(bytes,0,bytesRec);  
    if (data.IndexOf("<EOF>") > -1) {  
        break;  
    }  
}  
  
Console.WriteLine( "Text received : {0}", data);  
  
byte[] msg = Encoding.ASCII.GetBytes(data);  
handler.Send(msg);  
handler.Shutdown(SocketShutdown.Both);  
handler.Close();  
```  
  
## <a name="see-also"></a>참고 항목  
 [비동기 서버 소켓 사용](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)  
 [동기 서버 소켓 예제](../../../docs/framework/network-programming/synchronous-server-socket-example.md)  
 [소켓으로 수신](../../../docs/framework/network-programming/listening-with-sockets.md)
