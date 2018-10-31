---
title: 비동기 서버 소켓 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- Socket class, asynchronous server sockets
- data requests, sockets
- sockets, asynchronous server sockets
- requesting data from Internet, sockets
- server sockets
- receiving data, sockets
- asynchronous server sockets
- protocols, sockets
- Internet, sockets
ms.assetid: 813489a9-3efd-41b6-a33f-371d55397676
ms.openlocfilehash: d51553b34f221283429d40a65e08f5ba58faf36a
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50198865"
---
# <a name="using-an-asynchronous-server-socket"></a>비동기 서버 소켓 사용
비동기 서버 소켓은 .NET Framework 비동기 프로그래밍 모델을 사용하여 네트워크 서비스 요청을 처리합니다. <xref:System.Net.Sockets.Socket> 클래스는 표준 .NET Framework 비동기 명명 패턴을 따릅니다. 예를 들어 동기 <xref:System.Net.Sockets.Socket.Accept%2A> 메서드는 비동기 <xref:System.Net.Sockets.Socket.BeginAccept%2A> 및 <xref:System.Net.Sockets.Socket.EndAccept%2A> 메서드에 해당합니다.  
  
 비동기 서버 소켓에는 네트워크의 연결 요청 허용을 시작하는 메서드, 연결 요청을 처리하고 네트워크에서 데이터 수신을 시작하는 콜백 메서드, 데이터 수신을 종료하는 콜백 메서드가 필요합니다. 이 섹션에서는 이러한 모든 메서드에 대해 자세히 설명합니다.  
  
 다음 예제에서 네트워크의 연결 요청 허용을 시작하기 위해 `StartListening` 메서드는 **Socket**을 초기화한 다음 **BeginAccept** 메서드를 사용하여 새 연결 허용을 시작합니다. 소켓에 새 연결 요청을 받으면 허용 콜백 메서드가 호출됩니다. 이 메서드는 연결을 처리할 **소켓** 인스턴스를 가져온 다음 요청을 처리할 스레드에 해당 **Socket**을 전달합니다. 허용 콜백 메서드는 <xref:System.AsyncCallback> 대리자를 구현합니다. void를 반환하고 <xref:System.IAsyncResult> 형식의 단일 매개 변수를 사용합니다. 다음 예제는 허용 콜백 메서드의 셸입니다.  
  
```vb  
Sub acceptCallback(ar As IAsyncResult)  
    ' Add the callback code here.  
End Sub 'acceptCallback  
```  
  
```csharp  
void acceptCallback( IAsyncResult ar) {  
    // Add the callback code here.  
}  
```  
  
 **BeginAccept** 메서드는 허용 콜백 메서드를 가리키는 **AsyncCallback** 대리자와 상태 정보를 콜백 메서드에 전달하는 데 사용되는 개체 등 두 개의 매개 변수를 사용합니다. 다음 예제에서 수신 대기하는 **Socket**은 *state* 매개 변수를 통해 콜백 메서드에 전달됩니다. 이 예제에서는 **AsyncCallback** 대리자를 만들고 네트워크 연결 허용을 시작합니다.  
  
```vb  
listener.BeginAccept( _  
    New AsyncCallback(SocketListener.acceptCallback),_  
    listener)  
```  
  
```csharp  
listener.BeginAccept(  
    new AsyncCallback(SocketListener.acceptCallback),   
    listener);  
```  
  
 비동기 소켓은 시스템 스레드 풀의 스레드를 사용하여 들어오는 연결을 처리합니다. 한 스레드는 연결을 허용하고, 다른 스레드는 들어오는 각 연결을 처리하는 데 사용되고, 마지막 스레드는 연결에서 데이터를 받습니다. 스레드 풀에서 할당된 스레드에 따라 세 스레드는 동일한 스레드일 수 있습니다. 다음 예제에서 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 클래스는 주 스레드의 실행을 일시 중단하고 실행을 계속할 수 있으면 알려줍니다.  
  
 다음 예제에서는 로컬 컴퓨터에 비동기 TCP/IP 소켓을 만들고 연결 허용을 시작하는 비동기 메서드를 보여 줍니다. `allDone`이라는 전역 **ManualResetEvent**가 있고, 메서드는 `SocketListener`라는 클래스의 멤버이고, `acceptCallback`이라는 콜백 메서드가 정의되어 있다고 가정합니다.  
  
```vb  
Public Sub StartListening()  
    Dim ipHostInfo As IPHostEntry = Dns.Resolve(Dns.GetHostName())  
    Dim localEP = New IPEndPoint(ipHostInfo.AddressList(0), 11000)  
  
    Console.WriteLine("Local address and port : {0}", localEP.ToString())  
  
    Dim listener As New Socket(localEP.Address.AddressFamily, _  
       SocketType.Stream, ProtocolType.Tcp)  
  
    Try  
        listener.Bind(localEP)  
        listener.Listen(10)  
  
        While True  
            allDone.Reset()  
  
            Console.WriteLine("Waiting for a connection...")  
            listener.BeginAccept(New _  
                AsyncCallback(SocketListener.acceptCallback), _  
                listener)  
  
            allDone.WaitOne()  
        End While  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
    Console.WriteLine("Closing the listener...")  
End Sub 'StartListening  
```  
  
```csharp  
public void StartListening() {  
    IPHostEntry ipHostInfo = Dns.Resolve(Dns.GetHostName());  
    IPEndPoint localEP = new IPEndPoint(ipHostInfo.AddressList[0],11000);  
  
    Console.WriteLine("Local address and port : {0}",localEP.ToString());  
  
    Socket listener = new Socket( localEP.Address.AddressFamily,  
        SocketType.Stream, ProtocolType.Tcp );  
  
    try {  
        listener.Bind(localEP);  
        listener.Listen(10);  
  
        while (true) {  
            allDone.Reset();  
  
            Console.WriteLine("Waiting for a connection...");  
            listener.BeginAccept(  
                new AsyncCallback(SocketListener.acceptCallback),   
                listener );  
  
            allDone.WaitOne();  
        }  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
  
    Console.WriteLine( "Closing the listener...");  
}  
```  
  
 허용 콜백 메서드(앞의 예제에서 `acceptCallback`)는 주 응용 프로그램 스레드에 처리를 계속하도록 알리고, 클라이언트에 연결하고, 클라이언트에서 비동기 데이터 읽기를 시작합니다. 다음 예제에서는 `acceptCallback` 메서드 구현의 첫 번째 부분을 보여 줍니다. 이 메서드 섹션은 주 응용 프로그램 스레드에 처리를 계속하도록 알리고 클라이언트에 연결합니다. `allDone`이라는 전역 **ManualResetEvent**를 가정합니다.  
  
```vb  
Public Sub acceptCallback(ar As IAsyncResult)  
    allDone.Set()  
  
    Dim listener As Socket = CType(ar.AsyncState, Socket)  
    Dim handler As Socket = listener.EndAccept(ar)  
  
    ' Additional code to read data goes here.  
End Sub 'acceptCallback  
```  
  
```csharp  
public void acceptCallback(IAsyncResult ar) {  
    allDone.Set();  
  
    Socket listener = (Socket) ar.AsyncState;  
    Socket handler = listener.EndAccept(ar);  
  
    // Additional code to read data goes here.    
}  
```  
  
 클라이언트 소켓에서 데이터를 읽으려면 비동기 호출 간에 값을 전달하는 상태 개체가 필요합니다. 다음 예제에서는 원격 클라이언트에서 문자열을 수신하는 상태 개체를 구현합니다. 클라이언트 소켓에 대한 필드, 데이터 수신을 위한 데이터 버퍼, 클라이언트에서 보낸 데이터 문자열을 수신하기 위한 <xref:System.Text.StringBuilder>가 포함되어 있습니다. 이러한 필드를 상태 개체에 배치하면 여러 호출 간에 개체 값을 보존하여 클라이언트 소켓에서 데이터를 읽을 수 있습니다.  
  
```vb  
Public Class StateObject  
    Public workSocket As Socket = Nothing  
    Public BufferSize As Integer = 1024  
    Public buffer(BufferSize) As Byte  
    Public sb As New StringBuilder()  
End Class 'StateObject  
```  
  
```csharp  
public class StateObject {  
    public Socket workSocket = null;  
    public const int BufferSize = 1024;  
    public byte[] buffer = new byte[BufferSize];  
    public StringBuilder sb = new StringBuilder();  
}  
```  
  
 클라이언트 소켓에서 데이터 수신을 시작하는 `acceptCallback` 메서드 섹션은 먼저 `StateObject` 클래스의 인스턴스를 초기화한 다음 <xref:System.Net.Sockets.Socket.BeginReceive%2A> 메서드를 호출하여 클라이언트 소켓에서 비동기적으로 데이터 읽기를 시작합니다.  
  
 다음 예제에서는 전체 `acceptCallback` 메서드를 보여 줍니다. `allDone,`이라는 전역 **ManualResetEvent**가 있고, `StateObject`가 정의되어 있고, `readCallback` 메서드가 `SocketListener`라는 클래스에 정의되어 있다고 가정합니다.  
  
```vb  
Public Shared Sub acceptCallback(ar As IAsyncResult)  
    ' Get the socket that handles the client request.  
    Dim listener As Socket = CType(ar.AsyncState, Socket)  
    Dim handler As Socket = listener.EndAccept(ar)  
  
    ' Signal the main thread to continue.  
    allDone.Set()  
  
    ' Create the state object.  
    Dim state As New StateObject()  
    state.workSocket = handler  
    handler.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
        AddressOf AsynchronousSocketListener.readCallback, state)  
End Sub 'acceptCallback  
```  
  
```csharp  
public static void acceptCallback(IAsyncResult ar) {  
    // Get the socket that handles the client request.  
    Socket listener = (Socket) ar.AsyncState;  
    Socket handler = listener.EndAccept(ar);  
  
    // Signal the main thread to continue.  
    allDone.Set();  
  
    // Create the state object.  
    StateObject state = new StateObject();  
    state.workSocket = handler;  
    handler.BeginReceive( state.buffer, 0, StateObject.BufferSize, 0,  
        new AsyncCallback(AsynchronousSocketListener.readCallback), state);  
}  
```  
  
 비동기 소켓 서버에 대해 구현해야 하는 최종 메서드는 클라이언트에서 보낸 데이터를 반환하는 읽기 콜백 메서드입니다. 허용 콜백 메서드와 마찬가지로 읽기 콜백 메서드는 **AsyncCallback** 대리자입니다. 이 메서드는 클라이언트 소켓에서 1바이트 이상을 데이터 버퍼로 읽어온 다음 클라이언트에서 보낸 데이터가 완료될 때까지 **BeginReceive** 메서드를 다시 호출합니다. 클라이언트에서 전체 메시지를 읽은 후 문자열이 콘솔에 표시되고 클라이언트에 대한 연결을 처리하는 서버 소켓이 닫힙니다.  
  
 다음 샘플에서는 `readCallback` 메서드를 구현합니다. `StateObject` 클래스가 정의되어 있다고 가정합니다.  
  
```vb  
Public Shared Sub readCallback(ar As IAsyncResult)  
    Dim state As StateObject = CType(ar.AsyncState, StateObject)  
    Dim handler As Socket = state.workSocket  
  
    ' Read data from the client socket.   
    Dim read As Integer = handler.EndReceive(ar)  
  
    ' Data was read from the client socket.  
    If read > 0 Then  
        state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, read))  
        handler.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
            AddressOf readCallback, state)  
    Else  
        If state.sb.Length > 1 Then  
            ' All the data has been read from the client;  
            ' display it on the console.  
            Dim content As String = state.sb.ToString()  
            Console.WriteLine("Read {0} bytes from socket." + _  
                ControlChars.Cr + " Data : {1}", content.Length, content)  
        End If  
    End If  
End Sub 'readCallback  
```  
  
```csharp  
public static void readCallback(IAsyncResult ar) {  
    StateObject state = (StateObject) ar.AsyncState;  
    Socket handler = state.WorkSocket;  
  
    // Read data from the client socket.  
    int read = handler.EndReceive(ar);  
  
    // Data was read from the client socket.  
    if (read > 0) {  
        state.sb.Append(Encoding.ASCII.GetString(state.buffer,0,read));  
        handler.BeginReceive(state.buffer,0,StateObject.BufferSize, 0,  
            new AsyncCallback(readCallback), state);  
    } else {  
        if (state.sb.Length > 1) {  
            // All the data has been read from the client;  
            // display it on the console.  
            string content = state.sb.ToString();  
            Console.WriteLine("Read {0} bytes from socket.\n Data : {1}",  
               content.Length, content);  
        }  
        handler.Close();  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [동기 서버 소켓 사용](../../../docs/framework/network-programming/using-a-synchronous-server-socket.md)  
 [비동기 서버 소켓 예제](../../../docs/framework/network-programming/asynchronous-server-socket-example.md)  
 [스레딩](../../../docs/standard/threading/index.md)  
 [소켓으로 수신](../../../docs/framework/network-programming/listening-with-sockets.md)
