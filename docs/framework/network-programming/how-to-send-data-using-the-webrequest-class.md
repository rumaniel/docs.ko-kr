---
title: '방법: WebRequest 클래스를 사용하여 데이터 보내기'
ms.date: 03/25/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WebRequest class, sending data to a host
- Sending data to a host, using WebRequest class
ms.assetid: 66686878-38ac-4aa6-bf42-ffb568ffc459
ms.openlocfilehash: 2467b289df7a0361b51ad91d4458d32742c42275
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040823"
---
# <a name="how-to-send-data-by-using-the-webrequest-class"></a>방법: WebRequest 클래스를 사용하여 데이터 보내기

다음 프로시저에서는 서버에 데이터를 보내는 단계를 설명합니다. 이 프로시저는 일반적으로 웹 페이지에 데이터를 게시하는 데 사용됩니다.

## <a name="to-send-data-to-a-host-server"></a>호스트에 데이터를 보내려면

1. 스크립트 또는 ASP.NET 페이지와 같이 데이터를 허용하는 리소스의 URI에서 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType>을 호출하여 <xref:System.Net.WebRequest> 인스턴스를 만듭니다. 예:

    ```csharp
    WebRequest request = WebRequest.Create("http://www.contoso.com/PostAccepter.aspx");
    ```

    ```vb
    Dim request as WebRequest = WebRequest.Create("http://www.contoso.com/PostAccepter.aspx")
    ```

    > [!NOTE]
    > .NET Framework에서는 *http:* , *https:* , *ftp:* 및 *file:* 로 시작하는 URI에 대해 <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse> 클래스에서 파생된 프로토콜 지정 클래스를 제공합니다.

    그러나 프로토콜 지정 속성을 설정하거나 읽어야 하는 경우 <xref:System.Net.WebRequest> 또는 <xref:System.Net.WebResponse> 개체를 프로토콜 특정 개체 형식으로 캐스팅해야 합니다. 자세한 내용은 [플러그형 프로토콜 프로그래밍](programming-pluggable-protocols.md)을 참조하세요.

2. `WebRequest` 개체에서 필요한 속성 값을 설정합니다. 예를 들어 인증을 사용하도록 설정하려면 <xref:System.Net.WebRequest.Credentials%2A?displayProperty=nameWithType> 속성을 <xref:System.Net.NetworkCredential> 클래스의 인스턴스로 설정합니다.

    ```csharp
    request.Credentials = CredentialCache.DefaultCredentials;
    ```

    ```vb
    request.Credentials = CredentialCache.DefaultCredentials
    ```

3. 요청을 통해 데이터를 보내도록 허용하는 프로토콜 메서드를 지정합니다(예: HTTP `POST` 메서드).

    ```csharp
    request.Method = "POST";
    ```

    ```vb
    request.Method = "POST"
    ```

4. <xref:System.Web.HttpRequest.ContentLength> 속성을 요청에 포함된 바이트 수로 설정합니다. 예:

    ```csharp
    request.ContentLength = byteArray.Length;
    ```

    ```vb
    request.ContentLength = byteArray.Length
    ```

5. <xref:System.Web.HttpRequest.ContentType> 속성을 적절한 값으로 설정합니다. 예:

    ```csharp
    request.ContentType = "application/x-www-form-urlencoded";
    ```

    ```vb
    request.ContentType = "application/x-www-form-urlencoded"
    ```

6. <xref:System.Net.WebRequest.GetRequestStream%2A> 메서드를 호출하여 요청 데이터를 포함하는 스트림을 가져옵니다. 예:

    ```csharp
    Stream dataStream = request.GetRequestStream();
    ```

    ```vb
    Dim dataStream As Stream = request.GetRequestStream()
    ```

7. `GetRequestStream` 메서드에서 반환된 <xref:System.IO.Stream> 개체에 데이터를 기록합니다. 예:

    ```csharp
    dataStream.Write(byteArray, 0, byteArray.Length);
    ```

    ```vb
    dataStream.Write(byteArray, 0, byteArray.Length)
    ```

8. <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 메서드를 호출하여 요청 스트림을 닫습니다. 예:

    ```csharp
    dataStream.Close();
    ```

    ```vb
    dataStream.Close()
    ```

9. <xref:System.Net.WebRequest.GetResponse%2A?displayProperty=nameWithType>를 호출하여 요청을 서버에 보냅니다. 이 메서드는 서버 응답을 포함하는 개체를 반환합니다. 반환된 `WebResponse` 개체의 형식은 요청 URI 구성표에 따라 결정됩니다. 예:

    ```csharp
    WebResponse response = request.GetResponse();
    ```

    ```vb
    Dim response As WebResponse = request.GetResponse()
    ```

10. `WebResponse` 개체의 속성에 액세스하거나 프로토콜 지정 인스턴스로 캐스팅하여 프로토콜 지정 속성을 읽을 수 있습니다.

    예를 들어 <xref:System.Net.HttpWebResponse>의 HTTP 지정 속성에 액세스하려면 `WebResponse` 개체를 <xref:System.Net.HttpWebResponse> 참조로 캐스팅해야 합니다. 다음 코드 예제에서는 응답과 함께 전송된 HTTP 지정 <xref:System.Net.HttpWebResponse.StatusDescription%2A?displayProperty=nameWithType> 속성을 표시하는 방법을 보여줍니다.

    ```csharp
    Console.WriteLine(((HttpWebResponse)response).StatusDescription);
    ```

    ```vb
    Console.WriteLine(CType(response, HttpWebResponse).StatusDescription)
    ```

11. 서버에서 전송된 응답 데이터를 포함하는 스트림을 가져오려면 `WebResponse` 개체의 <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=nameWithType> 메서드를 호출합니다. 예:

    ```csharp
    Stream dataStream = response.GetResponseStream();
    ```

    ```vb
    Dim dataStream As Stream = response.GetResponseStream()
    ```

12. 응답 개체에서 데이터를 읽은 후에 <xref:System.Net.WebResponse.Close%2A?displayProperty=nameWithType> 메서드를 사용하여 해당 개체를 닫거나 <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 메서드를 사용하여 응답 스트림을 닫습니다. 응답이나 스트림을 닫지 않으면 애플리케이션이 서버 연결을 모두 사용하여 추가 요청을 처리하지 못하게 될 수 있습니다. `WebResponse.Close` 메서드가 응답을 닫으면 `Stream.Close`를 호출하기 때문에 모든 응답 및 스트림 개체에서 `Close`를 호출할 필요가 없지만 유해하지도 않습니다. 예:

    ```csharp
    response.Close();
    ```

    ```vb
    response.Close()
    ```

## <a name="example"></a>예

다음 예제에서는 웹 서버에 데이터를 보내고 응답에서 데이터를 읽는 방법을 보여줍니다.

[!code-csharp[SendDataUsingWebRequest](../../../samples/snippets/csharp/VS_Snippets_Network/SendDataUsingWebRequest/cs/WebRequestPostExample.cs)]
[!code-vb[SendDataUsingWebRequest](../../../samples/snippets/visualbasic/VS_Snippets_Network/SendDataUsingWebRequest/vb/WebRequestPostExample.vb)]

## <a name="see-also"></a>참고 항목

- [인터넷 요청 만들기](creating-internet-requests.md)
- [네트워크에서 스트림 사용](using-streams-on-the-network.md)
- [프록시를 통해 인터넷에 액세스](accessing-the-internet-through-a-proxy.md)
- [데이터 요청](requesting-data.md)
- [방법: WebRequest 클래스를 사용하여 데이터 요청](how-to-request-data-using-the-webrequest-class.md)
