---
title: 확장성을 위한 디자인
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- extending class libraries
- extensibility with class libraries in .NET Framework
- class library design guidelines [.NET Framework], extensibility
- class library extensibility [.NET Framework]
ms.assetid: 1cdb8740-871a-456c-9bd9-db96ca8d79b3
author: KrzysztofCwalina
ms.openlocfilehash: 94900dee72230a1b9d099d78168acc508af62af7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026460"
---
# <a name="designing-for-extensibility"></a>확장성을 위한 디자인
프레임 워크 디자인의 중요 한 측면 있는지 확인 하는 프레임 워크의 확장성을 신중 하 게 고려 했습니다. 그러려면, 비용 및 다양 한 확장성 메커니즘을 사용 하 여 연결 된 혜택을 파악 해야 합니다. 이 장에서 확장성 메커니즘을 결정 하 고-서브클래싱, 이벤트, 가상 멤버, 콜백 및 등-프레임 워크의 요구 사항을 충족할 수 있습니다.  
  
 프레임 워크의 확장성을 허용 하는 방법은 여러 가지입니다. 이러한 범위에서 덜 강력 하지만 비용이 덜 드는 매우 강력 하지만 비용이 많이 드는입니다. 모든 지정 된 확장성 요구 사항에 대 한 요구 사항을 충족 하는 가장 비용이 많이 드는 확장성 메커니즘을 선택 해야 합니다. 일반적으로 더 큰 확장성을 나중에 추가할 수 있기 벗어날 수 있지만 수 고 떨어진 새로운 변경 사항 없이 염두에서에 둡니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [봉인되지 않은 클래스](../../../docs/standard/design-guidelines/unsealed-classes.md)  
 [보호된 멤버](../../../docs/standard/design-guidelines/protected-members.md)  
 [이벤트 및 콜백](../../../docs/standard/design-guidelines/events-and-callbacks.md)  
 [가상 멤버](../../../docs/standard/design-guidelines/virtual-members.md)  
 [추상화(추상 형식 및 인터페이스)](../../../docs/standard/design-guidelines/abstractions-abstract-types-and-interfaces.md)  
 [추상화 구현을 위한 기본 클래스](../../../docs/standard/design-guidelines/base-classes-for-implementing-abstractions.md)  
 [봉인](../../../docs/standard/design-guidelines/sealing.md)  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
