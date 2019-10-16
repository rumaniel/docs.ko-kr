---
title: '전송: UDP'
ms.date: 03/30/2017
ms.assetid: 738705de-ad3e-40e0-b363-90305bddb140
ms.openlocfilehash: 051b5d6c7a1fc5d110016be9faf9b08653c28a6e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045441"
---
# <a name="transport-udp"></a>전송: UDP
UDP 전송 샘플은 UDP 유니캐스트 및 멀티 캐스트를 WCF (사용자 지정 Windows Communication Foundation) 전송으로 구현 하는 방법을 보여 줍니다. 이 샘플에서는 채널 프레임 워크 및 WCF 모범 사례를 사용 하 여 WCF에서 사용자 지정 전송을 만드는 권장 절차에 대해 설명 합니다. 사용자 지정 전송을 만드는 단계는 다음과 같습니다.  
  
1. ChannelFactory 및 ChannelListener에서 지원할 채널 [메시지 교환 패턴](#MessageExchangePatterns) (Ioutputchannel, IInputChannel, IDuplexChannel, IRequestChannel 또는 IReplyChannel)을 결정 합니다. 그런 다음 이러한 인터페이스의 세션 변형을 지원할지 여부를 결정합니다.  
  
2. 메시지 교환 패턴을 지원하는 채널 팩터리 및 수신기를 만듭니다.  
  
3. 네트워크 관련 예외가 <xref:System.ServiceModel.CommunicationException>의 적절한 파생 클래스로 정규화되는지 확인합니다.  
  
4. 사용자 지정 전송을 채널 스택에 추가 하는 [ 바인딩>요소를추가합니다.\<](../../../../docs/framework/misc/binding.md) 자세한 내용은 [바인딩 요소 추가](#AddingABindingElement)를 참조 하세요.  
  
5. 새 바인딩 요소가 구성 시스템에 노출되도록 바인딩 요소 확장명 섹션을 추가합니다.  
  
6. 기능을 다른 엔드포인트에 전달하도록 메타데이터 확장을 추가합니다.  
  
7. 올바르게 정의된 프로필에 따라 바인딩 요소 스택을 미리 구성하는 바인딩을 추가합니다. 자세한 내용은 [표준 바인딩 추가](#AddingAStandardBinding)를 참조 하세요.  
  
8. 바인딩이 구성 시스템에 노출되도록 바인딩 섹션 및 바인딩 구성 요소를 추가합니다. 자세한 내용은 [구성 지원 추가](#AddingConfigurationSupport)를 참조 하세요.  
  
<a name="MessageExchangePatterns"></a>   
## <a name="message-exchange-patterns"></a>메시지 교환 패턴  
 사용자 지정 전송을 작성하는 첫 번째 단계는 전송에 필요한 MEP(메시지 교환 패턴)를 결정하는 것입니다. 다음과 같은 세 개의 MEP가 있습니다.  
  
- 데이터그램(IInputChannel/IOutputChannel)  
  
     데이터그램 MEP를 사용하면 클라이언트가 메시지를 보낸 후 회신을 기다리지 않는 "fire and forget" 교환을 사용하여 메시지를 보냅니다. 실행 후 제거 교환은 성공적인 전달에 대한 out-of-band 확인이 필요한 교환입니다. 메시지는 전송 중에 손실되어 서비스에 전달되지 않을 수 있습니다. 보내기 작업이 클라이언트 쪽에서 완료되더라도 원격 엔드포인트에서 메시지를 수신했다고 보장할 수는 없습니다. 데이터그램은 메시징을 위한 기본적인 빌딩 블록으로, 이 위에 신뢰할 수 있는 프로토콜 및 보안 프로토콜을 포함한 고유 프로토콜을 빌드할 수 있습니다. 클라이언트 데이터그램 채널은 <xref:System.ServiceModel.Channels.IOutputChannel> 인터페이스를 구현하고, 서비스 데이터그램 채널은 <xref:System.ServiceModel.Channels.IInputChannel> 인터페이스를 구현합니다.  
  
- 요청-응답(IRequestChannel/IReplyChannel)  
  
     이 MEP에서는 메시지가 전송되고 회신이 수신됩니다. 이 패턴은 요청-응답 쌍으로 구성됩니다. 요청-응답 호출의 예로 RPC(원격 프로시저 호출)와 브라우저 GET를 들 수 있습니다. 이 패턴을 반이중이라고도 합니다. 이 MEP에서 클라이언트 채널은 <xref:System.ServiceModel.Channels.IRequestChannel>을 구현하고 서비스 채널은 <xref:System.ServiceModel.Channels.IReplyChannel>을 구현합니다.  
  
- 이중(IDuplexChannel)  
  
     이중 MEP를 사용하면 임의 개수의 메시지를 클라이언트에서 보내고 임의의 순서로 받을 수 있습니다. 이중 MEP는 말로 전달되는 각 단어가 메시지에 해당하는 전화 통화와 같습니다. 이 MEP에서는 양측의 송/수신이 가능하기 때문에 클라이언트와 서비스 채널에서 <xref:System.ServiceModel.Channels.IDuplexChannel> 인터페이스를 구현합니다.  
  
 또한 이러한 MEP는 각각 세션을 지원합니다. 채널에서 보내고 받은 모든 메시지를 상호 연결하는 기능이 세션 인식 채널에서 제공하는 기능에 추가되었습니다. 요청과 회신이 상호 연결되어 있기 때문에 요청-응답 패턴은 두 메시지로 구성된 독립 실행형 세션입니다. 반면 세션을 지원하는 요청-응답 패턴은 해당 채널의 모든 요청/응답 쌍이 서로 연결되어 있습니다. 따라서 데이터그램, 요청-응답, 이중, 세션 있는 데이터그램, 세션 있는 요청-응답 및 세션 있는 이중 등 6가지 MEP 중에서 선택할 수 있습니다.  
  
> [!NOTE]
> UDP 전송의 경우 UDP는 본래 "fire and forget" 프로토콜이므로 데이터그램 MEP만 지원됩니다.  
  
### <a name="the-icommunicationobject-and-the-wcf-object-lifecycle"></a>ICommunicationObject 및 WCF 개체 수명 주기  
 WCF에는 통신에 사용 되는, <xref:System.ServiceModel.Channels.IChannel> <xref:System.ServiceModel.Channels.IChannelFactory>및 <xref:System.ServiceModel.Channels.IChannelListener> 와 같은 개체의 수명 주기를 관리 하는 데 사용 되는 공용 상태 시스템이 있습니다. 이러한 통신 개체의 상태는 5가지로 나타낼 수 있습니다. 이러한 상태는 <xref:System.ServiceModel.CommunicationState> 열거형으로 나타내며 다음과 같습니다.  
  
- 만들어지며 이는 처음 인스턴스화될 <xref:System.ServiceModel.ICommunicationObject> 때의 상태입니다. 이 상태에서는 I/O(입/출력)이 발생하지 않습니다.  
  
- 연 를 호출 하면 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 개체가이 상태로 전환 됩니다. 이때 속성은 변경할 수 없으며 입/출력이 시작될 수 있습니다. Created 상태에서만 이 상태로 전환될 수 있습니다.  
  
- 열 열기 프로세스가 완료 되 면 개체는이 상태로 전환 됩니다. Opening 상태에서만 이 상태로 전환될 수 있습니다. 이때 개체는 전송을 위해 충분히 사용 가능한 상태입니다.  
  
- 닫고 정상적인 종료를 위해가 호출 <xref:System.ServiceModel.ICommunicationObject.Close%2A> 되 면 개체는이 상태로 전환 됩니다. Opened 상태에서만 이 상태로 전환될 수 있습니다.  
  
- 닫히면 에서 닫힘 상태의 개체는 더 이상 사용할 수 없습니다. 일반적으로 검사를 위해 대부분의 구성에 액세스할 수 있지만 통신은 이루어질 수 없습니다. 이 상태는 삭제된 상태와 같습니다.  
  
- 오류가 오류가 발생 한 상태에서 개체를 검사할 수 있지만 더 이상 사용할 수 없습니다. 복구 불가능한 오류가 발생하면 해당 개체는 이 상태로 전환됩니다. 이 상태 `Closed` 에서 유일 하 게 유효한 전환은 상태입니다.  
  
 각 상태 전환 시 실행되는 이벤트가 있습니다. <xref:System.ServiceModel.ICommunicationObject.Abort%2A> 메서드는 언제든지 호출 가능하며, 개체가 현재 상태에서 Closed 상태로 즉시 전환되게 합니다. <xref:System.ServiceModel.ICommunicationObject.Abort%2A>를 호출하면 완료되지 않은 작업이 모두 종료됩니다.  
  
<a name="ChannelAndChannelListener"></a>   
## <a name="channel-factory-and-channel-listener"></a>채널 팩터리 및 채널 수신기  
 사용자 지정 전송을 작성하는 다음 단계는 클라이언트 채널을 위한 <xref:System.ServiceModel.Channels.IChannelFactory> 및 서비스 채널을 위한 <xref:System.ServiceModel.Channels.IChannelListener>의 구현을 만드는 것입니다. 채널 계층은 채널을 만들기 위해 팩토리 패턴을 사용합니다. WCF는이 프로세스에 대 한 기본 클래스 도우미를 제공 합니다.  
  
- <xref:System.ServiceModel.Channels.CommunicationObject> 클래스는 <xref:System.ServiceModel.ICommunicationObject>를 구현하고 2단계에서 설명한 상태 시스템을 적용합니다. 

- <xref:System.ServiceModel.Channels.ChannelManagerBase> 클래스는 <xref:System.ServiceModel.Channels.CommunicationObject>를 구현하고 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 및 <xref:System.ServiceModel.Channels.ChannelListenerBase>에 대한 통합 기본 클래스를 제공합니다. <xref:System.ServiceModel.Channels.ChannelManagerBase> 클래스는 <xref:System.ServiceModel.Channels.ChannelBase>을 구현하는 기본 클래스인 <xref:System.ServiceModel.Channels.IChannel>와 함께 사용됩니다.  
  
- 클래스 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 는 및 <xref:System.ServiceModel.Channels.ChannelManagerBase> `CreateChannel` `OnCreateChannel` 를 구현 하 고 오버 로드를 하나의 추상 메서드에 통합 합니다. <xref:System.ServiceModel.Channels.IChannelFactory>  
  
- <xref:System.ServiceModel.Channels.ChannelListenerBase> 클래스는 <xref:System.ServiceModel.Channels.IChannelListener>을 구현합니다. 이 클래스는 기본 상태 관리를 담당합니다.  
  
 이 샘플에서 팩터리 구현은 UdpChannelFactory.cs에 포함되어 있고, 수신기 구현은 UdpChannelListener.cs에 포함되어 있습니다. <xref:System.ServiceModel.Channels.IChannel> 구현은 UdpOutputChannel.cs 및 UdpInputChannel.cs에 있습니다.  
  
### <a name="the-udp-channel-factory"></a>UDP 채널 팩터리  
 `UdpChannelFactory`는 <xref:System.ServiceModel.Channels.ChannelFactoryBase>에서 파생됩니다. 샘플에서는 메시지 인코더의 메시지 버전에 액세스할 수 있도록 <xref:System.ServiceModel.Channels.ChannelFactoryBase.GetProperty%2A>를 재정의합니다. 또한 샘플에서는 상태 시스템이 전환될 때 <xref:System.ServiceModel.Channels.ChannelFactoryBase.OnClose%2A>의 인스턴스를 중지할 수 있도록 <xref:System.ServiceModel.Channels.BufferManager>를 재정의합니다.  
  
#### <a name="the-udp-output-channel"></a>UDP 출력 채널  
 `UdpOutputChannel`은 <xref:System.ServiceModel.Channels.IOutputChannel>을 구현합니다. 생성자는 인수의 유효성을 검사하여 전달되는 <xref:System.Net.EndPoint>를 기반으로 대상 <xref:System.ServiceModel.EndpointAddress> 개체를 구성합니다.  
  
```csharp
this.socket = new Socket(this.remoteEndPoint.AddressFamily, SocketType.Dgram, ProtocolType.Udp);  
```  
  
 채널이 정상적 또는 비정상적으로 닫힐 수 있습니다. 채널이 정상적으로 닫히면 소켓이 닫히고 기본 클래스 `OnClose` 메서드가 호출됩니다. 이 때 예외가 throw되면 인프라가 `Abort`를 호출하여 채널을 정리합니다.  
  
```csharp
this.socket.Close(0);  
```  
  
 그런 다음 및 `Send()` 를 `BeginSend()` / 구현합니다`EndSend()`. 그러면 두 개의 기본 섹션으로 분할됩니다. 먼저 메시지를 바이트 배열로 serialize합니다.  
  
```csharp
ArraySegment<byte> messageBuffer = EncodeMessage(message);  
```  
  
 그런 다음 네트워크를 통해 결과 데이터를 보냅니다.  
  
```csharp
this.socket.SendTo(messageBuffer.Array, messageBuffer.Offset, messageBuffer.Count, SocketFlags.None, this.remoteEndPoint);  
```  
  
### <a name="the-udpchannellistener"></a>UdpChannelListener  
 샘플 `UdpChannelListener` 에서 구현 하는는 <xref:System.ServiceModel.Channels.ChannelListenerBase> 클래스에서 파생 됩니다. 단일 UDP 소켓을 사용하여 데이터그램을 받습니다. `OnOpen` 메서드는 비동기 루프에서 UDP 소켓을 사용하여 데이터를 받습니다. 그런 다음 데이터는 메시지 인코딩 프레임워크를 통해 메시지로 변환됩니다.  
  
```csharp
message = MessageEncoderFactory.Encoder.ReadMessage(new ArraySegment<byte>(buffer, 0, count), bufferManager);  
```  
  
 같은 데이터그램 채널은 여러 소스에서 도착한 메시지를 나타내므로 `UdpChannelListener`는 singleton 수신기입니다. 한 번에 최대 하나의 활성 <xref:System.ServiceModel.Channels.IChannel> 이이 수신기에 연결 되어 있습니다. 이 샘플에서는 `AcceptChannel` 메서드에서 반환되는 채널이 이후에 삭제되는 경우에만 새 채널을 생성합니다. 메시지를 받으면 이 singleton 채널의 큐에 삽입됩니다.  
  
#### <a name="udpinputchannel"></a>UdpInputChannel  
 `UdpInputChannel` 클래스는 `IInputChannel`을 구현합니다. 이 클래스는 `UdpChannelListener`의 소켓으로 채워지는 들어오는 메시지의 큐로 구성됩니다. 이러한 메시지는 `IInputChannel.Receive` 메서드에 의해 큐에서 제거됩니다.  
  
<a name="AddingABindingElement"></a>   
## <a name="adding-a-binding-element"></a>바인딩 요소 추가  
 이제 팩터리와 채널이 빌드되었으므로 바인딩을 통해 ServiceModel 런타임에 팩터리와 채널을 노출해야 합니다. 바인딩은 서비스 주소와 연결된 통신 스택을 나타내는 바인딩 요소의 컬렉션입니다. 스택의 각 요소는 [ \<binding >](../../../../docs/framework/misc/binding.md) 요소로 표시 됩니다.  
  
 이 샘플에서 바인딩 요소는 `UdpTransportBindingElement`에서 파생된 <xref:System.ServiceModel.Channels.TransportBindingElement>로, 바인딩에 연결되는 팩터리를 빌드하기 위해 다음 메서드를 재정의합니다.  
  
```csharp
public IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
{  
    return (IChannelFactory<TChannel>)(object)new UdpChannelFactory(this, context);  
}  
  
public IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
{  
    return (IChannelListener<TChannel>)(object)new UdpChannelListener(this, context);  
}  
```  
  
 이 바인딩 요소에는 `BindingElement`를 복제하고 soap.udp 체계를 반환하는 멤버도 포함됩니다.  
  
## <a name="adding-metadata-support-for-a-transport-binding-element"></a>전송 바인딩 요소에 대해 메타데이터 지원 추가  
 전송을 메타데이터 시스템에 통합하려면 정책 가져오기 및 내보내기를 모두 지원해야 합니다. 이를 통해 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)를 통해 바인딩의 클라이언트를 생성할 수 있습니다.  
  
### <a name="adding-wsdl-support"></a>WSDL 지원 추가  
 바인딩의 전송 바인딩 요소는 메타데이터에서 주소 지정 정보를 내보내고 가져옵니다. 또한 전송 바인딩 요소는 SOAP 바인딩을 사용할 때 메타데이터에서 올바른 전송 URI을 내보낼 수 있어야 합니다.  
  
#### <a name="wsdl-export"></a>WSDL 내보내기  
 주소 지정 정보를 내보내기 위해 `UdpTransportBindingElement`는 `IWsdlExportExtension` 인터페이스를 구현합니다. `ExportEndpoint` 메서드는 WSDL 포트에 올바른 주소 지정 정보를 추가합니다.  
  
```csharp
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 엔드포인트에서 SOAP 바인딩을 사용할 때 `UdpTransportBindingElement` 메서드의 `ExportEndpoint` 구현이 전송 URI도 내보냅니다.  
  
```csharp
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### <a name="wsdl-import"></a>WSDL 가져오기  
 주소 가져오기를 처리하기 위해 WSDL 가져오기 시스템을 확장하려면 Svcutil.exe.config 파일에서처럼 Svcutil.exe의 구성 파일에 다음 구성을 추가해야 합니다.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <wsdlImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Svcutil.exe를 실행하는 경우 Svcutil.exe에서 WSDL 가져오기 확장을 로드하는 방법은 두 가지가 있습니다.  
  
1. /SvcutilConfig:\<file >를 사용 하 여 svcutil.exe를 구성 파일에 지정 합니다.  
  
2. Svcutil.exe와 동일한 디렉터리에 있는 Svcutil.exe.config에 구성 섹션을 추가합니다.  
  
 `UdpBindingElementImporter` 형식은 `IWsdlImportExtension` 인터페이스를 구현합니다. `ImportEndpoint` 메서드는 WSDL 포트로부터 주소를 가져옵니다.  
  
```csharp
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### <a name="adding-policy-support"></a>정책 지원 추가  
 사용자 지정 바인딩 요소는 서비스 엔드포인트가 해당 바인딩 요소의 기능을 표현하도록 WSDL 바인딩에서 정책 어설션을 내보낼 수 있습니다.  
  
#### <a name="policy-export"></a>정책 내보내기  
 형식은 정책 내보내기 `IPolicyExportExtension` 에 대 한 지원을 추가 하기 위해을 구현 합니다. `UdpTransportBindingElement` 그 결과, `System.ServiceModel.MetadataExporter`는 이를 포함하는 모든 바인딩에 대한 정책 생성에 `UdpTransportBindingElement`를 포함합니다.  
  
 `IPolicyExportExtension.ExportPolicy`에서는 멀티캐스트 모드인 경우 UDP용 어설션 및 다른 어설션을 추가합니다. 이는 멀티캐스트 모드가 통신 스택의 구성 방법에 영향을 주므로 양쪽 모두에서 조정되어야 하기 때문입니다.  
  
```csharp
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(
        UdpPolicyStrings.Prefix, 
        UdpPolicyStrings.MulticastAssertion, 
        UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 사용자 지정 전송 바인딩 요소가 주소 지정을 처리하기 때문에 `IPolicyExportExtension`에서의 `UdpTransportBindingElement` 구현 역시 사용 중인 WS-Addressing의 버전을 나타내기 위해 적절한 WS-Addressing 정책 어설션 내보내기를 처리해야 합니다.  
  
```csharp
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### <a name="policy-import"></a>정책 가져오기  
 정책 가져오기 시스템을 확장하려면 Svcutil.exe.config 파일에서처럼 Svcutil.exe의 구성 파일에 다음 구성을 추가해야 합니다.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <policyImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 그런 다음 등록된 클래스(`IPolicyImporterExtension`)로부터 `UdpBindingElementImporter`을 구현합니다. `ImportPolicy()`에서는 네임스페이스의 어설션을 검토하면서 전송 생성을 위한 어설션을 처리하고 멀티캐스트인지 여부를 확인합니다. 또한 처리하는 어설션을 바인딩 어설션 목록에서 제거해야 합니다. 다시 한 번 말하지만 Svcutil.exe를 실행할 때 통합하는 방법은 두 가지가 있습니다.  
  
1. /SvcutilConfig:\<file >를 사용 하 여 svcutil.exe를 구성 파일에 지정 합니다.  
  
2. Svcutil.exe와 동일한 디렉터리에 있는 Svcutil.exe.config에 구성 섹션을 추가합니다.  
  
<a name="AddingAStandardBinding"></a>   
## <a name="adding-a-standard-binding"></a>표준 바인딩 추가  
 바인딩 요소를 다음 두 가지 방법으로 사용할 수 있습니다.  
  
- 사용자 지정 바인딩을 통해: 사용자 지정 바인딩을 사용 하면 임의의 바인딩 요소 집합을 기반으로 고유한 바인딩을 만들 수 있습니다.  
  
- 해당 바인딩 요소가 포함된 시스템 제공 바인딩 사용 WCF는 `BasicHttpBinding`, `NetTcpBinding`, `WsHttpBinding`등의 다양 한 시스템 정의 바인딩을 제공 합니다. 이러한 바인딩 각각은 제대로 정의된 프로필에 연결됩니다.  
  
 샘플에서는 `SampleProfileUdpBinding`에서 파생된 <xref:System.ServiceModel.Channels.Binding>의 프로필 바인딩을 구현합니다. `SampleProfileUdpBinding`은 최대 네 개의 바인딩 요소, 즉 `UdpTransportBindingElement`, `TextMessageEncodingBindingElement CompositeDuplexBindingElement` 및 `ReliableSessionBindingElement`를 포함합니다.  
  
```csharp
public override BindingElementCollection CreateBindingElements()  
{     
    BindingElementCollection bindingElements = new BindingElementCollection();  
    if (ReliableSessionEnabled)  
    {  
        bindingElements.Add(session);  
        bindingElements.Add(compositeDuplex);  
    }  
    bindingElements.Add(encoding);  
    bindingElements.Add(transport);  
    return bindingElements.Clone();  
}  
```  
  
### <a name="adding-a-custom-standard-binding-importer"></a>사용자 지정 표준 바인딩 가져오기 추가  
 Svcutil.exe 및 `WsdlImporter` 형식은 기본적으로 시스템 정의 바인딩을 인식하고 가져옵니다. 그렇지 않을 경우, 해당 바인딩을 `CustomBinding` 인스턴스로 가져옵니다. Svcutil.exe 및 `WsdlImporter`를 사용하도록 설정하여 `SampleProfileUdpBinding`을 가져오기 위해 `UdpBindingElementImporter`가 사용자 지정 표준 바인딩 가져오기도 수행합니다.  
  
 사용자 지정 표준 바인딩 가져오기는 메타데이터로부터 가져온 `ImportEndpoint` 인스턴스를 검사하여 특정 표준 바인딩에 의해 생성되었는지 여부를 확인하기 위해 `IWsdlImportExtension` 인터페이스에 `CustomBinding` 메서드를 구현합니다.  
  
```csharp
if (context.Endpoint.Binding is CustomBinding)  
{  
    Binding binding;  
    if (transportBindingElement is UdpTransportBindingElement)  
    {  
        //if TryCreate is true, the CustomBinding will be replace by a SampleProfileUdpBinding in the  
        //generated config file for better typed generation.  
        if (SampleProfileUdpBinding.TryCreate(bindingElements, out binding))  
        {  
            binding.Name = context.Endpoint.Binding.Name;  
            binding.Namespace = context.Endpoint.Binding.Namespace;  
            context.Endpoint.Binding = binding;  
        }  
    }  
}  
```  
  
 일반적으로 사용자 지정 표준 바인딩 가져오기를 구현하면 가져온 바인딩 요소의 속성을 확인하여 표준 바인딩에 의해 설정될 수 있는 속성만 변경되고, 다른 모든 속성은 기본값인지를 확인하는 작업이 포함됩니다. 표준 바인딩 가져오기를 구현하기 위한 기본 전략은 표준 바인딩의 인스턴스를 만들고, 바인딩 요소의 속성을 표준 바인딩이 지원하는 표준 바인딩 인스턴스로 전파하고, 가져온 바인딩 요소를 표준 바인딩의 바인딩 요소와 비교하는 것입니다.  
  
<a name="AddingConfigurationSupport"></a>   
## <a name="adding-configuration-support"></a>구성 지원 추가  
 구성을 통해 전송을 노출하려면 두 가지 구성 섹션을 구현해야 합니다. 첫 번째는 `BindingElementExtensionElement`의 `UdpTransportBindingElement`입니다. 이는 `CustomBinding` 구현이 해당 바인딩 요소를 참조하기 위해 필요합니다. 두 번째는 `Configuration`의 `SampleProfileUdpBinding`입니다.  
  
### <a name="binding-element-extension-element"></a>바인딩 요소 확장명 요소  
 `UdpTransportElement` 섹션은 구성 시스템에 `BindingElementExtensionElement`을 노출하는 `UdpTransportBindingElement`입니다. 몇 가지 기본 재정의를 통해 구성 섹션 이름, 바인딩 요소의 형식 및 바인딩 요소를 만드는 방법을 정의합니다. 그러면 다음 코드와 같이 구성 파일에 확장명 섹션을 등록할 수 있습니다.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
        <add name="udpTransport" type="Microsoft.ServiceModel.Samples.UdpTransportElement, UdpTransport />  
      </bindingElementExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
 사용자 지정 바인딩에서는 UDP를 전송으로 사용하기 위해 확장을 참조할 수 있습니다.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <customBinding>  
       <binding configurationName="UdpCustomBinding">  
         <udpTransport/>  
       </binding>  
      </customBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="binding-section"></a>바인딩 섹션  
 `SampleProfileUdpBindingCollectionElement` 섹션은 구성 시스템에 `StandardBindingCollectionElement`을 노출하는 `SampleProfileUdpBinding`입니다. 대량의 구현은 `SampleProfileUdpBindingConfigurationElement`로부터 파생되는 `StandardBindingElement`에 위임됩니다. 에는의 `SampleProfileUdpBinding`속성과 `ConfigurationElement` 바인딩에서 매핑할 함수에 해당 하는 속성이 있습니다.`SampleProfileUdpBindingConfigurationElement` 마지막으로 다음 샘플 코드와 같이 `OnApplyConfiguration`에서 `SampleProfileUdpBinding` 메서드를 재정의합니다.  
  
```csharp
protected override void OnApplyConfiguration(string configurationName)  
{  
    if (binding == null)
        throw new ArgumentNullException("binding");

    if (binding.GetType() != typeof(SampleProfileUdpBinding))
    {
        throw new ArgumentException(string.Format(CultureInfo.CurrentCulture,
            "Invalid type for binding. Expected type: {0}. Type passed in: {1}.",
            typeof(SampleProfileUdpBinding).AssemblyQualifiedName,
            binding.GetType().AssemblyQualifiedName));
    }
    SampleProfileUdpBinding udpBinding = (SampleProfileUdpBinding)binding;

    udpBinding.OrderedSession = this.OrderedSession;
    udpBinding.ReliableSessionEnabled = this.ReliableSessionEnabled;
    udpBinding.SessionInactivityTimeout = this.SessionInactivityTimeout;
    if (this.ClientBaseAddress != null)
        udpBinding.ClientBaseAddress = ClientBaseAddress;
}
```  
  
 구성 시스템에 이 처리기를 등록하려면 관련 구성 파일에 다음 섹션을 추가합니다.  
  
```xml
<configuration>  
  <configSections>  
     <sectionGroup name="system.serviceModel">  
        <sectionGroup name="bindings">  
          <section name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport />  
        </sectionGroup>  
     </sectionGroup>  
  </configSections>  
</configuration>  
```  
  
 이렇게 하면 serviceModel 구성 섹션에서 이 처리기를 참조할 수 있습니다.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint configurationName="calculator"  
                address="soap.udp://localhost:8001/"   
                bindingConfiguration="CalculatorServer"  
                binding="sampleProfileUdpBinding"   
                contract= "Microsoft.ServiceModel.Samples.ICalculatorContract">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="the-udp-test-service-and-client"></a>UDP 테스트 서비스 및 클라이언트  
 이 샘플 전송을 사용하기 위한 테스트 코드는 UdpTestService 및 UdpTestClient 디렉터리에 있습니다. 서비스 코드는 두 가지 테스트로 구성됩니다. 하나는 코드에서 바인딩 및 엔드포인트를 설정하고, 다른 하나는 구성을 통해 바인딩 및 엔드포인트를 설정합니다. 두 테스트 모두 두 개의 엔드포인트를 사용합니다. 하나의 끝점은 `SampleUdpProfileBinding` [ \<reliableSession >](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90)) 가로 `true`설정 된를 사용 합니다. 다른 엔드포인트는 `UdpTransportBindingElement`가 포함된 사용자 지정 바인딩을 사용합니다. 이는 `SampleUdpProfileBinding` `false` [ \<reliableSession >](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90)) 을로 설정 하 여를 사용 하는 것과 같습니다. 두 테스트 모두 서비스를 만들고 각 바인딩에 엔드포인트를 추가하며 서비스를 연 다음 서비스를 닫기 전에 사용자가 Enter 키를 누를 때까지 기다립니다.  
  
 서비스 테스트 애플리케이션을 시작하면 다음과 같이 출력되어야 합니다.  
  
```console
Testing Udp From Code.  
Service is started from code...  
Press <ENTER> to terminate the service and start service from config...  
```  
  
 그런 다음 게시된 엔드포인트에 대해 테스트 클라이언트 애플리케이션을 실행할 수 있습니다. 클라이언트 테스트 애플리케이션은 각 엔드포인트에 대해 클라이언트를 만들고 각 엔드포인트에 5개의 메시지를 보냅니다. 클라이언트에 다음과 같이 출력됩니다.  
  
```console
Testing Udp From Imported Files Generated By SvcUtil.  
0  
3  
6  
9  
12  
Press <ENTER> to complete test.  
```  
  
 서비스의 전체 출력은 다음과 같습니다.  
  
```console
Service is started from code...  
Press <ENTER> to terminate the service and start service from config...  
Hello, world!  
Hello, world!  
Hello, world!  
Hello, world!  
Hello, world!  
   adding 0 + 0  
   adding 1 + 2  
   adding 2 + 4  
   adding 3 + 6  
   adding 4 + 8  
```  
  
 구성을 사용하여 게시된 엔드포인트에 대해 클라이언트 애플리케이션을 실행하려면 서비스에서 Enter 키를 누른 다음 테스트 클라이언트를 다시 실행합니다. 서비스에서 다음과 같이 출력되어야 합니다.  
  
```console
Testing Udp From Config.  
Service is started from config...  
Press <ENTER> to terminate the service and exit...  
```  
  
 클라이언트를 다시 실행하면 이전과 동일한 결과가 나타납니다.  
  
 Svcutil.exe를 사용하여 클라이언트 코드 및 구성을 다시 생성하려면 서비스 애플리케이션을 시작한 다음 샘플의 루트 디렉터리에서 다음 Svcutil.exe를 실행합니다.  
  
```console
svcutil http://localhost:8000/udpsample/ /reference:UdpTransport\bin\UdpTransport.dll /svcutilConfig:svcutil.exe.config  
```  
  
 Svcutil.exe는 `SampleProfileUdpBinding`에 대한 바인딩 확장명 구성을 생성하지 않으므로 직접 추가해야 합니다.  
  
```xml
<configuration>  
  <system.serviceModel>      
    <extensions>  
      <!-- This was added manually because svcutil.exe does not add this extension to the file -->  
      <bindingExtensions>  
        <add name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
      </bindingExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
2. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
3. 앞의 "UDP 테스트 서비스 및 클라이언트" 단원을 참조하십시오.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Transport\Udp`
