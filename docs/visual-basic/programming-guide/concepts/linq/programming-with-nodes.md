---
title: 노드를 사용한 프로그래밍 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: d8422a9b-dd37-44a3-8aac-2237ed9561e0
ms.openlocfilehash: 2a331d77f1c54f6428d36b6ccb403dcc01094c98
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834926"
---
# <a name="programming-with-nodes-visual-basic"></a>노드를 사용한 프로그래밍 (Visual Basic)
XML 편집기, 변환 시스템 또는 보고서 작성기와 같은 프로그램을 작성해야 하는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 개발자는 요소와 특성보다 세부적인 단위에서 작업하는 프로그램을 작성해야 하는 경우가 많습니다. LINQ to XML 개발자는 흔히 노드 수준에서 작업하여 텍스트 노드, 처리 명령 및 주석을 조작해야 합니다. 이 항목에서는 노드 수준의 프로그래밍에 대해 자세히 설명합니다.  
  
## <a name="node-details"></a>노드 정보  
 노드 수준에서 작업하는 프로그래머가 알고 있어야 하는 프로그래밍 세부 정보가 많이 있습니다.  
  
### <a name="parent-property-of-children-nodes-of-xdocument-is-set-to-null"></a>XDocument에 대한 자식 노드의 부모 속성이 Null로 설정됨  
 <xref:System.Xml.Linq.XObject.Parent%2A> 속성에는 부모 노드가 아니라 부모 <xref:System.Xml.Linq.XElement>가 포함되어 있습니다. <xref:System.Xml.Linq.XDocument>의 자식 노드에는 부모 <xref:System.Xml.Linq.XElement>가 없습니다. 이러한 노드의 부모는 문서이므로 해당 노드의 <xref:System.Xml.Linq.XObject.Parent%2A> 속성은 null로 설정됩니다.  
  
 다음은 이에 대한 예입니다.  
  
```vb  
Dim doc As XDocument = XDocument.Parse("<!-- a comment --><Root/>")  
Console.WriteLine(doc.Nodes().OfType(Of XComment).First().Parent Is Nothing)  
Console.WriteLine(doc.Root.Parent Is Nothing)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
True  
True  
```  
  
### <a name="adjacent-text-nodes-are-possible"></a>인접 텍스트 노드가 가능함  
 많은 XML 프로그래밍 모델에서 인접 텍스트 노드는 항상 병합됩니다. 이를 텍스트 노드의 표준화라고 합니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 텍스트 노드를 표준화하지 않습니다. 동일한 요소에 두 텍스트 노드를 추가하는 경우 인접 텍스트 노드가 생성됩니다. 그러나 <xref:System.Xml.Linq.XText> 노드가 아니라 문자열로 지정된 내용을 추가하는 경우 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 인접 텍스트 노드를 사용하여 문자열을 병합할 수 있습니다.  
  
 다음은 이에 대한 예입니다.  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
' This does not add a new text node.  
xmlTree.Add("new content")  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
'// This does add a new, adjacent text node.  
xmlTree.Add(New XText("more text"))  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
1  
1  
2  
```  
  
### <a name="empty-text-nodes-are-possible"></a>빈 텍스트 노드가 가능함  
 일부 XML 프로그래밍 모델에서 텍스트 노드는 빈 문자열을 포함하지 않도록 보장됩니다. 그 이유는 이러한 텍스트 노드가 XML의 serialization에 영향을 미치지 않기 때문입니다. 그러나 인접 텍스트 노드가 가능한 것과 동일한 이유로, 값을 빈 문자열로 설정하여 텍스트 노드에서 텍스트를 제거하는 경우 텍스트 노드 자체는 삭제되지 않습니다.  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Dim textNode As XText = xmlTree.Nodes().OfType(Of XText)().First()  
  
' The following line does not cause the removal of the text node.  
textNode.Value = ""  
  
Dim textNode2 As XText = xmlTree.Nodes().OfType(Of XText)().First()  
Console.WriteLine(">>{0}<<", textNode2)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
>><<  
```  
  
### <a name="an-empty-text-node-impacts-serialization"></a>빈 텍스트 노드가 serialization에 영향을 미침  
 요소에 빈 자식 텍스트 노드만 포함되어 있으면 `<Child></Child>`와 같은 긴 태그 구문으로 serialize됩니다. 요소에 자식 노드가 포함되어 있지 않으면 `<Child />`와 같은 짧은 태그 구문으로 serialize됩니다.  
  
```vb  
Dim child1 As XElement = New XElement("Child1", _  
    New XText("") _  
)  
Dim child2 As XElement = New XElement("Child2")  
Console.WriteLine(child1)  
Console.WriteLine(child2)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Child1></Child1>  
<Child2 />  
```  
  
### <a name="namespaces-are-attributes-in-the-linq-to-xml-tree"></a>네임스페이스가 LINQ to XML 트리의 특성임  
 네임스페이스 선언의 구문은 특성의 구문과 동일하지만 XSLT 및 XPath와 같은 일부 프로그래밍 인터페이스에서 네임스페이스 선언은 특성으로 간주되지 않습니다. 그러나 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서 네임스페이스는 XML 트리에서 <xref:System.Xml.Linq.XAttribute> 개체로 저장됩니다. 네임스페이스 선언이 포함된 요소의 특성을 반복하는 경우 네임스페이스 선언이 반환된 컬렉션의 항목 중 하나로 나타납니다.  
  
 <xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A> 속성은 특성이 네임스페이스 선언인지 여부를 나타냅니다.  
  
```vb  
Dim root As XElement = _   
<Root  
    xmlns='http://www.adventure-works.com'  
    xmlns:fc='www.fourthcoffee.com'  
    AnAttribute='abc'/>  
For Each att As XAttribute In root.Attributes()  
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, _  
                      att.IsNamespaceDeclaration)  
Next  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
xmlns="http://www.adventure-works.com"  IsNamespaceDeclaration:True  
xmlns:fc="www.fourthcoffee.com"  IsNamespaceDeclaration:True  
AnAttribute="abc"  IsNamespaceDeclaration:False  
```  
  
### <a name="xpath-axis-methods-do-not-return-child-white-space-of-xdocument"></a>XPath 축 메서드에서 XDocument의 자식 공백을 반환하지 않음  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 텍스트 노드에 공백만 포함되어 있는 경우 <xref:System.Xml.Linq.XDocument>의 자식 텍스트 노드를 허용합니다. 그러나 XPath 개체 모델에서는 문서의 자식 노드로 공백을 포함하지 않으므로 <xref:System.Xml.Linq.XDocument> 축을 사용하여 <xref:System.Xml.Linq.XContainer.Nodes%2A>의 자식을 반복할 때 공백 텍스트 노드가 반환됩니다. 그러나 XPath 축 메서드를 사용하여 <xref:System.Xml.Linq.XDocument>의 자식을 반복하는 경우에는 공백 텍스트 노드가 반환되지 않습니다.  
  
```vb  
' Create a document with some white space child nodes of the document.  
Dim root As XDocument = XDocument.Parse( _  
"<?xml version='1.0' encoding='utf-8' standalone='yes'?>" & _  
vbNewLine & "<Root/>" & vbNewLine & "<!--a comment-->" & vbNewLine, _  
LoadOptions.PreserveWhitespace)  
  
' Count the white space child nodes using LINQ to XML.  
Console.WriteLine(root.Nodes().OfType(Of XText)().Count())  
  
' Count the white space child nodes using XPathEvaluate.  
Dim nodes As IEnumerable = CType(root.XPathEvaluate("text()"), IEnumerable)  
Console.WriteLine(nodes.OfType(Of XText)().Count())  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
3  
0  
```  
  
### <a name="xdeclaration-objects-are-not-nodes"></a>XDeclaration 개체는 노드가 아님  
 <xref:System.Xml.Linq.XDocument>의 자식 노드를 반복할 때 XML 선언 개체가 표시되지 않습니다. XML 선언 개체는 문서의 자식 노드가 아니라 문서의 속성입니다.  
  
```vb  
Dim doc As XDocument = _  
<?xml version='1.0' encoding='utf-8' standalone='yes'?>  
<Root/>  
  
doc.Save("Temp.xml")  
Console.WriteLine(File.ReadAllText("Temp.xml"))  
  
' This shows that there is only one child node of the document.  
Console.WriteLine(doc.Nodes().Count())  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root />  
1  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic (Advanced LINQ to XML 프로그래밍)](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
