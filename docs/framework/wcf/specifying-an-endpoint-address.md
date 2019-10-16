---
title: 엔드포인트 주소 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- endpoints [WCF], addressing
ms.assetid: ac24f5ad-9558-4298-b168-c473c68e819b
ms.openlocfilehash: 6f62d0f712f7461ef8cd65f15f3ed2690446bae1
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044451"
---
# <a name="specifying-an-endpoint-address"></a>엔드포인트 주소 지정

WCF (Windows Communication Foundation) 서비스와의 모든 통신은 해당 끝점을 통해 수행 됩니다. 각 <xref:System.ServiceModel.Description.ServiceEndpoint>에는 <xref:System.ServiceModel.Description.ServiceEndpoint.Address%2A>, <xref:System.ServiceModel.Description.ServiceEndpoint.Binding%2A> 및 <xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A>가 포함되어 있습니다. 계약은 사용할 수 있는 작업을 지정합니다. 바인딩은 서비스와 통신하는 방법을 지정하고 주소는 서비스를 찾을 위치를 지정합니다. 모든 엔드포인트에는 고유한 주소가 있어야 합니다. 엔드포인트 주소는 서비스 주소를 표시하는 URI(Uniform Resource Identifier)가 포함된 <xref:System.ServiceModel.EndpointAddress> 클래스, 서비스의 보안 ID를 표시하는 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 및 선택적 <xref:System.ServiceModel.EndpointAddress.Headers%2A>의 컬렉션에 의해 표시됩니다. 선택적 헤더는 엔드포인트를 확인하거나 상호 작용하는 데 필요한 자세한 주소 지정 정보를 제공합니다. 예를 들어 헤더는 들어오는 메시지를 처리하는 방법, 엔드포인트가 회신 메시지를 보내야 하는 위치 또는 여러 인스턴스를 사용할 수 있는 경우 특정 사용자의 들어오는 메시지를 처리하는 데 사용할 서비스 인스턴스를 나타낼 수 있습니다.

## <a name="definition-of-an-endpoint-address"></a>엔드포인트 주소 정의

WCF에서는 <xref:System.ServiceModel.EndpointAddress> ws-addressing 표준에 정의 된 대로 끝점 참조 (EPR)를 모델링 합니다.

대부분 전송 주소 URI에는 네 가지 부분이 있습니다. 예를 들어이 URI `http://www.fabrikam.com:322/mathservice.svc/secureEndpoint` 는 다음과 같은 네 부분으로 구성 됩니다.

- 스키마: http:

- 컴퓨터`www.fabrikam.com`

- 필드 포트인 322

- 경로: /mathservice.svc/secureEndpoint

EPR 모델 일부에서는 각 엔드포인트 참조에 추가 식별 정보를 추가하는 일부 참조 매개 변수를 포함할 수 있습니다. WCF에서 이러한 참조 매개 변수는 <xref:System.ServiceModel.Channels.AddressHeader> 클래스의 인스턴스로 모델링 됩니다.

서비스의 엔드포인트 주소는 코드를 사용하여 명령적으로 지정하거나 구성을 통해 선언적으로 지정할 수 있습니다. 일반적으로 배포된 서비스의 바인딩과 주소가 서비스를 배포할 때 사용된 바인딩 및 주소와 다르기 때문에 코드로 엔드포인트를 정의하는 것은 효과적이지 않습니다. 일반적으로 코드 대신 구성을 사용하여 서비스 엔드포인트를 정의하는 것이 좋습니다. 바인딩 및 주소 지정 정보를 코드와 구분하면 애플리케이션을 다시 컴파일하여 재배포할 필요 없이 해당 정보를 변경할 수 있습니다. 코드 또는 구성에서 엔드포인트를 지정하지 않으면 런타임이 서비스에서 구현되는 각 계약의 각 기본 주소에 대해 기본 엔드포인트를 하나씩 추가합니다.

WCF에서 서비스에 대 한 끝점 주소를 지정 하는 방법에는 두 가지가 있습니다. 서비스와 연결된 각 엔드포인트에 대한 절대 주소를 지정하거나 서비스의 <xref:System.ServiceModel.ServiceHost>에 대한 기본 주소를 제공할 수 있으며 그런 다음 이 기본 주소를 기준으로 정의된 이 서비스와 연결된 각 엔드포인트에 대한 주소를 지정할 수 있습니다. 이러한 각 절차를 사용하여 구성 또는 코드에서 서비스에 대한 엔드포인트 주소를 지정할 수 있습니다. 상대 주소를 지정하지 않을 경우 서비스는 기본 주소를 사용합니다. 또한 하나의 서비스에 대해 여러 기본 주소를 사용할 수 있지만 각 서비스는 각 전송에 대해 하나의 기본 주소만 허용됩니다. 여러 엔드포인트를 가진 경우 각 엔드포인트는 서로 다른 바인딩으로 구성되며 해당 주소가 고유해야 합니다. 동일한 바인딩을 사용하지만 서로 다른 계약을 사용하는 엔드포인트는 동일한 주소를 사용할 수 있습니다.

IIS를 사용하여 호스팅하는 경우 사용자는 <xref:System.ServiceModel.ServiceHost> 인스턴스를 직접 관리하지 않습니다. IIS에서 호스팅하는 경우 기본 주소는 항상 서비스의 .svc 파일에 지정된 주소입니다. 따라서 IIS에서 호스팅되는 서비스 엔드포인트에는 상대 엔드포인트 주소를 사용해야 합니다. 정규화된 엔드포인트 주소를 제공할 경우 서비스 배포 시 오류가 발생할 수 있습니다. 자세한 내용은 [인터넷 정보 서비스 호스팅된 WCF 서비스 배포](../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)를 참조 하세요.

## <a name="defining-endpoint-addresses-in-configuration"></a>구성에서 엔드포인트 주소 정의

구성 파일에서 끝점을 정의 하려면 [ \<끝점 >](../configure-apps/file-schema/wcf/endpoint-element.md) 요소를 사용 합니다.

[!code-xml[S_UEHelloWorld#5](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp2.config#5)]

메서드가 호출 될 때 (즉, 호스팅 응용 프로그램이 서비스를 시작 하려고 할 때) 시스템은 "UE를 지정 하는 이름 특성을 사용 하 여 [ \<서비스 >](../../../docs/framework/configure-apps/file-schema/wcf/service.md) 요소를 찾습니다. <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> HelloService ". 서비스 > 요소가 발견 되 면 시스템은 지정 된 클래스를 로드 하 고 구성 파일에 제공 된 끝점 정의를 사용 하 여 끝점을 만듭니다. [ \<](../../../docs/framework/configure-apps/file-schema/wcf/service.md) 이 메커니즘을 통해 두 개의 코드 줄에서 서비스를 로드하고 시작하는 동시에 해당 코드의 바인딩 및 주소 지정 정보를 유지할 수 있습니다. 이 접근 방식의 이점은 애플리케이션을 다시 컴파일하거나 다시 배포할 필요 없이 이러한 변경 작업을 수행할 수 있다는 점입니다.

선택적 헤더는 [ \<> 헤더](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)에 선언 됩니다. 다음은 두 헤더를 구분 하는 구성 파일에서 서비스에 대 한 끝점을 지정 하는 데 사용 되는 요소의 예입니다. 및의 "표준" `http://tempuri1.org/` `http://tempuri2.org/`클라이언트에서 "골드" 클라이언트 이 서비스를 호출 하는 클라이언트의 구성 파일에 > 적절 한 [ \<헤더가](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md) 있어야 합니다.

[!code-xml[S_UEHelloWorld#1](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp.config#1)]

또한 헤더는 이전에 설명한 것처럼 엔드포인트의 모든 메시지 대신 개별 메시지에서 설정될 수 있습니다. 이 작업은 다음 예제에서처럼 보내는 메시지에 사용자 지정 헤더를 추가하기 위해 <xref:System.ServiceModel.OperationContextScope>를 사용하여 클라이언트 애플리케이션에서 새 컨텍스트를 만들어 수행합니다.

[!code-csharp[OperationContextScope#4](../../../samples/snippets/csharp/VS_Snippets_CFX/operationcontextscope/cs/client.cs#4)]
[!code-vb[OperationContextScope#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationcontextscope/vb/client.vb#4)]

## <a name="endpoint-address-in-metadata"></a>메타데이터의 엔드포인트 주소

엔드포인트 주소는 해당 엔드포인트의 `EndpointReference` 요소 내에서 WS-Addressing `wsdl:port`(EPR) 요소로서 WSDL(웹 서비스 기술 언어)로 표시됩니다. EPR에는 엔드포인트 주소와 주소 속성이 포함되어 있습니다. `wsdl:port` 내의 EPR은 다음 예제에 표시된 것처럼 `soap:Address`로 바뀝니다.

## <a name="defining-endpoint-addresses-in-code"></a>코드에서 엔드포인트 주소 정의

엔드포인트 주소는 <xref:System.ServiceModel.EndpointAddress> 클래스를 사용하여 코드에 만들 수 있습니다. 엔드포인트 주소에 대해 지정된 URI는 정규화된 경로 또는 서비스 기본 주소에 상대적인 경로일 수 있습니다. 다음 코드에서는 <xref:System.ServiceModel.EndpointAddress> 클래스의 인스턴스를 만들어 서비스를 호스팅하는 <xref:System.ServiceModel.ServiceHost> 인스턴스에 추가하는 방법을 보여 줍니다.

다음 예제에서는 전체 엔드포인트 주소를 코드에서 지정하는 방법을 보여 줍니다.

[!code-csharp[S_UEHelloWorld#2](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#2)]

다음 예제에서는 상대 주소("MyService")를 서비스 호스트의 기본 주소에 추가하는 방법을 보여 줍니다.

[!code-csharp[S_UEHelloWorld#3](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#3)]

> [!NOTE]
> <xref:System.ServiceModel.Description.ServiceDescription>의 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> 메서드 다음에 나오는 서비스 애플리케이션의 <xref:System.ServiceModel.ServiceHostBase> 속성은 수정하면 안 됩니다. <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 및 `AddServiceEndpoint`에서 <xref:System.ServiceModel.ServiceHostBase> 속성과 <xref:System.ServiceModel.ServiceHost> 메서드와 같은 일부 멤버는 해당 지점을 지나서 수정할 경우 예외를 throw합니다. 다른 멤버에서는 이를 수정할 수 있지만 그 결과는 예측할 수 없습니다.
>
> 마찬가지로 클라이언트에서 <xref:System.ServiceModel.Description.ServiceEndpoint>의 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A>을 호출한 이후에는 <xref:System.ServiceModel.ChannelFactory> 값을 수정해서는 안 됩니다. <xref:System.ServiceModel.ChannelFactory.Credentials%2A> 속성은 해당 지점을 지나서 수정할 경우 예외를 throw합니다. 다른 클라이언트 설명 값은 수정해도 오류가 발생하지 않지만 결과가 정의되어 있지 않습니다.
>
> 서비스와 클라이언트 모두에 대해 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>을 호출하기 이전에 설명을 수정하는 것이 좋습니다.

## <a name="using-default-endpoints"></a>기본 엔드포인트 사용

코드 또는 구성에서 엔드포인트를 지정하지 않으면 런타임이 서비스에서 구현되는 각 서비스 계약의 각 기본 주소에 대해 기본 엔드포인트를 하나씩 추가하여 기본 엔드포인트를 제공합니다. 기본 주소는 코드 또는 구성에서 지정할 수 있으며 기본 엔드포인트는 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>에서 <xref:System.ServiceModel.ServiceHost>을 호출하면 추가됩니다.

엔드포인트를 명시적으로 제공하는 경우에도 <xref:System.ServiceModel.ServiceHostBase.AddDefaultEndpoints%2A>을 호출하기 전에 <xref:System.ServiceModel.ServiceHost>에서 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>를 호출하여 기본 엔드포인트를 추가할 수 있습니다. 기본 엔드포인트, 바인딩 및 동작에 대한 자세한 내용은 [단순화된 구성](../../../docs/framework/wcf/simplified-configuration.md) 및 [WCF 서비스를 위한 단순화된 구성](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)을 참조하세요.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.EndpointAddress>
- [서비스 ID 및 인증](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [엔드포인트 만들기 개요](../../../docs/framework/wcf/endpoint-creation-overview.md)
- [호스팅](../../../docs/framework/wcf/feature-details/hosting.md)
