---
title: (Visual Basic) XML 트리에서 요소, 특성 및 노드 제거
ms.date: 07/20/2015
ms.assetid: 5cf21919-4360-4b49-b29d-58ea3164ac72
ms.openlocfilehash: 85a7a3b4047e269c562177cfa045b952472aaac2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787072"
---
# <a name="removing-elements-attributes-and-nodes-from-an-xml-tree-visual-basic"></a>(Visual Basic) XML 트리에서 요소, 특성 및 노드 제거
XML 트리를 수정하여 요소, 특성 및 다른 형식의 노드를 제거할 수 있습니다.  
  
 XML 문서에서 요소나 특성을 하나만 제거하는 것은 간단합니다. 그러나 요소나 특성의 컬렉션을 제거하는 경우 먼저 컬렉션을 목록으로 구체화한 다음 요소나 특성을 목록에서 삭제해야 합니다. 가장 좋은 방법은 이 작업을 수행하는 <xref:System.Xml.Linq.Extensions.Remove%2A> 확장 메서드를 사용하는 것입니다.  
  
 이렇게 하는 주요 이유는 XML 트리에서 검색하는 대부분의 컬렉션이 지연된 실행을 사용하여 생성되기 때문입니다. 컬렉션을 먼저 목록으로 구체화하지 않거나 확장명 메서드를 사용하지 않는 경우 특정 유형의 버그가 발생할 수 있습니다. 자세한 내용은 [혼합 된 선언적 코드/명령적 코드 버그 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/mixed-declarative-code-imperative-code-bugs-linq-to-xml.md)합니다.  
  
 다음 메서드는 XML 트리에서 노드와 특성을 제거합니다.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XAttribute.Remove%2A?displayProperty=nameWithType>|부모에서 <xref:System.Xml.Linq.XAttribute>를 제거합니다.|  
|<xref:System.Xml.Linq.XContainer.RemoveNodes%2A?displayProperty=nameWithType>|<xref:System.Xml.Linq.XContainer>에서 자식 노드를 제거합니다.|  
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=nameWithType>|<xref:System.Xml.Linq.XElement>에서 내용과 특성을 제거합니다.|  
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=nameWithType>|<xref:System.Xml.Linq.XElement>의 특성을 제거합니다.|  
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=nameWithType>|값으로 `null`을 전달하면 특성을 제거합니다.|  
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=nameWithType>|값으로 `null`을 전달하면 자식 요소를 제거합니다.|  
|<xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=nameWithType>|부모에서 <xref:System.Xml.Linq.XNode>를 제거합니다.|  
|<xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=nameWithType>|부모 요소에서 소스 컬렉션의 모든 특성이나 요소를 제거합니다.|  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 이 예제에서는 요소를 제거하는 세 가지 방법을 보여 줍니다. 첫째, 단일 요소를 제거합니다. 둘째, 요소의 컬렉션을 검색하고 <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> 연산자를 사용하여 구체화한 다음 제거합니다. 마지막으로, 요소의 컬렉션을 검색하고 <xref:System.Xml.Linq.Extensions.Remove%2A> 확장 메서드를 사용하여 제거합니다.  
  
 에 대 한 자세한 합니다 <xref:System.Linq.Enumerable.ToList%2A> 연산자를 참조 하세요 [데이터 형식 변환 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md)합니다.  
  
### <a name="code"></a>코드  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <Child1>  
            <GrandChild1/>  
            <GrandChild2/>  
            <GrandChild3/>  
        </Child1>  
        <Child2>  
            <GrandChild4/>  
            <GrandChild5/>  
            <GrandChild6/>  
        </Child2>  
        <Child3>  
            <GrandChild7/>  
            <GrandChild8/>  
            <GrandChild9/>  
        </Child3>  
    </Root>  
root.<Child1>.<GrandChild1>.Remove()  
root.<Child2>.Elements().ToList().Remove()  
root.<Child3>.Elements().Remove()  
Console.WriteLine(root)  
```  
  
### <a name="comments"></a>설명  
 이 코드의 결과는 다음과 같습니다.  
  
```xml  
<Root>  
  <Child1>  
    <GrandChild2 />  
    <GrandChild3 />  
  </Child1>  
  <Child2 />  
  <Child3 />  
</Root>  
```  
  
 `Child1`에서는 첫 번째 손자 요소가 제거되었고, `Child2`와 `Child3`에서는 모든 손자 요소가 제거되었습니다.  
  
## <a name="see-also"></a>참고자료

- [XML 트리 수정 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
