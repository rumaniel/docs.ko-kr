---
title: XPathNavigator를 사용하여 강력한 형식의 XML 데이터 액세스
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 898e0f52-8a7c-4d1f-afcd-6ffb28b050b4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2bc33d27d48267f5b74f1baf67a49bdf0b55c839
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647982"
---
# <a name="accessing-strongly-typed-xml-data-using-xpathnavigator"></a>XPathNavigator를 사용하여 강력한 형식의 XML 데이터 액세스
XPath 2.0 데이터 모델의 인스턴스로서 <xref:System.Xml.XPath.XPathNavigator> 클래스는 CLR(공용 언어 런타임) 형식에 매핑되는 강력한 형식의 데이터를 포함할 수 있습니다. XPath 2.0 데이터 모델에 따르면 요소와 특성에만 강력한 형식의 데이터를 포함할 수 있습니다. <xref:System.Xml.XPath.XPathNavigator> 클래스는 데이터 형식을 변환하는 메커니즘뿐 아니라 강력한 형식의 데이터로 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체 내의 데이터에 액세스할 수 있는 메커니즘도 제공합니다.  
  
## <a name="type-information-exposed-by-xpathnavigator"></a>XPathNavigator에 의해 노출된 형식 정보  
 XML 1.0 데이터가 DTD, XSD(XML 스키마 정의 언어) 스키마 또는 기타 메커니즘으로 처리되지 않을 경우 기술적인 측면에서 XML 1.0 데이터에는 형식이 없습니다. XML 요소나 특성에 연결할 수 있는 형식 정보 범주에는 여러 가지가 있습니다.  
  
- 단순 CLR 형식: XML 스키마 언어는 CLR(공용 언어 런타임) 형식을 직접 지원하지 않습니다. 가장 적합한 CLR 형식으로 단순 요소 및 특성 내용을 볼 수 있으므로 스키마 정보가 없을 경우 이 내용을 보다 적합한 형식으로 구체화할 수 있는 추가된 스키마 정보를 사용하여 모든 단순 내용에 <xref:System.String> 형식을 지정할 수 있습니다. <xref:System.Xml.XPath.XPathNavigator.ValueType%2A> 속성을 사용하여 단순 요소 및 특성 내용의 가장 일치하는 CLR 형식을 찾을 수 있습니다. 스키마 기본 제공 형식에서 CLR 형식으로 매핑하는 방법에 대한 자세한 내용은 [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)을 참조하세요.  
  
- 단순 (CLR) 형식 목록: 단순 콘텐츠가 있는 요소나 특성에 공백으로 구분된 값 목록이 포함될 수 있습니다. 값은 XML 스키마에 의해 "목록 형식"으로 지정됩니다. XML 스키마가 없을 경우 이러한 단순 내용은 단일 텍스트 노드로 간주됩니다. XML 스키마를 사용할 수 있는 경우 이 단순 내용을 일련의 atomic 값으로 노출할 수 있습니다. 각 atomic 값은 CLR 개체 컬렉션으로 매핑되는 단순 형식입니다. 스키마 기본 제공 형식에서 CLR 형식으로 매핑하는 방법에 대한 자세한 내용은 [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)을 참조하세요.  
  
- 형식화된 값: 스키마에 의해 유효성이 검사되는 단순 형식의 특성 또는 요소에는 형식화된 값이 있습니다. 이 값은 numeric, string, date 형식 등의 기본 형식입니다. XSD의 모든 기본 제공 단순 형식을 CLR 형식으로 매핑할 수 있습니다. 이 CLR 형식을 사용하면 단순히 <xref:System.String>으로 노드 값에 액세스하는 대신 더욱 적합한 형식으로 노드 값에 액세스할 수 있습니다. 특성이나 요소 자식이 있는 요소는 복합 형식으로 간주됩니다. 단순 내용(자식으로 텍스트 노드만 포함)이 있는 복합 형식의 형식화된 값은 단순 내용의 단순 형식의 형식화된 값과 같습니다. 복합 내용(하나 이상의 자식 요소 포함)이 있는 복합 형식의 형식화된 값은 <xref:System.String>으로 반환된 모든 자식 텍스트 노드를 연결한 문자열 값입니다. 스키마 기본 제공 형식에서 CLR 형식으로 매핑하는 방법에 대한 자세한 내용은 [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)을 참조하세요.  
  
- 스키마 언어 관련 형식 이름: 대부분의 경우 외부 스키마를 적용함으로써 부수적으로 설정되는 CLR 형식을 사용하여 노드 값에 액세스할 수 있습니다. 그러나 XML 문서에 적용된 특정 스키마와 연결된 형식을 검사해야 할 경우가 있습니다. 예를 들어, XML 문서를 검색하여 "PurchaseOrder" 형식의 내용이 포함된 것으로 확인된 모든 요소를 연결된 스키마에 따라 추출할 수 있습니다. 이러한 형식 정보는 스키마 유효성 검사 결과로만 설정할 수 있으며 <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 속성을 통해 이 정보에 액세스할 수 있습니다. 자세한 내용은 아래의 PSVI(Post Schema Validation Infoset) 단원을 참조하세요.  
  
- 스키마 언어 관련 형식 리플렉션: XML 문서에 적용된 스키마 관련 형식의 세부 정보를 얻어야 할 경우가 있습니다. 예를 들어, XML 파일을 읽을 때 사용자 지정 계산을 수행하기 위해 XML 문서에서 유효한 각 노드의 `maxOccurs` 특성을 추출해야 할 수 있습니다. 이 정보는 스키마 유효성 검사를 통해서만 설정되므로 <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator> 속성을 통해 이 정보에 액세스할 수 있습니다. 자세한 내용은 아래의 PSVI(Post Schema Validation Infoset) 단원을 참조하세요.  
  
## <a name="xpathnavigator-typed-accessors"></a>XPathNavigator의 형식화된 접근자  
 다음 표에서는 노드에 대한 형식 정보에 액세스하는 데 사용할 수 있는 <xref:System.Xml.XPath.XPathNavigator> 클래스의 다양한 속성 및 메서드를 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Xml.XPath.XPathNavigator.XmlType%2A>|유효한 경우 노드에 대한 XML 스키마 형식 정보가 들어 있습니다.|  
|<xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A>|유효성 검사 후 추가된 노드의 Post Schema Validation Infoset이 들어 있습니다. 유효성 정보와 XML 스키마 형식 정보가 들어 있습니다.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueType%2A>|형식화된 노드 값의 CLR 형식입니다.|  
|<xref:System.Xml.XPath.XPathNavigator.TypedValue%2A>|하나 이상의 CLR 값의 형식이 노드의 XML 스키마 형식에 가장 일치하는 노드 내용입니다.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsBoolean%2A>|현재 노드의 <xref:System.String> 값은 <xref:System.Boolean>에 대한 XPath 2.0 캐스팅 규칙에 따라 `xs:boolean` 값을 캐스팅합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsDateTime%2A>|현재 노드의 <xref:System.String> 값은 <xref:System.DateTime>에 대한 XPath 2.0 캐스팅 규칙에 따라 `xs:datetime` 값을 캐스팅합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsDouble%2A>|현재 노드의 <xref:System.String> 값은 <xref:System.Double>에 대한 XPath 2.0 캐스팅 규칙에 따라 `xsd:double` 값을 캐스팅합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsInt%2A>|현재 노드의 <xref:System.String> 값은 <xref:System.Int32>에 대한 XPath 2.0 캐스팅 규칙에 따라 `xs:integer` 값을 캐스팅합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsLong%2A>|현재 노드의 <xref:System.String> 값은 <xref:System.Int64>에 대한 XPath 2.0 캐스팅 규칙에 따라 `xs:integer` 값을 캐스팅합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAs%2A>|노드 내용은 XPath 2.0 캐스팅 규칙에 따라 대상 형식을 캐스팅합니다.|  
  
 스키마 기본 제공 형식에서 CLR 형식으로 매핑하는 방법에 대한 자세한 내용은 [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)을 참조하세요.  
  
## <a name="the-post-schema-validation-infoset-psvi"></a>PSVI(Post Schema Validation Infoset)  
 XML 스키마 프로세서는 XML Infoset을 입력으로 허용하며 이 XML Infoset을 PSVI(Post Schema Validation Infoset)로 변환합니다. PSVI는 원래 입력 XML Infoset의 기존 정보 항목에 새 정보 항목과 새 속성을 추가한 것입니다. <xref:System.Xml.XPath.XPathNavigator>에 의해 노출된 PSVI에는 XML Infoset에 추가된 정보의 광범위한 클래스 세 개가 있습니다.  
  
1. 유효성 검사 결과: 요소나 특성에 대한 유효성 검사가 성공적으로 수행되었는지 여부를 나타내는 정보입니다. 그러면 <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> 속성에 들어 있는 <xref:System.Xml.XPath.XPathNavigator> 속성에 의해 노출됩니다.  
  
2. 기본 정보: 스키마에 지정된 기본값을 통해 요소 또는 특성 값을 얻었는지 여부를 나타냅니다. 그러면 <xref:System.Xml.Schema.IXmlSchemaInfo.IsDefault%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> 속성에 들어 있는 <xref:System.Xml.XPath.XPathNavigator> 속성에 의해 노출됩니다.  
  
3. 형식 주석: 형식 정의 또는 요소와 특성 선언 등의 스키마 구성 요소에 대한 참조 내용입니다. 유효한 경우 <xref:System.Xml.XPath.XPathNavigator.XmlType%2A>의 <xref:System.Xml.XPath.XPathNavigator> 속성에는 노드에 대한 특정 형식 정보가 들어 있습니다. 노드의 유효성을 검사한 후 노드를 편집한 경우와 같이 노드의 유효성을 알 수 없는 경우 <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> 속성은 `null`로 설정되지만 <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> 클래스에 대한 <xref:System.Xml.XPath.XPathNavigator> 속성의 다양한 속성을 통해 형식 정보를 확인할 수 있습니다.  
  
 다음 예제에서는 <xref:System.Xml.XPath.XPathNavigator>에 의해 노출된 Post Schema Validation Infoset의 정보를 사용하는 방법을 보여 줍니다.  
  
```vb  
Dim settings As XmlReaderSettings = New XmlReaderSettings()  
settings.Schemas.Add("http://www.contoso.com/books", "books.xsd")  
settings.ValidationType = ValidationType.Schema  
  
Dim reader As XmlReader = XmlReader.Create("books.xml", settings)  
  
Dim document As XmlDocument = New XmlDocument()  
document.Load(reader)  
Dim navigator As XPathNavigator = document.CreateNavigator()  
navigator.MoveToChild("books", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("published", "http://www.contoso.com/books")  
  
Console.WriteLine(navigator.SchemaInfo.SchemaType.Name)  
Console.WriteLine(navigator.SchemaInfo.Validity)  
Console.WriteLine(navigator.SchemaInfo.SchemaElement.MinOccurs)  
```  
  
```csharp  
XmlReaderSettings settings = new XmlReaderSettings();  
settings.Schemas.Add("http://www.contoso.com/books", "books.xsd");  
settings.ValidationType = ValidationType.Schema;  
  
XmlReader reader = XmlReader.Create("books.xml", settings);  
  
XmlDocument document = new XmlDocument();  
document.Load(reader);  
XPathNavigator navigator = document.CreateNavigator();  
navigator.MoveToChild("books", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("published", "http://www.contoso.com/books");  
  
Console.WriteLine(navigator.SchemaInfo.SchemaType.Name);  
Console.WriteLine(navigator.SchemaInfo.Validity);  
Console.WriteLine(navigator.SchemaInfo.SchemaElement.MinOccurs);  
```  
  
 이 예제에서는 `books.xml` 파일을 입력으로 사용합니다.  
  
```xml  
<books xmlns="http://www.contoso.com/books">  
    <book>  
        <title>Title</title>  
        <price>10.00</price>  
        <published>2003-12-31</published>  
    </book>  
</books>  
```  
  
 이 예제에서는 또한 `books.xsd` 스키마를 입력으로 사용합니다.  
  
```xml  
<xs:schema xmlns="http://www.contoso.com/books"   
attributeFormDefault="unqualified" elementFormDefault="qualified"   
targetNamespace="http://www.contoso.com/books"   
xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:simpleType name="publishedType">  
        <xs:restriction base="xs:date">  
            <xs:minInclusive value="2003-01-01" />  
            <xs:maxInclusive value="2003-12-31" />  
        </xs:restriction>  
    </xs:simpleType>  
    <xs:complexType name="bookType">  
        <xs:sequence>  
            <xs:element name="title" type="xs:string"/>  
            <xs:element name="price" type="xs:decimal"/>  
            <xs:element name="published" type="publishedType"/>  
        </xs:sequence>  
    </xs:complexType>  
    <xs:complexType name="booksType">  
        <xs:sequence>  
            <xs:element name="book" type="bookType" />  
        </xs:sequence>  
    </xs:complexType>  
    <xs:element name="books" type="booksType" />  
</xs:schema>  
```  
  
## <a name="obtain-typed-values-using-valueas-properties"></a>ValueAs 속성을 사용하여 형식화된 값 가져오기  
 <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A>의 <xref:System.Xml.XPath.XPathNavigator> 속성에 액세스하여 형식화된 노드 값을 검색할 수 있습니다. 형식화된 노드 값을 다른 형식으로 변환해야 할 경우가 있습니다. 일반적인 예는 XML 노드로부터 숫자 값을 가져오는 것입니다. 예를 들어, 무효화되고 형식화되지 않은 다음 XML 문서를 살펴보세요.  
  
```xml  
<books>  
    <book>  
        <title>Title</title>  
        <price>10.00</price>  
        <published>2003-12-31</published>  
    </book>  
</books>  
```  
  
 <xref:System.Xml.XPath.XPathNavigator>가 `price` 요소에 있을 경우 <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> 속성은 `null`이 되고 <xref:System.Xml.XPath.XPathNavigator.ValueType%2A> 속성은 <xref:System.String>이 되며 <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> 속성은 문자열 `10.00`이 됩니다.  
  
 그러나 여전히 <xref:System.Xml.XPath.XPathItem.ValueAs%2A>, <xref:System.Xml.XPath.XPathNavigator.ValueAsDouble%2A>, <xref:System.Xml.XPath.XPathNavigator.ValueAsInt%2A> 또는 <xref:System.Xml.XPath.XPathNavigator.ValueAsLong%2A> 같은 메서드 및 속성을 사용하여 숫자 값으로 값을 추출할 수 있습니다. 다음 예제에서는 <xref:System.Xml.XPath.XPathItem.ValueAs%2A> 메서드를 사용하여 이러한 캐스팅을 수행하는 방법을 보여 줍니다.  
  
```vb  
Dim document As New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
navigator.MoveToChild("books", "")  
navigator.MoveToChild("book", "")  
navigator.MoveToChild("price", "")  
  
Dim price = navigator.ValueAs(GetType(Decimal))  
Dim discount As Decimal = 0.2  
  
Console.WriteLine("The price of the book has been dropped 20% from {0:C} to {1:C}", navigator.Value, (price - price * discount))  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
navigator.MoveToChild("books", "");  
navigator.MoveToChild("book", "");  
navigator.MoveToChild("price", "");  
  
Decimal price = (decimal)navigator.ValueAs(typeof(decimal));  
  
Console.WriteLine("The price of the book has been dropped 20% from {0:C} to {1:C}", navigator.Value, (price - price * (decimal)0.20));  
```  
  
 스키마 기본 제공 형식에서 CLR 형식으로 매핑하는 방법에 대한 자세한 내용은 [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 노드 집합 탐색](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 특성 및 네임스페이스 노드 탐색](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 추출](../../../../docs/standard/data/xml/extract-xml-data-using-xpathnavigator.md)
