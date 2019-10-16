---
title: 변환 과정에서 노드 집합의 역할
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: ad034f0e-ff8b-4a71-9a4c-528c754263c4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fbcd9b93f63d48229c174b0f6518fd0150e98e18
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957025"
---
# <a name="node-sets-in-transformations"></a>변환 과정에서 노드 집합의 역할
노드 집합은 XPath(XML Path Language) 식에서 반환된 네 가지 기본 데이터 형식 중 하나입니다. 문서 순서로 만들어진 중복되지 않은 노드의 정렬되지 않은 컬렉션에 해당하는 노드 집합은 스타일시트의 변수에 할당될 수 있습니다.  
  
> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> 클래스는 .NET Framework 2.0에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)을 참조하세요.  
  
 노드 집합은 XPath 식에서 반환된 네 가지 기본 데이터 형식 중 하나입니다. 문서 순서로 만들어진 중복되지 않은 노드의 정렬되지 않은 컬렉션에 해당하는 노드 집합은 스타일시트의 변수에 할당될 수 있습니다. 변환에서 `select` 특성에 사용된 XPath 식의 결과로 만들어진 이 노드 집합은 XML DOM(문서 개체 모델)의 노드 집합과 동일한 동작을 수행합니다. 탐색에 <xref:System.Xml.XPath.XPathNodeIterator>를 사용하는 결과 트리 조각과는 달리 [XPathNavigator를 사용하여 노드 집합 탐색](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)에 표시된 메서드 집합을 사용하여 노드 집합을 탐색할 수 있습니다.  
  
 다음 코드 샘플에서는 스타일시트의 `variable` 또는 `parameter` 요소가 노드 집합으로 평가될 때 노드 집합을 검색하는 방법을 보여 줍니다.  
  
## <a name="style-sheet"></a>스타일시트  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">  
  
    <xsl:variable name="x" select="bookstore/book/title"></xsl:variable>  
  
    <xsl:template match="/">  
        <xsl:for-each select="$x">  
            ******  
            <xsl:value-of select="."></xsl:value-of>  
            ******  
        </xsl:for-each>  
    </xsl:template>  
  
</xsl:stylesheet>  
```  
  
## <a name="input"></a>입력  
  
```xml  
<bookstore>  
   <book style="autobiography">  
      <title>Seven Years in Trenton</title>  
   </book>  
  
   <book style="autobiography">  
      <title>Seven Years in Trenton2</title>  
   </book>  
  
   <book style="textbook">  
      <title>History of Trenton Vol 3</title>  
   </book>  
</bookstore>  
```  
  
## <a name="output"></a>출력  
  
```output  
******  
Seven Years in Trenton  
******  
  
******  
Seven Years in Trenton2  
******  
  
******  
History of Trenton Vol 3  
******  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Xml.XPath.XPathNodeIterator>
- [XslTransform 클래스를 사용하여 XSLT 변형](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)
- [XslTransform 클래스의 XSLT 프로세서 구현](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)
