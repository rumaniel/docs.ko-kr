---
title: XElement 클래스 개요(C#)
ms.date: 07/20/2015
ms.assetid: 2b9f0cd8-a1d1-4037-accf-0f38a410fa11
ms.openlocfilehash: e742741f56f3e39f93b9f1d6be30a54a4ede67f3
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590887"
---
# <a name="xelement-class-overview-c"></a>XElement 클래스 개요(C#)
<xref:System.Xml.Linq.XElement> 클래스는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]의 기본 클래스 중 하나이며 XML 요소를 나타냅니다. 이 클래스를 사용하여 요소를 만들거나, 요소의 내용을 변경하거나, 자식 요소를 추가, 변경 또는 삭제하거나, 특성을 요소에 추가하거나, 요소의 내용을 텍스트 형태로 serialize할 수 있습니다. 또한 <xref:System.Xml?displayProperty=nameWithType>, <xref:System.Xml.XmlReader> 및 <xref:System.Xml.XmlWriter>과 같은 <xref:System.Xml.Xsl.XslCompiledTransform>의 다른 클래스와 상호 운용할 수도 있습니다.  
  
이 항목에서는 <xref:System.Xml.Linq.XElement> 클래스에서 제공하는 기능에 대해 설명합니다.  
  
## <a name="constructing-xml-trees"></a>XML 트리 생성  
 다음과 같은 다양한 방법으로 XML 트리를 생성할 수 있습니다.  
  
- 코드에서 XML 트리를 생성할 수 있습니다. 자세한 내용은 [XML 트리 만들기(C#)](./linq-to-xml-overview.md)를 참조하세요.  
  
- <xref:System.IO.TextReader>, 텍스트 파일 또는 웹 주소(URL)와 같은 다양한 소스에서 XML의 구문을 분석할 수 있습니다. 자세한 내용은 [XML 구문 분석(C#)](./how-to-parse-a-string.md)을 참조하세요.  
  
- <xref:System.Xml.XmlReader>를 사용하여 트리를 채울 수 있습니다. 자세한 내용은 <xref:System.Xml.Linq.XNode.ReadFrom%2A>을 참조하세요.  
  
- 내용을 <xref:System.Xml.XmlWriter>에 쓸 수 있는 모듈이 있는 경우 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 메서드를 사용하여 작성기를 만들고 모듈에 작성기를 전달한 다음 <xref:System.Xml.XmlWriter>에 쓴 내용을 사용하여 XML 트리를 채울 수 있습니다.  
  
 그러나 XML 트리를 만드는 가장 일반적인 방법은 다음과 같습니다.  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 XML 트리를 만드는 또 다른 일반적인 방법에는 다음 예제에서와 같이 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리의 결과를 사용하여 XML 트리를 채우는 작업이 포함됩니다.  
  
```csharp  
XElement srcTree = new XElement("Root",  
    new XElement("Element", 1),  
    new XElement("Element", 2),  
    new XElement("Element", 3),  
    new XElement("Element", 4),  
    new XElement("Element", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    from el in srcTree.Elements()  
    where (int)el > 2  
    select el  
);  
Console.WriteLine(xmlTree);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="serializing-xml-trees"></a>XML 트리 serialization  
 XML 트리를 <xref:System.IO.File>, <xref:System.IO.TextWriter> 또는 <xref:System.Xml.XmlWriter>로 serialize할 수 있습니다.  
  
 자세한 내용은 [XML 트리 serialize(C#)](./preserving-white-space-while-serializing.md)를 참조하세요.  
  
## <a name="retrieving-xml-data-via-axis-methods"></a>축 메서드를 통해 XML 데이터 검색  
 축 메서드를 사용하여 특성, 자식 요소, 하위 요소 및 상위 요소를 검색할 수 있습니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리는 축 메서드에 대해 작동하며 XML 트리를 탐색하고 처리하는 융통성 있고 강력한 몇 가지 방법을 제공합니다.  
  
 자세한 내용은 [LINQ to XML 축(C#)](./linq-to-xml-axes-overview.md)을 참조하세요.  
  
## <a name="querying-xml-trees"></a>XML 트리 쿼리  
 XML 트리에서 데이터를 추출하는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 작성할 수 있습니다.  
  
 자세한 내용은 [XML 트리 쿼리(C#)](./how-to-find-an-element-with-a-specific-attribute.md)를 참조하세요.  
  
## <a name="modifying-xml-trees"></a>XML 트리 수정  
 내용이나 특성을 변경하는 등의 다양한 방법으로 요소를 수정할 수 있습니다. 또한 부모에서 요소를 제거할 수도 있습니다.  
  
 자세한 내용은 [XML 트리 수정(LINQ to XML)(C#)](./in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [LINQ to XML 프로그래밍 개요(C#)](serializing-to-files-textwriters-and-xmlwriters.md)
