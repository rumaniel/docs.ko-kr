---
title: 플러그형 프로토콜 소개
ms.date: 03/30/2017
helpviewer_keywords:
- data requests, pluggable protocols
- WebRequest class, pluggable protocols
- response to Internet request, pluggable protocols
- URI
- Windows Sockets
- request/response model
- sending data, pluggable protocols
- pluggable protocols
- WebClient class, about WebClient class
- pluggable protocols, about pluggable protocols
- Internet, pluggable protocols
- path identifiers
- Uniform Resource Identifier
- application development [.NET Framework], pluggable protocols
- requesting data from Internet, pluggable protocols
- receiving data, pluggable protocols
- protocols, pluggable
- server identifiers
- scheme identifiers
ms.assetid: 4b48e22d-e4e5-48f0-be80-d549bda97415
ms.openlocfilehash: a0a50af2d773a9489d9e908b751ba2035b9ba626
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50194022"
---
# <a name="introducing-pluggable-protocols"></a>플러그형 프로토콜 소개
Microsoft .NET Framework는 더 빠르고 쉽게 응용 프로그램에 통합할 수 있는 계층적이고 확장 가능하며 관리되는 인터넷 서비스 구현을 제공합니다. <xref:System.Net> 및 <xref:System.Net.Sockets> 네임스페이스의 인터넷 액세스 클래스를 사용하여 웹 기반 응용 프로그램과 인터넷 기반 응용 프로그램을 둘 다 구현할 수 있습니다.  
  
## <a name="internet-applications"></a>인터넷 응용 프로그램  
 인터넷 응용 프로그램은 다음과 같이 크게 두 종류로 분류할 수 있습니다. 정보를 요청하는 응용 프로그램 및 클라이언트의 정보 요청에 응답하는 서버 응용 프로그램. 클래식 인터넷 클라이언트-서버 응용 프로그램은 사용자가 브라우저를 사용하여 전 세계 웹 서버에 저장된 문서와 다른 데이터에 액세스하는 World Wide Web입니다.  
  
 응용 프로그램은 이러한 역할 중 하나만으로 제한되지 않습니다. 예를 들어 익숙한 중간 계층 응용 프로그램 서버는 다른 서버의 데이터를 요청하여 클라이언트의 요청에 응답합니다. 이 경우 이 응용 프로그램 서버는 동시에 서버 및 클라이언트로 동작합니다.  
  
 클라이언트 응용 프로그램은 요청 및 응답에 사용할 요청된 인터넷 리소스 및 통신 프로토콜을 식별하여 요청을 만듭니다. 필요한 경우 클라이언트는 요청을 완료하는 데 필요한 프록시 위치 또는 인증 정보(사용자 이름, 암호 등)와 같은 추가 데이터도 제공합니다. 요청이 구성된 후 요청이 서버에 전송될 수 있습니다.  
  
## <a name="identifying-resources"></a>리소스 식별  
 .NET Framework는 URI(Uniform Resource Identifier)를 사용하여 요청된 인터넷 리소스 및 통신 프로토콜을 식별합니다. URI는 다음과 같은 조각 중 3개 이상, 가능할 경우 4개로 구성됩니다. 요청 및 응답에 대한 통신 프로토콜을 식별하는 구성표 식별자, 인터넷에서 서버를 고유하게 식별하는 DNS(Domain Name System) 호스트 이름 또는 TCP 주소로 구성된 서버 식별자, 요청된 정보를 서버에 배치하는 경로 식별자 및 클라이언트에서 서버로 정보를 전달하는 선택적 쿼리 문자열. 예를 들어 URI `http://www.contoso.com/whatsnew.aspx?date=today`는 구성표 식별자 “http”, 서버 식별자 “www.contoso.com”, 경로 “/whatsnew.aspx” 및 쿼리 문자열 “?date=today”로 구성됩니다.  
  
 서버는 요청을 수신하고 응답을 처리한 후 응답을 클라이언트 응용 프로그램에 반환합니다. 응답에는 원시 텍스트 또는 XML 데이터 같은 콘텐츠 형식을 비롯한 보충 정보가 포함됩니다.  
  
## <a name="requests-and-responses-in-the-net-framework"></a>.NET Framework의 요청 및 응답  
 .NET Framework는 특정 클래스를 사용하여 요청/응답 모델을 통해 인터넷 리소스에 액세스하는 데 필요한 세 가지 정보인 검색할 인터넷 리소스의 URI가 포함된 <xref:System.Uri> 클래스, 리소스 요청이 포함된 <xref:System.Net.WebRequest> 클래스 및 들어오는 응답에 대한 컨테이너를 제공하는 <xref:System.Net.WebResponse> 클래스를 제공합니다.  
  
 클라이언트 응용 프로그램은 네트워크 리소스의 URI를 <xref:System.Net.WebRequest.Create%2A> 메서드에 전달하여 `WebRequest` 인스턴스를 만듭니다. 이 정적 메서드는 HTTP와 같은 특정 프로토콜에 대한 `WebRequest`를 만듭니다. 반환되는 `WebRequest`를 통해 서버에 대한 요청을 제어하는 속성에 액세스하고 요청이 생성될 때 전송되는 데이터 스트림에 액세스할 수 있습니다. `WebRequest`의 <xref:System.Net.WebRequest.GetResponse%2A> 메서드는 클라이언트 응용 프로그램에서 URI로 식별되는 서버로 요청을 보냅니다. 응답이 지연될 수 있는 경우 **WebRequest**에서 <xref:System.Net.WebRequest.BeginGetResponse%2A> 메서드를 사용하여 비동기적으로 요청을 만들 수 있고 나중에 <xref:System.Net.WebRequest.EndGetResponse%2A> 메서드를 사용하여 응답을 반환할 수 있습니다.  
  
 **GetResponse** 및 **EndGetResponse** 메서드는 서버에서 반환되는 데이터에 액세스할 수 있는 **WebResponse**를 반환합니다. 이 데이터는 <xref:System.Net.WebResponse.GetResponseStream%2A> 메서드를 통해 요청하는 응용 프로그램에 스트림으로 제공되므로 데이터 스트림이 사용되는 모든 응용 프로그램에서 사용할 수 있습니다.  
  
 **WebRequest** 및 **WebResponse** 클래스는 플러그형 프로토콜의 기반으로, 각 리소스가 사용하는 프로토콜의 특정 세부 정보를 걱정할 필요 없이 인터넷 리소스를 사용하는 응용 프로그램을 개발할 수 있는 네트워크 서비스를 구현합니다. **WebRequest**의 하위 항목 클래스는 인터넷 리소스에 실제 연결하는 작업의 세부 정보를 관리하기 위해 **WebRequest** 클래스에 등록됩니다.  
  
 예를 들어 <xref:System.Net.HttpWebRequest> 클래스는 HTTP를 사용하여 인터넷 리소스에 연결하는 작업의 세부 정보를 관리합니다. 기본적으로 **WebRequest.Create** 메서드가 “http:” 또는 “https:”(HTTP 및 보안 HTTP를 나타내는 프로토콜 식별자)으로 시작하는 URI를 발견하면, 반환되는 **WebRequest**를 있는 그대로 사용할 수 있고, 이러한 항목을 발견하지 않을 경우에는 **HttpWebRequest**로 형식 캐스팅하여 프로토콜별 속성에 액세스할 수 있습니다. 대부분의 경우 **WebRequest**는 요청을 만드는 데 필요한 모든 정보를 제공합니다.  
  
 요청/응답 트랜잭션으로 표현될 수 있는 모든 프로토콜을 **WebRequest**에서 사용할 수 있습니다. **WebRequest** 및 **WebResponse**에서 프로토콜별 클래스를 파생시킨 다음 정적 <xref:System.Net.WebRequest.RegisterPrefix%2A?displayProperty=nameWithType> 메서드를 사용하여 응용 프로그램에서 사용하도록 등록할 수 있습니다.  
  
 인터넷 요청에 대한 클라이언트 권한 부여가 필요할 경우 **WebRequest**의 <xref:System.Net.WebRequest.Credentials%2A> 속성이 필요한 자격 증명을 제공합니다. 이러한 자격 증명은 기본 HTTP 또는 다이제스트 인증의 경우 간단한 이름/암호 쌍이고, NTLM 또는 Kerberos 인증의 경우 이름/암호/도메인 집합일 수 있습니다. 하나의 자격 증명 집합을 <xref:System.Net.NetworkCredential> 인스턴스에 저장하거나 여러 집합을 동시에 <xref:System.Net.CredentialCache> 인스턴스에 저장할 수 있습니다. **CredentialCache**는 서버에 보낼 자격 증명을 결정하기 위해 서버에서 지원하는 인증 체계 및 요청 URI를 사용합니다.  
  
## <a name="simple-requests-with-webclient"></a>WebClient를 사용한 간단한 요청  
 인터넷 리소스에 대한 간단한 요청을 만들어야 하는 응용 프로그램의 경우 <xref:System.Net.WebClient> 클래스는 인터넷 서버에서 데이터를 업로드하거나 다운로드할 수 있는 일반적인 메서드를 제공합니다. **WebClient**는 **WebRequest** 클래스를 사용하여 인터넷 리소스에 액세스할 수 있으므로 **WebClient** 클래스는 모든 등록된 플러그형 프로토콜을 사용할 수 있습니다.  
  
 요청/응답 모델을 사용할 수 없는 응용 프로그램 또는 요청을 보내고 네트워크에서 수신 대기해야 하는 응용 프로그램을 위해 **System.Net.Sockets** 네임스페이스는 <xref:System.Net.Sockets.TcpClient>, <xref:System.Net.Sockets.TcpListener> 및 <xref:System.Net.Sockets.UdpClient> 클래스를 제공합니다. 이러한 클래스는 다양한 전송 프로토콜을 사용하여 연결을 만드는 작업의 세부 정보를 처리하고 응용 프로그램에 대한 네트워크 연결을 스트림으로 노출합니다.  
  
 Windows 소켓 인터페이스에 익숙한 개발자나 소켓 수준에서 프로그래밍을 통해 제공되는 컨트롤이 필요한 개발자는 **System.Net.Sockets** 클래스가 필요에 맞는다는 것을 알 수 있습니다. **System.Net.Sockets** 클래스는 **System.Net** 클래스 내에서 관리 코드에서 네이티브 코드로 전환되는 지점입니다. 대부분의 경우 **System.Net.Sockets** 클래스는 데이터를 Windows 32비트 데이터로 마샬링하고 모든 필요한 보안 검사를 처리합니다.  
  
## <a name="see-also"></a>참고 항목  
 [플러그형 프로토콜 프로그래밍](../../../docs/framework/network-programming/programming-pluggable-protocols.md)  
 [.NET Framework의 네트워크 프로그래밍](../../../docs/framework/network-programming/index.md)  
 [네트워크 프로그래밍 샘플](../../../docs/framework/network-programming/network-programming-samples.md)  
 [MSDN 코드 갤러리의 .NET용 네트워킹 샘플](https://code.msdn.microsoft.com/Wiki/View.aspx?ProjectName=nclsamples)
