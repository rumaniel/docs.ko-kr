---
title: Windows Communication Foundation 4.5의 새로운 기능
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], what's new
- Windows Communication Foundation [WCF], what's new
ms.assetid: 7e93fe73-af93-46b5-9f63-32f761ee40cf
ms.openlocfilehash: a50db521e986972e864ac60c8b84a63d3d1de69b
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834872"
---
# <a name="whats-new-in-windows-communication-foundation-45"></a>Windows Communication Foundation 4.5의 새로운 기능

이 항목에서는 Windows Communication Foundation (WCF) 버전 4.5에 대 한 새로운 기능을 설명 합니다.

## <a name="wcf-simplification-features"></a>WCF 단순화 기능

WCF 4.5 애플리케이션을 더 쉽게 개발하고 유지할 수 있도록 많은 작업이 이루어졌습니다. 자세한 내용은 [WCF 간소화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)을 참조 하세요.

### <a name="task-based-async-support"></a>태스크 기반 비동기 지원

기본적으로 서비스 참조를 추가하면 작업 반환 비동기 서비스 작업 메서드가 생성됩니다. 이는 동기 및 비동기 메서드에 대해 수행됩니다. 따라서 새로운 작업 기반 비동기 프로그래밍 모델을 사용하여 비동기적으로 서비스 작업을 호출할 수 있습니다. 생성된 프록시 메서드를 호출하면 WCF는 비동기 작업을 나타내는 작업 개체를 생성하고 해당 작업를 사용자에게 반환합니다. 작업이 완료 되 면 작업이 완료 됩니다. 비동기 작업을 구현 하는 경우이를 작업 기반 비동기 작업으로 구현할 수 있습니다. 자세한 내용은 [동기 및 비동기 작업](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)을 참조 하세요.

### <a name="simplified-generated-configuration-files"></a>단순화되어 생성된 구성 파일

Visual Studio에 서비스 참조를 추가하거나 SvcUtil.exe 도구를 사용하면 클라이언트 구성 파일이 생성됩니다. 이전 버전의 WCF에서는 바인딩 속성 값이 기본값인 경우를 포함하여 모든 바인딩 속성 값이 이러한 구성 파일에 포함되었습니다. WCF 4.5에서는 생성된 구성 파일에 기본값이 아닌 값으로 설정된 바인딩 속성만 포함됩니다.

자세한 내용은 [WCF 간소화 기능](wcf-simplification-features.md)을 참조 하세요.

### <a name="contract-first-development"></a>계약 중심 개발

WCF는 이제 계약 중심 개발을 지원합니다. Svcutil.exe에는 WSDL 문서에서 서비스 및 데이터 계약을 생성할 수 있는/serviceContract 스위치가 있습니다.

### <a name="add-service-reference-from-a-portable-subset-project"></a>이식 가능한 하위 집합 프로젝트의 서비스 참조 추가

이식 가능한 하위 집합 프로젝트를 사용하면 복수 .NET 플랫폼(데스크톱, Silverlight, Windows Phone, XBOX)을 지원하면서 .NET 어셈블리 프로그래머가 하나의 소스 트리를 유지하고 시스템을 빌드할 수 있습니다. 이식 가능한 하위 집합 프로젝트는 .net 플랫폼에서 사용할 수 있는 .net framework 어셈블리인 .NET 이식 가능한 라이브러리만 참조 합니다. 개발자 환경은 다른 WCF 클라이언트 애플리케이션에 서비스 참조를 추가하는 것과 동일합니다. 자세한 내용은 [이식 가능한 하위 집합 프로젝트의 서비스 참조 추가](../../../docs/framework/wcf/add-service-reference-in-a-portable-subset-project.md)을 참조 하세요.

### <a name="aspnet-compatibility-mode-default-changed"></a>ASP.NET 호환 모드 기본값 변경

WCF는 개발자가 WCF 서비스를 작성할 때 ASP.NET HTTP 파이프라인 기능에 완전하게 액세스할 수 있게 해 주는 ASP.NET 호환 모드를 제공합니다. 이 모드를 사용 하려면 web.config의 [@no__t 2serviceHostingEnvironment >](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) 섹션에서 `aspNetCompatibilityEnabled` 특성을 true로 설정 해야 합니다. 또한 이 appDomain의 모든 서비스는 `RequirementsMode`의 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 속성이 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> 또는 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Required>로 설정되어야 합니다. 기본적으로 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>이 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>로 설정 됩니다. 자세한 내용은 Windows Communication Foundation 및 [WCF 서비스와 ASP.NET](../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md) [의 새로운 기능](../../../docs/framework/wcf/whats-new.md) 을 참조 하세요.

### <a name="new-transport-default-values"></a>새 전송 기본값

구성을 단순화하기 위해 여러 전송 속성의 기본값이 변경되었습니다. 자세한 내용은 [WCF 간소화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)을 참조 하세요.

### <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas

<xref:System.Xml.XmlDictionaryReaderQuotas>에는 메시지를 만드는 동안 인코더가 사용하는 메모리의 크기를 제한하는 XML 사전 판독기에 대한 구성 가능 할당량 값이 포함됩니다. 이러한 할당량은 구성 가능하지만, 개발자가 이를 명시적으로 설정해야 할 가능성을 줄이기 위해 기본값이 변경되었습니다. 자세한 내용은 [WCF 간소화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)을 참조 하세요.

### <a name="wcf-configuration-validation"></a>WCF 구성 유효성 검사

이제 Visual Studio 내에서 빌드 프로세스의 일부로 WCF 구성 파일에 대해 프로젝트 내에 정의된 특성의 유효성이 검사됩니다. 유효성 검사가 실패할 경우 유효성 검사 오류 또는 경고의 목록이 Visual Studio에 표시됩니다.

### <a name="xml-editor-tooltips"></a>XML 편집기 도구 설명

WCF 서비스의 기존 및 새 개발자들이 서비스를 구성하는 데 도움이 되도록 이제 Visual Studio XML 편집기에서 서비스 구성 파일에 포함된 모든 구성 요소 및 해당 속성에 대한 도구 설명을 제공합니다.

## <a name="streaming-improvements"></a>스트리밍 향상

수신 측이 읽고 있지 않거나 느리게 읽고 있을 때 전송 측이 스레드를 차단하지 않는 진정한 의미의 비동기 스트리밍을 추가 지원하여 확장성을 향상시켰습니다. 클라이언트가 스트리밍된 메시지를 IIS에서 호스팅된 WCF 서비스에 전송할 때 메시지 버퍼링 제한을 제거하였습니다. 자세한 내용은 [WCF 간소화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)을 참조 하세요.

## <a name="simplifying-exposing-an-endpoint-over-https-with-iis"></a>IIS를 사용하여 HTTPS에 엔드포인트 노출 단순화

HTTPS에서 엔드포인트 노출을 단순화하기 위해 HTTPS 프로토콜 매핑이 추가되었습니다. HTTPS 엔드포인트를 활성화하려면 웹 사이트에 HTTPS 바인딩 및 SSL 인증서가 구성되어 있는지 확인하고 서비스를 호스팅하는 가상 디렉터리에 HTTPS를 사용하도록 설정하기만 하면 됩니다. 서비스에 메타데이터가 활성화되어 있으면 메타데이터도 HTTPS에 노출됩니다.

## <a name="generating-a-single-wsdl-document"></a>단일 WSDL 문서 생성

일부 타사 WSDL 처리 스택은 xsd:import를 통해 다른 문서에 종속된 WSDL 문서를 처리할 수 없습니다. WCF에서는 이제 모든 WSDL 정보가 단일 문서로 반환되도록 지정할 수 있습니다. 단일 WSDL 문서를 요청 하려면 서비스에서 메타 데이터를 요청할 때 URI에 "? singleWSDL"을 추가 합니다.

## <a name="websocket-support"></a>WebSocket 지원

WebSocket은 TCP와 유사한 성능 특성으로 포트 80 및 443에서 진정한 의미의 양방향 통신을 제공하는 기술입니다. WebSocket 전송에서 통신을 지원하기 위해 새로운 바인딩 두 개가 추가되었습니다. <xref:System.ServiceModel.NetHttpBinding>와 <xref:System.ServiceModel.NetHttpsBinding>을 참조하세요. 자세한 내용은 다음을 참조하십시오. [시스템 제공 바인딩](../../../docs/framework/wcf/system-provided-bindings.md)

## <a name="new-transport-default-values"></a>새 전송 기본값

다음 표에는 변경된 설정과 추가 정보를 찾을 수 있는 위치가 나와 있습니다.

|속성|켜짐|새 기본값|추가 정보|
|--------------|--------|-----------------|------------------------------|
|channelInitializationTimeout|<xref:System.ServiceModel.NetTcpBinding>|30초|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.ChannelInitializationTimeout%2A>|
|listenBacklog|<xref:System.ServiceModel.NetTcpBinding>|12 * 프로세서 수|<xref:System.ServiceModel.NetTcpBinding.ListenBacklog%2A>|
|maxPendingAccepts|ConnectionOrientedTransportBindingElement<br /><br /> SMSvcHost.exe|2 * 전송용 프로세서 수<br /><br /> 4 @no__t-Smsvchost.exe에 대 한 프로세서 수 0|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingAccepts%2A> [Net.tcp 포트 공유 서비스를 구성 하는](../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md) 중|
|maxPendingConnections|ConnectionOrientedTransportBindingElement|12 * 프로세서 수|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A>|
|receiveTimeout|SMSvcHost.exe|30초|[Net.TCP Port Sharing Service 구성](../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)|

## <a name="xml-editor-tooltips"></a>XML 편집기 도구 설명

WCF 서비스의 기존 및 새 개발자들이 서비스를 구성하는 데 도움이 되도록 이제 Visual Studio XML 편집기에서 서비스 구성 파일에 포함된 모든 구성 요소 및 해당 속성에 대한 도구 설명을 제공합니다.

## <a name="configuring-wcf-services-in-code"></a>코드로 WCF 서비스 구성

WCF (Windows Communication Foundation)를 사용 하면 개발자가 구성 파일 또는 코드를 사용 하 여 서비스를 구성할 수 있습니다. 구성 파일은 배포 후 서비스를 구성해야 하는 경우에 유용합니다. 구성 파일을 사용할 경우 IT 전문가가 구성 파일을 업데이트하기만 하면 되고 다시 컴파일할 필요가 없습니다. 하지만 구성 파일은 관리하기가 복잡하고 어려울 수 있습니다. 구성 파일 디버깅은 지원되지 않으며 구성 요소는 이름으로 참조되므로 구성 파일을 작성하기가 어렵고 오류가 발생하기 쉽습니다. WCF를 사용 하면 코드에서 서비스를 구성할 수도 있습니다. 이전 버전의 WCF (4.0 및 이전 버전)에서 코드의 서비스 구성은 자체 호스팅 시나리오에서 쉽기 때문에 클래스 <xref:System.ServiceModel.ServiceHost> 를 통해 ServiceHost를 호출 하기 전에 끝점과 동작을 구성할 수 있었습니다. 그러나 웹 호스팅 시나리오에서는 <xref:System.ServiceModel.ServiceHost> 클래스에 액세스할 수 없습니다. 웹 호스팅 서비스를 구성하려면 `System.ServiceModel.ServiceHostFactory`를 만들고 필요한 구성을 수행하는 <xref:System.ServiceModel.Activation.ServiceHostFactory>를 만들어야 했습니다. .NET 4.5부터 WCF는 자체 호스팅 서비스와 웹 호스팅 서비스를 코드에서 더 쉽게 구성 하는 방법을 제공 합니다. 자세한 내용은 [코드에서 WCF 서비스 구성](../../../docs/framework/wcf/configuring-wcf-services-in-code.md)을 참조 하세요.

## <a name="channelfactory-caching"></a>ChannelFactory 캐싱

WCF 클라이언트 애플리케이션에서는 <xref:System.ServiceModel.ChannelFactory%601> 클래스를 사용하여 WCF 서비스와의 통신 채널을 만듭니다. <xref:System.ServiceModel.ChannelFactory%601> 인스턴스를 만들 때는 다음 작업이 필요하기 때문에 약간의 오버헤드가 발생합니다.

1. 생성 된 <xref:System.ServiceModel.Description.ContractDescription> 트리

2. 필요한 모든 CLR 형식 반영

3. 채널 스택 생성

4. 리소스 삭제

이 오버헤드를 최소화하기 위해 사용자가 WCF 클라이언트 프록시를 사용할 때 WCF가 채널 팩터리를 캐시할 수 있습니다. 자세한 내용은 [채널 팩터리 및 캐싱](../../../docs/framework/wcf/feature-details/channel-factory-and-caching.md)을 참조 하세요.

## <a name="compression-and-the-binary-encoder"></a>압축 및 이진 인코더

WCF 4.5부터는 WCF 이진 인코더에서 압축을 추가 지원합니다. 압축 형식은 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A> 속성에서 구성합니다. 클라이언트와 서비스 모두 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A> 속성을 구성해야 합니다. HTTP, HTTPS 및 TCP 프로토콜에 대해 압축이 가능합니다. 클라이언트가 압축을 사용하도록 지정하더라도 서비스에서 이를 지원하지 않으면 프로토콜이 일치하지 않는다는 프로토콜 예외가 throw됩니다. 자세한 내용은 [메시지 인코더 선택](./feature-details/choosing-a-message-encoder.md)을 참조 하세요.

## <a name="udp"></a>UDP

개발자가 "실행 후 제거" 메시징을 사용 하는 서비스를 작성할 수 있도록 하는 UDP 전송에 대 한 지원이 추가 되었습니다. 클라이언트는 서비스에 메시지를 보내고 서비스에서 응답을 기대하지 않습니다.

## <a name="multiple-authentication-support"></a>다중 인증 지원

HTTP 전송 및 전송 보안을 사용할 경우 단일 WCF 엔드포인트에서 IIS의 지원 방식과 같은 복수 인증 모드 지원이 추가되었습니다. IIS에서는 가상 디렉터리에서 복수 인증 모드를 사용할 수 있습니다. 이 기능을 사용하면 단일 WCF 엔드포인트에서 WCF 서비스가 호스팅되는 가상 디렉터리에 대해 복수 인증 모드를 지원할 수 있습니다.

## <a name="idn-support"></a>IDN 지원

IDN(Internationalized Domain Name)을 사용하는 WCF 서비스에 대한 지원이 추가되었습니다. 자세한 내용은 [WCF 및 국제화 도메인 이름](../../../docs/framework/wcf/feature-details/wcf-and-internationalized-domain-names.md)을 참조 하세요.

## <a name="httpclient"></a>HttpClient

<xref:System.Net.Http.HttpClient>라는 새 클래스가 추가되어 HTTP 요청 작업을 더 쉽게 수행할 수 있습니다. 자세한 내용은 [응용 프로그램을 http 서비스를 사용 하 여 소셜 및 연결 만들기](https://go.microsoft.com/fwlink/?LinkId=231886) 및 [http 클라이언트 샘플](https://code.msdn.microsoft.com/windowsapps/HttpClient-sample-55700664)을 참조 하세요.

## <a name="configuration-intellisense"></a>구성 Intellisense

프로젝트에 정의된 사용자 지정 특성의 경우 이제 구성 파일의 특성 값에서 intellisense를 지원하므로 구성 작업을 쉽고 빠르고 정확하게 수행할 수 있습니다.

## <a name="configuration-tooltips"></a>구성 도구 설명

이제 WCF 요소와 특성에는 요소나 특성의 목적을 보다 쉽고 정확 하 게 식별할 수 있도록 XML 편집기의 도구 설명이 포함 되어 있습니다.

## <a name="paste-data-as-classes"></a>데이터를 클래스로 붙여넣기

WCF 프로젝트에서는 XML에 정의된 데이터 형식(서비스에 노출된 형식 등)을 코드 페이지에 직접 붙여넣을 수 있습니다. XML 형식은 CLR 형식으로 붙여 넣게 됩니다. 자세한 내용은 [XML에서 데이터 형식 클래스 생성](../../../docs/framework/wcf/generating-data-type-classes-from-xml.md) 을 참조 하세요.

## <a name="webservicehost-and-default-endpoints"></a>WebServiceHost 및 기본 엔드포인트

Visual Studio 2010에서는 사용자가 엔드포인트를 명시적으로 지정했는지 여부에 상관 없이 WebServiceHost가 기본 엔드포인트를 자동으로 만들었습니다. Visual Studio 2012 이상에서 명시적으로 끝점을 추가 하지 않은 경우에만 WebServiceHost가 기본 끝점을 만듭니다. 클라이언트에 기본 끝점이 필요한 경우 명시적으로 끝점을 추가 하 고 클라이언트를 가리키도록 할 수 있습니다. 또는 애플리케이션의 구성 파일에 다음 설정을 추가하여 WCF가 이전 동작으로 되돌아가도록 지정할 수도 있습니다.

```xml
<appSettings>
    <add key="wcf:webservicehost:enableautomaticendpointscompatability" value="true"/>
  </appSettings>
```

## <a name="ihttpcookiecontainermanager"></a>IHttpCookieContainerManager

이 인터페이스는 <xref:System.ServiceModel.Channels.IChannelFactory%601>에 의해 노출되며 클라이언트 측의 쿠키 작업을 훨씬 손쉽게 해 줍니다. 바인딩의 AllowCookies가 true로 설정되어 있으면 다음 코드를 사용하여 쿠키에 액세스할 수 있습니다.

```csharp
IHttpCookieContainerManager cookieManager = factory.GetProperty<IHttpCookieContainerManager>();
System.Net.CookieContainer container = cookieManager.CookieContainer;
```

그런 다음 <xref:System.Net.CookieContainer>에서 쿠키를 검색하거나 설정할 수 있습니다. AllowCookies가 false로 설정되어 있으면 <xref:System.ServiceModel.OperationContext>를 사용하여 쿠키를 수동으로 검색하고, 또 다른 <xref:System.ServiceModel.OperationContext>나 메시지 검사자를 사용하여 다른 요청에서 이 쿠키를 보낼 수 있습니다. IHttpCookieContainerManager 인터페이스를 사용하면 서비스에 사용자를 인증한 후 해당 서비스에서 반환된 인증 쿠키를 사용하여 다른 서비스에 대해 인증을 수행할 수 있습니다.
