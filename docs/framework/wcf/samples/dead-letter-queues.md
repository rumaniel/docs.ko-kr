---
title: 배달 못 한 편지 큐
ms.date: 03/30/2017
ms.assetid: ff664f33-ad02-422c-9041-bab6d993f9cc
ms.openlocfilehash: c8fea29fc420ea6bb922c93ea08e0e23d5bb941d
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928674"
---
# <a name="dead-letter-queues"></a>배달 못 한 편지 큐
이 샘플에서는 배달에 실패한 메시지를 처리하는 방법을 보여 줍니다. [트랜잭션 된 MSMQ 바인딩](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md) 샘플을 기반으로 합니다. 이 샘플에서는 `netMsmqBinding` 바인딩을 사용합니다. 이 서비스는 자체적으로 호스트되는 콘솔 애플리케이션으로서 이를 사용하여 서비스에서 대기된 메시지를 받는 것을 볼 수 있습니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

> [!NOTE]
> 이 샘플에서는 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서만 사용할 수 있는 각 애플리케이션의 배달 못 한 편지 큐를 보여 줍니다. 샘플을 수정하면 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 MSMQ 3.0에 기본 시스템 차원 큐를 사용할 수 있습니다.

 대기 중인 통신에서 클라이언트는 큐를 사용하여 서비스와 통신합니다. 좀더 정확하게 말하면 클라이언트는 큐에 메시지를 보내고, 서비스는 큐에서 보낸 메시지를 받습니다. 따라서 서비스와 클라이언트가 동시에 실행되고 있지 않더라도 큐를 사용하여 통신할 수 있습니다.

 대기 중인 통신에는 약간의 유휴 기간이 포함될 수 있으므로 메시지의 TTL(Time-To-Live) 값을 연결하여 시간이 지난 경우 메시지가 애플리케이션으로 배달되지 않도록 할 수 있습니다. 메시지 배달 실패 여부를 애플리케이션에 알려야 하는 경우도 있습니다. 메시지의 TTL(Time-To-Live)이 만료되었거나 메시지 배달에 실패한 경우 메시지는 배달 못 한 편지 큐에 저장됩니다. 그러면 보내는 애플리케이션에서 배달 못 한 편지 큐의 메시지를 읽고 아무 작업도 수행하지 않거나 배달 실패 원인을 해결하고 메시지를 다시 보내는 등의 수정 작업을 수행합니다.

 `NetMsmqBinding` 바인딩에서 배달 못 한 편지 큐는 다음과 같은 속성으로 표현됩니다.

- <xref:System.ServiceModel.MsmqBindingBase.DeadLetterQueue%2A> 속성은 클라이언트에 필요한 배달 못 한 편지 큐의 종류를 표현합니다. 이 열거형에는 다음과 같은 값이 있습니다.

- `None`: 클라이언트에서 배달 못 한 편지 큐가 필요 하지 않습니다.

- `System`: 배달 못한 시스템 편지 큐는 배달 하지 못한 메시지를 저장 하는 데 사용 됩니다. 배달 못 한 편지 시스템 큐는 컴퓨터에서 실행되는 모든 애플리케이션에서 공유합니다.

- `Custom`: <xref:System.ServiceModel.MsmqBindingBase.CustomDeadLetterQueue%2A> 속성을 사용 하 여 지정한 사용자 지정 배달 못 한 편지 큐는 배달 하지 못한 메시지를 저장 하는 데 사용 됩니다. 이 기능은 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서만 사용할 수 있습니다. 이 기능은 애플리케이션이 동일한 컴퓨터에서 실행되는 다른 애플리케이션과 배달 못 한 편지 큐를 공유하지 않고 고유한 배달 못 한 편지 큐를 사용해야 하는 경우에 사용됩니다.

- <xref:System.ServiceModel.MsmqBindingBase.CustomDeadLetterQueue%2A> 속성은 배달 못 한 편지 큐로 사용할 특정 큐를 표현합니다. 이 속성은 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서만 사용할 수 있습니다.

 이 샘플에서 클라이언트는 트랜잭션 범위 내에서 서비스로 일괄 처리 메시지를 보내고 이러한 메시지의 "TTL(Time-To-Live)" 값을 임의로 낮게 지정합니다(약 2초). 또한 클라이언트는 사용자 지정 배달 못 한 편지 큐를 지정하여 만료된 메시지를 큐에 삽입하는 데 사용합니다.

 클라이언트 애플리케이션은 배달 못 한 편지 큐에서 메시지를 읽고 메시지 보내기를 다시 시도하거나 원본 메시지가 배달 못 한 편지 큐에 저장된 원인을 해결한 후 메시지를 보낼 수 있습니다. 이 샘플에서 클라이언트는 오류 메시지를 표시합니다.

 다음 샘플 코드와 같이 서비스 계약은 `IOrderProcessor`입니다.

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true)]
    void SubmitPurchaseOrder(PurchaseOrder po);
}
```

 샘플의 서비스 코드는 [트랜잭션 된 MSMQ 바인딩의](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md)입니다.

 서비스와의 통신은 트랜잭션 범위 내에서 수행됩니다. 서비스는 큐에서 메시지를 읽고 작업을 수행한 후 작업 결과를 표시합니다. 애플리케이션도 배달 못 한 메시지에 대해 배달 못 한 편지 큐를 만듭니다.

```csharp
//The service contract is defined in generatedClient.cs, generated from the service by the svcutil tool.

//Client implementation code.
class Client
{
    static void Main()
    {
        // Get MSMQ queue name from app settings in configuration
        string deadLetterQueueName = ConfigurationManager.AppSettings["deadLetterQueueName"];

        // Create the transacted MSMQ queue for storing dead message if necessary.
        if (!MessageQueue.Exists(deadLetterQueueName))
            MessageQueue.Create(deadLetterQueueName, true);

        // Create a proxy with given client endpoint configuration
        OrderProcessorClient client = new OrderProcessorClient("OrderProcessorEndpoint");

        // Create the purchase order
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

        //Create a transaction scope.
        using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
        {
            // Make a queued call to submit the purchase order
            client.SubmitPurchaseOrder(po);
            // Complete the transaction.
            scope.Complete();
        }

        client.Close();

        Console.WriteLine();
        Console.WriteLine("Press <ENTER> to terminate client.");
        Console.ReadLine();
    }
}
```

 클라이언트 구성에는 메시지가 서비스에 도달하는 데 걸리는 시간을 짧게 지정됩니다. 지정된 시간 내에 메시지를 전송할 수 없으면 메시지가 만료되어 배달 못 한 편지 큐로 이동합니다.

> [!NOTE]
> 클라이언트는 지정된 시간 내에 서비스 큐로 메시지를 배달할 수 있습니다. 배달 못 한 편지 서비스가 실행되는지 확인하려면 서비스를 시작하기 전에 클라이언트를 실행해야 합니다. 메시지는 시간이 초과되면 배달 못 한 편지 서비스로 배달됩니다.

 애플리케이션에서 배달 못 한 편지 큐로 사용할 큐를 정의해야 합니다. 큐를 지정하지 않으면 기본 시스템 차원의 배달 못 한 트랜잭션 큐가 배달 못 한 메시지를 큐에 삽입하는 데 사용됩니다. 이 예제에서 클라이언트 애플리케이션은 애플리케이션 고유의 배달 못 한 편지 큐를 지정합니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <appSettings>
    <!-- use appSetting to configure MSMQ Dead Letter queue name -->
    <add key="deadLetterQueueName" value=".\private$\ServiceModelSamplesOrdersAppDLQ"/>
  </appSettings>

  <system.serviceModel>
    <client>
      <!-- Define NetMsmqEndpoint -->
      <endpoint name="OrderProcessorEndpoint"
                address="net.msmq://localhost/private/ServiceModelSamplesDeadLetter"
                binding="netMsmqBinding"
                bindingConfiguration="PerAppDLQBinding"
                contract="IOrderProcessor" />
    </client>

    <bindings>
      <netMsmqBinding>
        <binding name="PerAppDLQBinding"
                 deadLetterQueue="Custom"
                 customDeadLetterQueue="net.msmq://localhost/private/ServiceModelSamplesOrdersAppDLQ"
                 timeToLive="00:00:02"/>
      </netMsmqBinding>
    </bindings>
  </system.serviceModel>

</configuration>
```

 배달 못 한 메시지 서비스는 배달 못 한 편지 큐에서 메시지를 읽습니다. 배달 못 한 메시지 서비스는 `IOrderProcessor` 계약을 구현합니다. 그러나 이 구현에서는 주문을 처리하지 않습니다. 배달 못 한 메시지 서비스는 클라이언트 서비스이며 주문을 처리하는 기능이 없습니다.

> [!NOTE]
> 배달 못 한 편지 큐는 클라이언트 큐이며 클라이언트 큐 관리자에 대해 로컬입니다.

 배달 못 한 메시지 서비스 구현에서는 메시지 배달 실패의 원인을 확인하고 올바른 방법으로 해결합니다. 메시지 실패 원인은 <xref:System.ServiceModel.Channels.MsmqMessageProperty.DeliveryFailure%2A> 및 <xref:System.ServiceModel.Channels.MsmqMessageProperty.DeliveryStatus%2A> 열거형으로 캡처됩니다. 다음 샘플 코드와 같이 <xref:System.ServiceModel.Channels.MsmqMessageProperty>에서 <xref:System.ServiceModel.OperationContext>를 검색할 수 있습니다.

```csharp
public void SubmitPurchaseOrder(PurchaseOrder po)
{
    Console.WriteLine("Submitting purchase order did not succeed ", po);
    MsmqMessageProperty mqProp =
                  OperationContext.Current.IncomingMessageProperties[
                  MsmqMessageProperty.Name] as MsmqMessageProperty;
    Console.WriteLine("Message Delivery Status: {0} ",
                                                mqProp.DeliveryStatus);
    Console.WriteLine("Message Delivery Failure: {0}",
                                               mqProp.DeliveryFailure);
    Console.WriteLine();
    …
}
```

 배달 못 한 편지 큐의 메시지는 메시지를 처리하고 있는 서비스로 주소가 지정되는 메시지입니다. 따라서 배달 못 한 편지 메시지 서비스가 큐에서 메시지를 읽으면 WCF (Windows Communication Foundation) 채널 계층이 끝점에서 불일치를 찾아 메시지를 디스패치하지 않습니다. 이 경우 메시지의 주소는 주문 처리 서비스로 지정되지만 배달 못 한 메시지 서비스에서 해당 메시지를 받습니다. 다른 엔드포인트로 주소가 지정된 메시지를 받으려면 모든 주소와 일치하는 주소 필터를 `ServiceBehavior`에 지정합니다. 이 구성은 배달 못 한 편지 큐에서 읽은 메시지를 성공적으로 처리하기 위해 필요합니다.

 이 샘플에서 배달 못 한 메시지 서비스는 실패의 원인이 메시지 시간 초과인 경우 메시지를 다시 보냅니다. 다른 모든 원인에 대해서는 다음 샘플 코드와 같이 배달 오류를 표시합니다.

```csharp
// Service class that implements the service contract.
// Added code to write output to the console window.
[ServiceBehavior(InstanceContextMode=InstanceContextMode.Single, ConcurrencyMode=ConcurrencyMode.Single, AddressFilterMode=AddressFilterMode.Any)]
public class PurchaseOrderDLQService : IOrderProcessor
{
    OrderProcessorClient orderProcessorService;
    public PurchaseOrderDLQService()
    {
        orderProcessorService = new OrderProcessorClient("OrderProcessorEndpoint");
    }

    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]
    public void SubmitPurchaseOrder(PurchaseOrder po)
    {
        Console.WriteLine("Submitting purchase order did not succeed ", po);
        MsmqMessageProperty mqProp = OperationContext.Current.IncomingMessageProperties[MsmqMessageProperty.Name] as MsmqMessageProperty;

        Console.WriteLine("Message Delivery Status: {0} ", mqProp.DeliveryStatus);
        Console.WriteLine("Message Delivery Failure: {0}", mqProp.DeliveryFailure);
        Console.WriteLine();

        // resend the message if timed out
        if (mqProp.DeliveryFailure == DeliveryFailure.ReachQueueTimeout ||
            mqProp.DeliveryFailure == DeliveryFailure.ReceiveTimeout)
        {
            // re-send
            Console.WriteLine("Purchase order Time To Live expired");
            Console.WriteLine("Trying to resend the message");

            // reuse the same transaction used to read the message from dlq to enqueue the message to app. queue
            orderProcessorService.SubmitPurchaseOrder(po);
            Console.WriteLine("Purchase order resent");
        }
    }

    // Host the service within this EXE console application.
    public static void Main()
    {
        // Create a ServiceHost for the PurchaseOrderDLQService type.
        using (ServiceHost serviceHost = new ServiceHost(typeof(PurchaseOrderDLQService)))
        {
            // Open the ServiceHostBase to create listeners and start listening for messages.
            serviceHost.Open();

            // The service can now be accessed.
            Console.WriteLine("The dead letter service is ready.");
            Console.WriteLine("Press <ENTER> to terminate service.");
            Console.WriteLine();
            Console.ReadLine();
        }
    }
}
```

 다음 샘플에서는 배달 못 한 메시지에 대한 구성을 보여 줍니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service
          name="Microsoft.ServiceModel.Samples.PurchaseOrderDLQService">
        <!-- Define NetMsmqEndpoint in this case, DLQ end point to read messages-->
        <endpoint address="net.msmq://localhost/private/ServiceModelSamplesOrdersAppDLQ"
                  binding="netMsmqBinding"
                  bindingConfiguration="DefaultBinding"
                  contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />
      </service>
    </services>

    <client>
      <!-- Define NetMsmqEndpoint -->
      <endpoint name="OrderProcessorEndpoint"
                 address="net.msmq://localhost/private/ServiceModelSamplesDeadLetter"
                 binding="netMsmqBinding"
                 bindingConfiguration="SystemDLQBinding"
                 contract="IOrderProcessor" />
    </client>

    <bindings>
      <netMsmqBinding>
        <binding name="DefaultBinding" />
        <binding name="SystemDLQBinding"
                 deadLetterQueue="System"/>
      </netMsmqBinding>
    </bindings>
  </system.serviceModel>
</configuration>
```

 샘플을 실행하면 세 개의 실행 파일이 실행되어 각 애플리케이션에서 배달 못 한 편지 큐가 어떻게 작동하는지를 보여 줍니다. 이러한 실행 파일에는 클라이언트, 서비스 및 각 애플리케이션의 배달 못 한 편지 큐에서 메시지를 읽고 서비스로 다시 보내는 배달 못 한 편지 서비스가 있습니다. 모든 애플리케이션은 출력이 콘솔 창에 표시되는 콘솔 애플리케이션입니다.

> [!NOTE]
> 큐를 사용하므로 클라이언트와 서비스가 동시에 실행 중일 필요는 없습니다. 클라이언트를 실행하고 종료한 다음 서비스를 다시 시작해도 서비스에서 계속 메시지를 받을 수 있습니다. 큐를 만들려면 서비스를 시작했다가 종료해야 합니다.

 클라이언트를 실행하면 클라이언트에 다음 메시지가 표시됩니다.

```console
Press <ENTER> to terminate client.
```

 클라이언트에서 메시지를 보내려고 시도하지만 짧은 시간 제한으로 인해 메시지는 만료되고 각 애플리케이션의 배달 못 한 편지 큐에 삽입됩니다.

 그러면 메시지를 읽고 오류 코드를 표시한 다음 서비스로 메시지를 다시 보내는 배달 못 한 편지 서비스를 실행합니다.

```console
The dead letter service is ready.
Press <ENTER> to terminate service.

Submitting purchase order did not succeed
Message Delivery Status: InDoubt
Message Delivery Failure: ReachQueueTimeout

Purchase order Time To Live expired
Trying to resend the message
Purchase order resent
```

 서비스가 시작된 후 다시 전송된 메시지를 읽고 처리합니다.

```console
The service is ready.
Press <ENTER> to terminate service.

Processing Purchase Order: 97897eff-f926-4057-a32b-af8fb11b9bf9
        Customer: somecustomer.com
        OrderDetails
                Order LineItem: 54 of Blue Widget @unit price: $29.99
                Order LineItem: 890 of Red Widget @unit price: $45.89
        Total cost of this order: $42461.56
        Order status: Pending
```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. 서비스가 처음 실행되는 경우 서비스에서는 큐가 있는지 확인하고 큐가 없으면 큐를 만듭니다. 서비스를 처음 실행하여 큐를 만들거나 MSMQ 큐 관리자를 통해 큐를 만들 수 있습니다. Windows 2008에서 큐를 만들려면 다음 단계를 수행하세요.

    1. Visual Studio 2012에서 서버 관리자를 엽니다.

    2. **기능** 탭을 확장 합니다.

    3. **개인 메시지 큐**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**, **개인 큐**를 선택 합니다.

    4. **트랜잭션** 상자를 확인 합니다.

    5. 새 `ServiceModelSamplesTransacted` 큐의 이름으로을 입력 합니다.

3. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 큐 이름을 적절 하 게 변경 하 여 localhost를 컴퓨터의 전체 이름으로 바꾸고 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따릅니다.

### <a name="to-run-the-sample-on-a-computer-joined-to-a-workgroup"></a>작업 그룹에 가입된 컴퓨터에서 샘플을 실행하려면

1. 컴퓨터가 도메인에 속하지 않는 경우 다음 샘플 구성과 같이 인증 모드와 보호 수준을 `None`으로 설정하여 전송 보안을 해제합니다.

    ```xml
    <bindings>
        <netMsmqBinding>
            <binding name="TransactedBinding">
                <security mode="None"/>
            </binding>
        </netMsmqBinding>
    </bindings>
    ```

     엔드포인트의 `bindingConfiguration` 특성을 설정하여 엔드포인트가 바인딩과 연결되게 합니다.

2. 샘플을 실행하기 전에 DeadLetterService, 서버 및 클라이언트에서 구성을 변경해야 합니다.

    > [!NOTE]
    > `security mode`를 `None`으로 설정하는 것은 `MsmqAuthenticationMode`, `MsmqProtectionLevel` 및 `Message` 보안을 `None`으로 설정하는 것과 같습니다.

## <a name="comments"></a>주석
 기본적으로 `netMsmqBinding` 바인딩 전송을 사용하여 보안이 설정됩니다. `MsmqAuthenticationMode` 및 `MsmqProtectionLevel` 속성은 모두 전송 보안의 형식을 결정합니다. 기본적으로 인증 모드는 `Windows`로 설정되고 보호 수준은 `Sign`으로 설정됩니다. MSMQ에서 인증 및 서명 기능을 제공하려면 도메인에 속해 있어야 합니다. 도메인에 속하지 않은 컴퓨터에서이 샘플을 실행 하는 경우 다음과 같은 오류가 표시 됩니다. "사용자의 내부 메시지 큐 인증서가 없습니다."

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\DeadLetter`  
