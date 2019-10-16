---
title: XElement 및 XDocument 개체의 유효한 콘텐츠3
ms.date: 07/20/2015
ms.assetid: 0d253586-2b97-459f-b1a7-f30f38f3ed9f
ms.openlocfilehash: 1ad5b18e3bbc2143a56f9c8e7b34354761b4e42f
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590942"
---
# <a name="valid-content-of-xelement-and-xdocument-objects"></a>XElement 및 XDocument 개체의 올바른 콘텐츠
이 항목에서는 생성자에 전달될 수 있는 유효한 인수에 대해 설명하고 내용을 요소와 문서에 추가하는 데 사용하는 메서드에 대한 정보를 제공합니다.  
  
## <a name="valid-content"></a>유효한 내용  
 쿼리는 흔히 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XAttribute>로 확인되며, <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XAttribute> 개체의 컬렉션은 <xref:System.Xml.Linq.XElement> 생성자로 전달할 수 있습니다. 따라서 XML 트리를 채우는 데 사용하는 메서드와 생성자에 쿼리의 결과를 내용으로 전달하는 것이 편리합니다.  
  
 간단한 내용을 추가할 때 다양한 형식이 이 메서드에 전달될 수 있습니다. 유효한 형식은 다음과 같습니다.  
  
- <xref:System.String>  
  
- <xref:System.Double>  
  
- <xref:System.Single>  
  
- <xref:System.Decimal>  
  
- <xref:System.Boolean>  
  
- <xref:System.DateTime>  
  
- <xref:System.TimeSpan>  
  
- <xref:System.DateTimeOffset>  
  
- `Object.ToString`을 구현하는 임의의 형식  
  
- <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 임의의 형식  
  
 복잡한 내용을 추가할 때 다양한 형식이 이 메서드에 전달될 수 있습니다.  
  
- <xref:System.Xml.Linq.XObject>  
  
- <xref:System.Xml.Linq.XNode>  
  
- <xref:System.Xml.Linq.XAttribute>  
  
- <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 임의의 형식  
  
 개체가 <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 경우 개체의 컬렉션이 열거되고 컬렉션의 모든 항목이 추가됩니다. 컬렉션에 <xref:System.Xml.Linq.XNode> 또는 <xref:System.Xml.Linq.XAttribute> 개체가 포함되어 있으면 컬렉션의 각 항목이 개별적으로 추가됩니다. 컬렉션에 텍스트(또는 텍스트로 변환된 개체)가 포함되어 있으면 컬렉션의 텍스트가 연결되어 단일 텍스트 노드로 추가됩니다.  
  
 내용이 `null`이면 아무 것도 추가되지 않습니다. 컬렉션을 전달할 때 컬렉션의 항목은 `null`일 수 있습니다. 컬렉션의 `null` 항목은 트리에 아무 영향도 미치지 않습니다.  
  
 추가된 특성은 포함하는 요소에서 고유한 이름을 갖고 있어야 합니다.  
  
 <xref:System.Xml.Linq.XNode> 또는 <xref:System.Xml.Linq.XAttribute> 개체를 추가할 때 새 내용에 부모가 없으면 개체가 XML 트리에 추가되기만 합니다. 새 내용이 이미 부모를 갖고 있고 다른 XML 트리의 일부이면 새 내용이 복제되고 새로 복제된 내용이 XML 트리에 추가됩니다.  
  
## <a name="valid-content-for-documents"></a>문서의 유효한 내용  
 특성과 간단한 내용은 문서에 추가될 수 없습니다.  
  
 <xref:System.Xml.Linq.XDocument>를 만들어야 하는 시나리오는 많지 않습니다. 대신 일반적으로 <xref:System.Xml.Linq.XElement> 루트 노드를 사용하여 XML 트리를 만들 수 있습니다. 문서를 만들어야 하는 특정 요구 사항(예를 들어, 최상위 수준에서 처리 명령과 주석을 만들어야 하거나 문서 형식을 지원해야 하는 경우)이 없는 한 <xref:System.Xml.Linq.XElement>를 루트 노드로 사용하는 것이 더 편리한 경우가 많습니다.  
  
 문서의 유효한 내용은 다음과 같습니다.  
  
- 0개나 1개의 <xref:System.Xml.Linq.XDocumentType> 개체. 문서 형식이 요소 앞에 나와야 합니다.  
  
- 0개나 1개의 요소  
  
- 0개 이상의 주석  
  
- 0개 이상의 처리 명령  
  
- 공백만 포함된 0개 이상의 텍스트 노드  
  
## <a name="constructors-and-functions-that-allow-adding-content"></a>내용 추가를 허용하는 생성자 및 함수  
 다음 메서드를 사용하여 자식 내용을 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument>에 추가할 수 있습니다.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.%23ctor%2A>|<xref:System.Xml.Linq.XElement>를 생성합니다.|  
|<xref:System.Xml.Linq.XDocument.%23ctor%2A>|<xref:System.Xml.Linq.XDocument>를 생성합니다.|  
|<xref:System.Xml.Linq.XContainer.Add%2A>|<xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument>의 자식 내용 끝 부분에 내용을 추가합니다.|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|<xref:System.Xml.Linq.XNode> 뒤에 내용을 추가합니다.|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|<xref:System.Xml.Linq.XNode> 앞에 내용을 추가합니다.|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|<xref:System.Xml.Linq.XContainer>의 자식 내용 시작 부분에 내용을 추가합니다.|  
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A>|<xref:System.Xml.Linq.XElement>의 모든 내용(자식 노드 및 특성)을 바꿉니다.|  
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A>|<xref:System.Xml.Linq.XElement>의 특성을 바꿉니다.|  
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A>|자식 노드를 새 내용으로 바꿉니다.|  
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A>|노드를 새 내용으로 바꿉니다.|  
  
## <a name="see-also"></a>참고 항목

- [XML 트리 만들기(C#)](./linq-to-xml-overview.md)
