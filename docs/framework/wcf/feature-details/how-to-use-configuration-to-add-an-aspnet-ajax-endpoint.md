---
title: '방법: 구성을 사용하여 ASP.NET AJAX 엔드포인트 추가'
ms.date: 03/30/2017
ms.assetid: 7cd0099e-dc3a-47e4-a38c-6e10f997f6ea
ms.openlocfilehash: 33f99161034db2aa142a422139406a1a68d42b2c
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972271"
---
# <a name="how-to-use-configuration-to-add-an-aspnet-ajax-endpoint"></a>방법: 구성을 사용하여 ASP.NET AJAX 엔드포인트 추가
WCF (Windows Communication Foundation)를 사용 하면 클라이언트 웹 사이트의 JavaScript에서 호출할 수 있는 ASP.NET AJAX 사용 끝점을 사용할 수 있도록 하는 서비스를 만들 수 있습니다. 이러한 끝점을 만들려면 다른 모든 WCF (Windows Communication Foundation) 끝점과 마찬가지로 구성 파일을 사용 하거나 구성 요소가 필요 하지 않은 메서드를 사용할 수 있습니다. 이 항목에서는 구성 방법을 보여 줍니다.  
  
 서비스 끝점이 ASP.NET 될 수 있도록 하는 프로시저의 일부는를 사용 <xref:System.ServiceModel.WebHttpBinding> 하 고 [ \<enableWebScript >](../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md) 끝점 동작을 추가 하기 위해 끝점을 구성 하는 것으로 구성 됩니다. 끝점을 구성한 후 서비스를 구현 하 고 호스트 하는 단계는 모든 WCF 서비스에서 사용 하는 단계와 비슷합니다. 작업 예제는 [HTTP POST를 사용 하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)를 참조 하세요.  
  
 구성을 사용 하지 않고 ASP.NET AJAX 끝점을 구성 하는 방법에 대 한 자세한 [내용은 방법: 구성을](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)사용 하지 않고 ASP.NET AJAX 끝점을 추가 합니다.  
  
## <a name="to-create-a-basic-wcf-service"></a>기본 WCF 서비스를 만들려면  
  
1. <xref:System.ServiceModel.ServiceContractAttribute> 특성으로 표시 된 인터페이스를 사용 하 여 기본 WCF 서비스 계약을 정의 합니다. 각 작업을 <xref:System.ServiceModel.OperationContractAttribute>로 표시합니다. <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 속성을 설정해야 합니다.  
  
    ```csharp
    [ServiceContract(Namespace = "MyService")]  
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
    namespace Microsoft.Ajax.Samples  
    {  
        //Include the code for ICalculator and Caculator here.  
    }  
    ```  
  
## <a name="to-create-an-aspnet-ajax-endpoint-for-the-service"></a>서비스에 대한 ASP.NET AJAX 엔드포인트를 만들려면  
  
1. 동작 구성을 만들고 서비스의 ASP.NET AJAX 사용 끝점에 대 한 [ \<enableWebScript >](../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md) 동작을 지정 합니다.  
  
    ```xml  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="AspNetAjaxBehavior">  
                    <enableWebScript />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
    </system.serviceModel>  
    ```  
  
2. 이전 단계에서 정의한 <xref:System.ServiceModel.WebHttpBinding> 및 ASP.NET AJAX 동작을 사용하는 서비스에 대한 엔드포인트를 만듭니다.  
  
    ```xml  
    <system.serviceModel>  
        <services>  
            <service name="Microsoft.Ajax.Samples.CalculatorService">  
                <endpoint address=""  
                    behaviorConfiguration="AspNetAjaxBehavior"   
                    binding="webHttpBinding"  
                    contract="Microsoft.Ajax.Samples.ICalculator" />  
            </service>  
        </services>  
    </system.serviceModel>   
    ```  
  
## <a name="to-host-the-service-in-iis"></a>IIS에서 서비스를 호스팅하려면  
  
1. IIS에서 서비스를 호스팅하려면 애플리케이션에서 .svc 확장명을 가진 새 파일 서비스를 만듭니다. 서비스에 대 한 적절 한 [ \@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) 지시문 정보를 추가 하 여이 파일을 편집 합니다. 예를 들어 `CalculatorService` 샘플에 대한 서비스 파일의 내용에는 다음 정보가 포함되어 있습니다.  
  
    ```
    <%@ServiceHost   
    language=c#   
    Debug="true"   
    Service="Microsoft.Ajax.Samples.CalculatorService"  
    %>  
    ```  
  
2. IIS에서 호스트 [하는 방법에 대 한 자세한 내용은 방법: IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)에서 WCF 서비스를 호스팅합니다.  
  
## <a name="to-call-the-service"></a>서비스를 호출하려면  
  
1. 끝점은 .svc 파일을 기준으로 하는 빈 주소에 구성 되어 있으므로 서비스를 사용할 수 있으며, 서비스에\< `Add` 대 한 요청을 전송 하 여 호출할 수 있습니다. .svc/operation >-예를 들어 작업에 대 한 서비스를 추가 합니다. 엔드포인트 URL을 ASP.NET AJAX Script Manager 컨트롤의 스크립트 컬렉션에 입력하여 사용할 수 있습니다. 예제는 [HTTP POST를 사용 하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [ASP.NET AJAX용 WCF 서비스 만들기](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)
- [방법: AJAX를 사용 하는 ASP.NET 웹 서비스를 WCF로 마이그레이션](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)
