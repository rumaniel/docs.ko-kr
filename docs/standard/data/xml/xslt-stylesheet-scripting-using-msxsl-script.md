---
title: <msxsl:script>를 사용한 XSLT 스타일시트 스크립팅
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 60e2541b-0cea-4b2e-a4fa-85f4c50f1bef
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d3d1658b47d2cda344e2ec1fe7b48c929005563b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912054"
---
# <a name="xslt-stylesheet-scripting-using-msxslscript"></a>\<msxsl:script>를 사용한 XSLT 스타일시트 스크립팅
<xref:System.Xml.Xsl.XslTransform> 클래스는 `script` 요소를 사용하여 포함 스크립트를 지원합니다.  
  
> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> 클래스는 .NET Framework 2.0에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)을 참조하세요.  
  
 <xref:System.Xml.Xsl.XslTransform> 클래스는 `script` 요소를 사용하여 포함 스크립트를 지원합니다. 스타일시트가 로드될 때 정의된 모든 함수는 클래스 정의에서 래핑되어 MSIL(Microsoft Intermediate Language)로 컴파일되므로 성능이 저하되지 않습니다.  
  
 `<msxsl:script>` 요소는 다음에 정의되어 있습니다.  
  
```xml  
<msxsl:script language = "language-name" implements-prefix = "prefix of user namespace"> </msxsl:script>  
```  
  
 여기서 `msxsl`은 네임스페이스 `urn:schemas-microsoft-com:xslt`에 바인딩되는 접두사입니다.  
  
 `language` 특성은 필수 항목은 아니지만, 지정할 경우 값이 C#, VB, JScript, JavaScript, VisualBasic 또는 CSharp 중 하나여야 합니다. 지정하지 않을 경우 언어 기본값은 JScript입니다. `language-name`은 대/소문자를 구분하지 않으므로 'JavaScript'와 'javascript'는 같습니다.  
  
 `implements-prefix` 특성은 필수 항목입니다. 이 특성은 네임스페이스를 선언하고 스크립트 블록에 연결하는 데 사용됩니다. 이 특성 값은 네임스페이스를 나타내는 접두사입니다. 이 네임스페이스는 스타일시트에서 정의할 수 있습니다.  
  
 `msxsl:script` 요소가 네임스페이스 `urn:schemas-microsoft-com:xslt`에 속하기 때문에 스타일시트에는 네임스페이스 선언 `xmlns:msxsl=urn:schemas-microsoft-com:xslt`가 있어야 합니다.  
  
 스크립트의 호출자에게 <xref:System.Security.Permissions.SecurityPermissionFlag> 액세스 권한이 없으면 스타일시트의 스크립트는 컴파일되지 않으며 <xref:System.Xml.Xsl.XslTransform.Load%2A>에 대한 호출도 실패합니다.  
  
 호출자에게 `UnmanagedCode` 권한이 없는 경우에는 스크립트가 컴파일되지만 로드할 때 제공된 증명 정보에 따라 허용되는 작업이 결정됩니다.  
  
 <xref:System.Xml.Xsl.XslTransform.Load%2A> 또는 <xref:System.Xml.XmlReader>를 사용하는 <xref:System.Xml.XPath.XPathNavigator> 메서드 중 하나를 사용하여 스타일시트를 로드하는 경우 <xref:System.Xml.Xsl.XslTransform.Load%2A> 매개 변수를 인수 중 하나로 사용하는 <xref:System.Security.Policy.Evidence> 오버로드를 사용해야 합니다. 증명 정보를 제공하려는 경우 호출자는 <xref:System.Security.Permissions.SecurityPermissionFlag> 권한이 있어야 스크립트 어셈블리에 대한 `Evidence`를 제공할 수 있습니다. 호출자에게 이 권한이 없으면 `Evidence` 매개 변수를 `null`로 설정할 수 있습니다. 그러면 <xref:System.Xml.Xsl.XslTransform.Load%2A> 함수는 스크립트를 찾는 데 실패합니다. `ControlEvidence` 권한은 충분히 신뢰할 수 있는 코드에만 부여되는 매우 강력한 권한으로 간주됩니다.  
  
 어셈블리에서 증명 정보를 가져오려면 `this.GetType().Assembly.Evidence`를 사용합니다. URI(Uniform Resource Identifier)에서 증명 정보를 가져오려면 `Evidence e = XmlSecureResolver.CreateEvidenceForUrl(stylesheetURI)`을 사용합니다.  
  
 <xref:System.Xml.Xsl.XslTransform.Load%2A>가 아닌 <xref:System.Xml.XmlResolver>를 사용하는 `Evidence` 메서드를 사용하는 경우 어셈블리의 보안 영역은 기본적으로 Full Trust가 됩니다. 자세한 내용은 <xref:System.Security.SecurityZone> 및 [명명된 권한 집합](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/4652tyx7(v=vs.100))을 참조하세요.  
  
 함수는 `msxsl:script` 요소 내에서 선언할 수 있습니다. 다음 표에서는 기본적으로 지원되는 네임스페이스를 보여 줍니다. 나열된 네임스페이스 외부에 있는 클래스는 사용할 수 있지만, 정규화되어야만 사용 가능합니다.  
  
|기본 네임스페이스|설명|  
|------------------------|-----------------|  
|시스템|System 클래스|  
|System.Collection|Collection 클래스|  
|System.Text|Text 클래스|  
|System.Text.RegularExpressions|정규식 클래스|  
|System.Xml|핵심 XML 클래스|  
|System.Xml.Xsl|XSLT 클래스|  
|System.Xml.XPath|XPath(XML Path Language) 클래스|  
|Microsoft.VisualBasic|Microsoft Visual Basic 스크립트용 클래스|  
  
 함수를 선언하면 해당 함수는 스크립트 블록 내에 포함됩니다. 스타일시트에는 여러 스크립트 블록이 포함될 수 있으며 각 블록은 서로 독립적으로 작동합니다. 즉, 스크립트 블록 내부에서 실행할 경우 같은 네임스페이스와 같은 스크립트 언어를 사용하도록 선언된 경우에만 다른 스크립트 블록에 정의된 함수를 호출할 수 있습니다. 각 스크립트 블록에서는 서로 다른 언어를 사용할 수 있고, 블록은 해당 언어 파서의 문법 규칙에 따라 구문 분석되기 때문에 사용하는 언어의 올바른 구문을 사용해야 합니다. 예를 들어, C# 스크립트 블록에서 XML comment 노드 `<!-- an XML comment -->`를 사용하면 오류가 발생합니다.  
  
 스크립트 함수에 정의된 인수와 반환 값은 W3C(World Wide Web 컨소시엄) XPath 또는 XSLT 형식 중 하나여야 합니다. 다음 표에서는 해당하는 W3C 형식과 해당 .NET Framework 클래스(형식), W3C 형식이 XPath 형식인지 아니면 XSLT 형식인지를 보여줍니다.  
  
|형식|해당 .NET Framework 클래스(형식)|XPath 형식 또는 XSLT 형식|  
|----------|----------------------------------------------|-----------------------------|  
|문자열|System.String|XPath|  
|부울|System.Boolean|XPath|  
|수|System.Double|XPath|  
|결과 트리 조각|System.Xml.XPath.XPathNavigator|XSLT|  
|노드 집합|System.Xml.XPath.XPathNodeIterator|XPath|  
  
 스크립트 함수가 다음 숫자 유형 중 하나를 사용하는 경우: Int16, UInt16, Int32, UInt32, Int64, UInt64, Single 또는 Decimal의 경우 W3C XPath 형식 숫자에 매핑되는 Double이 되어야 합니다. 기타 모든 형식은 `ToString` 메서드 호출을 통해 문자열 형식이 됩니다.  
  
 스크립트 함수에서 위에 설명되어 있지 않은 형식을 사용하거나 스타일시트를 <xref:System.Xml.Xsl.XslTransform> 개체에 로드할 때 함수가 컴파일되지 않으면 예외가 throw됩니다.  
  
 `msxsl:script` 요소를 사용하는 경우에는 언어에 관계없이 스크립트를 CDATA 섹션에 배치하는 것이 좋습니다. 예를 들어, 다음 XML에서는 코드를 배치할 CDATA 섹션 템플릿을 보여 줍니다.  
  
```xml  
<msxsl:script implements-prefix='yourprefix' language='CSharp'>  
    <![CDATA[  
    ... your code here ...  
    ]]>  
</msxsl:script>  
```  
  
 지정된 언어의 연산자, 식별자 또는 구분자가 XML로 잘못 해석될 위험이 있으므로 스크립트 내용을 CDATA 섹션에 배치하는 것이 좋습니다. 다음 예제에서는 스크립트에서 논리곱 연산자를 사용하는 방법을 보여 줍니다.  
  
```xml  
<msxsl:script implements-prefix='yourprefix' language='CSharp'>  
    public string book(string abc, string xyz)  
    {  
        if ((abc == bar) && (abc == xyz)) return bar + xyz;  
        else return null;  
    }  
</msxsl:script>  
```  
  
 이 경우 앰퍼샌드가 이스케이프되지 않기 때문에 예외가 throw됩니다. 문서는 XML로 로드되고 `msxsl:script` 요소 태그 사이의 텍스트에는 특별한 작업이 수행되지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 포함 스크립트를 사용하여 주어진 반지름으로 원의 원주를 계산합니다.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public Class Sample  
  
   Private Const filename As String = "number.xml"  
   Private Const stylesheet As String = "calc.xsl"  
  
   Public Shared Sub Main()  
  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XmlTextWriter to output to the console.               
    Dim writer As XmlTextWriter = New XmlTextWriter(Console.Out)  
    writer.Formatting = Formatting.Indented  
  
    'Transform the file.  
    xslt.Transform(doc, Nothing, writer, Nothing)  
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
   private const String filename = "number.xml";  
   private const String stylesheet = "calc.xsl";  
  
   public static void Main()  
   {  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XmlTextWriter to output to the console.               
    XmlTextWriter writer = new XmlTextWriter(Console.Out);  
    writer.Formatting = Formatting.Indented;  
  
    //Transform the file.  
    xslt.Transform(doc, null, writer, null);  
    writer.Close();  
  }  
}  
```  
  
## <a name="input"></a>입력  
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
  
 calc.xsl  
  
```xml  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
    xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
    xmlns:user="urn:my-scripts">  
  
  <msxsl:script language="C#" implements-prefix="user">  
     <![CDATA[  
     public double circumference(double radius)  
     {  
       double pi = 3.14;  
       double circ = pi*radius*2;  
       return circ;  
     }  
      ]]>  
   </msxsl:script>  
  
  <xsl:template match="data">    
  <circles>  
  
  <xsl:for-each select="circle">  
    <circle>  
    <xsl:copy-of select="node()"/>  
       <circumference>  
          <xsl:value-of select="user:circumference(radius)"/>   
       </circumference>  
    </circle>  
  </xsl:for-each>  
  </circles>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
## <a name="output"></a>출력  
  
```xml  
<circles xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:user="urn:my-scripts">  
  <circle>  
    <radius>12</radius>  
    <circumference>75.36</circumference>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
    <circumference>235.5</circumference>  
  </circle>  
</circles>    
```  
  
## <a name="see-also"></a>참고 항목

- [XslTransform 클래스의 XSLT 프로세서 구현](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)
