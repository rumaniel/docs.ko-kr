---
title: '방법: 서비스 데이터 분할'
ms.date: 03/30/2017
ms.assetid: 1ccff72e-d76b-4e36-93a2-e51f7b32dc83
ms.openlocfilehash: 49aefd88d73732a139a79f8c53d5beca44d4d4ba
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947868"
---
# <a name="how-to-service-data-partitioning"></a>방법: 서비스 데이터 분할
이 항목에서는 동일한 대상 서비스의 여러 인스턴스에서 메시지를 분할하는 데 필요한 기본 단계에 대해 간략하게 설명합니다. 일반적으로 서비스 데이터 분할은 더 좋은 품질의 서비스를 제공하기 위해 서비스의 크기를 조정해야 하는 경우나 다양한 고객의 요청을 특정 방식으로 처리해야 하는 경우에 사용됩니다. 예를 들어 높은 값 또는 "골드" 고객의 메시지는 표준 고객의 메시지 보다 높은 우선 순위로 처리 되어야 할 수 있습니다.  
  
 이 예제에서는 메시지가 regularCalc 서비스의 두 인스턴스 중 하나로 라우트됩니다. 이 서비스의 두 인스턴스는 동일합니다. 단, calculator1 엔드포인트로 표시된 서비스는 우수 고객으로부터 받은 메시지를 처리하고 calculator2 엔드포인트로 표시된 서비스는 기타 고객으로부터 받은 메시지를 처리합니다.  
  
 클라이언트가 보낸 메시지에는 메시지를 라우트해야 하는 대상 서비스를 식별하는 데 사용할 수 있는 고유한 데이터가 없습니다. 각 클라이언트가 데이터를 특정 대상 서비스로 라우트할 수 있도록 하려면 메시지를 받는 데 사용할 두 개의 서비스 엔드포인트를 구현해야 합니다.  
  
> [!NOTE]
> 이 예제에서는 특정 엔드포인트를 사용하여 데이터를 분할하지만 헤더나 본문 데이터 같은 메시지 자체 내에 포함된 정보를 사용하여 데이터를 분할할 수도 있습니다.  
  
### <a name="implement-service-data-partitioning"></a>서비스 데이터 분할 구현  
  
1. 서비스에서 노출하는 서비스 엔드포인트를 지정하여 기본 라우팅 서비스 구성을 만듭니다. 다음 예제에서는 메시지를 받는 데 사용되는 두 개의 엔드포인트와 regularCalc 서비스 인스턴스에 메시지를 보내는 데 사용되는 클라이언트 엔드포인트를 정의합니다.  
  
    ```xml  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoints for the Routing Service-->  
        <!--create the endpoints for the calculator service-->  
        <endpoint address="calculator1"  
                  binding="wsHttpBinding"  
                  name="calculator1Endpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <endpoint address="calculator2"  
                  binding="wsHttpBinding"  
                  name="calculator2Endpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
       </service>  
    </services>  
    <client>  
    <!--set up the destination endpoints-->  
        <endpoint name="CalcEndpoint1"  
                  address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                  binding="netTcpBinding"  
                  contract="*" />  
  
        <endpoint name="CalcEndpoint2"  
                  address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                  binding="netTcpBinding"  
                  contract="*" />  
     </client>  
    ```  
  
2. 대상 엔드포인트에 메시지를 라우트하는 데 사용되는 필터를 정의합니다.  이 예제에서는 EndpointName 필터를 사용하여 메시지를 받은 서비스 엔드포인트를 확인합니다. 다음 예제에서는 필요한 라우팅 섹션과 필터를 정의합니다.  
  
    ```xml  
    <filters>  
      <!--define the different message filters-->  
      <!--define endpoint name filters looking for messages that show up on the virtual endpoints-->  
      <filter name="HighPriority" filterType="EndpointName"  
              filterData="calculator1Endpoint"/>  
      <filter name="NormalPriority" filterType="EndpointName"  
              filterData="calculator2Endpoint"/>  
    </filters>  
    ```  
  
3. 각 엔드포인트를 클라이언트 엔드포인트와 연결하는 필터 테이블을 정의합니다. 이 예제에서는 메시지를 받는 데 사용된 특정 엔드포인트를 기반으로 메시지가 라우트됩니다. 메시지가 두 개의 가능한 필터 중 하나와만 일치할 수 있으므로 필터 우선 순위를 사용하여 필터가 평가되는 순서를 제어하지 않아도 됩니다.  
  
     다음 예제에서는 필터 테이블을 정의하고 앞에서 정의한 필터를 추가합니다.  
  
    ```xml  
    <filterTables>  
       <filterTable name="filterTable1">  
         <!--add the filters to the message filter table-->  
         <add filterName="HighPriority" endpointName="CalcEndpoint1"/>  
         <add filterName="NormalPriority" endpointName="CalcEndpoint2"/>  
       </filterTable>  
    </filterTables>  
    ```  
  
4. 테이블에 포함된 필터에 대해 들어오는 메시지를 평가하려면 라우팅 동작을 사용하여 필터 테이블을 서비스 엔드포인트와 연결해야 합니다. 다음 예제에서는 "filterTable1"을 서비스 끝점과 연결 하는 방법을 보여 줍니다.  
  
    ```xml  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
## <a name="example"></a>예제  
 다음은 구성 파일의 전체 목록입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright (c) Microsoft Corporation. All rights reserved -->  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoints for the Routing Service-->  
        <!--create the endpoints for the calculator service-->  
        <endpoint address="calculator1"  
                  binding="wsHttpBinding"  
                  name="calculator1Endpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <endpoint address="calculator2"  
                  binding="wsHttpBinding"  
                  name="calculator2Endpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
  
      </service>  
    </services>  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
    <client>  
<!--set up the destination endpoints-->  
      <endpoint name="CalcEndpoint1"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
  
      <endpoint name="CalcEndpoint2"  
                address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
      <!-- use the namespace table element to define a prefix for our custom namespace-->  
  
      <filters>  
        <!--define the different message filters-->  
        <!--define endpoint name filters looking for messages that show up on the virtual endpoints-->  
        <filter name="HighPriority" filterType="EndpointName"  
                filterData="calculator1Endpoint"/>  
        <filter name="NormalPriority" filterType="EndpointName"  
                filterData="calculator2Endpoint"/>  
      </filters>  
  
      <filterTables>  
        <filterTable name="filterTable1">  
          <!--add the filters to the message filter table-->  
          <add filterName="HighPriority" endpointName="CalcEndpoint1"/>  
          <add filterName="NormalPriority" endpointName="CalcEndpoint2"/>  
        </filterTable>  
      </filterTables>  
  
    </routing>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [라우팅 서비스](../../../../docs/framework/wcf/samples/routing-services.md)
