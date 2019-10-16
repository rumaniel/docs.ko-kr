---
title: XPath 및 LINQ to XML 비교
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 87d361b1-daa9-4fd4-a53a-cbfa40111ad3
ms.openlocfilehash: e9bf192a2075653802f0c5a8b4e44ff0ceacb975
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66487536"
---
# <a name="comparison-of-xpath-and-linq-to-xml"></a>XPath 및 LINQ to XML 비교
XPath와 LINQ to XML은 유사한 기능을 제공합니다. XML 트리를 쿼리하여 결과를 요소 컬렉션, 특성 컬렉션, 노드 컬렉션 또는 요소나 특성의 값으로 반환하는 데 사용할 수 있습니다. 하지만 차이점도 있습니다.  
  
## <a name="differences-between-xpath-and-linq-to-xml"></a>XPath와 LINQ to XML의 차이점  
 XPath는 새 형식의 프로젝션을 허용하지 않습니다. XPath는 트리에서 노드 컬렉션만 반환할 수 있지만, LINQ to XML은 쿼리를 실행하고 개체 그래프나 XML 트리를 새 모양으로 프로젝션할 수 있습니다. LINQ to XML 쿼리는 훨씬 많은 기능을 포함하며 XPath 식보다 훨씬 더 강력합니다.  
  
 XPath 식은 문자열 내에 분리되어 존재합니다. C# 컴파일러는 컴파일 시간에 XPath 식의 구문을 분석할 수 없습니다. 이와 반대로 LINQ to XML 쿼리는 C# 컴파일러에서 구문이 분석되고 컴파일됩니다. 컴파일러에서는 많은 쿼리 오류를 catch할 수 있습니다.  
  
 XPath 결과는 강력한 형식이 아닙니다. 많은 경우에 XPath 식의 계산 결과는 개체이며 적절한 형식을 결정하고 필요한 경우 결과를 캐스팅하는 것은 개발자에게 달려 있습니다. 이와 반대로 LINQ to XML 쿼리의 프로젝션은 강력한 형식입니다.  
  
## <a name="result-ordering"></a>결과 정렬  
 XPath 1.0 권장 사항에는 XPath 식의 계산 결과인 컬렉션이 정렬되지 않는다고 나와 있습니다.  
  
 그러나 LINQ to XML XPath 축 메서드에서 반환하는 컬렉션을 반복할 때 컬렉션의 노드는 문서 순서로 반환됩니다. 이는 조건자가 `preceding` 및 `preceding-sibling`과 같이 문서 순서의 역순으로 표현되는 XPath 축에 액세스하는 경우에도 해당됩니다.  
  
 이와 반대로 대부분의 LINQ to XML 축은 문서 순서로 컬렉션을 반환하지만 그 중 <xref:System.Xml.Linq.XNode.Ancestors%2A> 및 <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A>는 문서 순서의 역순으로 컬렉션을 반환합니다. 다음 표에서는 축을 열거하고 각 축의 컬렉션 순서를 나타냅니다.  
  
|LINQ to XML 축|정렬|  
|----------------------|--------------|  
|XContainer.DescendantNodes|문서 순서|  
|XContainer.Descendants|문서 순서|  
|XContainer.Elements|문서 순서|  
|XContainer.Nodes|문서 순서|  
|XContainer.NodesAfterSelf|문서 순서|  
|XContainer.NodesBeforeSelf|문서 순서|  
|XElement.AncestorsAndSelf|문서 순서의 역순|  
|XElement.Attributes|문서 순서|  
|XElement.DescendantNodesAndSelf|문서 순서|  
|XElement.DescendantsAndSelf|문서 순서|  
|XNode.Ancestors|문서 순서의 역순|  
|XNode.ElementsAfterSelf|문서 순서|  
|XNode.ElementsBeforeSelf|문서 순서|  
|XNode.NodesAfterSelf|문서 순서|  
|XNode.NodesBeforeSelf|문서 순서|  
  
## <a name="positional-predicates"></a>위치 조건자  
 XPath 식에서 위치 조건자는 많은 축의 경우 문서 순서로 표현되지만 `preceding`, `preceding-sibling`, `ancestor` 및 `ancestor-or-self`와 같은 역방향 축의 경우에는 문서 순서의 역순으로 표현됩니다. 예를 들어, XPath 식 `preceding-sibling::*[1]`은 바로 이전 형제를 반환합니다. 이는 최종 결과 집합이 문서 순서로 제공되는 경우에도 해당됩니다.  
  
 이와 반대로 LINQ to XML의 모든 위치 조건자는 항상 축의 순서로 표현됩니다. 예를 들어, `anElement.ElementsBeforeSelf().ElementAt(0)`은 바로 이전 형제가 아니라 쿼리된 요소에 대한 부모의 첫 번째 자식 요소를 반환합니다. 또 다른 예로, `anElement.Ancestors().ElementAt(0)`은 부모 요소를 반환합니다.  
  
 LINQ to XML에서 바로 이전 요소를 찾으려는 경우 다음 식을 작성할 수 있습니다.  
  
```csharp
ElementsBeforeSelf().Last()
```
  
```vb
ElementsBeforeSelf().Last()
```
  
## <a name="performance-differences"></a>성능 차이점  
 LINQ to XML에서 XPath 기능을 사용하는 XPath 쿼리의 성능은 LINQ to XML 쿼리의 성능보다 낮습니다.  
  
## <a name="comparison-of-composition"></a>구성 비교  
 LINQ to XML 쿼리의 구성은 XPath 식의 구성과 다소 비슷하지만 구문은 매우 다릅니다.  
  
 예를 들어, `customers`라는 변수에 요소가 있고 `CompanyName`라는 모든 자식 요소 아래에서 `Customer`이라는 손자 요소를 찾으려는 경우 다음과 같이 XPath 식을 작성할 수 있습니다.  
  
```csharp  
customers.XPathSelectElements("./Customer/CompanyName")
```  
  
```vb
customers.XPathSelectElements("./Customer/CompanyName")
```

 동일한 LINQ to XML 쿼리는 다음과 같습니다.  
  
```csharp  
customers.Elements("Customer").Elements("CompanyName")
```  
  
```vb
customers.Elements("Customer").Elements("CompanyName")
```  

 각 XPath 축과 유사한 LINQ to XML 축은 다음과 같습니다.  
  
|XPath 축|LINQ to XML 축|  
|----------------|----------------------|  
|child(기본 축)|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|  
|Parent(..)|<xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=nameWithType>|  
|attribute axis(@)|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType><br /><br /> 또는<br /><br /> <xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|  
|ancestor 축|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|  
|ancestor-or-self 축|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|  
|descendant 축(//)|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType><br /><br /> 또는<br /><br /> <xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=nameWithType>|  
|descendant-or-self|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType><br /><br /> 또는<br /><br /> <xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=nameWithType>|  
|following-sibling|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType><br /><br /> 또는<br /><br /> <xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=nameWithType>|  
|preceding-sibling|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType><br /><br /> 또는<br /><br /> <xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=nameWithType>|  
|following|직접적으로 해당하는 축이 없음|  
|preceding|직접적으로 해당하는 축이 없음|  
  