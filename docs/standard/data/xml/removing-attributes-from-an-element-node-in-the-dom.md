---
title: DOM의 요소 노드에서 특성 제거
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 7ede6f9e-a3ac-49a4-8488-ab8360a44aa4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 65fd6d2baae29c72241350e4568faf09b9c71f39
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48835183"
---
# <a name="removing-attributes-from-an-element-node-in-the-dom"></a>DOM의 요소 노드에서 특성 제거
여러 가지 방법으로 특성을 제거할 수 있습니다. 그 중 한 가지 방법은 특성 컬렉션에서 특성을 제거하는 것입니다. 이 방법을 사용하려면 다음 단계를 수행합니다.  
  
1.  `XmlAttributeCollection attrs = elem.Attributes;`를 사용하여 요소에서 특성 컬렉션을 가져옵니다.  
  
2.  다음 세 가지 메서드 중 하나를 사용하여 특성 컬렉션에서 특성을 제거합니다.  
  
    -   특정 특성을 제거하려면 <xref:System.Xml.XmlAttributeCollection.Remove%2A>를 사용합니다.  
  
    -   컬렉션에서 모든 특성을 제거하고 특성이 없는 요소는 남겨 두려면 <xref:System.Xml.XmlAttributeCollection.RemoveAll%2A>을 사용합니다.  
  
    -   인덱스 번호를 사용하여 특성 컬렉션에서 특성을 제거하려면 <xref:System.Xml.XmlAttributeCollection.RemoveAt%2A>을 사용합니다.  
  
 다음 메서드는 요소 노드에서 특성을 제거합니다.  
  
-   특성 컬렉션을 제거하려면 <xref:System.Xml.XmlElement.RemoveAllAttributes%2A>를 사용합니다.  
  
-   컬렉션에서 이름으로 특성 하나를 제거하려면 <xref:System.Xml.XmlElement.RemoveAttribute%2A>를 사용합니다.  
  
-   컬렉션에서 인덱스 번호로 특성 하나를 제거하려면 <xref:System.Xml.XmlElement.RemoveAttributeAt%2A>을 사용합니다.  
  
 또 다른 방법은 요소를 가져오고 특성 컬렉션에서 특성을 가져온 다음 특성 노드를 직접 제거하는 것입니다. 특성 컬렉션에서 특성을 가져오려면 이름, `XmlAttribute attr = attrs["attr_name"];`, 인덱스 `XmlAttribute attr = attrs[0];`를 사용하거나 네임스페이스 `XmlAttribute attr = attrs["attr_localName", "attr_namespace"]`로 이름을 정규화합니다.  
  
 특성을 제거하는 데 사용한 메서드와 상관없이 DTD(문서 종류 정의)에 기본 특성으로 정의된 특성을 제거할 때는 특별한 제한 사항이 있습니다. 기본 특성이 속해 있는 요소를 제거해야 기본 특성을 제거할 수 있습니다. 기본 특성은 기본 특성을 선언한 요소에 대해 항상 존재합니다. <xref:System.Xml.XmlAttributeCollection> 또는 <xref:System.Xml.XmlElement>에서 기본 특성을 제거하면 대체 특성이 요소의 <xref:System.Xml.XmlAttributeCollection>에 삽입되고 선언된 기본값으로 초기화됩니다. `<book att1="1" att2="2" att3="3"></book>`으로 정의된 요소가 있을 경우 기본 특성 3개가 선언된 `book` 요소가 있습니다. XML DOM(문서 개체 모델)을 구현하면 이 `book` 요소가 있는 한, 기본 특성 `att1`, `att2` 및 `att3`이 있습니다.  
  
 <xref:System.Xml.XmlAttribute>를 사용하여 <xref:System.Xml.XmlAttributeCollection.RemoveAll%2A> 메서드를 호출하면 값이 없는 특성이 있을 수 없으므로 특성 값이 String.Empty로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
