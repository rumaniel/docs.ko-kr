---
title: 유지되지 않고 확장되는 엔터티 참조
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: ffd97806-ab43-4538-8de2-5828bfbbde57
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7a55aa71ff3976241b96dd12baef06a9a13ef9dd
ms.sourcegitcommit: 5bbfe34a9a14e4ccb22367e57b57585c208cf757
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2018
ms.locfileid: "45998424"
---
# <a name="entity-references-are-expanded-and-not-preserved"></a>유지되지 않고 확장되는 엔터티 참조
엔터티 참조가 확장되어 해당 참조가 나타내는 텍스트로 바뀌면 **XmlEntityReference** 노드가 생성되지 않습니다. 대신 엔터티 선언이 구문 분석되고 선언의 내용에서 생성된 노드가 **XmlEntityReference**를 대신하여 복사됩니다. 따라서 `&publisher;` 예제에서 `&publisher;`가 저장되는 대신 **XmlText** 노드가 생성됩니다.  
  
 ![확장된 트리 구조](../../../../docs/standard/data/xml/media/xmlentityref-expanded-nodes.gif "xmlentityref_expanded_nodes")  
확장되는 엔터티 참조의 트리 구조  
  
 `B` 또는 `<` 같은 문자 엔터티는 유지되지 않습니다. 대신 항상 확장되어 텍스트 노드로 표현됩니다.  
  
 **XmlEntityReference** 노드와 해당 노드에 첨부된 엔터티 참조의 자식 노드를 유지하려면 **EntityHandling** 플래그를 **ExpandCharEntities**로 설정합니다. 그러지 않을 경우 **EntityHandling** 플래그를 기본값인 **ExpandEntities**로 둡니다. 이 경우 DOM에서 entityreference 노드가 유지되지 않습니다. 노드는 엔터티 선언의 자식 노드 복사본인 노드로 바뀝니다.  
  
 엔터티 참조를 유지하지 않는 경우 발생할 수 있는 부작용 중 하나는 문서를 저장하고 다른 애플리케이션에 전달할 때 수신 애플리케이션에서 노드가 엔터티 참조로 만들어졌다는 것을 알 수 없게 된다는 점입니다. 그러나 엔터티 참조를 유지하는 경우 수신 애플리케이션에서 엔터티 참조를 인식하고 자식 노드를 읽습니다. 자식 노드가 엔터티 선언에 있던 정보를 나타내는 것은 분명합니다. 예를 들어, 엔터티 참조가 유지되는 경우 DOM은 이론적으로 다음과 같은 구조를 가집니다.  
  
 XmlElement: publisher  
  
 XmlEntityReference: `&publisher;`  
  
 XmlText: Microsoft Press  
  
 엔터티 참조가 DOM에서 확장되는 것이 기본 메서드이며 이 경우 다음 트리 형식의 구조를 갖습니다.  
  
 XmlElement: publisher  
  
 XmlText: Microsoft Press  
  
 엔터티 참조 노드가 없으며 수신 애플리케이션에서 “Microsoft Press”를 포함하는 **XmlText** 노드가 엔터티 선언에서 생성된 것을 알 수 없습니다.  
  
 엔터티를 확인하지 못하는 판독기를 사용하면 엔터티 참조가 나오는 경우 **Load** 메서드에서 예외를 throw합니다.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
