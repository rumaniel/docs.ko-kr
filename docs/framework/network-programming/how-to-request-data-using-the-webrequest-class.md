---
title: '방법: WebRequest 클래스를 사용하여 데이터 요청'
ms.date: 03/21/2019
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
ms.openlocfilehash: e670a2a503ce704eff847e9e0b3ee340ab52fe62
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71048161"
---
# <a name="how-to-request-data-by-using-the-webrequest-class"></a>방법: WebRequest 클래스를 사용하여 데이터 요청

다음 프로시저에서는 서버에서 웹 페이지 또는 파일과 같은 리소스를 요청하는 단계를 설명합니다. 리소스는 URI로 식별되어야 합니다.

## <a name="to-request-data-from-a-host-server"></a>호스트 서버의 데이터를 요청하려면

1. 리소스 URI를 통해 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType>를 호출하여 <xref:System.Net.WebRequest> 인스턴스를 만듭니다. 예:

    ```csharp
    WebRequest request = WebRequest.Create("https://docs.microsoft.com");
    ```

    ```vb
    Dim request as WebRequest = WebRequest.Create("https://docs.microsoft.com")
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

3. <xref:System.Net.WebRequest.GetResponse%2A?displayProperty=nameWithType>를 호출하여 요청을 서버에 보냅니다. 이 메서드는 서버 응답을 포함하는 개체를 반환합니다. 반환된 <xref:System.Net.WebResponse> 개체의 형식은 요청 URI 구성표에 따라 결정됩니다. 예:

    ```csharp
    WebResponse response = request.GetResponse();
    ```

    ```vb
    Dim response As WebResponse = request.GetResponse()
    ```

4. `WebResponse` 개체의 속성에 액세스하거나 프로토콜 지정 인스턴스로 캐스팅하여 프로토콜 지정 속성을 읽을 수 있습니다.

    예를 들어 <xref:System.Net.HttpWebResponse>의 HTTP 지정 속성에 액세스하려면 `WebResponse` 개체를 `HttpWebResponse` 참조로 캐스팅해야 합니다. 다음 코드 예제에서는 응답과 함께 전송된 HTTP 지정 <xref:System.Net.HttpWebResponse.StatusDescription%2A?displayProperty=nameWithType> 속성을 표시하는 방법을 보여줍니다.

    ```csharp
    Console.WriteLine (((HttpWebResponse)response).StatusDescription);
    ```

    ```vb
    Console.WriteLine(CType(response,HttpWebResponse).StatusDescription)
    ```

5. 서버에서 전송된 응답 데이터를 포함하는 스트림을 가져오려면 <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=nameWithType> 메서드를 호출합니다. 예:

    ```csharp
    Stream dataStream = response.GetResponseStream();
    ```

    ```vb
    Dim dataStream As Stream = response.GetResponseStream()
    ```

6. 응답 개체에서 데이터를 읽은 후에 <xref:System.Net.WebResponse.Close%2A?displayProperty=nameWithType> 메서드를 사용하여 해당 개체를 닫거나 <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 메서드를 사용하여 응답 스트림을 닫습니다. 응답 개체나 스트림을 닫지 않으면 애플리케이션이 서버 연결을 모두 사용하여 추가 요청을 처리하지 못하게 될 수 있습니다. `WebResponse.Close` 메서드가 응답을 닫으면 `Stream.Close`를 호출하기 때문에 모든 응답 및 스트림 개체에서 `Close`를 호출할 필요가 없지만 유해하지도 않습니다. 예:

    ```csharp
    response.Close();
    ```

    ```vb
    response.Close()
    ```

## <a name="example"></a>예

다음 코드 예제에서는 웹 서버에 데이터를 만들고 응답에서 데이터를 읽는 방법을 보여줍니다.

[!code-csharp[RequestDataUsingWebRequest](../../../samples/snippets/csharp/VS_Snippets_Network/RequestDataUsingWebRequest/cs/WebRequestGetExample.cs)]
[!code-vb[RequestDataUsingWebRequest](../../../samples/snippets/visualbasic/VS_Snippets_Network/RequestDataUsingWebRequest/vb/WebRequestGetExample.vb)]

## <a name="see-also"></a>참고 항목

- [인터넷 요청 만들기](creating-internet-requests.md)
- [네트워크에서 스트림 사용](using-streams-on-the-network.md)
- [프록시를 통해 인터넷에 액세스](accessing-the-internet-through-a-proxy.md)
- [데이터 요청](requesting-data.md)
- [방법: WebRequest 클래스를 사용하여 데이터 보내기](how-to-send-data-using-the-webrequest-class.md)
