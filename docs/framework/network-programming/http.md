---
title: HTTP
ms.date: 03/30/2017
helpviewer_keywords:
- protocols, HTTP
- sending data, HTTP
- HttpWebResponse class, sending and receiving data
- HTTP
- receiving data, HTTP
- application protocols, HTTP
- Internet, HTTP
- network resources, HTTP
- HTTP, about HTTP
- HttpWebRequest class, sending and receiving data
ms.assetid: 985fe5d8-eb71-4024-b361-41fbdc1618d8
ms.openlocfilehash: 65a799355e35fc7d14e3aaad973209147f7e7eae
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50182881"
---
# <a name="http"></a>HTTP
.NET Framework에서는 <xref:System.Net.HttpWebRequest> 및 <xref:System.Net.HttpWebResponse> 클래스를 사용하여 모든 인터넷 트래픽의 대부분을 구성하는 HTTP 프로토콜을 포괄적으로 지원합니다. <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse>에서 파생된 이러한 클래스는 기본적으로 정적 메서드 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType>가 “http” 또는 “https”로 시작하는 URI를 발견할 때마다 반환됩니다. 대부분의 경우 **WebRequest** 및 **WebResponse** 클래스는 요청을 만드는 데 필요한 모든 것을 제공하지만, 속성으로 노출되는 HTTP별 기능에 액세스해야 할 경우 이러한 클래스를 **HttpWebRequest** 또는 **HttpWebResponse**로 형식 캐스팅해야 합니다.  
  
 **HttpWebRequest** 및 **HttpWebResponse**는 표준 HTTP 요청 및 응답 트랜잭션을 캡슐화하고 일반 HTTP 헤더에 대한 액세스를 제공합니다. 이러한 클래스는 청크로 데이터 파이프라이닝/보내기/받기, 인증, 사전 인증, 암호화, 프록시 지원, 서버 인증서 유효성 검사, 연결 관리를 포함한 대부분의 HTTP 1.1 기능을 지원합니다. 사용자 지정 헤더 및 속성을 통해 제공되지 않는 헤더는 **Headers** 속성에 저장하고 이 속성을 통해 액세스할 수 있습니다.  
  
 **HttpWebRequest**는 **WebRequest**에서 사용되는 기본 클래스이며 URI를 **WebRequest.Create** 메서드에 전달하기 전에 등록되어 있으면 안 됩니다.  
  
 <xref:System.Net.HttpWebRequest.AllowAutoRedirect%2A> 속성을 **true**(기본값)로 설정하여 응용 프로그램이 HTTP 리디렉션을 자동으로 따르도록 구성할 수 있습니다. 응용 프로그램이 요청을 리디렉션하고 **HttpWebResponse**의 <xref:System.Net.HttpWebResponse.ResponseUri%2A> 속성에는 요청에 응답하는 실제 웹 리소스가 포함됩니다. **AllowAutoRedirect**를 **false**로 설정할 경우 응용 프로그램이 리디렉션을 HTTP 프로토콜 오류로 처리할 수 있어야 합니다.  
  
 응용 프로그램은 <xref:System.Net.WebException.Status%2A>가 <xref:System.Net.WebExceptionStatus>로 설정된 <xref:System.Net.WebException>을 catch하여 HTTP 프로토콜 오류를 수신합니다. <xref:System.Net.WebException.Response%2A> 속성은 서버에서 보낸 **WebResponse**를 포함하고 발생한 실제 HTTP 오류를 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [프록시를 통해 인터넷 액세스](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)  
 [응용 프로그램 프로토콜 사용](../../../docs/framework/network-programming/using-application-protocols.md)  
 [방법: HTTP 관련 속성에 액세스](../../../docs/framework/network-programming/how-to-access-http-specific-properties.md)
