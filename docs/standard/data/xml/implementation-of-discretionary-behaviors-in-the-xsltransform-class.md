---
title: XslTransform 클래스에서 임의 동작 구현
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: d2758ea1-03f6-47bd-88d2-0fb7ccdb2fab
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d0a6b3faff0208634e711b9d7908e3fd8dc640ae
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170837"
---
# <a name="implementation-of-discretionary-behaviors-in-the-xsltransform-class"></a>XslTransform 클래스에서 임의 동작 구현

> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> 클래스는 .NET Framework 2.0에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](migrating-from-the-xsltransform-class.md)을 참조하세요.

임의 동작은 구현 공급자가 특정 상황을 처리하기 위해 선택할 수 있는 여러 가지 방법을 안내하는 [W3C(World Wide Web 컨소시엄) XSLT(XSL Transformations) 버전 1.0 권장 사항](https://www.w3.org/TR/1999/REC-xslt-19991116)에 나열된 동작으로 설명됩니다. 예를 들어, 7.3단원의 처리 명령 만들기에 나오는 W3C 권장 사항에 따르면 `xsl:processing-instruction`의 내용을 인스턴스화하여 텍스트 노드 이외의 노드가 만들어질 경우 오류가 발생합니다. W3C에서는 일부 문제점에 대해, 프로세서가 오류에서 복구하기로 결정한 경우 어떤 결정을 내려야 하는지 알려 줍니다. 7\.3단원에 제시된 문제점의 경우에는 W3C에서 노드 및 해당 내용을 무시함으로써 이 오류에서 구현을 복구할 수 있다고 설명합니다.

따라서 다음 표에서는 W3C에서 허용하는 각각의 임의 동작에 대해 <xref:System.Xml.Xsl.XslTransform> 클래스의 .NET Framework 구현을 수행하는 임의 동작과 W3C XSLT 1.0 권장 사항에서 해당 문제점에 대해 설명하는 단원의 목록을 보여 줍니다.

|문제점|동작|단원|
|-------------|--------------|-------------|
|`xsl:strip-space` 및 `xsl:preserve-space`가 모두 텍스트 노드와 일치합니다.|복구|3.4|
|소스 노드가 둘 이상의 템플릿 규칙과 일치합니다.|복구|5.5|
|네임스페이스 URI(Uniform Resource Identifier)가 가져오기 우선 순위가 모두 같은 여러 네임스페이스 URI에 대한 별칭이 되도록 선언됩니다.|복구|7.1.1|
|특성 값 템플릿에서 생성된 `xsl:attribute` 및 `xsl:element`의 이름 특성이 유효한 정규화된 이름(QName)이 아닙니다.|throw된 예외|7.1.2 및 7.1.3|
|자식 노드가 이미 요소 노드에 추가된 후에 요소에 특성을 추가합니다.|복구|7.1.3|
|요소 노드 이외의 노드에 특성을 추가합니다.|복구|7.1.3|
|`xsl:attribute` 요소의 내용이 인스턴스화된 것은 텍스트 노드가 아닙니다.|복구|7.1.3|
|두 특성 집합의 가져오기 우선 순위와 확장 이름이 같습니다. 모두 동일한 특성을 가지고 있으며, 중요도가 더 높은 동일한 이름의 공통 특성을 포함하는 다른 특성 집합이 업습니다.|복구|7.1.4|
|`xsl:processing-instruction` 이름 특성에서 NCName(no-colon name) 및 처리 명령 대상을 생성하지 않습니다.|복구|7.3|
|`xsl:processing-instruction`의 내용을 인스턴스화하면 텍스트 노드가 아닌 노드가 만들어집니다.|복구|7.3|
|`xsl:processing-instruction`의 내용을 인스턴스화한 결과에 "`?>`" 문자열이 있습니다.|복구|7.3|
|`xsl:comment`의 내용을 인스턴스화한 결과에 “--” 문자열이 있거나 결과가 “-”로 끝납니다.|복구|7.4|
|`xsl:comment`의 내용을 인스턴스화한 결과에 텍스트 노드가 아닌 노드가 만들어집니다.|복구|7.4|
|가변 바인딩 요소 내의 템플릿에서 특성 노드나 네임스페이스 노드를 반환합니다.|복구|11.2|
|문서 함수에 전달된 URI의 리소스를 검색하는 중에 오류가 발생합니다.|throw된 예외|12.1|
|문서 함수의 URI 참조에 조각 식별자가 있으며 해당 조각 식별자를 처리하는 중에 오류가 발생합니다.|throw된 예외|12.1|
|`cdata-section-elements`에 명명된 `xls:output`가 아닌 같은 이름의 여러 특성이 있고 이러한 특성의 가져오기 우선 순위가 동일합니다.|복구|16|
|프로세서에서 `encoding` 요소의 `xsl:output` 특성에 지정된 문자 인코딩 값을 지원하지 않습니다.|복구|16.1|
|`disable-output-escaping`이 텍스트 노드에 사용되며 해당 텍스트 노드를 사용하여 결과 트리에 텍스트 노드 이외의 노드를 만듭니다.|`disable-output-escaping` 특성은 무시됩니다.|16.4|
|결과 트리 조각에 출력 이스케이프를 사용하는 텍스트 노드가 있는 경우 결과 트리 조각을 숫자나 문자열로 변환합니다.|무시됨|16.4|
|XSLT 프로세서에서 출력에 사용하는 인코딩으로 나타낼 수 없는 문자에 출력 이스케이프를 사용할 수 없습니다.|무시됨|16.4|
|요소에 자식을 추가하거나 특성을 추가한 후에 네임스페이스 노드를 추가합니다.|복구|Errata e25|
|`xsl:number`가 NaN 또는 무한 값이거나 0.5 미만입니다.|복구|Errata e24|
|문서 함수에 대한 두 번째 인수 노드 집합이 비어 있고 URI 참조가 상대적입니다.|복구|Errata e14|

정오표의 섹션은 W3C [XSLT(XSL Transformations) Version 1.0 사양 정오표](https://www.w3.org/1999/11/REC-xslt-19991116-errata/)에서 확인할 수 있습니다.

## <a name="custom-defined-implementation-behaviors"></a>사용자 정의 구현 동작

<xref:System.Xml.Xsl.XslTransform> 클래스 구현에는 고유한 동작이 있습니다. 이 단원에서는 `xsl:sort`의 공급자별 구현과 <xref:System.Xml.Xsl.XslTransform> 클래스에서 지원하는 선택적 기능에 대해 설명합니다.

## <a name="xslsort"></a>xsl:sort

변환을 사용하여 정렬할 경우 W3C XSLT 1.0 권장 사항에서는 다음과 같은 몇 가지 준수 사항을 다음 창이 여기에 포함됩니다.

- 규칙을 준수하는 두 XSLT 프로세서가 서로 다르게 정렬할 수 있습니다.

- 모든 XSLT 프로세서가 같은 언어를 지원하는 것은 아닙니다.

- 언어를 고려하면, `xsl:sort.`에 지정되지 않은 특정 언어에 대한 정렬 순서가 프로세서에 따라 다를 수 있습니다.

다음 표에서는 <xref:System.Xml.Xsl.XslTransform>을 사용한 .NET Framework의 변환 구현에서 각 데이터 형식에 대해 구현된 정렬 동작을 보여 줍니다.

|데이터 형식|정렬 동작|
|---------------|----------------------|
|Text|CLR(공용 언어 런타임) String.Compare 메서드와 culture 로캘을 사용하여 데이터를 정렬합니다. 데이터 형식이 "텍스트"에 해당하면 <xref:System.Xml.Xsl.XslTransform> 클래스에서 정렬은 CLR의 문자열 비교 동작과 동일하게 작동합니다.|
|수|숫자 값은 XPath(XML Path Language) 번호로 간주되며 W3C [XPath(XML Path Language) Version 1.0 권장 사항, 섹션 3.5](https://www.w3.org/TR/1999/REC-xpath-19991116/#numbers)에 설명된 세부 정보에 따라 정렬됩니다.|

## <a name="optional-features-supported"></a>지원되는 선택적 기능

다음 표에서는 XSLT 프로세서에서 선택적으로 구현되며 <xref:System.Xml.Xsl.XslTransform> 클래스에서는 일괄 구현되는 기능을 보여 줍니다.

|기능|참조 위치|참고 사항|
|-------------|------------------------|-----------|
|`disable-output-escaping` 및 `<xsl:text...>` 태그의 `<xsl:value-of...>` 특성|W3C XSLT 1.0 권장 사항<br /><br /> 16.4단원|`disable-output-escaping` 또는 `xsl:text` 요소가 `xsl:value-of`, `xsl:comment` 또는 `xsl:processing-instruction` 요소에서 사용되면 `xsl:attribute` 특성이 무시됩니다.<br /><br /> 텍스트가 들어 있는 결과 트리 조각 및 이스케이프된 텍스트 출력은 지원되지 않습니다.<br /><br /> disable-output-escaping 특성은 <xref:System.Xml.XmlReader> 또는 <xref:System.Xml.XmlWriter> 개체로 변환할 때 무시됩니다.|

## <a name="see-also"></a>참고 항목

- <xref:System.Xml.Xsl.XslTransform>
- [XslTransform 클래스의 XSLT 프로세서 구현](xsltransform-class-implements-the-xslt-processor.md)
- [XslTransform 클래스를 사용하여 XSLT 변형](xslt-transformations-with-the-xsltransform-class.md)
- [변형 과정에서 XPathNavigator의 역할](xpathnavigator-in-transformations.md)
- [변형 과정에서 XPathNodeIterator의 역할](xpathnodeiterator-in-transformations.md)
- [XslTransform에 대한 XPathDocument 입력](xpathdocument-input-to-xsltransform.md)
- [XslTransform에 대한 XmlDataDocument 입력](xmldatadocument-input-to-xsltransform.md)
- [XslTransform에 대한 XmlDocument 입력](xmldocument-input-to-xsltransform.md)
