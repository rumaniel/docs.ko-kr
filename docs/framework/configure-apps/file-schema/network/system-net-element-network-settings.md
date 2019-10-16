---
title: <system.Net> 요소(네트워크 설정)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#system.Net
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.Net
helpviewer_keywords:
- system.Net element
- <system.Net> element
ms.assetid: 52de4d6c-b24d-44aa-ba7d-6b5061f1357e
ms.openlocfilehash: 810e942394c75c192e4423afe4c674ef3a2b9900
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697500"
---
# <a name="systemnet-element-network-settings"></a>\<system.Net> 요소(네트워크 설정)
.NET Framework의 네트워크 연결 방법을 지정하는 설정을 포함합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1 **@no__t -3system >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.net>   
</system.net>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[authenticationModules](authenticationmodules-element-network-settings.md)|인터넷 요청을 인증 하는 데 사용 되는 모듈을 지정 합니다.|  
|[connectionManagement](connectionmanagement-element-network-settings.md)|인터넷 호스트에 대 한 최대 연결 수를 지정 합니다.|  
|[defaultProxy](defaultproxy-element-network-settings.md)|HTTP(Hypertext Transfer Protocol) 프록시 서버를 구성합니다.|  
|[mailSettings](mailsettings-element-network-settings.md)|SMTP (Simple Mail Transport Protocol) 메일 전송 옵션을 구성 합니다.|  
|[requestCaching](requestcaching-element-network-settings.md)|네트워크 요청에 대 한 캐싱 메커니즘을 제어 합니다.|  
|[settings](settings-element-network-settings.md)|@No__t-0 및 관련 된 하위 네임 스페이스의 클래스에 대 한 기본 네트워크 옵션을 구성 합니다.|  
|[webRequestModules](webrequestmodules-element-network-settings.md)|인터넷 호스트의 정보를 요청 하는 데 사용할 모듈을 지정 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[configuration](../configuration-element.md)|모든 네임 스페이스에 대 한 설정을 포함 합니다.|  
  
## <a name="remarks"></a>설명  
 [@No__t -1system >](system-net-element-network-settings.md) 요소에는 <xref:System.Net> 및 관련 자식 네임 스페이스의 클래스에 대 한 설정이 포함 되어 있습니다. 설정은 인터넷 호스트에서 정보를 수신 하기 위한 인증 모듈, 연결 관리, 메일 설정, 프록시 서버 및 인터넷 요청 모듈을 구성 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Net> 클래스에서 사용 하는 일반적인 구성을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.net>  
    <authenticationModules>  
      <add type="System.Net.DigestClient" />  
      <add type="System.Net.NegotiateClient" />  
      <add type="System.Net.KerberosClient" />  
      <add type="System.Net.NtlmClient" />  
      <add type="System.Net.BasicClient" />  
    </authenticationModules>  
    <connectionManagement>  
      <add address="*" maxconnection="2" />  
    </connectionManagement>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        bypassonlocal="true"  
      />  
    </defaultProxy>  
    <webRequestModules>  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator"  
      />  
      <add prefix="https"  
           type="System.Net.HttpRequestCreator"  
      />  
      <add prefix="file"  
           type="System.Net.FileWebRequestCreator"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- [네트워크 설정 스키마](index.md)
