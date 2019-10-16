---
title: 구성 및 메타데이터 지원
ms.date: 03/30/2017
ms.assetid: 27c240cb-8cab-472c-87f8-c864f4978758
ms.openlocfilehash: 16c386f8479778c7d2f17fbdfdb95dee558baf52
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795844"
---
# <a name="configuration-and-metadata-support"></a>구성 및 메타데이터 지원
이 항목에서는 바인딩 및 바인딩 요소에 대한 구성 및 메타데이터 지원을 사용하도록 설정하는 방법에 대해 설명합니다.  
  
## <a name="overview-of-configuration-and-metadata"></a>구성 및 메타데이터 개요  
 이 항목에서는 [채널 개발](developing-channels.md) 작업 목록에서 선택적 항목인 1, 2 및 4 인 다음 작업에 대해 설명 합니다.  
  
- 바인딩 요소에 대해 구성 파일 지원을 사용하도록 설정합니다.  
  
- 바인딩에 대해 구성 파일 지원을 사용하도록 설정합니다.  
  
- 바인딩 요소에 대해 WSDL 및 정책 어설션을 내보냅니다.  
  
- 바인딩 또는 바인딩 요소를 삽입하고 구성하기 위해 WSDL 및 정책 어설션을 식별합니다.  
  
 사용자 정의 바인딩 및 바인딩 요소를 만드는 방법에 대 한 자세한 내용은 [사용자 정의 바인딩 만들기](creating-user-defined-bindings.md) 및 [BindingElement 만들기](creating-a-bindingelement.md)를 참조 하세요.  
  
## <a name="adding-configuration-support"></a>구성 지원 추가  
 채널에 대해 구성 파일 지원을 사용하도록 설정하려면 두 개의 구성 섹션, 즉, 바인딩 요소에 대해 구성 지원을 사용하도록 설정하는 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=nameWithType>와 바인딩에 대해 구성 지원을 사용하도록 설정하는 <xref:System.ServiceModel.Configuration.StandardBindingElement?displayProperty=nameWithType> 및 <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602?displayProperty=nameWithType>를 구현해야 합니다.  
  
 이 작업을 수행 하는 보다 쉬운 방법은 [ConfigurationCodeGenerator](../samples/configurationcodegenerator.md) 샘플 도구를 사용 하 여 바인딩 및 바인딩 요소에 대 한 구성 코드를 생성 하는 것입니다.  
  
### <a name="extending-bindingelementextensionelement"></a>BindingElementExtensionElement 확장명  
 [전송에서 가져온 예제 코드는 다음과 같습니다. UDP](../samples/transport-udp.md) 샘플. `UdpTransportElement`는 구성 시스템에 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>를 노출하는 `UdpTransportBindingElement`입니다. 샘플에서는 몇 가지 기본 재정의를 통해 구성 섹션 이름, 바인딩 요소의 형식 및 바인딩 요소를 만드는 방법을 정의합니다. 그러면 사용자는 다음과 같이 구성 파일에서 확장명 섹션을 등록할 수 있습니다.  
  
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
  
### <a name="adding-configuration-for-a-binding"></a>바인딩에 대해 구성 추가  
 `SampleProfileUdpBindingCollectionElement` 섹션은 구성 시스템에 <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602>을 노출하는 `SampleProfileUdpBinding`입니다. 대량의 구현은 `SampleProfileUdpBindingConfigurationElement`로부터 파생되는 <xref:System.ServiceModel.Configuration.StandardBindingElement>에 위임됩니다. 에는의 `SampleProfileUdpBinding`속성과 `ConfigurationElement` 바인딩에서 매핑할 함수에 해당 하는 속성이 있습니다.`SampleProfileUdpBindingConfigurationElement` 마지막으로 `OnApplyConfiguration` 메서드는 다음 샘플 코드에서처럼 `SampleProfileUdpBinding`에서 재정의됩니다.  
  
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
  
 구성 시스템을 사용하여 이 처리기를 등록하려면 관련 구성 파일에 다음 섹션을 추가합니다.  
  
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
  
 그런 다음 [ \<system.servicemodel >](../../configure-apps/file-schema/wcf/system-servicemodel.md) 구성 섹션에서 참조할 수 있습니다.  
  
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
  
## <a name="adding-metadata-support-for-a-binding-element"></a>바인딩 요소에 대해 메타데이터 지원 추가  
 채널을 메타데이터 시스템으로 통합하려면 채널이 정책 가져오기와 내보내기를 모두 지원해야 합니다. 이를 통해 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) 와 같은 도구를 사용 하 여 바인딩 요소의 클라이언트를 생성할 수 있습니다.  
  
### <a name="adding-wsdl-support"></a>WSDL 지원 추가  
 바인딩의 전송 바인딩 요소는 메타데이터에서 주소 지정 정보를 내보내고 가져옵니다. 또한 전송 바인딩 요소는 SOAP 바인딩을 사용할 때 메타데이터에서 올바른 전송 URI을 내보낼 수 있어야 합니다. [전송에서 가져온 예제 코드는 다음과 같습니다. UDP](../samples/transport-udp.md) 샘플.  
  
#### <a name="wsdl-export"></a>WSDL 내보내기  
 주소 지정 정보를 내보내기 위해 `UdpTransportBindingElement` 는 <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> 인터페이스를 구현 합니다. <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A?displayProperty=nameWithType> 메서드는 WSDL 포트에 올바른 주소 지정 정보를 추가합니다.  
  
```csharp  
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 엔드포인트가 SOAP 바인딩을 사용할 때 `UdpTransportBindingElement` 메서드의 <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> 구현이 전송 URI도 내보냅니다.  
  
```csharp  
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### <a name="wsdl-import"></a>WSDL 가져오기  
 주소 가져오기를 처리하기 위해 WSDL 가져오기 시스템을 확장하려면 Svcutil.exe.config 파일에서처럼 Svcutil.exe에 대한 구성 파일에 다음 구성을 추가합니다.  
  
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
  
 `UdpBindingElementImporter` 형식은 <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> 인터페이스를 구현합니다. `ImportEndpoint` 메서드는 WSDL 포트로부터 주소를 가져옵니다.  
  
```csharp  
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### <a name="adding-policy-support"></a>정책 지원 추가  
 사용자 지정 바인딩 요소는 서비스 엔드포인트가 해당 바인딩 요소의 기능을 표현하도록 WSDL 바인딩에서 정책 어설션을 내보낼 수 있습니다. [전송에서 가져온 예제 코드는 다음과 같습니다. UDP](../samples/transport-udp.md) 샘플.  
  
#### <a name="policy-export"></a>정책 내보내기  
 형식은 정책 내보내기 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> 에 대 한 지원을 추가 하기 위해을 구현 합니다. `UdpTransportBindingElement` 그 결과, <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType>는 이를 포함하는 모든 바인딩에 대한 정책 생성에 `UdpTransportBindingElement`를 포함합니다.  
  
 <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A?displayProperty=nameWithType>에서는 채널이 멀티캐스트 모드인 경우 UDP용 어설션 및 다른 어설션을 추가합니다. 이는 멀티캐스트 모드가 통신 스택의 구성 방법에 영향을 주므로 양쪽 모두에서 조정되어야 하기 때문입니다.  
  
```csharp  
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.MulticastAssertion,     UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 사용자 지정 전송 바인딩 요소가 주소 지정을 처리하기 때문에 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType>에서의 `UdpTransportBindingElement` 구현 역시 사용 중인 WS-Addressing의 버전을 나타내기 위해 적절한 WS-Addressing 정책 어설션 내보내기를 처리해야 합니다.  
  
```csharp  
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### <a name="policy-import"></a>정책 가져오기  
 정책 가져오기 시스템을 확장하려면 Svcutil.exe.config 파일에서처럼 Svcutil.exe에 대한 구성 파일에 다음 구성을 추가합니다.  
  
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
  
 그런 다음 등록된 클래스(<xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType>)로부터 `UdpBindingElementImporter`을 구현합니다. <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=nameWithType>에서는 적절한 네임스페이스에서 어설션을 검사하고, 어셜션 중 하나를 처리하여 전송을 생성하고 멀티캐스트인지 여부를 확인합니다. 또한 가져오기가 바인딩 어설션 목록으로부터 처리하는 어설션을 제거합니다. 다시 한 번 말하지만 Svcutil.exe를 실행할 때 통합하는 방법은 두 가지가 있습니다.  
  
1. /SvcutilConfig:\<file >를 사용 하 여 svcutil.exe를 구성 파일에 지정 합니다.  
  
2. Svcutil.exe와 동일한 디렉터리에 있는 Svcutil.exe.config에 구성 섹션을 추가합니다.  
  
### <a name="adding-a-custom-standard-binding-importer"></a>사용자 지정 표준 바인딩 가져오기 추가  
 기본적으로 Svcutil.exe 및 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> 형식은 시스템 제공 바인딩을 인식하고 가져옵니다. 그렇지 않을 경우, 해당 바인딩을 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> 인스턴스로 가져옵니다. Svcutil.exe 및 <xref:System.ServiceModel.Description.WsdlImporter>를 사용하도록 설정하여 `SampleProfileUdpBinding`을 가져오기 위해 `UdpBindingElementImporter`가 사용자 지정 표준 바인딩 가져오기도 수행합니다.  
  
 사용자 지정 표준 바인딩 가져오기는 `ImportEndpoint` <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> 인터페이스에서 메서드를 구현 하 여 메타 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> 데이터에서 가져온 인스턴스를 검사 하 여 특정 표준 바인딩에서 생성 되었는지 여부를 확인 합니다.  
  
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
