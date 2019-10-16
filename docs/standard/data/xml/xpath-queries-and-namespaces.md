---
title: XPath 쿼리 및 네임스페이스
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: ef6402be-2f8e-4be2-8d3e-a80891cdef8b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0704e78a0e7fbf3987b3bc75bb46e135f00110e9
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615345"
---
# <a name="xpath-queries-and-namespaces"></a>XPath 쿼리 및 네임스페이스
XPath 쿼리는 XML 문서에서 네임스페이스를 인식하며 네임스페이스 접두사를 사용하여 요소 및 특성 이름을 정규화할 수 있습니다. 네임스페이스 접두사로 요소 및 특성 이름을 정규화하면 XPath 쿼리에 의해 반환되는 노드가 특정 네임스페이스에 속한 노드로만 제한됩니다.  
  
 예를 들어, 접두사 `books`를 네임스페이스 `http://www.contoso.com/books`에 매핑하면 다음 XPath 쿼리 `/books:books/books:book`은 네임스페이스 `book`에 있는 `http://www.contoso.com/books` 요소만 선택합니다.  
  
## <a name="the-xmlnamespacemanager"></a>XmlNamespaceManager  
 XPath 쿼리에서 네임스페이스를 사용할 수 있도록 <xref:System.Xml.IXmlNamespaceResolver> 클래스와 같은 <xref:System.Xml.XmlNamespaceManager> 인터페이스에서 파생된 개체가 XPath 쿼리에 포함할 네임스페이스 URI 및 접두사로 구성됩니다.  
  
 다음과 같은 방법으로 쿼리에서 <xref:System.Xml.XmlNamespaceManager> 개체를 사용할 수 있습니다.  
  
- <xref:System.Xml.XmlNamespaceManager> 개체의 <xref:System.Xml.XPath.XPathExpression> 메서드를 사용하여 <xref:System.Xml.XPath.XPathExpression.SetContext%2A> 개체를 기존 <xref:System.Xml.XPath.XPathExpression> 개체와 연결합니다. 또한 XPath 식을 나타내는 문자열과 <xref:System.Xml.XPath.XPathExpression> 개체를 매개 변수로 사용하며 새 <xref:System.Xml.XPath.XPathExpression.Compile%2A> 개체를 반환하는 정적<xref:System.Xml.XmlNamespaceManager> 메서드를 사용하여 새 <xref:System.Xml.XPath.XPathExpression> 개체를 컴파일할 수 있습니다.  
  
- <xref:System.Xml.XmlNamespaceManager> 개체 자체는 XPath 식을 나타내는 문자열과 함께 허용되는 <xref:System.Xml.XPath.XPathNavigator> 클래스 메서드에 매개 변수로 전달됩니다.  
  
 다음은 <xref:System.Xml.XPath.XPathNavigator> 인터페이스에서 파생된 개체를 매개 변수로 사용할 수 있는 <xref:System.Xml.IXmlNamespaceResolver> 클래스의 메서드입니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
### <a name="the-default-namespace"></a>기본 네임스페이스  
 다음 XML 문서에서는 빈 접두사가 있는 기본 네임스페이스를 사용하여 `http://www.contoso.com/books` 네임스페이스를 선언합니다.  
  
```xml  
<books xmlns="http://www.contoso.com/books">  
    <book>  
        <title>Title</title>  
        <author>Author Name</author>  
        <price>5.50</price>  
    </book>  
</books>  
```  
  
 XPath는 빈 접두사를 `null` 네임스페이스로 간주합니다. 즉, 네임스페이스에 매핑된 접두사만 XPath 쿼리에서 사용할 수 있습니다. 그러므로 XML 문서의 네임스페이스에 대해 쿼리하려는 경우 기본 네임스페이스라 하더라도 이에 대한 접두사를 정의해야 합니다.  
  
 예를 들어, 위의 XML 문서에 대한 접두사를 정의하지 않으면 XPath 쿼리 `/books/book`은 결과를 반환하지 않습니다.  
  
 네임스페이스에 없는 일부 노드와 기본 네임스페이스에 있는 일부 노드를 사용하여 문서를 쿼리하는 경우 접두사를 바인딩하여 모호성을 없애야 합니다.  
  
 다음 코드는 기본 네임스페이스에 대한 접두사를 정의하고 `book` 네임스페이스에서 모든 `http://www.contoso.com/books` 요소를 선택합니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
Dim query As XPathExpression = navigator.Compile("/books:books/books:book")  
Dim manager As XmlNamespaceManager = New XmlNamespaceManager(navigator.NameTable)  
manager.AddNamespace("books", "http://www.contoso.com/books")  
query.SetContext(manager)  
Dim nodes As XPathNodeIterator = navigator.Select(query)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
XPathExpression query = navigator.Compile("/books:books/books:book");  
XmlNamespaceManager manager = new XmlNamespaceManager(navigator.NameTable);  
manager.AddNamespace("books", "http://www.contoso.com/books");  
query.SetContext(manager);  
XPathNodeIterator nodes = navigator.Select(query);  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XML 데이터 선택](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XPath 식 계산](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 노드 일치시키기](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)
- [XPath 쿼리에서 인식하는 노드 형식](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)
- [컴파일된 XPath 식](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
