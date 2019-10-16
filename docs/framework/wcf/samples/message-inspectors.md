---
title: 메시지 검사자
ms.date: 03/30/2017
ms.assetid: 9bd1f305-ad03-4dd7-971f-fa1014b97c9b
ms.openlocfilehash: e7846b8710fa52a5b13de245b8b7147e217533db
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039394"
---
# <a name="message-inspectors"></a>메시지 검사자
이 샘플에서는 클라이언트 및 서비스 메시지 검사자를 구현하고 구성하는 방법을 보여 줍니다.  
  
 메시지 검사자는 서비스 모델의 클라이언트 런타임 및 디스패치 런타임에서 프로그래밍 방식으로나 구성을 통해 사용할 수 있으며, 메시지를 받은 후나 보내기 전에 해당 메시지를 검사하고 변경할 수 있는 확장성 개체입니다.  
  
 이 샘플에서는 구성 가능한 XML 스키마 문서 집합에 대해 들어오는 메시지의 유효성을 검사하는 기본 클라이언트 및 서비스 메시지 유효성 검사 메커니즘을 구현합니다. 이 샘플에서는 각 작업에 대해 메시지의 유효성을 검사하지 않습니다. 이는 의도적으로 작업을 단순화하기 위한 것입니다.  
  
## <a name="message-inspector"></a>메시지 검사자  
 클라이언트 메시지 검사자는 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> 인터페이스를 구현하고 서비스 메시지 검사자는 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector> 인터페이스를 구현합니다. 이러한 구현을 단일 클래스로 결합하여 양쪽에서 작동하는 메시지 검사자를 구성할 수 있습니다. 이 샘플에서는 이렇게 결합된 메시지 검사자를 구현합니다. 검사자는 들어오는 메시지와 나가는 메시지의 유효성을 검사하는 스키마 집합에 전달되어 구성되며, 이 검사자를 통해 개발자는 들어오는 메시지나 나가는 메시지의 유효성을 검사할지 여부와 검사자가 디스패치 모드에 있는지 클라이언트 모드에 있는지를 지정합니다. 이는 이 항목의 뒷부분에서 설명하는 오류 처리에 영향을 줄 수 있습니다.  
  
```  
public class SchemaValidationMessageInspector : IClientMessageInspector, IDispatchMessageInspector  
{  
    XmlSchemaSet schemaSet;  
    bool validateRequest;  
    bool validateReply;  
    bool isClientSide;  
    [ThreadStatic]  
    bool isRequest;  
  
    public SchemaValidationMessageInspector(XmlSchemaSet schemaSet,  
         bool validateRequest, bool validateReply, bool isClientSide)  
    {  
        this.schemaSet = schemaSet;  
        this.validateReply = validateReply;  
        this.validateRequest = validateRequest;  
        this.isClientSide = isClientSide;  
    }  
```  
  
 모든 서비스(디스패처) 메시지 검사자는 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector> 메서드 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>와 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%28System.ServiceModel.Channels.Message%40%2CSystem.Object%29>를 구현해야 합니다.  
  
 메시지를 받아 채널 스택에서 처리한 후 서비스에 할당한 경우 deserialize하여 작업에 디스패치하기 전에 디스패처에서 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>를 호출합니다. 들어오는 메시지가 암호화된 경우 메시지 검사자에 도달하면 해당 메시지는 이미 암호가 해독되어 있습니다. 메서드는 참조 매개 변수로 전달된 `request` 메시지를 가져오며, 이를 통해 필요에 따라 메시지를 검사, 조작 또는 대체할 수 있습니다. 반환 값은 임의의 개체가 될 수 있으며 서비스에서 현재 메시지에 대한 회신을 반환할 때 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%2A>에 전달되는 상관 관계 상태 개체로 사용됩니다. 이 샘플에서 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>는 메시지의 검사(유효성 검사)를 전용 로컬 메서드 `ValidateMessageBody`에 위임하며 상관 관계 상태 개체를 반환하지 않습니다. 이 메서드는 잘못된 메시지가 서비스에 전달되지 않도록 합니다.  
  
```  
object IDispatchMessageInspector.AfterReceiveRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel, System.ServiceModel.InstanceContext instanceContext)  
{  
    if (validateRequest)  
    {  
        // inspect the message. If a validation error occurs,  
        // the thrown fault exception bubbles up.  
        ValidateMessageBody(ref request, true);  
    }  
    return null;  
}  
```  
  
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%28System.ServiceModel.Channels.Message%40%2CSystem.Object%29>는 클라이언트로 회신을 다시 보낼 준비가 될 때마다 호출되며 단방향 메시지인 경우에는 들어오는 메시지가 처리되면 호출됩니다. 따라서 MEP에 관계없이 대칭적으로 확장을 호출할 수 있습니다. <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>와 마찬가지로 메시지는 참조 매개 변수로 전달되며 검사, 수정 또는 대체할 수 있습니다. 이 샘플에서 수행되는 메시지 유효성 검사는 `ValidMessageBody` 메서드에 다시 위임되지만 이 경우 유효성 검사 오류 처리가 약간 다릅니다.  
  
 서비스에서 유효성 검사 오류가 발생하면 `ValidateMessageBody` 메서드에서 <xref:System.ServiceModel.FaultException> 파생 예외를 throw합니다. <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>에서는 SOAP 오류로 자동 변환되어 클라이언트로 전달되는 서비스 모델 인프라에 이러한 예외를 넣을 수 있습니다. <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%2A>에서는 서비스에서 throw된 오류 예외가 메시지 검사자가 호출되기 전에 변환되므로 <xref:System.ServiceModel.FaultException> 예외를 인프라에 넣으면 안 됩니다. 따라서 다음 구현에서는 알려진 `ReplyValidationFault` 예외를 catch하고 회신 메시지를 명시적인 오류 메시지로 바꿉니다. 이 메서드는 서비스 구현에서 잘못된 메시지를 반환하지 않도록 합니다.  
  
```  
void IDispatchMessageInspector.BeforeSendReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
{  
    if (validateReply)  
    {  
        // Inspect the reply, catch a possible validation error   
        try  
        {  
            ValidateMessageBody(ref reply, false);  
        }  
        catch (ReplyValidationFault fault)  
        {  
            // if a validation error occurred, the message is replaced  
            // with the validation fault.  
            reply = Message.CreateMessage(reply.Version,   
                    fault.CreateMessageFault(), reply.Headers.Action);  
        }  
    }  
```  
  
 클라이언트 메시지 검사자는 서비스 메시지 검사자와 매우 유사합니다. <xref:System.ServiceModel.Dispatcher.IClientMessageInspector>에서 구현되어야 하는 두 가지 메서드는 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.AfterReceiveReply%2A>와 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A>입니다.  
  
 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A>는 클라이언트 응용 프로그램이나 작업 포맷터에서 메시지가 작성되면 호출됩니다. 디스패처 메시지 검사자와 마찬가지로 메시지를 검사만 하거나 완전히 바꿀 수 있습니다. 이 샘플에서 검사자는 디스패치 메시지 검사자에도 사용된 동일한 로컬 `ValidateMessageBody` 도우미 메서드에 위임합니다.  
  
 생성자에 지정된 대로 클라이언트 유효성 검사와 서비스 유효성 검사에는 동작 면에서 차이가 있는데, 클라이언트 유효성 검사에서는 서비스 오류 때문이 아니라 로컬에서 이러한 예외가 발생하기 때문에 사용자 코드에 들어가는 로컬 예외가 throw됩니다. 일반적으로 서비스 디스패처 검사자는 오류를 throw하고 클라이언트 검사자는 예외를 throw하는 규칙이 있습니다.  
  
 이 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A> 구현에서는 잘못된 메시지를 서비스로 보내지 않도록 합니다.  
  
```  
object IClientMessageInspector.BeforeSendRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel)  
{  
    if (validateRequest)  
    {  
        ValidateMessageBody(ref request, true);  
    }  
    return null;  
}  
```  
  
 `AfterReceiveReply` 구현에서는 서비스에서 받은 잘못된 메시지가 클라이언트 사용자 코드로 전달되지 않도록 합니다.  
  
```  
void IClientMessageInspector.AfterReceiveReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
{  
    if (validateReply)  
    {  
        ValidateMessageBody(ref reply, false);  
    }  
}  
```  
  
 이러한 특정 메시지 검사자에서는 `ValidateMessageBody` 메서드가 가장 중요합니다. 작업을 수행하기 위해 이 메서드는 전달된 메시지의 본문 내용 하위 트리 주위로 유효성을 검사하는 <xref:System.Xml.XmlReader>를 래핑합니다. 판독기는 메시지 검사자가 보유하는 스키마 집합으로 채워지고 유효성 검사 콜백은 이 메서드와 함께 정의된 `InspectionValidationHandler`를 나타내는 대리자로 설정됩니다. 유효성 검사를 수행하려면 메시지를 읽고 메모리 스트림 지원 <xref:System.Xml.XmlDictionaryWriter>로 스풀링합니다. 프로세스 중에 유효성 검사 오류나 경고가 발생하면 콜백 메서드가 호출됩니다.  
  
 오류가 발생하지 않으면 원본 메시지에서 속성 및 헤더를 복사하고 메모리 스트림에서 현재 유효성이 검사된 infoset을 사용하는 새 메시지가 생성됩니다. 이 메시지는 <xref:System.Xml.XmlDictionaryReader>에 의해 래핑되고 대체 메시지에 추가됩니다.  
  
```  
void ValidateMessageBody(ref System.ServiceModel.Channels.Message message, bool isRequest)  
{  
    if (!message.IsFault)  
    {  
        XmlDictionaryReaderQuotas quotas =   
                new XmlDictionaryReaderQuotas();  
        XmlReader bodyReader =   
            message.GetReaderAtBodyContents().ReadSubtree();  
        XmlReaderSettings wrapperSettings =   
                              new XmlReaderSettings();  
        wrapperSettings.CloseInput = true;  
        wrapperSettings.Schemas = schemaSet;  
        wrapperSettings.ValidationFlags =   
                                XmlSchemaValidationFlags.None;  
        wrapperSettings.ValidationType = ValidationType.Schema;  
        wrapperSettings.ValidationEventHandler += new   
           ValidationEventHandler(InspectionValidationHandler);  
        XmlReader wrappedReader = XmlReader.Create(bodyReader,   
                                            wrapperSettings);  
  
        // pull body into a memory backed writer to validate  
        this.isRequest = isRequest;  
        MemoryStream memStream = new MemoryStream();  
        XmlDictionaryWriter xdw =  
              XmlDictionaryWriter.CreateBinaryWriter(memStream);  
        xdw.WriteNode(wrappedReader, false);  
        xdw.Flush(); memStream.Position = 0;  
        XmlDictionaryReader xdr =   
        XmlDictionaryReader.CreateBinaryReader(memStream, quotas);  
  
        // reconstruct the message with the validated body  
        Message replacedMessage =   
            Message.CreateMessage(message.Version, null, xdr);  
        replacedMessage.Headers.CopyHeadersFrom(message.Headers);  
        replacedMessage.Properties.CopyProperties(message.Properties);  
        message = replacedMessage;  
    }  
}  
```  
  
 `InspectionValidationHandler` 메서드는 스키마 유효성 검사 오류나 경고가 발생할 때마다 유효성을 검사하는 <xref:System.Xml.XmlReader>에 의해 호출됩니다. 다음 구현은 오류가 발생할 때만 작동하며 경고는 모두 무시합니다.  
  
 무엇보다도 유효성을 검사하는 <xref:System.Xml.XmlReader>를 메시지 검사자와 함께 메시지에 삽입하고 메시지가 처리될 때 메시지를 버퍼링하지 않고 유효성 검사가 수행되도록 할 수 있습니다. 그러나 이 콜백에서는 잘못된 XML 노드가 검색되면 서비스 모델 인프라나 사용자 코드의 다른 위치에서 유효성 검사 예외가 throw되어 예기치 않은 동작이 발생할 수 있습니다. 버퍼링 접근 방식을 사용하면 잘못된 메시지로부터 사용자 코드를 완전히 보호할 수 있습니다.  
  
 앞에서 설명한 대로 처리기에 의해 throw된 예외는 클라이언트와 서비스 간에 서로 다릅니다. 서비스에서는 예외가 <xref:System.ServiceModel.FaultException>에서 파생되고, 클라이언트에서는 예외가 일반적인 사용자 지정 예외입니다.  
  
```  
        void InspectionValidationHandler(object sender, ValidationEventArgs e)  
{  
    if (e.Severity == XmlSeverityType.Error)  
    {  
        // We are treating client and service side validation errors  
        // differently here. Client side errors cause exceptions  
        // and are thrown straight up to the user code. Service side  
        // validations cause faults.  
        if (isClientSide)  
        {  
            if (isRequest)  
            {  
                throw new RequestClientValidationException(e.Message);  
            }  
            else  
            {  
                throw new ReplyClientValidationException(e.Message);  
            }  
        }  
        else  
        {  
            if (isRequest)  
            {  
                // this fault is caught by the ServiceModel   
                // infrastructure and turned into a fault reply.  
                throw new RequestValidationFault(e.Message);  
             }  
             else  
             {  
                // this fault is caught and turned into a fault message  
                // in BeforeSendReply in this class  
                throw new ReplyValidationFault(e.Message);  
              }  
          }  
      }  
    }  
```  
  
## <a name="behavior"></a>동작  
 메시지 검사자는 클라이언트 런타임이나 디스패치 런타임의 확장입니다. 이러한 확장은 *동작*을 사용 하 여 구성 됩니다. 동작은 기본 구성을 변경하거나 메시지 검사자와 같은 확장을 기본 구성에 추가하여 서비스 모델 런타임의 동작을 변경하는 클래스입니다.  
  
 다음 `SchemaValidationBehavior` 클래스는 클라이언트 런타임이나 디스패치 런타임에 이 샘플의 메시지 검사자를 추가하는 데 사용된 동작입니다. 두 경우 모두 기본 구현에 해당됩니다. <xref:System.ServiceModel.Description.IEndpointBehavior.ApplyClientBehavior%2A> 및 <xref:System.ServiceModel.Description.IEndpointBehavior.ApplyDispatchBehavior%2A>에서는 메시지 검사자를 만들어 해당 런타임의 <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> 컬렉션에 추가합니다.  
  
```  
public class SchemaValidationBehavior : IEndpointBehavior  
{  
    XmlSchemaSet schemaSet;   
    bool validateRequest;   
    bool validateReply;  
  
    public SchemaValidationBehavior(XmlSchemaSet schemaSet, bool   
                           inspectRequest, bool inspectReply)  
    {  
        this.schemaSet = schemaSet;  
        this.validateReply = inspectReply;  
        this.validateRequest = inspectRequest;  
    }  
    #region IEndpointBehavior Members  
  
    public void AddBindingParameters(ServiceEndpoint endpoint,   
       System.ServiceModel.Channels.BindingParameterCollection   
                                            bindingParameters)  
    {  
    }  
  
    public void ApplyClientBehavior(ServiceEndpoint endpoint,   
            System.ServiceModel.Dispatcher.ClientRuntime clientRuntime)  
    {  
        SchemaValidationMessageInspector inspector =   
           new SchemaValidationMessageInspector(schemaSet,   
                      validateRequest, validateReply, true);  
            clientRuntime.MessageInspectors.Add(inspector);  
    }  
  
    public void ApplyDispatchBehavior(ServiceEndpoint endpoint,   
         System.ServiceModel.Dispatcher.EndpointDispatcher   
                                          endpointDispatcher)  
    {  
        SchemaValidationMessageInspector inspector =   
           new SchemaValidationMessageInspector(schemaSet,   
                        validateRequest, validateReply, false);  
   endpointDispatcher.DispatchRuntime.MessageInspectors.Add(inspector);  
    }  
  
   public void Validate(ServiceEndpoint endpoint)  
   {  
   }  
  
    #endregion  
}  
```  
  
> [!NOTE]
> 이 특정 동작은 특성을 겸용하지 않으므로 서비스 유형의 계약 형식에 선언적으로 추가할 수 없습니다. 이 동작은 특성 선언에서 스키마 컬렉션을 로드할 수 없기 때문에 디자인에 따라 결정되며 이 특성의 추가 구성 위치(예: 응용 프로그램 설정)를 참조하는 것은 나머지 서비스 모델 구성과 일치하지 않는 구성 요소를 만든다는 의미입니다. 따라서 이 동작은 코드와 서비스 모델 구성 확장을 통해 명령적으로만 추가할 수 있습니다.  
  
## <a name="adding-the-message-inspector-through-configuration"></a>구성을 통해 메시지 검사자 추가  
 응용 프로그램 구성 파일에서 끝점에 대 한 사용자 지정 동작을 구성 하려면 서비스 모델에서 구현자를 통해에서 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>파생 된 클래스로 표현 되는 구성 *확장 요소* 를 만들어야 합니다. 그런 다음 이 섹션에 설명된 다음 확장에 대해 표시된 대로 확장에 대한 서비스 모델의 구성 섹션에 이 확장을 추가해야 합니다.  
  
```xml  
<system.serviceModel>  
…  
   <extensions>  
      <behaviorExtensions>  
        <add name="schemaValidator" type="Microsoft.ServiceModel.Samples.SchemaValidationBehaviorExtensionElement, MessageInspectors, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
      </behaviorExtensions>  
    </extensions>  
…  
</system.serviceModel>  
```  
  
 확장은 가장 일반적인 응용 프로그램이나 ASP.NET 구성 파일 또는 컴퓨터 구성 파일에서 추가할 수 있습니다.  
  
 구성 범위에 확장을 추가하면 다음 코드와 같이 동작 구성에 동작을 추가할 수 있습니다. 동작 구성은 필요에 따라 여러 엔드포인트에 적용할 수 있는 재사용 가능한 요소입니다. 여기에서 구성할 특정 동작은 <xref:System.ServiceModel.Description.IEndpointBehavior>를 구현하므로 이 동작은 구성 파일의 해당 구성 섹션에서만 유효합니다.  
  
```xml  
<system.serviceModel>  
   <behaviors>  
      …  
     <endpointBehaviors>  
        <behavior name="HelloServiceEndpointBehavior">  
          <schemaValidator validateRequest="True" validateReply="True">  
            <schemas>  
              <add location="messages.xsd" />    
            </schemas>  
          </schemaValidator>  
        </behavior>  
      </endpointBehaviors>  
      …  
    </behaviors>  
</system.serviceModel>  
```  
  
 메시지 검사자를 구성하는 `<schemaValidator>` 요소는 `SchemaValidationBehaviorExtensionElement` 클래스에서 지원합니다. 이 클래스는 `ValidateRequest`와 `ValidateReply`라는 두 가지 부울 공용 속성을 노출합니다. 이러한 속성은 모두 <xref:System.Configuration.ConfigurationPropertyAttribute>로 표시됩니다. 이 특성은 앞에서 설명한 XML 구성 요소에 표시되는 코드 속성과 XML 특성 간의 링크를 구성합니다. 이 클래스에는 추가로 `Schemas`로 표시되고 <xref:System.Configuration.ConfigurationCollectionAttribute> 형식인 `SchemaCollection` 속성도 있습니다. 이 속성도 이 샘플의 일부이지만 간단한 설명을 위해 이 문서에서 생략되었습니다. 컬렉션 및 컬렉션 요소 클래스 `SchemaConfigElement`와 함께 이 속성은 이전 구성 조각의 `<schemas>` 요소를 지원하며 이 속성을 통해 스키마 컬렉션을 유효성 검사 집합에 추가할 수 있습니다.  
  
 재정의된 `CreateBehavior` 메서드는 런타임에서 클라이언트나 엔드포인트를 빌드할 때 구성 데이터를 확인하여 동작 개체로 바꿉니다.  
  
```  
public class SchemaValidationBehaviorExtensionElement : BehaviorExtensionElement  
{  
    public SchemaValidationBehaviorExtensionElement()  
    {  
    }  
  
    public override Type BehaviorType   
    {   
        get  
        {  
            return typeof(SchemaValidationBehavior);  
        }   
    }  
  
    protected override object CreateBehavior()  
    {  
        XmlSchemaSet schemaSet = new XmlSchemaSet();  
        foreach (SchemaConfigElement schemaCfg in this.Schemas)  
        {  
            Uri baseSchema = new   
                Uri(AppDomain.CurrentDomain.BaseDirectory);  
            string location = new   
                Uri(baseSchema,schemaCfg.Location).ToString();  
            XmlSchema schema =   
                XmlSchema.Read(new XmlTextReader(location), null);  
            schemaSet.Add(schema);  
        }  
     return new   
     SchemaValidationBehavior(schemaSet,ValidateRequest,ValidateReply);  
    }  
  
[ConfigurationProperty("validateRequest",DefaultValue=false,IsRequired=false)]  
public bool ValidateRequest  
{  
    get { return (bool)base["validateRequest"]; }  
    set { base["validateRequest"] = value; }  
}  
  
[ConfigurationProperty("validateReply", DefaultValue = false, IsRequired = false)]  
        public bool ValidateReply  
        {  
            get { return (bool)base["validateReply"]; }  
            set { base["validateReply"] = value; }  
        }  
  
     //Declare the Schema collection property.  
     //Note: the "IsDefaultCollection = false" instructs   
     //.NET Framework to build a nested section of   
     //the kind <Schema> ...</Schema>.  
    [ConfigurationProperty("schemas", IsDefaultCollection = true)]  
    [ConfigurationCollection(typeof(SchemasCollection),  
        AddItemName = "add",  
        ClearItemsName = "clear",  
        RemoveItemName = "remove")]  
    public SchemasCollection Schemas  
    {  
        get  
        {  
            SchemasCollection SchemasCollection =  
            (SchemasCollection)base["schemas"];  
            return SchemasCollection;  
        }  
    }  
}  
```  
  
## <a name="adding-message-inspectors-imperatively"></a>명령으로 메시지 검사자 추가  
 앞에서 설명한 이유로 인해 이 샘플에서 지원되지 않는 특성 및 구성이 아닌 동작은 명령 코드를 사용하여 클라이언트 및 서비스 런타임에 매우 쉽게 추가할 수 있습니다. 이 샘플에서는 클라이언트 응용 프로그램에서 이 작업을 수행하여 클라이언트 메시지 검사자를 테스트합니다. `GenericClient` 클래스는 엔드포인트 구성을 사용자 코드에 노출하는 <xref:System.ServiceModel.ClientBase%601>에서 파생됩니다. 예를 들어, 다음 코드와 같이 동작을 추가하면 클라이언트를 암시적으로 열기 전에 엔드포인트 구성을 변경할 수 있습니다. 서비스에서 동작을 추가하는 작업은 여기에 표시된 클라이언트 기술과 거의 동일하며 서비스 호스트를 열기 전에 수행해야 합니다.  
  
```  
try  
{  
    Console.WriteLine("*** Call 'Hello' with generic client, with client behavior");  
    GenericClient client = new GenericClient();  
  
    // Configure client programmatically, adding behavior  
    XmlSchema schema = XmlSchema.Read(new StreamReader("messages.xsd"),   
                                                          null);  
    XmlSchemaSet schemaSet = new XmlSchemaSet();  
    schemaSet.Add(schema);  
    client.Endpoint.Behaviors.Add(new   
                SchemaValidationBehavior(schemaSet, true, true));  
  
    Console.WriteLine("--- Sending valid client request:");  
    GenericCallValid(client, helloAction);  
    Console.WriteLine("--- Sending invalid client request:");  
    GenericCallInvalid(client, helloAction);  
  
    client.Close();  
}  
catch (Exception e)  
{  
    DumpException(e);  
}  
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageInspectors`  
