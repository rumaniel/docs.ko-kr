---
title: 봉인
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- limiting extensibility
- classes [.NET Framework], sealing
- preventing customization
- sealed classes
ms.assetid: cc42267f-bb7a-427a-845e-df97408528d4
author: KrzysztofCwalina
ms.openlocfilehash: f25573c0fef29ef54dc04c5287757903429d89d4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615209"
---
# <a name="sealing"></a>봉인
개체 지향 프레임 워크의 기능 중 하나에 개발자가 확장 하 고 프레임 워크 디자이너에서 예기치 않은 방식으로 사용자 지정할 수 있는 것입니다. 이 기능과 확장 가능한 디자인 하는 위험 합니다. 프레임 워크를 디자인할 때, 따라서, 원할 경우 신중 하 게 확장성에 대 한 디자인 및 위험한 경우 확장성 제한에 매우 중요 합니다.  
  
 확장성을 방지 하는 강력한 메커니즘을 봉인 됩니다. 클래스 또는 개별 멤버를 봉인할 수 있습니다. 클래스를 봉인 사용자를 클래스에서 상속할 수 없습니다. 멤버를 봉인 사용자를에서 특정 멤버를 재정의할 수 없습니다.  
  
 **X DO NOT** 이유가 할 필요 없이 클래스를 봉인 합니다.  
  
 이유가 아닙니다 확장성 시나리오를 생각할 수 없습니다 때문에 클래스를 봉인 합니다. 프레임 워크 사용자 편의 멤버를 추가 하는 등 다양 한 nonobvious 이유로 클래스에서 상속 하려고 합니다. 참조 [봉인 되지 않은 클래스](../../../docs/standard/design-guidelines/unsealed-classes.md) nonobvious 이유의 예제를 보려면 사용자 형식에서 상속 하려고 합니다.  
  
 봉인 클래스에 대 한 좋은 이유는 다음과 같습니다.  
  
- 클래스는 정적 클래스입니다. 참조 [정적 클래스 디자인](../../../docs/standard/design-guidelines/static-class.md)합니다.  
  
- 클래스는 상속 된 보호 된 멤버의 보안과 관련 된 비밀을 저장합니다.  
  
- 클래스는 여러 가상 멤버를 상속 하 고 비용을 개별적으로 봉인 클래스 봉인 되지 않은 유지 이점 보다 클 것입니다.  
  
- 클래스에는 매우 빠른 런타임 조회를 필요로 하는 특성입니다. Sealed 특성 경우 봉인 되지 않은 것 보다 약간 더 높은 성능 수준 참조 [특성](../../../docs/standard/design-guidelines/attributes.md)합니다.  
  
 **X DO NOT** 보호 또는 가상 멤버를 sealed 형식으로 선언 합니다.  
  
 기본적으로 sealed 형식에서 상속할 수 없습니다. 즉, sealed 형식에 대해 보호 된 멤버를 호출할 수 없습니다를 sealed 형식에 대해 가상 메서드를 재정의할 수 없습니다.  
  
 **✓ CONSIDER** 재정의할 수 있는 멤버가 봉인 합니다.  
  
 가상 멤버 소개에서 발생할 수 있는 문제 (에서 설명한 [가상 멤버](../../../docs/standard/design-guidelines/virtual-members.md)) 약간 낮은 수준으로 지원 하지만 재정의를 적용 합니다. 재정의가 봉인 하면 상속 계층의 해당 지점에서 시작 하는 이러한 문제 로부터 보호 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [확장성을 위한 디자인](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
- [봉인되지 않은 클래스](../../../docs/standard/design-guidelines/unsealed-classes.md)
