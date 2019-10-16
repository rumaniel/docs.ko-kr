---
title: 작업 포맷터와 작업 선택기
ms.date: 03/30/2017
ms.assetid: 1c27e9fe-11f8-4377-8140-828207b98a0e
ms.openlocfilehash: 5853a791a92535c970f8010dd08d42e10292ffa8
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039040"
---
# <a name="operation-formatter-and-operation-selector"></a>작업 포맷터와 작업 선택기
이 샘플에서는 wcf (Windows Communication Foundation) 확장 요소를 사용 하 여 WCF에서 예상 하는 것과 다른 형식의 메시지 데이터를 허용 하는 방법을 보여 줍니다. 기본적으로 WCF 포맷터는 메서드 매개 변수를 `soap:body` 요소 아래에 포함 해야 합니다. 이 샘플에서는 대신 HTTP GET 쿼리 문자열의 매개 변수 데이터를 구문 분석하고 이 데이터를 사용하여 메서드를 호출하는 사용자 지정 작업 포맷터를 구현하는 방법을 보여 줍니다.  
  
 이 샘플은 `ICalculator` 서비스 계약을 구현 하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. 이 샘플에서는 클라이언트에서 서버로 보내는 요청에 대해 HTTP GET를 사용하고 서버에서 클라이언트로 보내는 응답에 대해 POX 메시지가 포함된 HTTP POST를 사용하도록 Add, Subtract, Multiply 및 Divide 메시지를 변경하는 방법을 보여 줍니다.  
  
 이를 위해 이 샘플에서는 다음을 제공합니다.  
  
- `QueryStringFormatter`(클라이언트와 서버에 대해 각각 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 및 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>를 구현하고 쿼리 문자열의 데이터를 처리합니다.)  
  
- `UriOperationSelector`(서버에서 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector>를 구현하여 GET 요청의 작업 이름을 기반으로 작업 디스패치를 수행합니다.)  
  
- `EnableHttpGetRequestsBehavior` 엔드포인트 동작과 해당 구성(런타임에 필요한 작업 선택기를 추가합니다.)  
  
- 런타임에 새 작업 포맷터를 삽입하는 방법을 보여 줍니다.  
  
- 이 샘플에서 클라이언트와 서비스는 모두 콘솔 애플리케이션(.exe)입니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
## <a name="key-concepts"></a>주요 개념  
 `QueryStringFormatter`-작업 포맷터는 메시지를 매개 변수 개체의 배열로 변환 하 고 매개 변수 개체의 배열을 메시지로 변환 하는 작업을 담당 하는 WCF의 구성 요소입니다. 이 작업은 클라이언트에서는 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 인터페이스를 사용하고 서버에서는 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> 인터페이스를 사용하여 수행됩니다. 사용자는 이러한 인터페이스를 사용하여 `Serialize` 및 `Deserialize` 메서드에서 요청 및 응답 메시지를 가져올 수 있습니다.  
  
 이 샘플에서 `QueryStringFormatter`는 이 두 가지 인터페이스를 모두 구현하며, 클라이언트와 서버에서 구현됩니다.  
  
 요청:  
  
- 이 샘플에서는 <xref:System.ComponentModel.TypeConverter> 클래스를 사용하여 요청 메시지의 매개 변수 데이터를 문자열로 변환하고 문자열을 매개 변수 데이터로 변환합니다. 특정 형식에 대해 <xref:System.ComponentModel.TypeConverter>를 사용할 수 없는 경우 샘플 포맷터는 예외를 throw합니다.  
  
- 클라이언트의 `IClientMessageFormatter.SerializeRequest` 메서드에서 포맷터는 적절한 받는 사람 주소가 포함된 URI를 만들고 작업 이름을 접미사로 추가합니다. 이 이름은 서버의 적절한 작업으로 디스패치하는 데 사용됩니다. 그런 다음 포맷터는 매개 변수 개체의 배열을 가져와서 매개 변수 이름 및 <xref:System.ComponentModel.TypeConverter> 클래스를 통해 변환된 값을 사용하여 매개 변수 데이터를 URI 쿼리 문자열로 serialize합니다. 그런 다음 <xref:System.ServiceModel.Channels.MessageHeaders.To%2A> 및 <xref:System.ServiceModel.Channels.MessageProperties.Via%2A> 속성이 이 URI로 설정됩니다. <xref:System.ServiceModel.Channels.MessageProperties>는 <xref:System.ServiceModel.Channels.Message.Properties%2A> 속성을 통해 액세스됩니다.  
  
- 서버의 `IDispatchMessageFormatter.DeserializeRequest` 메서드에서 포맷터는 들어오는 요청 메시지 속성에서 `Via` URI를 검색합니다. 포맷터는 URI 쿼리 문자열의 이름-값 쌍을 매개 변수 이름과 값으로 구문 분석하고 매개 변수 이름과 값을 사용하여 메서드로 전달되는 매개 변수의 배열을 채웁니다. 작업 디스패치가 이미 발생했으므로 이 메서드에서는 작업 이름 접미사가 무시됩니다.  
  
 응답:  
  
- 이 샘플에서 HTTP GET는 요청에만 사용됩니다. 포맷터는 XML 메시지를 생성하는 데 사용된 원래 포맷터에 응답 보내기 작업을 위임합니다. 이 샘플의 목적 중 하나는 이러한 위임 포맷터를 구현하는 방법을 보여 주는 데 있습니다.  
  
### <a name="uripathsuffixoperationselector-class"></a>UriPathSuffixOperationSelector 클래스  
 사용자는 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> 인터페이스를 사용하여 특정 메시지를 디스패치할 작업에 대한 고유 논리를 구현할 수 있습니다.  
  
 이 샘플에서는 작업 이름이 메시지의 동작 헤더가 아닌 HTTP GET URI에 포함되어 있기 때문에 적절한 작업을 선택하려면 서버에 `UriPathSuffixOperationSelector`가 구현되어 있어야 합니다. 이 샘플은 대/소문자를 구분하는 작업 이름만 허용하도록 설정되어 있습니다.  
  
 `SelectOperation` 메서드는 들어오는 메시지를 받아 메시지 속성에서 `Via` URI를 조회합니다. 그런 다음 URI에서 작업 이름 접미사를 추출하고 내부 테이블을 조회하여 메시지를 디스패치할 작업 이름을 가져온 다음 이 작업 이름을 반환합니다.  
  
### <a name="enablehttpgetrequestsbehavior-class"></a>EnableHttpGetRequestsBehavior 클래스  
 `UriPathSuffixOperationSelector` 구성 요소는 프로그래밍 방식으로 설치하거나 엔드포인트 동작을 통해 설치할 수 있습니다. 이 샘플에서는 서비스의 애플리케이션 구성 파일에 지정된 `EnableHttpGetRequestsBehavior` 동작을 구현합니다.  
  
 서버측:  
  
 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.OperationSelector%2A>는 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> 구현으로 설정됩니다.  
  
 기본적으로 WCF는 정확히 일치 하는 주소 필터를 사용 합니다. 들어오는 메시지의 URI는 작업 이름 접미사와, 그 뒤에 매개 변수 데이터가 포함된 쿼리 문자열로 구성되므로 엔드포인트 동작은 주소 필터를 접미사 일치 필터가 되도록 변경합니다. 이를 위해 WCF<xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter> 를 사용 합니다.  
  
### <a name="installing-operation-formatters"></a>작업 포맷터 설치  
 포맷터를 지정하는 작업 동작은 고유합니다. 이러한 동작은 모든 작업이 필요한 작업 포맷터를 만들 수 있도록 항상 기본적으로 구현됩니다. 그러나 이러한 동작은 단지 다른 작업 동작과 유사하게 보이며 다른 특성으로도 식별할 수 없습니다. 대체 동작을 설치 하려면 구현은 기본적으로 WCF 형식 로더에 의해 설치 되는 특정 포맷터 동작을 검색 하 고이를 대체 하거나 기본 동작 후에 실행할 호환 되는 동작을 추가 해야 합니다.  
  
 이러한 작업 포맷터 동작은 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=nameWithType>을 호출하기 전에 프로그래밍 방식으로 설치하거나, 기본 동작 이후에 실행되는 작업 동작을 지정하여 설치할 수 있습니다. 그러나 동작 모델에서는 동작이 다른 동작을 대체하거나 설명 트리를 수정하는 것을 허용하지 않기 때문에 이러한 작업 포맷터 동작을 엔드포인트 동작이나 구성을 통해 쉽게 설치할 수 없습니다.  
  
 클라이언트에서:  
  
 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 구현은 요청을 HTTP GET 요청으로 변환하고 응답의 원래 포맷터에 위임할 수 있도록 구현되어야 합니다. 이 작업은 `EnableHttpGetRequestsBehavior.ReplaceFormatterBehavior` 도우미 메서드를 호출하여 수행됩니다.  
  
 이 작업은 `CreateChannel`을 호출하기 전에 수행되어야 합니다.  
  
```  
void ReplaceFormatterBehavior(OperationDescription operationDescription, EndpointAddress address)  
{  
    // Remove the DataContract behavior if it is present.  
    IOperationBehavior formatterBehavior = operationDescription.Behaviors.Remove<DataContractSerializerOperationBehavior>();  
    if (formatterBehavior == null)  
    {  
        // Remove the XmlSerializer behavior if it is present.  
        formatterBehavior = operationDescription.Behaviors.Remove<XmlSerializerOperationBehavior>();  
        ...  
    }  
  
    // Remember what the innerFormatterBehavior was.  
    DelegatingFormatterBehavior delegatingFormatterBehavior = new DelegatingFormatterBehavior(address);  
    delegatingFormatterBehavior.InnerFormatterBehavior = formatterBehavior;  
   operationDescription.Behaviors.Add(delegatingFormatterBehavior);  
}  
```  
  
 서버측:  
  
- <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> 인터페이스는 HTTP GET 요청을 읽고 응답 쓰기의 원래 포맷터에 위임할 수 있도록 구현되어야 합니다. 이 작업은 클라이언트와 같은 `EnableHttpGetRequestsBehavior.ReplaceFormatterBehavior` 도우미 메서드(이전의 코드 샘플 참조)를 호출하여 수행됩니다.  
  
- 이 작업은 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>을 호출하기 전에 수행되어야 합니다. 이 샘플에서는 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>을 호출하기 전에 포맷터를 수동으로 수정하는 방법을 보여 줍니다. 같은 결과를 얻을 수 있는 다른 방법은 열기 전에 <xref:System.ServiceModel.ServiceHost>를 호출하는 `EnableHttpGetRequestsBehavior.ReplaceFormatterBehavior`에서 클래스를 파생하는 것입니다. 자세한 예는 호스팅 설명서와 샘플을 참조하십시오.  
  
### <a name="user-experience"></a>사용자 환경  
 서버측:  
  
- 서버 `ICalculator` 구현은 변경할 필요가 없습니다.  
  
- 서비스의 App.config에서는 `messageVersion` 요소의 `textMessageEncoding` 특성을 `None`으로 설정하는 사용자 지정 POX 바인딩을 사용해야 합니다.  
  
    ```xml  
    <bindings>  
      <customBinding>  
        <binding name="poxBinding">  
          <textMessageEncoding messageVersion="None" />  
          <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
- 서비스의 App.config에서는 또한 사용자 지정 `EnableHttpGetRequestsBehavior`를 동작 확장명 섹션에 추가한 다음 사용하여 이를 지정해야 합니다.  
  
    ```xml  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="enableHttpGetRequestsBehavior">  
          <enableHttpGetRequests />  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
  
    <extensions>  
      <behaviorExtensions>  
        <!-- Enabling HTTP GET requests: Behavior Extension -->  
        <add   
          name="enableHttpGetRequests"           type="Microsoft.ServiceModel.Samples.EnableHttpGetRequestsBehaviorElement, QueryStringFormatter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
      </behaviorExtensions>  
    </extensions>  
    ```  
  
- <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>을 호출하기 전에 작업 포맷터를 추가합니다.  
  
 클라이언트에서:  
  
- 클라이언트 구현은 변경할 필요가 없습니다.  
  
- 클라이언트의 App.config에서는 `messageVersion` 요소의 `textMessageEncoding` 특성을 `None`으로 설정하는 사용자 지정 POX 바인딩을 사용해야 합니다. 서비스와 다른 한 가지 차이점은 클라이언트는 나가는 받는 사람 주소를 수정할 수 있도록 수동 주소 지정을 사용하도록 설정해야 한다는 점에 있습니다.  
  
    ```xml  
    <bindings>  
      <customBinding>  
        <binding name="poxBinding">  
          <textMessageEncoding messageVersion="None" />  
          <httpTransport manualAddressing="True" />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
- 클라이언트의 App.config에서는 서버와 같은 사용자 지정 `EnableHttpGetRequestsBehavior`를 지정해야 합니다.  
  
- <xref:System.ServiceModel.ChannelFactory%601.CreateChannel>을 호출하기 전에 작업 포맷터를 추가합니다.  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 네 가지 작업(Add, Subtract, Multiply 및 Divide)이 모두 성공해야 합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Formatters\QueryStringFormatter`  
  
##### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
