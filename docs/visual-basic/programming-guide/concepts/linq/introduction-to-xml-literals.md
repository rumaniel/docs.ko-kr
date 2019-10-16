---
title: Visual Basic2의 XML 리터럴 소개
ms.date: 07/20/2015
ms.assetid: 94fc0e03-978e-4c08-ab6c-0dc3c1e64f10
ms.openlocfilehash: 5355a3c0f01bb247e38e52816693ee47d7d50556
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834989"
---
# <a name="introduction-to-xml-literals-in-visual-basic"></a>Visual Basic의 XML 리터럴 소개
이 섹션에서는 Visual Basic에서 XML 트리를 만드는 방법에 대 한 정보를 제공 합니다.  
  
 LINQ 쿼리의 결과를 XML 트리의 콘텐츠로 사용 하는 방법에 대 한 자세한 내용은 [함수 생성 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-construction-linq-to-xml.md)을 참조 하세요.  
  
 Visual Basic의 XML 리터럴에 대 한 자세한 내용은 Visual Basic의 [LINQ to XML 개요](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)를 참조 하세요.  
  
## <a name="creating-xml-trees"></a>XML 트리 만들기  
 다음 예제에서는 <xref:System.Xml.Linq.XElement>(이 경우에는 `contacts`)를 만드는 방법을 보여 줍니다.  
  
```vb  
Dim contacts As XElement = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone>206-555-0144</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
### <a name="creating-an-xelement-with-simple-content"></a>단순 내용을 사용하여 XElement 만들기  
 다음과 같이 단순 내용이 포함된 <xref:System.Xml.Linq.XElement>를 만들 수 있습니다.  
  
```vb  
Dim n as XElement = <Customer>Adventure Works</Customer>  
Console.WriteLine(n)   
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
### <a name="creating-an-empty-element"></a>빈 요소 만들기  
 다음과 같이 빈 <xref:System.Xml.Linq.XElement>를 만들 수 있습니다.  
  
```vb  
Dim n As XElement = <Customer/>  
Console.WriteLine(n)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Customer />  
```  
  
### <a name="using-embedded-expressions"></a>포함 식 사용  
 XML 리터럴의 중요한 특징은 포함 식을 허용한다는 점입니다. 포함 식을 통해 식을 계산하고 식의 결과를 XML 트리에 삽입할 수 있습니다. 식이 <xref:System.Xml.Linq.XElement> 형식으로 계산되면 요소가 트리에 삽입되고, 식이 <xref:System.Xml.Linq.XAttribute> 형식으로 계산되면 특성이 트리에 삽입됩니다. 유효한 경우에만 요소와 특성을 트리에 삽입할 수 있습니다.  
  
 단일 식만 포함 식에 들어갈 수 있는 점을 명심해야 합니다. 여러 문을 포함할 수는 없습니다. 식이 한 줄을 넘으면 줄 연속 문자를 사용해야 합니다.  
  
 포함 식을 사용하여 기존 노드(요소 포함)와 특성을 새 XML 트리에 추가하는 경우 기존 노드에 이미 부모가 있으면 노드가 복제됩니다. 새로 복제된 노드는 새 XML 트리에 추가됩니다. 기존 노드에 부모가 없으면 노드가 새 XML 트리에 추가되기만 합니다. 이 항목의 마지막 예제에서는 이에 대해 보여 줍니다.  
  
 다음 예제에서는 포함 식을 사용하여 요소를 트리에 삽입합니다.  
  
```vb  
xmlTree1 As XElement = _  
    <Root>  
        <Child>Contents</Child>  
    </Root>  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child> %>  
    </Root>  
Console.WriteLine(xmlTree2)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>  
  <Child>Contents</Child>  
</Root>  
```  
  
### <a name="using-embedded-expressions-for-content"></a>내용에 대해 포함 식 사용  
 포함 식을 사용하여 요소의 내용을 제공할 수 있습니다.  
  
```vb  
Dim str As String  
str = "Some content"  
Dim root As XElement = <Root><%= str %></Root>  
Console.WriteLine(root)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>Some content</Root>  
```  
  
### <a name="using-a-linq-query-in-an-embedded-expression"></a>포함 식에서 LINQ 쿼리 사용  
 LINQ 쿼리의 결과를 요소의 내용으로 사용할 수 있습니다.  
  
```vb  
Dim arr As Integer() = {1, 2, 3}  
  
Dim n As XElement = _  
    <Root>  
        <%= From i In arr Select <Child><%= i %></Child> %>  
    </Root>  
  
Console.WriteLine(n)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Child>3</Child>  
</Root>  
```  
  
### <a name="using-embedded-expressions-for-node-names"></a>노드 이름에 대해 포함 식 사용  
 포함 식을 사용하여 특성 이름, 특성 값, 요소 이름 및 요소 값을 계산할 수도 있습니다.  
  
```vb  
Dim eleName As String = "ele"  
Dim attName As String = "att"  
Dim attValue As String = "aValue"  
Dim eleValue As String = "eValue"  
Dim n As XElement = _  
    <Root <%= attName %>=<%= attValue %>>  
        <<%= eleName %>>  
            <%= eleValue %>  
        </>  
    </Root>  
Console.WriteLine(n)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root att="aValue">  
  <ele>eValue</ele>  
</Root>  
```  
  
### <a name="cloning-vs-attaching"></a>복제와 추가 비교  
 앞에서 설명했듯이 포함 식을 사용하여 기존 노드(요소 포함)와 특성을 새 XML 트리에 추가하는 경우 기존 노드에 이미 부모가 있으면 노드가 복제되고 새로 복제된 노드가 새 XML 트리에 추가됩니다. 기존 노드에 부모가 없으면 노드가 새 XML 트리에 추가되기만 합니다.  
  
```vb  
' Create a tree with a child element.  
Dim xmlTree1 As XElement = _  
    <Root>  
        <Child1>1</Child1>  
    </Root>  
  
' Create an element that is not parented.  
Dim child2 As XElement = <Child2>2</Child2>  
  
' Create a tree and add Child1 and Child2 to it.  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child1>(0) %>  
        <%= child2 %>  
    </Root>  
  
' Compare Child1 identity.  
Console.WriteLine("Child1 was {0}", _  
    IIf(xmlTree1.Element("Child1") Is xmlTree2.Element("Child1"), _  
    "attached", "cloned"))  
  
' Compare Child2 identity.  
Console.WriteLine("Child2 was {0}", _  
    IIf(child2 Is xmlTree2.Element("Child2"), _  
    "attached", "cloned"))  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>참조

- [XML 트리 만들기 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
