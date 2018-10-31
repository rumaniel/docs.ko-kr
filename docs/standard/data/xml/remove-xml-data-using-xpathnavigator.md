---
title: XPathNavigator를 사용하여 XML 데이터 제거
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 9f436bca-1b96-494b-a6d2-e102c7551752
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1827e40256bc4307006ce081cbb6cbc44a89a0bc
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48837273"
---
# <a name="remove-xml-data-using-xpathnavigator"></a>XPathNavigator를 사용하여 XML 데이터 제거
<xref:System.Xml.XPath.XPathNavigator> 클래스는 XML 문서에서 노드와 값을 제거하는 메서드 집합을 제공합니다. 이러한 메서드를 사용하려면 <xref:System.Xml.XPath.XPathNavigator> 개체가 편집 가능한 상태여야 합니다. 즉, <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 속성이 `true`여야 합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 클래스의 <xref:System.Xml.XmlDocument.CreateNavigator%2A> 메서드에서는 XML 문서를 편집할 수 있는 <xref:System.Xml.XmlDocument> 개체를 만듭니다. <xref:System.Xml.XPath.XPathNavigator> 클래스에서 만든 <xref:System.Xml.XPath.XPathDocument> 개체는 읽기 전용이며, <xref:System.Xml.XPath.XPathNavigator> 개체에서 만든 <xref:System.Xml.XPath.XPathDocument> 개체의 편집 메서드를 사용하려고 하면 <xref:System.NotSupportedException>이 발생합니다.  
  
 편집 가능한 <xref:System.Xml.XPath.XPathNavigator> 개체를 만드는 방법에 대한 자세한 내용은 [XPathDocument 및 XmlDocument를 사용하여 XML 데이터 읽기](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)를 참조하세요.  
  
## <a name="removing-nodes"></a>노드 제거  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 XML 문서에서 노드를 제거하는 <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> 메서드를 제공합니다.  
  
### <a name="removing-a-node"></a>노드 제거  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 XML 문서에서 <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> 개체가 현재 위치하고 있는 현재 노드를 삭제하는 <xref:System.Xml.XPath.XPathNavigator> 메서드를 제공합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> 메서드를 사용하여 노드를 삭제한 후에는 더 이상 <xref:System.Xml.XmlDocument> 개체의 루트에서 이 노드에 연결할 수 없습니다. 노드를 삭제한 후 <xref:System.Xml.XPath.XPathNavigator>는 삭제된 노드의 부모 노드에 배치됩니다.  
  
 노드를 삭제해도 삭제된 노드에 위치한 <xref:System.Xml.XPath.XPathNavigator> 개체의 위치에는 영향을 주지 않습니다. 이러한 <xref:System.Xml.XPath.XPathNavigator> 개체는 삭제된 하위 트리 내에서 이동할 수 있다는 점에서 유효하지만 <xref:System.Xml.XPath.XPathNavigator> 클래스의 일반 노드 집합 탐색 메서드를 사용하여 기본 노드 트리로 이동할 수 없습니다.  
  
> [!NOTE]
>  <xref:System.Xml.XPath.XPathNavigator.MoveTo%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator> 메서드를 사용하여 이러한 <xref:System.Xml.XPath.XPathNavigator> 개체를 다시 기본 노드 트리로 이동하거나 기본 노드 트리에서 삭제된 하위 트리로 이동할 수 있습니다.  
  
 다음 예제에서는 `price` 메서드를 사용하여 `book` 파일의 첫 번째 `contosoBooks.xml` 요소에서 <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> 요소를 삭제합니다. <xref:System.Xml.XPath.XPathNavigator> 요소를 삭제한 후 `price` 개체는 부모 `book` 요소에 배치됩니다.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.DeleteSelf()  
  
Console.WriteLine("Position after delete: {0}", navigator.Name)  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("contosoBooks.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.DeleteSelf();  
  
Console.WriteLine("Position after delete: {0}", navigator.Name);  
Console.WriteLine(navigator.OuterXml);  
```  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### <a name="removing-an-attribute-node"></a>특성 노드 제거  
 <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> 메서드를 사용하여 XML 문서에서 특성 노드를 삭제할 수 있습니다.  
  
 특성 노드를 삭제한 후에는 더 이상 <xref:System.Xml.XmlDocument> 개체의 루트 노드에서 이 노드에 연결할 수 없으며 <xref:System.Xml.XPath.XPathNavigator> 개체는 부모 요소에 배치됩니다.  
  
#### <a name="default-attributes"></a>기본 특성  
 특성을 제거하는 데 사용한 메서드와 상관없이 XML 문서의 DTD 또는 XML 스키마에 기본 특성으로 정의된 특성을 제거할 때는 특별한 제한 사항이 있습니다. 기본 특성이 속해 있는 요소도 제거해야 기본 특성을 제거할 수 있습니다. 기본 특성을 선언한 요소에 대해 기본 특성이 항상 있으므로 결과적으로 기본 특성을 삭제하면 대체 특성이 요소에 삽입되고 선언된 기본값으로 초기화됩니다.  
  
## <a name="removing-values"></a>값 제거  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 XML 문서에서 형식화되지 않은 값과 형식화된 값을 제거하는 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 및 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 메서드를 제공합니다.  
  
### <a name="removing-untyped-values"></a>형식화되지 않은 값 제거  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 메서드는 형식화되지 않은 `string` 값을 간단히 삽입합니다. 이 값은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 노드의 값인 매개 변수로서 전달됩니다. 빈 문자열을 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 메서드에 전달하면 현재 노드 값이 제거됩니다.  
  
 다음 예제에서는 `price` 메서드를 사용하여 `book` 파일에서 첫 번째 `contosoBooks.xml` 요소의 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 요소 값을 제거합니다.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.SetValue("")  
  
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
  
navigator.SetValue("");  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### <a name="removing-typed-values"></a>형식화된 값 제거  
 노드의 형식이 W3C XML 스키마 단순 형식이면 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 메서드에서 삽입한 새 값은 설정되기 전에 단순 형식의 패싯에 대해 검사됩니다. 노드의 형식에 따라 새 값이 유효하지 않은 경우, 예를 들면 `-1` 형식의 요소에 `xs:positiveInteger`의 값을 설정하는 경우에는 예외가 발생합니다. 또한 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A>을 매개 변수로 `null` 메서드에 전달할 수 없습니다. 결과적으로 형식화된 노드 값을 제거하려면 노드의 스키마 형식을 따라야 합니다.  
  
 다음 예제에서는 값을 `price`으로 설정하여 `book` 메서드로 `contosoBooks.xml` 파일에서 첫 번째 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 요소의 `0` 요소 값을 제거합니다. 노드 값은 제거되지 않지만 `xs:decimal`의 데이터 형식에 따라 책 가격이 제거됩니다.  
  
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
  
navigator.SetTypedValue(0)  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
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
  
navigator.SetTypedValue(0);  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
## <a name="namespace-nodes"></a>네임스페이스 노드  
 <xref:System.Xml.XmlDocument> 개체에서 네임스페이스 노드를 삭제할 수 없습니다. <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> 메서드를 사용하여 네임스페이스 노드를 삭제하려고 시도하면 예외가 발생합니다.  
  
## <a name="the-innerxml-and-outerxml-properties"></a>InnerXml 및 OuterXml 속성  
 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 노드의 XML 태그를 변경합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 자식 노드의 XML 태그를 주어진 XML `string`의 구문 분석된 내용과 함께 변경합니다. 마찬가지로, <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 자식 노드의 XML 태그뿐만 아니라 현재 노드 자체도 변경합니다.  
  
 이 항목에 설명된 메서드 외에도 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 및 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성을 사용하여 XML 문서에서 노드와 값을 제거할 수 있습니다. <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 및 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성을 사용하여 노드를 수정하는 방법에 대한 자세한 내용은 [XPathNavigator를 사용하여 XML 데이터 수정](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md) 항목을 참조하세요.  
  
## <a name="saving-an-xml-document"></a>XML 문서 저장  
 <xref:System.Xml.XmlDocument> 클래스의 메서드를 사용하면 <xref:System.Xml.XmlDocument> 개체에서 변경된 내용을 이 항목에서 설명하는 메서드의 결과로 저장할 수 있습니다. <xref:System.Xml.XmlDocument> 개체에서 변경된 내용을 저장하는 방법에 대한 자세한 내용은 [문서 작성 및 저장](../../../../docs/standard/data/xml/saving-and-writing-a-document.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>  
- <xref:System.Xml.XPath.XPathDocument>  
- <xref:System.Xml.XPath.XPathNavigator>  
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
- [XPathNavigator를 사용하여 XML 데이터 삽입](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md)  
- [XPathNavigator를 사용하여 XML 데이터 수정](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md)
