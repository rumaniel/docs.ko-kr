---
title: XDocument 쿼리와 XElement (Visual Basic) 쿼리
ms.date: 07/20/2015
ms.assetid: 2d111f84-0ded-4cde-8d93-5440557a726d
ms.openlocfilehash: 4aba08319abeb21de79b3b8511044b8272402984
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834942"
---
# <a name="querying-an-xdocument-vs-querying-an-xelement-visual-basic"></a>XDocument 쿼리와 XElement (Visual Basic) 쿼리
<xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>를 통해 문서를 로드하는 경우에는 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>를 통해 로드하는 경우와 약간 다르게 쿼리를 작성해야 합니다.  
  
## <a name="comparison-of-xdocumentload-and-xelementload"></a>XDocument.Load와 XElement.Load의 비교  
 <xref:System.Xml.Linq.XElement>를 통해 XML 문서를 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>에 로드하면 XML 트리의 루트에 있는 <xref:System.Xml.Linq.XElement>에 로드된 문서의 루트 요소가 포함되어 있습니다. 그러나 <xref:System.Xml.Linq.XDocument>를 통해 동일한 XML 문서를 <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>에 로드하면 트리의 루트가 <xref:System.Xml.Linq.XDocument> 노드이고 로드된 문서의 루트 요소가 <xref:System.Xml.Linq.XElement>의 허용된 하나의 자식 <xref:System.Xml.Linq.XDocument> 노드입니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 축은 루트 노드와 상대적으로 작동합니다.  
  
 이 첫 번째 예제에서는 <xref:System.Xml.Linq.XElement.Load%2A>를 사용하여 XML 트리를 로드한 다음 트리 루트의 자식 요소에 대해 쿼리합니다.  
  
```vb  
' Create a simple document and  write it to a file  
File.WriteAllText("Test.xml", "<Root>" + Environment.NewLine + _  
    "    <Child1>1</Child1>" + Environment.NewLine + _  
    "    <Child2>2</Child2>" + Environment.NewLine + _  
    "    <Child3>3</Child3>" + Environment.NewLine + _  
    "</Root>")  
  
Console.WriteLine("Querying tree loaded with XElement.Load")  
Console.WriteLine("----")  
Dim doc As XElement = XElement.Load("Test.xml")  
Dim childList As IEnumerable(Of XElement) = _  
        From el In doc.Elements() _  
        Select el  
For Each e As XElement In childList  
    Console.WriteLine(e)  
Next  
```  
  
 예상대로 이 예제는 다음과 같이 출력됩니다.  
  
```console
Querying tree loaded with XElement.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
 다음 예제는 XML 트리가 <xref:System.Xml.Linq.XDocument> 대신 <xref:System.Xml.Linq.XElement>에 로드되는 점을 제외하고 위의 예제와 동일합니다.  
  
```vb  
' Create a simple document and  write it to a file  
File.WriteAllText("Test.xml", "<Root>" + Environment.NewLine + _  
    "    <Child1>1</Child1>" + Environment.NewLine + _  
    "    <Child2>2</Child2>" + Environment.NewLine + _  
    "    <Child3>3</Child3>" + Environment.NewLine + _  
    "</Root>")  
  
Console.WriteLine("Querying tree loaded with XDocument.Load")  
Console.WriteLine("----")  
Dim doc As XDocument = XDocument.Load("Test.xml")  
Dim childList As IEnumerable(Of XElement) = _  
        From el In doc.Elements() _  
        Select el  
For Each e As XElement In childList  
    Console.WriteLine(e)  
Next  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console
Querying tree loaded with XDocument.Load  
----  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
</Root>  
```  
  
 동일한 쿼리에서 세 자식 노드 대신 하나의 `Root` 노드를 반환했습니다.  
  
 이를 처리하는 한 가지 방법은 축 메서드에 액세스하기 전에 다음과 같이 <xref:System.Xml.Linq.XDocument.Root%2A> 속성을 사용하는 것입니다.  
  
```vb  
' Create a simple document and  write it to a file  
File.WriteAllText("Test.xml", "<Root>" + Environment.NewLine + _  
    "    <Child1>1</Child1>" + Environment.NewLine + _  
    "    <Child2>2</Child2>" + Environment.NewLine + _  
    "    <Child3>3</Child3>" + Environment.NewLine + _  
    "</Root>")  
  
Console.WriteLine("Querying tree loaded with XDocument.Load")  
Console.WriteLine("----")  
Dim doc As XDocument = XDocument.Load("Test.xml")  
Dim childList As IEnumerable(Of XElement) = _  
        From el In doc.Root.Elements() _  
        Select el  
For Each e As XElement In childList  
    Console.WriteLine(e)  
Next  
```  
  
 이 쿼리는 이제 <xref:System.Xml.Linq.XElement>에서 시작하는 트리에 대한 쿼리와 동일한 방식으로 수행됩니다. 예제의 결과는 다음과 같습니다.  
  
```console
Querying tree loaded with XDocument.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
## <a name="see-also"></a>참조

- [기본 쿼리 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
