---
title: '방법: 서비스 버전 관리'
ms.date: 03/30/2017
ms.assetid: 4287b6b3-b207-41cf-aebe-3b1d4363b098
ms.openlocfilehash: 5ce9e7fc896f1ebc46dd25777fc629532339cbe2
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988702"
---
# <a name="how-to-service-versioning"></a>방법: 서비스 버전 관리
이 항목에서는 메시지를 동일한 서비스의 여러 버전에 라우트하는 라우팅 구성을 만드는 데 필요한 기본 단계에 대해 간략하게 설명합니다. 이 예제에서 메시지는 계산기 서비스의 서로 다른 두 버전인 `roundingCalc`(v1)와 `regularCalc`(v2)에 라우트됩니다. 두 구현 모두 같은 연산을 지원하지만 이전 버전인 `roundingCalc` 서비스에서는 반환 전에 가장 가까운 정수 값으로 모든 계산을 반올림합니다. 클라이언트 애플리케이션에서는 새 버전인 `regularCalc` 서비스를 사용할지 여부를 나타낼 수 있어야 합니다.  
  
> [!WARNING]
> 메시지를 특정 서비스 버전에 라우트하려면 라우팅 서비스에서 메시지 내용을 기반으로 메시지 대상을 확인할 수 있어야 합니다. 아래에서 설명하는 방법에서는 클라이언트가 메시지 헤더에 정보를 삽입하여 버전을 지정합니다. 그러나 클라이언트가 추가 데이터를 전달하지 않아도 서비스 버전을 관리할 수 있는 방법이 있습니다. 예를 들어 최신 또는 가장 호환성이 뛰어난 버전의 서비스에 메시지를 라우트할 수 있거나 라우터에서 표준 SOAP 봉투의 일부를 사용할 수 있습니다.  
  
 두 서비스에 의해 노출되는 연산은 다음과 같습니다.  
  
- 추가  
  
- 빼기  
  
- 곱하기  
  
- 나누기  
  
 두 서비스 구현은 모두 같은 연산을 처리하고 반환하는 데이터를 제외하면 본질적으로 동일하므로 클라이언트 애플리케이션에서 보낸 메시지에 포함된 기본 데이터는 요청을 라우트할 방법을 결정하기에는 고유성이 부족합니다. 예를 들어 두 서비스의 기본 동작이 같기 때문에 동작 필터를 사용할 수 없습니다.  
  
 이 문제는 각 서비스 버전의 라우터에 특정 엔드포인트를 노출하거나 서비스 버전을 나타내는 사용자 지정 헤더 요소를 메시지에 추가하는 등의 여러 가지 방법으로 해결할 수 있습니다.  이러한 각 방법을 사용하면 들어오는 메시지를 특정 버전의 서비스에 고유하게 라우트할 수 있지만 여러 서비스 버전에 대한 요청을 구별하기 위해서는 고유한 메시지 내용을 사용하는 것이 좋습니다.  
  
 이 예제에서는 클라이언트 애플리케이션에서 요청 메시지에 ‘CalcVer’ 사용자 지정 헤더를 추가합니다. 이 헤더에는 메시지를 라우트해야 하는 대상 서비스의 버전을 나타내는 값이 포함됩니다. 값 ‘1’은 roundingCalc 서비스로 메시지를 처리해야 함을 나타내고 값 ‘2’는 regularCalc 서비스로 메시지를 처리해야 함을 나타냅니다. 이러한 값을 사용하면 클라이언트 애플리케이션에서 메시지를 처리할 서비스의 버전을 직접 제어할 수 있습니다.  사용자 지정 헤더가 메시지 내에 포함된 값이므로 한 엔드포인트를 사용하여 두 서비스 버전의 대상이 되는 메시지를 받을 수 있습니다. 다음 코드를 사용하면 클라이언트 애플리케이션에서 이 사용자 지정 헤더를 메시지에 추가할 수 있습니다.  
  
```csharp  
messageHeadersElement.Add(MessageHeader.CreateHeader("CalcVer", "http://my.custom.namespace/", "2"));  
```  
  
### <a name="implement-service-versioning"></a>서비스 버전 관리 구현  
  
1. 서비스에서 노출하는 서비스 엔드포인트를 지정하여 기본 라우팅 서비스 구성을 만듭니다. 다음 예제에서는 메시지를 받는 데 사용할 하나의 서비스 엔드포인트와 `roundingCalc`(v1) 및 `regularCalc`(v2) 서비스에 메시지를 보내는 데 사용할 클라이언트 엔드포인트를 정의합니다.  
  
    ```xml  
    <services>  
        <service behaviorConfiguration="routingConfiguration"  
                 name="System.ServiceModel.Routing.RoutingService">  
          <host>  
            <baseAddresses>  
              <add baseAddress="http://localhost/routingservice/router" />  
            </baseAddresses>  
          </host>  
          <!--Set up the inbound endpoint for the Routing Service-->  
          <endpoint address="calculator"  
                    binding="wsHttpBinding"  
                    name="routerEndpoint"  
                    contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        </service>  
    </services>  
    <client>  
    <!--set up the destination endpoints-->  
          <endpoint name="regularCalcEndpoint"  
                    address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                    binding="netTcpBinding"  
                    contract="*" />  
  
          <endpoint name="roundingCalcEndpoint"  
                    address="http://localhost:8080/servicemodelsamples/service/"  
                    binding="wsHttpBinding"  
                    contract="*" />  
        </client>  
    ```  
  
2. 대상 엔드포인트에 메시지를 라우트하는 데 사용되는 필터를 정의합니다.  이 예에서는 XPath 필터를 사용 하 여 "CalcVer" 사용자 지정 헤더의 값을 검색 하 여 메시지를 라우팅해야 하는 버전을 결정 합니다. XPath 필터는 "CalcVer" 헤더를 포함 하지 않는 메시지를 검색 하는 데도 사용 됩니다. 다음 예제에서는 필요한 필터 및 네임스페이스 테이블을 정의합니다.  
  
    ```xml  
    <!-- use the namespace table element to define a prefix for our custom namespace-->  
    <namespaceTable>  
      <add prefix="custom" namespace="http://my.custom.namespace/"/>  
    </namespaceTable>  
    <filters>  
      <!--define the different message filters-->  
      <!--define an xpath message filter to look for the  
          custom header containing a value of 2-->  
      <filter name="XPathFilterRegular" filterType="XPath"  
              filterData="sm:header()/custom:CalcVer = '2'"/>  
      <!--define an xpath message filter to look for the  
          custom header containing a value of 1-->  
      <filter name="XPathFilterRounding" filterType="XPath"  
              filterData="sm:header()/custom:CalcVer = '1'"/>  
       <!--define an xpath message filter to look for  
           messages that do not contain the custom header-->  
       <filter name="XPathFilterNoHeader" filterType="XPath"  
               filterData="count(sm:header()/custom:CalcVer)=0"/>  
    </filters  
    ```  
  
    > [!NOTE]
    > S 12 네임 스페이스 접두사는 네임 스페이스 테이블에서 기본적으로 정의 되며 네임 스페이스 `http://www.w3.org/2003/05/soap-envelope`를 나타냅니다.
  
3. 각 엔드포인트를 클라이언트 엔드포인트와 연결하는 필터 테이블을 정의합니다. 메시지에 값이 1 인 "CalcVer" 헤더가 포함 되어 있으면 regularCalc 서비스로 전송 됩니다. 값이 2이면 메시지가 roundingCalc 서비스에 보내집니다. 헤더가 없으면 메시지가 regularCalc에 라우트됩니다.  
  
     다음 예제에서는 필터 테이블을 정의하고 앞에서 정의한 필터를 추가합니다.  
  
    ```xml  
    <filterTables>  
      <filterTable name="filterTable1">  
          <!--add the filters to the message filter table-->  
          <!--look for the custom header = 1, and if we find it,  
              send the message to the rounding calc endpoint-->  
          <add filterName="XPathFilterRounding" endpointName="roundingCalcEndpoint"/>  
          <!--look for the custom header = 2, and if we find it,  
              send the message to the rounding calc endpoint-->  
          <add filterName="XPathFilterRegular" endpointName="regularCalcEndpoint"/>  
          <!--look for the absence of the custom header, and if  
              it is not present, assume the v1 endpoint-->  
          <add filterName="XPathFilterNoHeader" endpointName="roundingCalcEndpoint"/>  
      </filterTable>  
    </filterTables>  
    ```  
  
4. 필터 테이블에 포함된 필터에 대해 들어오는 메시지를 평가하려면 라우팅 동작을 사용하여 필터 테이블을 서비스 엔드포인트와 연결해야 합니다. 다음 예제에서는 서비스 끝점과 `filterTable1` 연결 하는 방법을 보여 줍니다.  
  
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
        <!--Set up the inbound endpoint for the Routing Service-->  
        <endpoint address="calculator"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
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
                address="http://localhost:8080/servicemodelsamples/service/"  
                binding="wsHttpBinding"  
                contract="*" />  
    </client>  
    <routing>  
      <!-- use the namespace table element to define a prefix for our custom namespace-->  
      <namespaceTable>  
        <add prefix="custom" namespace="http://my.custom.namespace/"/>  
      </namespaceTable>  
      <filters>  
        <!--define the different message filters-->  
        <!--define an xpath message filter to look for the  
            custom header containing a value of 2-->  
        <filter name="XPathFilterRegular" filterType="XPath"  
                filterData="sm:header()/custom:CalcVer = '2'"/>  
        <!--define an xpath message filter to look for the  
            custom header containing a value of 1-->  
        <filter name="XPathFilterRounding" filterType="XPath"  
                filterData="sm:header()/custom:CalcVer = '1'"/>  
        <!--define an xpath message filter to look for  
            messages that do not contain the custom header-->  
        <filter name="XPathFilterNoHeader" filterType="XPath"  
                filterData="count(sm:header()/custom:CalcVer)=0"/>  
      </filters>  
      <filterTables>  
        <filterTable name="filterTable1">  
            <!--add the filters to the message filter table-->  
            <!--look for the custom header = 1, and if we find it,  
                send the message to the rounding calc endpoint-->  
            <add filterName="XPathFilterRounding" endpointName="roundingCalcEndpoint"/>  
            <!--look for the custom header = 2, and if we find it,  
                send the message to the rounding calc endpoint-->  
            <add filterName="XPathFilterRegular" endpointName="regularCalcEndpoint"/>  
            <!--look for the absence of the custom header, and if  
                it is not present, assume the v1 endpoint-->  
            <add filterName="XPathFilterNoHeader" endpointName="roundingCalcEndpoint"/>  
        </filterTable>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="example"></a>예제  
 다음은 클라이언트 애플리케이션의 전체 목록입니다.  
  
```csharp  
using System;  
using System.ServiceModel;  
using System.ServiceModel.Channels;  
  
namespace Microsoft.Samples.AdvancedFilters  
{  
    //The service contract is defined in generatedClient.cs, generated from the service by the svcutil tool.  
  
    //Client implementation code.  
    class Client  
    {  
        static void Main()  
        {  
            //Print out the welcome text  
            Console.WriteLine("This sample routes the Calculator Sample through the new WCF RoutingService");  
            Console.WriteLine("Wait for all the services to indicate that they've started, then press");  
            Console.WriteLine("<ENTER> to start the client.");  
  
            while (Console.ReadLine() != "quit")  
            {  
                //Offer the Address configuration for the client  
                Console.WriteLine("");  
                Console.WriteLine("Welcome to the Calculator Client!");  
  
                EndpointAddress epa;  
                //set the default address as the general router endpoint  
                epa = new EndpointAddress("http://localhost/routingservice/router/calculator");  
  
                //set up the CalculatorClient with the EndpointAddress, the WSHttpBinding, and the ICalculator contract  
                //We use the WSHttpBinding so that the outgoing has a message envelope, which we'll manipulate in a minute  
                CalculatorClient client = new CalculatorClient(new WSHttpBinding(), epa);  
                //client.Endpoint.Contract = ContractDescription.GetContract(typeof(ICalculator));  
  
                //Ask the customer if they want to add a custom header to the outgoing message.  
                //The Router will look for this header, and if so ignore the endpoint the message was  
                //received on, and instead direct the message to the RoundingCalcService.  
                Console.WriteLine("");  
                Console.WriteLine("Which calculator service should be used?");  
                Console.WriteLine("Enter 1 for the rounding calculator, 2 for the regular calculator.");  
                Console.WriteLine("[1] or [2]?");  
  
                string header = Console.ReadLine();  
  
                //get the current operationContextScope from the client's inner channel  
                using (OperationContextScope ocs = new OperationContextScope((client.InnerChannel)))  
                {  
                    //get the outgoing message headers element (collection) from the context  
                    MessageHeaders messageHeadersElement = OperationContext.Current.OutgoingMessageHeaders;  
  
                    //if they wanted to create the header, go ahead and add it to the outgoing message  
                    if (header != null && (header=="1" || header=="2"))  
                    {  
                        //create a new header "RoundingCalculator", no specific namespace, and set the value to   
                        //the value of header.  
                        //the Routing Service will look for this header in order to determine if the message  
                        //should be routed to the RoundingCalculator  
                        messageHeadersElement.Add(MessageHeader.CreateHeader("CalcVer", "http://my.custom.namespace/", header));  
                    }  
                    else //incorrect choice, no header added  
                    {  
                        Console.WriteLine("Incorrect value entered, not adding a header");  
                    }  
  
                        //call the client operations  
                        CallClient(client);  
                }  
  
                //close the client to clean it up  
                client.Close();  
                Console.WriteLine();  
                Console.WriteLine("Press <ENTER> to run the client again or type 'quit' to quit.");  
            }  
        }  
  
        private static void CallClient(CalculatorClient client)  
        {  
            Console.WriteLine("");  
            Console.WriteLine("Sending!");  
            // Call the Add service operation.  
            double value1 = 100.00D;  
            double value2 = 15.99D;  
            double result = client.Add(value1, value2);  
            Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Subtract service operation.  
            value1 = 145.00D;  
            value2 = 76.54D;  
            result = client.Subtract(value1, value2);  
            Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Multiply service operation.  
            value1 = 9.00D;  
            value2 = 81.25D;  
            result = client.Multiply(value1, value2);  
            Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Divide service operation.  
            value1 = 22.00D;  
            value2 = 7.00D;  
            result = client.Divide(value1, value2);  
            Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [라우팅 서비스](../../../../docs/framework/wcf/samples/routing-services.md)
