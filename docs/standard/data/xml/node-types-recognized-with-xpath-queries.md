---
title: XPath 쿼리에서 인식하는 노드 형식
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1d33e22d-18e5-43f8-a466-2e3d0a8dd094
author: mairaw
ms.author: mairaw
ms.openlocfilehash: aa004f0def04c7efe2ba7450050a899760b0bbcd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64590197"
---
# <a name="node-types-recognized-with-xpath-queries"></a>XPath 쿼리에서 인식하는 노드 형식
XPath 쿼리에서 인식하는 노드 형식은 DOM(문서 개체 모델)에 있는 노드 형식과 다릅니다.  
  
## <a name="w3c-xpath-node-types"></a>W3C XPath 노드 형식  
 XPath 쿼리에서 인식하는 노드 형식은 DOM(문서 개체 모델)에 있는 노드 형식이 아닙니다. 다음은 <xref:System.Xml.XPath.XPathNodeType> 열거형이 나타내는 XPath 노드 형식입니다.  
  
- <xref:System.Xml.XPath.XPathNodeType.All>  
  
- <xref:System.Xml.XPath.XPathNodeType.Attribute>  
  
- <xref:System.Xml.XPath.XPathNodeType.Comment>  
  
- <xref:System.Xml.XPath.XPathNodeType.Element>  
  
- <xref:System.Xml.XPath.XPathNodeType.Namespace>  
  
- <xref:System.Xml.XPath.XPathNodeType.ProcessingInstruction>  
  
- <xref:System.Xml.XPath.XPathNodeType.Root>  
  
- <xref:System.Xml.XPath.XPathNodeType.SignificantWhitespace>  
  
- <xref:System.Xml.XPath.XPathNodeType.Text>  
  
- <xref:System.Xml.XPath.XPathNodeType.Whitespace>  
  
 이 노드 형식은 XML 정보 집합에서 노드가 파생되는 XPath 데이터 모델을 기반으로 합니다. <xref:System.Xml.XPath.XPathNodeType.SignificantWhitespace> 및 <xref:System.Xml.XPath.XPathNodeType.Whitespace> 노드 형식은 XPath 데이터 모델에서 설명하는 기본 노드 형식에 대한 Microsoft .NET Framework 확장입니다.  
  
 XPath 데이터 모델에서는 DOM에서와 다른 방식으로 특성 노드 형식을 사용합니다. XPath 데이터 모델에서 요소 노드는 관련된 특성 노드 집합을 가지고 있으며 요소 노드는 각 특성 노드의 부모입니다. 그러나 DOM에서 요소 노드는 부모가 아니라 소유자입니다. 두 모델에서 특성 및 네임스페이스 노드는 요소 노드의 자식 노드로 간주되지 않습니다.  
  
 네임스페이스 노드 형식은 XPath 데이터 모델에 추가된 것이며 인식되는 DOM 노드 형식이 아닙니다.  
  
 요소, 특성 및 네임스페이스 노드 탐색에 대한 자세한 내용은 [XPathNavigator를 사용하여 노드 집합 탐색](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md) 및 [XPathNavigator를 사용하여 특성 및 네임스페이스 노드 탐색](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md) 항목을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XML 데이터 선택](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XPath 식 계산](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 노드 일치시키기](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)
- [XPath 쿼리 및 네임스페이스](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)
- [컴파일된 XPath 식](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
