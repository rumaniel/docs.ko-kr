---
title: '방법: 필터 사용'
ms.date: 03/30/2017
ms.assetid: f2c7255f-c376-460e-aa20-14071f1666e5
ms.openlocfilehash: 6c357f2f410362d56fc931529a9fe731df0a477e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968762"
---
# <a name="how-to-use-filters"></a>방법: 필터 사용
이 항목에서는 여러 필터를 사용하는 라우팅 구성을 만드는 데 필요한 기본 단계에 대해 간략하게 설명합니다. 이 예제에서 메시지는 regularCalc와 roundingCalc라는 두 계산기 서비스 구현으로 라우트됩니다. 두 구현 모두 같은 연산을 지원하지만 한 서비스에서 반환 전에 가장 가까운 정수 값으로 모든 계산을 반올림합니다. 클라이언트 애플리케이션은 서비스의 반올림 버전을 사용할 것인지 여부를 지정해야 합니다. 서비스 기본 설정이 지정되지 않으면 메시지는 두 서비스 사이에서 부하 분산됩니다. 두 서비스에 의해 노출되는 연산은 다음과 같습니다.  
  
- 추가  
  
- 빼기  
  
- 곱하기  
  
- 나누기  
  
 두 서비스 모두 같은 연산을 구현하고, 따라서 메시지에 지정된 작업이 고유하지 않으므로 Action 필터는 사용할 수 없습니다. 대신 메시지가 올바른 엔드포인트로 라우트되도록 추가 작업을 수행해야 합니다.  
  
### <a name="determine-unique-data"></a>고유 데이터 확인  
  
1. 두 서비스 구현은 모두 같은 연산을 처리하고 반환하는 데이터를 제외하면 본질적으로 동일하므로 클라이언트 애플리케이션에서 보낸 메시지에 포함된 기본 데이터는 요청을 라우트할 방법을 결정하기에는 고유성이 부족합니다. 그러나 클라이언트 애플리케이션이 메시지에 고유한 헤더 값을 추가하면 이 값을 사용하여 메시지를 라우트할 방법을 결정할 수 있습니다.  
  
     예를 들어 반올림 계산기에 의해 메시지를 처리해야 하는 경우 클라이언트 애플리케이션은 다음 코드를 사용하여 사용자 지정 헤더를 추가합니다.  
  
    ```csharp  
    messageHeadersElement.Add(MessageHeader.CreateHeader("RoundingCalculator",   
                                   "http://my.custom.namespace/", "rounding"));  
    ```  
  
     이제 XPath 필터를 사용하여 메시지에서 이 헤더를 검사하고, 헤더를 포함하는 메시지를 roundCalc 서비스로 라우트할 수 있습니다.  
  
2. 또한 라우팅 서비스는 EndpointName, EndpointAddress 또는 PrefixEndpointAddress 필터와 함께 사용하여 클라이언트 애플리케이션이 요청을 제출하는 엔드포인트를 기반으로 들어오는 메시지를 특정 계산기 구현으로 고유하게 라우트할 수 있는 두 개의 가상 서비스 엔드포인트를 노출합니다.  
  
### <a name="define-endpoints"></a>엔드포인트 정의  
  
1. 라우팅 서비스에 사용되는 엔드포인트를 정의할 때는 먼저 클라이언트와 서비스에 사용되는 채널의 셰이프를 결정해야 합니다. 이 시나리오에서는 두 대상 서비스 모두 요청-회신 패턴을 사용하므로 <xref:System.ServiceModel.Routing.IRequestReplyRouter>가 사용됩니다. 다음 예제에서는 라우팅 서비스에 의해 노출되는 서비스 엔드포인트를 정의합니다.  
  
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
            <!--first create the general router endpoint-->  
            <endpoint address="general"  
                      binding="wsHttpBinding"  
                      name="routerEndpoint"  
                      contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
            <!--create a virtual endpoint for the regular calculator service-->  
            <endpoint address="regular/calculator"  
                      binding="wsHttpBinding"  
                      name="calculatorEndpoint"  
                      contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
            <!--now create a virtual endpoint for the rounding calculator-->  
            <endpoint address="rounding/calculator"  
                      binding="wsHttpBinding"  
                      name="roundingEndpoint"  
                      contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
  
          </service>  
    </services>  
    ```  
  
     이 구성을 통해 라우팅 서비스는 세 개의 개별 엔드포인트를 노출합니다. 런타임에서의 선택에 따라 클라이언트 애플리케이션은 이러한 주소 중 하나에 메시지를 보냅니다. "가상" 서비스 끝점 ("반올림/계산기" 또는 "일반/계산기") 중 하나에 도착 하는 메시지는 해당 계산기 구현으로 전달 됩니다. 클라이언트 애플리케이션이 특정 엔드포인트로 요청을 보내지 않는 경우 메시지는 일반 엔드포인트로 전달됩니다. 엔드포인트 선택에 관계없이 클라이언트 애플리케이션은 사용자 지정 헤더를 포함하여 메시지가 반올림 계산기 구현으로 전달되어야 함을 나타내도록 선택할 수 있습니다.  
  
2. 다음 예제에서는 라우팅 서비스가 메시지를 라우트하는 클라이언트(대상) 엔드포인트를 정의합니다.  
  
    ```xml  
    <client>  
          <endpoint name="regularCalcEndpoint"  
                    address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                    binding="netTcpBinding"  
                    contract="*" />  
  
          <endpoint name="roundingCalcEndpoint"  
                    address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                    binding="netTcpBinding"  
                    contract="*" />  
    </client>  
    ```  
  
     이러한 엔드포인트는 필터 테이블에 사용되어 특정 필터에 일치할 경우 메시지를 보내는 대상 엔드포인트를 나타냅니다.  
  
### <a name="define-filters"></a>필터 정의  
  
1. 클라이언트 응용 프로그램이 메시지에 추가 하는 "RoundingCalculator" 사용자 지정 헤더를 기반으로 메시지를 라우팅하려면 XPath 쿼리를 사용 하 여이 헤더의 존재 여부를 확인 하는 필터를 정의 합니다. 이 헤더는 사용자 지정 네임 스페이스를 사용 하 여 정의 되므로 XPath 쿼리에 사용 되는 사용자 지정 네임 스페이스 접두사 "custom"을 정의 하는 네임 스페이스 항목도 추가 합니다. 다음 예제에서는 필요한 라우팅 섹션, 네임스페이스 테이블 및 XPath 필터를 정의합니다.  
  
    ```xml  
    <routing>  
          <!-- use the namespace table element to define a prefix for our custom namespace-->  
          <namespaceTable>  
            <add prefix="custom" namespace="http://my.custom.namespace/"/>  
          </namespaceTable>  
          <filters>  
            <!--define the different message filters-->  
            <!--define an xpath message filter to look for the custom header coming from the client-->  
            <filter name="XPathFilter" filterType="XPath"   
                    filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 'rounding'"/>  
          </filters>  
    </routing>  
    ```  
  
     이 **Messagefilter** 는 "반올림" 값을 포함 하는 메시지에서 RoundingCalculator 헤더를 찾습니다. 이 헤더는 클라이언트에 의해 설정되어 메시지가 roundingCalc 서비스로 라우트되어야 함을 나타냅니다.  
  
    > [!NOTE]
    > S 12 네임 스페이스 접두사는 네임 스페이스 테이블에서 기본적으로 정의 되며 네임 스페이스 `http://www.w3.org/2003/05/soap-envelope`를 나타냅니다.
  
2. 또한 두 가상 엔드포인트에 수신된 메시지를 찾는 필터도 정의해야 합니다. 첫 번째 가상 끝점은 "regular/계산기" 끝점입니다. 클라이언트는 이 엔드포인트에 요청을 보내 메시지가 regularCalc 서비스로 라우트되어야 함을 나타낼 수 있습니다. 다음 구성에서는 <xref:System.ServiceModel.Dispatcher.EndpointNameMessageFilter>를 사용하여 메시지가 filterData에 지정된 이름을 가진 엔드포인트를 통해 도착했는지 확인하는 필터를 정의합니다.  
  
    ```xml  
    <!--define an endpoint name filter looking for messages that show up on the virtual regular calculator endpoint-->  
    <filter name="EndpointNameFilter" filterType="EndpointName" filterData="calculatorEndpoint"/>  
    ```  
  
     "CalculatorEndpoint" 라는 서비스 끝점에서 메시지를 수신 하는 경우이 필터는로 `true`평가 됩니다.  
  
3. 다음으로 roundingEndpoint의 주소로 전송된 메시지를 찾는 필터를 정의합니다. 클라이언트는 이 엔드포인트에 요청을 보내 메시지가 roundingCalc 서비스로 라우트되어야 함을 나타낼 수 있습니다. 다음 구성에서는를 <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter> 사용 하 여 메시지가 "반올림/계산기" 끝점에 도착 했는지 확인 하는 필터를 정의 합니다.  
  
    ```xml  
    <!--define a filter looking for messages that show up with the address prefix.  The corresponds to the rounding calc virtual endpoint-->  
    <filter name="PrefixAddressFilter" filterType="PrefixEndpointAddress"  
            filterData="http://localhost/routingservice/router/rounding/"/>  
    ```  
  
     로 `http://localhost/routingservice/router/rounding/` 시작 하는 주소에서 메시지를 수신 하는 경우이 필터는 **true**로 평가 됩니다. 이 구성 `http://localhost/routingservice/router` 에서 사용 하는 기본 주소는이 고 roundingEndpoint에 지정 된 주소는 "반올림/계산기" 이므로이 `http://localhost/routingservice/router/rounding/calculator`끝점과 통신 하는 데 사용 되는 전체 주소는이 필터와 일치 합니다.  
  
    > [!NOTE]
    > PrefixEndpointAddress 필터는 일치를 수행할 때 호스트 이름을 평가하지 않습니다. 하나의 호스트가 다양한 호스트 이름을 사용하여 참조될 수 있고, 이러한 다양한 이름은 모두 클라이언트 애플리케이션에서 호스트를 참조하는 유효한 방법일 수 있기 때문입니다. 예를 들어 다음 항목은 모두 같은 호스트를 참조할 수 있습니다.  
    >   
    > - localhost  
    > - 127.0.0.1  
    > - `www.contoso.com`  
    > - ContosoWeb01  
  
4. 마지막 필터는 사용자 지정 헤더 없이 일반 엔드포인트에 도착하는 메시지의 라우팅을 지원해야 합니다. 이 시나리오의 경우 메시지는 regularCalc 서비스와 roundingCalc 서비스 사이를 번갈아 전환해야 합니다. 이러한 메시지의 "라운드 로빈" 라우팅을 지원 하려면 처리 된 각 메시지에 대해 하나의 필터 인스턴스가 일치 하도록 허용 하는 사용자 지정 필터를 사용 합니다.  다음 예제에서는 RoundRobinMessageFilter의 두 인스턴스를 정의하며, 이 두 인스턴스는 하나로 그룹화되어 서로 번갈아 전환되어야 함을 나타냅니다.  
  
    ```xml  
    <!-- Set up the custom message filters.  In this example,   
         we'll use the example round robin message filter,   
         which alternates between the references-->  
    <filter name="RoundRobinFilter1" filterType="Custom"  
                    customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly"  
                    filterData="group1"/>  
    <filter name="RoundRobinFilter2" filterType="Custom"  
                    customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly"  
                    filterData="group1"/>  
    ```  
  
     런타임 중에 이 필터 형식은 동일한 그룹으로 하나의 컬렉션에 구성된, 이 형식의 정의된 모든 필터 인스턴스 사이를 번갈아 전환합니다. 이로 인해이 사용자 지정 필터에 의해 처리 된 메시지가 `true` 및 `RoundRobinFilter1` `RoundRobinFilter2`에 대해 반환 되는 간을 대체 합니다.  
  
### <a name="define-filter-tables"></a>필터 테이블 정의  
  
1. 필터를 특정 클라이언트 엔드포인트에 연결하려면 해당 필터를 필터 테이블 내에 배치해야 합니다. 이 예제 시나리오에서는 필터가 처리되는 순서를 나타낼 수 있도록 하는 선택적인 설정인 필터 우선 순위 설정도 사용합니다. 필터 우선 순위를 지정하지 않으면 모든 필터가 동시에 평가됩니다.  
  
    > [!NOTE]
    > 필터 우선 순위를 지정하면 필터가 처리되는 순서를 제어할 수 있지만 라우팅 서비스의 성능에는 부정적인 영향을 미치게 됩니다. 가능한 경우 필터 우선 순위를 사용할 필요가 없도록 필터 논리를 생성하세요.  
  
     다음은 필터 테이블을 정의 하 고 우선 순위가 2 인 이전에 정의 된 "XPathFilter"를 테이블에 추가 합니다. 또한이 항목은가 `XPathFilter` 메시지와 일치 하는 경우 메시지가 `roundingCalcEndpoint`로 라우팅되도록 지정 합니다.  
  
    ```xml  
    <routing>  
    ...      <filters>  
    ...      </filters>  
          <filterTables>  
            <table name="filterTable1">  
              <entries>  
                <!--add the filters to the message filter table-->  
                <!--first look for the custom header, and if we find it,  
                    send the message to the rounding calc endpoint-->  
                <add filterName="XPathFilter" endpointName="roundingCalcEndpoint" priority="2"/>  
              </entries>  
            </table>  
          <filterTables>  
    </routing>  
    ```  
  
     필터 우선 순위를 지정하면 우선 순위가 가장 높은 필터가 가장 먼저 평가됩니다. 특정 우선 순위 수준에서 하나 이상의 필터가 일치하면 그 아래 우선 순위 수준의 필터는 평가되지 않습니다. 이 시나리오의 경우 2가 지정된 가장 높은 우선 순위이며, 이 필터가 이 수준에서 유일한 필터입니다.  
  
2. 필터 항목은 엔드포인트 이름 또는 주소 접두사를 검사하여 특정 엔드포인트에 메시지가 수신되었는지 확인하도록 정의되었습니다. 다음 항목은 필터 테이블에 이러한 두 필터 항목을 모두 추가하고 메시지가 라우트되는 대상 엔드포인트에 연결합니다. 이러한 필터는 우선 순위 1로 설정되어 이전 XPath 필터가 메시지와 일치하지 않은 경우에만 실행되어야 함을 나타냅니다.  
  
    ```xml  
    <!--if the header wasn't there, send the message based on which virtual endpoint it arrived at-->  
    <!--we determine this through the endpoint name, or through the address prefix-->  
    <add filterName="EndpointNameFilter" endpointName="regularCalcEndpoint" priority="1"/>  
    <add filterName="PrefixAddressFilter" endpointName="roundingCalcEndpoint" priority="1"/>  
    ```  
  
     이러한 필터는 우선 순위가 1이므로 우선 순위 수준 2의 필터가 메시지와 일치하지 않는 경우에만 평가됩니다. 또한 두 필터의 우선 순위 수준이 같으므로 두 필터는 동시에 평가됩니다. 두 필터 모두 상호 배타적이므로 둘 중 하나의 필터만 메시지와 일치할 수 있습니다.  
  
3. 이전 필터 중 메시지와 일치하는 필터가 없는 경우 메시지는 제네릭 서비스 엔드포인트를 통해 수신되며, 라우트될 지점을 나타내는 헤더 정보를 포함하지 않습니다. 이러한 메시지는 두 계산기 서비스로 메시지 부하를 분산하는 사용자 지정 필터에 의해 처리됩니다. 다음 예제에서는 필터 테이블에 필터 항목을 추가하는 방법을 보여 줍니다. 각 필터는 두 대상 엔드포인트 중 하나와 연결됩니다.  
  
    ```xml  
    <!--if none of the other filters have matched,   
        this message showed up on the default router endpoint,   
        with no custom header-->  
    <!--round robin these requests between the two services-->  
    <add filterName="RoundRobinFilter1" endpointName="regularCalcEndpoint" priority="0"/>  
    <add filterName="RoundRobinFilter2" endpointName="roundingCalcEndpoint" priority="0"/>  
    ```  
  
     이러한 항목은 우선 순위 0을 지정하므로 메시지와 일치하는 더 높은 우선 순위의 필터가 없는 경우에만 평가됩니다. 또한 두 필터는 우선 순위가 같으므로 동시에 평가됩니다.  
  
     앞서 설명한 바와 같이 이러한 필터 정의에 사용되는 사용자 지정 필터는 수신되는 각 메시지에 대해 둘 중 하나만 `true`로 평가됩니다. 두 개의 필터만 동일한 그룹 설정이 지정되어 이 필터로 정의되므로 라우팅 서비스는 regularCalcEndpoint와 RoundingCalcEndpoint로 번갈아 전송하게 됩니다.  
  
4. 필터를 기준으로 메시지를 평가하려면 먼저 메시지를 수신하는 데 사용될 서비스 엔드포인트에 필터 테이블을 연결해야 합니다.  다음 예제에서는 라우팅 동작을 사용하여 라우팅 테이블과 서비스 엔드포인트를 연결하는 방법을 보여 줍니다.  
  
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
        <!--first create the general router endpoint-->  
        <endpoint address="general"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <!--create a virtual endpoint for the regular calculator service-->  
        <endpoint address="regular/calculator"  
                  binding="wsHttpBinding"  
                  name="calculatorEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <!--now create a virtual endpoint for the rounding calculator-->  
        <endpoint address="rounding/calculator"  
                  binding="wsHttpBinding"  
                  name="roundingEndpoint"  
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
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
  
      <endpoint name="roundingCalcEndpoint"  
                address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
      <!-- use the namespace table element to define a prefix for our custom namespace-->  
      <namespaceTable>  
        <add prefix="custom" namespace="http://my.custom.namespace/"/>  
      </namespaceTable>  
      <filters>  
        <!--define the different message filters-->  
        <!--define an xpath message filter to look for the custom header coming from the client-->  
        <filter name="XPathFilter" filterType="XPath" filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 'rounding'"/>  
  
        <!--define an endpoint name filter looking for messages that show up on the virtual regular calculator endpoint-->  
        <filter name="EndpointNameFilter" filterType="EndpointName" filterData="calculatorEndpoint"/>  
  
        <!--define a filter looking for messages that show up with the address prefix.  The corresponds to the rounding calc virtual endpoint-->  
        <filter name="PrefixAddressFilter" filterType="PrefixEndpointAddress" filterData="http://localhost/routingservice/router/rounding/"/>  
  
        <!--Set up the custom message filters.  In this example, we'll use the example round robin message filter, which alternates between the references-->  
        <filter name="RoundRobinFilter1" filterType="Custom" customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly" filterData="group1"/>  
        <filter name="RoundRobinFilter2" filterType="Custom" customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly" filterData="group1"/>  
      </filters>  
      <filterTables>  
        <table name="filterTable1">  
          <entries>  
            <!--add the filters to the message filter table-->  
            <!--first look for the custom header, and if we find it, send the message to the rounding calc endpoint-->  
            <add filterName="XPathFilter" endpointName="roundingCalcEndpoint" priority="2"/>  
  
            <!--if the header wasn't there, send the message based on which virtual endpoint it arrived at-->  
            <!--we determine this through the endpoint name, or through the address prefix-->  
            <add filterName="EndpointNameFilter" endpointName="regularCalcEndpoint" priority="1"/>  
            <add filterName="PrefixAddressFilter" endpointName="roundingCalcEndpoint" priority="1"/>  
  
            <!--if none of the other filters have matched, this message showed up on the default router endpoint, with no custom header-->  
            <!--round robin these requests between the two services-->  
            <add filterName="RoundRobinFilter1" endpointName="regularCalcEndpoint" priority="0"/>  
            <add filterName="RoundRobinFilter2" endpointName="roundingCalcEndpoint" priority="0"/>  
          </entries>  
        </table>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [라우팅 서비스](../../../../docs/framework/wcf/samples/routing-services.md)
