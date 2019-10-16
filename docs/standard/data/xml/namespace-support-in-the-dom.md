---
title: DOM의 네임스페이스 지원
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: f0548ead-0fed-41ee-b33e-117ba900d3bc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1a468d1a2b15d1f92726d8d429fbc5ddece96e6d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647858"
---
# <a name="namespace-support-in-the-dom"></a>DOM의 네임스페이스 지원
XML DOM(문서 개체 모델)은 네임스페이스를 완전하게 인식합니다. 또한 네임스페이스를 인식하는 XML 문서만 지원됩니다. W3C(World Wide Web 컨소시엄)는 Level 1을 구현한 DOM 애플리케이션은 네임스페이스를 인식하지 못할 수 있으며 DOM Level 2 기능은 네임스페이스를 인식한다고 지정합니다. 하지만 메서드가 Level 1 또는 Level 2 DOM 권장 사항을 따르는지 여부에 관계없이 XML DOM의 모든 기능은 네임스페이스를 인식합니다.  
  
 예를 들어, 네임스페이스를 인식하지 않는 설정에서는 DOM Level 1 권장 사항에 지정된 것처럼 `setAttribute("A:b", "123")`를 호출해도 접두사 `A`와 로컬 이름 `b`를 갖는 특성에 적용되지 않습니다. 대신 `A:b` 값을 갖는 특성에 적용됩니다.  
  
 네임스페이스를 인식하는 환경에서 DOM Level 2 `setAttribute("A:b", "123")`를 호출하면 접두사 `A`와 로컬 이름 `b`를 갖는 특성에 적용됩니다. 이것이 Microsoft .NET Framework DOM의 작동 방식입니다.  
  
 따라서 이름 매개 변수가 사용되는 모든 메서드에서 이름을 정규화하는 접두사도 사용됩니다. **setAttribute** DOM Level 1 메서드의 `A:b`와 같은 이름 매개 변수는 다음과 같이 구문 분석됩니다.  
  
- 콜론(:)이 없으면 로컬 이름이 `name` 매개 변수로 설정되고 접두사와 NamespaceURI는 빈 문자열로 설정됩니다.  
  
- 콜론이 있으면 첫 번째 콜론의 위치에 따라 이름이 두 부분으로 나뉩니다. 콜론 앞에 있는 문자열이 접두사로 설정되고 콜론 뒤에 있는 문자열이 로컬 이름으로 설정됩니다. NamespaceURI 값을 사용하지 않는 메서드의 경우 NamespaceURI가 확인되지 않으며 빈 문자열로 설정된 상태를 유지합니다. 그렇지 않으면 NamespaceURI가 메서드에 전달된 문자열로 설정됩니다. 접두사가 정의되어 있지 않으면 **Save** 메서드와 **InnerXml** 및 **OuterXml** 속성에서 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
