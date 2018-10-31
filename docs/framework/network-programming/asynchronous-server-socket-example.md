---
title: 비동기 서버 소켓 예제
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sockets, asynchronous server sockets
- sockets, code examples
- asynchronous server sockets
ms.assetid: 13624cd3-f5c5-4950-8cda-31273b1fa6d1
ms.openlocfilehash: 26b5c53c4983aa392dba7346f357e2700cfe0178
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50088691"
---
# <a name="asynchronous-server-socket-example"></a>비동기 서버 소켓 예제
다음 예제 프로그램은 클라이언트의 연결 요청을 수신하는 서버를 만듭니다. 이 서버는 비동기 소켓으로 빌드되므로 클라이언트의 연결을 대기하는 동안 서버 응용 프로그램의 실행이 일시 중단되지 않습니다. 응용 프로그램은 클라이언트에서 문자열을 받아 콘솔에 문자열을 표시한 다음 문자열을 클라이언트에 다시 에코합니다. 클라이언트의 문자열에는 메시지의 끝을 알리는 “\<EOF >” 문자열이 포함되어야 합니다.  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Net.Sockets  
Imports System.Text  
Imports System.Threading  
Imports Microsoft.VisualBasic  
  
' State object for reading client data asynchronously  
  
Public Class StateObject  
    ' Client  socket.  
    Public workSocket As Socket = Nothing  
    ' Size of receive buffer.  
    Public Const BufferSize As Integer = 1024  
    ' Receive buffer.  
    Public buffer(BufferSize) As Byte  
    ' Received data string.  
    Public sb As New StringBuilder  
End Class 'StateObject  
  
Public Class AsynchronousSocketListener  
    ' Thread signal.  
    Public Shared allDone As New ManualResetEvent(False)  
  
    ' This server waits for a connection and then uses  asychronous operations to  
    ' accept the connection, get data from the connected client,   
    ' echo that data back to the connected client.  
    ' It then disconnects from the client and waits for another client.   
    Public Shared Sub Main()  
        ' Establish the local endpoint for the socket.  
        Dim ipHostInfo As IPHostEntry = Dns.GetHostEntry(Dns.GetHostName())  
        Dim ipAddress As IPAddress = ipHostInfo.AddressList(0)  
        Dim localEndPoint As New IPEndPoint(ipAddress, 11000)  
  
        ' Create a TCP/IP socket.  
        Dim listener As New Socket(ipAddress.AddressFamily, SocketType.Stream, ProtocolType.Tcp)  
  
        ' Bind the socket to the local endpoint and listen for incoming connections.  
        listener.Bind(localEndPoint)  
        listener.Listen(100)  
  
        While True  
            ' Set the event to nonsignaled state.  
            allDone.Reset()  
  
            ' Start an asynchronous socket to listen for connections.  
            Console.WriteLine("Waiting for a connection...")  
            listener.BeginAccept(New AsyncCallback(AddressOf AcceptCallback), listener)  
  
            ' Wait until a connection is made and processed before continuing.  
            allDone.WaitOne()  
        End While  
    End Sub 'Main  
  
    Public Shared Sub AcceptCallback(ByVal ar As IAsyncResult)  
        ' Get the socket that handles the client request.  
        Dim listener As Socket = CType(ar.AsyncState, Socket)  
        ' End the operation.  
        Dim handler As Socket = listener.EndAccept(ar)  
  
        ' Create the state object for the async receive.  
        Dim state As New StateObject  
        state.workSocket = handler  
        handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0, New AsyncCallback(AddressOf ReadCallback), state)  
    End Sub 'AcceptCallback  
  
    Public Shared Sub ReadCallback(ByVal ar As IAsyncResult)  
        Dim content As String = String.Empty  
  
        ' Retrieve the state object and the handler socket  
        ' from the asynchronous state object.  
        Dim state As StateObject = CType(ar.AsyncState, StateObject)  
        Dim handler As Socket = state.workSocket  
  
        ' Read data from the client socket.   
        Dim bytesRead As Integer = handler.EndReceive(ar)  
  
        If bytesRead > 0 Then  
            ' There  might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, bytesRead))  
  
            ' Check for end-of-file tag. If it is not there, read   
            ' more data.  
            content = state.sb.ToString()  
            If content.IndexOf("<EOF>") > -1 Then  
                ' All the data has been read from the   
                ' client. Display it on the console.  
                Console.WriteLine("Read {0} bytes from socket. " + vbLf + " Data : {1}", content.Length, content)  
                ' Echo the data back to the client.  
                Send(handler, content)  
            Else  
                ' Not all data received. Get more.  
                handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0, New AsyncCallback(AddressOf ReadCallback), state)  
            End If  
        End If  
    End Sub 'ReadCallback  
  
    Private Shared Sub Send(ByVal handler As Socket, ByVal data As String)  
        ' Convert the string data to byte data using ASCII encoding.  
        Dim byteData As Byte() = Encoding.ASCII.GetBytes(data)  
  
        ' Begin sending the data to the remote device.  
        handler.BeginSend(byteData, 0, byteData.Length, 0, New AsyncCallback(AddressOf SendCallback), handler)  
    End Sub 'Send  
  
    Private Shared Sub SendCallback(ByVal ar As IAsyncResult)  
        ' Retrieve the socket from the state object.  
        Dim handler As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete sending the data to the remote device.  
        Dim bytesSent As Integer = handler.EndSend(ar)  
        Console.WriteLine("Sent {0} bytes to client.", bytesSent)  
  
        handler.Shutdown(SocketShutdown.Both)  
        handler.Close()  
        ' Signal the main thread to continue.  
        allDone.Set()  
    End Sub 'SendCallback  
End Class 'AsynchronousSocketListener  
```  
  
```csharp  
using System;  
using System.Net;  
using System.Net.Sockets;  
using System.Text;  
using System.Threading;  
  
// State object for reading client data asynchronously  
public class StateObject {  
    // Client  socket.  
    public Socket workSocket = null;  
    // Size of receive buffer.  
    public const int BufferSize = 1024;  
    // Receive buffer.  
    public byte[] buffer = new byte[BufferSize];  
// Received data string.  
    public StringBuilder sb = new StringBuilder();    
}  
  
public class AsynchronousSocketListener {  
    // Thread signal.  
    public static ManualResetEvent allDone = new ManualResetEvent(false);  
  
    public AsynchronousSocketListener() {  
    }  
  
    public static void StartListening() {  
        // Establish the local endpoint for the socket.  
        // The DNS name of the computer  
        // running the listener is "host.contoso.com".  
        IPHostEntry ipHostInfo = Dns.GetHostEntry(Dns.GetHostName());  
        IPAddress ipAddress = ipHostInfo.AddressList[0];  
        IPEndPoint localEndPoint = new IPEndPoint(ipAddress, 11000);  
  
        // Create a TCP/IP socket.  
        Socket listener = new Socket(ipAddress.AddressFamily,  
            SocketType.Stream, ProtocolType.Tcp );  
  
        // Bind the socket to the local endpoint and listen for incoming connections.  
        try {  
            listener.Bind(localEndPoint);  
            listener.Listen(100);  
  
            while (true) {  
                // Set the event to nonsignaled state.  
                allDone.Reset();  
  
                // Start an asynchronous socket to listen for connections.  
                Console.WriteLine("Waiting for a connection...");  
                listener.BeginAccept(   
                    new AsyncCallback(AcceptCallback),  
                    listener );  
  
                // Wait until a connection is made before continuing.  
                allDone.WaitOne();  
            }  
  
        } catch (Exception e) {  
            Console.WriteLine(e.ToString());  
        }  
  
        Console.WriteLine("\nPress ENTER to continue...");  
        Console.Read();  
  
    }  
  
    public static void AcceptCallback(IAsyncResult ar) {  
        // Signal the main thread to continue.  
        allDone.Set();  
  
        // Get the socket that handles the client request.  
        Socket listener = (Socket) ar.AsyncState;  
        Socket handler = listener.EndAccept(ar);  
  
        // Create the state object.  
        StateObject state = new StateObject();  
        state.workSocket = handler;  
        handler.BeginReceive( state.buffer, 0, StateObject.BufferSize, 0,  
            new AsyncCallback(ReadCallback), state);  
    }  
  
    public static void ReadCallback(IAsyncResult ar) {  
        String content = String.Empty;  
  
        // Retrieve the state object and the handler socket  
        // from the asynchronous state object.  
        StateObject state = (StateObject) ar.AsyncState;  
        Socket handler = state.workSocket;  
  
        // Read data from the client socket.   
        int bytesRead = handler.EndReceive(ar);  
  
        if (bytesRead > 0) {  
            // There  might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(  
                state.buffer, 0, bytesRead));  
  
            // Check for end-of-file tag. If it is not there, read   
            // more data.  
            content = state.sb.ToString();  
            if (content.IndexOf("<EOF>") > -1) {  
                // All the data has been read from the   
                // client. Display it on the console.  
                Console.WriteLine("Read {0} bytes from socket. \n Data : {1}",  
                    content.Length, content );  
                // Echo the data back to the client.  
                Send(handler, content);  
            } else {  
                // Not all data received. Get more.  
                handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0,  
                new AsyncCallback(ReadCallback), state);  
            }  
        }  
    }  
  
    private static void Send(Socket handler, String data) {  
        // Convert the string data to byte data using ASCII encoding.  
        byte[] byteData = Encoding.ASCII.GetBytes(data);  
  
        // Begin sending the data to the remote device.  
        handler.BeginSend(byteData, 0, byteData.Length, 0,  
            new AsyncCallback(SendCallback), handler);  
    }  
  
    private static void SendCallback(IAsyncResult ar) {  
        try {  
            // Retrieve the socket from the state object.  
            Socket handler = (Socket) ar.AsyncState;  
  
            // Complete sending the data to the remote device.  
            int bytesSent = handler.EndSend(ar);  
            Console.WriteLine("Sent {0} bytes to client.", bytesSent);  
  
            handler.Shutdown(SocketShutdown.Both);  
            handler.Close();  
  
        } catch (Exception e) {  
            Console.WriteLine(e.ToString());  
        }  
    }  
  
    public static int Main(String[] args) {  
        StartListening();  
        return 0;  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [비동기 클라이언트 소켓 예제](../../../docs/framework/network-programming/asynchronous-client-socket-example.md)  
 [비동기 서버 소켓 사용](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)  
 [소켓 코드 예제](../../../docs/framework/network-programming/socket-code-examples.md)
