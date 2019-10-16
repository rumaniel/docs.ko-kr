---
title: XPathNavigator를 사용하여 노드 집합 탐색
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1a954b41-7173-40bc-8544-d430f209b1e5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 44b102cf160dcc4b3f188451d42d3b8dbefa5d1f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64590194"
---
# <a name="node-set-navigation-using-xpathnavigator"></a>XPathNavigator를 사용하여 노드 집합 탐색
<xref:System.Xml.XPath.XPathDocument> 클래스의 노드 집합 탐색 메서드를 사용하여 <xref:System.Xml.XmlDocument> 또는 <xref:System.Xml.XPath.XPathNavigator> 개체에서 노드를 탐색할 수 있습니다. 모든 노드를 탐색하거나 <xref:System.Xml.XPath.XPathNavigator> 클래스의 선택 메서드에서 하나가 반환한 노드 중 선택한 노드 집합을 탐색할 수 있습니다.  
  
## <a name="element-node-set-navigation"></a>요소 노드 집합 탐색  
 <xref:System.Xml.XPath.XPathNavigator> 클래스는 요소 노드를 탐색하는 여러 메서드를 제공합니다. 다음 표에서는 사용 가능한 탐색 메서드 및 이러한 메서드의 이동 방법에 대한 설명을 보여 줍니다. 여기에는 특성 및 네임스페이스 노드를 탐색하는 메서드가 포함되지 않습니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 개체에서 노드를 선택하는 방법에 대한 자세한 내용은 [XPathNavigator를 사용하여 XML 데이터 선택, 평가 및 일치시키기](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)를 참조하세요. 특성 및 네임스페이스 노드 탐색에 대한 자세한 내용은 [XPathNavigator를 사용하여 특성 및 네임스페이스 노드 탐색](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)을 참조하세요.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.XPath.XPathNavigator.MoveTo%2A>|지정된 <xref:System.Xml.XPath.XPathNavigator>와 동일한 위치로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToChild%2A>|현재 노드의 자식 노드로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A>|현재 노드의 첫 번째 형제 노드로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToFirstChild%2A>|현재 노드의 첫 번째 자식 노드로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToFollowing%2A>|문서 순서에서 지정된 요소로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToId%2A>|주어진 <xref:System.Xml.XPath.XPathNavigator>과 값이 일치하는 `ID` 형식의 특성을 갖춘 노드로 <xref:System.String>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A>|현재 노드의 다음 형제 노드로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToParent%2A>|현재 노드의 부모 노드로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A>|현재 노드의 이전 형제 노드로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToRoot%2A>|XML 문서의 루트 노드로 <xref:System.Xml.XPath.XPathNavigator>를 이동합니다.|  
  
## <a name="comments-and-processing-instruction-node-navigation"></a>주석 및 처리 명령 노드 탐색  
 다음 <xref:System.Xml.XPath.XPathNavigator> 클래스 메서드를 XML 문서의 다른 노드에서 주석 또는 처리 명령으로 이동할 수 있습니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveTo%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToFirstChild%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToChild%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToParent%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToId%2A>  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 특성 및 네임스페이스 노드 탐색](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 추출](../../../../docs/standard/data/xml/extract-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 강력한 형식의 XML 데이터 액세스](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)
