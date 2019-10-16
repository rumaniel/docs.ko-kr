---
title: <httpTransport>
ms.date: 03/30/2017
ms.assetid: 8b30c065-b32a-4fa3-8eb4-5537a9c6b897
ms.openlocfilehash: 51558a7f51ddeab4652abcc72376cb50a22c239b
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400367"
---
# <a name="httptransport"></a>\<httpTransport>
사용자 지정 바인딩의 SOAP 메시지 전송을 위한 HTTP 전송을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<httpTransport >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<httpTransport allowCookies="Boolean"
               authenticationScheme="Digest/Negotiate/Ntlm/Basic/Anonymous"
               bypassProxyOnLocal="Boolean"
               hostnameComparisonMode="StrongWildcard/Exact/WeakWildcard"
               keepAliveEnabled="Boolean"
               maxBufferSize="Integer"
               proxyAddress="Uri"
               proxyAuthenticationScheme="None/Digest/Negotiate/Ntlm/Basic/Anonymous"
               realm="String"
               transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
               unsafeConnectionNtlmAuthentication="Boolean"
               useDefaultWebProxy="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|allowCookies|클라이언트가 쿠키를 수락하고 이를 앞으로의 요청에서 전파할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 쿠키를 사용하는 ASMX 웹 서비스와 상호 작용할 때 이 특성을 사용할 수 있습니다. 그러면 서버에서 반환된 쿠키가 해당 서비스에 대한 이후의 모든 클라이언트 요청에 자동으로 복사되도록 할 수 있습니다.|  
|authenticationScheme|HTTP 수신기가 처리하는 클라이언트 요청을 인증하는 데 사용되는 프로토콜을 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> 이해할 다이제스트 인증을 지정합니다.<br />결정할 인증 체계를 결정 하는 클라이언트와 협상 합니다. 클라이언트와 서버 모두 Kerberos를 지원하면 이 인증 체계가 사용되고, 그렇지 않으면 NTLM이 사용됩니다.<br />-   Ntlm: NTLM 인증을 지정합니다.<br />기본 기본 인증을 지정합니다.<br />익명 익명 인증을 지정합니다.<br /><br /> 기본값은 Anonymous입니다. 이 특성은 <xref:System.Net.AuthenticationSchemes> 형식입니다. 이 특성은 한 번만 설정할 수 있습니다.|  
|bypassProxyOnLocal|로컬 주소에 대해 프록시 서버를 사용하지 않을 것인지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 로컬 주소는 로컬 LAN 또는 인트라넷에 있는 주소입니다.<br /><br /> 서비스 주소가로 시작 하 `http://localhost`는 경우 WCF (Windows Communication Foundation)는 항상 프록시를 무시 합니다.<br /><br /> 클라이언트가 동일한 시스템의 서비스와 통신할 때 프록시를 통하게 하려면 localhost 대신 호스트 이름을 사용해야 합니다.|  
|hostnameComparisonMode|URI 구문 분석에 사용되는 HTTP 호스트 이름 비교 모드를 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -StrongWildcard: ("+")는 지정 된 체계, 포트 및 상대 URI의 컨텍스트에서 가능한 모든 호스트 이름을 검색 합니다.<br />-Exact: 와일드 카드 없음<br />-WeakWildcard: ("\*")는 지정 된 체계, 포트 및 상대 uir (명시적으로 또는 강력한 와일드 카드 메커니즘을 통해 일치 하지 않는)의 컨텍스트에서 가능한 모든 호스트 이름과 일치 합니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.HostNameComparisonMode> 형식입니다. 기본값은 <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>입니다.|  
|keepAliveEnabled|인터넷 리소스에 영구 연결을 할 것인지 여부를 지정하는 부울 값입니다.|  
|maxBufferSize|버퍼의 최대 크기를 지정하는 양의 정수입니다. 기본값은 524288입니다.|  
|proxyAddress|HTTP 프록시의 주소를 지정하는 URI입니다. `useSystemWebProxy`가 `true`일 경우 이 설정은 `null`이어야 합니다. 기본값은 `null`입니다.|  
|proxyAuthenticationScheme|HTTP 프록시가 처리하는 클라이언트 요청을 인증하는 데 사용되는 프로토콜을 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> 없음을 인증 없이 수행 됩니다.<br />이해할 다이제스트 인증을 지정합니다.<br />결정할 인증 체계를 결정 하는 클라이언트와 협상 합니다. 클라이언트와 서버 모두 Kerberos를 지원하면 이 인증 체계가 사용되고, 그렇지 않으면 NTLM이 사용됩니다.<br />-   Ntlm: NTLM 인증을 지정합니다.<br />기본 기본 인증을 지정합니다.<br />익명 익명 인증을 지정합니다.<br /><br /> 기본값은 Anonymous입니다. 이 특성은 <xref:System.Net.AuthenticationSchemes> 형식입니다. <xref:System.Net.AuthenticationSchemes.IntegratedWindowsAuthentication?displayProperty=nameWithType> 은 지원 되지 않습니다.|  
|realm|프록시/서버에서 사용할 영역을 지정하는 문자열입니다. 기본값은 빈 문자열입니다.<br /><br /> 서버에서는 보호되는 리소스를 분할할 때 영역을 사용합니다. 각 파티션에는 자체 인증 체계 및/또는 권한 부여 데이터베이스가 있을 수 있습니다. 영역은 기본 및 다이제스트 인증에만 사용됩니다. 클라이언트가 성공적으로 인증되면 이 인증은 지정된 영역의 모든 리소스에 대해 유효합니다. 영역에 대 한 자세한 설명은 [IETF 웹 사이트](https://www.ietf.org)에서 RFC 2617을 참조 하세요.|  
|transferMode|메시지가 버퍼링되거나 스트리밍되는지 또는 요청이나 응답인지를 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> 그래픽 요청 및 응답 메시지는 버퍼링 됩니다.<br />브라우저로 요청 및 응답 메시지가 스트리밍됩니다.<br />-   StreamedRequest: 요청 메시지는 스트리밍되고 응답 메시지는 버퍼링됩니다.<br />StreamedResponse 요청 메시지는 버퍼링되고 응답 메시지는 스트리밍됩니다.<br /><br /> 기본값은 Buffered입니다. 이 특성은 <xref:System.ServiceModel.TransferMode> 형식입니다.|  
|unsafeConnectionNtlmAuthentication|서버에서 안전하지 않은 연결 공유를 사용할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다. 사용할 경우 각 TCP 연결에서 NTLM 인증이 한 번씩 수행됩니다.|  
|useDefaultWebProxy|사용자별 설정이 아닌 시스템 수준의 프록시 설정을 사용할지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 `httpTransport` 요소는 HTTP 전송 프로토콜을 구현하는 사용자 지정 바인딩을 만들기 위한 시작점입니다. HTTP는 상호 운용성을 위해 사용되는 기본 전송입니다. 이 전송은 wcf (Windows Communication Foundation)에서 지원 되므로 WCF가 아닌 다른 웹 서비스 스택과의 상호 운용성을 보장 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.HttpTransportElement>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [전송](../../../wcf/feature-details/transports.md)
- [전송 선택](../../../wcf/feature-details/choosing-a-transport.md)
- [바인딩](../../../wcf/bindings.md)
- [바인딩 확장](../../../wcf/extending/extending-bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
