---
ms.openlocfilehash: ae3766e2045b5834fbf6ea20415942413b1590c0
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858412"
---
### <a name="wcf-services-that-use-nettcp-with-ssl-security-and-md5-certificate-authentication"></a>SSL 보안 및 MD5 인증서 인증과 함께 NETTCP를 사용하는 WCF 서비스

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6은 WCF SSL 기본 프로토콜 목록에 TLS 1.1 및 TLS 1.2를 추가합니다. 클라이언트와 서버 컴퓨터 모두에 .NET Framework 4.6 이상이 설치되어 있으면 TLS 1.2가 협상에 사용됩니다. TLS 1.2는 MD5 인증서 인증을 지원하지 않습니다. 결과적으로, 고객이 MD5 인증서를 사용하는 경우 WCF 클라이언트는 WCF 서비스에 연결하지 못합니다.|
|제안|다음 중 하나를 수행하여 WCF 클라이언트가 WCF 서버에 연결할 수 있도록 함으로써 이 문제를 해결할 수 있습니다.<ul><li>MD5 알고리즘을 사용 하지 않도록 인증서를 업데이트합니다. 이것은 권장되는 해결 방법입니다.</li><li>소스 코드에서 바인딩이 동적으로 구성되지 않은 경우 TLS 1.1 또는 이전 버전의 프로토콜을 사용하도록 애플리케이션의 구성 파일을 업데이트합니다. 이렇게 하면 MD5 해시 알고리즘에서 인증서를 계속 사용할 수 있습니다.</li></ul> <blockquote> [!WARNING] MD5 해시 알고리즘을 사용하는 인증서는 안전하지 않은 것으로 간주되므로 이 해결 방법은 권장되지 않습니다.</blockquote> 다음 구성 파일에 이 내용이 나와 있습니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;system.serviceModel&gt;&#13;&#10;&lt;bindings&gt;&#13;&#10;&lt;netTcpBinding&gt;&#13;&#10;&lt;binding&gt;&#13;&#10;&lt;security mode= &quot;None/Transport/Message/TransportWithMessageCredential&quot; &gt;&#13;&#10;&lt;transport clientCredentialType=&quot;None/Windows/Certificate&quot;&#13;&#10;protectionLevel=&quot;None/Sign/EncryptAndSign&quot;&#13;&#10;sslProtocols=&quot;Ssl3/Tls1/Tls11&quot;&gt;&#13;&#10;&lt;/transport&gt;&#13;&#10;&lt;/security&gt;&#13;&#10;&lt;/binding&gt;&#13;&#10;&lt;/netTcpBinding&gt;&#13;&#10;&lt;/bindings&gt;&#13;&#10;&lt;/system.ServiceModel&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre><ul><li>소스 코드에서 바인딩이 동적으로 구성된 경우 소스 코드에서 TLS 1.1(<xref:System.Security.Authentication.SslProtocols.Tls11?displayProperty=nameWithType>) 또는 이전 버전의 프로토콜을 사용하도록 <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols?displayProperty=nameWithType> 속성을 업데이트합니다.</li></ul> <blockquote> [!WARNING] MD5 해시 알고리즘을 사용하는 인증서는 안전하지 않은 것으로 간주되므로 이 해결 방법은 권장되지 않습니다.</blockquote> |
|범위|부|
|버전|4.6|
|형식|런타임|

