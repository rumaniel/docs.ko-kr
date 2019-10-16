---
title: 엔드포인트 주소
ms.date: 03/30/2017
helpviewer_keywords:
- addresses [WCF]
- Windows Communication Foundation [WCF], addresses
- WCF [WCF], addresses
ms.assetid: 13f269e3-ebb1-433c-86cf-54fbd866a627
ms.openlocfilehash: a59e47e529a5002c806e37dba7267b2cf8318a35
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64912706"
---
# <a name="endpoint-addresses"></a>엔드포인트 주소
모든 엔드포인트에는 해당 엔드포인트를 찾아서 식별하는 데 사용되는 연결된 주소가 있습니다. 이 주소는 주로 엔드포인트의 위치를 지정하는 URI(Uniform Resource Identifier)로 구성됩니다. 끝점 주소에서 Windows Communication Foundation (WCF) 프로그래밍 모델에 표시 됩니다는 <xref:System.ServiceModel.EndpointAddress> 선택적인 포함 하는 클래스 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 다른 끝점에서 끝점을 인증할 수 있게 하는 속성을 exchange를 사용 하 여 메시지 및 선택적 집합이 <xref:System.ServiceModel.EndpointAddress.Headers%2A> 서비스에 도달 하는 데 필요한 다른 SOAP 헤더를 정의 하는 속성입니다. 선택적 헤더는 서비스 엔드포인트를 확인하거나 상호 작용하는 데 필요한 추가적인 자세한 주소 지정 정보를 제공합니다. 엔드포인트 주소는 통신 중에 WS-Addressing EPR(엔드포인트 참조)로 표시됩니다.  
  
## <a name="uri-structure-of-an-address"></a>주소의 URI 구조  
 대부분 전송 주소 URI에는 네 가지 부분이 있습니다. 예를 들어, URI의 네 가지 부분 `http://www.fabrikam.com:322/mathservice.svc/secureEndpoint` 같이 항목별로 수 있습니다.  
  
- 파티션 구성표: `http:`
  
- 컴퓨터: `www.fabrikam.com`  
  
- (선택 사항) 포트: 322  
  
- 경로: /mathservice.svc/secureEndpoint  
  
## <a name="defining-an-address-for-a-service"></a>서비스에 대한 주소 정의  
 서비스의 엔드포인트 주소는 코드를 사용하여 명령적으로 지정하거나 구성을 통해 선언적으로 지정할 수 있습니다. 일반적으로 배포된 서비스의 바인딩과 주소가 서비스를 배포할 때 사용된 바인딩 및 주소와 다르기 때문에 코드로 엔드포인트를 정의하는 것은 효과적이지 않습니다. 일반적으로 코드 대신 구성을 사용하여 서비스 엔드포인트를 정의하는 것이 좋습니다. 바인딩 및 주소 지정 정보를 코드와 구분하면 애플리케이션을 다시 컴파일하거나 재배포할 필요 없이 해당 정보를 변경할 수 있습니다.  
  
### <a name="defining-an-address-in-configuration"></a>구성에서 주소 정의  
 구성 파일에서 끝점을 정의 하려면 사용 합니다 [ \<끝점 >](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) 요소입니다. 세부 정보 및 예제를 참조 하세요 [끝점 주소 지정](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)합니다.  
  
### <a name="defining-an-address-in-code"></a>코드에서 주소 정의  
 엔드포인트 주소는 <xref:System.ServiceModel.EndpointAddress> 클래스를 사용하여 코드에 만들 수 있습니다. 세부 정보 및 예제를 참조 하세요 [끝점 주소 지정](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)합니다.  
  
### <a name="endpoints-in-wsdl"></a>WSDL의 엔드포인트  
 엔드포인트 주소는 해당 엔드포인트의 `wsdl:port` 요소 내에 있는 WS-Addressing EPR 요소로 WSDL에서 나타낼 수도 있습니다. EPR에는 엔드포인트 주소와 주소 속성이 포함되어 있습니다. 세부 정보 및 예제를 참조 하세요 [끝점 주소 지정](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)합니다.  
  
## <a name="multiple-iis-binding-support-in-net-framework-35"></a>여러 IIS 바인딩 지원.NET Framework 3.5에서  
 인터넷 서비스 공급자는 사이트 밀도를 높이고 총 소유 비용을 줄이기 위해 종종 같은 서버 및 사이트에서 여러 애플리케이션을 호스팅합니다. 이러한 애플리케이션은 일반적으로 다른 기본 주소로 바인딩됩니다. IIS(인터넷 정보 서비스) 웹 사이트에 여러 개의 애플리케이션이 포함될 수 있습니다. 하나 이상의 IIS 바인딩을 통해 한 사이트의 애플리케이션에 액세스할 수 있습니다.  
  
 IIS 바인딩은 바인딩 프로토콜과 바인딩 정보라는 두 가지 정보를 제공합니다. 바인딩 프로토콜은 통신이 이루어지는 스키마를 정의하며, 바인딩 정보는 사이트에 액세스하는 데 사용되는 정보입니다.  
  
 다음 예제에서는 IIS 바인딩에 나타낼 수 있는 구성 요소를 보여 줍니다.  
  
- 바인딩 프로토콜: HTTP  
  
- 바인딩 정보: IP 주소, 포트, 호스트 헤더  
  
 IIS에서는 각 사이트에 대해 여러 개의 바인딩을 지정할 수 있으므로, 각 스키마에 대해 여러 개의 기본 주소가 생성됩니다. 이전 버전 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)], WCF 스키마에 대 한 여러 주소를 지원 하지 않았습니다 고, 지정 된 경우 했습니다는 <xref:System.ArgumentException> 활성화 하는 동안.  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)]를 사용하면 인터넷 서비스 공급자가 동일한 사이트의 동일한 스키마에 대해 기본 주소가 다른 여러 애플리케이션을 호스팅할 수 있습니다.  
  
 예를 들어 사이트에 다음 기본 주소가 포함될 수 있습니다.  
  
- `http://payroll.myorg.com/Service.svc`
  
- `http://shipping.myorg.com/Service.svc`
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)]를 사용하여 구성 파일의 AppDomain 수준에서 접두사 필터를 지정합니다. 이 작업을 수행 합니다 [ \<baseAddressPrefixFilters >](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md) 접두사 목록을 포함 하는 요소입니다. IIS에서 제공하는 들어오는 기본 주소는 선택적 접두사 목록을 기반으로 필터링됩니다. 기본적으로 접두사가 지정되지 않으면 모든 주소가 통과됩니다. 접두사를 지정하면 해당 스키마에서 일치하는 기본 주소만 통과됩니다.  
  
 다음은 접두사 필터를 사용하는 구성 코드의 예제입니다.  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="net.tcp://payroll.myorg.com:8000"/>  
        <add prefix="http://shipping.myorg.com:8000"/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 위의 예에서 `net.tcp://payroll.myorg.com:8000` 및 `http://shipping.myorg.com:8000` 를 통해 전달 되는 해당 스키마에 대 한 유일한 기본 주소를 합니다.  
  
 `baseAddressPrefixFilter`는 와일드카드를 지원하지 않습니다.  
  
 IIS에서 제공하는 기본 주소에 `baseAddressPrefixFilters` 목록에 없는 다른 체계에 바인딩되는 주소가 포함될 수 있습니다. 이러한 주소는 필터링되지 않습니다.  
  
## <a name="multiple-iis-binding-support-in-net-framework-4-and-later"></a>.NET Framework 4 이상의 여러 IIS 바인딩 지원  
 .NET 4부터는 단일 기본 주소를 선택해야 할 필요 없이 <xref:System.ServiceModel.ServiceHostingEnvironment>의 <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> 설정을 true로 설정하여 IIS에서 여러 바인딩을 지원할 수 있습니다. 이 지원은 HTTP 프로토콜 체계로 제한됩니다.  
  
 다음은에서 multipleSiteBindingsEnabled를 사용 하는 구성 코드의 예로 [ \<serviceHostingEnvironment >](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)합니다.  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment multipleSiteBindingsEnabled="true" >  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 이 설정을 사용하여 여러 사이트 바인딩을 사용하도록 설정하는 경우 HTTP 프로토콜과 그 외의 프로토콜에 대한 모든 baseAddressPrefixFilters 설정이 무시됩니다.  
  
 세부 정보 및 예제를 참조 하세요 [여러 IIS 사이트 바인딩을 지 원하는](../../../../docs/framework/wcf/feature-details/supporting-multiple-iis-site-bindings.md) 고 <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A>입니다.  
  
## <a name="extending-addressing-in-wcf-services"></a>WCF 서비스에서 주소 확장  
 다음과 같은 용도로 끝점 주소 URI를 사용 하는 주소 지정 모델 WCF 서비스의 기본:  
  
- 엔드포인트가 메시지를 수신 대기하는 위치인 서비스 수신 대기 주소 지정  
  
- 엔드포인트가 SOAP 헤더로 간주하는 주소인 SOAP 주소 필터 지정  
  
 이러한 각 목적에 대해 값을 별도로 지정할 수 있으며, 이렇게 하면 유용한 시나리오를 다루는 여러 가지 주소 지정 확장을 사용할 수 있습니다.  
  
- SOAP 매개자: 클라이언트가 보낸 메시지는 메시지가 최종 대상에 도달하기 전에 메시지를 처리하는 하나 이상의 추가 서비스를 통과합니다. SOAP 매개자는 메시지에 캐싱, 라우팅, 부하 분산 또는 스키마 유효성 검사 등의 여러 가지 작업을 수행할 수 있습니다. 이 시나리오는 최종 대상을 지정하는 논리적 주소(`via`)가 아니라 매개자를 대상으로 하는 메시지를 별도의 실제 주소(`wsa:To`)로 보내어 수행됩니다.  
  
- 엔드포인트의 수신 대기 주소는 개인 URI이며 해당 `listenURI` 속성과 다른 값으로 설정됩니다.  
  
 `via`에서 지정하는 전송 주소는 `to` 매개 변수에서 지정하는 다른 원격 주소(서비스가 있는 주소)로 가기 위해 메시지가 처음 전송되어야 하는 위치입니다. 대부분의 인터넷 시나리오에서 `via` URI는 서비스의 최종 <xref:System.ServiceModel.EndpointAddress.Uri%2A> 주소의 `to` 속성과 같습니다. 수동 라우팅을 수행해야 하는 경우에만 이 두 주소를 구별합니다.  
  
### <a name="addressing-headers"></a>주소 지정 헤더  
 하나 이상의 SOAP 헤더와 해당 기본 URI로 엔드포인트에 주소를 지정할 수 있습니다. 이 유용한 하나의 시나리오 집합이 SOAP 매개 시나리오 집합입니다. 이 시나리오 집합에서는 엔드포인트에 매개자를 대상으로 한 SOAP 헤더를 포함할 해당 엔드포인트의 클라이언트가 필요합니다.  
  
 코드나 구성을 사용하여 사용자 지정 주소 헤더를 정의할 수 있습니다.  
  
- 코드에서는 <xref:System.ServiceModel.Channels.AddressHeader> 클래스를 사용하여 사용자 지정 주소 헤더를 만든 다음 <xref:System.ServiceModel.EndpointAddress> 생성에 사용합니다.  
  
- 구성에서 사용자 지정 [ \<헤더 >](../../configure-apps/file-schema/wcf/headers.md) 의 자식으로 지정 된 된 [ \<끝점 >](../../configure-apps/file-schema/wcf/endpoint-of-client.md) 요소입니다.  
  
 일반적으로 구성을 사용하면 배포 후에 헤더를 변경할 수 있으므로 구성을 사용하는 것이 코드를 사용하는 것보다 낫습니다.  
  
### <a name="custom-listening-addresses"></a>사용자 지정 수신 대기 주소  
 수신 대기 주소를 엔드포인트의 URI 이외의 다른 값으로 설정할 수 있습니다. 이 기능은 노출할 SOAP 주소가 공용 SOAP 매개자의 주소이지만 실제로 수신 대기하는 엔드포인트가 개인 네트워크 주소인 매개 시나리오에서 유용합니다.  
  
 코드나 구성을 사용하여 사용자 지정 수신 대기 주소를 지정할 수 있습니다.  
  
- 코드에서는 <xref:System.ServiceModel.Description.ClientViaBehavior> 클래스를 엔드포인트의 동작 컬렉션에 추가하여 사용자 지정 수신 대기 주소를 지정합니다.  
  
- 구성에서 사용 하 여 사용자 지정 수신 대기 주소를 지정 합니다 `ListenUri` 서비스의 특성 [ \<끝점 >](../../configure-apps/file-schema/wcf/endpoint-element.md) 요소입니다.  
  
### <a name="custom-soap-address-filter"></a>사용자 지정 SOAP 주소 필터  
 <xref:System.ServiceModel.EndpointAddress.Uri%2A>는 <xref:System.ServiceModel.EndpointAddress.Headers%2A> 속성과 함께 사용되어 엔드포인트의 SOAP 주소 필터(<xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>)를 정의합니다. 기본적으로 이 필터는 들어오는 메시지에 엔드포인트의 URI와 일치하는 `To` 메시지 헤더가 있는지, 모든 필수 엔드포인트 헤더가 메시지에 있는지 확인합니다.  
  
 일부 시나리오에서 엔드포인트는 기본 전송에 도착하는 모든 메시지를 받고 해당 `To` 헤더가 있는 메시지는 받지 않습니다. 이 기능을 사용하도록 설정하려면 사용자가 <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> 클래스를 사용합니다.  
  
## <a name="see-also"></a>참고자료

- [엔드포인트 주소 지정](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)
- [서비스 ID 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
