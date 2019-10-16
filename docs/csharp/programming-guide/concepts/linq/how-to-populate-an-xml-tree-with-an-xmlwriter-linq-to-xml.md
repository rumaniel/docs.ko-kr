---
title: '방법: XmlWriter를 사용하여 XML 트리 채우기(LINQ to XML)(C#)'
ms.date: 07/20/2015
ms.assetid: cd5674d1-5c54-4efc-ba68-e23b2875295f
ms.openlocfilehash: 88b088ddad54d1fef67cb4c86f8df4eee7bf3662
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593110"
---
# <a name="how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml-c"></a>방법: XmlWriter를 사용하여 XML 트리 채우기(LINQ to XML)(C#)
XML 트리를 채우는 한 가지 방법은 <xref:System.Xml.Linq.XContainer.CreateWriter%2A>를 사용하여 <xref:System.Xml.XmlWriter>를 만든 다음 <xref:System.Xml.XmlWriter>에 쓰는 것입니다. XML 트리는 <xref:System.Xml.XmlWriter>에 쓴 모든 노드로 채워집니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에 써야 하는 <xref:System.Xml.XmlWriter> 등의 다른 클래스와 함께 <xref:System.Xml.Xsl.XslCompiledTransform>을 사용할 때 이 메서드를 일반적으로 사용합니다.  
  
## <a name="example"></a>예  
 <xref:System.Xml.Linq.XContainer.CreateWriter%2A>를 사용할 수 있는 한 가지 경우는 XSLT 변환을 호출할 때입니다. 이 예제에서는 XML 트리를 만들고 XML 트리에서 <xref:System.Xml.XmlReader>를 만든 다음 <xref:System.Xml.XmlWriter>를 만들어 새 문서에 씁니다. 그런 다음 XSLT 변환을 호출하여 <xref:System.Xml.XmlReader> 및 <xref:System.Xml.XmlWriter>를 전달합니다. 변환이 성공적으로 완료된 후 새 XML 트리가 변환의 결과로 채워집니다.  
  
```csharp  
string xslMarkup = @"<?xml version='1.0'?>  
<xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>  
    <xsl:template match='/Parent'>  
        <Root>  
            <C1>  
            <xsl:value-of select='Child1'/>  
            </C1>  
            <C2>  
            <xsl:value-of select='Child2'/>  
            </C2>  
        </Root>  
    </xsl:template>  
</xsl:stylesheet>";  
  
XDocument xmlTree = new XDocument(  
    new XElement("Parent",  
        new XElement("Child1", "Child1 data"),  
        new XElement("Child2", "Child2 data")  
    )  
);  
  
XDocument newTree = new XDocument();  
using (XmlWriter writer = newTree.CreateWriter())  
{  
    // Load the style sheet.  
    XslCompiledTransform xslt = new XslCompiledTransform();  
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));  
  
    // Execute the transformation and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer);  
}  
  
Console.WriteLine(newTree);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.Linq.XContainer.CreateWriter%2A>
- <xref:System.Xml.XmlWriter>
- <xref:System.Xml.Xsl.XslCompiledTransform>
- [XML 트리 만들기(C#)](./linq-to-xml-overview.md)
