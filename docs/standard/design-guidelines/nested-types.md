---
title: 중첩 형식
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- types, nested
- public nested types
- type design guidelines, nested types
- nested types
- members [.NET Framework], type
- class library design guidelines [.NET Framework], nested types
ms.assetid: 12feb7f0-b793-4d96-b090-42d6473bab8c
author: KrzysztofCwalina
ms.openlocfilehash: 22c14d05105154ff642cb8a44eda8e7c5d0575e4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61756873"
---
# <a name="nested-types"></a>중첩 형식
중첩된 형식은 바깥쪽 형식 이라고 하는 다른 형식의 범위 내에 정의 된 형식인 합니다. 중첩된 형식은 바깥쪽 형식의 모든 멤버에 액세스할 수 있습니다. 예를 들어, 바깥쪽 형식 및 보호 된 바깥쪽 형식의 모든 상위 항목에 정의 된 필드를 정의 하는 전용 필드에 대 한 액세스를 권한이 있습니다.  
  
 일반적으로 중첩된 형식 꼭 필요할 때만 사용 해야 합니다. 여기에는 여러 가지 이유가 있습니다. 일부 개발자 들은 완전히 개념에 익숙하지 않습니다. 이러한 개발자가 중첩 형식의 변수를 선언 구문 사용 하 여 문제가 예를 들어, 할 수 있습니다. 중첩된 형식은 또한 매우 밀접 하 게 해당 바깥쪽 형식과 및 같이 범용 형식에 적합 하지 않습니다.  
  
 중첩 형식은 바깥쪽 해당 형식의 구현 세부 정보를 모델링 하는 데 적합 합니다. 최종 사용자는 중첩 된 형식의 변수를 선언할 필요가 거의 하 고 거의 발생 하지 않는다는 중첩된 형식을 명시적으로 인스턴스화할 수 있어야 합니다. 예를 들어, 컬렉션의 열거자는 컬렉션의 중첩된 형식 수 있습니다. 열거자, 바깥쪽 형식으로 일반적으로 인스턴스화됩니다 있고 다양 한 언어에서 foreach 문을 지원 하므로 열거자 변수 거의 최종 사용자가 선언 해야 합니다.  
  
 **✓ DO** 중첩된 형식 및 해당 외부 형식 간의 관계는 멤버 액세스 가능성 의미 체계는 바람직한 되도록 하는 경우 중첩 된 형식을 사용 합니다.  
  
 **X DO NOT** 논리적 그룹으로 사용 하 여 공용 중첩된 형식은 생성;이 대 한 네임 스페이스를 사용 합니다.  
  
 **X AVOID** 중첩된 형식은 공개적으로 노출 됩니다. 유일한 예외는 중첩 형식의 변수를 서브클래싱 또는 기타 고급 사용자 지정 시나리오와 같은 드문 시나리오 에서만에서 선언 해야 하는 경우.  
  
 **X DO NOT** 형식이 포함 하는 형식 외부에서 참조 될 가능성이 높은 경우 중첩 된 형식을 사용 합니다.  
  
 예를 들어, 클래스에 정의 된 메서드에 전달 된 열거형 클래스에서 중첩 된 형식으로 정의 되어야 합니다.  
  
 **X DO NOT** 클라이언트 코드에서 인스턴스화 대상으로 해야 하는 경우 중첩 된 형식을 사용 합니다.  형식에 public 생성자가 중첩 않을 해야 합니다.  
  
 형식을 인스턴스화할 수, 있으면 하는 것 처럼 보이지만 형식이 자체적으로 프레임 워크에서 (수를 만들고이 사용, 외부 형식을 사용할 필요 없이 제거), 따라서 중첩 해야 합니다. 내부 형식 관계 없는 외부 형식 외부에서 광범위 하 게 재사용 되지 않아야 외부 형식으로 수신 합니다.  
  
 **X DO NOT** 인터페이스의 구성원으로 중첩 된 형식을 정의 합니다. 대부분의 언어에서는 이러한 구문을 지원 하지 않습니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [형식 디자인 지침](../../../docs/standard/design-guidelines/type.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
