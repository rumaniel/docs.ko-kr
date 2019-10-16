---
title: <cookieHandler>
ms.date: 03/30/2017
ms.assetid: bfdc127f-8d94-4566-8bef-f583c6ae7398
author: BrucePerlerMS
ms.openlocfilehash: 853dc9817d080e59ac7a792576eda862bd0b1f1d
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252034"
---
# <a name="cookiehandler"></a>\<cookieHandler>
(SAM <xref:System.IdentityModel.Services.CookieHandler> )에서 <xref:System.IdentityModel.Services.SessionAuthenticationModule> 쿠키를 읽고 쓰는 데 사용 하는를 구성 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<federationConfiguration >** ](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<cookieHandler >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler name=xs:string  
        path=Path  
        mode="Chunked||Custom||Default"  
        persistentSessionLifetime=xs:string  
        hideFromScript=xs:boolean  
        requireSSL=xs:boolean  
        domain=xs:string  
      <chunkedCookieHandler size=xs:int />  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|name|작성 된 모든 쿠키의 기본 이름을 지정 합니다. 기본값은 "FedAuth"입니다.|  
|path|작성 된 모든 쿠키에 대 한 경로 값을 지정 합니다. 기본값은 "HttpRuntime. AppDomainAppVirtualPath"입니다.|  
|모드|SAM에서 사용 하는 쿠키 처리기의 종류를 지정 하는 값중하나입니다.<xref:System.IdentityModel.Services.CookieHandlerMode> 다음 값을 사용할 수 있습니다.<br /><br /> -"Default"-"청크 분할"과 동일 합니다.<br />-"청크 분할"- <xref:System.IdentityModel.Services.ChunkedCookieHandler> 클래스의 인스턴스를 사용 합니다. 이 쿠키 처리기는 개별 쿠키가 설정 된 최대 크기를 초과 하지 않도록 합니다. 이는 잠재적으로 논리 쿠키 하나를 실시간으로 많은 쿠키에 "청크" 하 여이를 수행 합니다.<br />-"Custom" —에서 <xref:System.IdentityModel.Services.CookieHandler>파생 된 사용자 지정 클래스의 인스턴스를 사용 합니다. 파생 된 클래스는 `<customCookieHandler>` 자식 요소에서 참조 됩니다.<br /><br /> 기본값은 "Default"입니다.|  
|persistentSessionLifetime|영구적 세션의 수명을 지정 합니다. 0 이면 임시 세션이 항상 사용 됩니다. 기본값은 임시 세션을 지정 하는 "0:0:0"입니다. 최대값은 365 일의 세션을 지정 하는 "365:0:0"입니다. 값은 다음 제한 사항에 따라 지정 해야 합니다. `<xs:pattern value="([0-9.]+:){0,1}([0-9]+:){0,1}[0-9.]+" />`여기서 왼쪽 값은 일을 지정 하 고, 중간 값 (있는 경우)은 시간을 지정 하 고, 가장 오른쪽 값 (있는 경우)은 분을 지정 합니다.|  
|requireSsl|작성 된 모든 쿠키에 대해 "보안" 플래그를 내보낼지 여부를 지정 합니다. 이 값을 설정 하면 로그인 세션 쿠키는 HTTPS를 통해서만 사용할 수 있습니다. 기본값은 "true"입니다.|  
|hideFromScript|작성 된 쿠키에 대 한 "HttpOnly" 플래그는 내보내집니다 여부를 제어 합니다. 특정 웹 브라우저는 클라이언트 쪽 스크립트가 쿠키 값에 액세스 하지 못하도록 하 여이 플래그를 적용 합니다. 기본값은 "true"입니다.|  
|domain|작성 된 모든 쿠키에 대 한 도메인 값입니다. 기본값은 ""입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<chunkedCookieHandler>](chunkedcookiehandler.md)|를 <xref:System.IdentityModel.Services.ChunkedCookieHandler>구성 합니다. `mode` 요소의 특성이`<cookieHandler>` "Default" 또는 "청크 분할" 인 경우에만이 요소가 있을 수 있습니다.|  
|[\<customCookieHandler>](customcookiehandler.md)|사용자 지정 쿠키 처리기 형식을 설정 합니다. `mode` 요소의 특성이`<cookieHandler>` "Custom" 이면이 요소가 있어야 합니다. `mode` 특성의 다른 값에 대해서는 사용할 수 없습니다. 사용자 지정 형식은 <xref:System.IdentityModel.Services.CookieHandler> 클래스에서 파생 되어야 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<federationConfiguration>](federationconfiguration.md)|<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> (Wsfam) <xref:System.IdentityModel.Services.SessionAuthenticationModule> 및 (SAM)을 구성 하는 설정을 포함 합니다.|  
  
## <a name="remarks"></a>설명  
 는 <xref:System.IdentityModel.Services.CookieHandler> HTTP 프로토콜 수준에서 원시 쿠키를 읽고 쓰는 역할을 담당 합니다. <xref:System.IdentityModel.Services.ChunkedCookieHandler> 또는 클래스<xref:System.IdentityModel.Services.CookieHandler> 에서 파생 된 사용자 지정 쿠키 처리기를 구성할 수 있습니다.  
  
 청크 분할 된 쿠키 처리기를 구성 하려면 mode 특성을 "청크 분할" 또는 "기본값"으로 설정 합니다. 기본 청크 크기는 2000 바이트 이지만 선택적으로 자식 요소를 `<chunkedCookieHandler>` 포함 하 여 다른 청크 크기를 지정할 수 있습니다.  
  
 사용자 지정 쿠키 처리기를 구성 하려면 mode 특성을 "Custom"으로 설정 합니다. 또한 사용자 지정 처리기의 `<customCookieHandler>` 형식을 참조 하는 자식 요소를 지정 해야 합니다.  
  
 합니다 `<cookieHandler>` 에서 요소가 표시 되는 <xref:System.IdentityModel.Services.CookieHandlerElement> 클래스입니다. 구성에 지정 된 쿠키 처리기는 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration.CookieHandler%2A> <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType> 속성에 설정 된 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> 개체의 속성에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 XML에서는 요소를 `<cookieHandler>` 보여 줍니다. 이 예제에서는 `mode` 특성을 지정 하지 않았기 때문에 SAM에서 기본 쿠키 처리기를 사용 합니다. <xref:System.IdentityModel.Services.ChunkedCookieHandler> 클래스의 인스턴스입니다. `<chunkedCookieHandler>` 자식 요소가 지정 되지 않았기 때문에 기본 청크 크기가 사용 됩니다. `requireSsl` 특성이 설정`false`되었으므로 HTTPS가 필요 하지 않습니다.  
  
> [!WARNING]
> 이 예제에서는 세션 쿠키를 작성 하는 데 HTTPS가 필요 하지 않습니다. 이는 `requireSsl` `<cookieHandler>` 요소의 특성이로 `false`설정 되어 있기 때문입니다. 이 설정은 보안 위험을 초래할 수 있으므로 대부분의 프로덕션 환경에는 권장 되지 않습니다.  
  
```xml  
<cookieHandler requireSsl="false" />  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Services.CookieHandler>
- <xref:System.IdentityModel.Services.ChunkedCookieHandler>
- <xref:System.IdentityModel.Services.SessionAuthenticationModule>
