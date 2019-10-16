---
title: 단일 ListenUri의 여러 엔드포인트
ms.date: 03/30/2017
ms.assetid: 911ffad4-4d47-4430-b7c2-79192ce6bcbd
ms.openlocfilehash: 8e514b28d9b3719a52d420551c607c49c70738e1
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044842"
---
# <a name="multiple-endpoints-at-a-single-listenuri"></a>단일 ListenUri의 여러 엔드포인트
이 샘플에서는 단일 `ListenUri`에서 여러 엔드포인트를 호스팅하는 서비스를 보여 줍니다. 이 샘플은 계산기 서비스를 구현 하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md) 을 기반으로 합니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 [여러 끝점](../../../../docs/framework/wcf/samples/multiple-endpoints.md) 샘플에서 볼 수 있듯이 서비스는 각각 서로 다른 주소를 사용 하는 여러 끝점 및 다른 바인딩을 호스트할 수 있습니다. 이 샘플에서는 동일한 주소에서 여러 엔드포인트를 호스팅할 수 있다는 것을 보여 줍니다. 또한 이 샘플에서는 서비스 엔드포인트가 가지는 두 종류의 주소인 `EndpointAddress` 및 `ListenUri` 간의 차이점을 보여 줍니다.  
  
 `EndpointAddress`는 서비스의 논리 주소입니다. SOAP 메시지의 주소가 이 주소로 지정됩니다. `ListenUri`는 서비스의 실제 주소입니다. 서비스 엔드포인트가 현재 컴퓨터에서 메시지를 실제로 수신 대기하는 포트 및 주소 정보가 이 주소에 포함됩니다. 대부분의 경우 이러한 주소는 다를 필요가 없습니다. `ListenUri`가 명시적으로 지정되지 않은 경우 엔드포인트의 `EndpointAddress`의 URI가 기본값으로 사용됩니다. 라우터를 구성하는 경우와 같은 일부 상황에서는 여러 다른 서비스로 주소가 지정된 메시지를 수락할 수 있도록 이러한 주소를 구별하는 것이 유용합니다.  
  
## <a name="service"></a>서비스  
 이 샘플의 서비스에는 두 개의 계약인 `ICalculator` 및 `IEcho`가 있습니다. 다음 코드에 표시된 것처럼 일반적인 `IMetadataExchange` 엔드포인트 외에도 세 개의 애플리케이션 엔드포인트가 있습니다.  
  
```xml  
<endpoint address="urn:Stuff"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.ICalculator"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
<endpoint address="urn:Stuff"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IEcho"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
<endpoint address="urn:OtherEcho"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IEcho"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
```  
  
 세 개의 엔드포인트는 모두 동일한 `ListenUri`에서 호스팅되고 동일한 `binding`을 사용합니다. 동일한 `ListenUri`에 있는 엔드포인트는 컴퓨터의 해당 실제 주소에서 메시지를 수신 대기하는 단일 채널 스택을 공유하므로 동일한 바인딩을 가져야 합니다. 각 엔드포인트의 `address`는 URN입니다. 일반적으로 주소가 실제 위치를 나타내지만 이 샘플에 나온 것처럼 실제로 이 주소는 일치 및 필터링 목적에 사용되므로 모든 종류의 URI가 될 수 있습니다.  
  
 3 개의 끝점이 모두 동일한 `ListenUri`를 공유 하기 때문에 메시지가 도착할 때 WCF (Windows Communication Foundation)는 메시지를 보낼 끝점을 결정 해야 합니다. 각 엔드포인트에는 주소 필터와 계약 필터의 두 부분으로 구성된 메시지 필터가 있습니다. 주소 필터는 SOAP 메시지의 `To`를 서비스 엔드포인트의 주소에 일치시킵니다. 예를 들어, `To "Urn:OtherEcho"`에 주소 지정된 메시지만 이 서비스의 세 번째 엔드포인트의 후보가 됩니다. 계약 필터는 특정 계약의 작업과 연관된 작업을 일치시킵니다. 예를 들면 `IEcho`의 작업을 가진 메시지입니다. 이 서비스의 두 번째 및 세 번째 엔드포인트가 `Echo` 계약을 호스팅하기 때문에 `IEcho`는 이러한 두 엔드포인트 모두의 계약 필터를 일치시킵니다.  
  
 따라서 주소 필터와 계약 필터를 조합하면 이 서비스의 `ListenUri`에 도착하는 각 메시지를 올바른 엔드포인트에 라우트할 수 있습니다. 세 번째 엔드포인트는 다른 엔드포인트에서 다른 주소로 보내진 메시지를 수락하기 때문에 다른 두 개와 구별됩니다. 첫 번째 및 두 번째 엔드포인트는 해당 계약(들어오는 메시지의 작업)에 기초하여 서로 구별됩니다.  
  
## <a name="client"></a>클라이언트  
 서버의 엔드포인트가 두 개의 다른 주소를 가진 것처럼 클라이언트 엔드포인트도 두 개의 주소를 가집니다. 서버 및 클라이언트 모두에서 논리 주소를 `EndpointAddress`라고 합니다. 그러나 서버에서 물리 주소를 `ListenUri`라고 하는 것과 달리 클라이언트에서는 물리 주소를 `Via`라고 합니다.  
  
 서버에서와 같이 기본적으로 이러한 두 주소는 동일합니다. 엔드포인트 주소와 다른 클라이언트의 `Via`를 지정하려면 `ClientViaBehavior`를 사용합니다.  
  
```csharp  
Uri via = new Uri("http://localhost/ServiceModelSamples/service.svc");  
CalculatorClient calcClient = new CalculatorClient();  
calcClient.ChannelFactory.Endpoint.Behaviors.Add(  
        new ClientViaBehavior(via));  
```  
  
 일반적인 경우와 같이 주소는 Svcutil.exe에 의해 생성된 클라이언트 구성 파일에서 제공됩니다. 서비스의 `Via`에 해당하는 `ListenUri`는 서비스의 메타데이터에 나타나지 않으므로 이 정보는 서비스의 메타데이터 주소와 같이 out-of-band로 클라이언트에 전달되어야 합니다.  
  
 이 샘플에서 클라이언트는 서버의 세 개 엔드포인트가 모두 동일한 `Via`를 가진 경우에도 이러한 엔드포인트와 통신하고 구별할 수 있다는 것을 보여 주기 위해 각 엔드포인트에 메시지를 보냅니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
    > [!NOTE]
    > 다중 컴퓨터 구성의 경우 Client.cs 파일의 localhost를 서비스 컴퓨터의 이름으로 대체해야 합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\MultipleEndpointsSingleUri`  
