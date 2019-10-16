---
title: XPathNavigator를 사용하여 XML 데이터 삽입
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 2ed8c28b-b88d-4be7-9c87-92df01f0821f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4ff9232272124c8706e64162d096eced8640c806
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966962"
---
# <a name="insert-xml-data-using-xpathnavigator"></a>XPathNavigator를 사용하여 XML 데이터 삽입
<xref:System.Xml.XPath.XPathNavigator> 클래스는 XML 문서에 형제, 자식 및 특성 노드를 삽입하는 메서드 집합을 제공합니다. 이러한 메서드를 사용하려면 <xref:System.Xml.XPath.XPathNavigator> 개체가 편집 가능한 상태여야 합니다. 즉, <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 속성이 `true`여야 합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 클래스의 <xref:System.Xml.XmlDocument.CreateNavigator%2A> 메서드에서는 XML 문서를 편집할 수 있는 <xref:System.Xml.XmlDocument> 개체를 만듭니다. <xref:System.Xml.XPath.XPathNavigator> 클래스에서 만든 <xref:System.Xml.XPath.XPathDocument> 개체는 읽기 전용이며, <xref:System.Xml.XPath.XPathNavigator> 개체에서 만든 <xref:System.Xml.XPath.XPathDocument> 개체의 편집 메서드를 사용하려고 하면 <xref:System.NotSupportedException>이 발생합니다.  
  
 편집 가능한 <xref:System.Xml.XPath.XPathNavigator> 개체를 만드는 방법에 대한 자세한 내용은 [XPathDocument 및 XmlDocument를 사용하여 XML 데이터 읽기](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)를 참조하세요.  
  
## <a name="inserting-nodes"></a>노드 삽입  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 XML 문서에 형제, 자식 및 특성 노드를 삽입하는 메서드를 제공합니다. 이러한 메서드를 사용하여 <xref:System.Xml.XPath.XPathNavigator> 개체의 현재 위치와 관련된 여러 위치에 노드와 특성을 삽입할 수 있습니다. 이 메서드에 대한 자세한 내용은 다음 단원을 참조하세요.  
  
### <a name="inserting-sibling-nodes"></a>형제 노드 삽입  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 다음과 같은 메서드를 통해 형제 노드를 삽입합니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.InsertElementAfter%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.InsertElementBefore%2A>  
  
 이러한 메서드는 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 배치되어 있는 노드의 앞뒤에 형제 노드를 삽입합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A> 및 <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A> 메서드가 오버로드되며 `string`, <xref:System.Xml.XmlReader> 개체 또는 추가할 형제 노드가 포함된 <xref:System.Xml.XPath.XPathNavigator> 개체를 매개 변수로 허용합니다. 또한 두 메서드는 형제 노드를 삽입하는 데 사용하는 <xref:System.Xml.XmlWriter> 개체를 반환합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.InsertElementAfter%2A> 및 <xref:System.Xml.XPath.XPathNavigator.InsertElementBefore%2A> 메서드는 네임스페이스 접두사, 로컬 이름, 네임스페이스 URI 및 매개 변수로 지정된 값을 사용하여 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 배치되어 있는 노드 앞뒤에 단일 형제 노드를 삽입합니다.  
  
 다음 예제에서는 `pages` 파일에서 첫 번째 `price` 요소의 `book` 자식 요소 앞에 새 `contosoBooks.xml` 요소를 삽입합니다.  
  
 [!code-cpp[XPathNavigatorMethods#19](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#19)]
 [!code-csharp[XPathNavigatorMethods#19](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#19)]
 [!code-vb[XPathNavigatorMethods#19](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#19)]  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertElementAfter%2A> 및 <xref:System.Xml.XPath.XPathNavigator.InsertElementBefore%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.XPath.XPathNavigator> 클래스 참조 문서를 참조하세요.  
  
### <a name="inserting-child-nodes"></a>자식 노드 삽입  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 다음과 같은 메서드를 통해 자식 노드를 삽입합니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.AppendChildElement%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.PrependChildElement%2A>  
  
 이러한 메서드는 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 배치되어 있는 노드의 자식 노드 목록 시작과 끝 부분에 자식 노드를 추가합니다.  
  
 "형제 노드 삽입" 단원의 메서드와 마찬가지로 <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A> 및 <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A> 메서드는 `string`, <xref:System.Xml.XmlReader> 개체 또는 추가할 자식 노드가 포함된 <xref:System.Xml.XPath.XPathNavigator> 개체를 매개 변수로 허용합니다. 또한 두 메서드는 자식 노드를 삽입하는 데 사용하는 <xref:System.Xml.XmlWriter> 개체를 반환합니다.  
  
 또한 "형제 노드 삽입" 단원의 메서드와 같이 <xref:System.Xml.XPath.XPathNavigator.AppendChildElement%2A> 및 <xref:System.Xml.XPath.XPathNavigator.PrependChildElement%2A> 메서드는 네임스페이스 접두사, 로컬 이름, 네임스페이스 URI 및 매개 변수로 지정된 값을 사용하여 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 배치되어 있는 노드의 자식 노드 목록 시작과 끝 부분에 단일 자식 노드를 삽입합니다.  
  
 다음 예제에서는 `pages` 파일에서 첫 번째 `book` 요소의 자식 요소 목록에 새 `contosoBooks.xml` 자식 요소를 추가합니다.  
  
 [!code-cpp[XPathNavigatorMethods#2](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#2)]
 [!code-csharp[XPathNavigatorMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#2)]
 [!code-vb[XPathNavigatorMethods#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#2)]  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>, <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A>, <xref:System.Xml.XPath.XPathNavigator.AppendChildElement%2A> 및 <xref:System.Xml.XPath.XPathNavigator.PrependChildElement%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.XPath.XPathNavigator> 클래스 참조 문서를 참조하세요.  
  
### <a name="inserting-attribute-nodes"></a>특성 노드 삽입  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 다음과 같은 메서드를 통해 특성 노드를 삽입합니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A>  
  
 이러한 메서드는 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 배치되어 있는 요소 노드에 특성 노드를 삽입합니다. <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> 메서드는 네임스페이스 접두사, 로컬 이름, 네임스페이스 URI 및 매개 변수로 지정된 값을 사용하여 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 배치되어 있는 요소 노드에 특성 노드를 만듭니다. <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A> 메서드는 특성 노드를 삽입하는 데 사용하는 <xref:System.Xml.XmlWriter> 개체를 반환합니다.  
  
 다음 예제에서는 `discount` 메서드에서 반환된 `currency` 개체를 사용하여 `price` 파일에서 첫 번째 `book` 요소의 `contosoBooks.xml` 자식 요소에 새 <xref:System.Xml.XmlWriter> 및 <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A> 특성을 만듭니다.  
  
 [!code-cpp[XPathNavigatorMethods#8](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#8)]
 [!code-csharp[XPathNavigatorMethods#8](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#8)]
 [!code-vb[XPathNavigatorMethods#8](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#8)]  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> 및 <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.XPath.XPathNavigator> 클래스 참조 문서를 참조하세요.  
  
## <a name="copying-nodes"></a>노드 복사  
 다른 XML 문서의 내용으로 XML 문서를 채워야 할 경우가 있습니다. <xref:System.Xml.XPath.XPathNavigator> 클래스와 <xref:System.Xml.XmlWriter> 클래스는 기존 <xref:System.Xml.XmlDocument> 개체 또는 <xref:System.Xml.XmlReader> 개체에서 <xref:System.Xml.XPath.XPathNavigator> 개체에 노드를 복사합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 메서드는 모두 오버로드되며 <xref:System.Xml.XPath.XPathNavigator> 개체나 <xref:System.Xml.XmlReader> 개체를 매개 변수로 허용합니다.  
  
 <xref:System.Xml.XmlWriter.WriteNode%2A> 클래스의 <xref:System.Xml.XmlWriter> 메서드는 오버로드되며 <xref:System.Xml.XmlNode>, <xref:System.Xml.XmlReader> 또는 <xref:System.Xml.XPath.XPathNavigator> 개체를 허용합니다.  
  
 다음 예제에서는 문서의 모든 `book` 요소를 다른 문서로 복사합니다.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", String.Empty)  
  
Dim newBooks As XPathDocument = New XPathDocument("newBooks.xml")  
Dim newBooksNavigator As XPathNavigator = newBooks.CreateNavigator()  
  
Dim nav As XPathNavigator  
For Each nav in newBooksNavigator.SelectDescendants("book", "", false)  
    navigator.AppendChild(nav)  
Next  
  
document.Save("newBooks.xml");  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", String.Empty);  
  
XPathDocument newBooks = new XPathDocument("newBooks.xml");  
XPathNavigator newBooksNavigator = newBooks.CreateNavigator();  
  
foreach (XPathNavigator nav in newBooksNavigator.SelectDescendants("book", "", false))  
{  
    navigator.AppendChild(nav);  
}  
  
document.Save("newBooks.xml");  
```  
  
## <a name="inserting-values"></a>값 삽입  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 노드 값을 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 개체에 삽입하는 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 및 <xref:System.Xml.XmlDocument> 메서드를 제공합니다.  
  
### <a name="inserting-untyped-values"></a>형식화되지 않은 값 삽입  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 메서드는 형식화되지 않은 `string` 값을 간단히 삽입합니다. 이 값은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 노드의 값인 매개 변수로서 전달됩니다. 이 값은 스키마 정보를 사용할 수 있을 경우 노드 형식에 따라 새 값이 유효한지 여부를 확인하지 않거나 특정한 형식 없이 삽입됩니다.  
  
 다음 예제에서는 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 메서드를 사용하여 `price` 파일의 모든 `contosoBooks.xml` 요소를 업데이트할 수 있습니다.  
  
 [!code-cpp[XPathNavigatorMethods#47](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#47)]
 [!code-csharp[XPathNavigatorMethods#47](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#47)]
 [!code-vb[XPathNavigatorMethods#47](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#47)]  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### <a name="inserting-typed-values"></a>형식화된 값 삽입  
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
  
## <a name="the-innerxml-and-outerxml-properties"></a>InnerXml 및 OuterXml 속성  
 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 노드의 XML 태그를 변경합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 자식 노드의 XML 태그를 주어진 XML `string`의 구문 분석된 내용과 함께 변경합니다. 마찬가지로, <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 현재 위치하는 자식 노드의 XML 태그뿐만 아니라 현재 노드 자체도 변경합니다.  
  
 이 항목에 설명된 메서드 외에도 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 및 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성을 사용하여 XML 문서에 노드와 값을 삽입할 수 있습니다. <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 및 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 속성을 사용하여 노드와 값을 삽입하는 방법에 대한 자세한 내용은 [XPathNavigator를 사용하여 XML 데이터 수정](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md) 항목을 참조하세요.  
  
## <a name="namespace-and-xmllang-conflicts"></a>네임스페이스와 xml:lang 충돌  
 `xml:lang` 개체를 매개 변수로 사용하는 <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A>, <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>, <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 메서드를 통해 XML 데이터를 삽입하면 네임스페이스 및 <xref:System.Xml.XmlReader> 선언의 범위와 관련된 충돌이 발생할 수 있습니다.  
  
 다음은 발생할 수 있는 네임스페이스 충돌입니다.  
  
- <xref:System.Xml.XmlReader> 개체의 컨텍스트에 네임스페이스 URI 접두사 매핑이 없을 경우 <xref:System.Xml.XPath.XPathNavigator> 개체의 컨텍스트 범위 내에 네임스페이스가 있으면 새로 삽입된 노드에 새 네임스페이스 선언이 추가됩니다.  
  
- <xref:System.Xml.XmlReader> 개체의 컨텍스트와 <xref:System.Xml.XPath.XPathNavigator> 개체의 컨텍스트 내에서 같은 네임스페이스 URI가 범위 내에 있지만 두 컨텍스트에서 다른 접두사가 매핑된 경우 새로 삽입된 노드에 새 네임스페이스 선언이 추가되고 <xref:System.Xml.XmlReader> 개체의 접두사와 네임스페이스 URI가 사용됩니다.  
  
- <xref:System.Xml.XmlReader> 개체의 컨텍스트와 <xref:System.Xml.XPath.XPathNavigator> 개체의 컨텍스트 내에서 같은 네임스페이스 접두사가 범위 내에 있지만 두 컨텍스트에 다른 네임스페이스 URI가 매핑된 경우 새로 삽입된 노드에 새 네임스페이스 선언이 추가되며 접두사가 다시 선언되고 <xref:System.Xml.XmlReader> 개체의 네임스페이스 URI가 사용됩니다.  
  
- <xref:System.Xml.XmlReader> 개체의 컨텍스트와 <xref:System.Xml.XPath.XPathNavigator> 개체의 컨텍스트에서 네임스페이스 URI와 접두사가 같을 경우 새로 삽입된 노드에 새 네임스페이스 선언이 추가되지 않습니다.  
  
> [!NOTE]
> 위 설명은 기본 네임스페이스 선언과 같이 접두사로 빈 `string`이 있는 네임스페이스 선언에도 적용됩니다.  
  
 다음은 발생할 수 있는 `xml:lang` 충돌입니다.  
  
- `xml:lang` 개체의 컨텍스트 내 범위에 <xref:System.Xml.XmlReader> 특성이 있지만 <xref:System.Xml.XPath.XPathNavigator> 개체의 컨텍스트에는 없을 경우 `xml:lang` 개체에서 값을 가져오는 <xref:System.Xml.XmlReader> 특성이 새로 삽입된 노드에 추가됩니다.  
  
- `xml:lang` 개체의 컨텍스트와 <xref:System.Xml.XmlReader> 개체의 컨텍스트 내 범위에 <xref:System.Xml.XPath.XPathNavigator> 특성이 있지만 각각 값이 다를 경우 `xml:lang` 개체에서 값을 가져오는 <xref:System.Xml.XmlReader> 특성이 새로 삽입된 노드에 추가됩니다.  
  
- `xml:lang` 개체의 컨텍스트와 <xref:System.Xml.XmlReader> 개체의 컨텍스트 내 범위에 <xref:System.Xml.XPath.XPathNavigator> 특성이 있고 값이 같을 경우 새로 삽입된 노드에 새 `xml:lang` 특성이 추가되지 않습니다.  
  
- `xml:lang` 개체의 컨텍스트 내 범위에 <xref:System.Xml.XPath.XPathNavigator> 특성이 있지만 <xref:System.Xml.XmlReader> 개체의 컨텍스트에는 없을 경우 새로 삽입된 노드에 `xml:lang` 특성이 추가되지 않습니다.  
  
## <a name="inserting-nodes-with-xmlwriter"></a>XmlWriter를 사용하여 노드 삽입  
 "노드 및 값 삽입" 단원에 설명된 형제, 자식 및 특성 노드를 삽입하는 데 사용하는 메서드는 오버로드됩니다. <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>, <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>, <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A>, <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 메서드는 노드를 삽입하는 데 사용하는 <xref:System.Xml.XmlWriter> 개체를 반환합니다.  
  
### <a name="unsupported-xmlwriter-methods"></a>지원되지 않는 XmlWriter 메서드  
 <xref:System.Xml.XmlWriter> 클래스를 통해 XML 문서에 정보를 작성하는 데 사용되는 메서드 중 일부는 XPath 데이터 모델과 DOM(문서 개체 모델)의 차이로 인해 <xref:System.Xml.XPath.XPathNavigator> 클래스에서 지원되지 않습니다.  
  
 다음 표에서는 <xref:System.Xml.XmlWriter> 클래스에서 지원하지 않는 <xref:System.Xml.XPath.XPathNavigator> 클래스 메서드에 대해 설명합니다.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.XmlWriter.WriteEntityRef%2A>|<xref:System.NotSupportedException> 예외를 throw합니다.|  
|<xref:System.Xml.XmlWriter.WriteDocType%2A>|루트 수준에서 무시되며 XML 문서의 다른 수준에서 호출할 경우 <xref:System.NotSupportedException> 예외가 throw됩니다.|  
|<xref:System.Xml.XmlWriter.WriteCData%2A>|해당 문자의 <xref:System.Xml.XmlWriter.WriteString%2A> 메서드에 대한 호출로 처리됩니다.|  
|<xref:System.Xml.XmlWriter.WriteCharEntity%2A>|해당 문자의 <xref:System.Xml.XmlWriter.WriteString%2A> 메서드에 대한 호출로 처리됩니다.|  
|<xref:System.Xml.XmlWriter.WriteSurrogateCharEntity%2A>|해당 문자의 <xref:System.Xml.XmlWriter.WriteString%2A> 메서드에 대한 호출로 처리됩니다.|  
  
 <xref:System.Xml.XmlWriter> 클래스에 대한 자세한 내용은 <xref:System.Xml.XmlWriter> 클래스 참조 문서를 참조하세요.  
  
### <a name="multiple-xmlwriter-objects"></a>여러 XmlWriter 개체  
 하나 이상의 <xref:System.Xml.XPath.XPathNavigator> 개체를 열어 놓은 상태에서 여러 <xref:System.Xml.XmlWriter> 개체가 각각 XML 문서의 다른 부분을 가리키도록 할 수 있습니다. 단일 스레드 시나리오에서 여러 <xref:System.Xml.XmlWriter> 개체가 허용 및 지원됩니다.  
  
 다음은 여러 <xref:System.Xml.XmlWriter> 개체를 사용할 때 고려해야 할 중요 참고 사항입니다.  
  
- 각 <xref:System.Xml.XmlWriter> 개체의 <xref:System.Xml.XmlWriter.Close%2A> 메서드를 호출하면 <xref:System.Xml.XmlWriter> 개체를 사용하여 작성한 XML 조각이 XML 문서에 추가됩니다. 그때까지 <xref:System.Xml.XmlWriter> 개체는 연결되지 않은 조각을 작성합니다. XML 문서에서 작업을 수행해도 <xref:System.Xml.XmlWriter>를 호출하기 전에 <xref:System.Xml.XmlWriter.Close%2A> 개체를 사용하여 작성 중인 조각에는 영향을 주지 않습니다.  
  
- 특정 XML 하위 트리에 <xref:System.Xml.XmlWriter> 개체가 열려 있을 경우 이 하위 트리를 삭제해도 <xref:System.Xml.XmlWriter> 개체가 이 하위 트리에 추가됩니다. 하위 트리는 단순히 삭제된 조각이 됩니다.  
  
- XML 문서의 동일한 지점에 여러 <xref:System.Xml.XmlWriter> 개체가 동시에 열려 있을 경우 <xref:System.Xml.XmlWriter> 개체를 연 순서가 아니라 닫은 순서대로 XML 문서에 추가됩니다.  
  
 다음 예제에서는 <xref:System.Xml.XmlDocument> 개체를 만들고 <xref:System.Xml.XPath.XPathNavigator> 개체를 만든 다음 <xref:System.Xml.XmlWriter> 메서드에서 반환된 <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A> 개체를 사용하여 `books.xml` 파일에 첫 번째 책의 구조를 만들고 `book.xml` 파일로 저장합니다.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
Using writer As XmlWriter = navigator.PrependChild()  
  
    writer.WriteStartElement("bookstore")  
    writer.WriteStartElement("book")  
    writer.WriteAttributeString("genre", "autobiography")  
    writer.WriteAttributeString("publicationdate", "1981-03-22")  
    writer.WriteAttributeString("ISBN", "1-861003-11-0")  
    writer.WriteElementString("title", "The Autobiography of Benjamin Franklin")  
    writer.WriteStartElement("author")  
    writer.WriteElementString("first-name", "Benjamin")  
    writer.WriteElementString("last-name", "Franklin")  
    writer.WriteElementString("price", "8.99")  
    writer.WriteEndElement()  
    writer.WriteEndElement()  
    writer.WriteEndElement()  
  
End Using  
  
document.Save("book.xml")  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
XPathNavigator navigator = document.CreateNavigator();  
  
using (XmlWriter writer = navigator.PrependChild())  
{  
    writer.WriteStartElement("bookstore");  
    writer.WriteStartElement("book");  
    writer.WriteAttributeString("genre", "autobiography");  
    writer.WriteAttributeString("publicationdate", "1981-03-22");  
    writer.WriteAttributeString("ISBN", "1-861003-11-0");  
    writer.WriteElementString("title", "The Autobiography of Benjamin Franklin");  
    writer.WriteStartElement("author");  
    writer.WriteElementString("first-name", "Benjamin");  
    writer.WriteElementString("last-name", "Franklin");  
    writer.WriteElementString("price", "8.99");  
    writer.WriteEndElement();  
    writer.WriteEndElement();  
    writer.WriteEndElement();  
}  
document.Save("book.xml");  
```  
  
## <a name="saving-an-xml-document"></a>XML 문서 저장  
 <xref:System.Xml.XmlDocument> 클래스의 메서드를 사용하면 <xref:System.Xml.XmlDocument> 개체에서 변경된 내용을 이 항목에서 설명하는 메서드의 결과로 저장할 수 있습니다. <xref:System.Xml.XmlDocument> 개체에서 변경된 내용을 저장하는 방법에 대한 자세한 내용은 [문서 작성 및 저장](../../../../docs/standard/data/xml/saving-and-writing-a-document.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XML 데이터 수정](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 제거](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md)
