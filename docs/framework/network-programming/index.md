---
title: .NET Framework의 네트워크 프로그래밍
ms.date: 03/30/2017
helpviewer_keywords:
- Networking
- Internet
- Internet, .NET Framework Internet services
- Network Resources
ms.assetid: 8d455610-67a0-4fa8-a62f-7747064a9256
ms.openlocfilehash: 230825c5259807cf693179878a45aeb3fdcbf0ac
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047990"
---
# <a name="network-programming-in-the-net-framework"></a>.NET Framework의 네트워크 프로그래밍
Microsoft .NET Framework는 더 빠르고 쉽게 애플리케이션에 통합할 수 있는 계층적이고 확장 가능하며 관리되는 인터넷 서비스 구현을 제공합니다. 네트워크 애플리케이션은 플러그 가능한 프로토콜을 바탕으로 빌드하여 새 인터넷 프로토콜을 자동으로 이용하거나, Windows 소켓 인터페이스의 관리되는 구현을 사용하여 소켓 수준에서 네트워크 작업을 수행할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  

 [플러그형 프로토콜 소개](introducing-pluggable-protocols.md)  
 필요한 액세스 프로토콜에 관계없이 인터넷 리소스에 액세스하는 방법을 설명합니다.  
  
 [데이터 요청](requesting-data.md)  
 플러그 가능한 프로토콜을 사용하여 인터넷 리소스에 데이터를 업로드하고 이 리소스에서 데이터를 다운로드하는 방법을 설명합니다.  
  
 [플러그형 프로토콜 프로그래밍](programming-pluggable-protocols.md)  
 플러그 가능한 프로토콜을 구현하기 위한 프로토콜별 클래스를 파생하는 방법을 설명합니다.  
  
 [애플리케이션 프로토콜 사용](using-application-protocols.md)  
 TCP, UDP, HTTP와 같은 네트워크 프로토콜을 이용하는 프로그래밍 애플리케이션을 설명합니다.  
  
 [인터넷 프로토콜 버전 6](internet-protocol-version-6.md)  
 현재 버전의 인터넷 프로토콜 모음(IPv4)에 비해 인터넷 프로토콜 버전 6(IPv6)이 지닌 장점을 설명하고, IPv6 주소 지정, 라우팅 및 자동 구성, IPv6을 사용하거나 사용하지 않는 방법을 설명합니다.  
  
 [인터넷 애플리케이션 구성](configuring-internet-applications.md)  
 .NET Framework 구성 파일을 사용하여 인터넷 애플리케이션을 구성하는 방법을 설명합니다.  
  
 [.NET Framework의 네트워크 추적](network-tracing.md)  
 네트워크 추적을 사용하여 메서드 호출과 관리되는 애플리케이션에서 생성되는 네트워크 트래픽에 대한 정보를 얻는 방법을 설명합니다.  
  
 [네트워크 애플리케이션에 대한 캐시 관리](cache-management-for-network-applications.md)  
 <xref:System.Net.WebClient?displayProperty=nameWithType>, <xref:System.Net.WebRequest?displayProperty=nameWithType>및 <xref:System.Net.HttpWebRequest?displayProperty=nameWithType> 클래스를 사용하는 애플리케이션에 대한 캐싱을 사용하는 방법을 설명합니다.  
  
 [네트워크 프로그래밍의 보안](security-in-network-programming.md)  
 표준 인터넷 보안 및 인증 기술을 사용하는 방법을 설명합니다.  
  
 [System.Net 클래스에 대한 모범 사례](best-practices-for-system-net-classes.md)  
 인터넷 애플리케이션을 최대한 활용하기 위한 팁과 트릭을 제공합니다.  
  
 [프록시를 통해 인터넷 액세스](accessing-the-internet-through-a-proxy.md)  
 프록시를 구성하는 방법을 설명합니다.  
  
 [NetworkInformation](networkinformation.md)  
 네트워크 이벤트, 변경 사항, 통계 및 속성에 대한 정보를 수집하는 방법을 설명하고, <xref:System.Net.NetworkInformation.Ping?displayProperty=nameWithType> 클래스를 사용하여 원격 호스트에 연결할 수 있는지 확인하는 방법도 설명합니다.  
  
 [버전 2.0에서 System.Uri 네임스페이스 변경 내용](changes-to-the-system-uri-namespace-in-version-2-0.md)  
 잘못된 동작을 수정하고 유용성을 향상하고 보안을 강화하기 위해 버전 2.0에서 <xref:System.Uri?displayProperty=nameWithType> 클래스에 대해 이루어진 여러 가지 변경 사항을 설명합니다.  
  
 [System.Uri의 국가별 리소스 식별자 지원](international-resource-identifier-support-in-system-uri.md)  
 IRI(International Resource Identifier) 및 IDN(Internationalized Domain Name) 지원을 위해 버전 3.5, 3.0 SP1 및 2.0 SP1에서 <xref:System.Uri?displayProperty=nameWithType> 클래스에 대해 강화된 기능을 설명합니다.  
  
 [버전 3.5의 소켓 성능 향상](socket-performance-enhancements-in-version-3-5.md)  
 버전 3.5, 3.0 SP1 및 2.0 SP1에서 <xref:System.Net.Sockets.Socket?displayProperty=nameWithType> 클래스에 대해 강화된 여러 가지 기능을 설명하며, 이런 기능에서는 특수화된 고성능 소켓 애플리케이션에서 사용할 수 있는 대체 비동기 패턴을 제공합니다.  
  
 [피어 이름 확인 프로토콜](peer-name-resolution-protocol.md)  
 버전 3.5에서 PNRP(Peer Name Resolution Protocol), 서버가 없는 동적 이름 등록 및 이름 확인 프로토콜을 지원하기 위해 추가된 지원 기능을 설명합니다. 이런 새로운 기능은 <xref:System.Net.PeerToPeer?displayProperty=nameWithType> 네임스페이스에 의해 지원됩니다.  
  
 [피어 투 피어 협업](peer-to-peer-collaboration.md)  
 PNRP를 기반으로 빌드되는 피어 투 피어 협업을 지원하기 위해 버전 3.5에 추가된 지원 기능을 설명합니다. 이런 새로운 기능은 <xref:System.Net.PeerToPeer.Collaboration?displayProperty=nameWithType> 네임스페이스에 의해 지원됩니다.  
  
 [버전 3.5 SP1에서 HttpWebRequest에 대한 NTLM 인증 변경 내용](changes-to-ntlm-authentication-for-httpwebrequest-in-version-3-5-sp1.md)  
 버전 3.5 SP1에서 <xref:System.Net.HttpWebRequest?displayProperty=nameWithType>, <xref:System.Net.HttpListener?displayProperty=nameWithType>, <xref:System.Net.Security.NegotiateStream?displayProperty=nameWithType>및 System.Net 네임스페이스의 관련 클래스에 의해 통합 Windows 인증이 처리되는 방식에 영향을 미치는 보안 변경 사항을 설명합니다.  
  
 [확장된 보호를 사용하는 Windows 통합 인증](integrated-windows-authentication-with-extended-protection.md)  
 <xref:System.Net.HttpWebRequest?displayProperty=nameWithType>, <xref:System.Net.HttpListener?displayProperty=nameWithType>, <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>, <xref:System.Net.Security.SslStream?displayProperty=nameWithType>, <xref:System.Net.Security.NegotiateStream?displayProperty=nameWithType>, 그리고 <xref:System.Net?displayProperty=nameWithType> 및 관련 네임스페이스의 관련 클래스에 의해 통합 Windows 인증이 처리되는 방식에 영향을 미치는 확장된 보호를 위해 향상된 기능을 설명합니다.  
  
 [IPv6 및 Teredo를 사용하는 NAT 통과](nat-traversal-using-ipv6-and-teredo.md)  
 IPv6 및 Teredo를 사용하여 NAT 통과를 지원하기 위해 <xref:System.Net?displayProperty=nameWithType>, <xref:System.Net.NetworkInformation?displayProperty=nameWithType>및 <xref:System.Net.Sockets?displayProperty=nameWithType> 네임스페이스에 추가된 향상된 기능을 설명합니다.  
  
 [Windows 스토어 앱에 대한 네트워크 격리](network-isolation-for-windows-store-apps.md)  
 <xref:System.Net>, <xref:System.Net.Http>및 <xref:System.Net.Http.Headers> 네임스페이스의 클래스가 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 사용될 때 네트워크 격리가 미치는 영향을 설명합니다.  
  
 [네트워크 프로그래밍 샘플](network-programming-samples.md)  
 <xref:System.Net>, <xref:System.Net.Cache>, <xref:System.Net.Configuration>, <xref:System.Net.Mail>, <xref:System.Net.Mime>, <xref:System.Net.NetworkInformation>, <xref:System.Net.PeerToPeer>, <xref:System.Net.Security>, <xref:System.Net.Sockets> 네임스페이스의 클래스를 사용하는 다운로드 가능한 네트워크 프로그래밍 샘플에 대한 링크입니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Net?displayProperty=nameWithType>  
 오늘날 네트워크에 사용되는 여러 프로토콜을 위한 간단한 프로그래밍 인터페이스를 제공합니다. 이 네임스페이스의 <xref:System.Net.WebRequest?displayProperty=nameWithType> 및 <xref:System.Net.WebResponse?displayProperty=nameWithType> 클래스는 플러그 가능한 프로토콜을 위한 기초입니다.  
  
 <xref:System.Net.Cache?displayProperty=nameWithType>  
 <xref:System.Net.WebRequest?displayProperty=nameWithType> 및 <xref:System.Net.HttpWebRequest?displayProperty=nameWithType> 클래스를 사용하여 얻은 리소스에 대한 캐시 정책을 정의하는 데 사용되는 형식과 열거형을 정의합니다.  
  
 <xref:System.Net.Configuration?displayProperty=nameWithType>  
 애플리케이션에서 System.Net 네임스페이스에 대한 구성 설정을 프로그래밍 방식으로 액세스 및 업데이트하는 데 사용하는 클래스입니다.  
  
 <xref:System.Net.Http?displayProperty=nameWithType>  
 최신 HTTP 애플리케이션의 프로그래밍 인터페이스를 제공하는 클래스입니다.  
  
 <xref:System.Net.Http.Headers?displayProperty=nameWithType>  
 <xref:System.Net.Http?displayProperty=nameWithType> 네임스페이스에서 사용되는 HTTP 헤더의 컬렉션 지원을 제공합니다.  
  
 <xref:System.Net.Mail?displayProperty=nameWithType>  
 SMTP 프로토콜을 사용하여 메일을 작성하고 보내기 위한 클래스입니다.  
  
 <xref:System.Net.Mime?displayProperty=nameWithType>  
 <xref:System.Net.Mail?displayProperty=nameWithType> 네임스페이스의 클래스에 사용되는 MIME(Multipurpose Internet Mail Exchange) 헤더를 나타내는 데 사용되는 형식을 정의합니다.  
  
 <xref:System.Net.NetworkInformation?displayProperty=nameWithType>  
 네트워크 이벤트, 변경 사항, 통계 및 속성에 대한 정보를 프로그래밍 방식으로 수집하기 위한 클래스입니다.  
  
 <xref:System.Net.PeerToPeer?displayProperty=nameWithType>  
 개발자를 위한 PNRP(피어 이름 확인 프로토콜)의 관리되는 구현을 제공합니다.  
  
 <xref:System.Net.PeerToPeer.Collaboration?displayProperty=nameWithType>  
 개발자를 위한 피어-투-피어 협업 인터페이스의 관리되는 구현을 제공합니다.  
  
 <xref:System.Net.Security?displayProperty=nameWithType>  
 호스트 간의 보안 통신을 위한 네트워크 스트림을 제공하는 클래스입니다.  
  
 <xref:System.Net.Sockets?displayProperty=nameWithType>  
 네트워크 액세스를 제어해야 하는 개발자를 위한 Winsock(Windows 소켓) 인터페이스에 대해 관리되는 구현을 제공합니다.  
  
 <xref:System.Net.WebSockets?displayProperty=nameWithType>  
 개발자를 위한 WebSocket 인터페이스에 대해 관리되는 구현을 제공합니다.  
  
 <xref:System.Uri?displayProperty=nameWithType>  
 URI(Uniform Resource Indentifier)의 개체 표현을 제공하며 URI 부분에 쉽게 액세스할 수 있도록 합니다.  
  
 <xref:System.Security.Authentication.ExtendedProtection?displayProperty=nameWithType>  
 애플리케이션의 확장된 보호를 사용하여 인증을 지원합니다.  
  
 <xref:System.Security.Authentication.ExtendedProtection.Configuration?displayProperty=nameWithType>  
 애플리케이션의 확장된 보호를 사용하여 인증 구성을 지원합니다.  
  
## <a name="see-also"></a>참고 항목

- [.NET Framework를 사용한 TLS(전송 계층 보안) 모범 사례](tls.md)
- [네트워크 프로그래밍 방법 항목](network-programming-how-to-topics.md)
- [네트워크 프로그래밍 샘플](network-programming-samples.md)
- [HttpClient 샘플](https://code.msdn.microsoft.com/windowsapps/HttpClient-sample-55700664)
