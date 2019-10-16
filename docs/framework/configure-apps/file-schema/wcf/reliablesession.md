---
title: <reliableSession>
ms.date: 03/30/2017
ms.assetid: 129b4a59-37f0-4030-b664-03795d257d29
ms.openlocfilehash: ef9416b2031bd457322b33dfa491d3fae766bf8c
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400005"
---
# <a name="reliablesession"></a>\<reliableSession>
WS-Reliable Messaging 설정을 정의합니다. 이 요소가 사용자 지정 바인딩에 추가되면 그 결과로 만들어지는 채널에서 EOD(Exactly-Once Delivery) 보증을 지원할 수 있습니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<reliableSession >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<reliableSession acknowledgementInterval="TimeSpan"
                 flowControlEnabled="Boolean"
                 inactivityTimeout="TimeSpan"
                 maxPendingChannels="Integer"
                 maxRetryCount="Integer"
                 maxTransferWindowSize="Integer"
                 reliableMessagingVersion="Default/WSReliableMessagingFebruary2005/WSReliableMessaging11"
                 ordered="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|acknowledgementInterval|채널이 해당 시점까지 받은 메시지에 대한 승인을 보내기 위해 대기하는 최대 시간 간격이 포함된 <xref:System.TimeSpan>입니다. 기본값은 00:00:0.2입니다.|  
|flowControlEnabled|WS-Reliable Messaging에 대한 Microsoft 고유의 흐름 제어 구현인 고급 흐름 제어를 활성화할지 여부를 나타내는 부울 값입니다. 기본값은 `true`입니다.|  
|InactivityTimeout|통신 상대방이 메시지를 보내지 않아도 채널에서 오류가 발생하지 않는 최대 기간을 지정하는 <xref:System.TimeSpan>입니다. 기본값은 00:10:00입니다.<br /><br /> 채널에서는 응용 프로그램 또는 인프라 메시지를 받는 작업이 이루어집니다. 이 속성은 비활성 세션을 유지하는 최대 시간을 제어합니다. 아무런 작업 없이 이 시간이 초과되면 인프라에서 해당 세션을 중단하며 채널에 오류가 발생합니다. **참고:**  응용 프로그램에서 연결을 유지하기 위해 정기적으로 메시지를 보낼 필요는 없습니다.|  
|maxPendingChannels|수신기에서 수락 대기할 수 있는 최대 채널 수를 지정하는 정수입니다. 이 값은 1 이상 16384 이하여야 합니다. 기본값은 4입니다.<br /><br /> 수락 대기 중인 채널은 보류됩니다. 최대 채널 수에 도달하면 채널이 만들어지지 않습니다. 대신 대기 중인 채널을 수락함으로써 채널 수가 줄어들 때까지 대기 중 모드를 유지합니다. 이것은 팩터리당 제한입니다.<br /><br /> 임계값에 도달하여 원격 애플리케이션이 신뢰할 수 있는 새 세션을 설정하려고 하면 요청이 거부되고 열기 작업에 이 오류가 표시됩니다. 이러한 제한은 보류 중인 보내는 채널 수에는 적용되지 않습니다.|  
|maxRetryCount|신뢰할 수 있는 채널이 기본 채널에서 Send를 호출하여 아직 승인을 받지 않은 메시지를 다시 전송하기 위해 시도할 수 있는 최대 횟수를 지정하는 정수입니다.<br /><br /> 이 값은 0보다 커야 합니다. 기본값은 8입니다.<br /><br /> 이 값은 0보다 큰 정수여야 합니다. 마지막 재전송 이후 승인을 받지 못한 경우 채널에 오류가 발생합니다.<br /><br /> 받는 사람이 메시지 배달을 승인했으면 메시지가 전송된 것으로 간주됩니다.<br /><br /> 전송된 메시지가 일정 시간 내에 승인을 받지 못하면 인프라에서 자동으로 메시지를 다시 전송합니다. 인프라는 이 속성에 지정된 횟수만큼 메시지를 다시 보내려고 합니다. 마지막 재전송 이후 승인을 받지 못한 경우 채널에 오류가 발생합니다.<br /><br /> 인프라는 지수 백오프 알고리즘을 사용하여 계산된 평균 라운드트립 시간에 따라 재전송 시간을 결정합니다. 처음에 시간은 재전송 1초 전에 시작되고 재전송 시도마다 두 배씩 지연되어, 결과적으로 첫 번째 전송 시도와 마지막 전송 시도 간에 약 8.5분이 지나게 됩니다. 첫 번째 재전송 시도는 계산된 라운드트립 시간에 따라 조정되고 결과적으로 재전송 시도에 따라 늘어나는 시간이 달라집니다. 따라서 재전송 시간을 다양한 네트워크 조건에 맞게 동적으로 적용할 수 있습니다.|  
|maxTransferWindowSize|버퍼의 최대 크기를 지정하는 정수입니다. 유효한 값은 1부터 4096까지입니다.<br /><br /> 클라이언트에서 이 특성은 수신자가 승인하지 않은 메시지를 저장하기 위해 신뢰할 수 있는 채널에서 사용하는 최대 버퍼 크기를 정의합니다. 할당량 단위는 메시지입니다. 버퍼가 꽉 차면 더 이상의 보내기 작업은 차단됩니다.<br /><br /> 수신자에서 이 특성은 응용 프로그램으로 발송되지 않은 들어오는 메시지를 저장하기 위해 채널에서 사용하는 최대 버퍼 크기를 정의합니다. 버퍼가 꽉 차면 그 이상의 메시지는 수신자에 의해 삭제되고 클라이언트가 다시 전송해야 합니다.|  
|ordered|전송된 순서대로 메시지 도착을 보장할지 여부를 지정하는 부울 값입니다. 이 설정이 `false`일 경우 메시지가 순서와 관계없이 도착할 수 있습니다. 기본값은 `true`입니다.|  
|reliableMessagingVersion|사용할 WS-ReliableMessaging 버전을 지정하는 <xref:System.ServiceModel.ReliableMessagingVersion>의 유효한 값입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 신뢰할 수 있는 세션은 신뢰할 수 있는 메시징 및 세션 기능을 제공합니다. 신뢰할 수 있는 메시징 기능은 실패 시 통신을 다시 시도하고 메시지 차례로 도착과 같은 배달 보증을 지정할 수 있게 합니다. 세션은 호출 간에 클라이언트의 상태를 유지합니다. 이 요소는 메시지를 순서대로 배달하는 기능을 선택적으로도 제공합니다. 이 구현된 세션은 SOAP 매개자 및 전송 매개자에 적용될 수 있습니다.  
  
 각 바인딩 요소는 메시지를 보내거나 받을 때의 처리 단계를 나타냅니다. 런타임에 바인딩 요소는 메시지를 주고 받는 데 필요한 나가는 채널 스택과 들어오는 채널 스택을 작성하기 위한 채널 팩터리 및 채널 수신기를 생성합니다. `reliableSession`는 끝점 간에 신뢰할 수 있는 세션을 설정하고 이 세션의 동작을 구성할 수 있는 선택적 계층을 스택에 제공합니다.  
  
 자세한 내용은 [신뢰할 수 있는 세션](../../../wcf/feature-details/reliable-sessions.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 다양한 전송 및 메시지 인코딩 요소, 특히 신뢰할 수 있는 세션 사용 등을 통해 사용자 지정 바인딩을 구성하는 방법을 보여 줍니다. 이렇게 하면 클라이언트 상태가 유지되며 차례로 배달 보증이 지정됩니다. 이 기능은 클라이언트 및 서비스의 응용 프로그램 구성 파일에서 구성됩니다. 예제에서는 서비스 구성을 보여 줍니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <!-- This endpoint is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc -->
        <!-- specify customBinding binding and a binding configuration to use -->
        <endpoint address=""
                  binding="customBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- The mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex -->
        <endpoint address="mex"
                  binding="mexHttpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>
    <!-- custom binding configuration - configures HTTP transport, reliable sessions -->
    <bindings>
      <customBinding>
        <binding name="Binding1">
          <reliableSession />
          <security authenticationMode="SecureConversation"
                    requireSecurityContextCancellation="true">
          </security>
          <compositeDuplex />
          <oneWay />
          <textMessageEncoding messageVersion="Soap12WSAddressing10"
                               writeEncoding="utf-8" />
          <httpTransport authenticationScheme="Anonymous"
                         bypassProxyOnLocal="false"
                         hostNameComparisonMode="StrongWildcard"
                         proxyAuthenticationScheme="Anonymous"
                         realm=""
                         useDefaultWebProxy="true" />
        </binding>
      </customBinding>
    </bindings>
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata httpGetEnabled="True" />
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ReliableSessionElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>
- [신뢰할 수 있는 세션](../../../wcf/feature-details/reliable-sessions.md)
- [바인딩](../../../wcf/bindings.md)
- [바인딩 확장](../../../wcf/extending/extending-bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
