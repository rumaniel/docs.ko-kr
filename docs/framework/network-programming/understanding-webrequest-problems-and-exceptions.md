---
title: WebRequest 문제 및 예외 이해
ms.date: 03/30/2017
ms.assetid: 74a361a5-e912-42d3-8f2e-8e9a96880a2b
ms.openlocfilehash: c5712467cdebb854d09cb55c29878cb8b553f271
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047096"
---
# <a name="understanding-webrequest-problems-and-exceptions"></a>WebRequest 문제 및 예외 이해
<xref:System.Net.WebRequest> 및 파생 클래스(<xref:System.Net.HttpWebRequest>, <xref:System.Net.FtpWebRequest> 및 <xref:System.Net.FileWebRequest>)는 예외를 throw하여 비정상 상태를 알립니다. 이러한 문제의 해결이 분명하지 않은 경우도 있습니다.  
  
## <a name="solutions"></a>솔루션  
 <xref:System.Net.WebException>의 <xref:System.Net.WebException.Status%2A> 속성을 검사하여 문제를 확인합니다. 다음 표에서는 여러 상태 값과 몇 가지 가능한 해결 방법을 보여 줍니다.  
  
|상태|세부 정보|솔루션|  
|------------|-------------|--------------|  
|<xref:System.Net.WebExceptionStatus.SendFailure><br /><br /> 또는<br /><br /> <xref:System.Net.WebExceptionStatus.ReceiveFailure>|기본 소켓에 문제가 있습니다. 연결이 재설정되었을 수 있습니다.|다시 연결하여 요청을 다시 보내세요.<br /><br /> 최신 서비스 팩이 설치되어 있는지 확인합니다.<br /><br /> <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A?displayProperty=nameWithType> 속성 값을 늘립니다.<br /><br /> <xref:System.Net.HttpWebRequest.KeepAlive%2A?displayProperty=nameWithType>를 `false`로 설정합니다.<br /><br /> <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> 속성을 사용하여 최대 연결 수를 늘립니다.<br /><br /> 프록시 구성을 확인합니다.<br /><br /> SSL을 사용하는 경우 서버 프로세스에 인증서 저장소에 액세스할 수 있는 권한이 있는지 확인합니다.<br /><br /> 대량 데이터를 보내는 경우 <xref:System.Net.HttpWebRequest.AllowWriteStreamBuffering%2A>을 `false`로 설정합니다.|  
|<xref:System.Net.WebExceptionStatus.TrustFailure>|서버 인증서의 유효성을 검사할 수 없습니다.|Internet Explorer를 사용하여 URI를 열려고 합니다. IE에 표시되는 보안 경고를 해결합니다. 보안 경고를 해결할 수 없는 경우 `true`를 반환하는 <xref:System.Net.ICertificatePolicy>를 구현하는 인증서 정책 클래스를 만든 후 <xref:System.Net.ServicePointManager.CertificatePolicy%2A>에 전달할 수 있습니다.<br /><br /> <https://support.microsoft.com/?id=823177>을 참조하세요.<br /><br /> 서버 인증서에 서명한 인증 기관의 인증서가 Internet Explorer의 신뢰할 수 있는 인증 기관 목록에 추가되었는지 확인합니다.<br /><br /> URL의 호스트 이름이 서버 인증서의 일반 이름과 일치하는지 확인합니다.|  
|<xref:System.Net.WebExceptionStatus.SecureChannelFailure>|SSL 트랜잭션에 오류가 발생했거나 인증서 문제가 있습니다.|.NET Framework 버전 1.1에서는 SSL 버전 3.0만 지원합니다. 서버에서 TLS 버전 1.0 또는 SSL 버전 2.0만 사용하는 경우 예외가 throw됩니다. .NET Framework 버전 2.0으로 업그레이드하고 <xref:System.Net.ServicePointManager.SecurityProtocol%2A>을 서버와 일치하도록 설정합니다.<br /><br /> 클라이언트 인증서가 서버에서 신뢰하지 않는 CA(인증 기관)에 의해 서명되었습니다. 서버에 CA의 인증서를 설치합니다. <https://support.microsoft.com/?id=332077>을 참조하세요.<br /><br /> 최신 서비스 팩이 설치되어 있는지 확인합니다.|  
|<xref:System.Net.WebExceptionStatus.ConnectFailure>|연결하지 못했습니다.|방화벽 또는 프록시가 연결을 차단합니다. 연결을 허용하도록 방화벽 또는 프록시를 수정합니다.<br /><br /> <xref:System.Net.WebProxy> 생성자(WebServiceProxyClass.Proxy = new WebProxy([http://server:80](http://server/), true))를 호출하여 클라이언트 애플리케이션에서 <xref:System.Net.WebProxy> 를 명시적으로 지정합니다.<br /><br /> Filemon 또는 Regmon을 실행하여 작업자 프로세스 ID에 WSPWSP.dll, HKLM\System\CurrentControlSet\Services\DnsCache 또는 HKLM\System\CurrentControlSet\Services\WinSock2를 액세스하는 데 필요한 권한이 있는지 확인합니다.|  
|<xref:System.Net.WebExceptionStatus.NameResolutionFailure>|도메인 이름 서비스가 호스트 이름을 확인할 수 없습니다.|프록시를 올바르게 구성합니다. <https://support.microsoft.com/?id=318140>을 참조하세요.<br /><br /> 설치된 바이러스 백신 소프트웨어 또는 방화벽이 연결을 차단하지 않는지 확인합니다.|  
|<xref:System.Net.WebExceptionStatus.RequestCanceled>|<xref:System.Net.WebRequest.Abort%2A>가 호출되었거나 오류가 발생했습니다.|이 문제는 클라이언트 또는 서버의 부하가 심해서 발생했을 수 있습니다. 부하를 줄입니다.<br /><br /> <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> 설정을 늘립니다.<br /><br /> <https://support.microsoft.com/?id=821268>을 참조하여 웹 서비스 성능 설정을 수정합니다.|  
|<xref:System.Net.WebExceptionStatus.ConnectionClosed>|애플리케이션이 이미 닫힌 소켓에 쓰려고 했습니다.|클라이언트 또는 서버가 오버로드되었습니다. 부하를 줄입니다.<br /><br /> <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> 설정을 늘립니다.<br /><br /> <https://support.microsoft.com/?id=821268>을 참조하여 웹 서비스 성능 설정을 수정합니다.|  
|<xref:System.Net.WebExceptionStatus.MessageLengthLimitExceeded>|메시지 길이에 설정된 제한(<xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>)을 초과했습니다.|<xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A> 속성 값을 늘립니다.|  
|<xref:System.Net.WebExceptionStatus.ProxyNameResolutionFailure>|도메인 이름 서비스가 프록시 호스트 이름을 확인할 수 없습니다.|프록시를 올바르게 구성합니다. <https://support.microsoft.com/?id=318140>을 참조하세요.<br /><br /> <xref:System.Net.HttpWebRequest.Proxy%2A> 속성을 `null`로 설정하여 <xref:System.Net.HttpWebRequest>가 프록시를 사용하지 않도록 강제로 적용합니다.|  
|<xref:System.Net.WebExceptionStatus.ServerProtocolViolation>|서버 응답이 유효한 HTTP 응답이 아닙니다. 이 문제는 .NET Framework에서 서버 응답이 HTTP 1.1 RFC에 맞지 않는 것을 감지할 경우 발생합니다. 응답에 잘못된 헤더 또는 잘못된 헤더 구분 기호가 포함된 경우 이 문제가 발생할 수 있습니다. RFC 2616에서는 HTTP 1.1 및 서버 응답에 유효한 형식을 정의합니다. 자세한 내용은 [IETF(Internet Engineering Task Force)](https://www.ietf.org/) 웹 사이트에서 [RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1](https://go.microsoft.com/fwlink/?LinkID=147388)을 참조하세요.|트랜잭션의 네트워크 추적을 가져오고 응답의 헤더를 검사합니다.<br /><br /> 애플리케이션에 구문 분석 없이 서버 응답이 필요한 경우(보안 문제가 발생할 수 있음) 구성 파일에서 `useUnsafeHeaderParsing`을 `true`로 설정합니다. [\<httpWebRequest> 요소(네트워크 설정)](../configure-apps/file-schema/network/httpwebrequest-element-network-settings.md)를 참조하세요.|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Net.HttpWebRequest>
- <xref:System.Net.HttpWebResponse>
- <xref:System.Net.Dns>
