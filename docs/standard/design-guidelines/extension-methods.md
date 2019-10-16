---
title: 확장명 메서드
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: 5de945cb-88f4-49d7-b0e6-f098300cf357
author: KrzysztofCwalina
ms.openlocfilehash: 1835f84a5126ef07adbe119089d2d943ffda18cd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615283"
---
# <a name="extension-methods"></a>확장명 메서드
확장 메서드는 정적 메서드를 인스턴스 메서드 호출 구문을 사용 하 여 호출할 수 있도록 언어 기능. 이러한 메서드는 메서드를의 동작에 인스턴스를 나타내는 하나 이상의 매개 변수를 수행 해야 합니다.  
  
 이러한 확장 메서드를 정의 하는 클래스를 "스폰서" 클래스 라고 하 고 정적으로 선언 되어야 합니다. 확장 메서드를 사용 하려면 하나 스폰서 클래스를 정의 하는 네임 스페이스를 가져와야 합니다.  
  
 **X AVOID** frivolously 소유 하지 않은 형식에서 특히 확장 메서드를 정의 합니다.  
  
 형식의 소스 코드를 소유 않은 경우에 일반 인스턴스 메서드를 대신 사용 하는 것이 좋습니다. 소유 하지 않습니다 하 고 메서드를 추가 하려는 경우 매우 주의 해야 합니다. 확장 메서드의 자유롭게 사용 하 여 이러한 메서드를 하도록 설계 되지 않았습니다 하는 형식의 Api 어지럽히지의 잠재력을 있습니다.  
  
 **✓ CONSIDER** 확장 메서드를 사용 하 여 다음과 같은 시나리오 중 하나:  
  
- 도우미를 제공 하는 핵심 인터페이스 측면에서 기능을 언급 하는 경우 인터페이스의 모든 구현 관련 기능을 작성할 수 있습니다. 구체적인 구현은 인터페이스가 고, 그렇지 할당할 수 없습니다 때문입니다. 예를 들어 합니다 `LINQ to Objects` 연산자는 모두에 대 한 확장 메서드로 구현 됩니다 <xref:System.Collections.Generic.IEnumerable%601> 형식입니다. 따라서 모든 `IEnumerable<>` 구현에서 자동으로 LINQ를 사용할 수 있습니다.  
  
- 일부 형식에 종속 되지만 이러한 종속성 인스턴스 메서드는 제공 하는 경우 종속성 관리 규칙 중단 됩니다. 예를 들어, 종속 <xref:System.String> 를 <xref:System.Uri?displayProperty=nameWithType> 바람직하지 않을 것 등 `String.ToUri()` 반환 되는 인스턴스 메서드 `System.Uri` 종속성 관리 측면에서 잘못 된 디자인 됩니다. 정적 확장 메서드 `Uri.ToUri(this string str)` 반환 `System.Uri` 훨씬 더 나은 디자인 됩니다.  
  
 **X AVOID** 에서 확장 메서드를 정의 <xref:System.Object?displayProperty=nameWithType>합니다.  
  
 VB 사용자 확장 메서드 구문을 사용 하 여 개체 참조에서 이러한 메서드를 호출할 수 없습니다. VB vb의 경우 바인딩된 개체를 가져오면 되도록 런타임에 대 한 모든 메서드 호출으로 대 한 참조를 선언 하기 때문에 이러한 메서드 호출을 지원 하지 않습니다 (실제 멤버는 런타임에 결정 됨), 확장 메서드 바인딩 컴파일 시간 (초기에 결정 되는 동안 바인딩된).  
  
 지침에 적용 됩니다. 동일한 바인딩 동작 있는지 다른 언어 또는 확장 메서드가 지원 되지 않습니다.  
  
 **X DO NOT** 종속성 관리 또는 인터페이스에 메서드 추가 하지 않은 확장된 유형으로 동일한 네임 스페이스에 확장 메서드를 배치 합니다.  
  
 **X AVOID** 다른 네임 스페이스에 상주 하는 경우에 동일한 서명으로 두 개 이상의 확장 메서드를 정의 합니다.  
  
 **✓ CONSIDER** 형식이 인터페이스 및 확장 메서드는 대부분 또는 모든 경우에 사용 하려는 경우 확장된 유형으로 동일한 네임 스페이스의 확장 메서드를 정의 합니다.  
  
 **X DO NOT** 다른 기능과 함께 일반적으로 관련 된 네임 스페이스에는 기능을 구현 하는 확장 메서드를 정의 합니다. 대신, 자신이 속한 기능과 관련 된 네임 스페이스에서 정의 합니다.  
  
 **X AVOID** 확장 메서드 (예: "확장")에 네임 스페이스의 일반 이름을 지정 합니다. 설명이 포함 된 이름을 사용 하 여 (예를 들어, "라우팅") 대신 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
