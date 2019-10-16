---
title: XPathNavigator를 사용하여 XPath 식 계산
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 2913ccf3-f932-4363-8028-9e2d22ce6093
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b8666aa9cb9f0512c600a77891b16f439c46995a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54517411"
---
# <a name="evaluate-xpath-expressions-using-xpathnavigator"></a>XPathNavigator를 사용하여 XPath 식 계산
<xref:System.Xml.XPath.XPathNavigator> 클래스는 XPath 식을 계산하는 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 메서드를 제공합니다. <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 메서드는 XPath 식을 가져와서 계산하고 XPath 식 결과를 기준으로 부울, 숫자, 문자열, 노드 집합 등의 W3C XPath 형식을 반환합니다.  
  
## <a name="the-evaluate-method"></a>Evaluate 메서드  
 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 메서드는 XPath 식을 가져와서 계산하고 부울(<xref:System.Boolean>), 숫자(<xref:System.Double>), 문자열(<xref:System.String>), 노드 집합(<xref:System.Xml.XPath.XPathNodeIterator>) 등의 형식화된 결과를 반환합니다. 예를 들어, 수학적 메서드에서 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 메서드를 사용할 수 있습니다. 다음 예제 코드에서는 `books.xml` 파일에 있는 모든 책의 총 가격을 계산합니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
Dim query As XPathExpression = navigator.Compile("sum(//price/text())")  
Dim total As Double = CType(navigator.Evaluate(query), Double)  
Console.WriteLine(total)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
XPathExpression query = navigator.Compile("sum(//price/text())");  
Double total = (Double)navigator.Evaluate(query);  
Console.WriteLine(total);  
```  
  
 이 예제에서는 `books.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="position-and-last-functions"></a>position 및 last 함수  
 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 메서드가 오버로드됩니다. <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 메서드 중 하나가 <xref:System.Xml.XPath.XPathNodeIterator> 개체를 매개 변수로 사용합니다. 이 특정 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 메서드는 매개 변수로 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 개체만을 사용하는 <xref:System.Xml.XPath.XPathExpression> 메서드와 일치합니다. 단, 노드 집합 인수에서 계산을 실행할 현재 컨텍스트를 지정할 수 있다는 점이 다릅니다. 이 컨텍스트는 XPath `position()` 및 `last()` 함수가 현재 컨텍스트 노드에 상대적인 경우 이러한 함수에 필요합니다. `position()` 및 `last()` 함수가 위치 단계에서 조건자로 사용되지 않을 경우 이를 계산하기 위해서는 노드 집합에 대한 참조가 필요합니다. 그렇지 않으면 `position` 및 `last` 함수는 `0`을 반환합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XML 데이터 선택](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 노드 일치시키기](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)
- [XPath 쿼리에서 인식하는 노드 형식](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)
- [XPath 쿼리 및 네임스페이스](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)
- [컴파일된 XPath 식](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
