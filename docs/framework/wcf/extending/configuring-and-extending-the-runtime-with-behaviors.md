---
title: 동작을 사용하여 런타임 구성 및 확장
ms.date: 03/30/2017
helpviewer_keywords:
- attaching extensions using behaviors [WCF]
ms.assetid: 149b99b6-6eb6-4f45-be22-c967279677d9
ms.openlocfilehash: 707b365a0f64055497e6b8814633acf7f4d7097c
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200061"
---
# <a name="configuring-and-extending-the-runtime-with-behaviors"></a>동작을 사용하여 런타임 구성 및 확장
동작을 사용 하 여 기본 동작을 수정 하 고 검사 하 고 서비스 구성의 유효성을 검사 하거나 Windows Communication Foundation (WCF) 클라이언트와 서비스 응용 프로그램에서 런타임 동작을 수정 하는 사용자 지정 확장을 추가할 수 있습니다. 이 항목에서는 동작 인터페이스에 대해 설명하고 이를 구현하는 방법 및 프로그래밍 방식이나 구성 파일을 통해 서비스 응용 프로그램의 서비스 설명 또는 클라이언트 응용 프로그램의 엔드포인트에 추가하는 방법에 대해 설명합니다. 시스템 제공 동작 사용에 대 한 자세한 내용은 참조 하십시오 [서비스 런타임 동작 지정](../../../../docs/framework/wcf/specifying-service-run-time-behavior.md) 하 고 [클라이언트 런타임 동작 지정](../../../../docs/framework/wcf/specifying-client-run-time-behavior.md)합니다.  
  
## <a name="behaviors"></a>동작  
 동작 형식이 서비스 또는 서비스 끝점 설명 개체에 추가 됩니다 (서비스 또는 클라이언트에서 각각) 전에 개체만 Windows Communication Foundation (WCF)에서 WCF 서비스 또는 WCF 클라이언트를 실행 하는 런타임을 만드는 데 사용 됩니다. 런타임 생성이 처리되는 동안 이러한 동작이 호출되면 동작은 계약, 바인딩 및 주소에 의해 생성된 런타임을 수정하는 메서드 및 런타임 속성에 액세스할 수 있습니다.  
  
### <a name="behavior-methods"></a>동작 메서드  
 모든 동작에는 `AddBindingParameters` 메서드, `ApplyDispatchBehavior` 메서드, `Validate` 메서드 및 `ApplyClientBehavior` 메서드가 있지만, 한 가지 예외가 있습니다. <xref:System.ServiceModel.Description.IServiceBehavior>는 클라이언트에서 실행되지 않기 때문에 `ApplyClientBehavior`를 구현하지 못합니다.  
  
-   런타임 생성 시 사용자 지정 개체를 사용하기 위해 이러한 개체를 사용자 지정 바인딩에서 액세스할 수 있는 컬렉션에 추가하거나 수정하려면 `AddBindingParameters` 메서드를 사용합니다. 예를 들어 보호 요구 사항에 지정된 내용은 채널 빌드 방식에 영향을 주지만 채널 개발자는 이를 모릅니다.  
  
-   설명 트리와 해당 런타임 개체를 검사하여 일부 조건에 부합하는지 확인하려면 `Validate` 메서드를 사용합니다.  
  
-   서비스나 클라이언트의 특정 범위에 대해 런타임을 수정하고 설명 트리를 검사하려면 `ApplyDispatchBehavior` 및 `ApplyClientBehavior` 메서드를 사용합니다. 확장 개체도 삽입할 수 있습니다.  
  
    > [!NOTE]
    >  이러한 메서드에 제공되는 설명 트리는 검사용입니다. 설명 트리가 수정되면 동작이 정의되지 않습니다.  
  
 서비스 및 클라이언트 런타임 클래스를 통해, 수정할 수 있는 속성과 구현할 수 있는 사용자 지정 인터페이스에 액세스합니다. 서비스 유형은 <xref:System.ServiceModel.Dispatcher.DispatchRuntime> 및  <xref:System.ServiceModel.Dispatcher.DispatchOperation> 클래스이며, 클라이언트 형식은 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 및 <xref:System.ServiceModel.Dispatcher.ClientOperation> 클래스입니다. <xref:System.ServiceModel.Dispatcher.ClientRuntime>과 <xref:System.ServiceModel.Dispatcher.DispatchRuntime> 클래스는 클라이언트 전체 및 서비스 전체의 런타임 속성과 확장 컬렉션에 각각 액세스할 수 있는 확장성 진입점입니다. 마찬가지로 <xref:System.ServiceModel.Dispatcher.ClientOperation>과 <xref:System.ServiceModel.Dispatcher.DispatchOperation> 클래스는 클라이언트 작업 및 서비스 작업의 런타임 속성과 확장 컬렉션을 각각 노출합니다. 하지만 작업 런타임 개체에서 더 넓은 범위의 런타임 개체에 액세스하거나 필요에 따라 그 반대로 액세스할 수도 있습니다.  
  
> [!NOTE]
>  런타임 속성 및 클라이언트의 실행 동작을 수정 하는 데 사용할 수 있는 확장 형식, 참조 [확장 클라이언트](../../../../docs/framework/wcf/extending/extending-clients.md)합니다. 런타임 속성 및 서비스 디스패처의 실행 동작을 수정 하는 데 사용할 수 있는 확장 형식, 참조 [디스패처 확장](../../../../docs/framework/wcf/extending/extending-dispatchers.md)합니다.  
  
 대부분의 WCF 사용자 상호 작용 하지 않으며 런타임에 직접; 대신 핵심 프로그래밍 끝점, 계약, 바인딩, 주소 및 구성 파일에 있는 동작이 나 클래스의 동작 특성과 같은 모델 구문을 사용 합니다. 이러한 구문 합니다 *설명 트리*, 서비스를 지 원하는 런타임을 생성 하기 위한 전체 사양인 또는 설명 트리에 설명 된 클라이언트입니다.  
  
 WCF의 동작의 네 가지 종류가 있습니다.  
  
-   서비스 동작(<xref:System.ServiceModel.Description.IServiceBehavior> 형식)을 사용하면 <xref:System.ServiceModel.ServiceHostBase>를 비롯한 전체 서비스 런타임을 사용자 지정할 수 있습니다.  
  
-   엔드포인트 동작(<xref:System.ServiceModel.Description.IEndpointBehavior> 형식)을 사용하면 서비스 엔드포인트와 이에 연결된 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> 개체를 사용자 지정할 수 있습니다.  
  
-   계약 동작(<xref:System.ServiceModel.Description.IContractBehavior> 형식)을 사용하면 각각 클라이언트 및 서비스 응용 프로그램에서 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 및 <xref:System.ServiceModel.Dispatcher.DispatchRuntime> 클래스를 모두 사용자 지정할 수 있습니다.  
  
-   작업 동작(<xref:System.ServiceModel.Description.IOperationBehavior> 형식)을 사용하면 클라이언트 및 서비스에서 <xref:System.ServiceModel.Dispatcher.ClientOperation> 및 <xref:System.ServiceModel.Dispatcher.DispatchOperation> 클래스를 사용자 지정할 수 있습니다.  
  
 이러한 동작은 응용 프로그램 구성 파일을 사용하여 사용자 지정 특성을 구현함으로써 다양한 설명 개체에 추가할 수 있고, 또는 적합한 설명 개체의 동작 컬렉션에 이를 바로 추가할 수 있습니다. 하지만 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.ServiceHost>에서의 <xref:System.ServiceModel.ChannelFactory%601> 호출 이전에 서비스 설명 또는 서비스 엔드포인트 설명 개체에 추가되어야 합니다.  
  
### <a name="behavior-scopes"></a>동작 범위  
 각각 특정 범위의 런타임 액세스에 해당하는 네 가지 동작 형식이 있습니다.  
  
#### <a name="service-behaviors"></a>서비스 동작  
 <xref:System.ServiceModel.Description.IServiceBehavior>를 구현하는 서비스 동작은 전체 서비스 런타임을 수정할 수 있는 기본 메커니즘입니다. 서비스 동작을 서비스에 추가하는 데는 다음과 같은 세 가지 메커니즘이 있습니다.  
  
1.  서비스 클래스의 특성 사용.  <xref:System.ServiceModel.ServiceHost>가 생성되면 <xref:System.ServiceModel.ServiceHost> 구현에서는 리플렉션을 사용하여 서비스 유형에 대한 특성 집합을 검색합니다. <xref:System.ServiceModel.Description.IServiceBehavior>를 구현하는 특성이 있는 경우 <xref:System.ServiceModel.Description.ServiceDescription>의 동작 컬렉션에 해당 특성이 추가됩니다. 이를 통해 이러한 동작이 서비스 런타임 생성에 참여할 수 있습니다.  
  
2.  프로그래밍 방식으로 동작을 <xref:System.ServiceModel.Description.ServiceDescription>의 동작 컬렉션에 추가. 이 작업은 다음 코드를 통해 수행할 수 있습니다.  
  
    ```csharp
    ServiceHost host = new ServiceHost(/* Parameters */);  
    host.Description.Behaviors.Add(/* Service Behavior */);  
    ```  
  
3.  구성을 확장하는 사용자 지정 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 구현. 이를 통해 응용 프로그램 구성 파일에서 서비스 동작을 사용할 수 있습니다.  
  
 WCF의 서비스 동작의 예로 <xref:System.ServiceModel.ServiceBehaviorAttribute> 특성을 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>, 및 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 동작.  
  
#### <a name="contract-behaviors"></a>계약 동작  
 <xref:System.ServiceModel.Description.IContractBehavior> 인터페이스를 구현하는 계약 동작은 계약에서 클라이언트와 서비스 런타임을 모두 확장하는 데 사용됩니다.  
  
 계약 동작을 계약에 추가하는 데는 다음과 같은 두 가지 메커니즘이 있습니다.  첫 번째 메커니즘에서는 계약 인터페이스에 사용될 사용자 지정 특성을 만듭니다. 계약 인터페이스를 전달 된 경우로 <xref:System.ServiceModel.ServiceHost> 또는 <xref:System.ServiceModel.ChannelFactory%601>, WCF 인터페이스의 특성을 검사 합니다. <xref:System.ServiceModel.Description.IContractBehavior>를 구현하는 특성이 있는 경우 해당 인터페이스용으로 만들어진 <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType>의 동작 컬렉션에 해당 특성이 추가됩니다.  
  
 사용자 지정 계약 동작 특성에 대한 <xref:System.ServiceModel.Description.IContractBehaviorAttribute?displayProperty=nameWithType>를 구현할 수도 있습니다. 이 경우 적용되는 동작은 다음과 같습니다.  
  
 • 계약 인터페이스. 이 경우 모든 끝점에서 해당 형식의 모든 계약에 동작이 적용 되 고 WCF의 값을 무시 합니다 <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A?displayProperty=nameWithType> 속성입니다.  
  
 • 서비스 클래스. 이 경우 해당 계약이 <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A> 속성 값인 엔드포인트에만 동작이 적용됩니다.  
  
 • 콜백 클래스. 이 경우 이중 클라이언트의 끝점에 동작이 적용 되 고 WCF의 값을 무시 합니다 <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A> 속성입니다.  
  
 두 번째 메커니즘에서는 <xref:System.ServiceModel.Description.ContractDescription>의 동작 컬렉션에 동작을 추가합니다.  
  
 WCF 계약 동작의 예로 <xref:System.ServiceModel.DeliveryRequirementsAttribute?displayProperty=nameWithType> 특성입니다. 자세한 내용 및 예제는 참조 항목을 참조하십시오.  
  
#### <a name="endpoint-behaviors"></a>엔드포인트 동작  
 <xref:System.ServiceModel.Description.IEndpointBehavior>를 구현하는 엔드포인트 동작은 특정 엔드포인트에 대한 전체 서비스 또는 클라이언트 런타임을 수정할 수 있는 기본 메커니즘입니다.  
  
 엔드포인트 동작을 서비스에 추가하는 데는 다음과 같은 두 가지 메커니즘이 있습니다.  
  
1.  동작을 <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> 속성에 추가합니다.  
  
2.  구성을 확장하는 사용자 지정 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>를 구현합니다.  
  
 자세한 내용 및 예제는 참조 항목을 참조하십시오.  
  
#### <a name="operation-behaviors"></a>작업 동작  
 <xref:System.ServiceModel.Description.IOperationBehavior> 인터페이스를 구현하는 작업 동작은 각 작업에 대해 클라이언트와 서비스 런타임을 모두 확장하는 데 사용됩니다.  
  
 작업 동작을 작업에 추가하는 데는 다음과 같은 두 가지 메커니즘이 있습니다. 첫 번째 메커니즘에서는 작업을 모델링하는 메서드에서 사용될 사용자 지정 특성을 만듭니다. 작업 중 하나에 추가 되는 경우는 <xref:System.ServiceModel.ServiceHost> 또는 <xref:System.ServiceModel.ChannelFactory>, WCF 추가 <xref:System.ServiceModel.Description.IOperationBehavior> 동작 컬렉션에 특성을 <xref:System.ServiceModel.Description.OperationDescription> 해당 작업에 대해 생성 합니다.  
  
 두 번째 메커니즘에서는 생성된 <xref:System.ServiceModel.Description.OperationDescription>의 동작 컬렉션에 동작을 직접 추가합니다.  
  
 WCF의 작업 동작의 예로 <xref:System.ServiceModel.OperationBehaviorAttribute> 하며 <xref:System.ServiceModel.TransactionFlowAttribute>합니다.  
  
 자세한 내용 및 예제는 참조 항목을 참조하십시오.  
  
### <a name="using-configuration-to-create-behaviors"></a>구성을 사용하여 동작 생성  
 서비스와 엔드포인트 및 계약 동작은 코드나 특성을 사용하여 지정하도록 디자인할 수 있지만, 서비스와 엔드포인트 동작은 응용 프로그램이나 웹 구성 파일을 통해서만 구성할 수 있습니다. 개발자는 특성을 사용하여 동작을 노출함으로써, 런타임에는 추가, 제거 또는 수정할 수 없는 동작을 컴파일 시간에 지정할 수 있습니다. 따라서 올바른 서비스 동작을 위해 항상 필요한 동작에 적합합니다(예: <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType> 특성에 대한 트랜잭션 관련 매개 변수). 또한 개발자는 구성을 사용하여 동작을 노출함으로써, 해당 동작의 구성과 사양을 서비스 배포자에게 맡길 수 있습니다. 따라서 서비스에 메타데이터가 노출되는지 또는 특정 권한 부여 구성이 노출되는지 등의 선택적 구성 요소 또는 기타 다른 배포 관련 구성 동작에 적합합니다.  
  
> [!NOTE]
>  또한 회사 응용 프로그램 정책이 적용되도록 구성을 지원하는 동작은 machine.config 구성 파일에 삽입하고 해당 항목을 잠금으로써 사용할 수 있습니다. 설명 및 예제를 참조 하세요 [방법: Lock Down Endpoints in 엔터프라이즈](../../../../docs/framework/wcf/extending/how-to-lock-down-endpoints-in-the-enterprise.md)합니다.  
  
 개발자의 경우 구성을 사용하여 동작을 노출하려면 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>의 파생 클래스를 만든 후 해당 확장을 구성에 등록해야 합니다.  
  
 다음 코드 예제에서는 <xref:System.ServiceModel.Description.IEndpointBehavior>를 통해 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>를 구현하는 방법을 보여 줍니다.  
  
```csharp
// BehaviorExtensionElement members  
public override Type BehaviorType  
{  
  get { return typeof(EndpointBehaviorMessageInspector); }  
}  
  
protected override object CreateBehavior()  
{  
  return new EndpointBehaviorMessageInspector();  
}  
```  
  
 구성 시스템에서 사용자 지정 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>를 로드하려면 이 클래스가 확장으로 등록되어야 합니다. 다음 코드 예제에서는 이전의 엔드포인트 동작에 대한 구성 파일을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
        name="Microsoft.WCF.Documentation.SampleService"  
        behaviorConfiguration="metadataSupport"  
      >  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8080/ServiceMetadata" />  
          </baseAddresses>  
        </host>  
        <endpoint  
          address="/SampleService"  
          binding="wsHttpBinding"  
          behaviorConfiguration="withMessageInspector"   
          contract="Microsoft.WCF.Documentation.ISampleService"  
        />  
        <endpoint  
           address="mex"  
           binding="mexHttpBinding"  
           contract="IMetadataExchange"  
        />  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
      <behavior name="metadataSupport">  
        <serviceMetadata httpGetEnabled="true" httpGetUrl=""/>  
      </behavior>  
      </serviceBehaviors>  
      <endpointBehaviors>  
        <behavior name="withMessageInspector">  
          <endpointMessageInspector />  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <extensions>  
      <behaviorExtensions>  
        <add   
          name="endpointMessageInspector"  
          type="Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector, HostApplication, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"  
        />  
      </behaviorExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
 여기서 `Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector` 동작 확장 유형 및 `HostApplication` 해당 클래스에 컴파일된 어셈블리의 이름입니다.  
  
### <a name="evaluation-order"></a>평가 순서  
 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>와 <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType>는 설명 및 프로그래밍 모델을 통해 런타임을 만듭니다. 앞에서 설명한 대로 동작은 서비스, 엔드포인트, 계약 및 작업에서 빌드 프로세스를 수행합니다.  
  
 <xref:System.ServiceModel.ServiceHost>는 다음 순서로 동작을 적용합니다.  
  
1.  서비스  
  
2.  계약  
  
3.  엔드포인트  
  
4.  작업  
  
 동작 컬렉션 내에서는 정해진 순서가 없습니다.  
  
 <xref:System.ServiceModel.ChannelFactory%601>는 다음 순서로 동작을 적용합니다.  
  
1.  계약  
  
2.  엔드포인트  
  
3.  작업  
  
 앞서 설명한 대로 동작 컬렉션 내에서는 정해진 순서가 없습니다.  
  
### <a name="adding-behaviors-programmatically"></a>프로그래밍 방식으로 동작 추가  
 <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=nameWithType>의 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A?displayProperty=nameWithType> 메서드 다음에 나오는 서비스 응용 프로그램의 <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType> 속성은 수정하면 안 됩니다. 이러한 지점을 지나서 수정될 경우 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A?displayProperty=nameWithType> 및 `AddServiceEndpoint`의 <xref:System.ServiceModel.ServiceHostBase> 메서드와 <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> 속성과 같은 일부 멤버는 예외를 throw합니다. 다른 멤버에서는 이를 수정할 수 있지만 그 결과는 예측할 수 없습니다.  
  
 마찬가지로 클라이언트에서 <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType>의 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A>을 호출한 이후에는 <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> 값을 수정해서는 안 됩니다. 이러한 지점을 지나서 수정될 경우 <xref:System.ServiceModel.ChannelFactory.Credentials%2A?displayProperty=nameWithType> 속성에서 예외를 throw하지만 다른 클라이언트 설명 값은 오류를 발생시키지 않고 수정할 수 있습니다. 하지만 그 결과는 예측할 수 없습니다.  
  
 서비스와 클라이언트 모두에 대해 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=nameWithType>을 호출하기 이전에 설명을 수정하는 것이 좋습니다.  
  
### <a name="inheritance-rules-for-behavior-attributes"></a>동작 특성의 상속 규칙  
 서비스 동작, 계약 동작 등 네 가지 형식의 모든 동작은 특성을 사용하여 채울 수 있습니다. 관리되는 개체 및 멤버에서 특성을 정의하고 관리되는 개체와 멤버에서는 상속을 지원하므로 상속 컨텍스트에서 동작 특성이 작동되는 방법을 정의해야 합니다.  
  
 상위 수준에서는 서비스, 계약 또는 작업 등의 특정 범위의 경우 해당 범위에 대해 상속 계층 구조의 모든 동작 특성이 적용된다는 것이 규칙입니다. 같은 형식의 동작 특성이 두 개 있으면 가장 많이 파생된 형식이 사용됩니다.  
  
#### <a name="service-behaviors"></a>서비스 동작  
 지정된 서비스 클래스의 경우, 해당 클래스 및 그 클래스 부모의 모든 서비스 동작 특성이 적용됩니다. 동일한 특성 형식이 상속 계층 구조의 여러 위치에 적용된 경우에는 가장 많이 파생된 형식이 사용됩니다.  
  
```csharp  
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Multiple)]  
[AspNetCompatibilityRequirementsAttribute(  
    AspNetCompatibilityRequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
public class A { /* … */ }  
  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
public class B : A { /* … */}  
```  
  
 예를 들어 앞의 경우에서 서비스 B는 <xref:System.ServiceModel.InstanceContextMode>가 <xref:System.ServiceModel.InstanceContextMode.Single>, <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> 모드가 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>, <xref:System.ServiceModel.ConcurrencyMode>가 <xref:System.ServiceModel.ConcurrencyMode.Single>인 상태로 끝납니다. 서비스 B의 <xref:System.ServiceModel.ConcurrencyMode> 특성이 서비스 A의 해당 특성보다 "더 많이 파생된" 상태이므로 <xref:System.ServiceModel.ConcurrencyMode.Single>는 <xref:System.ServiceModel.ServiceBehaviorAttribute>입니다.  
  
#### <a name="contract-behaviors"></a>계약 동작  
 지정된 계약의 경우, 해당 인터페이스 및 그 인터페이스 부모의 모든 계약 동작 특성이 적용됩니다. 동일한 특성 형식이 상속 계층 구조의 여러 위치에 적용된 경우에는 가장 많이 파생된 형식이 사용됩니다.  
  
#### <a name="operation-behaviors"></a>작업 동작  
 지정된 작업에서 기존의 추상 또는 가상 작업을 재정의하지 않으면 적용되는 상속 규칙은 없습니다.  
  
 작업이 기존 작업을 재정의하면 그 작업 및 해당 작업 부모의 모든 작업 동작 특성이 적용됩니다.  동일한 특성 형식이 상속 계층 구조의 여러 위치에 적용된 경우에는 가장 많이 파생된 형식이 사용됩니다.
