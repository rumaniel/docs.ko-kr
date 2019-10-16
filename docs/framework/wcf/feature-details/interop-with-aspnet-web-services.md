---
title: ASP.NET 웹 서비스와의 상호 운용성
ms.date: 03/30/2017
ms.assetid: 622422f8-6651-442f-b8be-e654a4aabcac
ms.openlocfilehash: 59ee6412cde152588e8007fe530cc8e5708410e5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991526"
---
# <a name="interoperability-with-aspnet-web-services"></a>ASP.NET 웹 서비스와의 상호 운용성
두 기술을 사용 하 여 구현 된 서비스가 WS-I Basic Profile 1.1 사양을 준수 하도록 하 여 WCF (ASP.NET Web services and Windows Communication Foundation) 웹 서비스 간의 상호 운용성을 실현할 수 있습니다. WS-I Basic Profile 1.1을 준수 하는 ASP.NET 웹 서비스는 WCF 시스템 제공 바인딩를 <xref:System.ServiceModel.BasicHttpBinding>사용 하 여 wcf 클라이언트와 상호 운용할 수 있습니다.  
  
 다음 샘플 코드에 표시 된 것 <xref:System.Web.Services.WebService> 처럼 <xref:System.Web.Services.WebMethodAttribute> , 클래스 대신 인터페이스에 및 특성을 추가 하 고 인터페이스를 구현 하는 클래스를 작성 하는 ASP.NET 2.0 옵션을 사용 합니다.  
  
```csharp
[WebService]  
public interface IEcho  
{  
    [WebMethod]  
    string Echo(string input);  
}  
  
public class Service : IEcho  
{  
  
   public string Echo(string input)  
   {  
        return input;  
    }  
}  
```  
  
 <xref:System.Web.Services.WebService> 특성을 가진 인터페이스는 서비스에 의해 수행되는 작업에 대한 계약을 구성하며, 같은 계약을 다른 방식으로 구현하는 다양한 클래스에서 이 서비스를 다시 사용할 수 있으므로 이 옵션을 사용하는 것이 좋습니다.  
  
 <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> HTTP 헤더가 아닌 SOAP 메시지 본문 요소의 정규화된 이름을 기반으로 메서드로 메시지를 라우팅하려면 `SOAPAction` 특성을 사용하지 마십시오. WCF는 메시지 `SOAPAction` 를 라우팅하는 데 HTTP 헤더를 사용 합니다.  
  
 <xref:System.Xml.Serialization.XmlSerializer>에서 기본적으로 형식을 serialize하는 XML은 해당 XML에 대한 네임스페이스가 명시적으로 정의되어 있는 경우 <xref:System.Runtime.Serialization.DataContractSerializer>에서 형식을 serialize하는 XML과 의미상 동일합니다. WCF를 채택 하는 것에 대비 하 여 ASP.NET 웹 서비스에서 사용할 데이터 형식을 정의 하는 경우 다음을 수행 합니다.  
  
- XML 스키마가 아닌 .NET Framework 클래스를 사용하여 형식을 정의합니다.  
  
- 클래스에는 <xref:System.SerializableAttribute> 및 <xref:System.Xml.Serialization.XmlRootAttribute>만 추가하며, 형식에 대한 네임스페이스를 명시적으로 정의하려면 후자를 사용합니다. .NET Framework 클래스를 XML로 변환하는 방법을 제어하려면 <xref:System.Xml.Serialization> 네임스페이스로부터 특성을 추가하지 마십시오.  
  
- 이 방법을 채택하면 전송을 위해 클래스가 serialize되도록 XML을 크게 변경하지 않고 나중에 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute>를 추가하여 .NET 클래스를 데이터 계약으로 만들 수 있습니다. ASP.NET 웹 서비스에서 메시지에 사용 되는 형식은 WCF 응용 프로그램에 의해 데이터 계약으로 처리 될 수 있으며,이에 따라 WCF 응용 프로그램의 성능이 향상 되는 이점이 있습니다.  
  
 IIS(인터넷 정보 서비스)에서 제공하는 인증 옵션은 사용하지 마십시오. WCF 클라이언트는 이러한 기능을 지원 하지 않습니다. 서비스의 보안을 유지 해야 하는 경우에는 WCF에서 제공 하는 옵션을 사용 합니다. 이러한 옵션은 강력 하며 표준 프로토콜을 기반으로 하기 때문입니다.  
  
## <a name="performance-impact-caused-by-loading-the-servicemodel-httpmodule"></a>ServiceModel HttpModule 로드에 의한 성능 영향  
 .NET Framework 3.0의 경우 WCF `HttpModule`은 모든 ASP.NET 애플리케이션에서 WCF를 사용할 수 있도록 루트 Web.config 파일에 설치되어 있습니다. 이는 성능에 영향을 줄 수 있기 때문에 다음 예제에서처럼 Web.config 파일에 대해 `ServiceModel`을 제거할 수 있습니다.  
  
```xml  
<httpModules>  
    <remove name="ServiceModel" />  
<httpModules/>  
```  
  
## <a name="see-also"></a>참고자료

- [방법: ASP.NET 웹 서비스 클라이언트와 상호 운용 하도록 WCF 서비스 구성](../../../../docs/framework/wcf/feature-details/config-wcf-service-with-aspnet-web-service.md)
