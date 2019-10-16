---
title: XPath 사용자에 대 한 LINQ to XML (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 0e64911c-a7cc-4c20-b927-ca99078b5656
ms.openlocfilehash: 5726ce646eba9fce36803ab12e6409b929d3cca5
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69667623"
---
# <a name="linq-to-xml-for-xpath-users-visual-basic"></a>XPath 사용자에 대 한 LINQ to XML (Visual Basic)

이 항목 집합에서는 다양한 XPath 식과 각 XPath 식에 해당하는 동일한 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 항목을 보여 줍니다.  
  
 모든 예제에서는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]의 확장 메서드에 의해 사용할 수 있게 된 <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>의 XPath 기능을 사용하며 XPath 식과 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 식을 모두 실행합니다. 그런 다음 두 쿼리의 결과를 비교하여 XPath 식이 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 쿼리와 기능적으로 동일한지 확인합니다. 두 형식의 쿼리가 동일한 XML 트리에서 노드를 반환하므로 쿼리 결과 비교는 참조 ID를 사용하여 수행됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[XPath 및 LINQ to XML 비교](../../../../visual-basic/programming-guide/concepts/linq/comparison-of-xpath-and-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]의 유사점과 차이점에 대해 간략히 설명합니다.|  
|[방법: 자식 요소 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-a-child-element-xpath-linq-to-xml.md)|XPath 자식 요소 축과 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <xref:System.Xml.Linq.XContainer.Element%2A> 메서드를 비교합니다.<br /><br /> 관련된 XPath 식은 `"DeliveryNotes"`입니다.|  
|[방법: 자식 요소 목록 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-a-list-of-child-elements-xpath-linq-to-xml.md)|XPath 자식 요소 축과 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <xref:System.Xml.Linq.XContainer.Elements%2A> 축을 비교합니다.<br /><br /> 관련된 XPath 식은 `"./*"`입니다.|  
|[방법: Root 요소 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-the-root-element-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 루트 요소를 가져오는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"/PurchaseOrders"`입니다.|  
|[방법: 하위 요소 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-descendant-elements-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 특정 이름을 가진 하위 요소를 가져오는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"//Name"`입니다.|  
|[방법: 특성에 대 한 필터링 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-filter-on-an-attribute-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 지정된 이름을 가진 하위 요소와 지정된 값을 가진 특성이 포함된 하위 요소를 가져오는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"./Address[@Type='Shipping']"`입니다.|  
|[방법: 관련 요소 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-related-elements-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 다른 요소의 값에 의해 참조되는 특성을 기준으로 선택하여 요소를 가져오는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"./Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]"`입니다.|  
|[방법: 네임 스페이스에서 요소 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-elements-in-a-namespace.md)|XML 네임스페이스로 작업하기 위해 XPath <xref:System.Xml.XmlNamespaceManager> 클래스를 사용하는 경우와 <xref:System.Xml.Linq.XName> 클래스의 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <xref:System.Xml.Linq.XName.Namespace%2A> 속성을 사용하는 경우를 비교합니다.<br /><br /> 관련된 XPath 식은 `"./aw:*"`입니다.|  
|[방법: 선행 형제 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-preceding-siblings-xpath-linq-to-xml.md)|XPath `preceding-sibling` 축과 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 자식 <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType> 축을 비교합니다.<br /><br /> 관련된 XPath 식은 `"preceding-sibling::*"`입니다.|  
|[방법: 자식 요소의 하위 항목 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-descendants-of-a-child-element-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 특정 이름을 가진 자식 요소의 하위 요소를 가져오는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"./Paragraph//Text/text()"`입니다.|  
|[방법: 두 위치 경로의 공용 구조체 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-a-union-of-two-location-paths-xpath.md)|XPath에서 통합 연산자 <code>&#124;</code>를 사용하는 경우와 <xref:System.Linq.Enumerable.Concat%2A>에서 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 표준 쿼리 연산자를 사용하는 경우를 비교합니다.<br /><br /> 관련된 XPath 식은 <code>"//Category&#124;//Price"</code>입니다.|  
|[방법: 형제 노드 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-sibling-nodes-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 특정 이름을 가진 노드의 형제를 모두 찾는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"../Book"`입니다.|  
|[방법: 부모의 특성 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-an-attribute-of-the-parent-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 부모 요소를 탐색하고 연결된 특성을 찾는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"../@id"`입니다.|  
|[방법: 특정 이름으로 형제의 특성 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-attributes-of-siblings-with-a-specific-name.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 컨텍스트 노드에 대한 형제의 특정 특성을 찾는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"../Book/@id"`입니다.|  
|[방법: 특정 특성으로 요소 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-elements-with-a-specific-attribute.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 특정 특성이 포함된 요소를 모두 찾는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"./*[@Select]"`입니다.|  
|[방법: 위치에 따라 자식 요소 찾기 (XPath-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-child-elements-based-on-position.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 상대 위치를 기준으로 요소를 찾는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"Test[position() >= 2 and position() <= 4]"`입니다.|  
|[방법: 직접 선행 형제 (XPath-LINQ to XML) 찾기 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-the-immediate-preceding-sibling-xpath-linq-to-xml.md)|XPath와 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하여 노드의 바로 이전 형제를 찾는 방법을 비교합니다.<br /><br /> 관련된 XPath 식은 `"preceding-sibling::*[1]"`입니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Xml.XPath?displayProperty=nameWithType>
- [XML 트리 쿼리 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/querying-xml-trees.md)
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
