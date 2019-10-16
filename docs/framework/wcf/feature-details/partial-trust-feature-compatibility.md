---
title: 부분 신뢰 기능 호환성
ms.date: 03/30/2017
ms.assetid: a36a540b-1606-4e63-88e0-b7c59e0e6ab7
ms.openlocfilehash: adeef7a8fa12751c53e2096ae6bf844f091a5545
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965312"
---
# <a name="partial-trust-feature-compatibility"></a>부분 신뢰 기능 호환성
WCF (Windows Communication Foundation)는 부분적으로 신뢰할 수 있는 환경에서 실행 될 때 제한 된 기능의 하위 집합을 지원 합니다. 부분 신뢰에서 지원되는 기능은 [Supported Deployment Scenarios](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md) 항목에서 설명한 대로 특정 시나리오 집합을 바탕으로 설계되었습니다.  
  
## <a name="minimum-permission-requirements"></a>최소 권한 요구 사항  
 WCF는 다음 표준 명명 된 권한 집합 중 하나에서 실행 되는 응용 프로그램의 기능 하위 집합을 지원 합니다.  
  
- 보통 신뢰 권한  
  
- 인터넷 영역 권한  
  
 더 제한적인 권한이 있는 부분 신뢰 응용 프로그램에서 WCF를 사용 하려고 하면 런타임에 보안 예외가 발생할 수 있습니다.  
  
## <a name="contracts"></a>계약  
 부분 신뢰에서 계약을 실행할 때 다음과 같은 제한 사항이 적용됩니다.  
  
- `[ServiceContract]` 인터페이스를 구현하는 서비스 클래스가 `public` 이어야 하며 `public` 생성자를 포함해야 합니다. 서비스 클래스가 `[OperationContract]` 메서드를 정의하는 경우 이 메서드는 `public`이어야 합니다. 서비스 클래스가 `[ServiceContract]` 인터페이스를 구현하는 경우에는 `private`인터페이스가 `[ServiceContract]` 일 때 이러한 메서드 구현이 명시적 또는 `public`일 수 있습니다.  
  
- `[ServiceKnownType]` 특성을 사용할 때는 지정된 메서드가 `public`이어야 합니다.  
  
- `[MessageContract]` 클래스와 해당 멤버는 `public`이어야 합니다. `[MessageContract]` 클래스는 응용 프로그램 어셈블리에 정의되어 있는 경우 `internal` 일 수 있으며 `internal` 멤버를 포함할 수 있습니다.  
  
## <a name="system-provided-bindings"></a>시스템 제공 바인딩  
 <xref:System.ServiceModel.BasicHttpBinding> 및 <xref:System.ServiceModel.WebHttpBinding> 은 부분 신뢰 환경에서 완전히 지원됩니다. <xref:System.ServiceModel.WSHttpBinding> 은 전송 보안 모드에만 지원됩니다.  
  
 <xref:System.ServiceModel.NetTcpBinding>, <xref:System.ServiceModel.NetNamedPipeBinding>또는 <xref:System.ServiceModel.NetMsmqBinding>과 같이 HTTP 이외의 전송을 사용하는 바인딩은 부분 신뢰 환경에서 실행하는 경우 지원되지 않습니다.  
  
## <a name="custom-bindings"></a>사용자 지정 바인딩  
 사용자 지정 바인딩을 부분 신뢰 환경에서 만들어 사용할 수 있지만 이 단원에 지정되어 있는 제한 사항을 준수해야 합니다.  
  
### <a name="transports"></a>전송  
 유일하게 허용된 전송 바인딩 요소는 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 및 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>입니다.  
  
### <a name="encoders"></a>인코더  
 다음 인코더를 사용할 수 있습니다.  
  
- 텍스트 인코더(<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>)  
  
- 이진 인코더(<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>)  
  
- 웹 메시지 인코더(<xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>)  
  
 MTOM(Message Transmission Optimization Mechanism) 인코더는 지원되지 않습니다.  
  
### <a name="security"></a>보안  
 부분적으로 신뢰할 수 있는 응용 프로그램은 통신을 보호 하기 위해 WCF의 전송 수준 보안 기능을 사용할 수 있습니다. 메시지 수준 보안은 지원되지 않습니다. 메시지 수준 보안을 사용하도록 바인딩을 구성할 경우 런타임에 예외가 발생합니다.  
  
### <a name="unsupported-bindings"></a>지원되지 않는 바인딩  
 신뢰할 수 있는 메시징, 트랜잭션 또는 메시지 수준 보안을 사용하는 바인딩은 지원되지 않습니다.  
  
## <a name="serialization"></a>Serialization  
 <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Xml.Serialization.XmlSerializer> 는 모두 부분 신뢰 환경에서 지원됩니다. 그러나 <xref:System.Runtime.Serialization.DataContractSerializer> 의 사용은 다음 조건에 따라 결정됩니다.  
  
- serialize할 수 있는 모든 `[DataContract]` 형식은 `public`이어야 합니다.  
  
- `[DataMember]` 형식의 serialize할 수 있는 모든 `[DataContract]` 필드 또는 속성은 public이고 읽기/쓰기가 가능해야 합니다. 부분적으로 신뢰할 수 있는 응용 프로그램에서 WCF를 실행 하는 경우 [읽기 전용](https://go.microsoft.com/fwlink/?LinkID=98854) 필드의 serialization 및 deserialization은 지원 되지 않습니다.  
  
- `[Serializable]`/ISerializable 프로그래밍 모델은 부분 신뢰 환경에서 지원되지 않습니다.  
  
- 코드 또는 시스템 수준 구성(machine.config)에서는 알려진 형식을 지정해야 합니다. 보안상의 이유로 애플리케이션 수준 구성에서는 알려진 형식을 지정할 수 없습니다.  
  
- <xref:System.Runtime.Serialization.IObjectReference> 를 구현하는 형식은 부분 신뢰 환경에서 예외를 throw합니다.  
  
 부분적으로 신뢰할 수 있는 애플리케이션에서 [T:System.Runtime.Serialization.DataContractSerializer](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md) 를 안전하게 사용하는 경우의 보안에 대한 자세한 내용은 <xref:System.Runtime.Serialization.DataContractSerializer> 의 Serialization 단원을 참조하세요.  
  
### <a name="collection-types"></a>컬렉션 형식  
 일부 컬렉션 형식은 <xref:System.Collections.Generic.IEnumerable%601> 및 <xref:System.Collections.IEnumerable>을 모두 구현합니다. 예제에는 <xref:System.Collections.Generic.ICollection%601>을 구현하는 형식이 포함되어 있습니다. 이러한 형식은 `public` 의 `GetEnumerator()`구현 및 `GetEnumerator()`의 명시적 구현을 구현할 수 있습니다. 이 경우 <xref:System.Runtime.Serialization.DataContractSerializer> 는 `public` 의 명시적 구현이 아니라 `GetEnumerator()`의 `GetEnumerator()`구현을 호출합니다. `GetEnumerator()` 구현이 모두 `public` 이 아니고 모든 구현이 명시적 구현인 경우 <xref:System.Runtime.Serialization.DataContractSerializer> 는 `IEnumerable.GetEnumerator()`를 호출합니다.  
  
 WCF가 부분 신뢰 환경에서 실행 되는 경우 컬렉션 형식의 경우, `GetEnumerator()` `public`구현 중 어떤 것도 없거나 명시적 인터페이스 구현인 항목이 없으면 보안 예외가 throw 됩니다.  
  
### <a name="netdatacontractserializer"></a>NetDataContractSerializer  
 <xref:System.Collections.Generic.List%601>, <xref:System.Collections.ArrayList>, <xref:System.Collections.Generic.Dictionary%602> 및 <xref:System.Collections.Hashtable> 와 같은 많은 .NET Framework 컬렉션 형식은 부분 신뢰의 <xref:System.Runtime.Serialization.NetDataContractSerializer> 에서 지원되지 않습니다. 이러한 형식에는 `[Serializable]` 특성이 설정되어 있으며 앞의 Serialization 단원에서 설명한 것처럼 이 특성은 부분 신뢰에서 지원되지 않습니다. <xref:System.Runtime.Serialization.DataContractSerializer> 는 컬렉션을 특별한 방법으로 다루기 때문에 이 제한을 해결할 수 있지만 <xref:System.Runtime.Serialization.NetDataContractSerializer> 에 이 제한 사항을 피할 수 있는 이러한 메커니즘이 없습니다.  
  
 <xref:System.DateTimeOffset> 형식은 부분 신뢰의 <xref:System.Runtime.Serialization.NetDataContractSerializer> 에서 지원되지 않습니다.  
  
 서로게이트는 부분 신뢰에서 실행할 때 <xref:System.Runtime.Serialization.NetDataContractSerializer> 메커니즘을 사용하여 <xref:System.Runtime.Serialization.SurrogateSelector> 와 함께 사용할 수 없습니다. 이러한 제한 사항은 서로게이트를 사용하는 경우에만 적용되며 서로게이트를 serialize하는 경우에는 적용되지 않습니다.  
  
## <a name="enabling-common-behaviors-to-run"></a>일반 동작이 실행되도록 설정  
 구성 파일의 [ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 섹션에 추가 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 된 특성 (APTCA)으로 표시 되지 않은 서비스 또는 끝점 동작은 응용 프로그램이 부분 신뢰 환경에서 실행 되 고 없는 경우 실행 되지 않습니다. 이 오류가 발생 하면 예외가 throw 됩니다. 일반 동작을 실행하려면 다음 옵션 중 하나를 수행해야 합니다.  
  
- 부분 신뢰 애플리케이션으로 배포될 때 실행될 수 있도록 일반 동작을 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 특성으로 표시합니다. APTCA로 표시된 어셈블리가 실행되지 않도록 컴퓨터에 레지스트리 항목을 설정할 수 있습니다. 이어야 합니다.  
  
- 부분 신뢰 환경에서 애플리케이션을 실행하기 위해 사용자가 코드 액세스 보안 설정을 수정할 수 없는 완전 신뢰 애플리케이션으로서 애플리케이션이 배포되는지 확인합니다. 사용자가 보안 설정을 수정할 수 있는 경우 동작이 실행되지 않고 예외가 throw되지 않습니다. 이를 확인 하려면 Caspol.exe를 사용 하 여 **levelfinal** 옵션 [(코드 액세스 보안 정책 도구)](../../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md)을 참조 하세요.  
  
 일반적인 동작에 대 한 예제를 보려면 [방법: 엔터프라이즈](../../../../docs/framework/wcf/extending/how-to-lock-down-endpoints-in-the-enterprise.md)에서 끝점을 잠급니다.  
  
## <a name="configuration"></a>Configuration  
 한 가지 예외를 제외 하 고 부분적으로 신뢰할 수 있는 코드는 로컬 `app.config` 파일의 WCF 구성 섹션만 로드할 수 있습니다. Machine.config 또는 루트 web.config 파일에서 WCF 섹션을 참조 하는 WCF 구성 섹션을 로드 하려면 ConfigurationPermission (제한 없음)이 필요 합니다. 이 권한이 없으면 로컬 구성 파일 외부에 있는 WCF 구성 섹션 (동작, 바인딩)을 참조할 때 구성이 로드 될 때 예외가 발생 합니다.  
  
 한 가지 예외는 이 항목의 Serialization 단원에서 설명한 것처럼 serialization에 대한 알려진 형식 구성입니다.  
  
> [!IMPORTANT]
> 구성 확장은 완전 신뢰에서 실행되는 경우에만 지원됩니다.  
  
## <a name="diagnostics"></a>진단  
  
### <a name="event-logging"></a>이벤트 로깅  
 제한된 이벤트 로깅은 부분 신뢰에서 지원됩니다. 서비스 활성화 오류 및 추적/메시지 로깅 실패만 이벤트 로그에 로깅됩니다. 이벤트에 너무 많은 메시지를 기록하지 않도록 프로세스에서 로깅할 수 있는 최대 이벤트 수가 5로 설정되어 있습니다.  
  
### <a name="message-logging"></a>메시지 로깅  
 WCF가 부분 신뢰 환경에서 실행 되는 경우 메시지 로깅이 작동 하지 않습니다. 부분 신뢰에서 사용하도록 설정된 경우 서비스 활성화는 실패하지 않지만 메시지가 기록되지 않습니다.  
  
### <a name="tracing"></a>추적  
 제한된 추적 기능은 부분 신뢰 환경에서 실행하는 경우 사용할 수 있습니다. 구성 파일의 <`listeners`> 요소에서 추가할 수 있는 형식은 <xref:System.Diagnostics.TextWriterTraceListener> 및 새로운 <xref:System.Diagnostics.EventSchemaTraceListener>뿐입니다. 표준 <xref:System.Diagnostics.XmlWriterTraceListener>를 사용하면 로그가 불완전하거나 잘못될 수 있습니다.  
  
 지원되는 추적 소스는 다음과 같습니다.  
  
- <xref:System.ServiceModel>  
  
- <xref:System.Runtime.Serialization>  
  
- <xref:System.IdentityModel.Claims>, <xref:System.IdentityModel.Policy>, <xref:System.IdentityModel.Selectors>및 <xref:System.IdentityModel.Tokens>가 있습니다.  
  
 다음 추적 소스는 지원되지 않습니다.  
  
- CardSpace  
  
- <xref:System.IO.Log>  

- [System.ServiceModel.Internal.TransactionBridge](https://docs.microsoft.com/previous-versions/aa346556(v=vs.110))]
  
 <xref:System.Diagnostics.TraceOptions> 열거형에 대한 다음 멤버는 지정하지 않아야 합니다.  
  
- <xref:System.Diagnostics.TraceOptions.Callstack?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceOptions.ProcessId?displayProperty=nameWithType>  
  
 부분 신뢰 환경에서 추적을 사용하는 경우 애플리케이션에 추적 수신기의 출력을 저장할 권한이 있는지 확인합니다. 예를 들어 <xref:System.Diagnostics.TextWriterTraceListener> 를 사용하여 추적 출력을 텍스트 파일에 기록하는 경우 애플리케이션에 추적 파일을 기록하는 데 필요한 FileIOPermission이 있는지 확인합니다.  
  
> [!NOTE]
> 중복 오류가 발생 한 추적 파일의 초과를 방지 하기 위해 WCF는 첫 번째 보안 실패 후 리소스 또는 작업 추적을 사용 하지 않도록 설정 합니다. 처음으로 리소스에 액세스하거나 작업을 수행할 때 실패한 각 리소스 액세스에 대해 한 가지 예외 추적이 있습니다.  
  
## <a name="wcf-service-host"></a>WCF 서비스 호스트  
 WCF 서비스 호스트는 부분 신뢰를 지원 하지 않습니다. 부분 신뢰에서 WCF 서비스를 사용 하려면 서비스를 빌드하기 위해 Visual Studio에서 WCF 서비스 라이브러리 프로젝트 템플릿을 사용 하지 마십시오. 대신 wcf 부분 신뢰가 지원 되는 웹 서버에서 서비스를 호스팅할 수 있는 WCF 서비스 웹 사이트 템플릿을 선택 하 여 Visual Studio에서 새 웹 사이트를 만듭니다.  
  
## <a name="other-limitations"></a>기타 제한 사항  
 WCF는 일반적으로 호스팅 응용 프로그램에서 적용 되는 보안 고려 사항으로 제한 됩니다. 예를 들어 WCF가 XBAP (XAML 브라우저 응용 프로그램)에서 호스트 되는 경우 [Windows Presentation Foundation 부분 신뢰 보안](https://go.microsoft.com/fwlink/?LinkId=89138)에 설명 된 대로 xbap 제한의 영향을 받습니다.  
  
 다음 추가 기능은 indigo2를 부분 신뢰 환경에서 실행하는 경우 사용할 수 없습니다.  
  
- WMI(Windows Management Instrumentation)  
  
- 이벤트 로깅은 부분적으로만 사용할 수 있습니다( **진단** 단원에서의 설명 참조).  
  
- 성능 카운터  
  
 부분 신뢰 환경에서 지원 되지 않는 WCF 기능을 사용할 경우 런타임에 예외가 발생할 수 있습니다.  
  
## <a name="unlisted-features"></a>목록에 없는 기능  
 부분 신뢰 환경에서 실행할 때 사용할 수 없는 정보 또는 작업 부분을 검색하는 가장 좋은 방법은 리소스에 액세스하거나 `try` 블록 내의 작업을 수행한 다음 오류를 `catch` 하는 것입니다. 중복 오류가 발생 한 추적 파일의 초과를 방지 하기 위해 WCF는 첫 번째 보안 실패 후 리소스 또는 작업 추적을 사용 하지 않도록 설정 합니다. 처음으로 리소스에 액세스하거나 작업을 수행할 때 실패한 각 리소스 액세스에 대해 한 가지 예외 추적이 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>
- [지원되는 배포 시나리오](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md)
- [부분 신뢰를 위한 최선의 방법](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md)
