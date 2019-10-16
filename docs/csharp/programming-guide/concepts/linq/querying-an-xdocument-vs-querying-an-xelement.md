---
title: XDocument 쿼리와 XElement 쿼리 비교(C#)
ms.date: 07/20/2015
ms.assetid: 46221ff5-62ee-4de8-93ba-66465facb5c1
ms.openlocfilehash: 475c77934ad535bad9ef79ff58bbddf991dc8f5c
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253133"
---
# <a name="querying-an-xdocument-vs-querying-an-xelement-c"></a>XDocument 쿼리와 XElement 쿼리 비교(C#)
<xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>를 통해 문서를 로드하는 경우에는 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>를 통해 로드하는 경우와 약간 다르게 쿼리를 작성해야 합니다.  
  
## <a name="comparison-of-xdocumentload-and-xelementload"></a>XDocument.Load와 XElement.Load의 비교  
 <xref:System.Xml.Linq.XElement>를 통해 XML 문서를 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>에 로드하면 XML 트리의 루트에 있는 <xref:System.Xml.Linq.XElement>에 로드된 문서의 루트 요소가 포함되어 있습니다. 그러나 <xref:System.Xml.Linq.XDocument>를 통해 동일한 XML 문서를 <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>에 로드하면 트리의 루트가 <xref:System.Xml.Linq.XDocument> 노드이고 로드된 문서의 루트 요소가 <xref:System.Xml.Linq.XElement>의 허용된 하나의 자식 <xref:System.Xml.Linq.XDocument> 노드입니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 축은 루트 노드와 상대적으로 작동합니다.  
  
 이 첫 번째 예제에서는 <xref:System.Xml.Linq.XElement.Load%2A>를 사용하여 XML 트리를 로드한 다음 트리 루트의 자식 요소에 대해 쿼리합니다.  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XElement.Load");  
Console.WriteLine("----");  
XElement doc = XElement.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 예상대로 이 예제는 다음과 같이 출력됩니다.  
  
```output  
Querying tree loaded with XElement.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
 다음 예제는 XML 트리가 <xref:System.Xml.Linq.XDocument> 대신 <xref:System.Xml.Linq.XElement>에 로드되는 점을 제외하고 위의 예제와 동일합니다.  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
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
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Root.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 이 쿼리는 이제 <xref:System.Xml.Linq.XElement>에서 시작하는 트리에 대한 쿼리와 동일한 방식으로 수행됩니다. 예제의 결과는 다음과 같습니다.  
  
```output  
Querying tree loaded with XDocument.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  