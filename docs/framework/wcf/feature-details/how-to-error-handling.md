---
title: '방법: 오류 처리'
ms.date: 03/30/2017
ms.assetid: de566e39-9358-44ff-8244-780f6b799966
ms.openlocfilehash: 3b8e48a74ff7671b942b5499fb3a0b5d0f389d61
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834706"
---
# <a name="how-to-error-handling"></a>방법: 오류 처리

이 항목에서는 오류 처리를 사용하는 라우팅 구성을 만드는 데 필요한 기본 단계에 대해 간략하게 설명합니다. 이 예제에서는 메시지를 대상 엔드포인트로 라우트합니다. 네트워크 또는 통신 관련 오류(<xref:System.ServiceModel.CommunicationException>)로 인해 메시지를 전달할 수 없는 경우에는 메시지가 대체 엔드포인트로 다시 보내집니다.

> [!NOTE]
> 네트워크 오류를 시뮬레이션하기 위해 이 예제에서 사용하는 대상 엔드포인트에는 잘못된 주소가 포함되어 있습니다. 따라서 지정된 주소에서 수신 대기하고 있는 서비스가 없으므로 이 엔드포인트로 라우트된 메시지는 실패합니다.

> [!NOTE]
> 이 항목의 예제에서는 제한 시간 설정에 대해 자세하게 설명하지 않지만 오류 처리를 사용할 때는 이러한 설정을 고려해야 합니다. 오류가 발생하면 클라이언트가 응답을 받기 전에 추가적인 지연이 발생합니다. 이는 라우팅 서비스가 오류를 받고 그 다음에 백업 엔드포인트에 메시지를 보내려고 시도하기 때문입니다. 기본 및 백업 대상 엔드포인트와 연결된 제한 시간 값이 클 경우 메시지가 성공적으로 전송될 때까지 백업 목록의 여러 엔드포인트로 장애 조치되기 때문에 클라이언트의 지연 시간이 길어질 수 있습니다.
>
> 라우팅 서비스에서 필터와 연결된 모든 엔드포인트의 제한 시간을 더한 것과 같은 최대 지연이 발생할 수 있으므로 클라이언트에서도 이에 따라 예상 제한 시간을 늘리는 것이 좋습니다.

### <a name="implement-error-handling"></a>오류 처리 구현

1. 서비스에서 노출하는 서비스 엔드포인트를 지정하여 기본 라우팅 서비스 구성을 만듭니다. 다음 예제에서는 메시지를 받는 데 사용되는 하나의 서비스 엔드포인트와 메시지를 보내는 데 사용되는 클라이언트 엔드포인트인 deadDestination과 realDestination을 정의합니다. deadDestination 엔드포인트에는 실행 중인 서비스를 참조하지 않는 주소가 포함되어 있습니다. 이 주소는 이 엔드포인트에 메시지를 보낼 때 네트워크 오류를 시뮬레이션하는 데 사용됩니다.

    ```xml
    <services>
      <service behaviorConfiguration="routingConfiguration"
               name="System.ServiceModel.Routing.RoutingService">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost/routingservice/" />
          </baseAddresses>
        </host>
        <!-- Create the Routing Service endpoint -->
        <endpoint address="router"
                  binding="basicHttpBinding"
                  name="RoutingServiceEndpoint"
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />
      </service>
    </services>

    <!-- Create the destination endpoints that we want to send to -->
    <client>
      <!-- Create a dummy endpoint that we know will be down -->
      <endpoint name="deadDestination"
                address="net.tcp://localhost:9090/servicemodelsamples/fakeDestination"
                binding="netTcpBinding"
                contract="*" />

      <!-- Now create the real service endpoint -->
      <endpoint name="realDestination"
                address="net.tcp://localhost:8080/servicemodelsamples/service"
                binding="netTcpBinding"
                contract="*" />
    </client>
    ```

2. 대상 엔드포인트에 메시지를 라우트하는 데 사용되는 필터를 정의합니다.  이 예제에서는 MatchAll 필터를 사용하여 라우팅 서비스에서 받는 모든 메시지를 일치시킵니다.

    ```xml
    <filters>
      <!-- Create a MatchAll filter which will catch all messages -->
      <filter name="MatchAllFilter1" filterType="MatchAll" />
    </filters>
    ```

3. 기본 대상 엔드포인트에 보낼 때 네트워크 또는 통신 오류가 발생할 경우 메시지를 보낼 엔드포인트가 들어 있는 백업 엔드포인트 목록을 정의합니다. 다음 예제에서는 하나의 엔드포인트가 들어 있는 백업 목록을 정의합니다. 실제 백업 목록에는 여러 개의 엔드포인트를 지정할 수 있습니다.

     백업 목록에 여러 개의 엔드포인트가 들어 있을 경우 네트워크 또는 통신 오류가 발생하면 라우팅 서비스는 백업 목록에 있는 첫 번째 엔드포인트에 메시지를 보내려고 시도합니다. 이 첫 번째 엔드포인트에 메시지를 보낼 때도 네트워크 또는 통신 오류가 발생하면 라우팅 서비스는 백업 목록에 있는 다음 엔드포인트에 메시지를 보내려고 시도합니다. 라우팅 서비스는 메시지가 성공적으로 전송되거나, 모든 백업 엔드포인트에서 네트워크 또는 통신 관련 오류를 반환하거나, 메시지를 받은 엔드포인트에서 네트워크 또는 통신과 관련 없는 오류를 반환할 때까지 백업 엔드포인트 목록에 있는 각 엔드포인트에 메시지를 계속 보냅니다.

    ```xml
    <backupLists>
      <backupList name="backupEndpointList">
          <add endpointName="realDestination" />
      </backupList>
    </backupLists>
    ```

4. 필터를 deadDestination 엔드포인트 및 백업 엔드포인트 목록과 연결하는 필터 테이블을 정의합니다.  라우팅 서비스는 먼저 필터와 연결된 대상 엔드포인트에 메시지를 보내려고 시도합니다. 이 경우 deadDestination에 실행 중인 서비스를 참조하지 않는 주소가 포함되어 있기 때문에 네트워크 오류가 발생합니다. 그런 다음 라우팅 서비스는 backupEndpointList에 지정 된 끝점으로 메시지를 보내려고 시도 합니다.

    ```xml
    <filterTables>
            <!-- Set up the Routing Service's Message Filter Table -->
            <filterTable name="filterTable1">
                <!-- Add an entity that maps the MatchAllMessageFilter to the dead destination -->
                <!-- If that endpoint is down, tell the Routing Service to try the endpoints -->
                <!-- Listed in the backupEndpointList -->
                <add filterName="MatchAllFilter1" endpointName="deadDestination" backupList="backupEndpointList"/>
            </filterTable>
          </filterTables>
    ```

5. 필터 테이블에 포함된 필터에 대해 들어오는 메시지를 평가하려면 라우팅 동작을 사용하여 필터 테이블을 서비스 엔드포인트와 연결해야 합니다.  다음 예제에서는 "filterTable1"을 서비스 끝점과 연결 하는 방법을 보여 줍니다.

    ```xml
    <behaviors>
      <serviceBehaviors>
        <!-- Set up the Routing Behavior -->
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
<!-- Copyright (c) Microsoft Corporation.  All Rights Reserved. -->
<configuration>
  <system.serviceModel>
    <services>
      <service behaviorConfiguration="routingConfiguration"
               name="System.ServiceModel.Routing.RoutingService">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost/routingservice/" />
          </baseAddresses>
        </host>
        <!-- Create the Routing Service endpoint -->
        <endpoint address="router"
                  binding="basicHttpBinding"
                  name="RoutingServiceEndpoint"
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <!-- Set up the Routing Behavior -->
        <behavior name="routingConfiguration">
          <routing filterTableName="filterTable1" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <!-- Create the destination endpoints that we want to send to -->
    <client>
      <!-- Create a dummy endpoint that we know will be down -->
      <endpoint name="deadDestination"
                address="net.tcp://localhost:9090/servicemodelsamples/fakeDestination"
                binding="netTcpBinding"
                contract="*" />

      <!-- Now create the real service endpoint -->
      <endpoint name="realDestination"
                address="net.tcp://localhost:8080/servicemodelsamples/service"
                binding="netTcpBinding"
                contract="*" />
    </client>
    <routing>
      <filters>
        <!-- Create a MatchAll filter which will catch all messages -->
        <filter name="MatchAllFilter1" filterType="MatchAll" />
      </filters>
      <filterTables>
        <!-- Set up the Routing Service's Message Filter Table -->
        <filterTable name="filterTable1">
            <!-- Add an entry that maps the MatchAllMessageFilter to the dead destination -->
            <!-- If that endpoint is down, tell the Routing Service to try the endpoints -->
            <!-- Listed in the backupEndpointList -->
            <add filterName="MatchAllFilter1" endpointName="deadDestination" backupList="backupEndpointList"/>
        </filterTable>
      </filterTables>
      <!-- Create the backup endpoint list -->
      <backupLists>
        <backupList name="backupEndpointList">
            <add endpointName="realDestination" />
        </backupList>
      </backupLists>
      </routing>
  </system.serviceModel>
</configuration>
```
