---
title: 새 엔터티 참조 만들기
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: a42f81b3-0403-4e34-b346-7d2129804e54
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 67fdbcdbff64bcd91c80fbeaec0c41982b68d98f
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48844516"
---
# <a name="creating-new-entity-references"></a>새 엔터티 참조 만들기
**CreateEntityReference** 메서드는 새 **XmlEntityReference** 노드를 만듭니다. XML DOM(문서 개체 모델)에서는 참조될 엔터티 이름이 이미 선언되지 않았는지 확인합니다. 선언된 경우 **XmlEntityReference** 노드의 자식 노드가 엔터티 선언 노드에서 복사됩니다. 일치하는 엔터티 선언이 없으면 entityreference 노드의 유일한 자식으로 빈 텍스트 노드가 추가됩니다. **XmlEntityReference** 노드의 자식 노드는 다른 노드의 복사본이므로 이러한 자식 노드는 읽기 전용이며 수정할 수 없습니다.  
  
 노드가 복사될 때 엔터티 참조가 있는 범위에 네임스페이스가 있을 수 있습니다. 이 네임스페이스는 생성되는 모든 요소 또는 특성 노드의 구성에 영향을 줍니다.  
  
> [!NOTE]
>  DOM에서는 **EntityReference** 노드를 문서에 삽입할 경우에만 **EntityReference**에 자식 노드를 추가합니다. 새로 생성되는 **EntityReference** 노드에는 자식 노드가 없습니다.  
  
 **XmlDataDocument**가 **XmlDocument**의 파생 클래스인 경우에도 **XmlDataDocument**는 엔터티 참조의 생성을 지원하지 않습니다. 이는 **EntityReference** 자식 노드가 읽기 전용이기 때문입니다. **EntityReference** 노드의 자식 노드는 둘 이상의 영역에 걸쳐 있을 수 있습니다. 이 경우 **EntityReference**의 일부를 포함하는 영역과 관련된 행의 일부가 읽기 전용이 됩니다.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
