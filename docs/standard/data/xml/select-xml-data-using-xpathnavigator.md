---
title: XPathNavigator를 사용하여 XML 데이터 선택
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: c268c49e-32b9-4171-b782-dcb7b065fa73
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3ab2dbe79e1b4b89070d07e0f2c966cb54f6e500
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64589984"
---
# <a name="select-xml-data-using-xpathnavigator"></a>XPathNavigator를 사용하여 XML 데이터 선택
<xref:System.Xml.XPath.XPathNavigator> 클래스는 XPath 식을 사용하여 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체의 노드 집합을 선택하는 데 사용되는 메서드 집합을 제공합니다. 선택한 후에는 선택한 노드 집합을 반복할 수 있습니다.  
  
## <a name="xpathnavigator-selection-methods"></a>XPathNavigator 선택 메서드  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 XPath 식을 사용하여 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체의 노드 집합을 선택하는 데 사용되는 메서드 집합을 제공합니다. 또한 <xref:System.Xml.XPath.XPathNavigator> 클래스는 XPath 식을 사용하는 것보다 더 빠르게 상위, 자식 및 하위 노드를 선택할 수 있는 최적화된 메서드 집합을 제공합니다. 선택한 노드 집합이 <xref:System.Xml.XPath.XPathNodeIterator> 개체 또는 <xref:System.Xml.XPath.XPathNavigator> 개체(선택한 노드가 하나일 경우)에 반환됩니다.  
  
### <a name="selecting-nodes-using-xpath-expressions"></a>XPath 식을 사용하여 노드 선택  
 XPath 식을 사용하여 노드 집합을 선택하려면 다음 선택 메서드 중 하나를 사용합니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
 이러한 메서드를 호출하면 <xref:System.Xml.XPath.XPathNodeIterator> 개체 또는 <xref:System.Xml.XPath.XPathNavigator> 개체(선택한 노드가 하나일 경우)를 사용하여 자유롭게 탐색할 수 있는 노드 집합이 반환됩니다.  
  
 <xref:System.Xml.XPath.XPathNodeIterator> 개체를 사용하여 탐색해도 개체를 만들 때 사용한 <xref:System.Xml.XPath.XPathNavigator> 개체의 위치에는 영향을 주지 않습니다. <xref:System.Xml.XPath.XPathNavigator> 메서드에서 반환된 <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> 개체는 반환된 단일 노드에 위치하며 개체를 만들 때 사용한 <xref:System.Xml.XPath.XPathNavigator> 개체의 위치에는 영향을 주지 않습니다.  
  
 다음 예제에서는 <xref:System.Xml.XPath.XPathNavigator> 개체로부터 <xref:System.Xml.XPath.XPathDocument> 개체를 만들고 <xref:System.Xml.XPath.XPathNavigator.Select%2A> 메서드를 사용하여 <xref:System.Xml.XPath.XPathDocument> 개체에서 노드를 선택하고 <xref:System.Xml.XPath.XPathNodeIterator> 개체를 사용하여 선택한 노드를 반복하는 것을 보여 줍니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
Dim nodes As XPathNodeIterator = navigator.Select("/bookstore/book")  
  
While nodes.MoveNext()  
    Console.WriteLine(nodes.Current.Name)  
End While  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
XPathNodeIterator nodes = navigator.Select("/bookstore/book");  
  
while(nodes.MoveNext())  
{  
    Console.WriteLine(nodes.Current.Name);  
}  
```  
  
 이 예제에서는 `books.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="optimized-selection-methods"></a>최적화된 선택 메서드  
 <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A>, <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> 및 <xref:System.Xml.XPath.XPathNavigator> 메서드는 일반적으로 자식, 하위 및 상위 노드를 검색하는 데 사용하는 XPath 식을 나타냅니다. 이러한 메서드는 성능을 위해 최적화되었으며 해당 XPath 식보다 빠릅니다. <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>, <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A> 및 <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> 메서드는 선택할 노드의 <xref:System.Xml.XPath.XPathNodeType> 값 또는 로컬 이름과 네임스페이스 URI를 기반으로 상위, 자식 및 하위 노드를 선택합니다. 선택된 상위, 자식 및 하위 노드는 <xref:System.Xml.XPath.XPathNodeIterator> 개체에 반환됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XPath 식 계산](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 노드 일치시키기](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)
- [XPath 쿼리에서 인식하는 노드 형식](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)
- [XPath 쿼리 및 네임스페이스](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)
- [컴파일된 XPath 식](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
