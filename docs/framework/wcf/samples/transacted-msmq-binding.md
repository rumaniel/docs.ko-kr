---
title: 트랜잭션된 MSMQ 바인딩
ms.date: 03/30/2017
ms.assetid: 71f5cb8d-f1df-4e1e-b8a2-98e734a75c37
ms.openlocfilehash: 259ca8059ac1c4f62636a2320d5eb64daa7f56cf
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61759988"
---
# <a name="transacted-msmq-binding"></a>트랜잭션된 MSMQ 바인딩

이 샘플에서는 MSMQ(메시지 큐)를 사용하여 큐에 있는 트랜잭션된 통신을 수행하는 방법을 보여 줍니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

대기 중인 통신에서 클라이언트는 큐를 사용하여 서비스와 통신합니다. 좀더 정확하게 말하면 클라이언트는 큐에 메시지를 보내고, 서비스는 큐에서 보낸 메시지를 받습니다. 따라서 서비스와 클라이언트가 동시에 실행되고 있지 않더라도 큐를 사용하여 통신할 수 있습니다.

트랜잭션을 사용하여 메시지를 보내고 받는 경우 실제로 두 개의 개별 트랜잭션이 있습니다. 클라이언트가 트랜잭션의 범위 내에서 메시지를 보낼 때 트랜잭션은 클라이언트 및 클라이언트 큐 관리자의 로컬에 있습니다. 서비스가 트랜잭션의 범위 내에서 메시지를 받을 때 트랜잭션은 서비스 및 수신 큐 관리자의 로컬에 있습니다. 클라이언트와 서비스는 동일한 트랜잭션에 참여하지 않습니다. 이들은 큐에서 보내기 및 받기와 같은 작업을 수행할 때 서로 다른 트랜잭션을 사용합니다.

이 샘플에서 클라이언트는 트랜잭션의 범위 내에서 일련의 메시지를 서비스로 보냅니다. 그러면 서비스는 큐로 전송된 메시지를 서비스에 정의된 트랜잭션 범위 내에서 받습니다.

다음 샘플 코드와 같이 서비스 계약은 `IOrderProcessor`입니다. 이 인터페이스는 큐에서 사용하기에 적합한 단방향 서비스를 정의합니다.

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true)]
    void SubmitPurchaseOrder(PurchaseOrder po);
}
```

서비스 동작은 `TransactionScopeRequired`가 `true`로 설정된 작업 동작을 정의합니다. 따라서 큐에서 메시지를 검색할 때 사용되는 트랜잭션 범위가 메서드에서 액세스하는 리소스 관리자에서 동일하게 사용됩니다. 또한 메서드에서 예외를 throw하는 경우 메시지가 큐로 반환됩니다. 이 작업 동작을 설정하지 않을 경우 큐에 있는 채널은 큐로부터 메시지를 읽는 트랜잭션을 만들고 디스패치 전에 자동으로 이를 커밋하므로, 작업이 실패하면 메시지를 잃게 됩니다. 가장 일반적인 시나리오는 다음 코드에서와 같이 큐로부터 메시지를 읽을 때 사용되는 트랜잭션에 서비스 작업이 참여하는 것입니다.

```csharp
 // This service class that implements the service contract.
 // This added code writes output to the console window.
 public class OrderProcessorService : IOrderProcessor
 {
     [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]
     public void SubmitPurchaseOrder(PurchaseOrder po)
     {
         Orders.Add(po);
         Console.WriteLine("Processing {0} ", po);
     }
  …
}
```

서비스는 자체 호스트됩니다. MSMQ 전송을 사용하는 경우에는 사용되는 큐를 미리 만들어야 합니다. 수동으로 또는 코드를 통해 이 작업을 수행할 수 있습니다. 이 샘플에서 서비스에는 큐가 있는지 확인하고 큐가 없으면 이를 만드는 코드가 포함되어 있습니다. 큐 이름은 구성 파일에서 읽습니다. 기본 주소를 사용 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 서비스 프록시를 생성 합니다.

```csharp
// Host the service within this EXE console application.
public static void Main()
{
    // Get the MSMQ queue name from appSettings in configuration.
    string queueName = ConfigurationManager.AppSettings["queueName"];

    // Create the transacted MSMQ queue if necessary.
    if (!MessageQueue.Exists(queueName))
        MessageQueue.Create(queueName, true);

    // Create a ServiceHost for the OrderProcessorService type.
    using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))
    {
        // Open the ServiceHost to create listeners and start listening for messages.
        serviceHost.Open();

        // The service can now be accessed.
        Console.WriteLine("The service is ready.");
        Console.WriteLine("Press <ENTER> to terminate service.");
        Console.WriteLine();
        Console.ReadLine();

        // Close the ServiceHost to shut down the service.
        serviceHost.Close();
    }
}
```

다음 샘플 구성에서 보여 주는 것처럼 MSMQ 큐 이름은 구성 파일의 appSettings 섹션에 지정됩니다.

```xml
<appSettings>
    <add key="queueName" value=".\private$\ServiceModelSamplesTransacted" />
</appSettings>
```

> [!NOTE]
> <xref:System.Messaging>을 사용하여 큐를 만들 때 큐 이름은 로컬 컴퓨터에 점(.)을, 그 경로에는 백슬래시 구분 기호를 사용합니다. Windows Communication Foundation (WCF) 끝점 net.msmq 체계를 사용 하 여 큐 주소를 사용 하 여를 로컬 컴퓨터를 나타내는 "localhost"를 사용 하며 해당 경로에 슬래시를 사용 합니다.

클라이언트는 트랜잭션 범위를 만듭니다. 트랜잭션 범위 내에서 큐와 통신을 수행하여 모든 메시지가 큐로 전송되거나 어떤 메시지도 큐로 전송되지 않는 가장 작은 단위로 처리되도록 합니다. 트랜잭션은 트랜잭션 범위에서 <xref:System.Transactions.TransactionScope.Complete%2A>를 호출하여 커밋합니다.

```csharp
// Create a client.
OrderProcessorClient client = new OrderProcessorClient();

// Create the purchase order.
PurchaseOrder po = new PurchaseOrder();
po.CustomerId = "somecustomer.com";
po.PONumber = Guid.NewGuid().ToString();

PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();
lineItem1.ProductId = "Blue Widget";
lineItem1.Quantity = 54;
lineItem1.UnitCost = 29.99F;

PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();
lineItem2.ProductId = "Red Widget";
lineItem2.Quantity = 890;
lineItem2.UnitCost = 45.89F;

po.orderLineItems = new PurchaseOrderLineItem[2];
po.orderLineItems[0] = lineItem1;
po.orderLineItems[1] = lineItem2;

// Create a transaction scope.
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
{
    // Make a queued call to submit the purchase order.
    client.SubmitPurchaseOrder(po);
    // Complete the transaction.
    scope.Complete();
}

// Closing the client gracefully closes the connection and cleans up resources.
client.Close();

Console.WriteLine();
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

트랜잭션이 작동 중임을 확인하려면 아래 샘플 코드에서와 같이 클라이언트를 수정하여 트랜잭션 범위를 주석 처리하고 솔루션을 다시 빌드한 다음 클라이언트를 실행합니다.

```csharp
//scope.Complete();
```

트랜잭션이 완료되지 않았으므로 메시지가 큐에 보내지지 않습니다.

샘플을 실행하면 클라이언트 및 서비스 동작이 서비스 콘솔 창과 클라이언트 콘솔 창에 모두 표시됩니다. 서비스에서 클라이언트가 보내는 메시지를 받는 것을 볼 수 있습니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다. 큐를 사용하므로 클라이언트와 서비스가 동시에 실행 중일 필요는 없습니다. 클라이언트를 실행하고 종료한 다음 서비스를 다시 시작해도 메시지를 받을 수 있습니다.

```
The service is ready.
Press <ENTER> to terminate service.

Processing Purchase Order: 7b31ce51-ae7c-4def-9b8b-617e4288eafd
        Customer: somecustomer.com
        OrderDetails
                Order LineItem: 54 of Blue Widget @unit price: $29.99
                Order LineItem: 890 of Red Widget @unit price: $45.89
        Total cost of this order: $42461.56
        Order status: Pending
```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.

2. 서비스가 처음 실행되는 경우 서비스에서는 큐가 있는지 확인하고 큐가 없으면 큐를 만듭니다. 서비스를 처음 실행하여 큐를 만들거나 MSMQ 큐 관리자를 통해 큐를 만들 수 있습니다. Windows 2008에서 큐를 만들려면 다음 단계를 수행하세요.

    1. Visual Studio 2012의 서버 관리자를 엽니다.

    2. 확장 된 **기능** 탭 합니다.

    3. 마우스 오른쪽 단추로 클릭 **개인 메시지 큐**, 선택한 **새로 만들기**합니다 **개인 큐**합니다.

    4. 확인 합니다 **트랜잭션** 상자입니다.

    5. 입력 `ServiceModelSamplesTransacted` 새 대기열의 이름으로 합니다.

3. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.

기본적으로 <xref:System.ServiceModel.NetMsmqBinding>을 사용하여 전송 보안이 설정됩니다. MSMQ 전송 보안과 관련된 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>와 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>이라는 두 속성이 있습니다. 기본적으로 인증 모드는 `Windows`로 설정되고 보호 수준은 `Sign`으로 설정됩니다. MSMQ에서 인증 및 서명 기능을 제공하려면 도메인에 속해 있어야 하며 MSMQ의 Active Directory 통합 옵션이 설치되어 있어야 합니다. 이 기준에 맞지 않는 컴퓨터에서 이 샘플을 실행하면 오류가 발생합니다.

### <a name="to-run-the-sample-on-a-computer-joined-to-a-workgroup-or-without-active-directory-integration"></a>작업 그룹에 속해 있거나 Active Directory 통합이 없는 컴퓨터에서 샘플을 실행하려면

1. 컴퓨터가 도메인에 속해 있지 않거나 Active Directory 통합이 설치되어 있지 않은 경우에는 다음 샘플 구성 코드에서와 같이 인증 모드와 보호 수준을 `None`으로 설정하여 전송 보안을 끕니다.

    ```xml
    <system.serviceModel>
      <services>
        <service name="Microsoft.ServiceModel.Samples.OrderProcessorService"
                 behaviorConfiguration="OrderProcessorServiceBehavior">
          <host>
            <baseAddresses>
              <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>
            </baseAddresses>
          </host>
          <!-- Define NetMsmqEndpoint. -->
          <endpoint
              address="net.msmq://localhost/private/ServiceModelSamplesTransacted"
              binding="netMsmqBinding"
              bindingConfiguration="Binding1"
           contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />
          <!-- The mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex. -->
          <endpoint address="mex"
                    binding="mexHttpBinding"
                    contract="IMetadataExchange" />
        </service>
      </services>

      <bindings>
        <netMsmqBinding>
          <binding name="Binding1">
            <security mode="None" />
          </binding>
        </netMsmqBinding>
      </bindings>

        <behaviors>
          <serviceBehaviors>
            <behavior name="OrderProcessorServiceBehavior">
              <serviceMetadata httpGetEnabled="True"/>
            </behavior>
          </serviceBehaviors>
        </behaviors>

      </system.serviceModel>
    ```

2. 샘플을 실행하기 전에 서버와 클라이언트 모두에서 구성을 변경해야 합니다.

    > [!NOTE]
    > `security mode`를 `None`으로 설정하는 것은 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> 및 `Message` 보안을 `None`으로 설정하는 것과 같습니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Transacted`
