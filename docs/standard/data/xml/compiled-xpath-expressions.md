---
title: 컴파일된 XPath 식
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: e25dd95f-b64c-4d8b-a3a4-379e1aa0ad55
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fb6e3677d79f3131432c3daebeee4d166b5450b2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916668"
---
# <a name="compiled-xpath-expressions"></a>컴파일된 XPath 식
<xref:System.Xml.XPath.XPathExpression> 개체는 <xref:System.Xml.XPath.XPathExpression.Compile%2A> 클래스의 정적 <xref:System.Xml.XPath.XPathExpression> 메서드 또는 <xref:System.Xml.XPath.XPathNavigator.Compile%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator> 메서드 중 하나에서 반환된 컴파일된 XPath 쿼리를 나타냅니다.  
  
## <a name="the-xpathexpression-class"></a>XPathExpression 클래스  
 같은 XPath 쿼리를 두 번 이상 사용하는 경우 <xref:System.Xml.XPath.XPathExpression> 개체가 나타내는 컴파일된 XPath 쿼리는 매우 유용합니다.  
  
 예를 들어, 매번 XPath 쿼리를 나타내는 문자열을 사용하는 대신 <xref:System.Xml.XPath.XPathNavigator.Select%2A> 메서드를 여러 번 호출할 경우 <xref:System.Xml.XPath.XPathExpression.Compile%2A> 클래스의 <xref:System.Xml.XPath.XPathExpression> 메서드 또는 <xref:System.Xml.XPath.XPathNavigator.Compile%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator> 메서드를 사용하여 <xref:System.Xml.XPath.XPathExpression> 개체에서 XPath 쿼리를 컴파일하고 캐시하면 다시 사용이 가능하며 성능도 향상시킬 수 있습니다.  
  
 컴파일한 후에는 XPath 쿼리에서 반환되는 형식에 따라 <xref:System.Xml.XPath.XPathExpression> 개체를 다음 <xref:System.Xml.XPath.XPathNavigator> 클래스 메서드에 대한 입력으로 사용할 수 있습니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.XPath.XPathNavigator.Matches%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
 다음 표에서는 각 W3C XPath 반환 형식, 해당 Microsoft .NET Framework 형식 및 반환 형식을 기준으로 <xref:System.Xml.XPath.XPathExpression> 개체와 함께 사용할 수 있는 메서드에 대해 설명합니다.  
  
|W3C XPath 반환 형식|해당 .NET Framework 형식|설명|메서드|  
|---------------------------|------------------------------------|-----------------|-------------|  
|`Node set`|<xref:System.Xml.XPath.XPathNodeIterator>|문서 순서에 따라 중복 없이 생성된, 정렬되지 않은 노드 컬렉션입니다.|<xref:System.Xml.XPath.XPathNavigator.Select%2A> 또는 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
|`Boolean`|<xref:System.Boolean>|`true` 또는 `false` 값입니다.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 또는<br /><br /> <xref:System.Xml.XPath.XPathNavigator.Matches%2A>|  
|`Number`|<xref:System.Double>|부동 소수점 숫자입니다.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
|`String`|<xref:System.String>|UCS 문자 시퀀스입니다.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
  
> [!NOTE]
> <xref:System.Xml.XPath.XPathNavigator.Matches%2A> 메서드에는 XPath 식을 매개 변수로 사용할 수 있습니다. <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> 메서드는 W3C XPath 반환 형식이 아닌 <xref:System.Xml.XPath.XPathNavigator> 개체를 반환합니다.  
  
### <a name="the-returntype-property"></a>ReturnType 속성  
 XPath 쿼리를 <xref:System.Xml.XPath.XPathExpression> 개체로 컴파일한 후 <xref:System.Xml.XPath.XPathExpression.ReturnType%2A> 개체의 <xref:System.Xml.XPath.XPathExpression> 속성을 사용하여 XPath 쿼리가 반환하는 대상을 결정합니다.  
  
 <xref:System.Xml.XPath.XPathExpression.ReturnType%2A> 속성은 W3C XPath 반환 형식을 나타내는 다음 <xref:System.Xml.XPath.XPathResultType> 열거형 값 중 하나를 반환합니다.  
  
- <xref:System.Xml.XPath.XPathResultType.Any>  
  
- <xref:System.Xml.XPath.XPathResultType.Boolean>  
  
- <xref:System.Xml.XPath.XPathResultType.Error>  
  
- <xref:System.Xml.XPath.XPathResultType.Navigator>  
  
- <xref:System.Xml.XPath.XPathResultType.NodeSet>  
  
- <xref:System.Xml.XPath.XPathResultType.Number>  
  
- <xref:System.Xml.XPath.XPathResultType.String>  
  
 다음 예제에서는 <xref:System.Xml.XPath.XPathExpression> 개체를 사용하여 `books.xml` 파일에서 숫자 및 노드 집합을 반환합니다. 각 <xref:System.Xml.XPath.XPathExpression.ReturnType%2A> 개체의 <xref:System.Xml.XPath.XPathExpression> 속성과 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 및 <xref:System.Xml.XPath.XPathNavigator.Select%2A> 메서드의 결과가 콘솔에 나타납니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Returns a number.  
Dim query1 As XPathExpression = navigator.Compile("bookstore/book/price/text()*10")  
Console.WriteLine(query1.ReturnType)  
  
Dim number As Double = CType(navigator.Evaluate(query1), Double)  
Console.WriteLine(number)  
  
' Returns a node set.  
Dim query2 As XPathExpression = navigator.Compile("bookstore/book/price")  
Console.WriteLine(query2.ReturnType)  
  
Dim nodes As XPathNodeIterator = navigator.Select(query2)  
nodes.MoveNext()  
Console.WriteLine(nodes.Current.Value)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Returns a number.  
XPathExpression query1 = navigator.Compile("bookstore/book/price/text()*10");  
Console.WriteLine(query1.ReturnType);  
  
Double number = (Double)navigator.Evaluate(query1);  
Console.WriteLine(number);  
  
// Returns a node set.  
XPathExpression query2 = navigator.Compile("bookstore/book/price");  
Console.WriteLine(query2.ReturnType);  
  
XPathNodeIterator nodes = navigator.Select(query2);  
nodes.MoveNext();  
Console.WriteLine(nodes.Current.Value);  
```  
  
 이 예제에서는 `books.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="higher-performance-xpath-expressions"></a>XPath 식의 성능 향상  
 성능을 향상시키려면 쿼리에 가능한 가장 구체적인 XPath 식을 사용합니다. 예를 들어, `book` 노드가 `bookstore` 노드의 자식 노드이고 `bookstore` 노드가 XML 문서에서 최상위 요소인 경우 XPath 식 `/bookstore/book`을 사용하면 `//book`을 사용하는 것보다 빠릅니다. `//book` XPath 식은 XML 트리에서 모든 노드를 검색하여 일치하는 노드를 식별합니다.  
  
 또한 선택 기준이 단순한 경우 <xref:System.Xml.XPath.XPathNavigator> 클래스에서 제공하는 노드 집합 탐색 메서드를 사용하면 <xref:System.Xml.XPath.XPathNavigator> 클래스에서 제공하는 선택 메서드를 사용하는 것보다 성능이 향상됩니다. 예를 들어, 현재 노드의 첫 번째 자식을 선택해야 할 경우 <xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A> 메서드를 사용하는 것이 `child::*[1]` XPath 식 및 <xref:System.Xml.XPath.XPathNavigator.Select%2A> 메서드를 사용하는 것보다 빠릅니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 클래스의 노드 집합 탐색 메서드에 대한 자세한 내용은 [XPathNavigator를 사용하여 노드 집합 탐색](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XML 데이터 선택](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XPath 식 계산](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 노드 일치시키기](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)
- [XPath 쿼리에서 인식하는 노드 형식](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)
- [XPath 쿼리 및 네임스페이스](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)
