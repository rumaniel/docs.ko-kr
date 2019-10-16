---
title: 본문 요소에 의한 디스패치
ms.date: 03/30/2017
ms.assetid: f64a3c04-62b4-47b2-91d9-747a3af1659f
ms.openlocfilehash: f1ff6d099ad0aee0c17b011000fe78f961293a82
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039768"
---
# <a name="dispatch-by-body-element"></a>본문 요소에 의한 디스패치
이 샘플에서는 들어오는 메시지를 작업에 할당하는 대체 알고리즘을 구현하는 방법을 보여 줍니다.  
  
 기본적으로 서비스 모델 디스패처는 메시지의 WS-Addressing "Action" 헤더나 HTTP SOAP 요청의 동일한 정보에 따라 들어오는 메시지에 적합한 처리 방법을 선택합니다.  
  
 WS-I Basic Profile 1.1 지침을 따르지 않는 일부 SOAP 1.1 웹 서비스 스택은 동작 URI 대신 SOAP 본문 내 첫 번째 요소의 정규화된 XML 이름에 따라 메시지를 디스패치합니다. 마찬가지로 이러한 스택의 클라이언트측은 SOAP 1.1 사양에 허용된 빈 HTTP SoapAction 헤더나 임의의 HTTP SoapAction 헤더를 사용하여 메시지를 보낼 수 있습니다.  
  
 메시지가 메서드로 디스패치되는 방법을 변경하기 위해 이 샘플에서는 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector>에서 `DispatchByBodyElementOperationSelector` 확장성 인터페이스를 구현합니다. 이 클래스는 메시지 본문의 첫 번째 요소에 따라 작업을 선택합니다.  
  
 클래스 생성자에는 `XmlQualifiedName`과 문자열 쌍으로 채워진 사전이 필요합니다. 여기에서 정규화된 이름은 SOAP 본문에서 첫 번째 자식의 이름을 나타내고 문자열은 일치하는 작업 이름을 나타냅니다. `defaultOperationName`은 이 사전과 일치하지 않는 모든 메시지를 받는 작업의 이름입니다.  
  
```csharp
class DispatchByBodyElementOperationSelector : IDispatchOperationSelector  
{  
    Dictionary<XmlQualifiedName, string> dispatchDictionary;  
    string defaultOperationName;  
  
    public DispatchByBodyElementOperationSelector(Dictionary<XmlQualifiedName,string> dispatchDictionary, string defaultOperationName)  
    {  
        this.dispatchDictionary = dispatchDictionary;  
        this.defaultOperationName = defaultOperationName;  
    }  
}
```  
  
 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> 구현은 인터페이스 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector.SelectOperation%2A>에 메서드가 하나만 있으므로 매우 간단하게 빌드할 수 있습니다. 이 메서드의 작업은 들어오는 메시지를 검사하고 현재 엔드포인트에 대한 서비스 계약의 메서드 이름과 동일한 문자열을 반환하는 것입니다.  
  
 이 샘플에서 작업 선택기는 <xref:System.Xml.XmlDictionaryReader>를 사용하여 들어오는 메시지의 본문에 대한 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A>를 가져옵니다. 이 메서드는 메시지 본문의 첫 번째 자식에 판독기를 미리 배치하여 현재 요소의 이름과 네임스페이스 URI를 가져와서 `XmlQualifiedName`에 결합한 다음 작업 선택기에서 보유하고 있는 사전에서 해당 작업을 조회하는 데 사용할 수 있도록 합니다.  
  
```csharp
public string SelectOperation(ref System.ServiceModel.Channels.Message message)  
{  
    XmlDictionaryReader bodyReader = message.GetReaderAtBodyContents();  
    XmlQualifiedName lookupQName = new  
       XmlQualifiedName(bodyReader.LocalName, bodyReader.NamespaceURI);  
    message = CreateMessageCopy(message,bodyReader);  
    if (dispatchDictionary.ContainsKey(lookupQName))  
    {  
         return dispatchDictionary[lookupQName];  
    }  
    else  
    {  
        return defaultOperationName;  
    }  
}  
```  
  
 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> 또는 메시지 본문 내용에 액세스할 수 있는 권한을 제공하는 다른 메서드를 사용하여 메시지 본문에 액세스하면 메시지가 "읽음"으로 표시됩니다. 즉, 메시지를 추가로 처리할 수 없습니다. 따라서 작업 선택기는 다음 코드에 표시된 메서드를 사용하여 들어오는 메시지의 복사본을 만듭니다. 판독기의 위치는 검사 중에 변경되지 않기 때문에 새로 만든 메시지에서 이를 참조할 수 있습니다. 입력 메시지의 메시지 속성 및 메시지 헤더도 이 새 메시지에 복사되므로 원본 메시지가 정확하게 복제됩니다.  
  
```csharp
private Message CreateMessageCopy(Message message,   
                                     XmlDictionaryReader body)  
{  
    Message copy = Message.CreateMessage(message.Version,message.Headers.Action,body);  
    copy.Headers.CopyHeaderFrom(message,0);  
    copy.Properties.CopyProperties(message.Properties);  
    return copy;  
}  
```  
  
## <a name="adding-an-operation-selector-to-a-service"></a>서비스에 작업 선택기 추가  
 서비스 디스패치 작업 선택기는 WCF (Windows Communication Foundation) 디스패처에 대 한 확장입니다. 이중 계약의 콜백 채널에서 메서드를 선택하기 위한 클라이언트 작업 선택기도 있습니다. 이 작업 선택기는 여기에서 설명하는 디스패치 작업 선택기와 매우 유사하게 작동하지만 이 샘플에서 명시적으로 설명하지는 않습니다.  
  
 대부분의 서비스 모델 확장처럼 디스패치 작업 선택기도 동작을 사용하여 디스패처에 추가됩니다. *동작은* 디스패치 런타임이나 클라이언트 런타임에 하나 이상의 확장을 추가 하거나 다른 방식으로 설정을 변경 하는 구성 개체입니다.  
  
 작업 선택기에는 계약 범위가 있으므로 여기서 구현하기에 적합한 동작은 <xref:System.ServiceModel.Description.IContractBehavior>입니다. 다음 코드와 같이 인터페이스는 <xref:System.Attribute> 파생 클래스에 구현되므로 이 동작을 서비스 계약에 선언적으로 추가할 수 있습니다. <xref:System.ServiceModel.ServiceHost>를 열고 디스패치 런타임을 빌드할 때마다 계약, 작업 및 서비스 구현의 특성이나 서비스 구성의 요소로 검색되는 모든 동작은 자동으로 추가된 후 확장을 적용하거나 기본 구성을 수정하라는 요청을 받습니다.  
  
 간단한 설명을 위해 다음에 인용된 코드에서는 이 샘플에 사용된 디스패처의 구성 변경에 영향을 주는 <xref:System.ServiceModel.Description.IContractBehavior.ApplyDispatchBehavior%2A> 메서드의 구현만 보여 줍니다. 다른 메서드는 작업을 수행하지 않고 호출자에게 반환되기 때문에 표시되지 않습니다.  
  
```csharp
[AttributeUsage(AttributeTargets.Class|AttributeTargets.Interface)]  
class DispatchByBodyElementBehaviorAttribute : Attribute, IContractBehavior  
{  
    // public void AddBindingParameters(...)   
    // public void ApplyClientBehavior(...)  
    // public void Validate(...)  
```  
  
 먼저 <xref:System.ServiceModel.Description.IContractBehavior.ApplyDispatchBehavior%2A> 구현에서는 서비스 엔드포인트의 <xref:System.ServiceModel.Description.OperationDescription>에서 <xref:System.ServiceModel.Description.ContractDescription> 요소를 반복하여 작업 선택기에 대한 조회 사전을 설정합니다. 그런 다음 각 작업 설명을 검사하여 이 샘플에도 정의되어 있는 `DispatchBodyElementAttribute`의 구현인 <xref:System.ServiceModel.Description.IOperationBehavior> 동작이 있는지 확인합니다. 이 클래스도 동작이지만 수동적이며 디스패치 런타임에 구성 변경 내용을 능동적으로 적용하지 않습니다. 클래스의 모든 메서드가 작업을 수행하지 않고 호출자에게 반환됩니다. 작업 동작만 존재하므로 새 디스패치 메커니즘에 필요한 메타데이터 즉, 작업이 선택되는 본문 요소의 정규화된 이름을 해당 작업에 연결할 수 있습니다.  
  
 이러한 동작이 있으면 정규화된 XML 이름(`QName` 속성)과 작업 이름(`Name` 속성)으로 만들어진 값 쌍이 사전에 추가됩니다.  
  
 사전이 채워지면 이 정보로 새 `DispatchByBodyElementOperationSelector`가 생성되고 디스패치 런타임의 작업 선택기로 설정됩니다.  
  
```csharp
public void ApplyDispatchBehavior(ContractDescription contractDescription, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.DispatchRuntime dispatchRuntime)  
{  
    Dictionary<XmlQualifiedName,string> dispatchDictionary =   
                     new Dictionary<XmlQualifiedName,string>();  
    foreach( OperationDescription operationDescription in   
                              contractDescription.Operations )  
    {  
        DispatchBodyElementAttribute dispatchBodyElement =   
   operationDescription.Behaviors.Find<DispatchBodyElementAttribute>();  
        if ( dispatchBodyElement != null )  
        {  
             dispatchDictionary.Add(dispatchBodyElement.QName,   
                              operationDescription.Name);  
        }  
    }  
    dispatchRuntime.OperationSelector =   
            new DispatchByBodyElementOperationSelector(  
               dispatchDictionary,   
               dispatchRuntime.UnhandledDispatchOperation.Name);  
    }  
}  
```  
  
## <a name="implementing-the-service"></a>서비스 구현  
 이 샘플에 구현된 동작은 네트워크의 메시지가 해석되고 디스패치되는 방식에 직접적인 영향을 주며, 이는 서비스 계약의 기능입니다. 따라서 이 동작을 사용하도록 선택하는 서비스 구현에서는 서비스 계약 수준으로 동작을 선언해야 합니다.  
  
 `DispatchByBodyElementBehaviorAttribute` 샘플 프로젝트 서비스는 계약 동작 `IDispatchedByBody` 을 서비스 계약에 적용 하 고 각 `DispatchBodyElementAttribute` 두 작업 `OperationForBodyA()` 및 `OperationForBodyB()` 작업 동작에 레이블을 적용 합니다. 이 계약을 구현하는 서비스에 대한 서비스 호스트를 열면 앞에서 설명한 대로 디스패처 작성기에서 이 메타데이터를 선택합니다.  
  
 작업 선택기는 메시지 본문 요소만을 기준으로 디스패치하고 "Action"을 무시하므로 `ReplyAction`의 <xref:System.ServiceModel.OperationContractAttribute> 속성에 와일드카드 "*"를 할당하여 반환된 회신에서 "Action" 헤더를 검사하지 않도록 런타임에 알려야 합니다. 또한 "Action" 속성이 와일드 카드 "\*"로 설정 된 기본 작업이 필요 합니다. 기본 작업은 디스패치할 수 없는 모든 메시지를 받으므로 `DispatchBodyElementAttribute`이 없습니다.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"),  
                            DispatchByBodyElementBehavior]  
public interface IDispatchedByBody  
{  
    [OperationContract(ReplyAction="*"),   
     DispatchBodyElement("bodyA","http://tempuri.org")]  
    Message OperationForBodyA(Message msg);  
    [OperationContract(ReplyAction = "*"),   
     DispatchBodyElement("bodyB", "http://tempuri.org")]  
    Message OperationForBodyB(Message msg);  
    [OperationContract(Action="*", ReplyAction="*")]  
    Message DefaultOperation(Message msg);  
}  
```  
  
 샘플 서비스 구현은 간단합니다. 모든 메서드는 수신된 메시지를 회신 메시지로 래핑하고 클라이언트에 다시 표시합니다.  
  
## <a name="running-and-building-the-sample"></a>샘플 실행 및 빌드  
 샘플을 실행하면 작업 응답의 본문 내용이 형식이 지정된 다음 출력과 유사하게 클라이언트 콘솔 창에 표시됩니다.  
  
 클라이언트는 본문 내용 요소의 이름이 각각 `bodyA`, `bodyB` 및 `bodyX`인 세 개의 메시지를 서비스로 보냅니다. 이전 설명과 표시된 서비스 계약에서 알 수 있듯이, `bodyA` 요소가 있는 들어오는 메시지는 `OperationForBodyA()` 메서드로 디스패치됩니다. `bodyX` 본문 요소가 있는 메시지의 경우에는 명시적인 디스패치 대상이 없으므로 메시지가 `DefaultOperation()`으로 디스패치됩니다. 각 서비스 작업은 수신된 메시지 본문을 메서드 관련 요소로 래핑하여 반환하며, 이 작업은 이 샘플의 입력 및 출력 메시지를 명확하게 상호 연결하기 위해 수행됩니다.  
  
```xml  
<?xml version="1.0" encoding="IBM437"?>  
<replyBodyA xmlns="http://tempuri.org">  
   <q:bodyA xmlns:q="http://tempuri.org">test</q:bodyA>  
</replyBodyA>  
<?xml version="1.0" encoding="IBM437"?>  
<replyBodyB xmlns="http://tempuri.org">  
  <q:bodyB xmlns:q="http://tempuri.org">test</q:bodyB>  
</replyBodyB>  
<?xml version="1.0" encoding="IBM437"?>  
<replyDefault xmlns="http://tempuri.org">  
   <q:bodyX xmlns:q="http://tempuri.org">test</q:bodyX>  
</replyDefault>  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Interop\AdvancedDispatchByBody`  
