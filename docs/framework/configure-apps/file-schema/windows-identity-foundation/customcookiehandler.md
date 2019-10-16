---
title: <customCookieHandler>
ms.date: 03/30/2017
ms.assetid: a03b153d-5ec6-4915-9031-6f0c3fd348be
author: BrucePerlerMS
ms.openlocfilehash: e1f32e17cf0da5e948d778e8b61aca6053eff4ef
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252013"
---
# <a name="customcookiehandler"></a>\<customCookieHandler>
사용자 지정 쿠키 처리기 형식을 설정 합니다. 이 요소는 `mode` `<cookieHandler>` 요소의 특성이 "Custom" 인 경우에만 존재할 수 있습니다. 사용자 지정 형식은 <xref:System.IdentityModel.Services.CookieHandler> 클래스에서 파생 되어야 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<federationConfiguration >** ](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<cookieHandler >** ](cookiehandler.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<customCookieHandler >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode="Custom">  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" >  
      </customCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|type|<xref:System.IdentityModel.Services.CookieHandler> 클래스에서 파생 되는 사용자 지정 형식을 지정 합니다. `type` 특성을 지정 하는 방법에 대 한 자세한 내용은 [사용자 지정 형식 참조](../windows-workflow-foundation/index.md)를 참조 하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<cookieHandler>](cookiehandler.md)|<xref:System.IdentityModel.Services.CookieHandler> 에서<xref:System.IdentityModel.Services.SessionAuthenticationModule> 쿠키를 읽고 쓰는 데 사용 하는를 구성 합니다.|  
  
## <a name="remarks"></a>설명  
 요소의 특성을 "custom"으로 설정 `<customCookieHandler>` 하 여 사용자 지정 쿠키 처리기를 지정 하는 경우 쿠키 처리기 형식을 참조 하는 자식 요소를 포함 하 여 사용자 지정 쿠키 처리기의 형식을 지정 해야 합니다. `mode` `<cookieHandler>` `mode` 특성이 "청크 분할" 또는 "기본값"으로 설정 된 경우에는이 요소를 지정할 수 없습니다. 사용자 지정 쿠키 처리기는 <xref:System.IdentityModel.Services.CookieHandler> 클래스에서 파생 되어야 합니다.  
  
 합니다 `<customCookieHandler>` 에서 요소가 표시 되는 <xref:System.IdentityModel.Configuration.CustomTypeElement> 클래스입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 구성 형식의 사용자 지정 쿠키 처리기를 사용 하려면 SAM `MyNamespace.MyCustomCookieHandler`합니다.  
  
```xml  
<cookieHandler mode="Custom">  
    <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
</cookieHandler>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Services.CookieHandler>
