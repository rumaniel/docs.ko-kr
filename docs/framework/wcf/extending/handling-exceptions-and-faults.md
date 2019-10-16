---
title: 예외 및 오류 처리
ms.date: 03/30/2017
ms.assetid: a64d01c6-f221-4f58-93e5-da4e87a5682e
ms.openlocfilehash: 4f95907d4f88315f2815b84e2ceb4e069783438d
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851272"
---
# <a name="handling-exceptions-and-faults"></a>예외 및 오류 처리
예외는 서비스 또는 클라이언트 구현 내에서 로컬 오류 통신에 사용됩니다. 이와 반대로 오류는 서버에서 클라이언트로 또는 그 반대로 가는 경우와 같이 서비스 경계 너머로 이루어지는 오류 통신에도 사용되는 말입니다. 오류 외에, 전송 채널에서 전송별 메커니즘을 사용하여 전송 수준의 오류 통신을 수행하는 경우도 많습니다. 예를 들어 HTTP 전송에서는 404 등의 상태 코드를 사용하여 엔드포인트 URL이 없는 경우(오류를 다시 보낼 엔드포인트가 없음)를 나타냅니다. 이 문서는 사용자 지정 채널 작성자를 위한 안내 자료를 제공하는 세 개의 단원으로 구성되어 있습니다. 첫 단원에서는 예외를 정의하고 throw하는 방법에 대한 안내 자료를 제공합니다. 둘째 단원에서는 오류 생성 및 소비에 대한 안내 자료를 제공합니다. 셋째 단원에서는 추적 정보를 제공하여 사용자 지정 채널 사용자의 애플리케이션 실행 문제 해결을 돕는 방법에 대해 설명합니다.  
  
## <a name="exceptions"></a>예외  
 예외를 throw 할 때는 다음 두 가지 사항을 염두에 두어야 합니다. 먼저 사용자가 예외에 적절 하 게 대응할 수 있는 올바른 코드를 작성할 수 있는 형식 이어야 합니다. 둘째, 잘못된 것이 무엇이고, 실패의 영향은 무엇이며, 문제를 해결하는 방법이 무엇인지 사용자가 이해하기에 충분한 정보를 제공해야 합니다. 다음 섹션에서는 WCF (Windows Communication Foundation) 채널에 대 한 예외 형식 및 메시지에 대 한 지침을 제공 합니다. .NET의 예외 디자인 지침 문서에도 예외에 대한 일반적인 안내 자료가 있습니다.  
  
### <a name="exception-types"></a>예외 형식  
 채널에서 throw되는 모든 예외는 <xref:System.TimeoutException?displayProperty=nameWithType>, <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType>이거나 <xref:System.ServiceModel.CommunicationException>에서 파생된 형식이어야 합니다. <xref:System.ObjectDisposedException> 등의 예외도 throw될 수 있지만 이는 오직 호출 코드에서 채널을 잘못 사용한 것을 나타내기 위한 것입니다. 채널을 올바르게 사용한 경우에는 지정된 예외만 throw해야 합니다. WCF는에서 <xref:System.ServiceModel.CommunicationException> 파생 되 고 채널에서 사용 하도록 디자인 된 7 가지 예외 형식을 제공 합니다. <xref:System.ServiceModel.CommunicationException>에서 파생되며 시스템의 다른 부분에서 사용하도록 디자인된 다른 예외도 있습니다. 예외 형식은 다음과 같습니다.  
  
|예외 형식|의미|내부 예외 콘텐츠|복구 전략|  
|--------------------|-------------|-----------------------------|-----------------------|  
|<xref:System.ServiceModel.AddressAlreadyInUseException>|수신용으로 지정된 엔드포인트 주소가 이미 사용 중입니다.|있는 경우 이 예외를 일으킨 전송 오류에 대한 세부 정보를 더 제공합니다. 예를 들어 <xref:System.IO.PipeException>, <xref:System.Net.HttpListenerException> 또는 <xref:System.Net.Sockets.SocketException>.|다른 주소를 지정하십시오.|  
|<xref:System.ServiceModel.AddressAccessDeniedException>|프로세스에 수신용으로 지정된 엔드포인트 주소에 대한 액세스가 허용되지 않습니다.|있는 경우 이 예외를 일으킨 전송 오류에 대한 세부 정보를 더 제공합니다. 예를 들면 <xref:System.IO.PipeException> 또는 <xref:System.Net.HttpListenerException>과 같습니다.|다른 자격 증명으로 시도해 보십시오.|  
|<xref:System.ServiceModel.CommunicationObjectFaultedException>|사용 중인이 (가) 오류 상태에 있습니다. 자세한 내용은 [상태 변경 내용 이해](understanding-state-changes.md)를 참조 하세요. <xref:System.ServiceModel.ICommunicationObject> 개체에서 보류 중인 호출이 여러 개인 경우에는 한 호출에서만 실패와 관련된 예외가 throw되며, 나머지 호출에서는 <xref:System.ServiceModel.CommunicationObjectFaultedException>이 throw됩니다. 이 예외는 보통 애플리케이션에서 예외를 간과하고 이미 실패한 개체를 사용하려는 경우에 throw되며, 원래 예외를 catch한 것과 다른 스레드에서 일어나는 경우가 많습니다.|있는 경우 내부 예외에 대한 세부 정보를 제공합니다.|새 개체를 만듭니다. 처음에 <xref:System.ServiceModel.ICommunicationObject>의 오류를 일으킨 것이 무엇인지에 따라 다른 복구 작업이 필요할 수도 있습니다.|  
|<xref:System.ServiceModel.CommunicationObjectAbortedException>|사용 중인이 (가) 중단 되었습니다. 자세한 내용은 [상태 변경 내용 이해](understanding-state-changes.md)를 참조 하세요. <xref:System.ServiceModel.ICommunicationObject> <xref:System.ServiceModel.CommunicationObjectFaultedException>과 마찬가지로, 이 예외는 애플리케이션에서 개체에 대해 <xref:System.ServiceModel.ICommunicationObject.Abort%2A>를 호출했으며 따라서 개체를 더 이상 사용할 수 없는 경우를 나타냅니다. 이러한 호출은 다른 스레드에서 이루어지는 경우도 많습니다.|있는 경우 내부 예외에 대한 세부 정보를 제공합니다.|새 개체를 만듭니다. 처음에 <xref:System.ServiceModel.ICommunicationObject>의 중단을 일으킨 것이 무엇인지에 따라 다른 복구 작업이 필요할 수도 있습니다.|  
|<xref:System.ServiceModel.EndpointNotFoundException>|대상 원격 엔드포인트가 수신 대기 상태가 아닙니다. 이는 엔드포인트 주소에 잘못된 부분이 있거나, 주소를 확인할 수 없거나, 엔드포인트가 다운된 경우에 발생할 수 있습니다. 예로는 DNS 오류, 큐 관리자를 사용할 수 없는 경우, 그리고 서비스가 실행되지 않는 경우가 포함됩니다.|내부 예외는 세부 정보(일반적으로 기본 전송에 대한 정보)를 제공합니다.|다른 주소를 지정하십시오. 또는 서비스가 다운된 경우 발신자가 잠시 기다렸다가 다시 시도할 수도 있습니다.|  
|<xref:System.ServiceModel.ProtocolException>|엔드포인트의 정책에 설명된 통신 프로토콜이 엔드포인트 사이에서 일치하지 않습니다. 예를 들어, 프레이밍 콘텐츠 형식이 일치하지 않거나 최대 메시지 크기가 초과된 경우일 수 있습니다.|있는 경우 특정 프로토콜 오류에 대한 세부 정보를 더 제공합니다. 예를 들어 <xref:System.ServiceModel.QuotaExceededException>은 오류의 원인이 MaxReceivedMessageSize 초과인 경우의 내부 예외입니다.|회복 보낸 사람 및 수신 프로토콜 설정이 일치 하는지 확인 합니다. 여기 사용되는 방법 중 하나는 서비스 엔드포인트의 메타데이터(정책)를 다시 가져온 다음 생성된 바인딩을 사용하여 채널을 다시 만드는 것입니다.|  
|<xref:System.ServiceModel.ServerTooBusyException>|원격 엔드포인트가 수신 대기 상태이지만 메시지를 처리할 준비가 되지 않았습니다.|있는 경우 내부 예외는 SOAP 오류 또는 전송 수준 오류의 세부 정보를 제공합니다.|회복 기다렸다가 나중에 작업을 다시 시도하십시오.|  
|<xref:System.TimeoutException>|제한 시간을 초과하기 전에 작업을 완료하지 못했습니다.|제한 시간에 대한 세부 정보를 제공할 수 있습니다.|기다렸다가 나중에 작업을 다시 시도하십시오.|  
  
 지정된 유형이 기존 예외 형식 모두와 다른 특정 복구 전략에 해당되는 경우에만 새 예외 형식을 정의합니다. 새 예외 형식을 정의하는 경우, 새 형식은 <xref:System.ServiceModel.CommunicationException> 또는 파생된 클래스 중 하나에서 파생된 것이어야 합니다.  
  
### <a name="exception-messages"></a>예외 메시지  
 예외 메시지는 프로그램이 아닌 사용자를 대상으로 하기 때문에 사용자가 문제를 이해하고 해결하는 데 충분히 도움이 될 만한 정보를 제공해야 합니다. 좋은 예외 메시지의 3가지 주요 부분은 다음과 같습니다.  
  
 발생 상황. 사용자의 경험과 밀접한 용어를 사용하여 문제를 명확하게 설명합니다. 예를 들어, 잘못된 예외 메시지의 예로는 "잘못된 구성 섹션"이 있습니다. 그러면 사용자는 구성 섹션에서 잘못된 부분이 어느 곳이며 잘못된 이유가 무엇인지 알 수 없습니다. 향상 된 메시지는 "잘못 된 구성 섹션 \<customBinding >"입니다. "바인딩에 이미 myTransport라는 전송이 있기 때문에 myBinding이라는 바인딩에 myTransport라는 전송을 추가할 수 없습니다"로 만들면 메시지가 한결 더 나아집니다. 이 메시지는 사용자가 애플리케이션의 구성 파일에서 쉽게 식별할 수 있는 용어와 이름을 사용한 매우 구체적인 메시지입니다. 하지만 여전히 몇 가지 주요 구성 요소가 빠져 있습니다.  
  
 오류의 중대성. 메시지에 오류의 의미가 명확하게 표시되어 있지 않으면 사용자는 치명적인 오류인지 무시해도 되는 오류인지 알 방법이 없습니다. 일반적으로 메시지를 통해 오류의 의미나 중대성을 알 수 있어야 합니다. 이전 예제를 개선 하기 위해 "구성 오류 때문에 ServiceHost를 열지 못했습니다. 바인딩에 이미 myTransport 라는 전송이 있기 때문에 Mytransport 이라는 바인딩에 myTransport 라는 전송을 추가할 수 없습니다.  
  
 사용자가 문제를 해결하는 방법. 메시지에서 가장 중요한 부분은 사용자가 문제를 해결할 수 있게 돕는 것입니다. 메시지에는 문제를 해결하기 위해 확인하거나 수정해야 할 사항에 대한 안내 자료 또는 힌트가 포함되어 있어야 합니다. 예를 들어 구성 오류로 인해 ServiceHost를 열지 못했습니다. 바인딩에 이미 myTransport 라는 전송이 있기 때문에 Mytransport 이라는 바인딩에 myTransport 라는 전송을 추가할 수 없습니다. 바인딩에 전송이 하나 뿐인지 확인하십시오"가 될 수 있습니다.  
  
## <a name="communicating-faults"></a>오류 통신  
 SOAP 1.1과 SOAP 1.2는 모두 오류의 특정 구조를 정의합니다. 두 사양 사이에 약간의 차이는 있지만 일반적으로 Message 및 MessageFault 형식을 사용하여 오류를 만들고 소비합니다.  
  
 ![예외 및 오류 처리](./media/wcfc-soap1-1andsoap1-2faultcomparisonc.gif "wcfc_SOAP1-1AndSOAP1-2FaultComparisonc")  
SOAP 1.2 오류(왼쪽)와 SOAP 1.1 오류(오른쪽). SOAP 1.1에서는 오류 요소의 네임스페이스만 정규화됩니다.  
  
 SOAP에서는 오류 메시지를 오류 요소(이름이 `<env:Fault>`인 요소)를 `<env:Body>`의 자식으로 포함하는 메시지로만 정의합니다. 그림 1에 표시된 것과 같이 오류 요소의 콘텐츠는 SOAP 1.1과 SOAP 1.2 사이에서 약간 다릅니다. 하지만 <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType> 클래스에서는 이런 차이를 한 개체 모델로 정규화합니다.  
  
```csharp
public abstract class MessageFault  
{  
    protected MessageFault();  
  
    public virtual string Actor { get; }  
    public virtual string Node { get; }  
    public static string DefaultAction { get; }  
    public abstract FaultCode Code { get; }  
    public abstract bool HasDetail { get; }  
    public abstract FaultReason Reason { get; }  
  
    public T GetDetail<T>();  
    public T GetDetail<T>( XmlObjectSerializer serializer);  
    public System.Xml.XmlDictionaryReader GetReaderAtDetailContents();  
  
    // other methods omitted  
}  
```  
  
 `Code` 속성은 `env:Code`(또는 SOAP 1.1의 경우 `faultCode`)이며 오류의 유형을 식별합니다. SOAP 1.2에서는 Sender 또는 Receiver 등의 5가지 허용되는 값을 `faultCode`에 정의하고 하위 코드 값을 포함할 수 있는 `Subcode` 요소를 정의합니다. 허용 되는 오류 코드 목록 및 해당 의미에 대해서는 [SOAP 1.2 사양을](https://go.microsoft.com/fwlink/?LinkId=95176) 참조 하십시오. SOAP 1.1에는 약간 다른 메커니즘이 있습니다. 완전히 새로운 값 `faultCode` 을 정의 하거나 점 표기법을 사용 하 여 더 구체적인 `faultCodes`(예: client.msi)를 만들어 확장할 수 있는 네 가지 값 (예: 클라이언트 및 서버)을 정의 합니다.  
  
 MessageFault를 사용하여 오류를 프로그래밍하면 FaultCode.Name 및 FaultCode.Namespace는 SOAP 1.2 `env:Code` 또는 SOAP 1.1 `faultCode`의 이름 및 네임스페이스에 매핑됩니다. FaultCode.SubCode는 SOAP 1.2의 경우 `env:Subcode`에 매핑되며 SOAP 1.1의 경우 null입니다.  
  
 프로그래밍 방식으로 오류를 구분하는 것이 좋은 경우에는 새 오류 하위 코드(또는 SOAP 1.1을 사용하는 경우 새 오류 코드)를 만들어야 합니다. 이는 새 예외 형식을 만드는 것과 유사합니다. SOAP 1.1 오류 코드에서는 점 표기법 사용을 피해야 합니다. 또한 [Ws-i Basic 프로필](https://go.microsoft.com/fwlink/?LinkId=95177) 은 오류 코드 점 표기법을 사용 하지 않습니다.  
  
```csharp  
public class FaultCode  
{  
    public FaultCode(string name);  
    public FaultCode(string name, FaultCode subCode);  
    public FaultCode(string name, string ns);  
    public FaultCode(string name, string ns, FaultCode subCode);  
  
    public bool IsPredefinedFault { get; }  
    public bool IsReceiverFault { get; }  
    public bool IsSenderFault { get; }  
    public string Name { get; }  
    public string Namespace { get; }  
    public FaultCode SubCode { get; }  
  
//  methods omitted  
  
}  
```  
  
 `Reason` 속성은 오류 조건을 사람이 읽을 수 있게 설명한 `env:Reason`(또는 SOAP 1.1의 경우 `faultString`)에 해당되며 예외 메시지와 비슷합니다. `FaultReason` 클래스(및 SOAP `env:Reason/faultString`)에는 세계화를 위해 여러 번역을 지원하는 기능이 기본 제공됩니다.  
  
```csharp  
public class FaultReason  
{  
    public FaultReason(FaultReasonText translation);  
    public FaultReason(IEnumerable<FaultReasonText> translations);  
    public FaultReason(string text);  
  
    public SynchronizedReadOnlyCollection<FaultReasonText> Translations   
    {   
       get;   
    }  
  
 }  
```  
  
 MessageFault에서는 T > 및 `GetDetail` `GetReaderAtDetailContents`()를 \<비롯 한 다양 한 방법을 사용 하 여 오류 정보 내용이 노출 됩니다. 오류 세부 정보는 오류에 대한 추가 정보를 전달하는 데 사용되는 불투명 요소입니다. 오류와 함께 전달할 임의 구조의 세무 정보가 있는 경우에 유용합니다.  
  
### <a name="generating-faults"></a>오류 생성  
 이 단원에서는 채널에서 검색된 오류나 채널에서 만든 메시지 속성에 대한 반응으로 오류를 생성하는 과정을 설명합니다. 일반적인 예로는 잘못된 데이터가 포함된 요청 메시지에 대한 반응으로 오류를 다시 보내는 경우가 있습니다.  
  
 오류를 생성할 때에는 사용자 지정 채널에서 오류를 직접 보내지 않고 예외를 throw한 다음 위의 계층에서 예외를 오류로 변환할 것인지 여부와 전송 방법을 결정하게 해야 합니다. 이 변환을 돕기 위해, 채널에서는 사용자 지정 채널에서 throw된 예외를 적절한 오류로 변환할 수 있는 `FaultConverter` 구현을 제공해야 합니다. `FaultConverter`는 다음과 같이 정의됩니다.  
  
```csharp  
public class FaultConverter  
{  
    public static FaultConverter GetDefaultFaultConverter(  
                                   MessageVersion version);  
    protected abstract bool OnTryCreateFaultMessage(  
                                   Exception exception,   
                                   out Message message);  
    public bool TryCreateFaultMessage(  
                                   Exception exception,   
                                   out Message message);  
}  
```  
  
 사용자 지정 오류를 생성하는 각 채널에서는 `FaultConverter`를 구현하여 호출에서 `GetProperty<FaultConverter>`로 반환해야 합니다. 사용자 지정 `OnTryCreateFaultMessage` 구현에서는 예외를 오류로 변환하거나 내부 채널의 `FaultConverter`에 위임해야 합니다. 채널이 전송 인 경우 예외 또는 대리자를 인코더 `FaultConverter` 의 또는 WCF에서 제공 된 기본값으로 `FaultConverter` 변환 해야 합니다. 기본 `FaultConverter`는 WS-Addressing 및 SOAP에서 지정한 오류 메시지에 해당되는 오류를 변환합니다. 다음은 `OnTryCreateFaultMessage` 구현 예입니다.  
  
```csharp  
public override bool OnTryCreateFaultMessage(Exception exception,   
                                             out Message message)  
{  
    if (exception is ...)  
    {  
        message = ...;  
        return true;  
    }  
  
#if IMPLEMENTING_TRANSPORT_CHANNEL  
    FaultConverter encoderConverter =   
                    this.encoder.GetProperty<FaultConverter>();  
    if ((encoderConverter != null) &&               
        (encoderConverter.TryCreateFaultMessage(  
         exception, out message)))  
    {  
        return true;  
    }  
  
    FaultConverter defaultConverter =   
                   FaultConverter.GetDefaultFaultConverter(  
                   this.channel.messageVersion);  
    return defaultConverter.TryCreateFaultMessage(  
                   exception,   
                   out message);  
#else  
    FaultConverter inner =   
                   this.innerChannel.GetProperty<FaultConverter>();  
    if (inner != null)  
    {  
        return inner.TryCreateFaultMessage(exception, out message);  
    }  
    else  
    {  
        message = null;  
        return false;  
    }  
#endif  
}  
```  
  
 이 패턴의 구현은 오류가 필요한 오류 조건의 계층 사이에서 throw된 예외에 해당 오류 생성기로 올바른 오류를 만들기에 충분한 정보가 있어야 한다는 것입니다. 사용자 지정 채널 작성자는 다양한 오류 조건에 해당하는 예외 형식을 정의할 수 있습니다(그러한 예외가 이미 존재하지 않는 경우). 채널 계층 사이를 이동하는 예외는 불투명 오류 데이터가 아닌 오류 조건을 전달해야 합니다.  
  
### <a name="fault-categories"></a>오류 범주  
 일반적으로 오류에는 세 가지 범주가 있습니다.  
  
1. 전체 스택에 퍼지는 오류. 이러한 오류는 InvalidCardinalityAddressingException와 같이 채널 스택 내의 어느 계층에서나 발생할 수 있습니다.  
  
2. 흐름 트랜잭션이나 보안 역할에 관한 일부 오류의 예와 같이 스택에서 특정 계층 위의 어느 곳에서나 발생할 수 있는 오류.  
  
3. WS-RM 시퀀스 번호 오류와 같이 스택의 단일 계층에 전달되는 오류.  
  
 범주 1. 오류는 일반적으로 WS-Addressing 및 SOAP 오류입니다. WCF에서 `FaultConverter` 제공 하는 기본 클래스는 ws-addressing 및 SOAP에 지정 된 오류 메시지에 해당 하는 오류를 변환 하므로 이러한 예외의 변환을 직접 처리할 필요가 없습니다.  
  
 범주 2. 오류는 계층에 대한 메시지 정보를 완전히 소비하지 않는 메시지에 계층에서 속성을 추가한 경우에 발생합니다. 높은 계층에서 메시지 속성에 추가로 메시지 정보를 처리하도록 요청하는 경우 이후에 오류가 검색될 수 있습니다. 이러한 채널에서는 이전에 지정한 `GetProperty`를 구현하여 높은 계층에서 올바른 오류를 다시 보낼 수 있게 합니다. 이러한 경우의 예에는 TransactionMessageProperty가 있습니다. 이 속성은 헤더에 있는 모든 데이터의 유효성을 완전히 검사하지 않고 메시지에 추가됩니다. 그 과정에서 DTC(Distributed Transaction Coordinator)에 연결해야 할 수도 있습니다.  
  
 범주 3. 오류는 프로세서 내의 단일 계층에서만 생성하여 보냅니다. 따라서 모든 예외는 계층 내에 포함됩니다. 채널 사이의 일관성을 향상시키고 유지 관리를 쉽게 하려면 사용자 지정 채널에서 내부 오류에 대해서도 이전에 지정한 패턴을 사용하여 오류 메시지를 생성해야 합니다.  
  
### <a name="interpreting-received-faults"></a>받은 오류 해석  
 이 단원에서는 오류 메시지를 받을 때 적절한 예외를 생성하는 경우에 대한 안내 자료를 제공합니다. 스택의 모든 계층에서 메시지를 처리하는 경우의 의사 결정 트리는 다음과 같습니다.  
  
1. 계층에서 메시지가 잘못된 것으로 간주하는 경우에는 계층에서 ‘잘못된 메시지’ 처리를 수행해야 합니다. 이러한 처리는 계층별로 적용되지만 메시지의 삭제, 추적 또는 오류로 변환되는 예외 throw 등이 포함될 수도 있습니다. 예에는 보안에서 제대로 보호되지 않은 메시지를 받는 경우나 RM에서 시퀀스 번호가 잘못된 메시지를 받는 경우가 포함됩니다.  
  
2. 그렇지 않은 경우, 메시지가 계층에만 적용되는 오류 메시지이면 계층 상호 작용의 외부에서 메시지가 의미를 갖지 못하기 때문에 계층에서 오류 조건을 처리해야 합니다. 이 경우의 예로는 RM 채널 위의 계층에서는 의미가 없고 RM 채널 안에서만 오류가 발생하며 보류 중인 작업에서 throw되는 RM 시퀀스 거부 오류가 있습니다.  
  
3. 그렇지 않으면 Request() 또는 Receive()에서 메시지가 반환되어야 합니다. 여기에는 계층에서 오류를 인식하지만, 채널에서 오류가 발생하고 보류 중인 작업에서 오류가 throw되는 것을 의미하지는 않고 단지 요청이 실패했다는 사실만을 알리는 경우가 포함됩니다. 이러한 경우에 기능성을 개선하려면 계층에서 `GetProperty<FaultConverter>`를 구현하고, `FaultConverter`을 재정의하여 오류를 예외로 변환할 수 있는 `OnTryCreateException` 파생 클래스를 반환해야 합니다.  
  
 다음 개체 모델에서는 메시지를 예외로 변환하는 기능을 지원합니다.  
  
```csharp  
public class FaultConverter  
{  
    public static FaultConverter GetDefaultFaultConverter(  
                                  MessageVersion version);  
    protected abstract bool OnTryCreateException(  
                                 Message message,   
                                 MessageFault fault,   
                                 out Exception exception);  
    public bool TryCreateException(  
                                 Message message,   
                                 MessageFault fault,   
                                 out Exception exception);  
}  
```  
  
 채널 계층에서는 `GetProperty<FaultConverter>`를 구현하여 오류 메시지를 예외로 변환하는 기능을 지원할 수 있습니다. 그러려면 `OnTryCreateException`을 재정의하고 오류 메시지를 검사합니다. 인식된 경우 변환을 수행하고, 그렇지 않은 경우 내부 채널에 변환을 요청합니다. 전송 채널은 `FaultConverter.GetDefaultFaultConverter`에 위임하여 기본 SOAP/WS-Addressing FaultConverter를 가져와야 합니다.  
  
 일반적인 구현은 다음과 같습니다.  
  
```csharp  
public override bool OnTryCreateException(  
                            Message message,   
                            MessageFault fault,   
                            out Exception exception)  
{  
    if (message.Action == "...")  
    {  
        exception = ...;  
        return true;  
    }  
    // OR  
    if ((fault.Code.Name == "...") && (fault.Code.Namespace == "..."))  
    {  
        exception = ...;  
        return true;  
    }  
  
    if (fault.IsMustUnderstand)  
    {  
        if (fault.WasHeaderNotUnderstood(  
                   message.Headers, "...", "..."))  
        {  
            exception = new ProtocolException(...);  
            return true;  
        }  
    }  
  
#if IMPLEMENTING_TRANSPORT_CHANNEL  
    FaultConverter encoderConverter =   
              this.encoder.GetProperty<FaultConverter>();  
    if ((encoderConverter != null) &&   
        (encoderConverter.TryCreateException(  
                              message, fault, out exception)))  
    {  
        return true;  
    }  
  
    FaultConverter defaultConverter =  
             FaultConverter.GetDefaultFaultConverter(  
                             this.channel.messageVersion);  
    return defaultConverter.TryCreateException(  
                             message, fault, out exception);  
#else  
    FaultConverter inner =   
                    this.innerChannel.GetProperty<FaultConverter>();  
    if (inner != null)  
    {  
        return inner.TryCreateException(message, fault, out exception);  
    }  
    else  
    {  
        exception = null;  
        return false;  
    }  
#endif  
}  
```  
  
 구분되는 복구 시나리오가 있는 특정 오류 조건의 경우에는 `ProtocolException`의 파생된 클래스를 사용하는 것을 고려해 보십시오.  
  
### <a name="mustunderstand-processing"></a>MustUnderstand 처리  
 SOAP에서는 수신기에서 필수 헤더가 이해되지 않은 경우를 나타내기 위한 일반 오류를 정의합니다. 이 오류를 `mustUnderstand` 오류라고 합니다. WCF에서 사용자 지정 채널은 오류 `mustUnderstand` 를 생성 하지 않습니다. 대신 wcf 통신 스택의 맨 위에 있는 WCF 디스패처는 MustUnderstand = true로 표시 된 모든 헤더를 기본 스택에서 인식 하는지 확인 합니다. 이해되지 않은 것이 있으면 그 순간 `mustUnderstand` 오류가 생성됩니다. 사용자는 이 `mustUnderstand` 처리를 끄고 애플리케이션에서 모든 메시지 헤더를 받게 만들 수 있습니다. 그런 경우에는 응용 프로그램에서 `mustUnderstand` 처리를 수행합니다. 생성된 오류에는 MustUnderstand=true이고 이해되지 않은 모든 헤더의 이름이 포함된 NotUnderstood 헤더가 있습니다.  
  
 프로토콜 채널에서 MustUnderstand=true인 사용자 지정 헤더를 보낸 후 `mustUnderstand` 오류를 받은 경우에는 헤더를 보냈기 때문에 발생한 오류인지 여부를 확인해야 합니다. `MessageFault` 클래스에는 여기에 유용한 2개의 멤버가 있습니다.  
  
```csharp  
public class MessageFault  
{  
    ...  
    public bool IsMustUnderstandFault { get; }  
    public static bool WasHeaderNotUnderstood(MessageHeaders headers,   
        string name, string ns) { }  
    ...  
  
}  
```  
  
 오류가 `IsMustUnderstandFault` 오류인 경우 `true`는 `mustUnderstand`를 반환합니다. `WasHeaderNotUnderstood`에서는 지정된 이름과 네임스페이스의 헤더가 오류에 NotUnderstood 헤더로 포함되어 있으면 `true`를 반환합니다.  그 외의 경우 `false`를 반환합니다.  
  
 채널에서 MustUnderstand = true로 표시된 헤더를 전송하면 계층에서도 Exception Generation API 패턴을 구현하고 앞서 설명한 것과 같이 헤더에서 발생한 `mustUnderstand` 오류를 좀더 유용한 예외로 변환해야 합니다.  
  
## <a name="tracing"></a>추적  
 .NET Framework에서는 디버거를 첨부하고 코드를 실행할 수 없는 경우 프로덕션 애플리케이션 또는 일시적인 문제의 진단을 돕는 방법으로서 프로그램 실행을 추적하는 메커니즘을 제공합니다. 이 메커니즘의 핵심 구성 요소는 <xref:System.Diagnostics?displayProperty=nameWithType> 네임스페이스에 있으며 다음으로 구성됩니다.  
  
- <xref:System.Diagnostics.TraceSource?displayProperty=nameWithType>는 쓰려는 추적 정보의 소스이고 <xref:System.Diagnostics.TraceListener?displayProperty=nameWithType>는 <xref:System.Diagnostics.TraceSource>로부터 추적할 정보를 받아 수신기별 대상으로 출력하는 구체적인 수신기의 추상 기본 클래스입니다. 예를 들어 <xref:System.Diagnostics.XmlWriterTraceListener>에서는 추적 정보를 XML 파일로 출력합니다. 마지막으로 <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType>은 애플리케이션 사용자가 추적의 자세한 정도를 추적할 수 있게 해 주며 일반적으로 구성에 지정됩니다.  
  
- 핵심 구성 요소 외에도 [Service Trace Viewer 도구 (svctraceviewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) 를 사용 하 여 WCF 추적을 보고 검색할 수 있습니다. 이 도구는 WCF에 의해 생성 되 고을 사용 하 여 <xref:System.Diagnostics.XmlWriterTraceListener>작성 된 추적 파일용으로 특별히 설계 되었습니다. 다음 그림에서는 추적에 관련된 다양한 구성 요소를 소개합니다.  
  
 ![예외 및 오류 처리](./media/wcfc-tracinginchannelsc.gif "wcfc_TracingInChannelsc")  
  
### <a name="tracing-from-a-custom-channel"></a>사용자 지정 채널에서 추적  
 사용자 지정 채널에서는 디버거를 실행 중인 애플리케이션에 첨부할 수 없는 경우 문제의 진단을 돕기 위한 추적 메시지를 작성해야 합니다. 여기에는 다음과 같은 두 가지 개략적인 작업이 포함 됩니다. 을 <xref:System.Diagnostics.TraceSource> 인스턴스화하고 해당 메서드를 호출 하 여 추적을 작성 합니다.  
  
 <xref:System.Diagnostics.TraceSource>를 인스턴스화하면 지정한 문자열이 소스의 이름이 됩니다. 이 이름은 추적 소스를 구성(활성화/비활성화/추적 수준 설정)하는 데 사용됩니다. 이 이름은 추적 출력 자체에도 표시됩니다. 사용자 지정 채널에서는 추적 출력을 읽는 사람이 추적 정보가 오는 곳을 파악할 수 있도록 고유한 소스 이름을 사용해야 합니다. 일반적으로는 정보를 쓰는 어셈블리의 이름을 추적 소스의 이름으로 사용합니다. 예를 들어 WCF는 system.servicemodel 어셈블리에서 작성 된 정보에 대 한 추적 소스로 System.servicemodel을 사용 합니다.  
  
 추적 소스가 있으면 <xref:System.Diagnostics.TraceSource.TraceData%2A>, <xref:System.Diagnostics.TraceSource.TraceEvent%2A> 또는 <xref:System.Diagnostics.TraceSource.TraceInformation%2A> 메서드를 호출하여 추적 수신기에 추적 항목을 씁니다. 쓰는 각 추적 항목에 대해 이벤트의 형식을 <xref:System.Diagnostics.TraceEventType>에 정의된 이벤트 형식 중 하나로 분류해야 합니다. 구성에서 이 분류와 추적 수준 설정에 따라 추적 항목이 수신기로 출력되는지 여부가 결정됩니다. 예를 들어 구성에서 추적 수준을 `Warning`으로 설정하면 `Warning`, `Error` 및 `Critical` 추적 항목을 쓰고 Information 및 Verbose 항목은 차단합니다. 다음은 추적 소스를 인스턴스화하고 Information 수준에서 항목을 쓰는 경우의 예입니다.  
  
```csharp
using System.Diagnostics;  
//...  
TraceSource udpSource=new TraceSource("Microsoft.Samples.Udp");  
//...  
udpsource.TraceInformation("UdpInputChannel received a message");  
```  
  
> [!IMPORTANT]
> 추적 출력을 읽는 사람이 출력이 온 위치를 파악할 수 있도록 추적 소스 이름을 지정하는 것이 좋습니다.  
  
#### <a name="integrating-with-the-trace-viewer"></a>Trace Viewer와 통합  
 채널에서 생성 된 추적은 추적 수신기로를 사용 <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> 하 여 [서비스 추적 뷰어 도구 (svctraceviewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) 에서 읽을 수 있는 형식으로 출력 될 수 있습니다. 채널 개발자에게는 이 기능이 필요 없습니다. 애플리케이션의 구성 파일에 이 추적 수신기를 구성할 필요가 있는 것은 애플리케이션 사용자(또는 애플리케이션 문제를 해결하는 사람)입니다. 예를 들어 다음 구성에서는 <xref:System.ServiceModel?displayProperty=nameWithType> 및 `Microsoft.Samples.Udp` 모두의 추적 정보를 `TraceEventsFile.e2e`라는 파일로 출력합니다.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <!-- configure System.ServiceModel trace source -->  
      <source name="System.ServiceModel" switchValue="Verbose"   
              propagateActivity="true">  
        <listeners>  
          <add name="e2e" />  
        </listeners>  
      </source>  
      <!-- configure Microsoft.Samples.Udp trace source -->  
      <source name="Microsoft.Samples.Udp" switchValue="Verbose" >  
        <listeners>  
          <add name="e2e" />  
        </listeners>  
      </source>  
    </sources>  
    <!--   
    Define a shared trace listener that outputs to TraceFile.e2e  
    The listener name is e2e   
    -->  
    <sharedListeners>  
      <add name="e2e" type="System.Diagnostics.XmlWriterTraceListener"  
        initializeData=".\TraceFile.e2e"/>  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
</configuration>  
```  
  
#### <a name="tracing-structured-data"></a>구조적 데이터 추적  
 <xref:System.Diagnostics.TraceSource?displayProperty=nameWithType>에는 추적 항목에 포함할 개체를 하나 이상 가져오는 <xref:System.Diagnostics.TraceSource.TraceData%2A> 메서드가 있습니다. 일반적으로 <xref:System.Object.ToString%2A?displayProperty=nameWithType> 메서드는 각 개체에서 호출되며 결과 문자열은 추적 항목의 일부로 기록됩니다. <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>를 사용하여 추적을 출력하는 경우 <xref:System.Xml.XPath.IXPathNavigable?displayProperty=nameWithType>을 데이터 개체로 <xref:System.Diagnostics.TraceSource.TraceData%2A>에 전달할 수 있습니다. 결과 추적 항목에는 <xref:System.Xml.XPath.XPathNavigator?displayProperty=nameWithType>에서 제공되는 XML이 포함됩니다. 다음은 XML 애플리케이션 데이터의 항목 예입니다.  
  
```xml  
<E2ETraceEvent xmlns="http://schemas.microsoft.com/2004/06/E2ETraceEvent">  
  <System xmlns="...">  
    <EventID>12</EventID>  
    <Type>3</Type>  
    <SubType Name="Information">0</SubType>  
    <Level>8</Level>  
    <TimeCreated SystemTime="2006-01-13T22:58:03.0654832Z" />  
    <Source Name="Microsoft.ServiceModel.Samples.Udp" />  
    <Correlation ActivityID="{00000000-0000-0000-0000-000000000000}" />  
    <Execution  ProcessName="UdpTestConsole"   
                ProcessID="3348" ThreadID="4" />  
    <Channel />  
    <Computer>COMPUTER-LT01</Computer>  
  </System>  
<!-- XML application data -->  
  <ApplicationData>  
  <TraceData>  
   <DataItem>  
   <TraceRecord   
     Severity="Information"  
     xmlns="…">  
        <TraceIdentifier>some trace id</TraceIdentifier>  
        <Description>EndReceive called</Description>  
        <AppDomain>UdpTestConsole.exe</AppDomain>  
        <Source>UdpInputChannel</Source>  
      </TraceRecord>  
    </DataItem>  
  </TraceData>  
  </ApplicationData>  
</E2ETraceEvent>  
```  
  
 WCF 추적 뷰어는 이전에 표시 된 `TraceRecord` 요소의 스키마를 이해 하 고 자식 요소에서 데이터를 추출 하 여 테이블 형식으로 표시 합니다. 채널에서는 Svctraceviewer.exe 사용자가 데이터를 읽는 데 도움이 되도록 구조적 애플리케이션 데이터를 추적할 때 이 스키마를 사용해야 합니다.
