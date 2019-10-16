---
title: TCP 서비스 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- requesting data from Internet, TCP
- receiving data, TCP
- TcpClient class, about TcpClient class
- data requests, TCP
- application protocols, TCP
- network resources, TCP
- sending data, TCP
- TCP
- protocols, TCP
- Internet, TCP
ms.assetid: d2811830-3bcb-495c-b82d-cda9cf919aad
ms.openlocfilehash: d9b3c9975c4d10649bdecd6f63cf362a2b2a2738
ms.sourcegitcommit: 438919211260bb415fc8f96ca3eabc33cf2d681d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2019
ms.locfileid: "59611954"
---
# <a name="using-tcp-services"></a>TCP 서비스 사용

<xref:System.Net.Sockets.TcpClient> 클래스는 TCP를 사용하여 인터넷 리소스의 데이터를 요청합니다. **TcpClient**의 메서드 및 속성은 TCP를 사용하여 데이터를 요청 및 수신하는 <xref:System.Net.Sockets.Socket>을 만들기 위한 세부 정보를 추상화합니다. 원격 디바이스에 대한 연결은 스트림으로 표현되므로 .NET Framework 스트림 처리 기법을 사용하여 데이터를 읽고 쓸 수 있습니다.  
  
 TCP 프로토콜은 원격 엔드포인트에 연결한 후 해당 연결을 사용하여 데이터 패킷을 주고받습니다. TCP는 데이터 패킷이 엔드포인트로 전송되고 도착 시 올바른 순서로 어셈블되도록 합니다.  
  
 TCP 연결을 설정하려면 필요한 서비스를 호스트하는 네트워크 디바이스의 주소를 알고 있어야 하고 서비스가 통신에 사용하는 TCP 포트를 알고 있어야 합니다. IANA(Internet Assigned Numbers Authority)는 공통 서비스의 포트 번호를 정의합니다([서비스 이름 및 전송 프로토콜 포트 번호 레지스트리](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml) 참조). Iana 목록에 없는 서비스에는 1,024~65,535 범위의 포트 번호를 사용할 수 있습니다.  
  
 다음 예제에서는 TCP 포트 13에서 시간 서버에 연결하도록 **TcpClient**를 설정하는 방법을 보여 줍니다.  
  
```vb  
Imports System  
Imports System.Net.Sockets  
Imports System.Text  
  
Public Class TcpTimeClient  
    Private const portNum As Integer = 13  
    Private const hostName As String = "host.contoso.com"  
  
    ' Entry point  that delegates to C-style main Private Function.  
    Public Overloads Shared Sub Main()  
        System.Environment.ExitCode = _  
            Main(System.Environment.GetCommandLineArgs())  
    End Sub  
  
    Overloads Public Shared Function Main(args() As [String]) As Integer  
        Try  
            Dim client As New TcpClient(hostName, portNum)  
  
            Dim ns As NetworkStream = client.GetStream()  
  
            Dim bytes(1024) As Byte  
            Dim bytesRead As Integer = ns.Read(bytes, 0, bytes.Length)  
  
            Console.WriteLine(Encoding.ASCII.GetString(bytes, 0, bytesRead))  
  
        Catch e As Exception  
            Console.WriteLine(e.ToString())  
        End Try  
  
        client.Close()  
  
        Return 0  
    End Function 'Main  
End Class 'TcpTimeClient  
```  
  
```csharp  
using System;  
using System.Net.Sockets;  
using System.Text;  
  
public class TcpTimeClient {  
    private const int portNum = 13;  
    private const string hostName = "host.contoso.com";  
  
    public static int Main(String[] args) {  
        try {  
            TcpClient client = new TcpClient(hostName, portNum);  
  
            NetworkStream ns = client.GetStream();  
  
            byte[] bytes = new byte[1024];  
            int bytesRead = ns.Read(bytes, 0, bytes.Length);  
  
            Console.WriteLine(Encoding.ASCII.GetString(bytes,0,bytesRead));  
  
            client.Close();  
  
        } catch (Exception e) {  
            Console.WriteLine(e.ToString());  
        }  
  
        return 0;  
    }  
}  
```  
  
 <xref:System.Net.Sockets.TcpListener>는 TCP 포트에서 들어오는 요청을 모니터링한 다음 클라이언트에 대한 연결을 관리하는 **Socket** 또는 **TcpClient**를 만드는 데 사용됩니다. <xref:System.Net.Sockets.TcpListener.Start%2A> 메서드는 수신 대기를 사용하도록 설정하고, <xref:System.Net.Sockets.TcpListener.Stop%2A> 메서드는 포트에서 수신 대기를 사용하지 않도록 설정합니다. <xref:System.Net.Sockets.TcpListener.AcceptTcpClient%2A> 메서드는 들어오는 연결 요청을 허용하고 **TcpClient**를 만들어 요청을 처리하며, <xref:System.Net.Sockets.TcpListener.AcceptSocket%2A> 메서드는 들어오는 연결 요청을 허용하고 **Socket**을 만들어 요청을 처리합니다.  
  
 다음 예제에서는 **TcpListener**를 사용해서 네트워크 시간 서버를 만들어 TCP 포트 13을 모니터링하는 방법을 보여 줍니다. 들어오는 연결 요청이 허용되면 시간 서버가 호스트 서버의 현재 날짜 및 시간을 사용하여 응답합니다.  
  
```vb  
Imports System  
Imports System.Net.Sockets  
Imports System.Text  
  
Public Class TcpTimeServer  
  
    Private const portNum As Integer = 13  
  
    ' Entry point that delegates to C-style main Private Function.  
    Public Overloads Shared Sub Main()  
        System.Environment.ExitCode = _  
            Main(System.Environment.GetCommandLineArgs())  
    End Sub  
  
    Overloads Public Shared Function Main(args() As [String]) As Integer  
        Dim done As Boolean = False  
  
        Dim listener As New TcpListener(portNum)  
  
        listener.Start()  
  
        While Not done  
            Console.Write("Waiting for connection...")  
            Dim client As TcpClient = listener.AcceptTcpClient()  
  
            Console.WriteLine("Connection accepted.")  
            Dim ns As NetworkStream = client.GetStream()  
  
            Dim byteTime As Byte() = _  
                Encoding.ASCII.GetBytes(DateTime.Now.ToString())  
  
            Try  
                ns.Write(byteTime, 0, byteTime.Length)  
                ns.Close()  
                client.Close()  
            Catch e As Exception  
                Console.WriteLine(e.ToString())  
            End Try  
        End While  
  
        listener.Stop()  
  
        Return 0  
    End Function 'Main  
End Class 'TcpTimeServer  
```  
  
```csharp  
using System;  
using System.Net.Sockets;  
using System.Text;  
  
public class TcpTimeServer {  
  
    private const int portNum = 13;  
  
    public static int Main(String[] args) {  
        bool done = false;  
  
        TcpListener listener = new TcpListener(portNum);  
  
        listener.Start();  
  
        while (!done) {  
            Console.Write("Waiting for connection...");  
            TcpClient client = listener.AcceptTcpClient();  
  
            Console.WriteLine("Connection accepted.");  
            NetworkStream ns = client.GetStream();  
  
            byte[] byteTime = Encoding.ASCII.GetBytes(DateTime.Now.ToString());  
  
            try {  
                ns.Write(byteTime, 0, byteTime.Length);  
                ns.Close();  
                client.Close();  
            } catch (Exception e) {  
                Console.WriteLine(e.ToString());  
            }  
        }  
  
        listener.Stop();  
  
        return 0;  
    }  
  
}  
```
