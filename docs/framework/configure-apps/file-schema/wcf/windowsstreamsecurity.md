---
title: '&lt;windowsStreamSecurity&gt;'
ms.date: 03/30/2017
ms.assetid: 926bea29-90c7-4a26-9cf0-fb4aa44f6f70
ms.openlocfilehash: e117c30ba2583158ee21fd11ff4a38b094c18fd9
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197641"
---
# <a name="ltwindowsstreamsecuritygt"></a>&lt;windowsStreamSecurity&gt;
사용자 지정의 바인딩에 대한 Windows 스트림 보안 설정을 지정합니다.  
  
 \<system.serviceModel>  
\<바인딩 >  
\<customBinding>  
\<바인딩 >  
\<windowsStreamSecurity >  
  
## <a name="syntax"></a>구문  
  
```xml  
<windowsStreamSecurity protectionLevel="None/Sign/EncryptAndSign"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|protectionLevel|메시지 보안 수준을 정의합니다. 메시지 서명은 메시지 전송 과정에서 제3자가 메시지를 위조할 수 있는 위험을 줄입니다. 암호화는 전송 과정에서 데이터 수준의 개인 정보 보호를 제공합니다. 유효한 값은 다음과 같습니다.<br /><br /> -None: 보호 되지 않습니다.<br />-Sign: 메시지가 서명 됩니다.<br />-EncryptAndSign: 메시지가 서명 및 암호화 합니다.<br /><br /> 기본값은 EncryptAndSign입니다.<br /><br /> 이 특성은 <xref:System.Net.Security.ProtectionLevel> 형식입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../../../docs/framework/misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 TCP 및 명명된 파이프와 같은 스트림 지향 프로토콜을 사용하는 전송은 스트림 기반 전송 업그레이드를 지원합니다. 특히 WCF는 보안 업그레이드를 제공합니다. 이 전송 보안의 구성은이 구성 요소에 캡슐화 [ \<sslStreamSecurity >](../../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md), 구성 및 사용자 지정 바인딩에 추가할 수 있는  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Channels.CustomBinding>  
 <xref:System.ServiceModel.Configuration.WindowsStreamSecurityElement>  
 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
 [바인딩](../../../../../docs/framework/wcf/bindings.md)  
 [바인딩 확장](../../../../../docs/framework/wcf/extending/extending-bindings.md)  
 [사용자 지정 바인딩](../../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
