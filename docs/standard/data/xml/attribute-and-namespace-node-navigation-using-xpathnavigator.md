---
title: XPathNavigator를 사용하여 특성 및 네임스페이스 노드 탐색
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 23975f88-e0af-4b88-93de-9e20e11880ad
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4188896fb36d8535f86b245c3b1942f5a058da9b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69936827"
---
# <a name="attribute-and-namespace-node-navigation-using-xpathnavigator"></a>XPathNavigator를 사용하여 특성 및 네임스페이스 노드 탐색
<xref:System.Xml.XPath.XPathNavigator> 클래스는 두 개의 탐색 메서드 집합을 제공합니다. [XPathNavigator를 사용하여 노드 집합 탐색](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md) 항목에서 찾을 수 있는 첫 번째 집합은 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체의 ‘노드 집합’을 탐색하는 데 사용합니다.  이 항목에서 설명하는 두 번째 집합은 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체의 ‘특성 및 네임스페이스 노드’를 탐색하는 데 사용합니다.   
  
## <a name="attribute-node-navigation"></a>특성 노드 탐색  
 특성은 요소의 자식이 아니라 요소의 속성입니다. 이러한 구분은 형제, 부모 및 자식 노드를 탐색하는 데 사용되는 <xref:System.Xml.XPath.XPathNavigator> 클래스의 메서드로 인해 중요하게 작용합니다.  
  
 예를 들어, <xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A> 및 <xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A> 메서드는 요소와 특성 사이 또는 특성 간을 탐색하는 데 사용되지 않습니다. 대신 특성에는 구분되는 탐색 메서드가 있습니다.  
  
 다음은 <xref:System.Xml.XPath.XPathNavigator> 클래스의 특성 탐색 메서드입니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToAttribute%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToFirstAttribute%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToNextAttribute%2A>  
  
 현재 노드가 요소이면 <xref:System.Xml.XPath.XPathNavigator.HasAttributes%2A> 속성을 사용하여 해당 요소와 연관된 특성이 있는지 확인할 수 있습니다. 요소에 특성이 있다고 확인되면 특성에 액세스하기 위한 여러 메서드가 있는 것입니다. 요소에서 단일 특성을 검색하려면 <xref:System.Xml.XPath.XPathNavigator.GetAttribute%2A> 메서드를 사용합니다. <xref:System.Xml.XPath.XPathNavigator>를 특정 특성으로 이동하려면 <xref:System.Xml.XPath.XPathNavigator.MoveToAttribute%2A> 메서드를 사용합니다. <xref:System.Xml.XPath.XPathNavigator.MoveToFirstAttribute%2A> 메서드를 사용하고 그 다음에 <xref:System.Xml.XPath.XPathNavigator.MoveToNextAttribute%2A> 메서드를 여러 번 호출하면 요소의 각 특성을 반복할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Xml.XPath.XPathNavigator> 개체가 특성 또는 네임스페이스 노드에 위치하면 <xref:System.Xml.XPath.XPathNavigator.MoveToChild%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToFirstChild%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToFollowing%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToId%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A> 및 <xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A> 메서드는 항상 `false`를 반환하고 <xref:System.Xml.XPath.XPathNavigator>의 위치에는 영향을 주지 않습니다. 예외에는 <xref:System.Xml.XPath.XPathNavigator.MoveTo%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToParent%2A> 및 <xref:System.Xml.XPath.XPathNavigator.MoveToRoot%2A>메서드가 있습니다.  
  
## <a name="namespace-node-navigation"></a>네임스페이스 노드 탐색  
 각 요소에는 네임스페이스 노드 집합이 연결되어 있으며 하나는 요소의 범위에 있는 네임스페이스 URI(모든 XML 문서에서 암시적으로 선언된 `http://www.w3.org/XML/1998/namespace` 네임스페이스에 바인딩된 XML 접두사 포함)에 바인딩된 각 네임스페이스 접두사에 대한 노드 집합이고 하나는 요소의 범위 내에 있을 경우 기본 네임스페이스에 대한 노드 집합입니다. 요소는 이러한 네임스페이스 노드 각각의 부모이지만 네임스페이스 노드는 해당 부모 요소의 자식이 아닙니다.  
  
 특성과 마찬가지로 <xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A> 및 <xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A> 메서드는 요소와 네임스페이스 노드 또는 네임스페이스 노드 간을 탐색하는 데 사용되지 않습니다. 대신 네임스페이스 노드에는 구분되는 탐색 메서드가 있습니다.  
  
 다음은 <xref:System.Xml.XPath.XPathNavigator> 클래스의 네임스페이스 탐색 메서드입니다.  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToNamespace%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.MoveToNextNamespace%2A>  
  
 XML 문서의 요소 범위 내에는 항상 네임스페이스 노드가 한 개 이상 있습니다. 이 네임스페이스 노드에는 접두사 `xml`과 네임스페이스 URI `http://www.w3.org/XML/1998/namespace`가 있습니다. 특정 접두사가 지정된 범위 내에서 네임스페이스 URI를 검색하려면 <xref:System.Xml.XPath.XPathNavigator.GetNamespace%2A> 메서드를 사용합니다. <xref:System.Xml.XPath.XPathNavigator> 개체를 특정 네임스페이스 노드로 이동하려면 <xref:System.Xml.XPath.XPathNavigator.MoveToNamespace%2A> 메서드를 사용합니다. <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A> 메서드를 사용하고 그 다음에 <xref:System.Xml.XPath.XPathNavigator.MoveToNextNamespace%2A> 메서드를 여러 번 호출하면 요소의 범위 내에서 각 네임스페이스 노드를 반복할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Xml.XPath.XPathNavigator> 개체가 특성 또는 네임스페이스 노드에 위치하면 <xref:System.Xml.XPath.XPathNavigator.MoveToChild%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToFirstChild%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToFollowing%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToId%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A> 및 <xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A> 메서드는 항상 `false`를 반환하고 <xref:System.Xml.XPath.XPathNavigator>의 위치에는 영향을 주지 않습니다. 예외에는 <xref:System.Xml.XPath.XPathNavigator.MoveTo%2A>, <xref:System.Xml.XPath.XPathNavigator.MoveToParent%2A> 및 <xref:System.Xml.XPath.XPathNavigator.MoveToRoot%2A>메서드가 있습니다.  
  
### <a name="the-xpathnamespacescope-enumeration"></a>XPathNamespaceScope 열거형  
 네임스페이스 노드를 탐색할 때 <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A> 매개 변수를 사용하여 <xref:System.Xml.XPath.XPathNavigator.MoveToNextNamespace%2A> 및 <xref:System.Xml.XPath.XPathNamespaceScope> 메서드를 호출할 수 있습니다. 이러한 메서드는 매개 변수 없이 호출되는 메서드와 다르게 동작합니다. <xref:System.Xml.XPath.XPathNamespaceScope> 열거형에는 <xref:System.Xml.XPath.XPathNamespaceScope.All>, <xref:System.Xml.XPath.XPathNamespaceScope.ExcludeXml> 또는 <xref:System.Xml.XPath.XPathNamespaceScope.Local> 값이 있습니다.  
  
 다음 예제에서는 XML 문서의 다양한 범위에서 <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A> 및 <xref:System.Xml.XPath.XPathNavigator.MoveToNextNamespace%2A> 메서드가 반환하는 네임스페이스를 보여 줍니다.  
  
```xml  
<root>  
    <element1 xmlns="http://www.contoso.com" xmlns:books="http://www.contoso.com/books">  
        <element2 />  
    </element1>  
</root>  
```  
  
 네임스페이스 시퀀스(<xref:System.Xml.XPath.XPathNavigator> 메서드를 호출하고 <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A> 메서드를 여러 번 호출한 후 <xref:System.Xml.XPath.XPathNavigator.MoveToNextNamespace%2A>가 배치되는 네임스페이스)는 다음과 같습니다.  
  
- `element2`에 위치하는 경우: `xmlns:books="http://www.contoso.com/books"`, `xmlns="http://www.contoso.com"` 및 `xmlns:xml="http://www.w3.org/XML/1998/namespace"`  
  
- `element1`에 위치하는 경우: `xmlns:books="http://www.contoso.com/books"`, `xmlns="http://www.contoso.com"` 및 `xmlns:xml="http://www.w3.org/XML/1998/namespace"`  
  
- `root`에 위치하는 경우: `xmlns:xml="http://www.w3.org/XML/1998/namespace".`  
  
> [!NOTE]
> <xref:System.Xml.XPath.XPathNavigator> 클래스는 네임스페이스 노드를 문서 순서와 역순으로 반환합니다. 따라서 <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A>는 기본적으로 현재 범위의 마지막 네임스페이스 노드로 이동합니다.  
  
 다음 예제에서는 XML 문서의 다양한 범위에서 <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A> 열거형을 지정한 경우 <xref:System.Xml.XPath.XPathNavigator.MoveToNextNamespace%2A> 및 <xref:System.Xml.XPath.XPathNamespaceScope> 메서드가 반환하는 네임스페이스를 보여 줍니다.  
  
```xml  
<root xmlns="http://www.contoso.com" xmlns:a="http://www.contoso.com/a" xmlns:b="http://www.contoso.com/b">  
    <child1 xmlns="" xmlns:a="urn:a">  
        <child2 xmlns:c="urn:c" />  
    </child1>  
</root>  
```  
  
 `child2`에 배치된 경우 네임스페이스 시퀀스(<xref:System.Xml.XPath.XPathNavigator> 메서드를 호출하고 <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A> 메서드를 여러 번 호출한 후 <xref:System.Xml.XPath.XPathNavigator.MoveToNextNamespace%2A>가 배치되는 네임스페이스)는 다음과 같습니다.  
  
- <xref:System.Xml.XPath.XPathNamespaceScope.All>: `xmlns:c="urn:c"`, `xmlns:a="urn:a"`, `xmlns=""`, `xmlns:b="http://www.contoso.com/b"`, `xmlns:a="http://www.contoso.com/a"`, `xmlns="http://www.contoso.com"` 및 `xmlns:xml="http://www.w3.org/XML/1998/namespace"`  
  
- <xref:System.Xml.XPath.XPathNamespaceScope.ExcludeXml>: `xmlns:c="urn:c"`, `xmlns:a="urn:a"`, `xmlns=""`, `xmlns:b="http://www.contoso.com/b"`, `xmlns:a="http://www.contoso.com/a"` 및 `xmlns="http://www.contoso.com"`  
  
- <xref:System.Xml.XPath.XPathNamespaceScope.Local>: `xmlns:c="urn:c"`입니다.  
  
> [!NOTE]
> <xref:System.Xml.XPath.XPathNavigator> 클래스는 네임스페이스 노드를 문서 순서와 역순으로 반환합니다. 따라서 <xref:System.Xml.XPath.XPathNavigator.MoveToFirstNamespace%2A>는 기본적으로 현재 범위의 마지막 네임스페이스 노드로 이동합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 노드 집합 탐색](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 추출](../../../../docs/standard/data/xml/extract-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 강력한 형식의 XML 데이터 액세스](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)
