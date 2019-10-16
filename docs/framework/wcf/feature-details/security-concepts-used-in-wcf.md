---
title: WCF에서 사용되는 보안 개념
ms.date: 03/30/2017
ms.assetid: 3b9dfcf5-4bf1-4f35-9070-723171c823a1
ms.openlocfilehash: 3ef2b9c104fa15de17a769c9ca9354e5cef085bf
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61990875"
---
# <a name="security-concepts-used-in-wcf"></a>WCF에서 사용되는 보안 개념
Windows Communication Foundation (WCF) 보안 개념을 이미 사용 중인 빌드 및 다양 한 보안 인프라에 배포 합니다.  
  
 WCF와 같은 계층 SSL (Secure Sockets) HTTP (HTTPS)을 통해 이러한 인프라 중 일부를 지원합니다. 그러나 WCF SOAP 인코딩된 메시지를 통해 최신 상호 운용 가능한 보안 표준 (예: Ws-security)를 구현 하 여 기존 보안 인프라를 지 원하는 초과 이동 합니다. 기존 메커니즘 또는 새로운 상호 운용 가능한 표준을 사용하는지 여부에 따라 두 가지의 보안 개념은 동일합니다. 따라서 기존 인프라 및 최신 표준에 적용된 개념을 이해하는 것이 특정 애플리케이션에 대해 가장 적합한 보안 모델을 구현하는 데 매우 중요합니다.  
  
## <a name="introduction-to-security-for-wcf-web-services"></a>WCF 웹 서비스 보안에 대한 소개  
 다운로드할 수 있는 WCF 보안 지침에 대 한 자세한 백서를 작성 하는 Microsoft Patterns and Practices 그룹: [WCF 보안 가이드](https://go.microsoft.com/fwlink/?LinkId=210210)합니다. 이 백서에서는 웹 서비스와 관련된 기본 보안 개념, 주요 WCF 보안 개념, 인트라넷 애플리케이션 시나리오 및 인터넷 애플리케이션 시나리오에 대해 설명합니다.  
  
## <a name="industry-wide-security-specifications"></a>산업 전반 보안 사양  
  
### <a name="public-key-infrastructure"></a>공개 키 인프라  
 PKI(공개 키 인프라)는 공개 키 암호화 사용을 통해 전자 트랜잭션에 참여하는 각각의 상대방을 확인하고 인증하는 디지털 인증서, 인증 기관 및 기타 등록 기관의 시스템입니다. 자세한 내용은 [Windows Server 2008 R2 인증서 서비스](https://go.microsoft.com/fwlink/?LinkId=210211)합니다.  
  
### <a name="kerberos-protocol"></a>Kerberos 프로토콜  
 합니다 *Kerberos 프로토콜* 는 Windows 도메인에서 사용자를 인증 하는 보안 메커니즘을 만들기에 대 한 사양입니다. 이를 통해 사용자가 도메인 내의 다른 엔터티로 보안 컨텍스트를 설정할 수 있습니다. Windows 2000 이상 플랫폼은 기본적으로 Kerberos 프로토콜을 사용합니다. 인트라넷 클라이언트와 상호 작용할 서비스를 만들 때 시스템의 메커니즘을 이해하는 것이 좋습니다. 또한 이후 합니다 *웹 서비스 보안 Kerberos 바인딩* 이 널리 게시를 사용할 수는 Kerberos 프로토콜 인터넷 클라이언트와 통신할 수 (즉, Kerberos 프로토콜은 상호 운용 가능). Windows에서 Kerberos 프로토콜을 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkId=210212)합니다.  
  
### <a name="x509-certificates"></a>X.509 인증서  
 X.509 인증서는 보안 애플리케이션에 사용되는 기본 자격 증명 양식입니다. 인증서 참조 X.509에 대 한 자세한 내용은 [X.509 공개 키 인증서](https://go.microsoft.com/fwlink/?LinkId=210213)합니다. X.509 인증서는 인증서 저장소 내에 저장됩니다. Windows를 실행하는 컴퓨터에는 여러 종류의 인증서 저장소가 있으며 저장소마다 용도가 다릅니다. 다양 한 저장소에 대 한 자세한 내용은 참조 하세요. [인증서 저장소](https://go.microsoft.com/fwlink/?LinkID=87787)합니다.  
  
## <a name="web-services-security-specifications"></a>웹 서비스 보안 사양  
 시스템 정의 바인딩에서는 일반적으로 많이 사용되는 웹 서비스 보안 사양을 지원합니다. 시스템 제공 바인딩 및 웹 서비스 사양의 전체 목록은 참조 지: [시스템 제공 상호 운용성 바인딩에서 지원하는 웹 서비스 프로토콜](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)  
  
## <a name="access-control-mechanisms"></a>Access Control 메커니즘  
 WCF에서는 서비스 또는 작업에 대한 액세스를 제어하는 여러 방법을 제공합니다. 다음과 같은 방법이 포함됩니다.  
  
1. <xref:System.Security.Permissions.PrincipalPermissionAttribute>  
  
2. ASP.NET 멤버 자격 공급자  
  
3. ASP.NET 역할 공급자  
  
4. 권한 부여 관리자  
  
5. ID 모델  
  
 이러한 항목 참조에 대 한 자세한 내용은 [Access Control 메커니즘](../../../../docs/framework/wcf/feature-details/access-control-mechanisms.md)  
  
## <a name="see-also"></a>참고자료

- [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [Windows Server appfabric 보안 모델](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
