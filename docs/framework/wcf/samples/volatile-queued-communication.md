---
title: 일시 대기 통신
ms.date: 03/30/2017
ms.assetid: 0d012f64-51c7-41d0-8e18-c756f658ee3d
ms.openlocfilehash: ad29efb2c2b22945cda09f3aecc57ef50ed97f5f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62006332"
---
# <a name="volatile-queued-communication"></a>일시 대기 통신

이 샘플에서는 MSMQ(메시지 큐) 전송을 통해 일시 대기 중인 통신을 수행하는 방법을 보여 줍니다. 이 샘플에서는 <xref:System.ServiceModel.NetMsmqBinding>을 사용합니다. 이 경우의 서비스는 자체 호스팅 콘솔 애플리케이션이며 이를 사용하여 서비스에서 대기 중인 메시지를 받는 것을 관찰할 수 있습니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

대기 중인 통신에서 클라이언트는 큐를 사용하여 서비스와 통신합니다. 좀더 정확하게 말하면 클라이언트는 큐에 메시지를 보내고, 서비스는 큐에서 보낸 메시지를 받습니다. 따라서 서비스와 클라이언트가 동시에 실행되고 있지 않더라도 큐를 사용하여 통신할 수 있습니다.

보증 없이 메시지를 보내는 경우 ExactlyOnce 보증과 달리 MSMQ는 메시지를 배달하기 위해 최선의 노력을 다합니다. MSMQ는 메시지가 배달되었는지 확인하고, 배달할 수 없으면 이를 알린다는 점에서 ExactlyOnce 보증과 다릅니다.

일부 시나리오에서는 메시지가 손실되는지 여부보다 적시에 전달되는지가 더 중요한 경우 큐를 통해 보증 없이 일시적 메시지를 보낼 수도 있습니다. 큐 관리자의 작동이 중단되는 경우 일시적 메시지는 보존되지 않습니다. 따라서 큐 관리자가 충돌하면 일시 메시지의 저장에 사용된 비트랜잭션 큐는 보존되지만 메시지는 디스크에 저장되지 않기 때문에 보존되지 않습니다.

> [!NOTE]
> MSMQ를 사용하여 트랜잭션 범위 내에서 보증이 없는 일시 메시지를 보낼 수는 없습니다. 또한 일시 메시지를 보내려면 비트랜잭션 큐를 만들어야 합니다.

이 샘플에서 서비스 계약은 큐에서 사용하기에 가장 적합한 단방향 서비스를 정의하는 `IStockTicker`입니다.

```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
public interface IStockTicker
{
    [OperationContract(IsOneWay = true)]
    void StockTick(string symbol, float price);
}
```

서비스 작업에서는 다음 샘플 코드에 표시된 것과 같이 주식 기호와 주가를 표시합니다.

```csharp
public class StockTickerService : IStockTicker
{
    public void StockTick(string symbol, float price)
    {
        Console.WriteLine("Stock Tick {0}:{1} ", symbol, price);
     }
     …
}
```

서비스는 자체 호스트됩니다. MSMQ 전송을 사용하는 경우에는 사용되는 큐를 미리 만들어야 합니다. 수동으로 또는 코드를 통해 이 작업을 수행할 수 있습니다. 이 샘플에서 서비스에는 큐가 있는지 확인하고 필요한 경우 큐를 만드는 코드가 포함되어 있습니다. 큐 이름은 구성 파일에서 읽습니다. 기본 주소를 사용 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 서비스용 프록시를 생성 합니다.

```csharp
// Host the service within this EXE console application.
public static void Main()
{
    // Get MSMQ queue name from app settings in configuration.
    string queueName = ConfigurationManager.AppSettings["queueName"];

    // Create the transacted MSMQ queue if necessary.
    if (!MessageQueue.Exists(queueName))
        MessageQueue.Create(queueName);

    // Create a ServiceHost for the StockTickerService type.
    using (ServiceHost serviceHost = new ServiceHost(typeof(StockTickerService)))
    {
        // Open the ServiceHost to create listeners and start listening for messages.
        serviceHost.Open();

        // The service can now be accessed.
        Console.WriteLine("The service is ready.");
        Console.WriteLine("Press <ENTER> to terminate service.");
        Console.WriteLine();
        Console.ReadLine();

        // Close the ServiceHost to shutdown the service.
        serviceHost.Close();
    }
}
```

MSMQ 큐 이름은 구성 파일의 appSettings 섹션에 지정됩니다. 서비스의 엔드포인트는 구성 파일의 system.serviceModel 섹션에 정의되며 `netMsmqBinding` 바인딩을 지정합니다.

> [!NOTE]
> <xref:System.Messaging>을 사용하여 큐를 만들 때 큐 이름은 로컬 컴퓨터에 점(.)을, 그 경로에는 백슬래시 구분 기호를 사용합니다. Windows Communication Foundation (WCF) 끝점 주소에서는 net.msmq 지정: 체계, "localhost"는 로컬 컴퓨터 및 해당 경로에 슬래시를 사용 합니다.

메시지의 보증과 함께 메시지가 지속적인지 또는 일시적인지도 구성에서 지정합니다.

```xml
<appSettings>
  <!-- use appSetting to configure MSMQ queue name -->
  <add key="queueName" value=".\private$\ServiceModelSamplesVolatile" />
</appSettings>

<system.serviceModel>
  <services>
    <service name="Microsoft.ServiceModel.Samples.StockTickerService"
             behaviorConfiguration="CalculatorServiceBehavior">
    ...
      <!-- Define NetMsmqEndpoint -->
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesVolatile"
                binding="netMsmqBinding"
                bindingConfiguration="volatileBinding"
                contract="Microsoft.ServiceModel.Samples.IStockTicker" />
    ...
    </service>
  </services>

  <bindings>
    <netMsmqBinding>
      <binding name="volatileBinding"
             durable="false"
           exactlyOnce="false"/>
    </netMsmqBinding>
  </bindings>
  ...
</system.serviceModel>
```

샘플에서 비트랜잭션 큐를 사용하여 대기 중인 메시지를 보내기 때문에 트랜잭션된 메시지를 큐로 보낼 수 없습니다.

```csharp
// Create a client.
Random r = new Random(137);

StockTickerClient client = new StockTickerClient();

float price = 43.23F;
for (int i = 0; i < 10; i++)
{
    float increment = 0.01f * (r.Next(10));
    client.StockTick("zzz" + i, price + increment);
}

//Closing the client gracefully cleans up resources.
client.Close();
```

샘플을 실행하면 클라이언트 및 서비스 동작이 서비스 콘솔 창과 클라이언트 콘솔 창에 모두 표시됩니다. 서비스에서 클라이언트가 보내는 메시지를 받는 것을 볼 수 있습니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다. 큐를 사용하므로 클라이언트와 서비스가 동시에 실행 중일 필요는 없습니다. 클라이언트를 실행하고 종료한 다음 서비스를 다시 시작해도 서비스에서 계속 메시지를 받을 수 있습니다.

```
The service is ready.
Press <ENTER> to terminate service.

Stock Tick zzz0:43.25
Stock Tick zzz1:43.23
Stock Tick zzz2:43.28
Stock Tick zzz3:43.3
Stock Tick zzz4:43.23
Stock Tick zzz5:43.25
Stock Tick zzz6:43.25
Stock Tick zzz7:43.24
Stock Tick zzz8:43.32
Stock Tick zzz9:43.3
```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

3. 단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.

기본적으로 <xref:System.ServiceModel.NetMsmqBinding>을 사용하여 전송 보안이 설정됩니다. MSMQ 전송 보안에 대 한 관련 속성을 두 가지 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> 하 고 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> `.` 기본적으로 인증 모드 설정 `Windows` 보호 수준이 설정 및 `Sign`합니다. MSMQ에서 인증 및 서명 기능을 제공하려면 도메인에 속해 있어야 하며 MSMQ의 Active Directory 통합 옵션이 설치되어 있어야 합니다. 이 기준에 맞지 않는 컴퓨터에서 이 샘플을 실행하면 오류가 발생합니다.

### <a name="to-run-the-sample-on-a-computer-joined-to-a-workgroup-or-without-active-directory-integration"></a>작업 그룹에 속해 있거나 Active Directory 통합이 없는 컴퓨터에서 샘플을 실행하려면

1. 컴퓨터가 도메인에 속해 있지 않거나 Active Directory 통합이 설치되어 있지 않은 경우에는 다음 샘플 구성 코드에 표시된 것과 같이 인증 모드와 보호 수준을 `None`으로 설정하여 전송 보안을 끕니다.

    ```xml
    <system.serviceModel>
        <services>
          <service name="Microsoft.ServiceModel.Samples.StockTickerService"
                   behaviorConfiguration="StockTickerServiceBehavior">
            <host>
              <baseAddresses>
                <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>
              </baseAddresses>
            </host>

            <!-- Define NetMsmqEndpoint -->
            <endpoint address="net.msmq://localhost/private/ServiceModelSamplesVolatile"
                      binding="netMsmqBinding"
                      bindingConfiguration="volatileBinding"
                      contract="Microsoft.ServiceModel.Samples.IStockTicker" />
            <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->
            <endpoint address="mex"
                      binding="mexHttpBinding"
                      contract="IMetadataExchange" />

          </service>
        </services>

        <bindings>
          <netMsmqBinding>
            <binding name="volatileBinding"
                  durable="false"
                  exactlyOnce="false">
              <security mode="None" />
            </binding>
          </netMsmqBinding>
        </bindings>

        <behaviors>
          <serviceBehaviors>
            <behavior name="StockTickerServiceBehavior">
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Volatile`
