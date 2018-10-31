---
title: DOM을 로드할 경우 공백 문자 및 유효 공백 문자 처리
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1b141a0a-50d8-4ebd-83cd-a84449bb22b2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1d9bbb14320b84a6d417c5c28026b169092de219
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49120988"
---
# <a name="white-space-and-significant-white-space-handling-when-loading-the-dom"></a>DOM을 로드할 경우 공백 문자 및 유효 공백 문자 처리
문서를 로드할 때 이 옵션을 설정하여 공백을 유지하고 문서 트리에 **XmlWhitespace** 노드를 만들 수 있습니다. 공백 노드를 만들려면 **PreserveWhitespace** 속성을 true로 설정합니다. 이 속성이 기본값인 **false**로 설정되면 공백 노드가 생성되지 않습니다. **PreserveWhitespace** 플래그 설정에 관계없이 항상 유효 공백 노드가 유지되며 이 데이터를 나타내는 **XmlSignificantWhitespace** 노드가 메모리에 생성됩니다.  
  
 판독기에서 문서가 로드되면 **XmlDocument** 클래스의 **PreserveWhitespace** 플래그 속성 설정은 **XmlTextReader**의 **WhitespaceHandling** 속성이 **WhitespaceHandling.None**으로 설정되지 않은 경우에만 **XmlWhitespace** 노드 생성에 영향을 줍니다. 이것은 판독기의 **WhitespaceHandling** 속성 값이 **XmlDocument**의 해당 플래그 설정보다 우선하기 때문입니다. **XmlSignificantWhitespace**에 대한 자세한 내용은 <xref:System.Xml.XmlSignificantWhitespace>를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
