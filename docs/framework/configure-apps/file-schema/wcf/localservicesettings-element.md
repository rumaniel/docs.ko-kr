---
title: <localServiceSettings> 요소
ms.date: 03/30/2017
ms.assetid: 0658549c-3f65-46dd-8c5c-9895441ed734
ms.openlocfilehash: 4883fd563ecf989d67c369085df4fc43d0c5f078
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400312"
---
# <a name="localservicesettings-element"></a>\<localServiceSettings > 요소
이 바인딩에 대한 로컬 서비스의 보안 설정을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<보안 >** ](security-of-custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<localServiceSettings >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<security>
  <localServiceSettings detectReplays="Boolean"
                        inactivityTimeout="TimeSpan"
                        issuedCookieLifeTime="TimeSpan"
                        maxCachedCookies="Integer"
                        maxClockSkew="TimeSpan"
                        maxPendingSessions="Integer"
                        maxStatefulNegotiations="Integer"
                        negotiationTimeout="TimeSpan"
                        reconnectTransportOnFailure="Boolean"
                        replayCacheSize="Integer"
                        replayWindow="TimeSpan"
                        sessionKeyRenewalInterval="TimeSpan"
                        sessionKeyRolloverInterval="TimeSpan"
                        timestampValidityDuration="TimeSpan" />
</security>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`detectReplays`|채널에 대한 재생 공격이 검색되어 자동으로 처리되는지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.|  
|`inactivityTimeout`|채널에서 제한 시간이 초과되기 전에 대기하는 비활성 기간을 지정하는 <xref:System.TimeSpan>(양수)입니다. 기본값은 "01:00:00"입니다.|  
|`issuedCookieLifeTime`|새로운 모든 보안 쿠키에 발급되는 수명을 지정하는 <xref:System.TimeSpan>입니다. 수명이 지난 쿠키는 재활용되며 다시 협상되어야 합니다. 기본값은 "10:00:00"입니다.|  
|`maxCachedCookies`|캐시할 수 있는 최대 쿠키 수를 지정하는 양의 정수입니다. 기본값은 1000입니다.|  
|`maxClockSkew`|서로 통신하는 양쪽의 시스템 클록 간의 최대 시간 차이를 지정하는 <xref:System.TimeSpan>입니다. 기본값은 "00:05:00"입니다.<br /><br /> 이 값을 기본값으로 설정하면 수신자는 메시지를 받은 시간을 기준으로 보낸 시간 타임스탬프가 전후 5분 이내인 메시지를 수신 허용합니다. 보낸 시간 테스트를 통과하지 못한 메시지는 거부됩니다. 이 설정은 `replayWindow` 특성과 함께 사용됩니다.|  
|`maxPendingSessions`|서비스에서 지원하는 보류 중인 보안 세션의 최대 수를 지정하는 양의 정수입니다. 이 한도에 도달하면 모든 새 클라이언트가 SOAP 오류를 받습니다. 기본값은 1000입니다.|  
|`maxStatefulNegotiations`|동시에 활성 상태를 유지할 수 있는 보안 협상 수를 지정하는 양의 정수입니다. 한도를 초과하는 협상 세션은 큐에 대기되며 한도 아래로 떨어져야 완료될 수 있습니다. 기본값은 1024입니다.|  
|`negotiationTimeout`|채널에서 사용하는 보안 정책의 수명을 지정하는 <xref:System.TimeSpan>입니다. 시간이 만료되면 채널이 새로운 보안 정책에 대해 클라이언트와 재협상합니다. 기본값은 "00:02:00"입니다.|  
|`reconnectTransportOnFailure`|WS-Reliable Messaging을 사용하는 연결에서 전송 실패 후 다시 연결을 시도할지 여부를 지정하는 부울 값입니다. 기본값은 `true`로, 다시 연결이 무한히 시도된다는 의미입니다. 이 순환은 비활성 제한 시간이 초과되어야만 중단되며, 이 경우 채널에서 다시 연결할 수 없으면 예외가 throw됩니다.|  
|`replayCacheSize`|재생 검색에 사용되는 캐시된 Nonce의 수를 지정하는 양의 정수입니다. 이 제한을 초과하면 가장 오래된 Nonce가 제거되고 새 메시지에 대해 새로운 Nonce가 만들어집니다. 기본값은 500000입니다.|  
|`replayWindow`|개별 메시지 Nonce의 유효 기간을 지정하는 <xref:System.TimeSpan>입니다.<br /><br /> 이 속성에서 지정한 시간이 지나면 이전에 보낸 메시지와 동일한 Nonce를 갖는 메시지는 허용되지 않습니다. 이 특성은 `maxClockSkew` 특성과 함께 사용되어 재생 공격을 방지합니다. 메시지 재생 창이 만료된 후에 공격자가 그 메시지를 재생할 수 있습니다. 그러나 이 메시지는 `maxClockSkew` 테스트를 통과하지 못합니다. 해당 테스트는 메시지의 보낸 시간 타임스탬프가 메시지를 받은 시간보다 지정된 시간 이상으로 늦거나 빠르면 그 메시지를 거부합니다.|  
|`sessionKeyRenewalInterval`|개시자가 보안 세션을 위해 키를 갱신하는 시간 간격을 지정하는 <xref:System.TimeSpan>입니다. 기본값은 "10:00:00"입니다.|  
|`sessionKeyRolloverInterval`|키 갱신 중에 들어오는 메시지에서 이전 세션 키를 사용할 수 있는 시간 간격을 지정하는 <xref:System.TimeSpan>입니다. 기본값은 "00:05:00"입니다.<br /><br /> 키 갱신 중에 클라이언트와 서버는 반드시 사용 가능한 최신 키를 사용하여 메시지를 보내야 합니다. 양쪽 모두 롤오버 시간이 만료될 때까지는 이전 세션 키를 사용하여 보안되는 메시지를 수락할 수 있습니다.|  
|`timestampValidityDuration`|타임스탬프의 유효 기간을 지정하는 <xref:System.TimeSpan>(양수)입니다. 기본값은 "00:15:00"입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](security-of-custombinding.md)|사용자 지정 바인딩에 대한 보안 옵션을 지정합니다.|  
|[\<secureConversationBootstrap>](secureconversationbootstrap.md)|보안 대화 서비스 개시에 사용되는 기본값을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 이 설정은 서비스 보안 정책의 일부로 게시되지 않고 클라이언트의 바인딩에 영향을 주지 않으므로 로컬 속성에 속합니다.  
  
 `localServiceSecuritySettings` 요소의 다음 특성을 사용하면 DOS(서비스 거부) 보안 공격을 줄일 수 있습니다.  
  
- `maxCachedCookies`: SPNEGO 또는 SSL 협상 후에 서버에서 캐시하는 시간 제한 SecurityContextToken의 최대 개수를 제어합니다.  
  
- `issuedCookieLifetime`: SPNEGO 또는 SSL 협상 후에 서버에서 발급하는 SecurityContextToken의 수명을 제어합니다. 서버는 이 기간 동안 SecurityContextToken을 캐시합니다.  
  
- `maxPendingSessions`: 서버에서 설정되었지만 애플리케이션 메시지가 처리되지 않은 보안 대화의 최대 개수를 제어합니다. 이 할당량은 클라이언트가 서비스에서 보안 대화를 설정할 수 없도록 하고 서비스에서 각 클라이언트의 상태를 유지 관리하게 하지만 사용하지는 않습니다.  
  
- `inactivityTimeout`: 애플리케이션 메시지가 수신되지 않을 때 서비스에서 보안 대화를 활성 상태로 유지하는 최대 시간을 제어합니다. 이 할당량은 클라이언트가 서비스에서 보안 대화를 설정할 수 없도록 하고 서비스에서 각 클라이언트의 상태를 유지 관리하게 하지만 사용하지는 않습니다.  
  
 보안 대화 세션에서 바인딩의 `inactivityTimeout` 및 `receiveTimeout` 특성은 모두 세션 시간 제한에 영향을 줍니다. 제한 시간은 두 속성 값 중 짧은 시간으로 결정됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.LocalServiceSettings%2A>
- <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A>
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [바인딩](../../../wcf/bindings.md)
- [바인딩 확장](../../../wcf/extending/extending-bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [방법: SecurityBindingElement를 사용 하 여 사용자 지정 바인딩 만들기](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [사용자 지정 바인딩 보안](../../../wcf/samples/custom-binding-security.md)
