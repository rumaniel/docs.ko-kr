---
title: XPathNavigator를 사용하여 XML 데이터 수정
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 03a7c5a1-b296-4af4-b209-043c958dc0a5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ba6393d19909d8be762ee38b4c925987528d6304
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967347"
---
# <a name="modify-xml-data-using-xpathnavigator"></a>XPathNavigator를 사용하여 XML 데이터 수정
<xref:System.Xml.XPath.XPathNavigator> 클래스는 XML 문서에서 노드와 값을 수정하는 메서드 집합을 제공합니다. 이러한 메서드를 사용하려면 <xref:System.Xml.XPath.XPathNavigator> 개체가 편집 가능한 상태여야 합니다. 즉, <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 속성이 `true`여야 합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 클래스의 <xref:System.Xml.XmlDocument.CreateNavigator%2A> 메서드에서는 XML 문서를 편집할 수 있는 <xref:System.Xml.XmlDocument> 개체를 만듭니다. <xref:System.Xml.XPath.XPathNavigator> 클래스에서 만든 <xref:System.Xml.XPath.XPathDocument> 개체는 읽기 전용이며, <xref:System.Xml.XPath.XPathNavigator> 개체에서 만든 <xref:System.Xml.XPath.XPathDocument> 개체의 편집 메서드를 사용하려고 하면 <xref:System.NotSupportedException>이 발생합니다.  
  
 편집 가능한 <xref:System.Xml.XPath.XPathNavigator> 개체를 만드는 방법에 대한 자세한 내용은 [XPathDocument 및 XmlDocument를 사용하여 XML 데이터 읽기](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)를 참조하세요.  
  
## <a name="modifying-nodes"></a>노드 수정  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 메서드를 사용하면 쉽게 노드 값을 변경할 수 있습니다.  
  
 다음 표에서는 여러 노드 형식에서 이러한 메서드를 사용한 결과를 보여 줍니다.  
  
|<xref:System.Xml.XPath.XPathNodeType>|변경되는 데이터|  
|---------------------------------------------------------------------------------------------------------------------------------------------|------------------|  
|<xref:System.Xml.XPath.XPathNodeType.Root>|지원되지 않습니다.|  
|<xref:System.Xml.XPath.XPathNodeType.Element>|요소 내용입니다.|  
|<xref:System.Xml.XPath.XPathNodeType.Attribute>|특성 값|  
|<xref:System.Xml.XPath.XPathNodeType.Text>|텍스트 내용입니다.|  
|<xref:System.Xml.XPath.XPathNodeType.ProcessingInstruction>|대상을 제외한 내용|  
|<xref:System.Xml.XPath.XPathNodeType.Comment>|주석의 내용입니다.|  
|<xref:System.Xml.XPath.XPathNodeType.Namespace>|지원되지 않음|  
  
> [!NOTE]
> <xref:System.Xml.XPath.XPathNodeType.Namespace> 노드나 <xref:System.Xml.XPath.XPathNodeType.Root> 노드를 편집할 수 없습니다.  
  
 또한 <xref:System.Xml.XPath.XPathNavigator> 클래스는 노드를 삽입하고 제거하는 메서드 집합을 제공합니다. XML 문서에서 노드를 삽입하고 제거하는 방법에 대한 자세한 내용은 [XPathNavigator를 사용하여 XML 데이터 삽입](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md) 및 [XPathNavigator를 사용하여 XML 데이터 제거](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md) 항목을 참조하세요.  
  
### <a name="modifying-untyped-values"></a>형식화되지 않은 값 수정  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 메서드는 형식화되지 않은 `string` 값을 간단히 삽입합니다. 이 값은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 노드의 값인 매개 변수로서 전달됩니다. 이 값은 스키마 정보를 사용할 수 있을 경우 노드 형식에 따라 새 값이 유효한지 여부를 확인하지 않거나 특정한 형식 없이 삽입됩니다.  
  
 다음 예제에서는 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 메서드를 사용하여 `price` 파일의 모든 `contosoBooks.xml` 요소를 업데이트할 수 있습니다.  
  
 [!code-cpp[XPathNavigatorMethods#47](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#47)]
 [!code-csharp[XPathNavigatorMethods#47](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#47)]
 [!code-vb[XPathNavigatorMethods#47](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#47)]  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### <a name="modifying-typed-values"></a>형식화된 값 수정  
 노드의 형식이 W3C XML 스키마 단순 형식이면 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 메서드에서 삽입한 새 값은 설정되기 전에 단순 형식의 패싯에 대해 검사됩니다. 노드의 형식에 따라 새 값이 유효하지 않은 경우, 예를 들면 `-1` 형식의 요소에 `xs:positiveInteger`의 값을 설정하는 경우에는 예외가 발생합니다.  
  
 다음 예제에서는 `price` 파일에 있는 첫 번째 `book` 요소의 `contosoBooks.xml` 요소 값을 <xref:System.DateTime> 값으로 변경합니다. `price` 요소의 XML 스키마 형식은 `xs:decimal` 파일의 `contosoBooks.xsd`로 정의되므로 예외가 발생합니다.  
  
```vb  
Dim settings As XmlReaderSettings = New XmlReaderSettings()  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
settings.ValidationType = ValidationType.Schema  
  
Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
Dim document As XmlDocument = New XmlDocument()  
document.Load(reader)  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.SetTypedValue(DateTime.Now)  
```  
  
```csharp  
XmlReaderSettings settings = new XmlReaderSettings();  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
settings.ValidationType = ValidationType.Schema;  
  
XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
XmlDocument document = new XmlDocument();  
document.Load(reader);  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.SetTypedValue(DateTime.Now);  
```  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 이 예제에서는 또한 `contosoBooks.xsd`를 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
#### <a name="the-effects-of-editing-strongly-typed-xml-data"></a>강력한 형식의 XML 데이터를 편집한 결과  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 W3C XML 스키마를 사용해 강력한 형식의 XML을 설명합니다. W3C XML 스키마 문서에 대한 유효성 검사를 기반으로 요소 및 특성에 형식 정보로 주석을 추가할 수 있습니다. 다른 요소나 특성을 포함할 수 있는 요소를 복합 형식이라고 하며 텍스트 내용만 포함할 수 있는 요소를 단순 형식이라고 합니다.  
  
> [!NOTE]
> 특성에는 단순 형식만 있을 수 있습니다.  
  
 특성이나 요소가 해당 형식 정의와 관련된 모든 규칙을 준수하는 경우 이 특성이나 요소는 스키마에 대해 유효한 것으로 간주될 수 있습니다. 스키마에 대해 유효하려면 단순 형식 `xs:int`가 포함된 요소에는 -2147483648에서 2147483647까지의 숫자 값이 포함되어야 합니다. 복합 형식의 경우 요소의 스키마 유효성 검사는 자식 요소 및 특성의 스키마 유효성 검사에 따라 결정됩니다. 그러므로 요소가 복합 형식 정의에 대해 유효할 경우 모든 자식 요소 및 특성은 해당 형식 정의에 대해 유효합니다. 마찬가지로 요소의 자식 요소 또는 특성 중 하나라도 형식 정의에 대해 유효하지 않을 경우 또는 유효성을 알 수 없는 경우 해당 요소도 유효하지 않거나 요소의 유효성을 알 수 없습니다.  
  
 요소의 유효성이 자식 요소 및 특성의 유효성에 따라 결정되는 경우 자식 요소나 특성을 수정하면 요소가 이전에 유효했더라도 요소의 유효성이 변경됩니다. 특히 요소의 자식 요소 또는 특성을 삽입, 업데이트 또는 삭제할 경우 요소의 유효성을 알 수 없습니다. 요소의 유효성은 요소의 <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> 속성의 <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> 속성을 <xref:System.Xml.Schema.XmlSchemaValidity.NotKnown>으로 설정하여 나타낼 수 있습니다. 더욱이 요소의 부모 요소, 이 부모 요소의 부모 요소 등의 유효성도 알 수 없기 때문에 이 결과는 XML 문서에서 재귀적 상향 계단식으로 나타납니다.  
  
 스키마 유효성 검사 및 <xref:System.Xml.XPath.XPathNavigator> 클래스에 대한 자세한 내용은 [XPathNavigator를 사용하여 스키마 유효성 검사](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)를 참조하세요.  
  
### <a name="modifying-attributes"></a>특성 수정  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 및 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 메서드를 사용하여 형식화되지 않은 특성 노드와 형식화된 특성 노드 및 "노드 수정" 단원에 나열된 기타 노드 형식을 수정할 수 있습니다.  
  
 다음 예제에서는 `genre` 파일에서 첫 번째 `book` 요소의 `books.xml` 특성 값을 변경합니다.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", String.Empty)  
navigator.MoveToChild("book", String.Empty)  
navigator.MoveToAttribute("genre", String.Empty)  
  
navigator.SetValue("non-fiction")  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", String.Empty);  
navigator.MoveToChild("book", String.Empty);  
navigator.MoveToAttribute("genre", String.Empty);  
  
navigator.SetValue("non-fiction");  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 및 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 메서드에 대한 자세한 내용은 "형식화되지 않은 값 수정" 및 "형식화된 값 수정" 단원을 참조하세요.  
  
## <a name="innerxml-and-outerxml-properties"></a>InnerXml 및 OuterXml 속성  
 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 노드의 XML 태그를 변경합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 자식 노드의 XML 태그를 주어진 XML `string`의 구문 분석된 내용과 함께 변경합니다. 마찬가지로, <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 자식 노드의 XML 태그뿐만 아니라 현재 노드 자체도 변경합니다.  
  
 다음 예제에서는 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성을 사용하여 `price` 요소 값을 수정하고 `discount` 파일의 첫 번째 `book` 요소에 새 `contosoBooks.xml` 특성을 삽입합니다.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml");  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>"  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("contosoBooks.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>";  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
## <a name="modifying-namespace-nodes"></a>네임스페이스 노드 수정  
 DOM(문서 개체 모델)에서 네임스페이스 선언은 삽입, 업데이트 및 삭제할 수 있는 정규 특성으로 간주됩니다. 다음 예제와 같이 네임스페이스 노드 값을 변경하면 네임스페이스 노드 범위 내에 있는 요소 및 특성의 ID가 변경될 수 있으므로 <xref:System.Xml.XPath.XPathNavigator> 클래스는 네임스페이스 노드에서 이러한 작업을 허용하지 않습니다.  
  
```xml  
<root xmlns="http://www.contoso.com">  
    <child />  
</root>  
```  
  
 다음과 같은 방법으로 위의 XML 예제를 변경하면 각 요소의 네임스페이스 URI 값이 변경되기 때문에 문서에서 모든 요소의 이름을 효과적으로 바꿀 수 있습니다.  
  
```xml  
<root xmlns="urn:contoso.com">  
    <child />  
</root>  
```  
  
 <xref:System.Xml.XPath.XPathNavigator> 클래스에서는 삽입하는 범위에서 네임스페이스 선언과 충돌하지 않는 네임스페이스 노드를 삽입할 수 있습니다. 이러한 경우 XML 문서의 더 낮은 범위에서는 이 네임스페이스가 선언되지 않으며 다음 예제와 같이 이름이 바뀌지 않습니다.  
  
```xml  
<root xmlns:a="http://www.contoso.com">  
    <parent>  
        <a:child />  
    </parent>  
</root>  
```  
  
 다음과 같은 방법으로 위의 XML 예제를 변경하면 XML 문서에서 다른 네임스페이스 선언의 범위 아래에 네임스페이스 선언이 올바르게 전파됩니다.  
  
```xml  
<root xmlns:a="http://www.contoso.com">  
    <parent a:parent-id="1234" xmlns:a="http://www.contoso.com/parent-id">  
        <a:child xmlns:a="http://www.contoso.com/">  
    </parent>  
</root>  
```  
  
 위 XML 예제에서는 `a:parent-id` 네임스페이스의 `parent` 요소에 `http://www.contoso.com/parent-id` 특성을 삽입합니다. <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> 요소에서 `parent` 메서드를 사용하여 특성을 삽입할 수 있습니다. `http://www.contoso.com` 클래스에서 <xref:System.Xml.XPath.XPathNavigator> 네임스페이스 선언을 자동으로 삽입하여 XML 문서 나머지 부분의 일관성을 유지합니다.  
  
## <a name="modifying-entity-reference-nodes"></a>엔터티 참조 노드 수정  
 <xref:System.Xml.XmlDocument> 개체의 엔터티 참조 노드는 읽기 전용이므로 <xref:System.Xml.XPath.XPathNavigator> 또는 <xref:System.Xml.XmlNode> 클래스를 사용하여 편집할 수 없습니다. 엔터티 참조 노드를 수정하려고 시도하면 <xref:System.InvalidOperationException>이 발생합니다.  
  
## <a name="modifying-xsinil-nodes"></a>xsi:nil 노드 수정  
 W3C XML 스키마 권장 사항에는 nillable 요소의 개념이 새로 추가되었습니다. nillable 요소는 내용이 없고 여전히 유효할 수 있습니다. nillable 요소의 개념은 `null`인 개체의 개념과 비슷합니다. 주요 차이점은 `null` 개체에는 액세스할 수 없으며 `xsi:nil` 요소에는 액세스할 수 있지만 자식 요소나 텍스트 등의 내용이 없는 특성과 같은 속성이 있다는 점입니다. XML 문서의 요소에서 `xsi:nil` 값의 `true` 특성을 사용하여 요소에 내용이 없음을 나타낼 수 있습니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 개체를 사용하여 `xsi:nil` 값의 `true` 특성이 있는 유효한 요소에 내용을 추가하는 경우 `xsi:nil` 특성 값은 `false`로 설정됩니다.  
  
> [!NOTE]
> `xsi:nil` 특성이 `false`로 설정된 요소의 내용을 삭제하면 이 특성 값은 `true`로 변경되지 않습니다.  
  
## <a name="saving-an-xml-document"></a>XML 문서 저장  
 <xref:System.Xml.XmlDocument> 클래스의 메서드를 사용하면 <xref:System.Xml.XmlDocument> 개체에서 변경된 내용을 이 항목에서 설명하는 편집 메서드의 결과로 저장할 수 있습니다. <xref:System.Xml.XmlDocument> 개체에서 변경된 내용을 저장하는 방법에 대한 자세한 내용은 [문서 작성 및 저장](../../../../docs/standard/data/xml/saving-and-writing-a-document.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XML 데이터 삽입](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 제거](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md)
