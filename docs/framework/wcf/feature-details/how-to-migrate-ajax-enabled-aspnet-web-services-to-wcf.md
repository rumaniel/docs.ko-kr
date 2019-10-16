---
title: '방법: AJAX 사용 ASP.NET 웹 서비스를 WCF로 마이그레이션'
ms.date: 03/30/2017
ms.assetid: 1428df4d-b18f-4e6d-bd4d-79ab3dd5147c
ms.openlocfilehash: f492efe9e364195dce6b73a14e9ca5fa34a6df25
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972297"
---
# <a name="how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf"></a>방법: AJAX 사용 ASP.NET 웹 서비스를 WCF로 마이그레이션
이 항목에서는 기본 ASP.NET AJAX 서비스를 해당 하는 AJAX 사용 Windows Communication Foundation (WCF) 서비스로 마이그레이션하는 절차를 간략하게 설명 합니다. ASP.NET AJAX 서비스의 기능적으로 동일한 WCF 버전을 만드는 방법을 보여 줍니다. 그런 다음 두 서비스를 함께 사용할 수 있습니다. 또는 WCF 서비스를 사용 하 여 ASP.NET AJAX 서비스를 대체할 수 있습니다.

 기존 ASP.NET AJAX 서비스를 WCF AJAX 서비스로 마이그레이션하면 다음과 같은 이점이 제공 됩니다.

- 최소의 추가 구성만으로 AJAX 서비스를 SOAP 서비스로 노출할 수 있습니다.

- 추적과 같은 WCF 기능의 이점을 누릴 수 있습니다.

 다음 절차에서는 Visual Studio 2012을 사용 하 고 있다고 가정 합니다.

 이 항목에서 간략히 설명된 절차에서 얻어진 코드는 다음 예제에 나와 있습니다.

 AJAX 사용 끝점 [을 통해 WCF 서비스를 노출 하는 방법에 대 한 자세한 내용은 방법: 구성을 사용 하 여 ASP.NET AJAX 끝점](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md) 항목을 추가 합니다.

### <a name="to-create-and-test-the-aspnet-web-service-application"></a>ASP.NET 웹 서비스 애플리케이션을 만들고 테스트하려면

1. Visual Studio 2012을 엽니다.

2. **파일** 메뉴에서 **새로 만들기**, **프로젝트**, **웹**을 차례로 선택한 다음 **ASP.NET 웹 서비스 응용 프로그램**을 선택 합니다.

3. 프로젝트 `ASPHello` 이름을로 확인 하 고 **확인을**클릭 합니다.

4. 이 서비스에서 AJAX를 사용하려면 Service1.asmx.cs 파일에서 `System.Web.Script.Services.ScriptService]`가 포함된 행의 주석 처리를 제거합니다.

5. **빌드** 메뉴에서 **솔루션 빌드**를 선택 합니다.

6. **디버그** 메뉴에서 **디버깅하지 않고 시작**을 선택합니다.

7. 생성된 웹 페이지에서 `HelloWorld` 작업을 선택합니다.

8. `HelloWorld` 테스트 페이지에서 **호출** 단추를 클릭 합니다. 다음과 같은 XML 응답을 받게 됩니다.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <string xmlns="http://tempuri.org/">Hello World</string>
    ```

9. 이 응답을 통해 현재 ASP.NET AJAX 서비스가 작동 중임을 확인할 수 있으며, 특히 해당 서비스가 Service1.asmx/HelloWorld에서 HTTP POST 요청에 응답하는 엔드포인트를 노출하고 XML을 반환함을 확인할 수 있습니다.

     이제이 서비스를 변환 하 여 WCF AJAX 서비스를 사용할 준비가 되었습니다.

### <a name="to-create-an-equivalent-wcf-ajax-service-application"></a>동등한 WCF AJAX 서비스 애플리케이션을 만들려면

1. 기능 **hello** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**, **AJAX 사용 WCF 서비스**를 차례로 선택 합니다.

2. 서비스 `WCFHello` 이름을로, **추가**를 클릭 합니다.

3. WCFHello.svc.cs 파일을 엽니다.

4. Service1.asmx.cs에서 다음 `HelloWorld` 작업 구현을 복사 합니다.

    ```csharp
    public string HelloWorld()
    {
         return "Hello World";
    }
    ```

5. 다음 코드 대신 복사 된 `HelloWorld` 작업의 구현을 WCFHello.svc.cs 파일에 붙여 넣습니다.

    ```csharp
    public void DoWork()
    {
          // Add your operation implementation here
          return;
    }
    ```

6. 에 대 한 <xref:System.ServiceModel.ServiceContractAttribute> `WCFHello`특성을로 지정 합니다. `Namespace`

    ```csharp
    [ServiceContract(Namespace="WCFHello")]
    [AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Required)]
    public class WCFHello
    { … }
    ```

7. <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> <xref:System.ServiceModel.Web.WebMessageFormat.Xml>를 작업 <xref:System.ServiceModel.Web.WebInvokeAttribute> `HelloWorld` 에 추가 하 고 속성을로 설정 하 여를 반환 합니다. 이 속성을 설정하지 않은 경우 기본 반환 형식은 <xref:System.ServiceModel.Web.WebMessageFormat.Json>입니다.

    ```csharp
    [OperationContract]
    [WebInvoke(ResponseFormat=WebMessageFormat.Xml)]
    public string HelloWorld()
    {
        return "Hello World";
    }
    ```

8. **빌드** 메뉴에서 **솔루션 빌드**를 선택 합니다.

9. Wcfhello.svc 파일을 열고 **디버그** 메뉴에서 **디버깅 하지 않고 시작**을 선택 합니다.

10. 이제 서비스는 HTTP POST 요청에 `WCFHello.svc/HelloWorld`응답 하는 끝점을 노출 합니다. HTTP POST 요청은 브라우저에서 테스트할 수 없지만 엔드포인트는 다음과 같은 XML을 반환합니다.

    ```xml
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Hello World</string>
    ```

11. `WCFHello.svc/HelloWorld` 및끝점은이제`Service1.aspx/HelloWorld` 기능적으로 동일 합니다.

## <a name="example"></a>예제
 이 항목에서 간략히 설명된 절차에서 얻어진 코드는 다음 예제에 나와 있습니다.

```csharp
//This is the ASP.NET code in the Service1.asmx.cs file.

using System;
using System.Collections;
using System.ComponentModel;
using System.Data;
using System.Linq;
using System.Web;
using System.Web.Services;
using System.Web.Services.Protocols;
using System.Xml.Linq;
using System.Web.Script.Services;

namespace ASPHello
{
    /// <summary>
    /// Summary description for Service1.
    /// </summary>
    [WebService(Namespace = "http://tempuri.org/")]
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
    [ToolboxItem(false)]
    // To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line.
    [System.Web.Script.Services.ScriptService]
    public class Service1 : System.Web.Services.WebService
    {

        [WebMethod]
        public string HelloWorld()
        {
            return "Hello World";
        }
    }
}

//This is the WCF code in the WCFHello.svc.cs file.
using System;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Activation;
using System.ServiceModel.Web;

namespace ASPHello
{
    [ServiceContract(Namespace = "WCFHello")]
    [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]
    public class WCFHello
    {
        // Add [WebInvoke] attribute to use HTTP GET.
        [OperationContract]
        [WebInvoke(ResponseFormat=WebMessageFormat.Xml)]
        public string HelloWorld()
        {
            return "Hello World";
        }

        // Add more operations here and mark them with [OperationContract].
    }
}
```

 <xref:System.Xml.XmlDocument> 형식은 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>를 통해 serialize할 수 없으므로 <xref:System.Xml.Serialization.XmlSerializer>에서 지원하지 않습니다. 대신 <xref:System.Xml.Linq.XDocument> 형식을 사용하거나 <xref:System.Xml.XmlDocument.DocumentElement%2A>를 serialize할 수 있습니다.

 ASMX 웹 서비스를 WCF 서비스와 나란히 업그레이드 하 고 마이그레이션하는 경우 클라이언트에서 두 형식을 동일한 이름으로 매핑하지 마세요. 이 경우 같은 형식을 <xref:System.Web.Services.WebMethodAttribute> 및 <xref:System.ServiceModel.ServiceContractAttribute>에서 사용하면 serializer에 예외가 발생합니다.

- Wcf 서비스를 먼저 추가한 경우 프록시의 wcf 스타일 정의가 우선적으로 적용 되기 때문에 ASMX <xref:System.Web.UI.ObjectConverter.ConvertValue%28System.Object%2CSystem.Type%2CSystem.String%29> 웹 서비스에서 메서드를 호출 하면에서 예외가 발생 합니다.

- ASMX 웹 서비스를 먼저 추가한 경우 프록시의 웹 서비스 스타일 정의가 우선적으로 적용 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 되기 때문에 WCF 서비스에서 메서드를 호출 하면 예외가 발생 합니다.

 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>와 ASP.NET AJAX <xref:System.Web.Script.Serialization.JavaScriptSerializer>의 동작에는 상당한 차이점이 있습니다. 예를 들어, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>는 키/값 쌍의 배열로 사전을 나타내고, ASP.NET AJAX <xref:System.Web.Script.Serialization.JavaScriptSerializer>는 실제 JSON 개체로 사전을 나타냅니다. 따라서 ASP.NET AJAX에서 사전은 다음과 같이 나타납니다.

```csharp
Dictionary<string, int> d = new Dictionary<string, int>();
d.Add("one", 1);
d.Add("two", 2);
```

 이 사전은 다음 목록에 표시된 것처럼 JSON 개체로 표현됩니다.

- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>에 의한 [{"Key":"one","Value":1},{"Key":"two","Value":2}]

- ASP.NET AJAX의 {"one": 1, "two": 2}<xref:System.Web.Script.Serialization.JavaScriptSerializer>

 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>는 키 유형이 문자열이 아닌 사전을 처리할 수 있다는 점에서 훨씬 강력합니다. 반면 <xref:System.Web.Script.Serialization.JavaScriptSerializer>는 키 유형이 문자열이 아닌 사전을 처리할 수 없습니다. 그러나 후자가 JSON에 더 적합합니다.

 이 두 serializer의 중요한 차이점이 다음 표에 요약되어 있습니다.

|차이의 범주|DataContractJsonSerializer|ASP.NET AJAX JavaScriptSerializer|
|-----------------------------|--------------------------------|---------------------------------------|
|빈 버퍼(새 바이트[0])를 <xref:System.Object> 또는 <xref:System.Uri> 또는 다른 클래스로 deserialize함|SerializationException|null|
|<xref:System.DBNull.Value>의 serialization|{}(또는 {"__type": "#System"})|Null|
|[Serializable] 형식의 private 멤버 serialization|serialize됨|serialize되지 않음|
|<xref:System.Runtime.Serialization.ISerializable> 형식의 .public 속성 serialization|serialize되지 않음|serialize됨|
|JSON "확장명"|개체 멤버 이름({"a":"hello"})에 따옴표를 사용해야 하는 JSON 사양 준수|따옴표가 없는 개체 멤버 이름({a:"hello"}) 지원|
|<xref:System.DateTime> UTC(협정 세계시)|\\"{4}/Date (123456789U\\)/" 또는 "\\/날짜\\(\d\\+\\+(U&#124;(-[\d]))형식을지원하지\\않습니다. \\\\/)".|\\"{4}/Date (123456789U\\)/" 및 "\\/date\\(\d\\+\\+(U&#124;(-[\d]))형식을지원\\합니다. \\ /)\\"를 DateTime 값으로|
|사전의 표현|KeyValuePair\<K, V >의 배열은 문자열이 아닌 키 유형을 처리 합니다.|실제 JSON 개체로 문자열인 키 유형만 처리합니다.|
|이스케이프된 문자|항상 이스케이프 슬래시(/)가 포함되고, "\n"과 같이 이스케이프되지 않은 잘못된 JSON 문자는 사용할 수 없습니다.|DateTime 값에 이스케이프 슬래시(/)가 포함됩니다.|

## <a name="see-also"></a>참고자료

- [방법: 구성을 사용 하 여 ASP.NET AJAX 끝점 추가](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)
