---
title: 구성 파일에서 검색 구성
ms.date: 03/30/2017
ms.assetid: b9884c11-8011-4763-bc2c-c526b80175d0
ms.openlocfilehash: 0ad44d0ad1f0d67d84cc42f6b9938d096c245417
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834755"
---
# <a name="configuring-discovery-in-a-configuration-file"></a>구성 파일에서 검색 구성
검색에 사용되는 구성 설정에는 네 가지 기본 그룹이 있습니다. 이 항목에서는 각 그룹에 대해 간략하게 설명하고 이러한 그룹을 구성하는 방법을 보여 줍니다. 아래에 나오는 각 단원은 각 영역에 대해 보다 자세히 설명하는 문서로 연결됩니다.  
  
## <a name="behavior-configuration"></a>동작 구성  
 검색에는 서비스 동작과 엔드포인트 동작이 사용됩니다. <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> 동작을 사용하면 모든 서비스의 엔드포인트를 검색하고 알림 엔드포인트를 지정할 수 있습니다.  다음 예제에서는 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>를 추가하고 알림 엔드포인트를 지정하는 방법을 보여 줍니다.  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="helloWorldServiceBehavior">  
          <serviceDiscovery>  
            <announcementEndpoints>  
              <endpoint kind="udpAnnouncementEndpoint"/>  
            </announcementEndpoints>  
          </serviceDiscovery>  
        </behavior>  
      </serviceBehaviors>  
```  
  
 동작을 지정한 후에는 다음 샘플과 같이 < `service` > 요소에서 참조 합니다.  
  
```xml  
<system.serviceModel>  
   <services>  
      <service name="HelloWorldService" behaviorConfiguration="helloWorldServiceBehavior">  
         <!-- Application Endpoint -->  
         <endpoint address="endpoint0"  
                   binding="basicHttpBinding"  
                   contract="IHelloWorldService" />  
         <!-- Discovery Endpoints -->  
         <endpoint kind="udpDiscoveryEndpoint" />  
        </service>  
    </service>  
```  
  
 서비스를 검색 가능하게 만들려면 검색 엔드포인트도 추가해야 합니다. 위의 예제에서는 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 표준 엔드포인트를 추가했습니다.  
  
 알림 끝점을 추가할 때는 다음 예제와 같이 < `services` > 요소에 알림 수신기 서비스도 추가 해야 합니다.  
  
```xml  
<services>  
   <service name="HelloWorldService" behaviorConfiguration="helloWorldServiceBehavior">  
      <!-- Application Endpoint -->  
      <endpoint address="endpoint0"  
                binding="basicHttpBinding"  
                contract="IHelloWorldService" />  
      <!-- Discovery Endpoints -->  
      <endpoint kind="udpDiscoveryEndpoint" />  
   </service>  
   <!-- Announcement Listener Configuration -->  
   <service name="AnnouncementListener">  
      <endpoint kind="udpAnnouncementEndpoint" />  
   </service>  
```  
  
 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 동작은 특정 엔드포인트의 검색을 사용하거나 사용하지 않도록 설정하는 데 사용됩니다.  다음 예제에서는 하나는 검색이 가능하고 다른 하나는 검색이 가능하지 않은 두 개의 응용 프로그램 엔드포인트가 있는 서비스를 구성합니다. 각 엔드포인트에는 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 동작이 추가됩니다.  
  
```xml  
<system.serviceModel>  
   <services>  
      <service name="HelloWorldService"  
               behaviorConfiguration="helloWorldServiceBehavior">  
  
        <!-- Application Endpoints -->  
        <endpoint address="endpoint0"  
                 binding="basicHttpBinding"  
                 contract="IHelloWorldService"   
                 behaviorConfiguration="ep0Behavior" />  
  
        <endpoint address="endpoint1"  
                  binding="basicHttpBinding"  
                  contract="IHelloWorldService"  
                  behaviorConfiguration="ep1Behavior" />  
  
        <!-- Discovery Endpoints -->  
        <endpoint kind="udpDiscoveryEndpoint" />  
      </service>  
   </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="helloWorldServiceBehavior">  
          <serviceDiscovery />  
        </behavior>  
      </serviceBehaviors>  
      <endpointBehaviors>  
        <behavior name="ep0Behavior">  
          <endpointDiscovery enabled="true"/>  
        </behavior>  
        <behavior name="ep1Behavior">  
          <endpointDiscovery enabled="false"/>  
        </behavior>  
     </endpointBehaviors>  
   </behaviors>  
```  
  
 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 동작을 사용하여 서비스에서 반환되는 엔드포인트 메타데이터에 사용자 지정 메타데이터를 추가할 수도 있습니다. 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.  
  
```xml  
<behavior name="ep4Behavior">  
   <endpointDiscovery enabled="true">  
      <extensions>  
         <CustomMetadata>This is custom metadata.</CustomMetadata>  
         <d:Types xmlns:d="http://schemas.xmlsoap.org/ws/2005/04/discovery" xmlns:i="http://printer.example.org/2003/imaging">i:PrintBasic</d:Types>  
         <CustomMetadata netsted="true">  
            <NestedMetadata>This is a nested custom metadata.</NestedMetadata>  
         </CustomMetadata>  
      </extensions>  
   </endpointDiscovery>  
</behavior>  
```  
  
 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 동작을 사용하여 클라이언트에서 서비스를 검색하는 데 사용하는 범위와 형식을 추가할 수도 있습니다. 다음 예제에서는 클라이언트측 구성 파일에서 이 작업을 수행하는 방법을 보여 줍니다.  
  
```xml  
<behavior name="ep2Behavior">  
   <endpointDiscovery enabled="true">  
      <scopes>  
         <add scope="http://www.microsoft.com/building42/floor1"/>  
         <add scope="ldap:///ou=engineeringo=examplecomc=us"/>  
      </scopes>  
      <types>  
         <add name="test" namespace="http://example.microsoft.com/" />  
         <add name="additionalContract" namespace="http://example.microsoft.com/" />  
      </types>  
   </endpointDiscovery>  
</behavior>  
```  
  
 @No__t-0 및 @no__t에 대 한 자세한 내용은 [WCF 검색 개요](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)를 참조 하세요.  
  
## <a name="binding-element-configuration"></a>바인딩 요소 구성  
 바인딩 요소 구성은 클라이언트측에서 가장 흥미로운 부분입니다. 구성을 사용하면 WCF 클라이언트 애플리케이션에서 서비스를 검색하는 데 사용되는 찾기 조건을 지정할 수 있습니다.  다음 예제에서는 <xref:System.ServiceModel.Discovery.DiscoveryClient> 채널을 사용하여 사용자 지정 바인딩을 만들고 형식과 범위가 포함된 찾기 조건을 지정합니다. 또한 이 예제에서는 <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> 및 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 속성의 값도 지정합니다.  
  
```xml  
<bindings>  
   <customBinding>  
      <!-- Binding Configuration for the Application Endpoint -->  
      <binding name="discoBindingConfiguration">  
         <discoveryClient>  
            <endpoint kind="discoveryEndpoint"  
                      address="http://localhost:8000/ConfigTest/Discovery"  
                      binding="customBinding"  
                      bindingConfiguration="httpSoap12WSAddressing10"/>  
            <findCriteria duration="00:00:10" maxResults="2">  
              <types>  
                <add name="IHelloWorldService"/>  
              </types>  
              <scopes>  
                <add scope="http://www.microsoft.com/building42/floor1"/>  
              </scopes>              
            </findCriteria>  
          </discoveryClient>  
          <textMessageEncoding messageVersion="Soap11"/>  
          <httpTransport />  
        </binding>  
```  
  
 이 사용자 지정 바인딩 구성은 다음과 같이 클라이언트 엔드포인트에서 참조해야 합니다.  
  
```xml  
<client>  
      <endpoint address="http://schemas.microsoft.com/discovery/dynamic"  
                binding="customBinding"  
                bindingConfiguration="discoBindingConfiguration"  
                contract="IHelloWorldService" />  
    </client>  
```  
  
 찾기 조건에 대 한 자세한 내용은 [검색 찾기 및 FindCriteria](../../../../docs/framework/wcf/feature-details/discovery-find-and-findcriteria.md)를 참조 하세요. 검색 및 바인딩 요소에 대 한 자세한 내용은 [WCF 검색 개요](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md) 를 참조 하세요.  
  
## <a name="standard-endpoint-configuration"></a>표준 엔드포인트 구성  
 표준 엔드포인트는 하나 이상의 속성(주소, 바인딩 또는 계약)에 대한 기본값이나 변경할 수 없는 하나 이상의 속성 값이 있는 미리 정의된 엔드포인트입니다. .NET 4에는 세 개의 검색 관련 표준 엔드포인트인 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> 및 <xref:System.ServiceModel.Discovery.DynamicEndpoint>가 제공됩니다.  <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>는 UDP 멀티캐스트 바인딩을 통한 검색 작업에 대해 미리 구성된 표준 엔드포인트입니다. <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>는 UDP 바인딩을 통해 알림 메시지를 보내기 위해 미리 구성된 표준 엔드포인트입니다. <xref:System.ServiceModel.Discovery.DynamicEndpoint>는 런타임에 동적으로 검색을 사용하여 검색된 서비스의 엔드포인트 주소를 찾는 데 사용되는 표준 엔드포인트입니다.  표준 바인딩은 추가할 표준 끝점의 형식을 지정 하는 kind 특성이 포함 된 < `endpoint` > 요소를 사용 하 여 지정 됩니다. 다음 예제에서는 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 및 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>를 추가하는 방법을 보여 줍니다.  
  
```xml  
<services>  
   <service name="HelloWorldService">  
      <!-- ...  -->          
      <endpoint kind="udpDiscoveryEndpoint" />  
   </service>  
   <service name="AnnouncementListener">  
      <endpoint kind="udpAnnouncementEndpoint" />  
   </service>  
</services>  
```  
  
 표준 끝점은 < `standardEndpoints` > 요소에서 구성 됩니다. 다음 예제에서는 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 및 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>를 구성하는 방법을 보여 줍니다.  
  
```xml  
<standardEndpoints>  
      <udpAnnouncementEndpoint>  
        <standardEndpoint   
            name="udpAnnouncementEndpointSettings"   
            multicastAddress="soap.udp://239.255.255.250:3703"    
            maxAnnouncementDelay="00:00:00.800">  
          <transportSettings  
            duplicateMessageHistoryLength="1028"  
            maxPendingMessageCount="10"  
            maxMulticastRetransmitCount="3"  
            maxUnicastRetransmitCount="2"  
            socketReceiveBufferSize="131072"  
            timeToLive="2" />  
        </standardEndpoint>  
      </udpAnnouncementEndpoint>  
      <udpDiscoveryEndpoint>  
        <standardEndpoint  
            name="udpDiscoveryEndpointSettings"  
            multicastAddress="soap.udp://239.255.255.252:3704"  
            maxResponseDelay="00:00:00.800">  
          <transportSettings  
            duplicateMessageHistoryLength="2048"  
            maxPendingMessageCount="5"  
            maxReceivedMessageSize="8192"  
            maxBufferPoolSize="262144"/>  
        </standardEndpoint>  
      </udpDiscoveryEndpoint>  
```  
  
 표준 끝점 구성을 추가 했으면 다음 샘플과 같이 각 끝점에 대 한 < `endpoint` > 요소의 구성을 참조 합니다.  
  
```xml  
<services>  
   <service name="HelloWorldService">  
      <!-- ...  -->          
      <endpoint kind="udpDiscoveryEndpoint" endpointConfiguration="udpDiscoveryEndpointSettings"/>  
   </service>  
   <service name="AnnouncementListener">  
      <endpoint kind="udpAnnouncementEndpoint" endpointConfiguration="udpAnnouncementEndpointSettings" >  
   </service>  
</services>  
```  
  
 검색에 사용되는 다른 표준 엔드포인트와 달리 <xref:System.ServiceModel.Discovery.DynamicEndpoint>에는 바인딩과 계약을 지정합니다. 다음 예제에서는 <xref:System.ServiceModel.Discovery.DynamicEndpoint>를 추가하고 구성하는 방법을 보여 줍니다.  
  
```xml  
<system.serviceModel>  
    <client>  
      <endpoint kind="dynamicEndpoint" binding="basicHttpBinding" contract="IHelloWorldService" endpointConfiguration="dynamicEndpointConfiguration" />  
    </client>   
   <standardEndpoints>  
      <dynamicEndpoint>  
         <standardEndpoint name="dynamicEndpointConfiguration">  
             <discoveryClientSettings>  
              <findCriteria scopeMatchBy="http://schemas.microsoft.com/ws/2008/06/discovery/rfc" duration="00:00:10" maxResults="2">  
                 <types>  
                   <add name="IHelloWorldService"/>  
                 </types>  
                 <scopes>  
                   <add scope="http://www.microsoft.com/building42/floor1"/>  
                 </scopes>  
                 <extensions>  
                   <CustomMetadata>This is custom metadata.</CustomMetadata>          
                 </extensions>  
               </findCriteria>  
             </discoveryClientSettings>  
           </standardEndpoint>  
         </dynamicEndpoint>  
   </standardEndpoints>  
</system.ServiceModel>  
```  
  
 표준 끝점에 대 한 자세한 내용은 [표준 끝점](standard-endpoints.md)을 참조 하세요.
