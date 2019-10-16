---
title: ASP.NET AJAX용 WCF 서비스 만들기
ms.date: 03/30/2017
ms.assetid: 04c0402c-e617-4ba5-aedf-d17692234776
ms.openlocfilehash: 64be5c8ec0d3ee105e026794912a9820bd7892d0
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045958"
---
# <a name="creating-wcf-services-for-aspnet-ajax"></a>ASP.NET AJAX용 WCF 서비스 만들기

Microsoft ASP.NET AJAX를 사용하면 응답성이 높고 친숙한 사용자 인터페이스 요소를 통해 풍부한 사용자 경험을 제공하는 웹 페이지를 빠르게 만들 수 있습니다. ASP.NET AJAX는 크로스 브라우저 ECMAScript(JavaScript) 및 DHTML(동적 HTML) 기술을 통합하는 클라이언트 스크립트 라이브러리를 제공하며 ASP.NET 2.0 서버 기반 개발 플랫폼과 통합됩니다. ASP.NET AJAX를 사용하여 사용자 환경 및 웹 애플리케이션의 효율성을 개선할 수 있습니다.

ASP.NET AJAX는 강력한 개발 프레임워크를 제공하기 위해 통합된 서버 구성 요소와 클라이언트 스크립트 라이브러리로 구성됩니다. ASP.NET 페이지에서 서비스에 액세스하려는 경우 일단, 서비스 URL을 페이지의 ASP.NET 스크립트 관리자 컨트롤에 추가하면 일반 JavaScript 기능 호출과 똑같은 JavaScript 코드를 사용하여 서비스 작업을 호출할 수 있습니다. AJAX 프레임 워크 내에서 웹 서비스 사용에 대 한 [ASP.NET Ajax 알아보기](https://go.microsoft.com/fwlink/?LinkId=186475) 를 참조 하세요.

가장 Windows Communication Foundation (WCF) 서비스는 적절 한 ASP.NET AJAX 끝점을 추가 하 여 ASP.NET AJAX와 호환 되는 서비스로 노출 될 수 있습니다.

Visual Studio를 사용 하는 경우 ASP.NET 웹 사이트 또는 웹 응용 프로그램으로 작업할 때 **새 항목 추가** 대화 상자에서 사용할 수 있는 AJAX 사용 WCF 서비스에 대해 미리 작성 된 템플릿을 사용할 수 있습니다.

Visual Studio 템플릿을 사용하지 않는 경우 다음 두 가지 방법으로 ASP.NET AJAX 엔드포인트를 만듭니다.

- 구성을 사용하지 않고 동적 호스트 활성화를 사용하여 엔드포인트를 만듭니다. 이 방법은 WCF 구성 시스템에 익숙하지 않은 경우 사용할 수 있는 가장 기본적인 방법입니다. 자세한 내용은 [방법: 구성을](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)사용 하지 않고 ASP.NET AJAX 끝점을 추가 합니다.

- 구성을 사용 하 여 WCF 서비스에 AJAX 사용 끝점을 추가 합니다. 자세한 내용은 [방법: 구성을 사용 하 여 ASP.NET AJAX 끝점](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)을 추가 합니다.

[WCF 웹 HTTP 프로그래밍 모델 개요](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md) 에 설명 된 웹 프로그래밍 모델은 ASP.NET AJAX 서비스와 함께 사용할 수 있습니다. 구체적으로는 다음과 같습니다.

- <xref:System.ServiceModel.Web.WebGetAttribute> 및 <xref:System.ServiceModel.Web.WebInvokeAttribute> 특성을 사용하여 HTTP GET 및 HTTP POST 동사 중에서 선택할 수 있습니다. 이 기능을 올바르게 사용하면 애플리케이션의 성능이 크게 향상될 수 있습니다. 자세한 내용은 [방법: ASP.NET AJAX 끝점](../../../../docs/framework/wcf/feature-details/http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md)에 대 한 HTTP POST 및 http GET 요청 중에서 선택 합니다.

- <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> 및 <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> 속성을 사용하여 서비스에서 기본 JSON(JavaScript Object Notation) 대신 XML 데이터를 반환하도록 설정할 수 있습니다. ASP.NET AJAX 프레임워크를 사용하여 이 작업을 수행하면 JavaScript 클라이언트가 XML DOM 개체를 받게 됩니다.

  > [!WARNING]
  > 이 작업을 수행하려면 콘텐츠 형식을 text/xml로 설정해야 합니다. 그렇지 않으면 JavaScript 클라이언트가 XML DOM 개체 대신 XML이 들어 있는 문자열을 받게 됩니다.

    다음은 콘텐츠 형식이 적절하게 설정된 XML 데이터를 반환하는 작업의 예제입니다.

  ```csharp
  [OperationContract, WebGet(ResponseFormat=WebMessageFormat.Xml)]
  public XElement GetData()
  {
      XElement x;
      //Get some data here...

      WebOperationContext.Current.OutgoingResponse.ContentType = "text/xml";
      return x;
  }
  ```

- ASP.NET AJAX와의 호환성이 필요한 경우에는 <xref:System.ServiceModel.Web.WebGetAttribute> 및 <xref:System.ServiceModel.Web.WebInvokeAttribute> 특성의 다른 속성을 변경할 수 없습니다. ASP.NET AJAX 호출 규칙을 위반하지 않는 한 웹 프로그래밍 모델의 다른 부분을 사용할 수 있습니다.

 고급 시나리오의 경우 WCF의 AJAX 지원에 대 한 추가 정보를 이해 해야 합니다.

- JavaScript를 사용 하 여 AJAX 페이지 클라이언트와 WCF 서비스 간에 데이터를 전송 하는 방법을 이해 하 고 .NET Framework 형식이 JavaScript 형식에 매핑되는 방법에 대 한 자세한 내용은 [JSON 및 기타 데이터 전송 형식에 대 한 지원](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md)을 참조 하세요.

- URL 기반 인증 및 ASP.NET 세션 정보 액세스 등 ASP.NET 기능을 사용하려면 구성을 통해 ASP.NET 호환 모드를 활성화하는 것이 좋습니다.

WCF의 AJAX 끝점은 ASP.NET AJAX 프레임 워크 없이도 사용 될 수 있습니다. 이렇게 하려면 WCF에서 AJAX 지원의 지원 아키텍처를 이해 해야 합니다. 이 아키텍처에 대 한 자세한 내용은 [WCF 웹 HTTP 프로그래밍 개체 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)을 참조 하세요. 이 방법을 보여 주는 코드 샘플은 [JSON 및 XML을 사용 하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md)를 참조 하세요.

## <a name="see-also"></a>참고자료

- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
- [방법: 구성을 사용 하지 않고 ASP.NET AJAX 끝점 추가](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)
- [방법: 구성을 사용 하 여 ASP.NET AJAX 끝점 추가](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)
- [방법: ASP.NET AJAX 끝점에 대 한 HTTP POST 및 HTTP GET 요청 중에서 선택](../../../../docs/framework/wcf/feature-details/http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md)
