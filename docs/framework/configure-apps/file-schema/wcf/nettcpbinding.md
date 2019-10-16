---
title: <netTcpBinding>
ms.date: 03/30/2017
helpviewer_keywords:
- netTcpBinding Element
ms.assetid: 5c5104a7-8754-4335-8233-46a45322503e
ms.openlocfilehash: c2d0a5729aeea3cd30e07ce1cfa485bda7b8ed20
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400134"
---
# <a name="nettcpbinding"></a>\<netTcpBinding>

시스템 간 통신에 적합한 안전하고, 신뢰할 수 있으며, 최적화된 바인딩을 지정합니다. 기본적으로 메시지 보안 및 인증을 위한 Windows 보안, 메시지 배달을 위한 TCP 및 이진 메시지 인코딩을 지원하는 런타임 통신 스택을 생성합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<netTcpBinding >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<netTcpBinding>
  <binding closeTimeout="TimeSpan"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           listenBacklog="Integer"
           maxBufferPoolSize="integer"
           maxBufferSize="Integer"
           maxConnections="Integer"
           maxReceivedMessageSize="Integer"
           name="string"
           openTimeout="TimeSpan"
           portSharingEnabled="Boolean"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           transactionFlow="Boolean"
           transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse">
    <reliableSession ordered="Boolean"
                     inactivityTimeout="TimeSpan"
                     enabled="Boolean" />
    <security mode="None/Transport/Message/Both">
      <message clientCredentialType="None/Windows/UserName/Certificate/CardSpace"
               algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15" />
      <transport clientCredentialType="None/Windows/Certificate"
                 protectionLevel="None/Sign/EncryptAndSign" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</netTcpBinding>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소

다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`closeTimeout`|닫기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|  
|`hostNameComparisonMode`|URI 구문 분석에 사용되는 HTTP 호스트 이름 비교 모드를 지정합니다. 이 특성은 <xref:System.ServiceModel.HostNameComparisonMode> 형식이며 URI에 대해 비교할 때 호스트 이름이 서비스에 연결하는 데 사용되는지 여부를 나타냅니다. 기본값은 <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>이며 이 값은 비교 시 호스트 이름을 무시합니다.|  
|`listenBacklog`|수신기에서 수락하기까지 대기할 수 있는 최대 채널 수를 지정하는 양의 정수입니다. 이 한도를 초과하는 연결은 채널 수가 한도 아래로 내려갈 때까지 큐에 대기됩니다. `connectionTimeout` 특성은 연결 예외가 throw되기 전에 클라이언트가 연결을 대기하는 시간을 제한합니다. 기본값은 10입니다.|  
|`maxBufferPoolSize`|이 바인딩의 최대 버퍼 풀 크기를 지정하는 정수입니다. 기본값은 512 * 1024바이트입니다. WCF(Windows Communication Foundation)의 많은 부분에서 버퍼를 사용합니다. 버퍼를 사용할 때마다 만들고 삭제하면 비용이 많이 들며, 버퍼에 대한 가비지 수집 역시 비용이 많이 듭니다. 버퍼 풀이 있으면 이 풀로부터 버퍼를 가져와 사용한 다음 다시 풀로 반환할 수 있습니다. 따라서 버퍼를 만들고 삭제하는 데 오버헤드를 피할 수 있습니다.|  
|`maxBufferSize`|메시지를 메모리에 저장하는 데 사용되는 버퍼의 최대 크기(바이트)를 지정하는 양의 정수입니다.<br /><br /> `transferMode` 특성이 `Buffered`와 같은 경우 이 특성은 `maxReceivedMessageSize` 특성 값과 같아야 합니다.<br /><br /> `transferMode` 특성이 `Streamed`와 같은 경우 이 특성은 `maxReceivedMessageSize` 특성 값보다 클 수 없으며 적어도 헤더 크기 이상이어야 합니다.<br /><br /> 기본값은 65536입니다. 자세한 내용은 <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>을 참조하세요.|  
|`maxConnections`|서비스에서 생성하고 수락하는 최대 아웃바운드 및 인바운드 연결 수를 지정하는 정수입니다. 들어오는 연결과 나가는 연결 수는 이 특성에서 지정한 별도의 제한에 따라 계산됩니다.<br /><br /> 이 제한을 초과하는 인바운드 연결은 연결 수가 제한 아래로 내려갈 때까지 큐에 대기됩니다.<br /><br /> 이 한도를 초과하는 아웃바운드 연결은 연결 수가 한도 아래로 내려갈 때까지 큐에 대기됩니다.<br /><br /> 기본값은 10입니다.|  
|`maxReceivedMessageSize`|헤더를 비롯하여 이 바인딩으로 구성된 채널에서 받을 수 있는 최대 메시지 크기(바이트)를 지정하는 양의 정수입니다. 이 한도를 초과하는 메시지를 보낸 사람은 SOAP 오류를 받습니다. 수신자는 메시지를 삭제하고 추적 로그에 이벤트 항목을 만듭니다. 기본값은 65536입니다.|  
|`name`|바인딩의 구성 이름을 포함하는 문자열입니다. 이 값은 바인딩의 ID로 사용되므로 고유해야 합니다. [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)]부터는 바인딩 및 동작에 이름이 필요하지 않습니다. 기본 구성 및 이름이 없는 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.|  
|`openTimeout`|열기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|  
|`portSharingEnabled`|이 연결에서 TCP 포트 공유를 사용하는지 여부를 지정하는 부울 값입니다. 이 값이 `false`이면 바인딩마다 자체 단독 포트가 사용됩니다. 클라이언트는 영향을 받지 않으므로 이 설정은 서비스에만 적용됩니다.|  
|`receiveTimeout`|받기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:10:00입니다.|  
|`sendTimeout`|보내기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|  
|`transactionFlow`|바인딩에서 WS-Transactions 이동을 지원할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.|  
|`transactionProtocol`|이 바인딩과 함께 사용되는 트랜잭션 프로토콜을 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -OleTransactions<br />-   WSAtomicTransactionOctober2004<br /><br /> 기본값은 OleTransactions입니다. 이 특성은 <xref:System.ServiceModel.TransactionProtocol> 형식입니다.|  
|`transferMode`|메시지가 버퍼링되거나 스트리밍되는지 또는 요청이나 응답인지 지정하는 <xref:System.ServiceModel.TransferMode> 값입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](security-of-nettcpbinding.md)|바인딩에 대한 보안 설정을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.NetTcpSecurityElement> 형식입니다.|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|이 바인딩으로 구성된 엔드포인트에서 처리할 수 있는 SOAP 메시지의 복잡성에 대한 제약 조건을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> 형식입니다.|  
|[\<reliableSession>](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90))|채널 엔드포인트 간에 신뢰할 수 있는 세션이 설정되는지 여부를 지정합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|이 요소는 표준 및 사용자 지정 바인딩의 컬렉션을 보유합니다.|  
  
## <a name="remarks"></a>설명

이 바인딩에서는 기본적으로 런타임 통신 스택을 생성하며, 이 스택은 전송 보안, 메시지 배달을 위한 TCP 및 이진 메시지 인코딩을 사용합니다. 이 바인딩에 적절 한 Windows Communication Foundation (WCF) 시스템에서 제공한 인트라넷을 통해 통신 합니다.  
  
 에 대 한 기본 구성 합니다 `netTcpBinding` 에서 제공 하는 구성 보다 더 빠릅니다를 `wsHttpBinding`, 아니라 WCF 통신만을 위한 것입니다. 보안 동작은 선택적 `securityMode` 특성을 사용하여 구성할 수 있습니다. WS-ReliableMessaging 사용 시 선택적 `reliableSessionEnabled` 특성을 사용하여 구성할 수 있습니다. 그러나 신뢰 메시징은 기본적으로 해제되어 있습니다. `wsHttpBinding` 및 `basicHttpBinding`과 같이 HTTP 시스템에서 제공한 바인딩은 기본적으로 설정을 적용하도록 구성되는 반면, `netTcpBinding` 바인딩은 기본적으로 설정을 해제하는 것이 일반적이므로, 예를 들어 WS-* 사양 지원을 받으려면 옵트인(opt in)해야 합니다. 따라서 엔드포인트 간에 메시지를 교환할 경우의 TCP 기본 구성이 HTTP 바인딩을 위한 기본 구성보다 더 빠릅니다.  
  
## <a name="example"></a>예제

클라이언트 및 서비스 구성 파일에 바인딩이 지정됩니다. 바인딩 형식은 `binding` 요소의 `<endpoint>` 특성에서 지정합니다. netTcpBinding 바인딩을 구성하고 일부 설정을 변경하려면 바인딩 구성을 정의해야 합니다. 엔드포인트는 `bindingConfiguration` 특성을 사용하여 바인딩 구성을 참조해야 합니다. 다음 예제에서는 바인딩 구성을 정의합니다.  
  
```xml  
<services>
  <service name="Microsoft.ServiceModel.Samples.CalculatorService"
           behaviorConfiguration="CalculatorServiceBehavior">
    ...
    <endpoint address=""
              binding="netTcpBinding"
              contract="Microsoft.ServiceModel.Samples.ICalculator" />
    ...
  </service>
</services>
<bindings>
  <netTcpBinding>
    <binding closeTimeout="00:01:00"
             openTimeout="00:01:00"
             receiveTimeout="00:10:00"
             sendTimeout="00:01:00"
             transactionFlow="false"
             transferMode="Buffered"
             transactionProtocol="OleTransactions"
             hostNameComparisonMode="StrongWildcard"
             listenBacklog="10"
             maxBufferPoolSize="524288"
             maxBufferSize="65536"
             maxConnections="10"
             maxReceivedMessageSize="65536">
      <readerQuotas maxDepth="32"
                    maxStringContentLength="8192"
                    maxArrayLength="16384"
                    maxBytesPerRead="4096"
                    maxNameTableCharCount="16384" />
      <reliableSession ordered="true"
                       inactivityTimeout="00:10:00"
                       enabled="false" />
      <security mode="Transport">
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign" />
      </security>
    </binding>
  </netTcpBinding>
</bindings>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.NetTcpBinding>
- <xref:System.ServiceModel.Configuration.NetTcpBindingElement>
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
