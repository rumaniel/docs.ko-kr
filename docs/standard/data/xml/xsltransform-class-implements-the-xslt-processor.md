---
title: XslTransform 클래스의 XSLT 프로세서 구현
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 88373fe2-4a6b-44f9-8a62-8a3e348e3a46
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8cc3eb3e3f147d8ed15587946af743c96739a9b1
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956860"
---
# <a name="xsltransform-class-implements-the-xslt-processor"></a>XslTransform 클래스의 XSLT 프로세서 구현

> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> 클래스는 .NET Framework 2.0에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)을 참조하세요.

<xref:System.Xml.Xsl.XslTransform> 클래스는 XSLT(XSL Transformations) 버전 1.0 권장 사항을 구현한 XSLT 프로세서입니다. <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드는 스타일시트를 찾아서 읽으며 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드는 지정된 소스 문서를 변환합니다. <xref:System.Xml.XPath.IXPathNavigable> 인터페이스를 구현하는 저장소를 <xref:System.Xml.Xsl.XslTransform>에 대한 소스 문서로 사용할 수 있습니다. .NET Framework는 현재 <xref:System.Xml.XmlDocument>, <xref:System.Xml.XmlDataDocument> 및 <xref:System.Xml.XPath.XPathDocument>에 대해 <xref:System.Xml.XPath.IXPathNavigable> 인터페이스를 구현하므로 이 모든 개체를 변환에 사용할 입력 소스 문서로 사용할 수 있습니다.

.NET Framework에서 <xref:System.Xml.Xsl.XslTransform> 개체는 다음 네임스페이스로 정의된 XSLT 1.0 사양만 지원합니다.

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
```

<xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드를 사용하여 다음 클래스 중 하나에서 스타일시트를 로드할 수 있습니다.

- XPathNavigator

- XmlReader

- URL을 나타내는 문자열

위의 각 입력 클래스마다 서로 다른 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드가 있습니다. 일부 메서드는 이러한 클래스 중 하나와 <xref:System.Xml.XmlResolver> 클래스를 인수로 사용합니다. <xref:System.Xml.XmlResolver>는 스타일시트에 있는 `<xsl:import>` 또는 `<xsl:include>`가 참조하는 리소스를 찾습니다. 다음 메서드는 문자열 <xref:System.Xml.XmlReader> 또는 <xref:System.Xml.XPath.XPathNavigator>를 입력으로 사용합니다.

```vb
Overloads Public Sub Load(String)
```

```csharp
public void Load(string);
```

```vb
Overloads Public Sub Load(String, XmlResolver)
```

```csharp
public void Load(string, XmlResolver);
```

```vb
Overloads Public Sub Load(XmlReader, XmlResolver, Evidence)
```

```csharp
public void Load(XmlReader, XmlResolver, Evidence);
```

```vb
Overloads Public Sub Load(XPathNavigator, XmlResolver, Evidence)
```

```csharp
public void Load(XPathNavigator, XmlResolver, Evidence);
```

위에 표시된 대부분의 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드는 <xref:System.Xml.XmlResolver>를 매개 변수로 사용합니다. <xref:System.Xml.XmlResolver>를 사용하여 해당 스타일시트와 xsl:import 및 xsl:include 요소에 참조되는 다른 스타일시트를 로드합니다.

대부분의 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드는 증명 정보도 매개 변수로 사용합니다. 증명 매개 변수는 스타일시트와 연관된 <xref:System.Security.Policy.Evidence>입니다. 스타일시트의 보안 수준은 스타일시트에 포함된 스크립트, 스타일시트가 사용하는 `document()` 함수 및 <xref:System.Xml.Xsl.XsltArgumentList>가 사용하는 확장명 개체 등 해당 스타일시트가 참조하는 모든 후속 리소스의 보안 수준에 영향을 줍니다.

URL 매개 변수를 포함하지만 증명 매개 변수는 포함하지 않는 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드를 사용하여 스타일시트를 로드하는 경우 지정된 URL과 해당 사이트 및 영역을 조합해서 스타일시트의 증명 정보를 계산합니다.

URI나 증명 정보가 모두 제공되지 않으면 스타일시트의 증명 정보 집합은 완전하게 신뢰됩니다. 신뢰되지 않는 소스에서 스타일시트를 로드하거나 신뢰되지 않는 확장명 개체를 <xref:System.Xml.Xsl.XsltArgumentList>에 추가하지 마세요.

보안 수준 및 증명 정보와 증명 정보가 스크립트에 미치는 영향에 대한 자세한 내용은 [\<msxsl:script>를 사용한 XSLT 스타일시트 스크립트](../../../../docs/standard/data/xml/xslt-stylesheet-scripting-using-msxsl-script.md)를 참조하세요. 보안 수준 및 증명 정보와 증명 정보가 확장 개체에 미치는 영향에 대한 자세한 내용은 [스타일시트 매개 변수 및 확장 개체의 XsltArgumentList](../../../../docs/standard/data/xml/xsltargumentlist-for-style-sheet-parameters-and-extension-objects.md)를 참조하세요.

보안 수준 및 증명 정보와 증명 정보가 `document()` 함수에 미치는 영향에 대한 자세한 내용은 [외부 XSLT 스타일시트 및 문서 확인](../../../../docs/standard/data/xml/resolving-external-xslt-style-sheets-and-documents.md)을 참조하세요.

스타일시트에 많은 입력 매개 변수가 제공될 수 있습니다. 또한 스타일시트는 확장 개체에 대해 함수를 호출할 수도 있습니다. 이러한 매개 변수와 확장명 개체는 모두 <xref:System.Xml.Xsl.XsltArgumentList> 클래스를 사용하여 스타일시트에 제공됩니다. <xref:System.Xml.Xsl.XsltArgumentList>에 대한 자세한 내용은 <xref:System.Xml.Xsl.XsltArgumentList>를 참조하십시오.

## <a name="recommended-secure-use-of-xsltransform-class"></a>XslTransform 클래스의 권장되는 보안 사용

스타일시트의 보안 권한은 제공되는 증명 정보에 따라 다릅니다. 다음 표에서는 스타일시트의 위치를 요약해서 설명하고 제공할 증명 정보 형식을 설명합니다.

- XSLT 스타일시트에 외부 참조가 없거나 스타일시트를 사용자가 신뢰하는 코드베이스에서 가져옵니다.

  - 어셈블리에서 증명 정보를 제공합니다.

    ```vb
    Dim xslt = New XslTransform() xslt.Load(stylesheet, resolver, Me.GetType().Assembly.Evidence)

    XsltTransform xslt = new XslTransform();  xslt.Load(stylesheet, resolver, this.GetType().Assembly.Evidence);
    ```

- XSLT 스타일시트를 외부 소스에서 가져옵니다. 소스의 출처를 알고 있으며 확인 가능한 URI가 있습니다.

  - URI를 사용하여 증명 정보를 만듭니다.

    ```vb
    Dim xslt As New XslTransform() Dim ev As Evidence = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri) xslt.Load(stylesheet, resolver, evidence)

    XslTransform xslt = new XslTransform(); Evidence ev = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri); xslt.Load(stylesheet, resolver, evidence);
    ```

- XSLT 스타일시트를 외부 소스에서 가져옵니다. 소스의 원본을 알 수 없습니다.

  - 증명 정보를 `null`로 설정합니다. 스크립트 블록이 처리되지 않고, XSLT `document()` 함수가 지원되지 않으며, 권한 있는 확장 개체는 사용할 수 없습니다.

    또한 `resolver` 매개 변수를 `null`로 설정할 수 있습니다. 이렇게 하면 `xsl:import` 및 `xsl:include` 요소가 처리되지 않습니다.

- XSLT 스타일시트를 외부 소스에서 가져옵니다. 소스의 원본을 알 수 없지만 스크립트 지원이 필요합니다.

  - 호출자의 증명 정보를 요청합니다.

## <a name="transformation-of-xml-data"></a>XML 데이터의 변형

스타일시트가 로드된 후에는 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드 중 하나를 호출하고 입력 소스 문서를 제공하여 변환을 시작합니다. <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드는 다양한 변환 출력을 제공하도록 오버로드됩니다. 변형의 출력 형식은 다음과 같습니다.

- <xref:System.Xml.XmlReader>

- <xref:System.Xml.XmlWriter>

- <xref:System.IO.TextWriter>

- <xref:System.IO.Stream>

- 파일의 문자열 URL

마지막 형식인 문자열 URL은 URL에 있는 입력 문서를 변형하여 출력 URL에 문서를 쓸 경우에 자주 사용됩니다. 이 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드는 파일에서 XML 문서를 로드하고 XSLT 변환을 수행하여 출력을 파일에 쓸 때 편리한 메서드입니다. 이 메서드를 사용하면 입력 소스 문서를 만들고 로드한 다음 파일 스트림에 쓸 필요가 없습니다. 다음 코드 예제에서는 문자열 URL을 입력 및 출력으로 사용하는 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드를 보여 줍니다.

```vb
Dim xsltransform As XslTransform = New XslTransform()
xsltransform.Load("favorite.xsl")
xsltransform.Transform("MyDocument.Xml", "TransformResult.xml", Nothing)
```

```csharp
XslTransform xsltransform = new XslTransform();
xsltransform.Load("favorite.xsl");
xsltransform.Transform("MyDocument.xml", "TransformResult.xml", null);
```

## <a name="transforming-a-section-of-an-xml-document"></a>XML 문서의 섹션 변형

변형은 문서 전체에 적용됩니다. 즉, 문서 루트 노드 이외의 노드에 전달해도 변환 프로세스에서 로드된 문서의 모든 노드에 액세스할 수 있습니다. 결과 트리 조각을 변환하려면 결과 트리 조각만 들어 있는 <xref:System.Xml.XmlDocument>를 만든 후 해당 <xref:System.Xml.XmlDocument>를 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드에 전달해야 합니다. 다음 예제에서는 결과 트리 조각에 대해 변환을 수행합니다.

```vb
Dim xslt As New XslTransform()
xslt.Load("print_root.xsl")
Dim doc As New XmlDocument()
doc.Load("library.xml")
' Create a new document containing just the result tree fragment.
Dim testNode As XmlNode = doc.DocumentElement.FirstChild
Dim tmpDoc As New XmlDocument()
tmpDoc.LoadXml(testNode.OuterXml)
' Pass the document containing the result tree fragment
' to the Transform method.
Console.WriteLine(("Passing " + tmpDoc.OuterXml + " to print_root.xsl"))
xslt.Transform(tmpDoc, Nothing, Console.Out, Nothing)
```

```csharp
XslTransform xslt = new XslTransform();
xslt.Load("print_root.xsl");
XmlDocument doc = new XmlDocument();
doc.Load("library.xml");
// Create a new document containing just the result tree fragment.
XmlNode testNode = doc.DocumentElement.FirstChild;
XmlDocument tmpDoc = new XmlDocument();
tmpDoc.LoadXml(testNode.OuterXml);
// Pass the document containing the result tree fragment
// to the Transform method.
Console.WriteLine("Passing " + tmpDoc.OuterXml + " to print_root.xsl");
xslt.Transform(tmpDoc, null, Console.Out, null);
```

이 예제에서는 라이브러리 .xml 및 print_root 파일을 입력으로 사용 하 고 다음을 콘솔에 출력 합니다.

```console
Passing <book genre="novel" ISBN="1-861001-57-5"><title>Pride And Prejudice</title></book> to print_root.xsl
Root node is book.
```

library.xml

```xml
<library>
  <book genre='novel' ISBN='1-861001-57-5'>
     <title>Pride And Prejudice</title>
  </book>
  <book genre='novel' ISBN='1-81920-21-2'>
     <title>Hook</title>
  </book>
</library>
```

print_root.xsl

```xml
<stylesheet version="1.0" xmlns="http://www.w3.org/1999/XSL/Transform" >
  <output method="text" />
  <template match="/">
     Root node is  <value-of select="local-name(//*[position() = 1])" />
  </template>
</stylesheet>
```

## <a name="migration-of-xslt-from-net-framework-version-10-to-net-framework-version-11"></a>.NET Framework 버전 1.0에서 .NET Framework 버전 1.1로 XSLT 마이그레이션

다음 표에서는 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드의 사용되지 않는 .NET Framework 버전 1.0 메서드와 새로운 .NET Framework 버전 1.1 메서드를 보여 줍니다. 새로운 메서드를 사용하면 증명 정보를 지정하여 스타일시트의 권한을 제한할 수 있습니다.

|더 이상 사용되지 않는 .NET Framework 버전 1.0 Load 메서드|대체 .NET Framework 버전 1.1 Load 메서드|
|------------------------------------------------------|---------------------------------------------------------|
|Load(XPathNavigator input);<br /><br /> Load(XPathNavigator input, XmlResolver resolver);|Load(XPathNavigator stylesheet, XmlResolver resolver, Evidence evidence);|
|Load(IXPathNavigable stylesheet);<br /><br /> Load(IXPathNavigable stylesheet, XmlResolver resolver);|Load(IXPathNavigable stylesheet, XmlResolver resolver, Evidence evidence);|
|Load(XmlReader stylesheet);<br /><br /> Load(XmlReader stylesheet, XmlResolver resolver);|Load(XmlReader stylesheet, XmlResolver resolver, Evidence evidence);|

다음 표에서는 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드의 사용되지 않는 메서드와 새로운 메서드를 보여 줍니다. 새로운 메서드는 <xref:System.Xml.XmlResolver> 개체를 사용합니다.

|더 이상 사용되지 않는 .NET Framework 버전 1.0 Transform 메서드|대체 .NET Framework 버전 1.1 Transform 메서드|
|-----------------------------------------------------------|--------------------------------------------------------------|
|XmlReader Transform(XPathNavigator input, XsltArgumentList args)|XmlReader Transform(XPathNavigator input, XsltArgumentList args, XmlResolver resolver)|
|XmlReader Transform(IXPathNavigable input, XsltArgumentList args)|XmlReader 변형(IXPathNavigable input, XsltArgumentList args, XmlResolver resolver)|
|Void 변형(XPathNavigator input, XsltArgumentList args, XmlWriter output)|Void 변형(XPathNavigator input, XsltArgumentList args, XmlWriter output, XmlResolver resolver)|
|Void 변형(IXPathNavigable input, XsltArgumentList args, XmlWriter output)|Void Transform(IXpathNavigable input, XsltArgumentList args, XmlWriter output, XmlResolver resolver)|
|Void 변형(XPathNavigator input, XsltArgumentList args, TextWriter output)|Void Transform(XPathNavigator input, XsltArgumentList args, TextWriter output, XmlResolver resolver)|
|Void Transform(IXPathNavigable input, XsltArgumentList args, TextWriter output)|Void 변형(IXPathNavigable input, XsltArgumentList args, TextWriter output, XmlResolver resolver)|
|Void Transform(XPathNavigator input, XsltArgumentList args, Stream output)|Void Transform(XPathNavigator input, XsltArgumentList args, Stream output, XmlResolver resolver)|
|Void 변형(IXPathNavigable input, XsltArgumentList args, Stream output)|Void Transform(IXPathNavigable input, XsltArgumentList args, Stream output, XmlResolver resolver)|
|Void Transform(String input, String output);|Void Transform(String input, String output, XmlResolver resolver);|

<xref:System.Xml.Xsl.XslTransform.XmlResolver%2A?displayProperty=nameWithType> 속성은 .NET Framework 버전 1.1에서 사용되지 않습니다. 대신 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 개체를 사용하는 새로운 <xref:System.Xml.XmlResolver> 오버로드를 사용합니다.

## <a name="see-also"></a>참조

- <xref:System.Xml.Xsl.XslTransform>
- [XslTransform 클래스를 사용하여 XSLT 변형](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)
- [변형 과정에서 XPathNavigator의 역할](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)
- [변형 과정에서 XPathNodeIterator의 역할](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)
- [XslTransform에 대한 XPathDocument 입력](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)
- [XslTransform에 대한 XmlDataDocument 입력](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)
- [XslTransform에 대한 XmlDocument 입력](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)
