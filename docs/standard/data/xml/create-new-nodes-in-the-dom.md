---
title: DOM에서 새 노드 만들기
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 59ac88b2e7c6b3ecd4d06c0183a2f8a7f4a9e2d4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64590260"
---
# <a name="create-new-nodes-in-the-dom"></a>DOM에서 새 노드 만들기
<xref:System.Xml.XmlDocument>에는 모든 노드 형식에 대한 create 메서드가 있습니다. 필요에 따라 메서드에 이름을 제공하고, 텍스트 노드처럼 내용이 있는 노드에 대한 내용이나 기타 매개 변수를 지정하면 노드가 생성됩니다. 다음은 적합한 노드를 만들기 위해 이름 및 몇 개의 매개 변수를 제공해야 하는 메서드입니다.  
  
- <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
- <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
- <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
- <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
- <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 다른 노드 형식에는 매개 변수에 데이터를 제공하는 것 이상의 요구 사항이 있습니다.  
  
 특성에 대한 자세한 내용은 [DOM에서 요소의 새 특성 만들기](../../../../docs/standard/data/xml/creating-new-attributes-for-elements-in-the-dom.md)를 참조하세요. 요소 및 특성 이름 유효성 검사에 대한 자세한 내용은 [새 노드를 만들 때 XML 요소 및 특성 이름 확인](../../../../docs/standard/data/xml/xml-element-and-attribute-name-verification-when-creating-new-nodes.md)을 참조하세요. 엔터티 참조를 만드는 방법은 [새 엔터티 참조 만들기](../../../../docs/standard/data/xml/creating-new-entity-references.md)를 참조하세요. 네임스페이스가 엔터티 참조의 확장에 미치는 영향에 대한 자세한 내용은 [요소 및 특성이 있는 새 노드의 엔터티 참조 확장에 대한 네임스페이스의 영향](../../../../docs/standard/data/xml/namespace-affect-on-entity-ref-expansion-for-new-nodes.md)을 참조하세요.  
  
 새 노드를 만든 후에 트리에 해당 노드를 삽입하는 데 사용할 수 있는 몇 가지 메서드가 있습니다. 다음 표에는 XML DOM(문서 개체 모델)에서 새 노드가 나타나는 위치에 대한 설명과 함께 해당 메서드가 나열되어 있습니다.  
  
|메서드|노드 배치|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|참조 노드 앞에 삽입됩니다. 예를 들어, 위치 5에 새 노드를 삽입하려면 다음과 같이 입력합니다.<br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> 자세한 내용은 <xref:System.Xml.XmlNode.InsertBefore%2A> 메서드를 참조하세요.|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|참조 노드 다음에 삽입됩니다. 예:<br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> 자세한 내용은 <xref:System.Xml.XmlNode.InsertAfter%2A> 메서드를 참조하세요.|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|노드를 지정된 노드의 자식 노드 목록 끝에 추가합니다. 추가되는 노드가 <xref:System.Xml.XmlDocumentFragment>이면 문서 조각의 전체 내용이 이 노드의 자식 목록으로 이동합니다. 자세한 내용은 <xref:System.Xml.XmlNode.AppendChild%2A> 메서드를 참조하세요.|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|노드를 지정된 노드의 자식 노드 목록 시작 부분에 추가합니다. 추가되는 노드가 <xref:System.Xml.XmlDocumentFragment>이면 문서 조각의 전체 내용이 이 노드의 자식 목록으로 이동합니다. 자세한 내용은 <xref:System.Xml.XmlNode.PrependChild%2A> 메서드를 참조하세요.|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|<xref:System.Xml.XmlAttribute> 노드를 요소와 연관된 특성 컬렉션의 끝에 추가합니다. 자세한 내용은 <xref:System.Xml.XmlAttributeCollection.Append%2A> 메서드를 참조하세요.|  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
