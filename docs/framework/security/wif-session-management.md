---
title: WIF 세션 관리
ms.date: 03/30/2017
ms.assetid: 98bce126-18a9-401b-b20d-67ee462a5f8a
author: BrucePerlerMS
ms.openlocfilehash: 141eda509530cab1120d519c3cbc94693ef1cc51
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69946230"
---
# <a name="wif-session-management"></a>WIF 세션 관리
클라이언트는 신뢰 당사자에 호스트된 보호된 리소스에 처음 액세스를 시도할 때 먼저 신뢰 당사자에 의해 신뢰된 STS(보안 토큰 서비스)에 인증해야 합니다. 그런 다음 STS는 클라이언트에 보안 토큰을 발급합니다. 클라이언트가 신뢰 당사자에게 이 토큰을 제공하면 신뢰 당사자가 보호된 리소스에 대한 액세스를 클라이언트에 부여합니다. 그러나 동일한 컴퓨터 또는 신뢰 당사자와 동일한 도메인에 없을 수도 있기 때문에 클라이언트가 각 요청에 대해 STS에 다시 인증할 필요가 없기를 바랍니다. 대신 WIF(Windows Identity Foundation)에서는 클라이언트 및 신뢰 당사자가 세션을 설정하고, 세션 중에 클라이언트는 첫 번째 요청 이후의 모든 요청에 대해 세션 보안 토큰을 사용하여 신뢰 당사자에 인증합니다. 신뢰 당사자는 쿠키 안에 저장된 이 세션 보안 토큰을 사용하여 클라이언트의 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType>을 다시 구성할 수 있습니다.  
  
 STS는 클라이언트에서 제공해야 하는 인증을 정의합니다. 그러나 STS에 인증하는 데 사용할 수 있는 자격 증명이 클라이언트에 여러 개 있을 수도 있습니다. 예를 들어 Windows Live의 토큰, 사용자 이름 및 암호, 인증서 및 smartkey가 있을 수 있습니다. 이 경우 STS는 클라이언트에 여러 ID를 부여하며, 각 ID는 클라이언트에서 제공하는 자격 증명 중 하나에 해당합니다. 신뢰 당사자는 클라이언트에 부여할 액세스 수준을 결정할 때 이러한 ID 중 하나 이상을 사용할 수 있습니다.  
  
 <xref:System.IdentityModel.Tokens.SessionSecurityToken?displayProperty=nameWithType>은 클라이언트의 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType>을 다시 구성하는 데 사용되며, <xref:System.Security.Claims.ClaimsPrincipal.Identities%2A>에 있는 모든 클라이언트 ID를 포함합니다. 컬렉션에 있는 각 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType>에는 해당 ID와 연결된 부트스트랩 토큰이 포함됩니다.  
  
 새 세션 토큰이 원래 세션 토큰의 세션 ID로 발급된 경우 <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler?displayProperty=nameWithType>는 토큰 캐시의 세션 토큰을 업데이트하지 않습니다. 항상 고유한 세션 ID로 세션 토큰을 인스턴스화해야 합니다.  
  
> [!NOTE]
> Session.SecurityTokenHandler.ReadToken은 잘못된 입력을 수신할 경우 <xref:System.Xml.XmlException> 예외를 throw합니다. 예를 들어 세션 토큰을 포함하는 쿠키가 손상된 경우입니다. 이 예외를 catch하고 애플리케이션별 동작을 제공하는 것이 좋습니다.  
  
 보호된 웹 페이지에 보호된 도메인에도 있는 많은 리소스(예: 작은 그래픽)가 포함되어 있을 경우 클라이언트는 각 리소스를 다운로드하기 위해 신뢰 당사자에 다시 인증해야 합니다. 세션 인증 토큰을 사용하면 각 요청에 대해 STS에 인증할 필요가 없지만 여전히 많은 쿠키가 전송되고 있음을 의미합니다. 미러 항목이 보호되지 않은 도메인에 저장되고 기본 웹 페이지에서 연결되는 동안 중요한 데이터와 리소스가 보호된 도메인에 저장되도록 웹 페이지를 설정하는 것이 좋습니다. 또한 보호된 도메인만 참조하도록 쿠키 경로를 설정합니다.  
  
 참조 모드로 작동하려면 **global.asax.cs** 파일에 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SessionSecurityTokenCreated> 이벤트 처리기를 제공하고 <xref:System.IdentityModel.Services.SessionSecurityTokenCreatedEventArgs.SessionToken%2A> 속성에 전달된 토큰에 **IsReferenceMode** 속성을 설정하는 것이 좋습니다. 이러한 업데이트는 세션 토큰이 모든 요청에 대해 참조 모드로 작동하고 단순히 세션 인증 모듈에 <xref:System.IdentityModel.Services.SessionAuthenticationModule.IsReferenceMode%2A> 속성을 설정하여 우선 적용되도록 합니다.  
  
## <a name="extensibility"></a>확장성  
 세션 관리 메커니즘을 확장할 수 있습니다. 이 작업의 한 가지 이유는 성능을 향상하기 위한 것입니다. 예를 들어 메모리 내 상태와 쿠키에 포함할 항목 간에 세션 보안 토큰을 변환 또는 최적화하는 사용자 지정 쿠키 처리기를 만들 수 있습니다. 이 작업을 위해 <xref:System.IdentityModel.Services.CookieHandler?displayProperty=nameWithType>에서 파생되는 사용자 지정 쿠키 처리기를 사용하도록 <xref:System.IdentityModel.Services.SessionAuthenticationModule?displayProperty=nameWithType>의 <xref:System.IdentityModel.Services.SessionAuthenticationModule.CookieHandler%2A?displayProperty=nameWithType> 속성을 구성할 수 있습니다. 쿠키는 HTTP(Hypertext Transfer Protocol)에 허용되는 크기를 초과하기 때문에 <xref:System.IdentityModel.Services.ChunkedCookieHandler?displayProperty=nameWithType>가 기본 쿠키 처리기입니다. 사용자 지정 쿠키 처리기를 대신 사용하는 경우 청크를 구현해야 합니다.  
  
 자세한 내용은 [ClaimsAwareWebFarm](https://go.microsoft.com/fwlink/?LinkID=248408) 샘플을 참조 하세요. 이 샘플에서는 큰 쿠키를 교환하는 대신 참조로 세션을 사용할 수 있도록 tokenreplycache와 비교해서 팜 준비 세션 캐시를 보여 줍니다. 또한 팜의 쿠키를 보호하는 보다 손쉬운 방법을 보여 줍니다. 세션 캐시는 WCF 기반입니다. 세션 보안과 관련해서 이 샘플은 MachineKey 기반의 쿠키 변환에 대한 WIF 4.5의 새로운 기능을 보여 줍니다. 이 기능은 web.config에 적절한 코드 조각을 붙여넣어 활성화할 수 있습니다. 샘플 자체는 “팜” 환경이 아니지만 팜에서 앱을 사용하는 데 필요한 사항을 보여 줍니다.
