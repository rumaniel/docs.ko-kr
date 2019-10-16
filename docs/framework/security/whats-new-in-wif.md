---
title: Windows Identity Foundation 4.5의 새로운 기능
ms.date: 03/30/2017
ms.assetid: 3b381f04-593b-471f-bd33-0362be1aade5
author: BrucePerlerMS
ms.openlocfilehash: 93631c1171f81ec8b8d94b56a56012343f6c3220
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045277"
---
# <a name="whats-new-in-windows-identity-foundation-45"></a>Windows Identity Foundation 4.5의 새로운 기능
독립 실행형 다운로드로 제공되는 WIF(Windows Identity Foundation)의 첫 번째 버전은 .NET 3.5 SP1 기간에 도입되었기 때문에 WIF 3.5로 알려져 있습니다. .NET 4.5부터는 WIF가 .NET Framework의 일부로 제공됩니다. WIF 클래스를 프레임워크에서 직접 사용할 수 있도록 하면 .NET에 클레임 기반 ID를 더욱 심층적으로 통합하여 클레임을 더욱 쉽게 사용하도록 할 수 있습니다. 새 모델을 이용하기 위해 WIF 3.5용으로 작성된 애플리케이션을 수정할 필요가 있습니다. 자세한 내용은 [WIF 3.5를 사용하여 빌드된 애플리케이션을 WIF 4.5로 마이그레이션하는 지침](guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)을 참조하세요.  
  
 아래에서 몇 가지 주요 변경 사항에 대한 정보를 확인할 수 있습니다.  
  
## <a name="wif-is-now-part-of-the-net-framework"></a>WIF는 현재 .NET Framework의 일부로 제공됩니다.  
 WIF 클래스는 현재 여러 어셈블리에서 분산되어 있는데, `mscorlib`, `System.IdentityModel`, `System.IdentityModel.Services` 및 `System.ServiceModel`이 주요 클래스입니다. 마찬가지로, WIF 클래스는 <xref:System.Security.Claims?displayProperty=nameWithType>, 여러 가지 [System.IdentityModel](https://go.microsoft.com/fwlink/?LinkId=272004) 네임스페이스 및 <xref:System.ServiceModel.Security?displayProperty=nameWithType>와 같은 여러 네임스페이스에 분산되어 있습니다. <xref:System.Security.Claims?displayProperty=nameWithType> 네임스페이스에는 새로운 <xref:System.Security.Claims.ClaimsPrincipal> 및 <xref:System.Security.Claims.ClaimsIdentity> 클래스가 포함됩니다(아래 참조). .NET의 모든 보안 주체는 이제 <xref:System.Security.Claims.ClaimsPrincipal>에서 파생됩니다. WIF 네임스페이스와 이런 네임스페이스에 포함되는 클래스의 종류에 대한 자세한 내용은 [WIF API 참조](wif-api-reference.md)를 참조하세요. 네임스페이스가 WIF 3.5와 WIF 4.5 사이에서 매핑하는 방식에 대한 자세한 내용은 [WIF 3.5와 WIF 4.5 간의 네임스페이스 매핑](namespace-mapping-between-wif-3-5-and-wif-4-5.md)을 참조하세요.  
  
## <a name="new-claims-model-and-principal-object"></a>새 클레임 모델 및 보안 주체 개체  
 클레임은 .NET Framework 4.5에서 가장 중요한 핵심입니다. 기본 클레임 클래스(<xref:System.Security.Claims.Claim>, <xref:System.Security.Claims.ClaimsIdentity>, <xref:System.Security.Claims.ClaimsPrincipal>, <xref:System.Security.Claims.ClaimTypes>, <xref:System.Security.Claims.ClaimValueTypes>)는 모두 `mscorlib` 네임스페이스의 <xref:System.Security.Claims?displayProperty=nameWithType>에 있습니다. 클레임을 .NET ID 시스템에 플러그 인하기 위해 더 이상 인터페이스를 사용할 필요가 없습니다. <xref:System.Security.Principal.WindowsPrincipal>, <xref:System.Security.Principal.GenericPrincipal> 및 <xref:System.Web.Security.RolePrincipal>은 <xref:System.Security.Claims.ClaimsPrincipal>에서 상속하고, <xref:System.Security.Principal.WindowsIdentity>, <xref:System.Security.Principal.GenericIdentity> 및 <xref:System.Web.Security.FormsIdentity>는 <xref:System.Security.Claims.ClaimsIdentity>에서 상속합니다. 즉, 이제는 모든 보안 주체 클래스가 클레임을 제공합니다. 따라서 WIF 3.5 통합 클래스 및 인터페이스(`WindowsClaimsIdentity`, `WindowsClaimsPrincipal`, `IClaimsPrincipal`, `IClaimsIdentity`)가 제거되었습니다. 그 밖에도, <xref:System.Security.Claims.ClaimsIdentity> 클래스는 이제 메서드를 노출하므로 ID의 클레임 컬렉션을 더 쉽게 쿼리할 수 있습니다.  
  
## <a name="changes-to-the-wif-45-visual-studio-experience"></a>WIF 4.5 Visual Studio 환경의 변경 사항  
  
- **STS 참조 추가...** Visual Studio 기능(명령줄 유틸리티 FedUtil)이 더 이상 존재하지 않습니다. 대신 새로운 Visual Studio 확장명 기능인 **Visual Studio 2012용 ID 및 액세스 도구**를 사용할 수 있습니다. 이렇게 하면 기존 STS와 연합하거나 LocalSTS를 사용하여 솔루션을 테스트할 수 있습니다. 확장명 기능을 설치한 후, 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **ID 및 액세스**를 찾을 수 있습니다.  
  
- ASP.Net, 웹 사이트 및 WCF에 대한 기존 프로젝트 템플릿에서 바로 클레임을 사용할 수 있으므로 ASP.NET 및 STS 템플릿은 더 이상 제공되지 않습니다.  
  
- `Microsoft.IdentityModel.Web.Controls` 네임스페이스의 컨트롤(`SignInControl`, `FederatedPassiveSignInControl`, `FederatedPassiveSignInStatus`)은 WIF 4.5로 이전되지 않습니다.  
  
## <a name="changes-to-the-wif-45-api"></a>WIF 4.5 API에 대한 변경 사항  
  
- 일반적으로, 클레임 관련 클래스는 <xref:System.Security.Claims?displayProperty=nameWithType> 네임스페이스에 있고, WCF 관련 클래스(WS-Trust 시나리오에 사용되는 서비스 계약, 채널, 채널 팩터리 및 서비스 호스트)는 <xref:System.ServiceModel.Security?displayProperty=nameWithType>에 있고, 다른 모든 WIF 클래스는 다양한 [System.IdentityModel](https://go.microsoft.com/fwlink/?LinkId=272004) 네임스페이스에 분산되어 있는데, 예를 들어 여기에는 WS-* 및 SAML 아티팩트를 표시하는 클래스, 토큰 처리기 및 관련 클래스, WS-페더레이션 시나리오에 사용되는 클래스가 포함됩니다. 자세한 내용은 [WIF 3.5와 WIF 4.5 간의 네임스페이스 매핑](namespace-mapping-between-wif-3-5-and-wif-4-5.md) 및 [WIF API 참조](wif-api-reference.md)를 참조하세요.  
  
- 웹 팜 시나리오에 대한 세션 쿠키에서 사용하기 위해 컴퓨터 키가 활성화되었습니다. 자세한 내용은 [WIF 및 웹 팜](wif-and-web-farms.md)을 참조하세요.  
  
- 이제 [\<system.identityModel>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 및 [\<system.identityModel.services>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 요소 아래에서 WIF를 선언적으로 구성합니다. WIF 구성에 대한 자세한 내용은 [WIF 구성 참조](wif-configuration-reference.md)를 참조하세요.  
  
## <a name="other-notable-net-changes-or-features-that-are-caused-by-the-integration-of-wif-into-net"></a>WIF를 .NET으로 통합함으로써 발생하는 다른 주목할 만한 .NET 변경 사항 또는 특징  
  
- 이제는 클레임 기반 권한 부여(CBAC)를 수행할 가능성이 .NET Framework에 필수적인 사항이 되었습니다. <xref:System.Security.Claims.ClaimsAuthorizationManager> 개체를 구성한 다음, <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> 및 <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> 클래스를 사용하여 코드에서 명령적 및 선언적 액세스 검사를 수행할 수 있습니다. CBAC는 기존의 역할 기반 액세스 검사(RBAC)보다 더 향상된 유연성과 세분성을 제공합니다. 비즈니스 논리는 특정 클레임 또는 클레임 집합에 대한 액세스 검사를 기초로 할 수 있고 그와 같은 클레임에 대한 권한 부여 정책을 [\<claimsAuthorizationManager>](../configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md) 요소 아래에서 선언적으로 구성할 수 있기 때문에 비즈니스 논리에서 권한 부여 정책을 더욱 세분화할 수도 있습니다.  
  
## <a name="wcf-changes-as-a-result-of-wif-integration"></a>WIF 통합의 결과로서 발생하는 WCF 변경 사항:  
  
- WCF 클레임 기반 ID 모델은 WIF로 대체됩니다. 이는 WIF 클래스를 사용하는 데 유리하도록 <xref:System.IdentityModel.Claims?displayProperty=nameWithType>, <xref:System.IdentityModel.Policy?displayProperty=nameWithType> 및 <xref:System.IdentityModel.Selectors?displayProperty=nameWithType> 네임스페이스의 클래스를 삭제해야 한다는 의미입니다.  
  
- 다음 XML에서처럼 `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>` 요소에 대해 `useIdentityConfiguration` 특성을 지정하여 WCF 서비스에서 WIF가 사용됩니다.  
  
    ```xml  
    <serviceCredentials useIdentityConfiguration="true">  
        <!--Certificate added by Identity And Access VS Package.  Subject='CN=localhost', Issuer='CN=localhost'. Make sure you have this certificate installed. The Identity and Access tool does not install this certificate.-->  
        <serviceCertificate findValue="CN=localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName" />  
    </serviceCredentials>  
    ```  
  
     **Visual Studio 2012용 ID 및 액세스 도구**(위의 **Visual Studio 환경의 변경 사항** 참조)를 사용할 때, 이 도구는 `useIdentityConfiguration` 특성 집합을 포함한 `<serviceCredentials>` 요소를 자동으로 구성 파일에 추가합니다. 또한, WIF 구성 설정을 포함한 해당 [\<system.identityModel>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 요소를 추가하고 선택한 STS에 대한 인증을 아웃소싱하는 데 필요한 다른 설정과 바인딩을 추가합니다.  
  
## <a name="see-also"></a>참고자료

- [WIF 3.5를 사용하여 빌드된 응용 프로그램을 WIF 4.5로 마이그레이션하는 지침](guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)
- [WIF 3.5와 WIF 4.5 간의 네임스페이스 매핑](namespace-mapping-between-wif-3-5-and-wif-4-5.md)
- [WIF API 참조](wif-api-reference.md)
- [WIF 구성 참조](wif-configuration-reference.md)
