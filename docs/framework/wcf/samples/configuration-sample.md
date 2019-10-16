---
title: 구성 샘플
ms.date: 03/30/2017
ms.assetid: 75515b4a-8d70-44c8-99e0-7423df41380e
ms.openlocfilehash: 87afeb0c562254e0f4cf6a85946a765a740c79ec
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990074"
---
# <a name="configuration-sample"></a>구성 샘플
이 샘플에서는 구성 파일을 사용하여 서비스를 검색 가능하게 만드는 방법을 보여 줍니다.  
  
> [!NOTE]
> 이 샘플은 구성에서 검색을 구현합니다. 코드에서 검색을 구현 하는 샘플은 [Basic](../../../../docs/framework/wcf/samples/basic-sample.md)을 참조 하세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\Configuration`  
  
## <a name="service-configuration"></a>서비스 구성  
 이 샘플의 구성 파일에서는 다음 두 가지 기능을 보여 줍니다.  
  
- 표준 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>를 통해 서비스를 검색할 수 있게 만듭니다.  
  
- 서비스의 애플리케이션 엔드포인트에 대한 검색 관련 정보를 조정하고 표준 엔드포인트의 검색 관련 설정 중 일부를 조정합니다.  
  
 검색 가능하도록 설정하려면 서비스의 응용 프로그램 구성 파일에서 몇 가지 변경 작업을 수행해야 합니다.  
  
- `<service>` 요소에 검색 끝점을 추가해야 합니다. 이는 표준 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 엔드포인트로서, 런타임에서 검색 서비스와 연결하는 시스템 엔드포인트입니다. 검색 서비스는 이 엔드포인트에서 메시지를 수신 대기합니다.  
  
- `<serviceDiscovery>` 섹션에 `<serviceBehaviors>` 동작을 추가합니다. 이 동작은 런타임에 서비스를 검색할 수 있게 해 주며, 앞에서 설명한 검색 엔드포인트를 사용하여 검색 `Probe` 및 `Resolve` 메시지를 수신 대기합니다. 이 두 가지 항목을 추가하면 서비스를 지정된 검색 엔드포인트에서 검색할 수 있게 됩니다.  
  
 다음 구성 코드 조각에서는 애플리케이션 엔드포인트와 검색 엔드포인트가 정의된 서비스를 보여 줍니다.  
  
```xml
<services>  
        <service name="Microsoft.Samples.Discovery.CalculatorService"  
                 behaviorConfiguration="calculatorServiceBehavior">  
          <endpoint address=""  
                    binding="wsHttpBinding"  
                    contract="Microsoft.Samples.Discovery.ICalculatorService"  
                    behaviorConfiguration="endpointBehaviorConfiguration" />  
          <endpoint name="udpDiscovery"   
                    kind="udpDiscoveryEndpoint"   
                endpointConfiguration="adhocDiscoveryEndpointConfiguration"/>        </service>  
      </services>  
```  
  
 알림을 사용하려면 알림 엔드포인트를 추가해야 합니다. 이렇게 하려면 다음 코드와 같이 구성 파일을 수정합니다.  
  
```xml  
<serviceDiscovery>  
            <announcementEndpoints>  
              <endpoint kind="udpAnnouncementEndpoint"/>  
            </announcementEndpoints>  
          </serviceDiscovery>  
```  
  
 알림 엔드포인트를 검색 서비스 동작에 추가하면 서비스에 대한 기본 알림 클라이언트가 만들어집니다. 이렇게 되면 서비스에서 서비스가 열리거나 닫힐 때 각각 온라인 및 오프라인 알림을 보냅니다.  
  
 이 구성 파일에서는 추가 동작을 수정하여 이러한 간단한 단계 외의 작업도 수행할 수 있습니다. 특정 엔드포인트를 사용하여 검색 관련 정보를 제어할 수 있습니다. 즉, 사용자가 엔드포인트의 검색 가능 여부를 제어할 수 있으며 해당 엔드포인트를 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior.Scopes%2A> 및 사용자 지정 XML 메타데이터로 표시할 수도 있습니다. 이렇게 하려면 애플리케이션 엔드포인트에 `behaviorConfiguration` 속성을 추가해야 합니다. 이 경우 다음 속성이 애플리케이션 엔드포인트에 추가됩니다.  
  
`behaviorConfiguration="endpointBehaviorConfiguration"`  
  
 이제 동작 구성 요소를 통해 검색 관련 특성을 제어할 수 있습니다. 이 경우 두 개의 범위가 애플리케이션 엔드포인트에 추가됩니다.  
  
```xml  
<endpointBehaviors>  
          <behavior name="endpointBehaviorConfiguration">  
            <endpointDiscovery>  
              <scopes>  
                <add scope="http://www.example.com/calculator"/>  
                <add scope="ldap:///ou=engineering,o=examplecom,c=us"/>  
              </scopes>  
            </endpointDiscovery>  
  
          </behavior>            
        </endpointBehaviors>  
```  
  
 범위에 대 한 자세한 내용은 [Discovery 찾기 및 FindCriteria](../../../../docs/framework/wcf/feature-details/discovery-find-and-findcriteria.md)를 참조 하세요.  
  
 검색 엔드포인트의 특정 세부 정보를 제어할 수도 있습니다. 이 작업은 <xref:System.ServiceModel.Configuration.StandardEndpointsSection>을 통해 수행합니다. 이 샘플에서는 다음 코드 예제와 같이 사용되는 프로토콜 버전을 수정할 뿐 아니라 `maxResponseDelay` 특성도 추가합니다.  
  
```xml  
<standardEndpoints>  
   <udpDiscoveryEndpoint>  
      <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11" maxResponseDelay="00:00:00.600" />    
   </udpDiscoveryEndpoint>  
</standardEndpoints>  
```  
  
 다음은 이 예제에 사용되는 전체 구성 파일입니다.  
  
```xml  
<configuration>  
    <system.serviceModel>  
  
      <services>  
        <service name="Microsoft.Samples.Discovery.CalculatorService"  
                 behaviorConfiguration="calculatorServiceBehavior">  
          <endpoint address=""  
                    binding="wsHttpBinding"  
                    contract="Microsoft.Samples.Discovery.ICalculatorService"  
                    behaviorConfiguration="endpointBehaviorConfiguration" />  
         <!-- Define the discovery endpoint -->            
<endpoint name="udpDiscovery" kind="udpDiscoveryEndpoint" endpointConfiguration="adhocDiscoveryEndpointConfiguration"/>        </service>  
      </services>  
  
      <behaviors>  
  
        <serviceBehaviors>  
          <behavior name="calculatorServiceBehavior">  
  
            <!-- Add an announcement endpoint -->  
            <serviceDiscovery>  
              <announcementEndpoints>  
                <endpoint kind="udpAnnouncementEndpoint"/>  
              </announcementEndpoints>  
            </serviceDiscovery>  
          </behavior>  
        </serviceBehaviors>  
  
        <endpointBehaviors>  
          <behavior name="endpointBehaviorConfiguration">  
            <!-- Add scopes used to identify the service -->  
            <endpointDiscovery>  
              <scopes>  
                <add scope="http://www.example.com/calculator"/>  
                <add scope="ldap:///ou=engineering,o=examplecom,c=us"/>  
              </scopes>  
            </endpointDiscovery>  
  
          </behavior>            
        </endpointBehaviors>  
  
      </behaviors>  
  
      <standardEndpoints>  
        <udpDiscoveryEndpoint>  
         <!-- Configure the UDP discovery endpoint -->  
          <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11" maxResponseDelay="00:00:00.600" />    
        </udpDiscoveryEndpoint>  
      </standardEndpoints>  
  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="client-configuration"></a>클라이언트 구성  
 클라이언트의 애플리케이션 구성 파일에서 `standardEndpoint` 형식의 `dynamicEndpoint`는 다음 구성 코드 조각과 같이 검색을 활용하는 데 사용됩니다.  
  
```xml  
<client>  
   <!--  Create an endpoint, make kind="dynamicEndpoint" and use the endpointConfiguration to change settings of DynamicEndpoint -->  
   <endpoint name="calculatorEndpoint"  
             binding="wsHttpBinding"  
             contract="ICalculatorService"  
             kind ="dynamicEndpoint"  
             endpointConfiguration="dynamicEndpointConfiguration">  
   </endpoint>  
</client>  
```  
  
 클라이언트에서 `dynamicEndpoint`를 사용하는 경우 런타임에서는 검색을 자동으로 수행합니다. 사용할 검색 엔드포인트의 형식을 지정하는 `discoveryClientSettings` 섹션에 정의된 설정과 같은 다양한 설정이 검색 중에 사용됩니다.  
  
```xml  
<endpoint kind="udpDiscoveryEndpoint" endpointConfiguration="adhocDiscoveryEndpointConfiguration" />  
```  
  
 서비스를 검색하는 데 사용되는 찾기 조건은 다음과 같습니다.  
  
```xml  
<!-- Add Scopes, ScopeMatchBy, Extensions and termination criteria in FindCriteria -->  
<findCriteria scopeMatchBy="http://schemas.microsoft.com/ws/2008/06/discovery/rfc" duration="00:00:10" maxResults="1">  
   <scopes>  
      <add scope="http://www.microsoft.com/building42/floor1"/>  
   </scopes>  
   <!-- These extensions are sent from the client to the service as part of the probe message -->  
   <extensions>  
      <CustomMetadata>This is custom metadata that is sent to the service along with the client's find request.</CustomMetadata>  
   </extensions>  
</findCriteria>  
```  
  
 이 샘플에서는 이 기능을 확장하고, 클라이언트에서 사용하는 <xref:System.ServiceModel.Discovery.FindCriteria>뿐 아니라 검색에 사용되는 표준 `updDiscoveryEndpoint`의 일부 속성도 수정합니다. 범위, 특정 <xref:System.ServiceModel.Discovery.FindCriteria> 알고리즘 및 사용자 지정 종료 조건을 사용하도록 `scopeMatchBy`를 수정합니다. 또한 이 샘플에서는 클라이언트가 `Probe` 메시지를 사용하여 XML 요소를 보내는 방법도 보여 줍니다. 마지막으로 다음 구성 파일과 같이 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>에 대해 사용되는 프로토콜 버전 및 UDP 관련 설정 등의 사항을 변경합니다.  
  
```xml  
<udpDiscoveryEndpoint>    
        <!-- Specify the discovery protocol version and UDP transport settings. -->   
        <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11">  
          <transportSettings duplicateMessageHistoryLength="2048"  
                             maxPendingMessageCount="5"  
                             maxReceivedMessageSize="8192"  
                             maxBufferPoolSize="262144"/>  
        </standardEndpoint>        
      </udpDiscoveryEndpoint>  
```  
  
 다음은 샘플에 사용되는 전체 클라이언트 구성입니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
  
    <client>  
      <!--  Create an endpoint, make kind="dynamicEndpoint" and use the endpointConfiguration to change settings of DynamicEndpoint -->  
      <endpoint name="calculatorEndpoint"  
                binding="wsHttpBinding"  
                contract="ICalculatorService"  
                kind ="dynamicEndpoint"  
                endpointConfiguration="dynamicEndpointConfiguration">  
      </endpoint>  
    </client>  
  
    <standardEndpoints>  
  
      <dynamicEndpoint>        
        <standardEndpoint name="dynamicEndpointConfiguration">  
          <discoveryClientSettings>  
            <!-- Controls where the discovery happens. In this case, Probe message is sent over UdpDiscoveryEndpoint. -->  
            <endpoint kind="udpDiscoveryEndpoint" endpointConfiguration="adhocDiscoveryEndpointConfiguration" />  
  
            <!-- Add Scopes, ScopeMatchBy, Extensions and termination criteria in FindCriteria -->  
            <findCriteria scopeMatchBy="http://schemas.microsoft.com/ws/2008/06/discovery/rfc" duration="00:00:10" maxResults="1">  
              <scopes>  
                <add scope="http://www.microsoft.com/building42/floor1"/>  
              </scopes>  
              <!-- These extensions are sent from the client to the service as part of the probe message -->  
              <extensions>  
                <CustomMetadata>This is custom metadata that is sent to the service along with the client's find request.</CustomMetadata>  
              </extensions>  
            </findCriteria>  
          </discoveryClientSettings>  
        </standardEndpoint>     
      </dynamicEndpoint>  
  
      <udpDiscoveryEndpoint>    
        <!-- Specify the discovery protocol version and UDP transport settings. -->   
        <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11">  
          <transportSettings duplicateMessageHistoryLength="2048"  
                             maxPendingMessageCount="5"  
                             maxReceivedMessageSize="8192"  
                             maxBufferPoolSize="262144"/>  
        </standardEndpoint>        
      </udpDiscoveryEndpoint>  
  
    </standardEndpoints>  
  
  </system.serviceModel>  
```  
  
#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면  
  
1. 이 샘플에서는 HTTP 끝점을 사용 하며이 샘플을 실행 하려면 적절 한 URL Acl을 추가 해야 합니다. 자세한 내용은 [http 및 HTTPS 구성](https://go.microsoft.com/fwlink/?LinkId=70353) 을 참조 하세요. 높은 권한으로 다음 명령을 실행하면 적절한 ACL이 추가됩니다. 명령이 지정한 대로 작동하지 않는 경우 다음 인수의 도메인과 사용자 이름을 대체할 수 있습니다. `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`  
  
2. 솔루션을 빌드합니다.  
  
3. 빌드 디렉터리에서 서비스 실행 파일을 실행합니다.  
  
4. 클라이언트 실행 파일을 실행합니다. 클라이언트에서 서비스를 찾을 수 있는지 확인합니다.  
