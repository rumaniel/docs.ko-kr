---
title: WCF 웹 HTTP 프로그래밍 개체 모델
ms.date: 03/30/2017
ms.assetid: ed96b5fc-ca2c-4b0d-bdba-d06b77c3cb2a
ms.openlocfilehash: 43ec16927c703ca373eaa4299093503b2fab2266
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988568"
---
# <a name="wcf-web-http-programming-object-model"></a>WCF 웹 HTTP 프로그래밍 개체 모델
WCF 웹 HTTP 프로그래밍 모델을 통해 개발자는 SOAP 없이 기본 HTTP 요청을 통해 WCF (Windows Communication Foundation) 웹 서비스를 노출할 수 있습니다. WCF 웹 HTTP 프로그래밍 모델은 기존 WCF 확장성 모델을 기반으로 빌드됩니다. 다음과 같은 클래스를 정의합니다.  
  
 **프로그래밍 모델:**  
  
- <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>  
  
- <xref:System.ServiceModel.Web.WebGetAttribute>  
  
- <xref:System.ServiceModel.Web.WebInvokeAttribute>  
  
- <xref:System.ServiceModel.Web.WebServiceHost>  
  
 **채널 및 디스패처 인프라:**  
  
- <xref:System.ServiceModel.WebHttpBinding>  
  
- <xref:System.ServiceModel.Description.WebHttpBehavior>  
  
 **유틸리티 클래스 및 확장성 가리키기:**  
  
- <xref:System.UriTemplate>  
  
- <xref:System.UriTemplateTable>  
  
- <xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
- <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>  
  
## <a name="aspnetcacheprofileattribute"></a>AspNetCacheProfileAttribute  
 서비스 작업에 적용된 경우 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>는 작업의 응답을 ASP .NET 출력 캐시에 캐시하는 데 사용해야 하는 구성 파일의 ASP.NET 출력 캐시 프로필을 나타냅니다. 이 속성은 하나의 매개 변수, 즉 구성 파일에서 캐시 설정을 지정하는 캐시 프로필 이름만 사용합니다.  
  
## <a name="webgetattribute"></a>WebGetAttribute  
 <xref:System.ServiceModel.Web.WebGetAttribute> 특성은 서비스 작업을 HTTP GET 요청에 응답하는 작업으로 표시하는 데 사용됩니다. 이는 작업 설명에 메타데이터를 추가하는 수동 작업 동작입니다(<xref:System.ServiceModel.Description.IOperationBehavior> 메서드는 아무 작업도 하지 않음). 작업 설명에서 이 메타데이터를 찾는 동작(특히 <xref:System.ServiceModel.Web.WebGetAttribute>)이 서비스의 동작 컬렉션에 추가되지 않으면 <xref:System.ServiceModel.Description.WebHttpBehavior>를 적용해도 아무 효과가 없습니다. <xref:System.ServiceModel.Web.WebGetAttribute> 특성은 다음 표에 있는 선택적 매개 변수를 사용합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|`BodyStyle`|특성이 적용된 서비스 작업으로 보내거나 받은 요청 및 응답을 래핑할지 여부를 제어합니다.|  
|`RequestFormat`|요청 메시지의 형식을 지정하는 방법을 제어합니다.|  
|`ResponseFormat`|응답 메시지의 형식을 지정하는 방법을 제어합니다.|  
|`UriTemplate`|특성이 적용된 서비스 작업에 매핑되는 HTTP 요청을 제어하는 URI 템플릿을 지정합니다.|  
  
## <a name="webhttpbinding"></a>WebHttpBinding  
 <xref:System.ServiceModel.WebHttpBinding> 클래스는 <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>를 사용하여 XML, JSON 및 원시 이진 데이터에 대한 지원을 통합합니다. 이는 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>, <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 및 <xref:System.ServiceModel.WebHttpSecurity> 개체로 구성됩니다. <xref:System.ServiceModel.WebHttpBinding>은 <xref:System.ServiceModel.Description.WebHttpBehavior>와 함께 사용하도록 디자인되었습니다.  
  
## <a name="webinvokeattribute"></a>WebInvokeAttribute  
 <xref:System.ServiceModel.Web.WebInvokeAttribute> 특성은 <xref:System.ServiceModel.Web.WebGetAttribute>와 비슷하지만 서비스 작업을 GET가 아닌 HTTP 요청에 응답하는 작업으로 표시하는 데 사용됩니다. 이는 작업 설명에 메타데이터를 추가하는 수동 작업 동작입니다(<xref:System.ServiceModel.Description.IOperationBehavior> 메서드는 아무 작업도 하지 않음). 작업 설명에서 이 메타데이터를 찾는 동작(특히 <xref:System.ServiceModel.Web.WebInvokeAttribute>)이 서비스의 동작 컬렉션에 추가되지 않으면 <xref:System.ServiceModel.Description.WebHttpBehavior>를 적용해도 아무 효과가 없습니다.  
  
 <xref:System.ServiceModel.Web.WebInvokeAttribute> 특성은 다음 표에 있는 선택적 매개 변수를 사용합니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|`BodyStyle`|특성이 적용된 서비스 작업으로 보내거나 받은 요청 및 응답을 래핑할지 여부를 제어합니다.|  
|`Method`|서비스 작업이 매핑되는 HTTP 메서드를 지정합니다.|  
|`RequestFormat`|요청 메시지의 형식을 지정하는 방법을 제어합니다.|  
|`ResponseFormat`|응답 메시지의 형식을 지정하는 방법을 제어합니다.|  
|`UriTemplate`|특성이 적용된 서비스 작업에 매핑되는 GET 요청을 제어하는 URI 템플릿을 지정합니다.|  
  
## <a name="uritemplate"></a>UriTemplate  
 <xref:System.UriTemplate> 클래스를 사용하면 구조적으로 비슷한 URI 집합을 정의할 수 있습니다. 템플릿은 경로와 쿼리의 두 부분으로 구성됩니다. 경로는 슬래시(/)로 구분된 세그먼트로 구성됩니다. 각 세그먼트는 리터럴 값, 변수 값 (중괄호 [{}] 안에 작성 됨, 정확히 한 세그먼트의 내용과 일치 하도록 제한 됨) 또는 와일드 카드 (별표 [\*]로 작성 됨)를 포함할 수 있습니다 .이는 다음에 표시 되어야 합니다. 경로의 끝입니다. 쿼리 식은 완전히 생략할 수 있습니다. 쿼리 식(있는 경우)은 순서가 지정되지 않은 이름/값 쌍을 지정합니다. 쿼리 식의 요소는 리터럴 쌍 (? x = 2) 또는 변수 쌍 (? x = {*value*}) 중 하나일 수 있습니다. 짝이 없는 값은 사용할 수 없습니다. <xref:System.UriTemplate>는 WCF 웹 HTTP 프로그래밍 모델에서 특정 Uri 또는 Uri 그룹을 서비스 작업에 매핑하는 데 내부적으로 사용 됩니다.  
  
## <a name="uritemplatetable"></a>UriTemplateTable  
 <xref:System.UriTemplateTable> 클래스는 개발자가 선택한 개체에 바인딩된 <xref:System.UriTemplate> 개체의 관련 집합을 나타냅니다. 후보 URI(Uniform Resource Identifier)를 세트의 템플릿에 일치시키고 일치하는 템플릿과 연결된 데이터를 검색할 수 있습니다. <xref:System.UriTemplateTable>는 WCF 웹 HTTP 프로그래밍 모델에서 특정 Uri 또는 Uri 그룹을 서비스 작업에 매핑하는 데 내부적으로 사용 됩니다.  
  
## <a name="webservicehost"></a>WebServiceHost  
 <xref:System.ServiceModel.Web.WebServiceHost>는 비SOAP 웹 스타일 서비스를 보다 쉽게 호스트할 수 있도록 <xref:System.ServiceModel.ServiceHost>를 확장합니다. <xref:System.ServiceModel.Web.WebServiceHost>는 서비스 설명에서 엔드포인트를 찾지 못하는 경우 자동으로 서비스의 기본 주소에 기본 엔드포인트를 만듭니다. 기본 HTTP 엔드포인트를 만들 때 <xref:System.ServiceModel.Web.WebServiceHost>는 메타데이터 엔드포인트가 기본 HTTP 엔드포인트와 간섭하지 않도록 HTTP 도움말 페이지 및 WSDL(웹 서비스 기술 언어) GET 기능을 비활성화합니다. <xref:System.ServiceModel.Web.WebServiceHost>는 또한 <xref:System.ServiceModel.WebHttpBinding>을 사용하는 모든 엔드포인트에 필수 <xref:System.ServiceModel.Description.WebHttpBehavior>가 연결되어 있는지 확인합니다. 마지막으로<xref:System.ServiceModel.Web.WebServiceHost>는 보안 가상 디렉터리에서 사용될 때 연결된 IIS(인터넷 정보 서비스) 보안 설정과 함께 작동하도록 엔드포인트의 바인딩을 자동으로 구성합니다.  
  
## <a name="webservicehostfactory"></a>WebServiceHostFactory  
 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 클래스는 서비스가 IIS(인터넷 정보 서비스) 또는 WAS(Windows Process Activation Service)에서 호스트될 때 동적으로 <xref:System.ServiceModel.Web.WebServiceHost>를 만드는 데 사용됩니다. 호스팅 애플리케이션이 <xref:System.ServiceModel.Web.WebServiceHost>를 인스턴스화하는 자체 호스팅 서비스와 달리 IIS 또는 WAS에서 호스트되는 서비스는 이 클래스를 사용하여 서비스에 대한 <xref:System.ServiceModel.Web.WebServiceHost>를 만듭니다. <xref:System.ServiceModel.Activation.WebServiceHostFactory.CreateServiceHost%28System.Type%2CSystem.Uri%5B%5D%29> 메서드는 서비스에 대한 들어오는 요청을 수신할 때 호출됩니다.  
  
## <a name="webhttpbehavior"></a>WebHttpBehavior  
 <xref:System.ServiceModel.Description.WebHttpBehavior> 클래스는 서비스 모델 계층에서 웹 스타일 서비스 지원에 필요한 필수 포맷터, 작업 선택기 등을 제공합니다. 이 클래스는 <xref:System.ServiceModel.WebHttpBinding>과 함께 사용되는 엔드포인트 동작으로 구현되며 각 엔드포인트에 대해 포맷터와 작업 선택기를 지정하도록 허용하여 동일한 서비스 구현에서 SOAP 엔드포인트와 POX 엔드포인트를 모두 노출할 수 있습니다.  
  
### <a name="extending-webhttpbehavior"></a>WebHttpBehavior 확장  
 <xref:System.ServiceModel.Description.WebHttpBehavior>는 <xref:System.ServiceModel.Description.WebHttpBehavior.GetOperationSelector%28System.ServiceModel.Description.ServiceEndpoint%29>, <xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>, <xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>, <xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>, <xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29> 등과 같은 여러 가지 가상 메서드를 사용하여 확장할 수 있습니다. 개발자는 <xref:System.ServiceModel.Description.WebHttpBehavior>에서 클래스를 파생하고 이러한 메서드를 재정의하여 기본 동작을 사용자 지정할 수 있습니다.  
  
 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>는 <xref:System.ServiceModel.Description.WebHttpBehavior>를 확장한 한 예입니다. <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>WCF (Windows Communication Foundation) 끝점에서 브라우저 기반 ASP.NET AJAX 클라이언트의 HTTP 요청을 받을 수 있도록 합니다. [HTTP POST를 사용 하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md) 는이 확장성 지점을 사용 하는 예입니다.  
  
> [!WARNING]
> <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>를 사용할 때 <xref:System.UriTemplate>은 <xref:System.ServiceModel.Web.WebGetAttribute> 또는 <xref:System.ServiceModel.Web.WebInvokeAttribute> 특성 내에서 지원되지 않습니다.  
  
## <a name="webhttpdispatchoperationselector"></a>WebHttpDispatchOperationSelector  
 <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector> 클래스는 <xref:System.UriTemplate> 및 <xref:System.UriTemplateTable> 클래스를 사용하여 호출을 서비스 작업에 디스패치합니다.  
  
## <a name="compatibility"></a>호환성  
 WCF 웹 HTTP 프로그래밍 모델은 SOAP 기반 메시지를 사용 하지 않으므로 WS-* 프로토콜을 지원 하지 않습니다. 그러나 SOAP를 사용하는 엔드포인트와 SOAP를 사용하지 않는 엔드포인트 등 두 개의 다른 엔드포인트에 대해 동일한 계약을 노출할 수 있습니다. [방법: 예제를 위해 SOAP 및 웹 클라이언트](../../../../docs/framework/wcf/feature-details/how-to-expose-a-contract-to-soap-and-web-clients.md) 에 계약을 노출 합니다.  
  
## <a name="security"></a>보안  
 WCF 웹 HTTP 프로그래밍 모델은 WS-* 프로토콜을 지원 하지 않으므로 WCF 웹 HTTP 프로그래밍 모델을 기반으로 하는 웹 서비스를 보호 하는 유일한 방법은 SSL을 사용 하 여 서비스를 노출 하는 것입니다. IIS 7.0로 SSL을 설정 하는 방법에 대 한 자세한 내용은 [iis에서 ssl을 구현 하는 방법을](https://go.microsoft.com/fwlink/?LinkId=131613) 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>
- [WCF 웹 HTTP 프로그래밍 모델 개요](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)
