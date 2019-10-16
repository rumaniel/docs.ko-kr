---
title: XslTransform 클래스에서 마이그레이션
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 9404d758-679f-4ffb-995d-3d07d817659e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2b0536607faa629e6113db0012056622d1adb541
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57674603"
---
# <a name="migrating-from-the-xsltransform-class"></a>XslTransform 클래스에서 마이그레이션

XSLT 아키텍처는 Visual Studio 2005 릴리스에서 다시 디자인되었습니다. <xref:System.Xml.Xsl.XslTransform> 클래스는 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스로 대체되었습니다.

다음 단원에서는 <xref:System.Xml.Xsl.XslCompiledTransform> 및 <xref:System.Xml.Xsl.XslTransform> 클래스 사이의 주요 차이점에 대해 설명합니다.

## <a name="performance"></a>성능

<xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 여러 가지로 성능이 향상되었습니다. CLR(공용 언어 런타임)이 다른 프로그래밍 언어에 대해 수행하는 것과 비슷하게 새 XSLT 프로세서는 XSLT 스타일시트를 공용 중간 형식으로 컴파일합니다. 스타일시트를 컴파일한 후 캐시하고 다시 사용할 수 있습니다.

또한 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 <xref:System.Xml.Xsl.XslTransform> 클래스보다 훨씬 빠르게 작동하도록 최적화되었습니다.

> [!NOTE]
> <xref:System.Xml.Xsl.XslCompiledTransform> 클래스의 전체적인 성능이 <xref:System.Xml.Xsl.XslTransform> 클래스보다 좋지만 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스의 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 메서드는 변환에 대해 처음 호출될 때 <xref:System.Xml.Xsl.XslTransform> 클래스의 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드보다 느리게 수행될 수 있습니다. 이는 XSLT 파일이 로드되기 전에 컴파일되어야 하기 때문입니다. 자세한 내용은 다음 블로그 게시물을 참조하세요. [XslCompiledTransform이 XslTransform보다 느리나요?](https://blogs.msdn.microsoft.com/antosha/2006/07/16/xslcompiledtransform-slower-than-xsltransform/)

## <a name="security"></a>보안

<xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 기본적으로 XSLT `document()` 함수 및 포함된 스크립팅에 대한 지원을 비활성화합니다. 이 기능을 활성화하는 <xref:System.Xml.Xsl.XsltSettings> 개체를 만들고 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 메서드에 전달하여 이러한 기능을 활성화할 수 있습니다. 다음 예제에서는 스크립팅을 활성화하고 XSLT 변환을 수행하는 방법을 보여 줍니다.

[!code-csharp[XML_Migration#16](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#16)]
[!code-vb[XML_Migration#16](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#16)]

자세한 내용은 [XSLT 보안 고려 사항](../../../../docs/standard/data/xml/xslt-security-considerations.md)을 참조하세요.

## <a name="new-features"></a>새 기능

### <a name="temporary-files"></a>임시 파일

XSLT를 처리하는 동안 임시 파일이 생성되는 경우가 있습니다. 스타일시트에 스크립트 블록이 포함되었거나 디버그 설정이 true로 설정된 상태에서 스타일시트가 컴파일된 경우 %TEMP% 폴더에 임시 파일이 만들어질 수 있습니다. 타이밍 문제로 인해 일부 임시 파일이 삭제되지 않을 때 이러한 경우가 생깁니다. 예를 들어 파일이 현재 AppDomain 또는 디버거에서 사용 중인 경우 <xref:System.CodeDom.Compiler.TempFileCollection> 개체의 종료자는 파일을 제거할 수 없습니다.

모든 임시 파일이 클라이언트에서 제거되도록 <xref:System.Xml.Xsl.XslCompiledTransform.TemporaryFiles%2A> 속성을 사용하여 추가 정리할 수도 있습니다.

### <a name="support-for-the-xsloutput-element-and-xmlwriter"></a>xsl:output 요소 및 XmlWriter 지원

변형 출력을 <xref:System.Xml.Xsl.XslTransform> 개체로 보낸 경우 `xsl:output` 클래스에서는 <xref:System.Xml.XmlWriter> 설정을 무시합니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 스타일시트의 <xref:System.Xml.Xsl.XslCompiledTransform.OutputSettings%2A> 요소에서 파생된 출력 정보가 있는 <xref:System.Xml.XmlWriterSettings> 개체를 반환하는 `xsl:output` 개체를 포함합니다. <xref:System.Xml.XmlWriterSettings> 개체를 사용하여 <xref:System.Xml.XmlWriter> 메서드로 전달될 수 있는 올바른 설정을 가진 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 개체를 만들 수 있습니다. 다음 C# 코드에서는 이 동작을 보여 줍니다.

```csharp
// Create the XslTransform object and load the style sheet.
XslCompiledTransform xslt = new XslCompiledTransform();
xslt.Load(stylesheet);

// Load the file to transform.
XPathDocument doc = new XPathDocument(filename);

// Create the writer.
XmlWriter writer = XmlWriter.Create(Console.Out, xslt.OutputSettings);

// Transform the file and send the output to the console.
xslt.Transform(doc, writer);
writer.Close();
```

### <a name="debug-option"></a>디버그 옵션

<xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 Microsoft Visual Studio Debugger에서 스타일시트를 디버그할 수 있는 디버그 정보를 생성합니다. 자세한 내용은 <xref:System.Xml.Xsl.XslCompiledTransform.%23ctor%28System.Boolean%29>를 참조하세요.

## <a name="behavioral-differences"></a>동작 차이점

### <a name="transforming-to-an-xmlreader"></a>XmlReader로 변환

<xref:System.Xml.Xsl.XslTransform> 클래스에는 변형 결과를 <xref:System.Xml.XmlReader> 개체로 반환하는 여러 변형 오버로드가 있습니다. 이러한 오버로드를 사용하여 결과 XML 트리의 serialization 및 deserialization 오버헤드 없이 변형 결과를 메모리 내 표현(예: <xref:System.Xml.XmlDocument> 또는 <xref:System.Xml.XPath.XPathDocument>)으로 로드할 수 있습니다. 다음 C# 코드에서는 변형 결과를 <xref:System.Xml.XmlDocument> 개체로 로드하는 방법을 보여 줍니다.

```csharp
// Load the style sheet
XslTransform xslt = new XslTransform();
xslt.Load("MyStylesheet.xsl");

// Transform input document to XmlDocument for additional processing
XmlDocument doc = new XmlDocument();
doc.Load(xslt.Transform(input, (XsltArgumentList)null));
```

<xref:System.Xml.Xsl.XslCompiledTransform> 클래스에서는 <xref:System.Xml.XmlReader> 개체로 변환하는 작업을 지원하지 않습니다. 그러나 <xref:System.Xml.XPath.XPathNavigator.CreateNavigator%2A>에서 직접 결과 XML 트리를 로드하기 위해 <xref:System.Xml.XmlWriter> 메서드를 사용하여 유사한 작업을 할 수 있습니다. 다음 C# 코드에서는 <xref:System.Xml.Xsl.XslCompiledTransform>을 사용하여 동일한 작업을 수행하는 방법을 보여 줍니다.

```csharp
// Transform input document to XmlDocument for additional processing
XmlDocument doc = new XmlDocument();
using (XmlWriter writer = doc.CreateNavigator().AppendChild()) {
    xslt.Transform(input, (XsltArgumentList)null, writer);
}
```

### <a name="discretionary-behavior"></a>임의 동작

W3C XSLT(XSL Transformations) 버전 1.0 권장 사항에는 구현 공급자가 특정 상황을 처리하는 방법을 결정할 수 있는 영역이 포함되어 있습니다. 이러한 영역은 임의 동작으로 간주됩니다. <xref:System.Xml.Xsl.XslCompiledTransform>이 <xref:System.Xml.Xsl.XslTransform> 클래스와 다르게 동작하는 여러 상황이 있습니다. 자세한 내용은 [복구 가능한 XSLT 오류](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)를 참조하세요.

### <a name="extension-objects-and-script-functions"></a>확장 개체 및 스크립트 함수

<xref:System.Xml.Xsl.XslCompiledTransform>에는 스크립트 함수 사용에 대한 새로운 두 가지 제한 사항이 추가되었습니다.

- 공용 메서드만 XPath 식에서 호출될 수 있습니다.

- 오버로드는 인수 수에 따라 서로 다르게 구분됩니다. 둘 이상의 오버로드에 동일한 수의 인수가 있는 경우 예외가 발생합니다.

<xref:System.Xml.Xsl.XslCompiledTransform>에서 함수를 스크립팅하는 바인딩(메서드 이름 lookup)은 컴파일 시간에 발생하므로 XslTransform에서 작동하는 스타일시트가 <xref:System.Xml.Xsl.XslCompiledTransform>에서 로드될 때 예외가 발생할 수 있습니다.

<xref:System.Xml.Xsl.XslCompiledTransform>에서는 `msxsl:using` 요소 내에 `msxsl:assembly` 및 `msxsl:script` 자식 요소를 가질 수 있습니다. `msxsl:using` 및 `msxsl:assembly` 요소를 사용하여 스크립트 블록에서 사용할 추가 네임스페이스 및 어셈블리를 선언합니다. 자세한 내용은 [msxsl:script를 사용하는 스크립트 블록](../../../../docs/standard/data/xml/script-blocks-using-msxsl-script.md)을 참조하세요.

<xref:System.Xml.Xsl.XslCompiledTransform>에서는 확장 개체가 동일한 수의 인수를 가지는 여러 개의 오버로드를 포함하지 못하도록 합니다.

### <a name="msxml-functions"></a>MSXML 함수

<xref:System.Xml.Xsl.XslCompiledTransform> 클래스에 추가된 추가 MSXML 함수를 지원합니다. 다음 목록에서는 새 기능 또는 향상된 기능을 설명합니다

- msxsl:node-set: <xref:System.Xml.Xsl.XslTransform>에서 [node-set 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256197(v=vs.100))의 인수는 결과 트리 조각이어야 합니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스에는 이러한 요구 사항이 없습니다.

- msxsl:version: 이 함수는 <xref:System.Xml.Xsl.XslCompiledTransform>에서 지원됩니다.

- XPath 확장 함수: [ms:string-compare 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256114(v=vs.100)), [ms:utc 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256474(v=vs.100)), [ms:namespace-uri 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256231(v=vs.100)), [ms:local-name 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256055(v=vs.100)), [ms:number 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256155(v=vs.100)), [ms:format-date 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256099(v=vs.100)) 및 [ms:format-time 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256467(v=vs.100))가 이제 지원됩니다.

- 스키마 관련 XPath 확장 함수: 이러한 함수는 기본적으로 <xref:System.Xml.Xsl.XslCompiledTransform>에서 지원되지 않습니다. 그러나 이러한 함수를 확장명 함수로 구현할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)
- [XslCompiledTransform 클래스 사용](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)
