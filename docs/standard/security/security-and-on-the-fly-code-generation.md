---
title: 보안 및 빠른 코드 생성
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- code security, on-the-fly code generation
- on-the-fly code generation
- security [.NET Framework], on-the-fly code generation
- secure coding, on-the-fly code generation
ms.assetid: 6d221724-bb21-4d76-90c3-0ee2a2e69be2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ffb1081c80c31353ad38080ae16ef9f8a74b5481
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61860544"
---
# <a name="security-and-on-the-fly-code-generation"></a>보안 및 빠른 코드 생성
일부 라이브러리는 코드를 생성하고 실행하여 호출자에 대한 일부 작업을 수행하는 방식으로 작동합니다. 기본적인 문제는 낮은 신뢰 수준의 코드를 대신하여 코드를 생성하고 높은 신뢰 수준에서 실행하는 것입니다. 호출자가 코드 생성에 영향을 줄 수 있는 경우 문제가 더욱 악화되므로 안전하다고 생각하는 코드만 생성되도록 해야 합니다.  
  
 항상 어떤 코드를 생성하는지 정확히 알고 있어야 합니다. 즉, 따옴표로 묶인 문자열(예기치 않은 코드 요소를 포함할 수 없도록 이스케이프해야 함), 식별자(유효한 식별자인지 확인해야 함) 또는 기타 값인지에 관계없이 사용자로부터 얻는 값을 엄격하게 제어해야 합니다. 보안 취약성인 경우는 드물지만 식별자에 이상한 문자가 포함되도록 컴파일된 어셈블리를 수정할 수 있고 이 경우 어셈블리가 손상되기 때문에 식별자는 위험할 수 있습니다.  
  
 리플렉션 내보내기를 사용하여 코드를 생성하는 것이 좋으며, 그러면 이러한 많은 문제를 방지하는 데 도움이 되는 경우가 많습니다.  
  
 코드를 컴파일하는 경우 악성 프로그램이 코드를 수정할 수 있는 방법이 있는지 여부를 고려합니다. 컴파일러가 소스 코드를 읽기 전이나 코드가 .dll 파일을 로드하기 전에 악성 코드가 디스크의 소스 코드를 변경할 수 있는 짧은 기간이 있나요? 있다면 파일 시스템에서 액세스 제어 목록을 적절하게 사용하여 이러한 파일을 포함하는 디렉터리를 보호해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../../docs/standard/security/secure-coding-guidelines.md)
