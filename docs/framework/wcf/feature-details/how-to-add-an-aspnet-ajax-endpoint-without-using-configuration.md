---
title: '방법: 구성을 사용하지 않고 ASP.NET AJAX 엔드포인트 추가'
ms.date: 03/30/2017
ms.assetid: b05c1742-8d0a-4673-9d71-725b18a3008e
ms.openlocfilehash: 4a7ff48e529ab58c8744edea22d52ad12a4d7b96
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895083"
---
# <a name="how-to-add-an-aspnet-ajax-endpoint-without-using-configuration"></a>방법: 구성을 사용하지 않고 ASP.NET AJAX 엔드포인트 추가
WCF (Windows Communication Foundation)를 사용 하면 클라이언트 웹 사이트의 JavaScript에서 호출할 수 있는 ASP.NET AJAX 사용 끝점을 노출 하는 서비스를 만들 수 있습니다. 이와 같은 엔드포인트를 만들려면 다른 모든 WCF 엔드포인트에서처럼 구성 파일을 사용하거나 구성 요소가 필요하지 않은 메서드를 사용할 수 있습니다. 이 항목에서는 두 번째 접근 방법을 보여 줍니다.  
  
 구성 없이 ASP.NET AJAX 엔드포인트를 사용하여 서비스를 만들려면 서비스는 IIS(인터넷 정보 서비스)에 의해 호스팅되어야 합니다. 이 접근 방식을 사용 하 여 ASP.NET AJAX 끝점을 활성화 하려면 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> .svc 파일의 [ \@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) 지시문에서를 팩터리 매개 변수로 지정 합니다. 이 사용자 지정 팩터리는 클라이언트 웹 사이트의 JavaScript에서 호출할 수 있도록 ASP.NET AJAX 엔드포인트를 자동으로 구성하는 구성 요소입니다.  
  
 작업 예제는 [구성 없이 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-without-configuration.md)를 참조 하세요.  
  
 구성 요소를 사용 하 여 ASP.NET AJAX 끝점을 [구성 하는 방법에 대 한 개요는 방법: 구성을 사용 하 여 ASP.NET AJAX 끝점](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)을 추가 합니다.  
  
### <a name="to-create-a-basic-wcf-service"></a>기본 WCF 서비스를 만들려면  
  
1. <xref:System.ServiceModel.ServiceContractAttribute> 특성으로 표시 된 인터페이스를 사용 하 여 기본 WCF 서비스 계약을 정의 합니다. 각 작업을 <xref:System.ServiceModel.OperationContractAttribute>로 표시합니다. <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 속성을 설정해야 합니다.  
  
    ```csharp  
    [ServiceContract(Namespace = "MyService")]]  
    public interface ICalculator  
    {  
        [OperationContract]  
        // This operation returns the sum of d1 and d2.  
        double Add(double n1, double n2);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2. `ICalculator`를 사용하여 `CalculatorService` 서비스 계약을 구현합니다.  
  
    ```csharp  
    public class CalculatorService : ICalculator  
    {  
        public double Add(double n1, double n2)  
        {  
            return n1 + n2;  
        }  
  
    //Other operations omitted…  
    ```  
  
3. 네임스페이스 블록에 `ICalculator` 및 `CalculatorService` 구현을 래핑하여 이러한 구현에 대한 네임스페이스를 정의합니다.  
  
    ```csharp  
    Namespace Microsoft.Ajax.Samples  
    {  
        //Include the code for ICalculator and Caculator here.  
    }  
    ```  
  
### <a name="to-host-the-service-in-internet-information-services-without-configuration"></a>구성 없이 인터넷 정보 서비스에서 서비스를 호스팅하려면  
  
1. 애플리케이션에서 .svc 확장명이 있는 service라는 새 파일을 만듭니다. 서비스에 대 한 적절 한 [ \@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) 지시문 정보를 추가 하 여이 파일을 편집 합니다. ASP.NET AJAX 끝점 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 을 자동으로 구성 하기 위해 [ \@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) 지시문에서를 사용 하도록 지정 합니다.  
  
    ```text
    <%@ServiceHost   
        language=c#   
        Debug="true"   
        Service="Microsoft.Ajax.Samples.CalculatorService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
2. 서비스를 빌드하고 클라이언트에서 호출합니다. 호출하면 IIS(인터넷 정보 서비스)가 해당 서비스를 활성화합니다. IIS에서 호스트 [하는 방법에 대 한 자세한 내용은 방법: IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)에서 WCF 서비스를 호스팅합니다.  
  
### <a name="to-call-the-service"></a>서비스를 호출하려면  
  
1. 끝점은 .svc 파일을 기준으로 하는 빈 주소에 구성 되어 있으므로 서비스를 사용할 수 있으며, 서비스에\< `Add` 대 한 요청을 전송 하 여 호출할 수 있습니다. .svc/operation >-예를 들어 작업에 대 한 서비스를 추가 합니다. 서비스 URL을 ASP.NET AJAX Script Manager 컨트롤의 스크립트 컬렉션에 입력하여 사용할 수 있습니다. 예제는 [구성 없이 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-without-configuration.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
  
 자동으로 구성된 엔드포인트는 기본 URL을 기준으로 비어 있는 주소에 생성됩니다. 또한 구성 파일을 추가하여 이 접근 방법으로 사용할 수 있습니다. 구성 파일에 엔드포인트 정의가 포함된 경우 이러한 엔드포인트는 자동으로 구성된 엔드포인트에 추가됩니다.  
  
 예를 들어, service.svc는 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>를 사용하고 서비스 디렉터리에는 "soap" 상대 주소에서 <xref:System.ServiceModel.BasicHttpBinding>을 사용하여 동일한 서비스에 대해 엔드포인트를 정의하는 Web.config 파일이 포함되어 있습니다. 이 경우 서비스는 두 개의 엔드포인트를 포함합니다. 한 엔드포인트는 ASP.NET AJAX 요청에 응답하는 service.svc에 위치하고 다른 엔드포인트는 SOAP 요청에 응답하는 service.svc/soap에 위치합니다.  
  
 구성 파일이 비어 있는 상대 주소에 엔드포인트를 정의하고 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>가 사용되는 경우 예외가 throw되어 서비스를 시작할 수 없습니다.  
  
 구성을 사용하여 자동으로 구성된 엔드포인트에서 설정을 수정할 수 없습니다. 판독기 할당량과 같은 설정을 수정해야 하는 경우 .svc 파일에서 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>를 제거하고 엔드포인트에 대한 구성 항목을 만들어 구성을 사용하지 않는 접근 방법을 사용하지 말아야 합니다.  
  
 서비스를 사용하려면 ASP.NET 호환 모드가 필요합니다. 예를 들어, <xref:System.Web.HttpContext> 클래스 또는 ASP.NET 인증 메커니즘을 사용하는 경우 이 모드를 사용하도록 설정하려면 구성 파일이 필요합니다. 필요한 구성 요소는 [ serviceHostingEnvironment>요소이며다음과같이추가해야합니다.\<](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)  
  
 `<system.serviceModel>`  
  
 `<serviceHostingEnvironment aspNetCompatibilityEnabled="true" /> </system.serviceModel>`  
  
 자세한 내용은 [WCF 서비스 및 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md) 항목을 참조 하세요.  
  
 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 클래스가 <xref:System.ServiceModel.Activation.ServiceHostFactory>의 파생 클래스인 경우 서비스 호스트 팩터리 메커니즘에 대 한 자세한 설명은 [ServiceHostFactory을 사용 하 여 호스팅 확장](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md) 항목을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [ASP.NET AJAX용 WCF 서비스 만들기](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)
- [방법: AJAX를 사용 하는 ASP.NET 웹 서비스를 WCF로 마이그레이션](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)
