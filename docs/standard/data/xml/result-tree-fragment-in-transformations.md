---
title: 변형의 결과 트리 조각
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: df363480-ba02-4233-9ddf-8434e421c4f1
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e3b99606698124455ca9b325042ffbe430915aee
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170769"
---
# <a name="result-tree-fragment-in-transformations"></a>변형의 결과 트리 조각

> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> 클래스는 .NET Framework 2.0에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](migrating-from-the-xsltransform-class.md)을 참조하세요.

 결과 트리 조각이라고도 하는 노드 조각은 특수한 형식의 노드 집합과 크게 다르지 않습니다. 노드 집합에 대해 수행될 수 있는 함수는 노드 조각에 대해서도 수행될 수 있습니다. 또는 `node-set()` 함수를 사용하여 결과 트리 조각을 노드 집합으로 변환한 후 나중에 노드 집합을 사용할 수 있는 위치에서 변환된 해당 노드 집합을 사용할 수 있습니다.

 결과 트리 조각은 스타일시트에서 `<xsl:variable>` 또는 `<xsl:param>` 요소를 특정한 방식으로 사용하여 만들어집니다. `variable` 및 `parameter` 요소의 구문은 다음과 같습니다.

```xml
<xsl:param name=Qname select= XPath Expression >
    template body
</xsl:param>

<xsl:variable name=Qname select=XPath Expression >
    template body
</xsl:variable>
```

`parameter` 요소의 경우 해당 값이 여러 방법으로 정규화된 이름(`Qname`)에 할당됩니다. `select` 특성의 XPath(XML Path Language) 식에서 내용을 반환하거나 해당 매개 변수를 템플릿 본문의 내용에 지정하는 방법으로 매개 변수에 기본값을 지정할 수 있습니다.

`variable` 요소의 경우에도 해당 값이 여러 방법으로 지정됩니다. `select` 특성의 XPath 식에서 내용을 반환하거나 해당 값을 템플릿 본문의 내용에 지정하는 방법으로 값을 지정할 수 있습니다.

`parameter` 및 `variable` 요소의 경우, XPath 식에 값이 지정되면 네 가지 기본 XPath 형식 중 하나가 반환됩니다. 부울, 문자열, 숫자 또는 노드 집합. 비어 있지 않은 템플릿 본문을 사용하여 해당 값이 지정되면 XPath 이외의 데이터 형식이 반환된 후 결과 트리 조각이 됩니다.

변수가 이러한 네 가지 기본 XPath 데이터 형식에 속하지 않는 결과 트리 조각에 바인딩될 때가 바로 XPath 쿼리가 네 가지 XPath 개체 형식에 속하지 않는 형식을 반환하는 유일한 경우입니다. 결과 트리 조각 및 해당 동작은 [11.6단원 템플릿에 매개 변수 전달](https://www.w3.org/TR/xslt-10/#section-Passing-Parameters-to-Templates)을 통한 [W3C(World Wide Web 컨소시엄) 사양](https://www.w3.org/TR/xslt-10/), [11.1단원 결과 트리 조각](https://www.w3.org/TR/xslt-10/#section-Result-Tree-Fragments)에 설명되어 있습니다. 또한 [1단원의 소개](https://www.w3.org/TR/xslt-10/#section-Introduction)에서는 결과 트리 조각을 반환하거나 만드는 XSLT 네임스페이스에서 템플릿이 요소를 얻는 방법에 대해 설명합니다.

개념적으로 볼 때 결과 트리 조각은 단일 루트 노드만 있는 노드 집합과 동일하게 작동합니다. 그러나 반환된 노드의 나머지는 자식 노드에 해당합니다. 자식 노드를 프로그래밍 방식으로 나타내려면 `<xsl:copy-of>` 요소를 사용하여 결과 트리 조각을 결과 트리로 복사합니다. copy-of가 수행될 때 모든 자식 노드도 순서대로 결과 트리에 복사됩니다. `copy` 또는 `copy-of`가 사용될 때까지 결과 트리 조각은 결과 트리 또는 변형 결과에 속하지 않습니다.

결과 트리 조각의 반환된 노드를 검색하기 위해 <xref:System.Xml.XPath.XPathNavigator>가 사용됩니다. 다음 코드 샘플에서는 XML을 포함하는 매개 변수 `fragment`로 함수를 호출하여 스타일시트 내부에서 결과 트리 조각을 만드는 방법을 보여 줍니다.

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"
                xmlns:user="http://www.adventure-works.com"
                version="1.0">
    <xsl:var name="fragment">
        <node1>
            <node2/>
        </node1>
    <xsl:var>

  <msxsl:script language="C#" implements-prefix="user">
    function NodeFragment(XPathNavigator nav)
    {
      if (nav.HasSelection == false)
        XPathNavigator.MoveToNext();
      return;
    }
  </msxsl:script>

    <xsl:template match="/">
            <xsl:value-of select="user:NodeFragment(msxml:node-set($fragment))"/>
    </xsl:template>
</xsl:stylesheet>
```

다음은 RTF(서식 있는 텍스트), 즉 노드 집합으로 변환되지 않은 결과 트리 집합 형식으로 된 변수를 보여 주는 또 다른 예제입니다. 대신 이 변수는 스크립트 함수로 전달되며 <xref:System.Xml.XPath.XPathNavigator>를 사용하여 노드를 탐색합니다.

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"
        xmlns:user="urn:books"
        exclude-result-prefixes="msxsl">

<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>

<xsl:variable name="node-fragment">
    <book>Book1</book>
    <book>Book2</book>
    <book>Book3</book>
    <book>Book4</book>
</xsl:variable>

<msxsl:script implements-prefix="user" language="c#">

<![CDATA[
    string func(XPathNavigator nav)
    {
        bool b = nav.MoveToFirstChild();
        if (b)
            return nav.Value;
        else
            return "Does not exist";
    }

]]>

</msxsl:script>

<xsl:template match="/">
    <first_book>
        <xsl:value-of select="user:func($node-fragment)"/>
    </first_book>
</xsl:template>

</xsl:stylesheet>
```

다음 출력에서는 이 스타일시트를 사용하여 XML을 변환한 결과를 보여 줍니다.

## <a name="output"></a>Output

```xml
<first_book xmlns:user="urn:books">Book1</first_book>
```

위의 설명대로 `node-set` 함수를 사용하면 결과 트리 조각을 노드 집합으로 변환할 수 있습니다. 이렇게 만들어지는 노드는 항상 트리의 루트 노드인 단일 노드를 포함합니다. 결과 트리 조각을 노드 집합으로 변환하면 해당 노드 집합을 for-each 문이나 `select` 특성 값 등 일반 노드 집합의 어디에서든 사용할 수 있습니다. 다음 코드 줄에서는 노드 집합으로 변환되어 노드 집합으로 사용되는 조각을 보여 줍니다.

`<xsl:for-each select="msxsl:node-set($node-fragment)">`

`<xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>`

조각이 노드 집합으로 변환되면 더 이상 <xref:System.Xml.XPath.XPathNavigator>를 사용하여 노드 집합을 탐색할 수 없습니다. 노드 집합을 탐색하려면 <xref:System.Xml.XPath.XPathNodeIterator>를 사용해야 합니다.

다음 예제에서 `$var`는 스타일시트의 노드 트리인 변수입니다. for-each 문과 `node-set` 함수를 함께 사용하면 이러한 노드 트리를 노드 집합으로 검색할 수 있습니다.

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"
                xmlns:user="http://www.adventure-works.com"
                version="1.0">
    <xsl:variable name="states">
        <node1>AL</node1>
        <node1>CA</node1>
        <node1>CO</node1>
        <node1>WA</node1>
    </xsl:variable>

    <xsl:template match="/">
            <xsl:for-each select="msxsl:node-set($states)"/> 
    </xsl:template>
</xsl:stylesheet>
```

다음은 RTF, 즉 XPathNodeIterator로 스크립트 함수에 전달되기 전에 노드 집합으로 변환되는 결과 트리 조각 형식의 변수를 보여 주는 또 다른 예제입니다.

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"
        xmlns:user="urn:books"
        exclude-result-prefixes="msxsl">

<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>

<xsl:variable name="node-fragment">
    <book>Book1</book>
    <book>Book2</book>
    <book>Book3</book>
    <book>Book4</book>
</xsl:variable>

<msxsl:script implements-prefix="user" language="c#">

<![CDATA[
    string func(XPathNodeIterator it)
    {
        it.MoveNext(); 
        return it.Current.Value; 
        //it.Current returns XPathNavigator positioned on the current node
    }

]]>

</msxsl:script>
<xsl:template match="/">
    <books>
        <xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>
    </books>
</xsl:template>

</xsl:stylesheet>
```

다음은 이 스타일시트를 사용하여 XML을 변형한 결과입니다.

```xml
<books xmlns:user="urn:books">Book1Book2Book3Book4</books>
```

## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XPath.XPathNodeIterator>
- [XslTransform 클래스를 사용하여 XSLT 변형](xslt-transformations-with-the-xsltransform-class.md)
- [XslTransform 클래스의 XSLT 프로세서 구현](xsltransform-class-implements-the-xslt-processor.md)
