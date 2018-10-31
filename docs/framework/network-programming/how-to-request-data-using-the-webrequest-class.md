---
title: '방법: WebRequest 클래스를 사용하여 데이터 요청'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- downloading Internet resources, steps
- requesting data from Internet, steps
- WebRequest class, receiving data
- receiving data, using WebRequest class
- Internet, requesting data
ms.assetid: 368b8d0f-dc5e-4469-a8b8-b2adbf5dd800
ms.openlocfilehash: 8a740d2eecd4d866fd3042985f1f6f3194a12ec5
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50192761"
---
# <a name="how-to-request-data-using-the-webrequest-class"></a>방법: WebRequest 클래스를 사용하여 데이터 요청
다음 프로시저에서는 서버의 웹 페이지 또는 파일과 같은 리소스를 요청하는 데 사용되는 단계를 설명합니다. 리소스는 URI로 식별되어야 합니다.  
  
### <a name="to-request-data-from-a-host-server"></a>호스트 서버의 데이터를 요청하려면  
  
1.  리소스 URI를 통해 <xref:System.Net.WebRequest.Create%2A>를 호출하여 <xref:System.Net.WebRequest> 인스턴스를 만듭니다.  
  
    ```csharp  
    WebRequest request = WebRequest.Create("http://www.contoso.com/");  
    ```  
  
    ```vb  
    Dim request as WebRequest = WebRequest.Create("http://www.contoso.com/")  
    ```  
  
    > [!NOTE]
    >  .NET Framework에서는 “http:”, “https:”, “ftp:” 및 “file:”으로 시작하는 URI에 대해 **WebRequest** 및 **WebResponse**에서 파생된 프로토콜별 클래스를 제공합니다. 다른 프로토콜을 사용하는 리소스에 액세스하려면 **WebRequest** 및 **WebResponse**에서 파생되는 프로토콜별 클래스를 구현해야 합니다. 자세한 내용은 [플러그형 프로토콜 프로그래밍](../../../docs/framework/network-programming/programming-pluggable-protocols.md)을 참조하세요.  
  
2.  **WebRequest**에서 필요한 속성 값을 설정합니다. 예를 들어 인증을 사용하도록 설정하려면 **Credentials** 속성을 <xref:System.Net.NetworkCredential> 클래스의 인스턴스로 설정합니다.  
  
    ```csharp  
    request.Credentials = CredentialCache.DefaultCredentials;  
    ```  
  
    ```vb  
    request.Credentials = CredentialCache.DefaultCredentials  
    ```  
  
     대부분의 경우 데이터를 수신하는 데는 **WebRequest**로 충분합니다. 그러나 프로토콜별 속성을 설정해야 할 경우 **WebRequest**를 프로토콜별 형식으로 캐스팅해야 합니다. 예를 들어 <xref:System.Net.HttpWebRequest>의 HTTP 관련 속성에 액세스하려면 **WebRequest**를 **HttpWebRequest** 참조로 캐스팅해야 합니다. 다음 코드 예제에서는 HTTP 관련 <xref:System.Net.HttpWebRequest.UserAgent%2A> 속성을 설정하는 방법을 보여 줍니다.  
  
    ```csharp  
    ((HttpWebRequest)request).UserAgent = ".NET Framework Example Client";  
    ```  
  
    ```vb  
    Ctype(request,HttpWebRequest).UserAgent = ".NET Framework Example Client"  
    ```  
  
3.  요청을 서버에 보내려면 <xref:System.Net.HttpWebRequest.GetResponse%2A>를 호출합니다. 반환된 **WebResponse** 개체의 실제 형식은 요청된 URI 구성표에 따라 결정됩니다.  
  
    ```csharp  
    WebResponse response = request.GetResponse();  
    ```  
  
    ```vb  
    Dim response As WebResponse = request.GetResponse()  
    ```  
  
    > [!NOTE]
    >  <xref:System.Net.WebResponse> 개체가 필요 없게 되면 <xref:System.Net.WebResponse.Close%2A> 메서드를 호출하여 개체를 닫아야 합니다. 또는 응답 개체에서 응답 스트림을 이미 가져온 경우 <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 메서드를 호출하여 스트림을 닫을 수 있습니다. 응답이나 스트림을 닫지 않으면 응용 프로그램이 서버에 대한 연결을 모두 사용하여 추가 요청을 처리하지 못하게 될 수 있습니다.  
  
4.  **WebResponse**의 속성에 액세스하거나 **WebResponse**를 프로토콜별 인스턴스로 캐스팅하여 프로토콜별 속성을 읽을 수 있습니다. 예를 들어 <xref:System.Net.HttpWebResponse>의 HTTP 관련 속성에 액세스하려면 **WebResponse**를 **HttpWebResponse** 참조로 캐스팅해야 합니다. 다음 코드 예제에서는 응답과 함께 전송된 상태 정보를 표시하는 방법을 보여 줍니다.  
  
    ```csharp  
    Console.WriteLine (((HttpWebResponse)response).StatusDescription);  
    ```  
  
    ```vb  
    Console.WriteLine(CType(response,HttpWebResponse).StatusDescription)  
    ```  
  
5.  서버에서 전송된 응답 데이터를 포함하는 스트림을 가져오려면 **WebResponse**의 <xref:System.Net.HttpWebResponse.GetResponseStream%2A> 메서드를 사용합니다.  
  
    ```csharp  
    Stream dataStream = response.GetResponseStream();  
    ```  
  
    ```vb  
    Dim dataStream As Stream = response.GetResponseStream()  
    ```  
  
6.  응답에서 데이터를 읽은 후 **Stream.Close** 메서드를 사용하여 응답 스트림을 닫거나 **WebResponse.Close** 메서드를 사용하여 응답을 닫아야 합니다. 응답 스트림 및 **WebResponse**에서 둘 다 **Close** 메서드를 호출할 필요가 없지만 호출해도 문제가 되지 않습니다. **WebResponse.Close**는 응답을 닫을 때 **Stream.Close**를 호출합니다.  
  
    ```csharp  
    response.Close();  
    ```  
  
    ```vb  
    response.Close()  
    ```  
  
## <a name="example"></a>예  
  
```csharp  
using System;  
using System.IO;  
using System.Net;  
using System.Text;  
  
namespace Examples.System.Net  
{  
    public class WebRequestGetExample  
    {  
        public static void Main()  
        {  
            // Create a request for the URL.   
            WebRequest request = WebRequest.Create(  
              "http://www.contoso.com/default.html");  
            // If required by the server, set the credentials.  
            request.Credentials = CredentialCache.DefaultCredentials;  
            // Get the response.  
            WebResponse response = request.GetResponse();  
            // Display the status.  
            Console.WriteLine (((HttpWebResponse)response).StatusDescription);  
            // Get the stream containing content returned by the server.  
            Stream dataStream = response.GetResponseStream();  
            // Open the stream using a StreamReader for easy access.  
            StreamReader reader = new StreamReader(dataStream);  
            // Read the content.  
            string responseFromServer = reader.ReadToEnd();  
            // Display the content.  
            Console.WriteLine(responseFromServer);  
            // Clean up the streams and the response.  
            reader.Close();  
            response.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Net  
Imports System.Text  
Namespace Examples.System.Net  
    Public Class WebRequestGetExample  
  
        Public Shared Sub Main()  
            ' Create a request for the URL.   
            Dim request As WebRequest = _  
              WebRequest.Create("http://www.contoso.com/default.html")  
            ' If required by the server, set the credentials.  
            request.Credentials = CredentialCache.DefaultCredentials  
            ' Get the response.  
            Dim response As WebResponse = request.GetResponse()  
            ' Display the status.  
            Console.WriteLine(CType(response,HttpWebResponse).StatusDescription)  
            ' Get the stream containing content returned by the server.  
            Dim dataStream As Stream = response.GetResponseStream()  
            ' Open the stream using a StreamReader for easy access.  
            Dim reader As New StreamReader(dataStream)  
            ' Read the content.  
            Dim responseFromServer As String = reader.ReadToEnd()  
            ' Display the content.  
            Console.WriteLine(responseFromServer)  
            ' Clean up the streams and the response.  
            reader.Close()  
            response.Close()  
        End Sub   
    End Class   
End Namespace  
```  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 요청 만들기](../../../docs/framework/network-programming/creating-internet-requests.md)  
 [네트워크에서 스트림 사용](../../../docs/framework/network-programming/using-streams-on-the-network.md)  
 [프록시를 통해 인터넷 액세스](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)  
 [데이터 요청](../../../docs/framework/network-programming/requesting-data.md)  
 [방법: WebRequest 클래스를 사용하여 데이터 보내기](../../../docs/framework/network-programming/how-to-send-data-using-the-webrequest-class.md)
