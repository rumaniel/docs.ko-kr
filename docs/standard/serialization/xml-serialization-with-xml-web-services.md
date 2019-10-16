---
title: XML Web Services의 XML Serialization
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML Web services, XML serialization
- XML serialization, XML Web services
- SOAP, XML serialization
- asmx files
- serialization, SOAP
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- .asmx files
- encoded XML serialization
- literal XML serialization
- serialization, attributes
ms.assetid: a416192f-8102-458e-bc0a-0b8f3f784da9
ms.openlocfilehash: 79cc53be0f099151db1b64190c844b1d57205a44
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018071"
---
# <a name="xml-serialization-with-xml-web-services"></a>XML Web Services의 XML Serialization
XML serialization은 XML Web services 아키텍처에 사용되며 <xref:System.Xml.Serialization.XmlSerializer> 클래스에 의해 수행되는 내부 전송 메커니즘입니다. XML Web services로 생성된 XML을 제어하려면 [XML serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md) 및 [인코드된 SOAP serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)에 나열된 특성을 XML Web services(.asmx)를 만드는 데 사용된 파일의 클래스, 반환 값, 매개 변수 및 필드에 적용할 수 있습니다. XML 웹 서비스를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET XML Web Services를 사용 하 여](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ba0z6a33(v=vs.100))입니다.  
  
## <a name="literal-and-encoded-styles"></a>리터럴 및 인코딩된 스타일  
 XML 웹 서비스에서 생성 된 XML 리터럴 중 두 가지 방법 중 하나로 형식 지정 하거나에 설명 된 대로 인코딩할 수 [SOAP 메시지 형식을 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dkwy2d72(v=vs.100))합니다. 따라서 XML serialization을 제어하는 두 개의 특성 집합이 있습니다. [XML serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md)에 나열된 특성은 리터럴 스타일 XML을 제어하도록 설계되었습니다. [인코드된 SOAP serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)에 나열된 특성은 인코드된 스타일을 제어합니다. 이러한 특성을 선택적으로 적용하여 애플리케이션이 두 스타일 중 하나 또는 둘 모두를 반환하도록 조정할 수 있습니다. 또한 이러한 특성을 필요에 따라 반환 값 및 매개 변수에 적용할 수 있습니다.  
  
### <a name="example-of-using-both-styles"></a>두 스타일 사용 예제  
 XML Web service를 만들 때는 메서드에 두 특성 집합 모두를 사용할 수 있습니다. 다음 코드 예제에서는 `MyService`라는 클래스에 두 개의 XML Web services 메서드인 `MyLiteralMethod` 및 `MyEncodedMethod`가 포함됩니다. 두 메서드 모두 `Order` 클래스의 인스턴스를 반환하는 동일한 기능을 수행합니다. `Order` 클래스에서 <xref:System.Xml.Serialization.XmlTypeAttribute> 및 <xref:System.Xml.Serialization.SoapTypeAttribute> 특성이 둘 다 `OrderID` 필드에 적용되며 두 특성의 `ElementName` 속성은 서로 다르게 설정됩니다.  
  
 예제를 실행하려면 코드를 .asmx 확장명의 파일로 붙여넣은 다음 파일을 IIS(인터넷 정보 서비스)에서 관리하는 가상 디렉터리에 넣습니다. Internet Explorer와 같은 HTML 브라우저에서 컴퓨터, 가상 디렉터리 및 파일의 이름을 입력합니다.  
  
```vb  
<%@ WebService Language="VB" Class="MyService" %>  
Imports System  
Imports System.Web.Services  
Imports System.Web.Services.Protocols  
Imports System.Xml.Serialization  
Public Class Order  
    ' Both types of attributes can be applied. Depending on which type  
    ' the method used, either one will affect the call.  
    <SoapElement(ElementName:= "EncodedOrderID"), _  
    XmlElement(ElementName:= "LiteralOrderID")> _  
    public OrderID As String  
End Class  
  
Public Class MyService  
    <WebMethod, SoapDocumentMethod> _  
    public Function MyLiteralMethod() As Order   
        Dim myOrder As Order = New Order()  
        return myOrder  
    End Function  
    <WebMethod, SoapRpcMethod> _  
    public Function MyEncodedMethod() As Order   
        Dim myOrder As Order = New Order()  
        return myOrder  
    End Function  
End Class  
```  
  
```csharp  
<%@ WebService Language="C#" Class="MyService" %>  
using System;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using System.Xml.Serialization;  
public class Order {  
    // Both types of attributes can be applied. Depending on which type  
    // the method used, either one will affect the call.  
    [SoapElement(ElementName = "EncodedOrderID")]  
    [XmlElement(ElementName = "LiteralOrderID")]  
    public String OrderID;  
}  
public class MyService {  
    [WebMethod][SoapDocumentMethod]  
    public Order MyLiteralMethod(){  
        Order myOrder = new Order();  
        return myOrder;  
    }  
    [WebMethod][SoapRpcMethod]  
    public Order MyEncodedMethod(){  
        Order myOrder = new Order();  
        return myOrder;  
    }  
}  
```  
  
 다음 코드 예제에서는 `MyLiteralMethod`를 호출합니다. 요소 이름이 "LiteralOrderID"로 변경됩니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
    <soap:Body>  
        <MyLiteralMethodResponse xmlns="http://tempuri.org/">  
            <MyLiteralMethodResult>  
                <LiteralOrderID>string</LiteralOrderID>  
            </MyLiteralMethodResult>  
        </MyLiteralMethodResponse>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 다음 코드 예제에서는 `MyEncodedMethod`를 호출합니다. 요소 이름은 "EncodedOrderID"입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" xmlns:tns="http://tempuri.org/" xmlns:types="http://tempuri.org/encodedTypes" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
    <soap:Body soap:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
        <tns:MyEncodedMethodResponse>  
            <MyEncodedMethodResult href="#id1" />  
        </tns:MyEncodedMethodResponse>  
        <types:Order id="id1" xsi:type="types:Order">  
            <EncodedOrderID xsi:type="xsd:string">string</EncodedOrderID>  
        </types:Order>  
    </soap:Body>  
</soap:Envelope>  
```  
  
### <a name="applying-attributes-to-return-values"></a>특성을 반환 값에 적용  
 또한 특성을 반환 값에 적용하여 네임스페이스, 요소 이름 등을 제어할 수도 있습니다. 다음 코드 예제에서는 `XmlElementAttribute` 특성을 `MyLiteralMethod` 메서드의 반환 값에 적용합니다. 이렇게 하면 네임스페이스와 요소 이름을 제어할 수 있습니다.  
  
```vb  
<WebMethod, SoapDocumentMethod> _  
public Function MyLiteralMethod() As _  
<XmlElement(Namespace:="http://www.cohowinery.com", _  
ElementName:= "BookOrder")> _  
Order   
    Dim myOrder As Order = New Order()  
    return myOrder  
End Function  
```  
  
```csharp  
[return: XmlElement(Namespace = "http://www.cohowinery.com",  
ElementName = "BookOrder")]  
[WebMethod][SoapDocumentMethod]  
public Order MyLiteralMethod(){  
    Order myOrder = new Order();  
    return myOrder;  
}  
```  
  
 호출될 때 코드는 다음과 같은 XML을 반환합니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
    <soap:Body>  
        <MyLiteralMethodResponse xmlns="http://tempuri.org/">  
            <BookOrder xmlns="http://www.cohowinery.com">  
                <LiteralOrderID>string</LiteralOrderID>  
            </BookOrder>  
        </MyLiteralMethodResponse>  
    </soap:Body>  
</soap:Envelope>  
```  
  
### <a name="attributes-applied-to-parameters"></a>매개 변수에 적용되는 특성  
 또한 특성을 매개 변수에 적용하여 네임스페이스, 요소 이름 등을 지정할 수도 있습니다. 다음 코드 예제에서는 매개 변수를 `MyLiteralMethodResponse` 메서드에 추가하고 `XmlAttributeAttribute` 특성을 매개 변수에 적용합니다. 요소 이름과 네임스페이스는 모두 매개 변수에 대해 설정됩니다.  
  
```vb  
<WebMethod, SoapDocumentMethod> _  
public Function MyLiteralMethod(<XmlElement _  
("MyOrderID", Namespace:="http://www.microsoft.com")>ID As String) As _  
<XmlElement(Namespace:="http://www.cohowinery.com", _  
ElementName:= "BookOrder")> _  
Order   
    Dim myOrder As Order = New Order()  
    myOrder.OrderID = ID  
    return myOrder  
End Function  
```  
  
```csharp  
[return: XmlElement(Namespace = "http://www.cohowinery.com",  
ElementName = "BookOrder")]  
[WebMethod][SoapDocumentMethod]  
public Order MyLiteralMethod([XmlElement("MyOrderID",   
Namespace="http://www.microsoft.com")] string ID){  
    Order myOrder = new Order();  
    myOrder.OrderID = ID;  
    return myOrder;  
}   
```  
  
 SOAP 요청은 다음과 같습니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
    <soap:Body>  
        <MyLiteralMethod xmlns="http://tempuri.org/">  
            <MyOrderID xmlns="http://www.microsoft.com">string</MyOrderID>  
        </MyLiteralMethod>  
    </soap:Body>  
</soap:Envelope>  
```  
  
### <a name="applying-attributes-to-classes"></a>특성을 클래스에 적용  
 클래스에 관련된 요소의 네임스페이스를 제어하려면 필요에 따라 `XmlTypeAttribute`, `XmlRootAttribute` 및 `SoapTypeAttribute`를 적용할 수 있습니다. 다음 코드 예제에서는 세 가지 모두를 `Order` 클래스에 적용합니다.  
  
```vb  
<XmlType("BigBookService"), _  
SoapType("SoapBookService"), _  
XmlRoot("BookOrderForm")> _  
Public Class Order  
    ' Both types of attributes can be applied. Depending on which  
    ' the method used, either one will affect the call.  
    <SoapElement(ElementName:= "EncodedOrderID"), _  
    XmlElement(ElementName:= "LiteralOrderID")> _  
    public OrderID As String  
End Class  
```  
  
```csharp  
[XmlType("BigBooksService", Namespace = "http://www.cpandl.com")]  
[SoapType("SoapBookService")]  
[XmlRoot("BookOrderForm")]  
public class Order {  
    // Both types of attributes can be applied. Depending on which  
    // the method used, either one will affect the call.  
    [SoapElement(ElementName = "EncodedOrderID")]  
    [XmlElement(ElementName = "LiteralOrderID")]  
    public String OrderID;  
}  
```  
  
 `XmlTypeAttribute` 및 `SoapTypeAttribute`를 적용한 결과는 다음 코드 예제에서처럼 서비스 설명에서 확인할 수 있습니다.  
  
```xml  
    <s:element name="BookOrderForm" type="s0:BigBookService" />   
- <s:complexType name="BigBookService">  
- <s:sequence>  
    <s:element minOccurs="0" maxOccurs="1" name="LiteralOrderID" type="s:string" />   
    </s:sequence>  
  
- <s:schema targetNamespace="http://tempuri.org/encodedTypes">  
- <s:complexType name="SoapBookService">  
- <s:sequence>  
    <s:element minOccurs="1" maxOccurs="1" name="EncodedOrderID" type="s:string" />   
    </s:sequence>  
    </s:complexType>  
    </s:schema>  
```  
  
 `XmlRootAttribute`의 효과는 다음과 같이 HTTP GET 및 HTTP POST 결과에서도 볼 수 있습니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<BookOrderForm xmlns="http://tempuri.org/">  
    <LiteralOrderID>string</LiteralOrderID>  
</BookOrderForm>  
```  
  
## <a name="see-also"></a>참고자료

- [XML 및 SOAP serialization](../../../docs/standard/serialization/xml-and-soap-serialization.md)
- [인코딩된 SOAP serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)
- [방법: SOAP 인코딩된 XML Stream으로 개체를 serialize 합니다.](../../../docs/standard/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [방법: 인코딩된 SOAP XML Serialization 재정의](../../../docs/standard/serialization/how-to-override-encoded-soap-xml-serialization.md)
- [XML serialization 소개](../../../docs/standard/serialization/introducing-xml-serialization.md)
- [방법: 개체 serialize](../../../docs/standard/serialization/how-to-serialize-an-object.md)
- [방법: 개체 deserialize](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
