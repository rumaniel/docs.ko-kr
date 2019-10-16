---
title: '방법: 동적 업데이트'
ms.date: 03/30/2017
ms.assetid: 9b8f6e0d-edab-4a7e-86e3-8c66bebc64bb
ms.openlocfilehash: 95d99afd09daf4d9bf3937a71d7773332ff1bc14
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834714"
---
# <a name="how-to-dynamic-update"></a>방법: 동적 업데이트
이 항목에서는 라우팅 구성을 만들고 동적으로 업데이트하는 데 필요한 기본 단계에 대해 간략하게 설명합니다. 이 예제에서는 구성 파일에서 초기 라우팅 구성을 가져오고 이 구성을 사용하여 모든 메시지를 regularCalc 계산기 서비스에 라우트합니다. 그러나 이 구성은 대상 엔드포인트를 roundingCalc 서비스로 변경하기 위해 이후에 프로그래밍 방식으로 업데이트됩니다.  
  
> [!NOTE]
> 다양한 구현에서 구성은 완전히 동적으로 업데이트되며 기본 구성에 의존하지 않지만 서비스를 시작할 때처럼 기본 구성을 사용해야 하는 경우도 있습니다.  
  
> [!NOTE]
> 동적 업데이트는 메모리에서만 발생하며 구성 파일을 수정하지는 않습니다.  
  
 regularCalc와 roundingCalc는 모두 같은 연산(더하기, 빼기, 곱하기, 나누기)을 지원하지만 roundingCalc는 가장 가까운 정수 값으로 모든 계산을 반올림합니다. 구성 파일은 모든 메시지를 regularCalc 서비스에 라우트하도록 서비스를 구성하는 데 사용됩니다. 라우팅 서비스가 시작된 후에는 메시지를 roundingCalc 서비스에 라우트하도록 서비스를 다시 구성하는 데 <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A>이 사용됩니다.  
  
### <a name="implement-initial-configuration"></a>초기 구성 구현  
  
1. 서비스에서 노출하는 서비스 엔드포인트를 지정하여 기본 라우팅 서비스 구성을 만듭니다. 다음 예제에서는 메시지를 받는 데 사용할 하나의 서비스 엔드포인트와 regularCalc에 메시지를 보내는 데 사용할 클라이언트 엔드포인트를 정의합니다.  
  
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
    <!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    ```  
  
2. 대상 엔드포인트에 메시지를 라우트하는 데 사용되는 필터를 정의합니다. 이 예제에서는 MatchAll 필터를 사용하여 모든 메시지를 앞에서 정의한 regularCalcEndpoint에 라우트합니다. 다음 예제에서는 필터와 필터 테이블을 정의합니다.  
  
    ```xml  
    <filters>  
      <!--define the message filter-->  
      <filter name="MatchAllFilter" filterType="MatchAll"/>  
    </filters>  
    <filterTables>  
      <filterTable name="filterTable1">  
          <!--add the filter to the message filter table-->  
          <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
      </filterTable>  
    </filterTables>  
    ```  
  
3. 필터 테이블에 포함된 필터에 대해 들어오는 메시지를 평가하려면 라우팅 동작을 사용하여 필터 테이블을 서비스 엔드포인트와 연결해야 합니다. 다음 예제에서는 "filterTable1"을 서비스 끝점과 연결 하는 방법을 보여 줍니다.  
  
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
  
## <a name="implement-dynamic-configuration"></a>동적 구성 구현  
 라우팅 서비스의 동적 구성은 새 <xref:System.ServiceModel.Routing.RoutingConfiguration>을 만들고 <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A>을 사용하여 현재 구성을 대체하는 방식으로 코드에서만 수행할 수 있습니다.  이 예제에서는 라우팅 서비스가 콘솔 애플리케이션 내에서 자체 호스팅됩니다. 애플리케이션이 시작되면 콘솔 창에 ‘regular’ 또는 ‘rounding’을 입력하여 메시지가 라우트되는 대상 엔드포인트를 구성하는 방식으로 라우팅 구성을 수정할 수 있습니다. ‘regular’를 입력하면 대상 엔드포인트가 regularCalc가 되고 ‘rounding’을 입력하면 대상 엔드포인트가 roundingCalc가 됩니다.  
  
1. 라우팅 서비스를 지원하려면 다음 using 문을 추가해야 합니다.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ServiceModel;  
    using System.ServiceModel.Channels;  
    using System.ServiceModel.Description;  
    using System.ServiceModel.Dispatcher;  
    using System.ServiceModel.Routing;  
    ```  
  
2. 다음 코드는 라우팅 서비스를 콘솔 애플리케이션으로 자체 호스팅하는 데 사용됩니다. 이 코드는 이전 단계에서 설명한 구성을 사용하여 라우팅 서비스를 초기화합니다. 이 구성은 애플리케이션 구성 파일에 들어 있습니다. while 루프에는 라우팅 구성을 변경하는 데 사용되는 코드가 포함됩니다.  
  
    ```csharp  
    // Host the service within this EXE console application.  
    public static void Main()  
    {  
        // Create a ServiceHost for the CalculatorService type.  
        using (ServiceHost serviceHost =  
            new ServiceHost(typeof(RoutingService)))  
        {  
            // Open the ServiceHost to create listeners           
            // and start listening for messages.  
            Console.WriteLine("The Routing Service configured, opening....");  
            serviceHost.Open();  
            Console.WriteLine("The Routing Service is now running.");  
             Console.WriteLine("Type 'quit' to terminate router.");  
             Console.WriteLine("<ENTER> to change routing configuration.");  
             while (Console.ReadLine() != "quit")  
             {  
            ....  
            }  
        }  
    }  
    ```  
  
3. 라우팅 구성을 동적으로 업데이트하려면 새 라우팅 구성을 만들어야 합니다. 기존 라우팅 구성을 완전히 대체하므로 여기에는 새 라우팅 구성에 필요한 모든 엔드포인트, 필터 및 필터 테이블이 포함되어야 합니다. 새 라우팅 구성을 사용하려면 <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A>을 호출하고 새 구성을 전달해야 합니다.  
  
     앞에서 정의한 while 루프에 다음 코드를 추가하여 사용자 입력을 기반으로 서비스를 다시 구성할 수 있도록 합니다.  
  
    ```csharp  
    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
    string destEndpoint = Console.ReadLine();  
    // Create a new RoutingConfiguration  
    RoutingConfiguration rc = new RoutingConfiguration();  
    // Determine the endpoint to configure for  
    switch (destEndpoint)  
    {  
        case "regular":  
            // Define the destination endpoint  
            ServiceEndpoint regularCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        case "rounding":  
            // Define the destination endpoint  
            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        default:  
            Console.WriteLine("Incorrect value entered, no change.");  
            break;  
    }  
    ```  
  
    > [!NOTE]
    > 새 RoutingConfiguration을 제공하는 메서드가 RoutingExtension 서비스 확장에 포함되어 있으므로 새 RoutingConfiguration 개체는 ServiceHost 또는 ServiceExtensions에 대한 참조를 가지고 있거나 가져올 수 있는 WCF 확장성 모델의 아무 위치에나 제공될 수 있습니다. 예를 들면 다른 ServiceExtension에 제공될 수 있습니다.
  
## <a name="example"></a>예제  

다음은이 예제에서 사용 되는 콘솔 응용 프로그램의 전체 목록입니다.
  
```csharp
//-----------------------------------------------------------------  
//  Copyright (c) Microsoft Corporation.  All Rights Reserved.  
//-----------------------------------------------------------------  
  
using System;  
using System.Collections.Generic;  
using System.ServiceModel;  
using System.ServiceModel.Channels;  
using System.ServiceModel.Description;  
using System.ServiceModel.Dispatcher;  
using System.ServiceModel.Routing;  
  
namespace Microsoft.Samples.AdvancedFilters  
{  
    public class Router  
    {  
        // Host the service within this EXE console application.  
        public static void Main()  
        {             
            // Create a ServiceHost for the CalculatorService type.  
            using (ServiceHost serviceHost =  
                new ServiceHost(typeof(RoutingService)))  
            {  
                // Open the ServiceHost to create listeners           
                // and start listening for messages.  
                Console.WriteLine("The Routing Service configured, opening....");  
                serviceHost.Open();  
                Console.WriteLine("The Routing Service is now running.");  
                Console.WriteLine("Type 'quit' to terminate router.");  
                Console.WriteLine("<ENTER> to change routing configuration.");  
                while (Console.ReadLine() != "quit")  
                {  
                    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
                    string destEndpoint = Console.ReadLine();  
                    // Create a new RoutingConfiguration  
                    RoutingConfiguration rc = new RoutingConfiguration();  
                    // Determine the endpoint to configure for  
                    switch (destEndpoint)  
                    {  
                        case "regular":  
                            // Define the destination endpoint  
                            ServiceEndpoint regularCalc = new ServiceEndpoint(  
                            ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                            new NetTcpBinding(),  
                            new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        case "rounding":  
                            // Define the destination endpoint  
                            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
                                ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                                new NetTcpBinding(),  
                                new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        default:  
                            Console.WriteLine("Incorrect value entered, no change.");  
                            break;  
                    }  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="example"></a>예제  
 
다음은이 예제에 사용 되는 구성 파일의 전체 목록입니다.
  
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
<!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
  
      <filters>  
        <!--define the message filter-->  
        <filter name="MatchAllFilter" filterType="MatchAll"/>  
      </filters>  
      <filterTables>  
        <filterTable name="filterTable1">  
            <!--add the filter to the message filter table-->  
            <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
        </filterTable>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- [라우팅 서비스](../samples/routing-services.md)
