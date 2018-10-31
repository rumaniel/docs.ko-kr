---
title: DOM의 네임스페이스 및 DTD
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1e9b55c4-76ad-4f54-8d96-7ce4b4cf1e05
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bc8a1de8ab10eff88757720a35aa9668125cfbfa
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582163"
---
# <a name="namespaces-and-dtds-in-the-dom"></a>DOM의 네임스페이스 및 DTD
DTD(문서 종류 정의)는 네임스페이스 지원을 어렵게 합니다. 예를 들어, 다음 XML에는 이름에 콜론이 포함되는 기본 특성이 있습니다.  
  
```xml  
<!ATTLIST item x:id CDATA #IMPLIED>  
```  
  
 다음은 이 구문이 허용되는 경우의 해결책입니다.  
  
-   `x:`를 네임스페이스 접두사로 처리하지만 이 접두사는 `xmlns:x` 네임스페이스 선언을 사용하여 확인할 수 있도록 DTD에도 포함되어 있어야 합니다. 이 접두사를 인스턴스 문서의 다른 항목에 매핑하는 것은 오류입니다.  
  
-   `x:`는 네임스페이스 접두사로 처리하지만 이 접두사는 항상 인스턴스 요소의 컨텍스트에서 확인됩니다. 즉, 실제로 `item` 요소가 나타난 네임스페이스 범위에 따라 다양한 네임스페이스 URI(Uniform Resource Identifier)에 접두사가 매핑될 수 있습니다. 이 동작은 이전 목록에서 제시된 해결책보다는 예측 가능성이 크지만 기본 특성을 구체화해야 하기 때문에 다른 복잡한 문제를 가져옵니다.  
  
-   콜론은 DTD에 있기 때문에 무시되고 특성 이름은 접두사와 네임스페이스 URI가 없는 `x:y`입니다.  
  
-   기본 특성의 콜론은 DTD 내부에서 이름에 콜론을 사용할 수 없음을 알리는 예외가 throw됩니다. 이것은 예측 가능한 동작이지만 W3C(World Wide Web 컨소시엄)에서 배포한 많은 DTD를 로드할 수 없다는 것을 의미합니다.  
  
-   사용자가 DTD 유효성 검사를 요청하면 전체 문서에 대한 네임스페이스 지원이 해제됩니다. 이렇게 하면 W3C DTD를 로드하고 동작을 예측할 수 있습니다.  
  
 Microsoft .NET Framework의 XML은 W3C 호환성을 극대화하기 위해 두 번째 옵션을 구현합니다.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
