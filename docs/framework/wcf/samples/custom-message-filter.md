---
title: 사용자 지정 메시지 필터
ms.date: 03/30/2017
ms.assetid: 98dd0af8-fce6-4255-ac32-42eb547eea67
ms.openlocfilehash: 30405800cd219f56fcc08b8e8d22f4fe0b907e32
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928697"
---
# <a name="custom-message-filter"></a>사용자 지정 메시지 필터
이 샘플에서는 WCF (Windows Communication Foundation)에서 메시지를 끝점으로 디스패치할 때 사용 하는 메시지 필터를 대체 하는 방법을 보여 줍니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 채널의 첫 번째 메시지가 서버에 도착하면 서버에서는 해당 URI에 연결된 엔드포인트 중에서 해당 메시지를 받을 엔드포인트(있는 경우)를 결정해야 합니다. 이 프로세스는 <xref:System.ServiceModel.Dispatcher.MessageFilter>에 연결된 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> 개체에 의해 제어됩니다.  
  
 서비스의 각 엔드포인트에는 단일 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>가 있습니다. <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>에는 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>와 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>가 모두 있습니다. 이러한 두 필터를 결합하면 해당 엔드포인트에 사용된 메시지 필터가 됩니다.  
  
 기본적으로 엔드포인트에 대한 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>는 서비스 엔드포인트의 <xref:System.ServiceModel.EndpointAddress>와 일치하는 주소로 해당 주소가 지정된 모든 메시지와 일치합니다. 기본적으로 끝점에 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> 대 한는 들어오는 메시지의 동작을 검사 하 고 서비스 끝점 계약 `IsInitiating` = `true`의작업중하나에해당하는작업과모든메시지를일치시킵니다.작업을 고려 합니다. 따라서 기본적으로 엔드포인트에 대한 필터는 두 메시지의 받는 사람 헤더가 엔드포인트의 <xref:System.ServiceModel.EndpointAddress>인 경우에만 일치하고 메시지의 동작은 엔드포인트 작업의 동작 중 하나와 일치합니다.  
  
 이러한 필터는 동작을 사용하여 변경할 수 있습니다. 이 샘플에서 서비스는 <xref:System.ServiceModel.Description.IEndpointBehavior>의 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>와 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>를 대체하는 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>를 만듭니다.  
  
```csharp
class FilteringEndpointBehavior : IEndpointBehavior
{
    //...
}
```  
  
 다음과 같이 두 개의 주소 필터가 정의됩니다.  
  
```csharp  
// Matches any message whose To address contains the letter 'e'  
class MatchEAddressFilter : MessageFilter …  
// Matches any message whose To address does not contain the letter 'e'  
class MatchNoEAddressFilter : MessageFilter  
```  
  
 `FilteringEndpointBehavior`는 구성 가능하며 두 가지 다른 변형에 대해 허용됩니다.  
  
```csharp  
public class FilteringEndpointBehaviorExtension : BehaviorExtensionElement  
```  
  
 변형 1에서는 'e'를 포함하지만 동작이 있는 주소만 일치하고 변형 2에서는 'e'가 없는 주소만 일치합니다.  
  
```csharp  
if (Variation == 1)  
    return new FilteringEndpointBehavior(  
        new MatchEAddressFilter(), new MatchAllMessageFilter());  
else  
    return new FilteringEndpointBehavior(  
        new MatchNoEAddressFilter(), new MatchAllMessageFilter());  
```  
  
 구성 파일에서 서비스는 새 동작을 등록합니다.  
  
```xml  
<extensions>  
    <behaviorExtensions>  
        <add name="filteringEndpointBehavior" type="Microsoft.ServiceModel.Samples.FilteringEndpointBehaviorExtension, service" />  
    </behaviorExtensions>  
</extensions>      
```  
  
 그런 다음 서비스에서는 각 변형에 대한 `endpointBehavior` 구성을 만듭니다.  
  
```xml  
<endpointBehaviors>  
    <behavior name="endpoint1">  
        <filteringEndpointBehavior variation="1" />  
    </behavior>  
    <behavior name="endpoint2">  
        <filteringEndpointBehavior variation="2" />  
    </behavior>  
</endpointBehaviors>  
```  
  
 마지막으로 서비스의 엔드포인트는 `behaviorConfigurations` 중 하나를 참조합니다.  
  
```xml  
<endpoint address=""  
        bindingConfiguration="ws"  
        listenUri=""   
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IHello"   
        behaviorConfiguration="endpoint2" />  
```  
  
 클라이언트 애플리케이션의 구현은 간단합니다. 이 구현에서는 서비스의 URI에 대한 채널 두 개를 만들고 해당 값을 두 번째 `via` 매개 변수로 <xref:System.ServiceModel.Channels.IChannelFactory%601.CreateChannel%28System.ServiceModel.EndpointAddress%29>에 전달함으로써 각 채널에서 단일 메시지를 보냅니다. 그러나 각각 다른 엔드포인트 주소를 사용합니다. 따라서 클라이언트의 아웃바운드 메시지에는 다른 받는 사람이 지정되고 클라이언트의 출력에 표시된 대로 서버는 그에 따라 응답합니다.  
  
```console  
Sending message to urn:e...  
Exception: The message with To 'urn:e' cannot be processed at the receiver, due to an AddressFilter mismatch at the EndpointDispatcher.  Check that the sender and receiver's EndpointAddresses agree.  
  
Sending message to urn:a...  
Hello  
```  
  
 서버의 구성 파일에서 변형을 전환하면 필터가 대체되고 클라이언트에 반대 동작이 표시됩니다. 즉, `urn:e`에 대한 메시지는 성공하고 `urn:a`에 대한 메시지는 실패합니다.  
  
```xml  
<endpoint address=""  
          bindingConfiguration="ws"  
          listenUri=""   
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.IHello"   
          behaviorConfiguration="endpoint1" />  
```  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageFilter`  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
2. 단일 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
3. 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md) 의 지침을 따르고 Client.cs에서 다음 줄을 변경 합니다.  
  
    ```csharp  
    Uri serviceVia = new Uri("http://localhost/ServiceModelSamples/service.svc");  
    ```  
  
     localhost를 서버 이름으로 바꿉니다.  
  
    ```csharp  
    Uri serviceVia = new Uri("http://servermachinename/ServiceModelSamples/service.svc");  
    ```  
