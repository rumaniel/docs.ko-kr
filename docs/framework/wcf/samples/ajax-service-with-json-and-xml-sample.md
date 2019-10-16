---
title: JSON 및 XML 샘플을 포함한 AJAX 서비스
ms.date: 03/30/2017
ms.assetid: 8ea5860d-0c42-4ae9-941a-e07efdd8e29c
ms.openlocfilehash: eadb884667a0b29ef36056f0c3bec4675b7f1b05
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895145"
---
# <a name="ajax-service-with-json-and-xml-sample"></a>JSON 및 XML 샘플을 포함한 AJAX 서비스

이 샘플에서는 WCF (Windows Communication Foundation)를 사용 하 여 JavaScript Object Notation (JSON) 또는 XML 데이터를 반환 하는 AJAX (비동기 JavaScript and XML) 서비스를 만드는 방법을 보여 줍니다. 웹 브라우저 클라이언트에서 JavaScript 코드를 사용하여 AJAX 서비스에 액세스할 수 있습니다. 이 샘플은 [기본 AJAX 서비스](../../../../docs/framework/wcf/samples/basic-ajax-service.md) 샘플을 기반으로 합니다.

다른 AJAX 샘플과 달리 이 샘플에서는 ASP.NET AJAX 및 <xref:System.Web.UI.ScriptManager> 컨트롤을 사용하지 않습니다. 일부 추가 구성에서는 JavaScript를 통해 모든 HTML 페이지에서 WCF AJAX 서비스에 액세스할 수 있으며,이 시나리오는 여기에 나와 있습니다. ASP.NET AJAX에서 WCF를 사용 하는 예제는 [Ajax 샘플](ajax.md)을 참조 하세요.

이 샘플에서는 작업의 응답 형식을 JSON과 XML 간에 전환하는 방법을 보여 줍니다. 이 기능은 서비스가 ASP.NET AJAX에서 액세스하도록 구성되었는지 아니면 HTML/JavaScript 클라이언트 페이지에서 액세스하도록 구성되었는지 여부에 관계없이 사용할 수 있습니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

ASP.NET 이외의 AJAX 클라이언트를 사용할 수 있도록 설정하려면 .svc 파일에서 <xref:System.ServiceModel.Activation.WebServiceHostFactory>가 아닌 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>를 사용합니다. <xref:System.ServiceModel.Activation.WebServiceHostFactory>는 <xref:System.ServiceModel.Description.WebHttpEndpoint> 표준 엔드포인트를 서비스에 추가합니다. 끝점은 .svc 파일을 기준으로 하는 빈 주소에 구성 됩니다. 즉, 서비스의 주소는 이며 `http://localhost/ServiceModelSamples/service.svc`작업 이름이 아닌 추가 접미사를 포함 하지 않습니다.

`<%@ServiceHost language="c#" Debug="true" Service="Microsoft.Samples.XmlAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebServiceHostFactory" %>`

Web.config의 다음 섹션은 끝점에 대한 추가 구성 변경 작업을 수행하는 데 사용할 수 있으며 추가 변경이 필요하지 않은 경우 제거할 수 있습니다.

```xml
<system.serviceModel>
  <standardEndpoints>
    <webHttpEndpoint>
      <!-- Use this element to configure the endpoint -->
      <standardEndpoint name="" />
    </webHttpEndpoint>
  </standardEndpoints>
</system.serviceModel>
```

의 <xref:System.ServiceModel.Description.WebHttpEndpoint> 기본 데이터 형식은 XML 이지만의 <xref:System.ServiceModel.Description.WebScriptEndpoint> 기본 데이터 형식은 JSON입니다. 자세한 내용은 ASP.NET를 사용 [하지 않고 WCF AJAX 서비스 만들기](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md)를 참조 하세요.

다음 샘플의 서비스는 두 개의 작업을 포함 하는 표준 WCF 서비스입니다. 두 작업 모두 <xref:System.ServiceModel.Web.WebMessageBodyStyle.Wrapped> 또는 <xref:System.ServiceModel.Web.WebGetAttribute> 특성에서 <xref:System.ServiceModel.Web.WebInvokeAttribute> 본문 스타일을 필요로 합니다. 이는 `webHttp` 동작과 관련이 있으며 JSON/XML 데이터 형식 전환과는 관계가 없습니다.

```csharp
[OperationContract]
[WebInvoke(ResponseFormat = WebMessageFormat.Xml, BodyStyle = WebMessageBodyStyle.Wrapped)]
MathResult DoMathXml(double n1, double n2);
```

작업에 대 한 응답 형식은 [ \<webhttp >](../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) 동작에 대 한 기본 설정인 XML로 지정 됩니다. 그러나 응답 형식을 명시적으로 지정하는 것이 좋습니다.

다른 작업에서는 `WebInvokeAttribute` 특성을 사용하고 응답에 대해 XML 대신 명시적으로 JSON을 지정합니다.

```csharp
[OperationContract]
[WebInvoke(ResponseFormat = WebMessageFormat.Json, BodyStyle = WebMessageBodyStyle.Wrapped)]
MathResult DoMathJson(double n1, double n2);
```

두 경우 모두 `MathResult`, 작업은 표준 WCF 데이터 계약 형식인 복합 형식인을 반환 합니다.

클라이언트 웹 페이지 Xmlajaxclientpage.htm에는 사용자가 **계산 수행 (JSON 반환)** 또는 페이지에서 **계산 수행 (XML 반환)** 단추를 클릭할 때 앞의 두 작업 중 하나를 호출 하는 JavaScript 코드가 포함 됩니다. 서비스를 호출하는 코드는 JSON 본문을 만든 다음 HTTP POST를 사용하여 전송합니다. [기본 Ajax 서비스](../../../../docs/framework/wcf/samples/basic-ajax-service.md) 샘플과 ASP.NET ajax를 사용 하는 다른 샘플과 달리이 요청은 JavaScript에서 수동으로 생성 됩니다.

```csharp
// Create HTTP request
var xmlHttp;
// Request instantiation code omitted…
// Result handler code omitted…

// Build the operation URL
var url = "service.svc/ajaxEndpoint/";
url = url + operation;

// Build the body of the JSON message
var body = '{"n1":';
body = body + document.getElementById("num1").value + ',"n2":';
body = body + document.getElementById("num2").value + '}';

// Send the HTTP request
xmlHttp.open("POST", url, true);
xmlHttp.setRequestHeader("Content-type", "application/json");
xmlHttp.send(body);
```

서비스가 응답하면 페이지의 텍스트 상자에서 더 이상의 처리 작업 없이 응답이 표시됩니다. 이는 사용된 XML 및 JSON 데이터 형식을 직접 확인할 수 있도록 데모용으로 구현됩니다.

```javascript
// Create result handler
xmlHttp.onreadystatechange=function(){
     if(xmlHttp.readyState == 4){
          document.getElementById("result").value = xmlHttp.responseText;
     }
}
```

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\XmlAjaxService`

#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)에 설명 된 대로 XmlAjaxService 솔루션을 빌드합니다.

3. 로 `http://localhost/ServiceModelSamples/XmlAjaxClientPage.htm` 이동 합니다 (프로젝트 디렉터리에서 브라우저의 xmlajaxclientpage.htm을 열지 마십시오.).

## <a name="see-also"></a>참고자료

- [HTTP POST를 사용하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)
