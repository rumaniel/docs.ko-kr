---
title: 복구할 수 있는 XSLT 오류
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 484929b0-fefb-4629-87ee-ebdde70ff1f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 215fb807aa27b8a544351d26fd0c9500c76b6ead
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50202987"
---
# <a name="recoverable-xslt-errors"></a>복구할 수 있는 XSLT 오류
W3C XSLT(XSL Transformations) 버전 1.0 권장 사항에는 구현 공급자가 특정 상황을 처리하는 방법을 결정할 수 있는 영역이 포함되어 있습니다. 이러한 영역은 임의 동작으로 간주됩니다. 예를 들어, 7.3단원의 처리 명령 만들기에 나오는 XSLT 1.0 권장 사항에 따르면 `xsl:processing-instruction`의 내용을 인스턴스화하여 텍스트 노드 이외의 노드가 만들어질 경우 오류가 발생합니다. XSLT 1.0 권장 사항에서는 일부 문제점에 대해 프로세서가 오류로부터 복구하기로 결정한 경우 어떤 결정을 내려야 하는지 알려 줍니다. 7.3단원에 제시된 문제점의 경우에는 W3C에서 노드 및 해당 내용을 무시함으로써 이 오류에서 구현을 복구할 수 있다고 설명합니다.  
  
## <a name="discretionary-behaviors"></a>임의 동작  
 다음 표에서는 XSLT 1.0 권장 사항에서 허용하는 임의 동작 및 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 임의 동작을 처리하는 방법을 보여 줍니다.  
  
-   복구는 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스가 이 오류로부터 복구하는 것을 나타냅니다. <xref:System.Xml.Xsl.XsltArgumentList.XsltMessageEncountered?displayProperty=nameWithType> 이벤트를 사용하여 XSLT 프로세서의 모든 이벤트를 보고할 수 있습니다.  
  
-   오류는 이 조건에 대해 예외가 발생함을 나타냅니다.  
  
-   [W3C XSLT(XSL 변환) 버전 1.0 권장 사항](https://www.w3.org/TR/xslt) 및 [W3C XSLT(XSL 변환) 버전 1.0 Specification Errata](https://www.w3.org/1999/11/REC-xslt-19991116-errata/)에서 섹션 참조를 찾을 수 있습니다.  
  
|XSLT 조건|단원|XslCompiledTransform 동작|  
|--------------------|-------------|-----------------------------------|  
|`xsl:strip-space` 및 `xsl:preserve-space`가 모두 텍스트 노드와 일치합니다.|3.4|복구|  
|소스 노드가 둘 이상의 템플릿 규칙과 일치합니다.|5.5|복구|  
|네임스페이스 URI가 가져오기 우선 순위가 모두 같은 여러 네임스페이스 URI에 대한 별칭이 되도록 선언됩니다.|7.1.1|복구|  
|특성 값에서 생성된 `name` 및 `xsl:attribute`의 `xsl:element` 특성은 QName이 아닙니다.|7.1.2, 7.1.3|오류*|  
|가져오기 및 확장명 이름이 같은 두 특성 집합에는 공통적인 특성이 하나 있으며 중요도가 더 높고 동일한 이름의 공통 특성을 포함하는 다른 특성 집합은 없습니다.|7.1.4|복구|  
|요소에 자식을 추가한 후 특성을 추가합니다.|7.1.3|오류*|  
|이름이 'xmlns'인 특성을 만듭니다.|7.1.3|오류*|  
|요소가 아닌 노드에 특성을 추가합니다.|7.1.3|오류*|  
|`xsl:attribute` 특성의 내용을 인스턴스화하는 동안 텍스트 노드 이외의 노드를 만듭니다.|7.1.3|오류*|  
|`name`의 `xsl:processing-instruction` 특성은 NCName과 처리 명령 대상을 둘 다 생성하지 않습니다.|7.3|오류*|  
|`xsl:processing-instruction`의 내용을 인스턴스화하면 텍스트 노드가 아닌 노드가 만들어집니다.|7.3|오류*|  
|`xsl:processing-instruction`의 내용을 인스턴스화한 결과에 "?>" 문자열이 있습니다.|7.3|복구|  
|`xsl:processing-instruction`의 내용을 인스턴스화한 결과에 "--" 문자열이 있거나 결과가 "-"로 끝납니다.|7.4|복구|  
|`xsl:comment`의 내용을 인스턴스화한 결과에 텍스트 노드가 아닌 노드가 만들어집니다.|7.4|오류*|  
|가변 바인딩 요소 내의 템플릿에서 특성 노드나 네임스페이스 노드를 반환합니다.|11.2|오류*|  
|문서 함수에 전달된 URI의 리소스를 검색하는 중에 오류가 발생합니다.|12.1|Error|  
|문서 함수의 URI 참조에 조각 식별자가 있으며 해당 조각 식별자를 처리하는 중에 오류가 발생합니다.|12.1|복구*|  
|가져오기 우선 순위가 같은 `xsl:output`에는 이름이 같지만 값이 다르며 명명된 cdata-section 요소가 아닌 여러 특성이 있습니다.|16|복구|  
|프로세서는 `xsl:output` 인코딩 특성에서 인코딩을 지원하지 않습니다.|16.1|복구|  
|결과 트리에서 텍스트 노드가 아닌 노드에 사용되는 텍스트 노드의 출력 이스케이프를 비활성화합니다.|16.4|복구*|  
|결과 트리 조각에 출력 이스케이프를 사용하는 텍스트 노드가 있는 경우 결과 트리 조각을 숫자나 문자열로 변환합니다.|16.4|복구*|  
|XSLT 프로세서에서 출력에 사용하는 인코딩으로 나타낼 수 없는 문자에 출력 이스케이프를 사용할 수 없습니다.|16.4|복구*|  
|요소에 자식을 추가하거나 특성을 추가한 후에 네임스페이스 노드를 추가합니다.|errata 25|오류*|  
|`value`의 `xsl:number` 특성이 NAN 또는 무한 값이거나 0.5 미만입니다.|errata 24|복구|  
|문서 함수에 대한 두 번째 인수 노드 집합이 비어 있고 URI 참조가 상대적입니다.|errata 14|복구|  
  
 <sup>*</sup> 이 동작은 <xref:System.Xml.Xsl.XslTransform> 클래스의 동작과 다릅니다. 자세한 내용은 [XslTransform 클래스에서 임의 동작 구현](../../../../docs/standard/data/xml/implementation-of-discretionary-behaviors-in-the-xsltransform-class.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)
