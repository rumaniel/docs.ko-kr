---
title: ASP.NET을 사용하지 않고 WCF AJAX 서비스 만들기
ms.date: 03/30/2017
ms.assetid: ba4a7d1b-e277-4978-9f62-37684e6dc934
ms.openlocfilehash: 04d2831407f4aa32c72aabbbff0e6fdde769bd23
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895095"
---
# <a name="creating-wcf-ajax-services-without-aspnet"></a>ASP.NET을 사용하지 않고 WCF AJAX 서비스 만들기
ASP.NET AJAX를 요구 하지 않고 모든 JavaScript 사용 웹 페이지에서 WCF (Windows Communication Foundation) AJAX 서비스에 액세스할 수 있습니다. 이 항목에서는 이러한 WCF 서비스를 만드는 방법에 대해 설명 합니다.  
  
 ASP.NET AJAX에서 WCF를 사용 하는 방법에 대 한 지침은 [ASP.NET ajax 용 Wcf 서비스 만들기](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)를 참조 하세요.  
  
 WCF AJAX 서비스를 만드는 세 가지 부분이 있습니다.  
  
- 브라우저에서 액세스할 수 있는 AJAX 엔드포인트 만들기  
  
- AJAX 호환 서비스 계약 만들기  
  
- WCF AJAX 서비스 액세스  
  
## <a name="creating-an-ajax-endpoint"></a>AJAX 엔드포인트 만들기  
 WCF 서비스에서 AJAX 지원을 사용 하도록 설정 하는 가장 기본적인 방법은 다음 예제와 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 같이 서비스와 연결 된 .svc 파일에서를 사용 하는 것입니다.  
  
```text
<%ServiceHost   
    language=c#  
    Debug="true"  
    Service="Microsoft.Ajax.Samples.CityService"  
    Factory=System.ServiceModel.Activation.WebServiceHostFactory  
%>  
```  
  
 또는 구성을 사용하여 AJAX 엔드포인트를 추가할 수도 있습니다. 서비스 엔드포인트에서 <xref:System.ServiceModel.WebHttpBinding>을 사용하고 해당 엔드포인트를 다음 코드 조각에 표시된 것처럼 <xref:System.ServiceModel.Description.WebHttpBehavior>로 구성합니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="AjaxBehavior">  
          <webHttp/>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <services>  
      <service name="Microsoft.Ajax.Samples.CityService">  
        <endpoint   
          address="ajaxEndpoint"  
          behaviorConfiguration="AjaxBehavior"  
          binding="webHttpBinding"  
          contract="Microsoft.Ajax.Samples.ICityService" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
 작업 예제는 [JSON 및 XML을 사용 하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md)를 참조 하세요.  
  
## <a name="creating-an-ajax-compatible-service-contract"></a>AJAX 호환 서비스 계약 만들기  
 기본적으로 AJAX 엔드포인트를 통해 노출된 서비스 계약은 데이터를 XML 형식으로 반환합니다. 또한 기본적으로 서비스 작업은 다음 예제에서처럼 HTTP POST 요청을 통해 엔드포인트 주소 다음에 작업 이름이 오는 URL에 액세스할 수 있습니다.  
  
```csharp
[OperationContract]  
string[] GetCities(string firstLetters);  
```  
  
 이 작업은에 대 한 HTTP POST를 `http://serviceaddress/endpointaddress/GetCities` 사용 하 여 액세스할 수 있으며 XML 메시지를 반환 합니다.  
  
 전체 웹 프로그래밍 모델을 사용하여 이러한 기본 측면을 사용자 지정할 수 있습니다. 예를 들어 <xref:System.ServiceModel.Web.WebGetAttribute> 또는 <xref:System.ServiceModel.Web.WebInvokeAttribute> 특성을 사용하여 작업이 응답하는 HTTP 동사를 제어하거나 이러한 각 특성의 `UriTemplate` 속성을 사용하여 사용자 지정 URI를 지정할 수 있습니다. 자세한 내용은 [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md) 항목을 참조 하세요.  
  
 JSON 데이터 형식은 AJAX 서비스에서 주로 사용됩니다. XML 대신 JSON을 반환하는 작업을 만들려면 <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> (또는 <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A>) 속성을 <xref:System.ServiceModel.Web.WebMessageFormat.Json>으로 설정합니다. [독립 실행형 Json Serialization](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md) 항목에서는 기본 제공 .net 형식 및 데이터 계약 형식이 JSON에 매핑되는 방법을 보여 줍니다.  
  
 일반적으로 JSON 요청 및 응답은 하나의 항목으로만 구성됩니다. 앞의 `GetCities` 작업의 경우 요청은 다음 문과 유사하고.  
  
```json
"na"  
```  
  
 해당 요청에 대한 응답은 다음 문과 유사합니다.  
  
```json
["Nairobi", "Naples", "Nashville"]  
```  
  
 작업에서 추가 매개 변수를 가져올 경우 요청 스타일은 단일 JSON 개체에서 두 매개 변수를 래핑하기 위해 래핑되어야 합니다. 이 스타일 JSON 메시지의 예는 다음 예제에 나와 있습니다.  
  
```json  
{"firstLetters": "na", "maxNumber": 2}  
```  
  
 다음 계약이 이 메시지를 받습니다.  
  
```csharp
[WebInvoke(BodyStyle=WebMessageBodyStyle.WrappedRequest, ResponseFormat=WebMessageFormat.Json)]  
[OperationContract]  
string[] GetCities(string firstLetters, int maxNumber);  
```  
  
## <a name="accessing-ajax-services"></a>AJAX 서비스 액세스  
 WCF AJAX 끝점은 항상 JSON 및 XML 요청을 허용 합니다.  
  
 콘텐츠 형식이 "application/json" 인 HTTP POST 요청은 JSON으로 처리 되 고 XML을 나타내는 content-type 형식 (예: "text/XML")이 XML로 처리 됩니다.  
  
 HTTP GET 요청에는 URL 자체의 모든 요청 매개 변수가 포함되어 있습니다.  
  
 엔드포인트에 대한 HTTP 요청을 만드는 방법을 결정하는 것은 사용자의 몫입니다. 또한 사용자는 요청 본문을 형성하는 JSON 생성에 대한 전체 제어 권한을 가집니다. JavaScript에서 요청을 만드는 방법에 대 한 예제는 [JSON 및 XML을 사용 하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md)를 참조 하세요.
