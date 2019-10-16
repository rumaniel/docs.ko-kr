---
title: WCF 웹 HTTP 프로그래밍 모델 개요
ms.date: 03/30/2017
ms.assetid: 381fdc3a-6e6c-4890-87fe-91cca6f4b476
ms.openlocfilehash: 8c13ad943bf4ef272c28266e12e175a0a21d5d40
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045239"
---
# <a name="wcf-web-http-programming-model-overview"></a>WCF 웹 HTTP 프로그래밍 모델 개요
WCF (Windows Communication Foundation) 웹 HTTP 프로그래밍 모델은 WCF를 사용 하 여 웹 HTTP 서비스를 빌드하는 데 필요한 기본 요소를 제공 합니다. WCF 웹 HTTP 서비스는 웹 브라우저를 포함 하 여 가능한 광범위 한 클라이언트에서 액세스할 수 있도록 설계 되었으며 다음과 같은 고유한 요구 사항이 있습니다.  
  
- Uri **및 Uri 처리** Uri는 웹 HTTP 서비스의 디자인에서 중앙 역할을 수행 합니다. WCF 웹 HTTP 프로그래밍 모델은 <xref:System.UriTemplate> 및 <xref:System.UriTemplateTable> 클래스를 사용 하 여 URI 처리 기능을 제공 합니다.  
  
- **GET 및 POST 작업 지원** 웹 HTTP 서비스는 데이터 수정 및 원격 호출에 대 한 다양 한 호출 동사 뿐만 아니라 데이터 검색에 GET 동사를 사용 합니다. WCF 웹 HTTP 프로그래밍 모델은 및 <xref:System.ServiceModel.Web.WebGetAttribute> <xref:System.ServiceModel.Web.WebInvokeAttribute> 를 사용 하 여 PUT, POST, DELETE 등의 GET 및 다른 HTTP 동사 둘 다에 서비스 작업을 연결 합니다.  
  
- **여러 데이터 형식** 웹 스타일 서비스는 SOAP 메시지 외에도 여러 종류의 데이터를 처리 합니다. WCF 웹 HTTP 프로그래밍 모델은 <xref:System.ServiceModel.WebHttpBinding> 및 <xref:System.ServiceModel.Description.WebHttpBehavior> 를 사용 하 여 XML 문서, JSON 데이터 개체 및 이미지, 비디오 파일, 일반 텍스트 등의 이진 콘텐츠 스트림을 비롯 한 다양 한 데이터 형식을 지원 합니다.  
  
 WCF 웹 HTTP 프로그래밍 모델은 웹 HTTP 서비스, AJAX 및 JSON 서비스 및 배포 (ATOM/RSS) 피드가 포함 된 웹 스타일 시나리오를 포함 하도록 WCF의 범위를 확장 합니다. AJAX 및 JSON 서비스에 대 한 자세한 내용은 [Ajax 통합 및 Json 지원](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)을 참조 하세요. 배포에 대 한 자세한 내용은 [WCF 배포 개요](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)를 참조 하세요.  
  
 WEB HTTP 서비스에서 반환될 수 있는 데이터 형식에 대한 추가 제한은 없습니다. 모든 직렬화 가능 형식이 WEB HTTP 서비스 작업에서 반환될 수 있습니다. 웹 브라우저가 WEB HTTP 서비스 작업을 호출할 수 있기 때문에 URL에 지정할 수 있는 데이터 형식에 대한 제한이 있습니다. 기본적으로 지원 되는 형식에 대 한 자세한 내용은 아래의 **UriTemplate 쿼리 문자열 매개 변수 및 url** 섹션을 참조 하십시오. URL에 지정된 매개 변수를 실제 매개 변수 형식으로 변환하는 방법을 지정하는 고유한 T:System.ServiceModel.Dispatcher.QueryStringConverter 구현을 제공하여 기본 동작을 변경할 수 있습니다. 자세한 내용은 <xref:System.ServiceModel.Dispatcher.QueryStringConverter>을 참조하세요.  
  
> [!CAUTION]
> WCF 웹 HTTP 프로그래밍 모델을 사용 하 여 작성 된 서비스는 SOAP 메시지를 사용 하지 않습니다. SOAP는 사용 되지 않으므로 WCF에서 제공 하는 보안 기능을 사용할 수 없습니다. 그러나 HTTPS를 사용하여 서비스를 호스트하면 전송 기반 보안을 사용할 수 있습니다. WCF 보안에 대 한 자세한 내용은 [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md) 를 참조 하세요.  
  
> [!WARNING]
> IIS의 WebDAV 확장을 설치하면 WebDAV 확장에서 모든 PUT 요청을 처리하려고 하므로 WEB HTTP 서비스에서 HTTP 405 오류를 반환할 수 있습니다. 이 문제를 해결하려면 WebDAV 확장을 제거하거나 웹 사이트에 대해 WebDAV 확장을 사용하지 않도록 설정할 수 있습니다. 자세한 내용은 [IIS 및 WebDav](https://learn.iis.net/page.aspx/357/webdav-for-iis-70/) 를 참조 하세요.  
  
## <a name="uri-processing-with-uritemplate-and-uritemplatetable"></a>UriTemplate 및 UriTemplateTable을 사용한 URI 처리  
 URI 템플릿은 구조적으로 비슷한 아주 많은 URI 집합을 나타내기 위한 효율적인 구문을 제공합니다. 예를 들면 다음 템플릿은 중간 세그먼트 값에 관계없이 "a"로 시작해서 "c"로 끝나는 세 개의 세그먼트로 구성된 URI 집합(a/{segment}/c)을 나타냅니다.  
  
 이 템플릿에서는 다음과 같은 URI를 설명합니다.  
  
- a/x/c  
  
- a/y/c  
  
- a/z/c  
  
- 등  
  
 이 템플릿에서 중괄호 표기법("{segment}")은 리터럴 값 대신 변수 세그먼트를 나타냅니다.  
  
 .NET Framework는 <xref:System.UriTemplate>이라는 URI 템플릿으로 작업하기 위한 API를 제공합니다. `UriTemplates`을 사용하여 다음 작업을 수행할 수 있습니다.  
  
- 매개 변수 집합을 사용 하 `Bind` 여 메서드 중 하나를 호출 하 여 템플릿과 일치 하는 *완전히 폐쇄형 URI* 를 생성할 수 있습니다. 즉, URI 템플릿 내에 있는 변수는 모두 실제 값으로 바뀝니다.  
  
- 후보 URI로 `Match`()를 호출할 수 있으며, 후보 URI는 템플릿을 사용하여 후보 URI를 구성 부분으로 나누고 템플릿의 변수에 따라 레이블이 지정된 URI의 다른 부분이 포함된 사전을 반환합니다.  
  
- `Bind`() 및 `Match`()는 서로가 반대이므로, 사용자는 `Match`(`Bind`( x ))를 호출하고 시작한 환경으로 돌아갈 수 있습니다.  
  
 대부분의 경우, 특히 URI를 기반으로 서비스 작업에 대한 요청을 디스패치해야 하는 서버에서는 포함된 각 템플릿을 독립적으로 처리할 수 있는 데이터 구조의 <xref:System.UriTemplate> 개체 집합을 추적할 수 있습니다. <xref:System.UriTemplateTable>은 URI 템플릿 집합을 나타내며 템플릿 집합과 후보 URI가 지정된 경우 가장 일치하는 항목을 선택합니다. 이는 특정 네트워킹 스택 (WCF 포함)과 관련이 없으므로 필요할 때마다 사용할 수 있습니다.  
  
 WCF 서비스 모델은 <xref:System.UriTemplate> 및 <xref:System.UriTemplateTable>을 사용하여, <xref:System.UriTemplate>에서 설명한 URI 집합과 서비스 작업을 연결합니다. 서비스 작업은 <xref:System.UriTemplate> 또는 <xref:System.ServiceModel.Web.WebGetAttribute>를 사용하여 <xref:System.ServiceModel.Web.WebInvokeAttribute>과 연결됩니다. <xref:System.UriTemplate> 및<xref:System.UriTemplateTable>에 대 한 자세한 내용은 [UriTemplate 및 UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md) 를 참조 하세요.  
  
## <a name="webget-and-webinvoke-attributes"></a>WebGet 및 WebInvoke 특성  
 WCF 웹 HTTP 서비스는 다양 한 호출 동사 (예: HTTP POST, PUT 및 DELETE) 뿐 아니라 검색 동사 (예: HTTP GET)를 사용 합니다. WCF 웹 HTTP 프로그래밍 모델을 사용 하면 서비스 개발자가 URI 템플릿과 <xref:System.ServiceModel.Web.WebGetAttribute> 및 <xref:System.ServiceModel.Web.WebInvokeAttribute>를 사용 하 여 서비스 작업과 연결 된 동사를 모두 제어할 수 있습니다. <xref:System.ServiceModel.Web.WebGetAttribute> 및 <xref:System.ServiceModel.Web.WebInvokeAttribute>를 사용하면 개별 작업이 URI 및 이러한 URI와 관련된 HTTP 메서드에 바인딩되는 방법을 제어할 수 있습니다. 예를 들어 다음 코드에 <xref:System.ServiceModel.Web.WebGetAttribute> 및 <xref:System.ServiceModel.Web.WebInvokeAttribute>를 추가합니다.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It"  
  
  [WebGet]  
  Customer GetCustomer():  
  
  //"Do It"  
    [WebInvoke]  
  Customer UpdateCustomerName( string id,   
                               string newName );  
}  
```  
  
 이전 코드를 통해 다음과 같은 HTTP 요청을 만들 수 있습니다.  
  
 `GET /GetCustomer`  
  
 `POST /UpdateCustomerName`  
  
 <xref:System.ServiceModel.Web.WebInvokeAttribute>는 기본적으로 POST로 설정되지만 다른 동사에도 사용할 수 있습니다.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It" -> HTTP GET  
    [WebGet( UriTemplate="customers/{id}" )]  
  Customer GetCustomer( string id ):  
  
  //"Do It" -> HTTP PUT  
  [WebInvoke( UriTemplate="customers/{id}", Method="PUT" )]  
  Customer UpdateCustomer( string id, Customer newCustomer );  
}  
```  
  
 Wcf 웹 HTTP 프로그래밍 모델을 [사용 하는 wcf 서비스의 전체 샘플을 보려면 방법: 기본 WCF 웹 HTTP 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)  
  
## <a name="uritemplate-query-string-parameters-and-urls"></a>UriTemplate 쿼리 문자열 매개 변수 및 URL  
 웹 스타일 서비스는 서비스 작업과 관련된 URL을 입력하여 웹 브라우저에서 호출할 수 있습니다. 이러한 서비스 작업은 URL 내의 문자열 형식에 지정해야 하는 쿼리 문자열 매개 변수를 가져올 수 있습니다. 다음 표에서는 URL 내에서 전달할 수 있는 형식과 사용된 형식을 보여 줍니다.  
  
|형식|형식|  
|----------|------------|  
|<xref:System.Byte>|0 - 255|  
|<xref:System.SByte>|-128 - 127|  
|<xref:System.Int16>|-32768 - 32767|  
|<xref:System.Int32>|-2,147,483,648 - 2,147,483,647|  
|<xref:System.Int64>|-9,223,372,036,854,775,808 - 9,223,372,036,854,775,807|  
|<xref:System.UInt16>|0 - 65535|  
|<xref:System.UInt32>|0 - 4,294,967,295|  
|<xref:System.UInt64>|0 - 18,446,744,073,709,551,615|  
|<xref:System.Single>|-3.402823e38 - 3.402823e38(지수 표기법이 필요하지 않음)|  
|<xref:System.Double>|-1.79769313486232e308 - 1.79769313486232e308(지수 표기법이 필요하지 않음)|  
|<xref:System.Char>|단일 문자|  
|<xref:System.Decimal>|표준 표기법으로 나타낸 10진수(지수 없음)|  
|<xref:System.Boolean>|True 또는 False(대/소문자 구분 안 함)|  
|<xref:System.String>|모든 문자열(null 문자열이 지원되지 않으며 이스케이프가 수행되지 않음)|  
|<xref:System.DateTime>|MM/DD/YYYY<br /><br /> MM/DD/YYYY HH: MM: SS [AM&#124;PM]<br /><br /> 월/일/연도<br /><br /> 월 일 연도 HH: MM: SS [AM&#124;PM]|  
|<xref:System.TimeSpan>|DD.HH:MM:SS<br /><br /> 여기서 DD = 일, HH = 시간, MM = 분, SS = 초입니다.|  
|<xref:System.Guid>|GUID, 예:<br /><br /> 936DA01F-9ABD-4d9d-80C7-02AF85C822A8|  
|<xref:System.DateTimeOffset>|MM/DD/YYYY HH:MM:SS MM:SS<br /><br /> 여기서 DD = 일, HH = 시간, MM = 분, SS = 초입니다.|  
|열거형|다음 코드에서처럼 열거형을 정의하는 예제의 열거형 값입니다.<br /><br /> `public enum Days{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };`<br /><br /> 개별 열거형 값 또는 해당 정수 값은 쿼리 문자열에 지정할 수 있습니다.|  
|문자열 표현과 형식을 서로 변환할 수 있는 `TypeConverterAttribute`가 있는 형식입니다.|형식 변환기에 따라 다릅니다.|  
  
## <a name="formats-and-the-wcf-web-http-programming-model"></a>형식 및 WCF WEB HTTP 프로그래밍 모델  
 WCF WEB HTTP 프로그래밍 모델에는 다양 한 데이터 형식으로 작업할 수 있는 새로운 기능이 있습니다. <xref:System.ServiceModel.WebHttpBinding>은 바인딩 계층에서 다음과 같은 여러 종류의 데이터를 읽고 쓸 수 있습니다.  
  
- XML  
  
- JSON  
  
- 불투명 이진 스트림  
  
 즉, WCF 웹 HTTP 프로그래밍 모델은 모든 형식의 데이터를 처리할 수 있지만에 대해 <xref:System.IO.Stream>프로그래밍할 수 있습니다.  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)]에서는 JSON 데이터(AJAX)와 배포 피드(ATOM 및 RSS 포함)를 지원합니다. 이러한 기능에 대 한 자세한 내용은 [Wcf 웹 HTTP 형식 지정](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)[wcf 배포 개요](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md) 및 [AJAX 통합 및 JSON 지원](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)을 참조 하세요.  
  
## <a name="wcf-web-http-programming-model-and-security"></a>WCF WEB HTTP 프로그래밍 모델 및 보안  
 WCF 웹 HTTP 프로그래밍 모델은 WS-* 프로토콜을 지원 하지 않으므로 WCF 웹 HTTP 서비스를 보호 하는 유일한 방법은 SSL을 사용 하 여 HTTPS를 통해 서비스를 노출 하는 것입니다. IIS 7.0에서 SSL을 설정 하는 방법에 대 한 자세한 내용은 [iis에서 ssl을 구현 하는 방법](https://go.microsoft.com/fwlink/?LinkId=131613) 을 참조 하십시오.  
  
## <a name="troubleshooting-the-wcf-web-http-programming-model"></a>WCF WEB HTTP 프로그래밍 모델 문제 해결  
 <xref:System.ServiceModel.Channels.ChannelFactoryBase%601>을 사용하는 WCF WEB HTTP 서비스를 호출해 채널을 만들 때 <xref:System.ServiceModel.Description.WebHttpBehavior>는 다른 <xref:System.ServiceModel.EndpointAddress>가 <xref:System.ServiceModel.EndpointAddress>로 전달되어도 구성 파일에 설정된 <xref:System.ServiceModel.Channels.ChannelFactoryBase%601>를 사용합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 배포](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)
- [WCF 웹 HTTP 프로그래밍 개체 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)
- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
