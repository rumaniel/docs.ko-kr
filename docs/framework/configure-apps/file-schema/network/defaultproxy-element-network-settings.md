---
title: '&lt;defaultProxy&gt; 요소 (네트워크 설정)'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultProxy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy
helpviewer_keywords:
- defaultProxy element
- <defaultProxy> element
ms.assetid: 9d663c4b-07b4-4f6f-9b12-efbd3630354f
ms.openlocfilehash: 54185c7cca734ced166fbe0a52b96214321d4469
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200511"
---
# <a name="ltdefaultproxygt-element-network-settings"></a>&lt;defaultProxy&gt; 요소 (네트워크 설정)
HTTP(Hypertext Transfer Protocol) 프록시 서버를 구성합니다.  
  
 \<configuration>  
\<system.net>  
\<defaultProxy >  
  
## <a name="syntax"></a>구문  
  
```xml  
      <defaultProxy  
        enabled="true|false"  
        useDefaultCredentials="true|false">  
           <bypasslist> … </bypasslist>  
           <proxy> … </proxy>  
           <module> … </module>  
      </defaultProxy>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|`enabled`|웹 프록시의 사용 여부를 지정합니다. 기본값은 `true`입니다.|  
|`useDefaultCredentials`|이 호스트에 대한 기본 자격 증명을 사용하여 웹 프록시에 액세스하는지 여부를 지정합니다. 기본값은 `false`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|프록시를 사용하지 않는 주소를 설명하는 정규식 집합을 제공합니다.|  
|[module](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md)|응용 프로그램에 새 프록시 모듈을 추가합니다.|  
|[프록시](../../../../../docs/framework/configure-apps/file-schema/network/proxy-element-network-settings.md)|프록시 서버를 정의합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[system.net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|.NET Framework의 네트워크 연결 방법을 지정하는 설정을 포함합니다.|  
  
## <a name="remarks"></a>설명  
 DefaultProxy 요소 비어 있으면 Internet Explorer의 프록시 설정이 사용됩니다. 이 동작은 .NET Framework 버전 1.1과 다릅니다.  
  
 경우 예외가 throw 됩니다 합니다 [모듈](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md) 요소는 public이 아닌 형식 지정, 형식에서 파생 하지 않거나는 <xref:System.Net.IWebProxy> 클래스를이 개체의 기본 생성자에서 예외가 발생 하거나 예외가 발생 했습니다 하는 동안 시스템 지정 기본 프록시를 검색합니다. 예외의 <xref:System.Exception.InnerException%2A> 속성에는 오류의 근본 원인에 대한 추가 정보가 있어야 합니다.  
  
## <a name="configuration-files"></a>구성 파일  
 이 요소는 응용 프로그램 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 Internet Explorer 프록시의 기본값을 사용 하 여 프록시 주소를 지정 하며 로컬 액세스 및 contoso.com에 대 한 프록시를 무시 합니다.  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
      <bypasslist>  
        <add address="[a-z]+\.contoso\.com$" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
- <xref:System.Net.WebProxy?displayProperty=nameWithType>  
- [네트워크 설정 스키마](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
