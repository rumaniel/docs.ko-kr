---
title: 메시지 상관 관계
ms.date: 03/30/2017
ms.assetid: 3f62babd-c991-421f-bcd8-391655c82a1f
ms.openlocfilehash: 657f7c6e3fd544614e193d9e6843a8ed58881387
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039405"
---
# <a name="message-correlation"></a>메시지 상관 관계
이 샘플은 메시지 큐 (MSMQ) 응용 프로그램에서 WCF (Windows Communication Foundation) 서비스로 MSMQ 메시지를 보내는 방법과 요청/응답 시나리오에서 보낸 사람과 받는 사람 응용 프로그램 간에 메시지를 상호 연결 하는 방법을 보여 줍니다. 이 샘플에서는 msmqIntegrationBinding 바인딩을 사용합니다. 이 경우 서비스는 자체 호스팅 콘솔 애플리케이션으로, 이를 사용하여 대기 중인 메시지를 받는 서비스를 확인할 수 있습니다. k  
  
 서비스는 발신자로부터 받은 메시지를 처리하여 발신자에게 응답 메시지를 보냅니다. 발신자는 받은 응답을 원래 보낸 요청에 상호 연결합니다. 메시지의 `MessageID` 속성과 `CorrelationID` 속성은 요청 메시지와 응답 메시지를 상호 연결하는 데 사용됩니다.  
  
 `IOrderProcessor` 서비스 계약은 큐에 사용하기 적합한 단방향 서비스 작업을 정의합니다. MSMQ 메시지에는 동작 헤더가 없기 때문에 여러 MSMQ 메시지를 작업 계약에 자동으로 매핑할 수 없습니다. 따라서 이 경우에는 한 작업 계약만 있을 수 있습니다. 서비스에 좀더 많은 작업 계약을 정의하려는 경우 애플리케이션은 발송할 작업 계약을 결정하는 데 사용할 수 있는 MSMQ 메시지의 헤더에 대한 정보(예: 레이블 또는 correlationID)를 제공해야 합니다. 
  
 MSMQ 메시지에는 작업 계약의 다른 매개 변수에 매핑되는 헤더에 대한 정보도 포함되지 않습니다. 따라서 작업 계약에는 한 매개 변수만 있을 수 있습니다. 매개 변수는 내부 MSMQ <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>메시지를 포함 하는 형식입니다. `MsmqMessage<T>` 클래스의 "T" 형식은 MSMQ 메시지 본문에 serialize되는 데이터를 나타냅니다. 이 샘플에서는 `PurchaseOrder` 형식이 MSMQ 메시지 본문으로 serialize됩니다.  

```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
[ServiceKnownType(typeof(PurchaseOrder))]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true, Action = "*")]
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);
}
```

 서비스 작업을 통해 구매 주문을 처리하고 구매 주문의 내용과 상태를 서비스 콘솔 창에 표시합니다. <xref:System.ServiceModel.OperationBehaviorAttribute>를 통해 트랜잭션에 작업을 큐로 나열하고 작업이 반환되면 트랜잭션이 완료된 것으로 표시하도록 구성합니다. `PurchaseOrder`에는 서비스에서 처리해야 할 주문 세부 정보가 포함되어 있습니다.

```csharp
// Service class that implements the service contract.
public class OrderProcessorService : IOrderProcessor
{
   [OperationBehavior(TransactionScopeRequired = true,
          TransactionAutoComplete = true)]
   public void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> ordermsg)
   {
       PurchaseOrder po = (PurchaseOrder)ordermsg.Body;
       Random statusIndexer = new Random();
       po.Status = PurchaseOrder.OrderStates[statusIndexer.Next(3)];
       Console.WriteLine("Processing {0} ", po);
       //Send a response to the client that the order has been received
         and is pending fullfillment.
       SendResponse(ordermsg);
    }

    private void SendResponse(MsmqMessage<PurchaseOrder> ordermsg)
    {
        OrderResponseClient client = new OrderResponseClient("OrderResponseEndpoint");

        //Set the correlation ID such that the client can correlate the response to the order.
        MsmqMessage<PurchaseOrder> orderResponsemsg = new MsmqMessage<PurchaseOrder>(ordermsg.Body);
        orderResponsemsg.CorrelationId = ordermsg.Id;
        using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
        {
            client.SendOrderResponse(orderResponsemsg);
            scope.Complete();
        }

        client.Close();
    }
}
```

 서비스는 사용자 지정 클라이언트 `OrderResponseClient`를 사용하여 MSMQ 메시지를 큐에 보냅니다. 메시지를 수신 하 고 처리 하는 응용 프로그램은 WCF 응용 프로그램이 아니라 MSMQ 응용 프로그램 이므로 두 응용 프로그램 간에 암시적 서비스 계약이 없습니다. 따라서 이 시나리오에서는 Svcutil.exe 도구를 사용하여 프록시를 만들 수 없습니다.

 사용자 지정 프록시는 `msmqIntegrationBinding` 바인딩을 사용 하 여 메시지를 보내는 모든 WCF 응용 프로그램에 대해 기본적으로 동일 합니다. 하지만 다른 프록시와 달리 사용자 지정 프록시에는 일정 범위의 서비스 작업이 포함되지 않습니다. 메시지 제출 작업으로만 한정됩니다.

```csharp
[System.ServiceModel.ServiceContractAttribute(Namespace = "http://Microsoft.ServiceModel.Samples")]
public interface IOrderResponse
{

    [System.ServiceModel.OperationContractAttribute(IsOneWay = true, Action = "*")]
    void SendOrderResponse(MsmqMessage<PurchaseOrder> msg);
}

public partial class OrderResponseClient : System.ServiceModel.ClientBase<IOrderResponse>, IOrderResponse
{

    public OrderResponseClient()
    { }

    public OrderResponseClient(string configurationName)
        : base(configurationName)
    { }

    public OrderResponseClient(System.ServiceModel.Channels.Binding binding, System.ServiceModel.EndpointAddress address)
        : base(binding, address)
    { }

    public void SendOrderResponse(MsmqMessage<PurchaseOrder> msg)
    {
        base.Channel.SendOrderResponse(msg);
    }
}
```

 서비스는 자체 호스트됩니다. MSMQ 통합 전송을 사용하는 경우에는 사용되는 큐를 미리 만들어야 합니다. 수동으로 또는 코드를 통해 이 작업을 수행할 수 있습니다. 이 샘플의 서비스에는 큐가 있는지 확인하고 필요한 경우 만드는 <xref:System.Messaging> 코드가 포함되어 있습니다. 큐 이름은 구성 파일에서 읽습니다.

```csharp
public static void Main()
{
       // Get the MSMQ queue name from application settings in configuration.
      string queueName =
                ConfigurationManager.AppSettings["orderQueueName"];
      // Create the transacted MSMQ queue if necessary.
      if (!MessageQueue.Exists(queueName))
                MessageQueue.Create(queueName, true);
     // Create a ServiceHost for the OrderProcessorService type.
     using (ServiceHost serviceHost = new
                   ServiceHost(typeof(OrderProcessorService)))
     {
            serviceHost.Open();
            // The service can now be accessed.
            Console.WriteLine("The service is ready.");
            Console.WriteLine("Press <ENTER> to terminate service.");
            Console.ReadLine();
            // Close the ServiceHost to shutdown the service.
            serviceHost.Close();
      }
}
```

 주문 요청을 받는 MSMQ 큐는 구성 파일의 appSettings 섹션에 지정됩니다. 클라이언트 엔드포인트와 서비스 엔드포인트는 구성 파일의 system.serviceModel 섹션에 정의됩니다. 둘 다 `msmqIntegrationbinding` 바인딩을 지정합니다.

```xml
<appSettings>
  <add key="orderQueueName" value=".\private$\Orders" />
</appSettings>

<system.serviceModel>
  <client>
    <endpoint    name="OrderResponseEndpoint"
              address="msmq.formatname:DIRECT=OS:.\private$\OrderResponse"
              binding="msmqIntegrationBinding"
              bindingConfiguration="OrderProcessorBinding"
              contract="Microsoft.ServiceModel.Samples.IOrderResponse">
    </endpoint>
  </client>

  <services>
    <service
      name="Microsoft.ServiceModel.Samples.OrderProcessorService">
      <endpoint address="msmq.formatname:DIRECT=OS:.\private$\Orders"
                            binding="msmqIntegrationBinding"
                bindingConfiguration="OrderProcessorBinding"
                contract="Microsoft.ServiceModel.Samples.IOrderProcessor">
      </endpoint>
    </service>
  </services>

  <bindings>
    <msmqIntegrationBinding>
      <binding name="OrderProcessorBinding" >
        <security mode="None" />
      </binding>
    </msmqIntegrationBinding>
  </bindings>

</system.serviceModel>
```

 클라이언트 애플리케이션은 <xref:System.Messaging>을 사용하여 지속적인 메시지와 트랜잭션 메시지를 큐로 보냅니다. 메시지 본문에는 구매 주문이 포함됩니다.

```csharp
static void PlaceOrder()
{
    //Connect to the queue
    MessageQueue orderQueue =
            new MessageQueue(
                    ConfigurationManager.AppSettings["orderQueueName"])
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

    Message msg = new Message();
    msg.UseDeadLetterQueue = true;
    msg.Body = po;

    //Create a transaction scope.
    using (TransactionScope scope = new
     TransactionScope(TransactionScopeOption.Required))
    {
        // Submit the purchase order.
        orderQueue.Send(msg, MessageQueueTransactionType.Automatic);
        // Complete the transaction.
        scope.Complete();
    }
    //Save the messageID for order response correlation.
    orderMessageID = msg.Id;
    Console.WriteLine("Placed the order, waiting for response...");
}
```

 주문 응답을 받는 MSMQ 큐는 다음 샘플 구성에 표시된 것처럼 구성 파일의 appSettings 섹션에 지정됩니다.

> [!NOTE]
> 큐 이름은 로컬 컴퓨터에 점(.)을, 그 경로에는 백슬래시 구분 기호를 사용합니다. WCF 끝점 주소는 msmq.formatname 체계를 지정 하며 로컬 컴퓨터에 대해 "localhost"를 사용 합니다. 적절한 형식의 형식 이름은 MSMQ 지침에 따라 URI에서 msmq.formatname을 따릅니다.

```xml
<appSettings>
    <add key=" orderResponseQueueName" value=".\private$\Orders" />
</appSettings>
```

 클라이언트 애플리케이션은 서비스로 보내는 주문 요청 메시지의 `messageID`를 저장하고 서비스의 응답을 기다립니다. 큐에 응답이 도착하면 클라이언트는 메시지의 `correlationID` 속성을 사용하여 보낸 주문 메시지와 응답 메시지를 상호 연결합니다. 여기에는 클라이언트에서 원래 서비스로 보낸 주문 메시지의 `messageID`가 포함되어 있습니다.

```csharp
static void DisplayOrderStatus()
{
    MessageQueue orderResponseQueue = new
     MessageQueue(ConfigurationManager.AppSettings
                  ["orderResponseQueueName"]);
    //Create a transaction scope.
    bool responseReceived = false;
    orderResponseQueue.MessageReadPropertyFilter.CorrelationId = true;
    while (!responseReceived)
    {
       Message responseMsg;
       using (TransactionScope scope2 = new
         TransactionScope(TransactionScopeOption.Required))
       {
          //Receive the Order Response message.
          responseMsg =
              orderResponseQueue.Receive
                   (MessageQueueTransactionType.Automatic);
          scope2.Complete();
     }
     responseMsg.Formatter = new
     System.Messaging.XmlMessageFormatter(new Type[] {
         typeof(PurchaseOrder) });
     PurchaseOrder responsepo = (PurchaseOrder)responseMsg.Body;
    //Check if the response is for the order placed.
    if (orderMessageID == responseMsg.CorrelationId)
    {
       responseReceived = true;
       Console.WriteLine("Status of current Order: OrderID-{0},Order
            Status-{1}", responsepo.PONumber, responsepo.Status);
    }
    else
    {
       Console.WriteLine("Status of previous Order: OrderID-{0},Order
            Status-{1}", responsepo.PONumber, responsepo.Status);
    }
  }
}
```

 샘플을 실행하면 클라이언트 및 서비스 동작이 서비스 콘솔 창과 클라이언트 콘솔 창에 모두 표시됩니다. 클라이언트의 서비스 수신 메시지를 확인하고 클라이언트로 다시 응답을 보낼 수 있습니다. 클라이언트는 서비스로부터 받은 응답을 표시합니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다.

> [!NOTE]
> 이 샘플을 사용하려면 MSMQ(메시지 큐)를 설치해야 합니다. 참고 항목 단원의 MSMQ 설치 지침을 참조하십시오.

### <a name="to-setup-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. 서비스가 처음 실행되는 경우 서비스에서는 큐가 있는지 확인하고 큐가 없으면 큐를 만듭니다. 서비스를 처음 실행하여 큐를 만들거나 MSMQ 큐 관리자를 통해 큐를 만들 수 있습니다. Windows 2008에서 큐를 만들려면 다음 단계를 수행하세요.

    1. Visual Studio 2012에서 서버 관리자를 엽니다.

    2. **기능** 탭을 확장 합니다.

    3. **개인 메시지 큐**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**, **개인 큐**를 선택 합니다.

    4. **트랜잭션** 상자를 확인 합니다.

    5. 새 `ServiceModelSamplesTransacted` 큐의 이름으로을 입력 합니다.

3. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

4. 단일 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

### <a name="to-run-the-sample-across-computers"></a>다중 컴퓨터 구성에서 샘플을 실행하려면

1. 언어별 폴더의 \service\bin\ 폴더에서 서비스 컴퓨터로 서비스 프로그램 파일을 복사합니다.

2. 언어별 폴더의 \client\bin\ 폴더에서 클라이언트 프로그램 파일을 클라이언트 컴퓨터로 복사합니다.

3. Client.exe.config 파일에서 orderQueueName을 변경하여 "." 대신 서비스 컴퓨터 이름을 지정합니다.

4. Service.exe.config 파일에서 클라이언트 엔드포인트 주소를 변경하여 "." 대신 클라이언트 컴퓨터 이름을 지정합니다.

5. 서비스 컴퓨터의 명령 프롬프트에서 Service.exe를 실행합니다.

6. 클라이언트 컴퓨터의 명령 프롬프트에서 Client.exe를 실행합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\MessageCorrelation`  
  
## <a name="see-also"></a>참고자료

- [WCF의 큐](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)
- [메시지 큐](https://go.microsoft.com/fwlink/?LinkId=94968)
