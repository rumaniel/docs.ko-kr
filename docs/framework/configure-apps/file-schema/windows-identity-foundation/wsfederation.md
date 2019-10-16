---
title: <wsFederation>
ms.date: 03/30/2017
ms.assetid: c537f770-68bd-4f82-96ad-6424ad91369f
author: BrucePerlerMS
ms.openlocfilehash: 0e3e33d5ba8c21738bdea11bd24a025d44919863
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251724"
---
# <a name="wsfederation"></a>\<wsFederation>
<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> (Wsfam)에 대 한 구성을 제공 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<federationConfiguration >** ](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<wsFederation >**  
  
## <a name="syntax"></a>구문  
  
```xml
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation authenticationType=xs:string (URI)  
                  freshness=xs:decimal  
                  homerealm=xs:string (URI)  
                  issuer=xs:string (URI)  
                  persistentCookiesOnPassiveRedirects=xs:boolean  
                  passiveRedirectEnabled=xs:boolean  
                  policy=xs:string (URI)  
                  realm=xs:string (URI)  
                  reply=xs:string (URI)  
                  request=xs:string (URI)  
                  requestPtr=xs:string (URI)  
                  requireHttps=xs:boolean  
                  resource=xs:string (URI)  
                  signInQueryString=xs:string  
                  signOutQueryString=xs:string  
                  signOutReply=xs:string (URL)  
    </wsFederation>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|authenticationType|인증 유형을 지정 하는 URI입니다. WS-FEDERATION 로그인 요청 wauth 매개 변수를 설정 합니다. 선택 사항입니다. 기본값은 빈 문자열로, wauth 매개 변수가 요청에 포함 되지 않도록 지정 합니다.|  
|고침|원하는 최대 기간 인증 요청 (분)입니다. Ws-federation 로그인 요청 wfresh 매개 변수를 설정합니다. 선택 사항입니다. 기본값은 0입니다. 선택 사항입니다. **경고:**  .NET Framework 4.5 `freshness` 의 다음 릴리스에서는 특성이 형식이 `xs:string` 되며 기본값 `null`은입니다.|  
|homeRealm|인증에 사용할 id 공급자 (IdP)의 홈 영역입니다. Ws-federation 로그인 요청 whr 매개 변수를 설정합니다. 선택 사항입니다. 기본값은 빈 문자열로, whr 매개 변수가 요청에 포함 되지 않도록 지정 합니다.|  
|issuer|의도 한 토큰 발급자의 URI입니다. WS-FEDERATION 로그인 요청 및 로그 아웃 요청에 대 한 기준 URL을 설정 합니다.|  
|persistentCookiesOnPassiveRedirects|인증 시 영구적 쿠키가 발급 되는지 여부를 지정 합니다. 선택 사항입니다. 기본값은 "false" 이며 쿠키가 발급 되지 않습니다.|  
|passiveRedirectEnabled|WSFAM이 인증 되지 않은 요청을 STS로 자동 리디렉션할 수 있는지 여부를 지정 합니다. 선택 사항입니다. 기본값은 "true" 이며 권한이 없는 요청은 자동으로 리디렉션됩니다.|  
|policy(정책)|로그인 요청에 사용할 관련 정책의 위치를 지정 하는 URL입니다. 기본값은 빈 문자열입니다. Ws-federation 로그인 요청 wp 매개 변수를 설정합니다. 선택 사항입니다. 기본값은 빈 문자열로, wp 매개 변수가 요청에 포함 되지 않도록 지정 합니다.|  
|realm|요청 영역에 대 한 URI입니다. (STS (보안 토큰 서비스)에 대 한 RP (신뢰 당사자)를 식별 하는 URI입니다. Wtrealm WS-FEDERATION 로그인 요청 매개 변수를 설정 합니다. 필수 요소.|  
|회신|RP(신뢰 당사자) 애플리케이션이 STS(보안 토큰 서비스)에서 응답을 받을 주소를 식별하는 URL입니다. WS-FEDERATION 로그인 요청 wreply 매개 변수를 설정 합니다. 선택 사항입니다. 기본값은 빈 문자열로, wreply 매개 변수가 요청에 포함 되지 않도록 지정 합니다.|  
|요청|토큰 발급 요청입니다. Ws-federation 로그인 요청 wreq 매개 변수를 설정합니다. 선택 사항입니다. 기본값은 빈 문자열로, wreq 매개 변수가 요청에 포함 되지 않도록 지정 합니다. 요청에 wreq 또는 wreqptr 매개 변수를 포함 하지 않으면 STS가 발급할 토큰의 종류를 알고 있음을 의미 합니다.|  
|requestPtr|토큰 발급 요청의 위치를 지정 하는 URL입니다. Request wreqptr 매개 변수를 설정 합니다. 선택 사항입니다. 기본값은 빈 문자열로, wreqptr 매개 변수가 요청에 포함 되지 않도록 지정 합니다. 요청에 wreq 또는 wreqptr 매개 변수를 포함 하지 않으면 STS가 발급할 토큰의 종류를 알고 있음을 의미 합니다.|  
|requireHttps|STS (보안 토큰 서비스)와의 통신에서 HTTPS 프로토콜을 사용 해야 하는지 여부를 지정 합니다. 선택 사항입니다. 기본값은 "true"이 고, HTTPS를 사용 해야 합니다.|  
|resource|에 액세스 하는 신뢰 당사자 (RP) 리소스를 식별 하는 URI는 보안 토큰 서비스 (STS). 선택 사항입니다. WS-FEDERATION 로그인 요청 wres 매개 변수를 설정 합니다. 선택 사항입니다. 기본값은 빈 문자열로, wres 매개 변수가 요청에 포함 되지 않도록 지정 합니다. **참고:** wres는 레거시 매개 변수입니다. 대신 wtrealm `realm` 매개 변수를 사용 하는 특성을 지정 합니다.|  
|signInQueryString|WS-FEDERATION 로그인 요청 URL에서 응용 프로그램 정의 쿼리 매개 변수를 지정 하기 위한 확장 지점을 제공 합니다. 선택 사항입니다. 기본값은 빈 문자열로, 요청에 추가 매개 변수를 포함 하지 않도록 지정 합니다. 매개 변수는 다음과 같은 형식을 `"param1=value1&param2=value2&param3=value3"` 사용 하 여 쿼리 문자열 조각으로 지정 됩니다. **참고:**  구성 파일에서 쿼리 문자열의 ' & ' 문자는 해당 엔터티 참조를 `&`사용 하 여 지정 해야 합니다.|  
|signOutQueryString|WS-FEDERATION 로그인 요청 URL에서 응용 프로그램 정의 쿼리 매개 변수를 지정 하기 위한 확장 지점을 제공 합니다. 선택 사항입니다. 기본값은 빈 문자열로, 요청에 추가 매개 변수를 포함 하지 않도록 지정 합니다. 매개 변수는 다음과 같은 형식을 `"param1=value1&param2=value2&param3=value3"` 사용 하 여 쿼리 문자열 조각으로 지정 됩니다. **참고:**  구성 파일에서 쿼리 문자열의 ' & ' 문자는 해당 엔터티 참조를 `&`사용 하 여 지정 해야 합니다.|  
|signOutReply|WS-FEDERATION 프로토콜을 통해 수동 로그 아웃 하는 동안 STS (보안 토큰 서비스)에서 클라이언트를 리디렉션해야 하는 URL을 지정 합니다. Ws-federation 로그 아웃 요청에 wreply 매개 변수를 설정합니다. 선택 사항입니다. 기본값은 빈 문자열로, 요청에 추가 매개 변수를 포함 하지 않도록 지정 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<federationConfiguration>](federationconfiguration.md)|<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> (Wsfam) <xref:System.IdentityModel.Services.SessionAuthenticationModule> 및 (SAM)을 구성 하는 설정을 포함 합니다.|  
  
## <a name="remarks"></a>설명  
 요소를 `<wsFederation>` 사용 하 여 기본 ws-federation 매개 변수 설정 및 wsfam의 기본 동작을 구성할 수 있습니다. 요소 아래에 `<wsFederation>` 정의 된 ws-federation 매개 변수 설정은 클래스에 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 의해 노출 되는 동등한 속성을 설정 합니다. 이러한 속성은 WSFAM에서 발행 한 모든 요청에 대해 동일 하 게 유지 됩니다. WSFAM에서 노출 하는 이벤트에 대 한 이벤트 처리기를 추가 하 여 요청을 처리 하는 동안 WS-FEDERATION 매개 변수를 동적으로 변경할 수 있습니다. 예를 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider> 들어 이벤트입니다. 자세한 내용은 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 클래스에 대 한 설명서를 참조 하세요.  
  
 합니다 `<wsFederation>` 에서 요소가 표시 되는 <xref:System.IdentityModel.Services.Configuration.WSFederationElement> 클래스입니다. 구성 개체 자체는 <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration> 클래스로 표현 됩니다. 단일 <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration> 인스턴스는 속성을 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType> 통해 액세스 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> 되는 개체에 대해 설정 되 고 wsfam에 대 한 구성을 제공 합니다.  
  
## <a name="example"></a>예제  
 다음 XML에서는 wsfam에 대 한 설정을 지정 하는 요소를 `<wsFederation>` 보여 줍니다.  
  
> [!WARNING]
> 이 예에서 WSFAM은 HTTPS를 사용 하는 데 필요 하지 않습니다. 이는 `requireHttps` `<wsFederation>` 요소의 특성이 설정 `false`되었기 때문입니다. 이 설정은 보안 위험을 초래할 수 있으므로 대부분의 프로덕션 환경에는 권장 되지 않습니다.  
  
```xml
<wsFederation passiveRedirectEnabled="true"   
              issuer="http://localhost:15839/wsFederationSTS/Issue"   
              realm="http://localhost:50969/"   
              reply="http://localhost:50969/"   
              requireHttps="false"   
              signOutReply="http://localhost:50969/SignedOutPage.html"   
              signOutQueryString="Param1=value2&Param2=value2"   
              persistentCookiesOnPassiveRedirects="true" />
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>
- <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType>
