---
title: '방법: 클라이언트에서 메시지 검사 또는 수정'
ms.date: 03/30/2017
ms.assetid: b8256335-f1c2-419f-b862-9f220ccad84c
ms.openlocfilehash: 14c24c16a36be600881de402de50086dd18b30b4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796979"
---
# <a name="how-to-inspect-or-modify-messages-on-the-client"></a>방법: 클라이언트에서 메시지 검사 또는 수정
을 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType> 구현 하 고 클라이언트 런타임에 삽입 하 여 WCF 클라이언트에서 들어오거나 나가는 메시지를 검사 하거나 수정할 수 있습니다. 자세한 내용은 [클라이언트 확장](extending-clients.md)을 참조 하세요. 서비스의 해당 기능은 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType>입니다. 전체 코드 예제는 [메시지 검사기](../samples/message-inspectors.md) 샘플을 참조 하세요.  
  
### <a name="to-inspect-or-modify-messages"></a>메시지를 검사하거나 수정하려면  
  
1. <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType> 인터페이스를 구현합니다.  
  
2. 클라이언트 메시지 검사자를 삽입하려는 범위에 따라 <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>를 구현합니다. <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>끝점 수준에서 동작을 변경할 수 있습니다. <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>계약 수준에서 동작을 변경할 수 있습니다.  
  
3. <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType>에서 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> 메서드를 호출하여 동작을 삽입합니다. 자세한 내용은 [동작을 사용 하 여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 아래 순서대로 나열되어 있습니다.  
  
- 클라이언트 검사자 구현.  
  
- 검사자를 삽입하는 엔드포인트 동작.  
  
- 구성 파일에 동작을 추가하는 데 사용할 수 있는 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 파생 클래스.  
  
- 클라이언트 메시지 검사자를 클라이언트 런타임에 삽입하는 엔드포인트 동작을 추가하는 구성 파일.  
  
```csharp  
// Client message inspector  
public class SimpleMessageInspector : IClientMessageInspector  
{  
    public void AfterReceiveReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
    {  
        // Implement this method to inspect/modify messages after a message  
        // is received but prior to passing it back to the client   
        Console.WriteLine("AfterReceiveReply called");  
    }  
  
    public object BeforeSendRequest(ref System.ServiceModel.Channels.Message request, IClientChannel channel)  
    {  
        // Implement this method to inspect/modify messages before they   
        // are sent to the service  
        Console.WriteLine("BeforeSendRequest called");  
        return null;  
    }  
}  
```  
  
```csharp  
// Endpoint behavior  
public class SimpleEndpointBehavior : IEndpointBehavior  
{  
    public void AddBindingParameters(ServiceEndpoint endpoint, System.ServiceModel.Channels.BindingParameterCollection bindingParameters)  
    {  
         // No implementation necessary  
    }  
  
    public void ApplyClientBehavior(ServiceEndpoint endpoint, ClientRuntime clientRuntime)  
    {  
        clientRuntime.MessageInspectors.Add(new SimpleMessageInspector());  
    }  
  
    public void ApplyDispatchBehavior(ServiceEndpoint endpoint, EndpointDispatcher endpointDispatcher)  
    {  
         // No implementation necessary  
    }  
  
    public void Validate(ServiceEndpoint endpoint)  
    {  
         // No implementation necessary  
    }  
}  
```  
  
```csharp  
// Configuration element   
public class SimpleBehaviorExtensionElement : BehaviorExtensionElement  
{  
    public override Type BehaviorType  
    {  
        get { return typeof(SimpleEndpointBehavior); }  
    }  
  
    protected override object CreateBehavior()  
    {  
         // Create the  endpoint behavior that will insert the message  
         // inspector into the client runtime  
        return new SimpleEndpointBehavior();  
    }  
}  
```  
  
```xml
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
    <system.serviceModel>  
        <client>  
            <endpoint address="http://localhost:8080/SimpleService/"   
                      binding="wsHttpBinding"
                      behaviorConfiguration="clientInspectorsAdded"
                      contract="ServiceReference1.IService1"  
                      name="WSHttpBinding_IService1"/>  
        </client>  
  
      <behaviors>  
        <endpointBehaviors>  
          <behavior name="clientInspectorsAdded">  
            <simpleBehaviorExtension />  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>  
      <extensions>  
        <behaviorExtensions>  
          <add  
            name="simpleBehaviorExtension"  
            type="SimpleServiceLib.SimpleBehaviorExtensionElement, Host, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
        </behaviorExtensions>  
      </extensions>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType>
- [동작을 사용하여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)
