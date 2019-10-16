---
title: 스타일시트 매개 변수 및 확장 개체의 XsltArgumentList
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: de2f0dce-6b98-4908-bba7-ed150cc50355
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9d08399933f37c4110639bf1f4a81f222dd597b4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910315"
---
# <a name="xsltargumentlist-for-style-sheet-parameters-and-extension-objects"></a>스타일시트 매개 변수 및 확장 개체의 XsltArgumentList
<xref:System.Xml.Xsl.XsltArgumentList> 클래스에는 XSLT(Extensible Stylesheet Language for Transformations) 매개 변수와 XSLT 확장 개체가 포함되어 있습니다. 이러한 매개 변수와 확장명 개체는 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드에 전달될 경우 스타일시트에서 호출할 수 있습니다.  
  
> [!NOTE]
> .NET Framework 2.0에서는 <xref:System.Xml.Xsl.XslTransform> 및 <xref:System.Xml.Xsl.XsltArgumentList> 클래스가 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)을 참조하세요.  
  
 <xref:System.Xml.Xsl.XsltArgumentList> 클래스에는 XSLT 매개 변수와 XSLT 확장 개체가 포함되어 있습니다. 이러한 매개 변수와 확장명 개체는 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드에 전달될 경우 스타일시트에서 호출할 수 있습니다.  
  
 포함 스크립트를 사용하는 대신 개체를 전달하면 다음과 같은 이점을 활용할 수 있습니다.  
  
- 클래스의 캡슐화 및 재사용에 효과적입니다.  
  
- 스타일시트를 더 작게 유지하고 보다 쉽게 관리할 수 있습니다.  
  
- 지원되는 <xref:System> 네임스페이스의 집합 내에 정의된 네임스페이스 이외의 다른 네임스페이스에 속하는 클래스에서 메서드를 호출할 수 있습니다.  
  
- <xref:System.Xml.XPath.XPathNodeIterator>를 사용하여 스타일시트에 결과 트리 조각을 전달할 수 있습니다.  
  
## <a name="xslt-style-sheet-parameters"></a>XSLT 스타일시트 매개 변수  
 <xref:System.Xml.Xsl.XsltArgumentList> 메서드를 사용하여 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>에 XSLT 매개 변수를 추가합니다. 그러면 정규화된 이름과 네임스페이스 URI(Uniform Resource Identifier)가 매개 변수 개체와 연결됩니다.  
  
 매개 변수 개체는 W3C(World Wide Web 컨소시엄) 형식과 일치해야 합니다. 다음 표에서는 해당하는 W3C 형식과 해당 .NET Framework 클래스(형식), 그리고 W3C 형식이 XPath(XML Path Language) 형식인지, 또는 XSLT 형식인지를 보여 줍니다.  
  
|W3C 형식|해당 .NET Framework 클래스(형식)|XPath 형식 또는 XSLT 형식|  
|--------------|----------------------------------------------|-----------------------------|  
|문자열|System.String|XPath|  
|부울|System.Boolean|XPath|  
|수|System.Double|XPath|  
|결과 트리 조각|System.Xml.XPath.XPathNavigator|XSLT|  
|노드 집합|System.Xml.XPath.XPathNodeIterator|XPath|  
  
 매개 변수 개체가 위 클래스에 해당하지 않으면 Double 또는 String 형식이 적절히 적용됩니다. Int16, UInt16, Int32, UInt32, Int64, UInt64, Single 및 Decimal 형식은 Double 형식이 되며 기타 모든 형식은 `ToString` 메서드를 사용하여 String 형식이 됩니다.  
  
#### <a name="to-use-the-xslt-parameter-the-user-needs-to-do-the-following"></a>XSLT 매개 변수를 사용하려면 다음 작업을 수행해야 합니다.  
  
1. <xref:System.Xml.Xsl.XsltArgumentList>을 사용하여 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>를 만들고 개체를 추가합니다.  
  
2. 스타일시트에서 매개 변수를 호출합니다.  
  
3. <xref:System.Xml.Xsl.XsltArgumentList>를 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드에 전달합니다.  
  
### <a name="example"></a>예  
 다음 예제에서는 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 메서드를 사용하여 계산된 할인 기간을 유지하는 매개 변수를 만듭니다. 할인 기간은 주문 날짜로부터 20일 동안으로 계산됩니다.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public class Sample  
  
   Private Const filename As String = "order.xml"  
   Private Const stylesheet As String = "discount.xsl"  
  
   Public Shared Sub Main()  
  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XsltArgumentList.  
    Dim xslArg As XsltArgumentList = New XsltArgumentList  
  
    'Calculate the discount date.  
    Dim today As DateTime = DateTime.Now  
    Dim d As DateTime = today.AddDays(20)  
    xslArg.AddParam("discount", "", d.ToString())  
  
    'Create an XmlTextWriter to handle the output.  
    Dim writer As XmlTextWriter = New XmlTextWriter("orderout.xml", Nothing)  
  
    'Transform the file.  
    xslt.Transform(doc, xslArg, writer, Nothing)  
  
    writer.Close()  
  
  End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.XPath;  
using System.Xml.Xsl;  
  
public class Sample  
{  
   private const String filename = "order.xml";  
   private const String stylesheet = "discount.xsl";  
  
   public static void Main() {  
  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XsltArgumentList.  
    XsltArgumentList xslArg = new XsltArgumentList();  
  
    //Calculate the discount date.  
    DateTime today = DateTime.Now;  
    DateTime d = today.AddDays(20);  
    xslArg.AddParam("discount", "", d.ToString());  
  
    //Create an XmlTextWriter to handle the output.  
    XmlTextWriter writer = new XmlTextWriter("orderout.xml", null);  
  
    //Transform the file.  
    xslt.Transform(doc, xslArg, writer, null);  
    writer.Close();  
  }  
}  
```  
  
### <a name="input"></a>입력  
 order.xml  
  
```xml  
<!--Represents a customer order-->  
<order>  
  <book ISBN='10-861003-324'>  
    <title>The Handmaid's Tale</title>  
    <price>19.95</price>  
  </book>  
  <cd ISBN='2-3631-4'>  
    <title>Americana</title>  
    <price>16.95</price>  
  </cd>  
</order>  
```  
  
 discount.xsl  
  
```xml  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
  <xsl:param name="discount"/>  
  <xsl:template match="/">  
    <order>  
      <xsl:variable name="sub-total" select="sum(//price)"/>  
      <total><xsl:value-of select="$sub-total"/></total>  
      15% discount if paid by: <xsl:value-of select="$discount"/>  
    </order>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
### <a name="output"></a>Output  
  
```xml  
<order>  
   <total>36.9</total>   
   15% discount if paid by: 5/6/2001 5:01:15 PM   
</order>  
```  
  
## <a name="xslt-extension-objects"></a>XSLT 확장명 개체  
 <xref:System.Xml.Xsl.XsltArgumentList> 메서드를 사용하여 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>에 XSLT 확장명 개체를 추가합니다. 이 때 정규화된 이름과 네임스페이스 URI가 확장 개체와 연결됩니다.  
  
 개체가 추가될 때 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>의 호출자는 보안 정책에서 완전히 신뢰되어야 합니다. 호출자가 일부 신뢰되는 경우에는 추가 작업이 실패합니다.  
  
 개체가 추가되더라도 성공적으로 실행된다고 보장할 수는 없습니다. <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드가 호출되면 <xref:System.Xml.Xsl.XslTransform.Load%2A> 시 제공된 증명 정보에 따라 권한이 판별되어 해당 권한 집합이 전체 변환 프로세스에 지정됩니다. 확장명 개체가 해당 권한 집합에 없는 권한을 요구하는 작업을 시작하려고 하면 예외가 throw됩니다.  
  
 확장명 개체에서 반환된 데이터 형식은 네 가지 기본 XPath 데이터 형식인 숫자, 문자열, 부울 및 노드 집합 중 하나입니다.  
  
#### <a name="to-use-the-xslt-extension-object-the-user-needs-to-do-the-following"></a>XSLT 확장 개체를 사용하려면 다음 작업을 수행해야 합니다.  
  
1. <xref:System.Xml.Xsl.XsltArgumentList>를 사용하여 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>를 만들고 확장명 개체를 추가합니다.  
  
2. 스타일시트에서 확장 개체를 호출합니다.  
  
3. <xref:System.Xml.Xsl.XsltArgumentList>를 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드에 전달합니다.  
  
### <a name="example"></a>예  
 다음 예제에서는 반지름이 주어진 원의 원주를 계산합니다.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public Class Sample  
   Private Const filename As String = "number.xml"  
   Private Const stylesheet As String = "circle.xsl"  
  
   Public Shared Sub Main()  
        Dim test As Sample = New Sample  
   End Sub  
  
  Public Sub New()  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XsltArgumentList.  
    Dim xslArg As XsltArgumentList = New XsltArgumentList  
  
    'Add an object to calculate the circumference of the circle.  
    Dim obj As Calculate = New Calculate  
    xslArg.AddExtensionObject("urn:myObj", obj)  
  
    'Create an XmlTextWriter to output to the console.  
    Dim writer As XmlTextWriter = New XmlTextWriter(Console.Out)  
  
    'Transform the file.  
    xslt.Transform(doc, xslArg, writer, Nothing)  
    writer.Close()  
  
  End Sub  
  
  'Calculates the circumference of a circle given the radius.  
  Public Class Calculate  
  
    Private circ As double = 0  
  
    Public Function Circumference(radius As Double) As Double  
       circ = Math.PI*2*radius  
       Return circ  
    End Function  
  End Class  
End Class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.XPath;  
using System.Xml.Xsl;  
  
public class Sample  
{  
   private const String filename = "number.xml";  
   private const String stylesheet = "circle.xsl";  
  
   public static void Main() {  
  
        Sample test = new Sample();  
    }  
  
  public Sample() {  
  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XsltArgumentList.  
    XsltArgumentList xslArg = new XsltArgumentList();  
  
    //Add an object to calculate the circumference of the circle.  
    Calculate obj = new Calculate();  
    xslArg.AddExtensionObject("urn:myObj", obj);  
  
    //Create an XmlTextWriter to output to the console.  
    XmlTextWriter writer = new XmlTextWriter(Console.Out);  
  
    //Transform the file.  
    xslt.Transform(doc, xslArg, writer, null);  
    writer.Close();  
  
  }  
  
  //Calculates the circumference of a circle given the radius.  
  public class Calculate {  
  
    private double circ = 0;  
  
    public double Circumference(double radius){  
       circ = Math.PI*2*radius;  
       return circ;  
    }  
  }  
}  
```  
  
### <a name="input"></a>입력  
 number.xml  
  
```xml  
<?xml version='1.0'?>  
<data>  
  <circle>  
    <radius>12</radius>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
  </circle>  
</data>    
```  
  
 circle.xsl  
  
```xml  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
    xmlns:myObj="urn:myObj">  
  
  <xsl:template match="data">  
  <circles>  
  <xsl:for-each select="circle">  
    <circle>  
    <xsl:copy-of select="node()"/>  
       <circumference>  
          <xsl:value-of select="myObj:Circumference(radius)"/>          
       </circumference>  
    </circle>  
  </xsl:for-each>  
  </circles>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
### <a name="output"></a>Output  
 `<circles xmlns:myObj="urn:myObj">`  
  
 `<circle>`  
  
 `<radius>12</radius>`  
  
 `<circumference>75.398223686155</circumference>`  
  
 `</circle>`  
  
 `<circle>`  
  
 `<radius>37.5</radius>`  
  
 `<circumference>235.61944901923448</circumference>`  
  
 `</circle>`  
  
 `</circles>`  
  
## <a name="see-also"></a>참고 항목

- [XslTransform 클래스의 XSLT 프로세서 구현](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)
