---
title: 'Windows Communication Foundation 채택에 대한 기대: 향후 마이그레이션 간소화'
ms.date: 03/30/2017
ms.assetid: f49664d9-e9e0-425c-a259-93f0a569d01b
ms.openlocfilehash: 09bbb11c58992f0fabcb822f5f3d88fef273bea9
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425280"
---
# <a name="anticipating-adopting-the-windows-communication-foundation-easing-future-migration"></a>Windows Communication Foundation 채택에 대한 기대: 향후 마이그레이션 간소화
새 ASP.NET 응용 프로그램을 WCF의 향후 마이그레이션이 원활 해지 되도록 앞에서 설명한 권장 뿐만 아니라 다음 권장 사항을 따릅니다.  
  
## <a name="protocols"></a>프로토콜  
 SOAP 1.2에 대한 ASP.NET 2.0 지원을 사용하지 않습니다.  
  
```xml  
<configuration>  
     <system.web>  
      <webServices >  
          <protocols>  
           <remove name="HttpSoap12"/>  
          </protocols>    
      </webServices>  
     </system.web>   
</configuration>  
```  
  
 WCF 메시지 SOAP 1.1과 SOAP 1.2 처럼 서로 다른 프로토콜을 따르는 다양 한 끝점을 사용 하 여 이동할 필요 하기 때문에 이렇게 것이 좋습니다. ASP.NET 2.0 웹 서비스는 SOAP 1.1과 SOAP 1.2 될 수 없습니다. 기본 구성으로가 모두를 지원 하도록 구성 되어 확실히 수는 원래 주소의 단일 WCF 끝점으로 전달 마이그레이션된 경우 ASP.NET web 모든 호환 되어야 서비스의 기존 클라이언트입니다. 또한 SOAP 1.1 대신 1.2를 선택하면 서비스의 클라이언트가 보다 엄격하게 제한됩니다.  
  
## <a name="service-development"></a>서비스 개발  
 WCF를 사용 하면 적용 하 여 서비스 계약을 정의 하는 <xref:System.ServiceModel.ServiceContractAttribute> 인터페이스 또는 클래스. 이 특성을 인터페이스에 적용하면 원하는 수의 클래스에서 다양하게 구현할 수 있는 계약의 정의가 생성되므로 클래스보다는 인터페이스에 적용하는 것이 좋습니다. ASP.NET 2.0은 클래스뿐만 아니라 인터페이스에도 <xref:System.Web.Services.WebService> 특성을 적용하는 옵션을 지원합니다. 그러나 이미 설명했듯이 ASP.NET 2.0에는 <xref:System.Web.Services.WebService> 특성이 클래스가 아닌 인터페이스에 적용될 경우 이 특성의 Namespace 매개 변수가 아무런 효과가 없다는 결점이 있습니다. 기본값에서 서비스의 네임 스페이스를 수정 하는 것이 일반적으로 좋습니다 이므로 `http://tempuri.org`의 Namespace 매개 변수를 사용 합니다 <xref:System.Web.Services.WebService> 특성을 적용 하 여 ASP.NET 웹 서비스 정의 계속 해야 하나는 <xref:System.ServiceModel.ServiceContractAttribute> 인터페이스 또는 클래스에 특성입니다.  
  
- 이러한 인터페이스를 정의하는 메서드에 코드를 가능한 한 적게 사용합니다. 메서드의 작업을 다른 클래스에 위임하도록 합니다. 새 WCF 서비스 유형 다음 위임할 수도 클래스에는 상당한 작업입니다.  
  
- `MessageName`의 <xref:System.Web.Services.WebMethodAttribute> 매개 변수를 사용하여 서비스 작업에 명시적 이름을 제공합니다.  
  
    ```csharp  
    [WebMethod(MessageName="ExplicitName")]  
    string Echo(string input);  
    ```  
  
     ASP.NET에서 작업에 대 한 기본 이름을 WCF에서 제공 된 기본 이름과에서 다르기 때문에 이렇게 하는 것이 중요 합니다. 명시적 이름을 제공함으로써 기본 이름을 사용하지 않아도 됩니다.  
  
- WCF의 다형적 메서드를 사용 하 여 구현 작업을 지원 하지 않으므로 다형 메서드로 ASP.NET 웹 서비스 작업을 구현 하지 않습니다.  
  
- <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute>를 사용하여 HTTP 요청을 메서드로 라우트할 SOAPAction HTTP 헤더에 명시적 값을 제공합니다.  
  
    ```csharp  
    [WebMethod]  
    [SoapDocumentMethod(RequestElementName="ExplicitAction")]  
    string Echo(string input);  
    ```  
  
     이 접근 방식을 ASP.NET 및 WCF는 동일한 사용 된 SOAPAction 값을 기본값에 의존 하지 우회 됩니다.  
  
- SOAP 확장을 사용하지 마세요. SOAP 확장이 필요한 경우 목적이 있는 것으로 간주 되는 WCF에서 이미 제공 하는 기능 인지 확인 합니다. 실제로 이것이 경우 당장은 바로 WCF를 채택 하지.  
  
## <a name="state-management"></a>상태 관리  
 서비스의 상태를 유지하지 마세요. 응용 프로그램의 확장성을 떨어뜨리는 경향이 상태를 유지 하는 할 뿐만 아니라 WCF는 ASP.NET 호환 모드에서 ASP.NET 메커니즘을 지원 하지만 ASP.NET 및 WCF의 상태 관리 메커니즘은 매우 다릅니다.  
  
## <a name="exception-handling"></a>예외 처리  
 서비스에서 보내고 받을 데이터 형식의 구조를 디자인할 때 클라이언트로 전달하려는 서비스에서 발생할 수 있는 다양한 종류의 예외를 표시하기 위한 구조도 디자인합니다.  
  
```csharp  
[Serializable]  
[XmlRoot(Namespace="ExplicitNamespace", IsNullable=true)]  
public partial class AnticipatedException 
{ 
    private string anticipatedExceptionInformationField;  

    public string AnticipatedExceptionInformation 
    {  
        get {   
            return this.anticipatedExceptionInformationField;  
        }  
        set {  
            this.anticipatedExceptionInformationField = value;  
        }  
    }  
}  
```  
  
 다음과 같이 해당 클래스에 자신을 XML로 serialize할 수 있는 기능을 부여합니다.  
  
```csharp  
public XmlNode ToXML()  
{  
     XmlSerializer serializer = new XmlSerializer(  
      typeof(AnticipatedException));  
     MemoryStream memoryStream = new MemoryStream();  
     XmlTextWriter writer = new XmlTextWriter(  
     memoryStream, UnicodeEncoding.UTF8);  
     serializer.Serialize(writer, this);  
     XmlDocument document = new XmlDocument();  
     document.LoadXml(new string(  
     UnicodeEncoding.UTF8.GetChars(  
     memoryStream.GetBuffer())).Trim());  
    return document.DocumentElement;  
}  
```  
  
 그러면 해당 클래스를 사용하여 명시적으로 throw된 <xref:System.Web.Services.Protocols.SoapException> 인스턴스에 대한 자세한 정보를 제공할 수 있습니다.  
  
```csharp  
AnticipatedException exception = new AnticipatedException();  
exception.AnticipatedExceptionInformation = "…";  
throw new SoapException(  
     "Fault occurred",  
     SoapException.ClientFaultCode,  
     Context.Request.Url.AbsoluteUri,  
     exception.ToXML());  
```  
  
 이러한 예외 클래스는 WCF를 사용 하 여 쉽게 다시 사용할 <xref:System.ServiceModel.FaultException%601> 새 시키려면 클래스 `FaultException<AnticipatedException>(anticipatedException);`  
  
## <a name="security"></a>보안  
 다음은 몇 가지 보안 권장 사항입니다.  
  
- 방지 ASP.NET 2.0 프로필을 사용 하 여 사용이 제한 됩니다 ASP.NET 통합 모드의 경우 서비스를 WCF로 마이그레이션 했습니다.  
  
- Acl을 사용 하 여 ASP.NET 웹 서비스에서는 인터넷 정보 서비스 (IIS)를 사용 하 여 Acl 서비스에 대 한 액세스를 제어 하려면 방지, WCF 않습니다-ASP.NET 웹 서비스는 IIS 호스팅의 경우 이므로 WCF는 반드시 IIS에서 호스트할 필요가 없습니다.  
  
- 서비스 리소스에 대한 액세스 권한을 부여할 때 ASP.NET 2.0 역할 공급자를 사용할 것을 고려해 보세요.  
  
## <a name="see-also"></a>참고자료

- [Windows Communication Foundation 채택 예상: 향후 통합 간소화](../../../../docs/framework/wcf/feature-details/anticipating-adopting-the-wcf-easing-future-integration.md)
