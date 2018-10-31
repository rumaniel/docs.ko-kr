---
title: 변형 과정에서 XPathNodeIterator의 역할
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 2bc6ddc6-674a-4f75-b264-abc35e4e5857
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6f71d409729707f4af93fd7f8d5b82a99404579b
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836055"
---
# <a name="xpathnodeiterator-in-transformations"></a>변형 과정에서 XPathNodeIterator의 역할
<xref:System.Xml.XPath.XPathNodeIterator>는 XPath(XML Path Language) 쿼리의 결과로 만들어진 노드 집합이나 노드 집합 메서드를 사용하여 노드 집합으로 변환된 결과 트리 조각을 반복하기 위한 메서드를 제공합니다. <xref:System.Xml.XPath.XPathNodeIterator>를 사용하면 해당 노드 집합 내의 노드를 반복할 수 있습니다. 노드 집합을 검색한 후 <xref:System.Xml.XPath.XPathNodeIterator> 클래스는 선택한 노드 집합에 대해 앞으로만 이동 가능한 읽기 전용 커서를 제공합니다. 노드 집합은 문서 순서에 따라 만들어지므로 이 메서드를 호출하면 문서 순서에서 다음 노드로 이동하게 됩니다. <xref:System.Xml.XPath.XPathNodeIterator>는 집합에 속하는 모든 노드의 노드 트리를 빌드하지 않습니다. 대신 트리에서 이동하는 것을 나타내는 원본으로 사용하는 노드를 노출하는 데이터에 대한 단일 노드 창을 제공합니다. <xref:System.Xml.XPath.XPathNodeIterator> 클래스에서 사용할 수 있는 메서드 및 속성을 통해 현재 노드에서 정보를 가져올 수 있습니다. 사용 가능한 메서드 및 속성 목록을 보려면 <xref:System.Windows.Forms.ToolBar>를 참조하세요.  
  
 <xref:System.Xml.XPath.XPathNodeIterator>는 XPath 쿼리에서 만든 노드 집합에서 앞으로만 이동하기 때문에 이동 방법은 <xref:System.Xml.XPath.XPathNodeIterator.MoveNext%2A> 메서드를 사용하는 것입니다. 이 메서드의 반환 형식은 `Boolean`이며 선택된 다음 노드로 이동할 경우 `true`를, 더 이상 선택된 노드가 없는 경우에는 `false`를 반환합니다. 다음은 `true`가 반환되는 경우에 사용할 수 있는 속성 목록입니다.  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.Current%2A>  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.CurrentPosition%2A>  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.Count%2A>  
  
 노드 집합을 처음 확인하는 경우에는 <xref:System.Xml.XPath.XPathNodeIterator.MoveNext%2A>를 호출하여 <xref:System.Xml.XPath.XPathNodeIterator>를 선택된 집합의 첫 번째 노드에 배치해야 합니다. 그러면 while 루프를 작성할 수 있습니다.  
  
 다음 코드 예제에서는 <xref:System.Xml.XPath.XPathNodeIterator>를 <xref:System.Xml.Xsl.XslTransform>의 매개 변수로 <xref:System.Xml.Xsl.XsltArgumentList>에 전달하는 방법을 보여 줍니다. 코드의 입력은 **books.xml**이고 스타일시트는 **text.xsl**입니다. **test.xml** 파일은 <xref:System.Xml.XPath.XPathDocument>입니다.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Xsl  
Imports System.Xml.XPath  
Imports System.Text  
  
Public Class sample  
  
   Public Shared Sub Main()  
      Dim Doc As New XPathDocument("books.xml")  
      Dim nav As XPathNavigator = Doc.CreateNavigator()  
      Dim Iterator As XPathNodeIterator = nav.Select("/bookstore/book")  
  
      Dim arg As New XsltArgumentList()  
      arg.AddParam("param1", "", Iterator)  
  
      Dim xslt As New XslTransform()  
      xslt.Load("test.xsl")  
  
      Dim xd As New XPathDocument("test.xml")  
  
      Dim strmTemp = New FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite)  
      xslt.Transform(xd, arg, strmTemp, Nothing)  
   End Sub 'Main  
End Class 'sample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Xsl;  
using System.Xml.XPath;  
using System.Text;  
  
public class sample  
{  
    public static void Main()  
    {  
        XPathDocument Doc = new XPathDocument("books.xml");  
        XPathNavigator nav = Doc.CreateNavigator();  
        XPathNodeIterator Iterator = nav.Select("/bookstore/book");  
  
        XsltArgumentList arg = new XsltArgumentList();  
        arg.AddParam("param1", "", Iterator);  
  
        XslTransform xslt = new XslTransform();  
        xslt.Load("test.xsl");  
  
        XPathDocument xd = new XPathDocument("test.xml");  
  
        Stream strmTemp = new FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite);  
        xslt.Transform(xd, arg, strmTemp, null);  
    }  
}  
```  
  
## <a name="booksxml"></a>books.xml  
  
```xml  
<?xml version='1.0'?>  
<!-- This file represents a fragment of a book store inventory database. -->  
<bookstore specialty="novel">  
    <book style="autobiography">  
    <title>Seven Years in Trenton</title>  
        <author>  
            <first-name>Jay</first-name>  
            <last-name>Adams</last-name>  
            <award>Trenton Literary Review Honorable Mention</award>  
            <country>USA</country>  
        </author>  
        <price>12</price>  
    </book>  
    <book style="textbook">  
        <title>History of Trenton</title>  
        <author>  
            <first-name>Kim</first-name>  
            <last-name>Akers</last-name>  
            <publication>  
                Selected Short Stories of  
                <first-name>Scott</first-name>  
                <last-name>Bishop</last-name>  
                <country>US</country>  
            </publication>  
        </author>  
        <price>55</price>  
    </book>  
</bookstore>  
```  
  
## <a name="testxsl"></a>test.xsl  
  
```xml  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
xmlns:msxsl="urn:schemas-microsoft-com:xslt" exclude-result-prefixes="msxsl">  
  
<xsl:output method="xml" indent="yes"/>  
<xsl:param name="param1"/>  
  
<xsl:template match="/">  
    <out>  
        <xsl:for-each select="$param1/title">  
            <title><xsl:value-of select="."/></title>  
        </xsl:for-each>  
    </out>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
## <a name="testxml"></a>test.xml  
  
```xml  
<Title attr="Test">this is a test</Title>  
```  
  
## <a name="output-outxml"></a>출력(out.xml)  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<out>  
  <title>Seven Years in Trenton</title>  
  <title>History of Trenton</title>  
</out>  
```  
  
## <a name="see-also"></a>참고 항목

- [XslTransform 클래스의 XSLT 프로세서 구현](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)
