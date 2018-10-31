---
title: 비동기 클라이언트 소켓 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- asynchronous client sockets
- Socket class, asynchronous client sockets
- requesting data from Internet, sockets
- sockets, asynchronous client sockets
- receiving data, sockets
- protocols, sockets
- Internet, sockets
- client sockets
ms.assetid: fd85bc88-e06c-467d-a30d-9fd7cffcfca1
ms.openlocfilehash: 386b9d3cf0342784c09ed8fc7a815a242924b068
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50194958"
---
# <a name="using-an-asynchronous-client-socket"></a>비동기 클라이언트 소켓 사용
비동기 클라이언트 소켓은 네트워크 작업이 완료될 때까지 기다리는 동안 응용 프로그램을 일시 중단하지 않습니다. 대신, 표준 .NET Framework 비동기 프로그래밍 모델을 사용하여 응용 프로그램이 원래 스레드에서 계속 실행되는 동안 한 스레드에서 네트워크 연결을 처리합니다. 비동기 소켓은 네트워크를 많이 사용하거나 계속하기 전에 네트워크 작업이 완료될 때까지 기다릴 수 없는 응용 프로그램에 적합합니다.  
  
 <xref:System.Net.Sockets.Socket> 클래스는 비동기 메서드에 대한 .NET Framework 명명 패턴을 따릅니다. 예를 들어 동기 <xref:System.Net.Sockets.Socket.Receive%2A> 메서드는 비동기 <xref:System.Net.Sockets.Socket.BeginReceive%2A> 및 <xref:System.Net.Sockets.Socket.EndReceive%2A> 메서드에 해당합니다.  
  
 비동기 작업에서는 콜백 메서드가 작업 결과를 반환해야 합니다. 응용 프로그램이 결과를 알 필요가 없는 경우 콜백 메서드가 필요하지 않습니다. 이 섹션의 예제 코드에서는 메서드를 사용하여 네트워크 장치에 연결을 시작하고 콜백 메서드를 사용하여 연결을 완료하는 방법, 메서드를 사용하여 데이터 전송을 시작하고 콜백 메서드를 사용하여 전송을 완료하는 방법, 메서드를 사용하여 데이터 수신을 시작하고 콜백 메서드를 사용하여 데이터 수신을 끝내는 방법을 보여 줍니다.  
  
 비동기 소켓은 시스템 스레드 풀의 여러 스레드를 사용하여 네트워크 연결을 처리합니다. 한 스레드는 데이터 전송 또는 수신을 시작하고, 다른 스레드는 네트워크 장치에 대한 연결을 완료하고 데이터를 보내거나 받습니다. 다음 예제에서 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 클래스 인스턴스는 주 스레드의 실행을 일시 중단하고 실행을 계속할 수 있으면 알려주는 데 사용됩니다.  
  
 다음 예제에서 비동기 소켓을 네트워크 장치에 연결하기 위해 `Connect` 메서드는 **Socket**을 초기화한 다음 <xref:System.Net.Sockets.Socket.Connect%2A?displayProperty=nameWithType> 메서드를 호출하고 네트워크 장치를 나타내는 원격 엔드포인트, 연결 콜백 메서드 및 비동기 호출 간에 상태 정보를 전달하는 데 사용되는 상태 개체(클라이언트 **Socket**)를 전달합니다. 이 예제에서는 `Connect` 메서드를 구현하여 지정된 **Socket**을 지정된 엔드포인트에 연결합니다. `connectDone`이라는 전역 **ManualResetEvent**를 가정합니다.  
  
```vb  
Public Shared Sub Connect(remoteEP As EndPoint, client As Socket)  
    client.BeginConnect(remoteEP, _  
       AddressOf ConnectCallback, client)  
  
    connectDone.WaitOne()  
End Sub 'Connect  
```  
  
```csharp  
public static void Connect(EndPoint remoteEP, Socket client) {  
    client.BeginConnect(remoteEP,   
        new AsyncCallback(ConnectCallback), client );  
  
   connectDone.WaitOne();  
}  
```  
  
 연결 콜백 메서드 `ConnectCallback`은 <xref:System.AsyncCallback> 대리자를 구현합니다. 원격 장치를 사용할 수 있는 경우 원격 장치에 연결한 다음 **ManualResetEvent** `connectDone`을 설정하여 연결이 완료되었음을 응용 프로그램 스레드에 알립니다. 다음 코드에서는 `ConnectCallback` 메서드를 구현합니다.  
  
```vb  
Private Shared Sub ConnectCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the socket from the state object.  
        Dim client As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete the connection.  
        client.EndConnect(ar)  
  
        Console.WriteLine("Socket connected to {0}", _  
            client.RemoteEndPoint.ToString())  
  
        ' Signal that the connection has been made.  
        connectDone.Set()  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'ConnectCallback  
```  
  
```csharp  
private static void ConnectCallback(IAsyncResult ar) {  
    try {  
        // Retrieve the socket from the state object.  
        Socket client = (Socket) ar.AsyncState;  
  
        // Complete the connection.  
        client.EndConnect(ar);  
  
        Console.WriteLine("Socket connected to {0}",  
            client.RemoteEndPoint.ToString());  
  
        // Signal that the connection has been made.  
        connectDone.Set();  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 예제 메서드 `Send`는 지정된 문자열 데이터를 ASCII 형식으로 인코드하고 지정된 소켓이 나타내는 네트워크 장치에 비동기적으로 보냅니다. 다음 예제에서는 `Send` 메서드를 구현합니다.  
  
```vb  
Private Shared Sub Send(client As Socket, data As [String])  
    ' Convert the string data to byte data using ASCII encoding.  
    Dim byteData As Byte() = Encoding.ASCII.GetBytes(data)  
  
    ' Begin sending the data to the remote device.  
    client.BeginSend(byteData, 0, byteData.Length, SocketFlags.None, _  
        AddressOf SendCallback, client)  
End Sub 'Send  
```  
  
```csharp  
private static void Send(Socket client, String data) {  
    // Convert the string data to byte data using ASCII encoding.  
    byte[] byteData = Encoding.ASCII.GetBytes(data);  
  
    // Begin sending the data to the remote device.  
    client.BeginSend(byteData, 0, byteData.Length, SocketFlags.None,  
        new AsyncCallback(SendCallback), client);  
}  
```  
  
 전송 콜백 메서드 `SendCallback`은 <xref:System.AsyncCallback> 대리자를 구현합니다. 네트워크 장치가 수신할 준비가 되면 데이터를 보냅니다. 다음 예제에서는 `SendCallback` 메서드의 구현을 보여 줍니다. `sendDone`이라는 전역 **ManualResetEvent**를 가정합니다.  
  
```vb  
Private Shared Sub SendCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the socket from the state object.  
        Dim client As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete sending the data to the remote device.  
        Dim bytesSent As Integer = client.EndSend(ar)  
        Console.WriteLine("Sent {0} bytes to server.", bytesSent)  
  
        ' Signal that all bytes have been sent.  
        sendDone.Set()  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'SendCallback  
```  
  
```csharp  
private static void SendCallback(IAsyncResult ar) {  
    try {  
        // Retrieve the socket from the state object.  
        Socket client = (Socket) ar.AsyncState;  
  
        // Complete sending the data to the remote device.  
        int bytesSent = client.EndSend(ar);  
        Console.WriteLine("Sent {0} bytes to server.", bytesSent);  
  
        // Signal that all bytes have been sent.  
        sendDone.Set();  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 클라이언트 소켓에서 데이터를 읽으려면 비동기 호출 간에 값을 전달하는 상태 개체가 필요합니다. 다음 클래스는 클라이언트 소켓에서 데이터를 수신하기 위한 예제 상태 개체입니다. 클라이언트 소켓에 대한 필드, 수신된 데이터에 대한 버퍼, 들어오는 데이터 문자열을 저장할 <xref:System.Text.StringBuilder>가 포함되어 있습니다. 이러한 필드를 상태 개체에 배치하면 여러 호출 간에 개체 값을 보존하여 클라이언트 소켓에서 데이터를 읽을 수 있습니다.  
  
```vb  
Public Class StateObject  
    ' Client socket.  
    Public workSocket As Socket = Nothing   
    ' Size of receive buffer.  
    Public BufferSize As Integer = 256  
    ' Receive buffer.  
    Public buffer(256) As Byte   
    ' Received data string.  
    Public sb As New StringBuilder()  
End Class 'StateObject  
```  
  
```csharp  
public class StateObject {  
    // Client socket.  
    public Socket workSocket = null;  
    // Size of receive buffer.  
    public const int BufferSize = 256;  
    // Receive buffer.  
    public byte[] buffer = new byte[BufferSize];  
    // Received data string.  
    public StringBuilder sb = new StringBuilder();  
}  
```  
  
 예제 `Receive` 메서드는 상태 개체를 설정한 다음 **BeginReceive** 메서드를 호출하여 클라이언트 소켓에서 데이터를 비동기적으로 읽습니다. 다음 예제에서는 `Receive` 메서드를 구현합니다.  
  
```vb  
Private Shared Sub Receive(client As Socket)  
    Try  
        ' Create the state object.  
        Dim state As New StateObject()  
        state.workSocket = client  
  
        ' Begin receiving the data from the remote device.  
        client.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
            AddressOf ReceiveCallback, state)  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'Receive  
```  
  
```csharp  
private static void Receive(Socket client) {  
    try {  
        // Create the state object.  
        StateObject state = new StateObject();  
        state.workSocket = client;  
  
        // Begin receiving the data from the remote device.  
        client.BeginReceive( state.buffer, 0, StateObject.BufferSize, 0,  
            new AsyncCallback(ReceiveCallback), state);  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 수신 콜백 메서드 `ReceiveCallback`은 **AsyncCallback** 대리자를 구현합니다. 네트워크 장치에서 데이터를 수신하고 메시지 문자열을 작성합니다. 네트워크에서 1바이트 이상의 데이터를 데이터 버퍼로 읽어온 다음 클라이언트에서 보낸 데이터가 완료될 때까지 **BeginReceive** 메서드를 다시 호출합니다. 클라이언트에서 모든 데이터를 읽은 후 `ReceiveCallback`은 **ManualResetEvent** `sendDone`을 설정하여 데이터가 완료되었음을 응용 프로그램 스레드에 알립니다.  
  
 다음 예제 코드에서는 `ReceiveCallback` 메서드를 구현합니다. 받은 문자열을 저장하는 `response`라는 전역 문자열과 `receiveDone`이라는 전역 **ManualResetEvent**를 가정합니다. 서버는 네트워크 세션을 종료하기 위해 클라이언트 소켓을 정상적으로 종료해야 합니다.  
  
```vb  
Private Shared Sub ReceiveCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the state object and the client socket   
        ' from the asynchronous state object.  
        Dim state As StateObject = CType(ar.AsyncState, StateObject)  
        Dim client As Socket = state.workSocket  
  
        ' Read data from the remote device.  
        Dim bytesRead As Integer = client.EndReceive(ar)  
  
        If bytesRead > 0 Then  
            ' There might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, _  
                bytesRead))  
  
            '  Get the rest of the data.  
            client.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
                AddressOf ReceiveCallback, state)  
        Else  
            ' All the data has arrived; put it in response.  
            If state.sb.Length > 1 Then  
                response = state.sb.ToString()  
            End If  
            ' Signal that all bytes have been received.  
            receiveDone.Set()  
        End If  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'ReceiveCallback  
```  
  
```csharp  
private static void ReceiveCallback( IAsyncResult ar ) {  
    try {  
        // Retrieve the state object and the client socket   
        // from the asynchronous state object.  
        StateObject state = (StateObject) ar.AsyncState;  
        Socket client = state.workSocket;  
        // Read data from the remote device.  
        int bytesRead = client.EndReceive(ar);  
        if (bytesRead > 0) {  
            // There might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer,0,bytesRead));  
                //  Get the rest of the data.  
            client.BeginReceive(state.buffer,0,StateObject.BufferSize,0,  
                new AsyncCallback(ReceiveCallback), state);  
        } else {  
            // All the data has arrived; put it in response.  
            if (state.sb.Length > 1) {  
                response = state.sb.ToString();  
            }  
            // Signal that all bytes have been received.  
            receiveDone.Set();  
        }  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [동기 클라이언트 소켓 사용](../../../docs/framework/network-programming/using-a-synchronous-client-socket.md)  
 [소켓으로 수신](../../../docs/framework/network-programming/listening-with-sockets.md)  
 [비동기 클라이언트 소켓 예제](../../../docs/framework/network-programming/asynchronous-client-socket-example.md)
