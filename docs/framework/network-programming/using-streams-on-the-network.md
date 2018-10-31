---
title: 네트워크에서 스트림 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- requesting data from Internet, streams
- Networking
- response to Internet request, streams
- network resources, stream capabilities
- receiving data, stream capabilities
- Network Resources
- sending data, stream capabilities
- downloading Internet resources, streams
- streams, capabilities
- Internet, streams
- streams
ms.assetid: 02b05fba-7235-45ce-94e5-060436ee0875
ms.openlocfilehash: a51d87aeef8d39356af10d526db63b7b16b9ca58
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50189578"
---
# <a name="using-streams-on-the-network"></a>네트워크에서 스트림 사용
네트워크 리소스는 .NET Framework에서 스트림으로 표현됩니다. 스트림을 일반적으로 처리하여 .NET Framework는 다음과 같은 기능을 제공합니다.  
  
-   웹 데이터를 송수신하는 일반적인 방법. 파일의 실제 내용에 관계없이(HTML, XML 또는 기타 모든 항목) 응용 프로그램은 <xref:System.IO.Stream.Write%2A?displayProperty=nameWithType> 및 <xref:System.IO.Stream.Read%2A?displayProperty=nameWithType>를 사용하여 데이터를 주고받습니다.  
  
-   .NET Framework 전체에서 스트림과 호환성. 스트림은 처리를 위한 풍부한 인프라가 있는 .NET Framework 전체에서 사용됩니다. 예를 들어 스트림을 초기화하는 코드 몇 줄만 변경하여 <xref:System.IO.FileStream>에서 XML 데이터를 읽는 응용 프로그램을 <xref:System.Net.Sockets.NetworkStream>에서 데이터를 읽도록 수정할 수 있습니다. **NetworkStream** 클래스와 다른 스트림 간의 주요 차이점은 **NetworkStream**은 검색할 수 없고, <xref:System.Net.Sockets.NetworkStream.CanSeek%2A> 속성은 항상 **false**를 반환하고, <xref:System.Net.Sockets.NetworkStream.Seek%2A> 및 <xref:System.Net.Sockets.NetworkStream.Position%2A> 메서드는 <xref:System.NotSupportedException>을 throw한다는 것입니다.  
  
-   데이터 도착 시 처리. 스트림은 전체 데이터 집합이 다운로드될 때까지 응용 프로그램을 강제로 대기시키는 대신 네트워크에서 도착하는 대로 데이터에 대한 액세스를 제공합니다.  
  
 <xref:System.Net.Sockets> 네임스페이스에는 네트워크 리소스에 사용할 수 있도록 특별히 고안된 <xref:System.IO.Stream> 클래스를 구현하는 **NetworkStream** 클래스가 포함되어 있습니다. <xref:System.Net.Sockets> 네임스페이스에 있는 클래스는 **NetworkStream** 클래스를 사용하여 스트림을 나타냅니다.  
  
 반환된 스트림을 사용하여 데이터를 네트워크에 보내려면 <xref:System.Net.WebRequest>에서 <xref:System.Net.WebRequest.GetRequestStream%2A>을 호출합니다. **WebRequest**는 요청 헤더를 서버에 보냅니다. 그러면 반환된 스트림에서 <xref:System.IO.Stream.BeginWrite%2A>, <xref:System.IO.Stream.EndWrite%2A> 또는 <xref:System.IO.Stream.Write%2A> 메서드를 호출하여 데이터를 네트워크 리소스에 보낼 수 있습니다. HTTP와 같은 일부 프로토콜의 경우 데이터를 보내기 전에 프로토콜 관련 속성을 설정해야 할 수도 있습니다. 다음 코드 예제에서는 데이터 전송을 위한 HTTP 관련 속성을 설정하는 방법을 보여 줍니다. `sendData` 변수에 보낼 데이터가 들어 있고 `sendLength` 변수는 보낼 데이터의 바이트 수라고 가정합니다.  
  
```csharp  
HttpWebRequest request =   
   (HttpWebRequest) WebRequest.Create("http://www.contoso.com/");  
request.Method = "POST";  
request.ContentLength = sendLength;  
try  
{  
   Stream sendStream = request.GetRequestStream();  
   sendStream.Write(sendData,0,sendLength);  
   sendStream.Close();  
}  
catch  
{  
   // Handle errors . . .  
}  
```  
  
```vb  
Dim request As HttpWebRequest = _  
   CType(WebRequest.Create("http://www.contoso.com/"), HttpWebRequest)  
request.Method = "POST"  
request.ContentLength = sendLength  
Try  
   Dim sendStream As Stream = request.GetRequestStream()  
   sendStream.Write(sendData, 0, sendLength)  
   sendStream.Close()  
Catch  
   ' Handle errors . . .  
End Try  
```  
  
 네트워크에서 데이터를 수신하려면 <xref:System.Net.WebResponse>에서 <xref:System.Net.WebResponse.GetResponseStream%2A>을 호출합니다. 반환된 스트림에서 <xref:System.IO.Stream.BeginRead%2A>, <xref:System.IO.Stream.EndRead%2A> 또는 <xref:System.IO.Stream.Read%2A> 메서드를 호출하여 네트워크 리소스에서 데이터를 읽을 수 있습니다.  
  
 네트워크 리소스의 스트림을 사용하는 경우 다음 사항에 유의하세요.  
  
-   **NetworkStream** 클래스가 스트림 내의 위치를 변경할 수 없기 때문에 **CanSeek** 속성은 항상 **false**를 반환합니다. **Seek** 및 **Position** 메서드는 **NotSupportedException**을 throw합니다.  
  
-   **WebRequest** 및 **WebResponse**를 사용하는 경우 **GetResponseStream**을 호출하여 만든 스트림 인스턴스는 읽기 전용이고 **GetRequestStream**을 호출하여 만든 스트림 인스턴스는 쓰기 전용입니다.  
  
-   <xref:System.IO.StreamReader> 클래스를 사용하여 인코딩을 용이하게 합니다. 다음 코드 예제에서는 **StreamReader**를 사용하여 **WebResponse**에서 ASCII로 인코드된 스트림을 읽습니다(예제에는 요청을 만드는 방법이 포함되지 않음).  
  
-   네트워크 리소스를 사용할 수 없는 경우 **GetResponse** 호출이 차단할 수 있습니다. <xref:System.Net.WebRequest.BeginGetResponse%2A> 및 <xref:System.Net.WebRequest.EndGetResponse%2A> 메서드와 함께 비동기 요청을 사용하는 것이 좋습니다.  
  
-   서버에 연결하는 동안 **GetRequestStream** 호출이 차단할 수 있습니다. <xref:System.Net.WebRequest.BeginGetRequestStream%2A> 및 <xref:System.Net.WebRequest.EndGetRequestStream%2A> 메서드와 함께 스트림에 대한 비동기 요청을 사용하는 것이 좋습니다.  
  
```csharp  
// Create a response object.  
WebResponse response = request.GetResponse();  
// Get a readable stream from the server.  
StreamReader sr =   
   new StreamReader(response.GetResponseStream(), Encoding.ASCII);  
// Use the stream. Remember when you are through with the stream to close it.  
sr.Close();  
```  
  
```vb  
' Create a response object.  
Dim response As WebResponse = request.GetResponse()  
' Get a readable stream from the server.  
Dim sr As _   
   New StreamReader(response.GetResponseStream(), Encoding.ASCII)  
' Use the stream. Remember when you are through with the stream to close it.  
sr.Close()  
```  
  
## <a name="see-also"></a>참고 항목  
 [방법: WebRequest 클래스를 사용하여 데이터 요청](../../../docs/framework/network-programming/how-to-request-data-using-the-webrequest-class.md)  
 [데이터 요청](../../../docs/framework/network-programming/requesting-data.md)
