---
title: 오류 처리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, WebRequest and WebResponse classes exceptions
- Status property
- WebExceptions class, about WebExceptions class
- Timeout enumeration member
- ConnectFailure enumeration member
- TrustFailure enumeration member
- WebRequest class, exceptions
- requesting data from Internet, error handling
- Success enumeration member
- receiving data, errors
- ProtocolError enumeration member
- downloading Internet resources, error handling
- WebResponse class, exceptions
- SendFailure enumeration member
- errors [.NET Framework], WebRequest and WebResponse classes exceptions
- sending data, errors
- response to Internet request, error handling
- NameResolutionFailure enumeration member
- KeepAliveFailure enumeration member
- network resources, WebRequest and WebResponse classes exceptions
- RequestCanceled enumeration member
- ReceiveFailure enumeration member
- ServerProtocolViolation enumeration member
- ConnectionClosed enumeration member
- SecureChannelFailure enumeration member
ms.assetid: 657141cd-5cf5-4fdb-a4b2-4c040eba84b5
ms.openlocfilehash: d199219b36e2cc06314b38303fb2296f9f3794ea
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198343"
---
# <a name="handling-errors"></a>오류 처리
<xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse> 클래스는 시스템 예외(예: <xref:System.ArgumentException>) 및 웹 관련 예외(<xref:System.Net.WebRequest.GetResponse%2A> 메서드에서 throw된 <xref:System.Net.WebException>)를 둘 다 throw합니다.  
  
 각 **WebException**에는 <xref:System.Net.WebExceptionStatus> 열거형의 값을 포함하는 <xref:System.Net.WebException.Status%2A> 속성이 포함됩니다. **Status** 속성을 검사하여 발생한 오류를 확인하고 적절한 단계를 수행하여 오류를 해결할 수 있습니다.  
  
 다음 표에서는 **Status** 속성의 가능한 값을 설명합니다.  
  
|상태|설명|  
|------------|-----------------|  
|ConnectFailure|원격 서비스가 전송 수준에서 연결될 수 없습니다.|  
|ConnectionClosed|연결이 조기에 닫혔습니다.|  
|KeepAliveFailure|서버가 연결 유지 헤더 집합을 통해 설정된 연결을 닫았습니다.|  
|NameResolutionFailure|이름 서비스가 호스트 이름을 확인할 수 없습니다.|  
|ProtocolError|서버에서 받은 응답이 완료되었으나 프로토콜 수준에서 오류를 나타냈습니다.|  
|ReceiveFailure|전체 응답이 원격 서버에서 수신되지 않았습니다.|  
|RequestCanceled|요청이 취소되었습니다.|  
|SecureChannelFailure|보안 채널 링크에서 오류가 발생했습니다.|  
|SendFailure|전체 요청을 원격 서버로 보낼 수 없습니다.|  
|ServerProtocolViolation|서버 응답이 유효한 HTTP 응답이 아니었습니다.|  
|성공|오류가 발생하지 않았습니다.|  
|시간 제한|요청에 대해 설정된 시간 제한 내에 응답이 수신되지 않았습니다.|  
|TrustFailure|서버 인증서를 유효성 검사할 수 없습니다.|  
|MessageLengthLimitExceeded|요청을 보내거나 서버에서 응답을 받을 때 지정된 제한을 초과한 메시지를 받았습니다.|  
|보류 중|내부 비동기 요청이 보류 중입니다.|  
|PipelineFailure|이 값은 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|  
|ProxyNameResolutionFailure|이름 확인자 서비스가 프록시 호스트 이름을 확인할 수 없습니다.|  
|UnknownError|알 수 없는 형식의 예외가 발생했습니다.|  
  
 **Status** 속성이 **WebExceptionStatus.ProtocolError**이면 서버의 응답이 포함된 **WebResponse**를 사용할 수 있습니다. 이 응답을 검사하여 프로토콜 오류의 실제 소스를 확인합니다.  
  
 다음 예제에서는 **WebException**을 catch하는 방법을 보여 줍니다.  
  
```csharp  
try   
{  
    // Create a request instance.  
    WebRequest myRequest =   
    WebRequest.Create("http://www.contoso.com");  
    // Get the response.  
    WebResponse myResponse = myRequest.GetResponse();  
    //Get a readable stream from the server.   
    Stream sr = myResponse.GetResponseStream();  
  
    //Read from the stream and write any data to the console.  
    bytesread = sr.Read( myBuffer, 0, length);  
    while( bytesread > 0 )   
    {  
        for (int i=0; i<bytesread; i++) {  
            Console.Write( "{0}", myBuffer[i]);  
        }  
        Console.WriteLine();  
        bytesread = sr.Read( myBuffer, 0, length);  
    }  
    sr.Close();  
    myResponse.Close();  
}  
catch (WebException webExcp)   
{  
    // If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.");  
    // Write out the WebException message.  
    Console.WriteLine(webExcp.ToString());  
    // Get the WebException status code.  
    WebExceptionStatus status =  webExcp.Status;  
    // If status is WebExceptionStatus.ProtocolError,   
    //   there has been a protocol error and a WebResponse   
    //   should exist. Display the protocol error.  
    if (status == WebExceptionStatus.ProtocolError) {  
        Console.Write("The server returned protocol error ");  
        // Get HttpWebResponse so that you can check the HTTP status code.  
        HttpWebResponse httpResponse = (HttpWebResponse)webExcp.Response;  
        Console.WriteLine((int)httpResponse.StatusCode + " - "  
           + httpResponse.StatusCode);  
    }  
}  
catch (Exception e)   
{  
    // Code to catch other exceptions goes here.  
}  
```  
  
```vb  
Try  
    ' Create a request instance.  
    Dim myRequest As WebRequest = WebRequest.Create("http://www.contoso.com")  
    ' Get the response.  
    Dim myResponse As WebResponse = myRequest.GetResponse()  
    'Get a readable stream from the server.   
    Dim sr As Stream = myResponse.GetResponseStream()  
  
    Dim i As Integer      
    'Read from the stream and write any data to the console.  
    bytesread = sr.Read(myBuffer, 0, length)  
    While bytesread > 0  
        For i = 0 To bytesread - 1  
            Console.Write("{0}", myBuffer(i))  
        Next i  
        Console.WriteLine()  
        bytesread = sr.Read(myBuffer, 0, length)  
    End While  
    sr.Close()  
    myResponse.Close()  
Catch webExcp As WebException  
    ' If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.")  
    ' Write out the WebException message.  
    Console.WriteLine(webExcp.ToString())  
    ' Get the WebException status code.  
    Dim status As WebExceptionStatus = webExcp.Status  
    ' If status is WebExceptionStatus.ProtocolError,   
    '   there has been a protocol error and a WebResponse   
    '   should exist. Display the protocol error.  
    If status = WebExceptionStatus.ProtocolError Then  
        Console.Write("The server returned protocol error ")  
        ' Get HttpWebResponse so that you can check the HTTP status code.  
        Dim httpResponse As HttpWebResponse = _  
           CType(webExcp.Response, HttpWebResponse)  
        Console.WriteLine(CInt(httpResponse.StatusCode).ToString() & _  
           " - " & httpResponse.StatusCode.ToString())  
    End If  
Catch e As Exception  
    ' Code to catch other exceptions goes here.  
End Try  
```  
  
 <xref:System.Net.Sockets.Socket> 클래스를 사용하는 응용 프로그램은 Windows 소켓에서 오류가 발생할 경우 <xref:System.Net.Sockets.SocketException>을 throw합니다. <xref:System.Net.Sockets.TcpClient>, <xref:System.Net.Sockets.TcpListener> 및 <xref:System.Net.Sockets.UdpClient> 클래스는 **Socket** 클래스의 맨 위에 빌드되고 **SocketExceptions**도 throw합니다.  
  
 **SocketException**이 throw되면 **SocketException** 클래스는 마지막으로 발생한 운영 체제 소켓 오류로 <xref:System.Net.Sockets.SocketException.ErrorCode%2A> 속성을 설정합니다. 소켓 오류 코드에 대한 자세한 내용은 MSDN에서 Winsock 2.0 API 오류 코드 문서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [예외 처리 기본 사항](../../../docs/standard/exceptions/exception-handling-fundamentals.md)  
 [데이터 요청](../../../docs/framework/network-programming/requesting-data.md)
