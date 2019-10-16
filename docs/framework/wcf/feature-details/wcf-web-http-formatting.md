---
title: WCF 웹 HTTP 형식 지정
ms.date: 03/30/2017
ms.assetid: e2414896-5463-41cd-b0a6-026a713eac2c
ms.openlocfilehash: 884193dc26794be5e8a3c95e05be2ca43a90f6e2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64643464"
---
# <a name="wcf-web-http-formatting"></a>WCF 웹 HTTP 형식 지정
WCF 웹 HTTP 프로그래밍 모델을 사용하면 서비스 작업의 응답을 반환하는 데 사용할 수 있는 가장 적절한 형식을 동적으로 결정할 수 있습니다. 적절한 형식을 결정하는 데 지원되는 방법은 자동 형식 지정과 명시적 형식 지정, 두 가지가 있습니다.  
  
## <a name="automatic-formatting"></a>자동 서식 지정  
 자동 형식 지정을 사용하도록 설정하면 자동 형식 지정이 응답을 반환하는 가장 적절한 형식을 선택합니다. 자동 형식 지정은 다음을 순서대로 확인하여 가장 적절한 형식을 결정합니다.  
  
1. 요청 메시지의 Accept 헤더에 있는 미디어 유형  
  
2. 요청 메시지의 콘텐츠 형식  
  
3. 작업의 기본 형식 설정  
  
4. WebHttpBehavior의 기본 형식 설정  
  
 요청 메시지에 Accept 헤더를 포함 하는 경우 지원 되는 형식에 대 한 Windows Communication Foundation (WCF) 인프라를 검색 합니다. `Accept` 헤더가 해당 미디어 유형의 우선 순위를 지정하는 경우 이러한 우선 순위는 무시되지 않습니다. `Accept` 헤더에서 적절한 형식을 찾지 못할 경우 요청 메시지의 콘텐츠 형식이 사용됩니다. 적절한 콘텐츠 형식이 지정되지 않은 경우 작업의 기본 형식 설정이 사용됩니다. 기본 형식은 `ResponseFormat` 및 <xref:System.ServiceModel.Web.WebGetAttribute> 특성의 <xref:System.ServiceModel.Web.WebInvokeAttribute> 매개 변수를 사용하여 설정됩니다. 작업의 기본 형식이 지정되지 않은 경우 <xref:System.ServiceModel.Description.WebHttpBehavior.DefaultOutgoingResponseFormat%2A> 속성의 값이 사용됩니다. 자동 형식은 <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> 속성에 의해 결정됩니다. 이 속성이 `true`로 설정되면 WCF 인프라가 사용할 가장 적절한 형식을 결정합니다. 기본적으로 자동 형식 선택은 이전 버전과의 호환성을 위해 사용되지 않습니다. 자동 형식 선택은 프로그래밍 방식이나 구성을 통해 사용하도록 설정할 수 있습니다. 다음 예제에서는 코드에서 자동 형식 선택을 사용하도록 설정하는 방법을 보여 줍니다.  
  
```csharp
// This code assumes the service name is MyService and the service contract is IMyContract     
Uri baseAddress = new Uri("http://localhost:8000");  
  
WebServiceHost host = new WebServiceHost(typeof(MyService), baseAddress)  
try  
{  
   ServiceEndpoint sep = host.AddServiceEndpoint(typeof(IMyContract), new WebHttpBinding(), "");  
   // Check it see if the WebHttpBehavior already exists  
   WebHttpBehavior whb = sep.Behaviors.Find<WebHttpBehavior>();  
  
   if (whb != null)  
   {  
      whb.AutomaticFormatSelectionEnabled = true;  
   }  
   else  
   {  
      WebHttpBehavior webBehavior = new WebHttpBehavior();  
      webBehavior.AutomaticFormatSelectionEnabled = true;  
      sep.Behaviors.Add(webBehavior);  
   }  
         // Open host to start listening for messages  
   host.Open();        
  
  // ...  
}  
  catch(CommunicationException ex)  
  {  
     Console.WriteLine("An exception occurred: " + ex.Message());  
  }  
```  
  
 구성을 통해 자동 형식 지정을 사용하도록 설정할 수도 있습니다. <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> 속성을 <xref:System.ServiceModel.Description.WebHttpBehavior>에 직접 설정하거나 <xref:System.ServiceModel.Description.WebHttpEndpoint>를 사용하여 설정할 수 있습니다. 다음 예제에서는 <xref:System.ServiceModel.Description.WebHttpBehavior>에서 자동 형식 선택을 사용하도록 설정하는 방법을 보여 줍니다.  
  
```xml  
<system.serviceModel>  
  <behaviors>  
    <endpointBehaviors>  
      <behavior>  
        <webHttp automaticFormatSelectionEnabled="true" />  
      </behavior>  
    </endpointBehaviors>  
  </behaviors>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
      <standardEndpoint name="" helpEnabled="true" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 다음 예제에서는 <xref:System.ServiceModel.Description.WebHttpEndpoint>를 사용하여 자동 형식 선택을 사용하도록 설정하는 방법을 보여 줍니다.  
  
```xml  
<system.serviceModel>  
    <standardEndpoints>  
      <webHttpEndpoint>  
        <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
        <standardEndpoint name="" helpEnabled="true" automaticFormatSelectionEnabled="true"  />  
      </webHttpEndpoint>  
    </standardEndpoints>  
  </system.serviceModel>  
```  
  
## <a name="explicit-formatting"></a>명시적 형식 지정  
 이름에서 알 수 있듯이 명시적 형식 지정에서는 개발자가 작업 코드 내에서 사용할 가장 적절한 형식을 결정합니다. 가장 적절한 형식이 XML 또는 JSON이면 개발자는 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> 을 <xref:System.ServiceModel.Web.WebMessageFormat.Xml> 또는 <xref:System.ServiceModel.Web.WebMessageFormat.Json>으로 설정합니다. <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> 속성이 명시적으로 설정되지 않으면 작업의 기본 형식이 사용됩니다.  
  
 다음 예제에서는 사용할 형식에 대한 형식 쿼리 문자열 매개 변수를 확인합니다. 이 매개 변수가 지정되어 있으면 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A>을 사용하여 작업의 형식이 설정됩니다.  
  
```csharp
public class Service : IService  
{  
    [WebGet]  
     public string EchoWithGet(string s)  
    {  
        // if a format query string parameter has been specified, set the response format to that. If no such
        // query string parameter exists the Accept header will be used
        string formatQueryStringValue = WebOperationContext.Current.IncomingRequest.UriTemplateMatch.QueryParameters["format"];  
        if (!string.IsNullOrEmpty(formatQueryStringValue))  
        {  
            if (formatQueryStringValue.Equals("xml", System.StringComparison.OrdinalIgnoreCase))  
            {
                WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Xml;
            }
            else if (formatQueryStringValue.Equals("json", System.StringComparison.OrdinalIgnoreCase))  
            {  
                WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Json;  
            }  
            else  
            {  
                throw new WebFaultException<string>($"Unsupported format '{formatQueryStringValue}'",   HttpStatusCode.BadRequest);
            }  
        }  
        return "You said " + s;  
    }  
```  
  
 XML 또는 JSON 이외의 다른 형식을 지원해야 하는 경우 반환 형식이 <xref:System.ServiceModel.Channels.Message>인 작업을 정의합니다. 작업 코드 내에서 사용할 적절한 형식을 결정하고 다음 메서드 중 하나를 사용하여 <xref:System.ServiceModel.Channels.Message> 개체를 만듭니다.  
  
- `WebOperationContext.CreateAtom10Response`  
  
- `WebOperationContext.CreateJsonResponse`  
  
- `WebOperationContext.CreateStreamResponse`  
  
- `WebOperationContext.CreateTextResponse`  
  
- `WebOperationContext.CreateXmlResponse`  
  
 이러한 각 메서드는 콘텐츠를 사용하여 적절한 형식의 메시지를 만듭니다. `WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements` 메서드를 사용하면 선호도가 높은 것부터 낮은 것 순으로 클라이언트가 선호하는 형식의 목록을 가져올 수 있습니다. 다음 예제에서는 `WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements`를 사용하여 사용할 형식을 결정한 다음 적절한 응답 만들기 메서드를 사용하여 응답 메시지를 만드는 방법을 보여 줍니다.  
  
```csharp
public class Service : IService  
{  
    public Message EchoListWithGet(string list)  
    {  
        List<string> returnList = new List<string>(list.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries));  
        IList<ContentType> acceptHeaderElements = WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements();  
        for (int x = 0; x < acceptHeaderElements.Count; x++)  
        {  
            string normalizedMediaType = acceptHeaderElements[x].MediaType.ToLowerInvariant();  
            switch (normalizedMediaType)  
            {  
                case "image/jpeg": return CreateJpegResponse(returnList);  
                case "application/xhtml+xml": return CreateXhtmlResponse(returnList);  
                case "application/atom+xml": return CreateAtom10Response(returnList);  
                case "application/xml": return CreateXmlResponse(returnList);  
                case "application/json": return CreateJsonResponse(returnList);  
          }  
    }  
  
    // Default response format is XML  
    return CreateXmlResponse(returnList);  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.UriTemplate>
- <xref:System.UriTemplateMatch>
- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
- [UriTemplate 및 UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)
- [WCF 웹 HTTP 프로그래밍 모델 개요](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)
- [WCF 웹 HTTP 프로그래밍 개체 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)
