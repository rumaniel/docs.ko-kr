---
title: 멤버 디자인 지침
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines [.NET Framework], about member design guidelines
- members [.NET Framework], design guidelines
- class library design guidelines [.NET Framework], members
- member design guidelines [.NET Framework]
ms.assetid: 0ce93180-1d7b-4f8c-9306-f828b2d66b8f
author: KrzysztofCwalina
ms.openlocfilehash: d7023bbe59eb3590af47952a2fe24c5f40b3ca68
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945524"
---
# <a name="member-design-guidelines"></a>멤버 디자인 지침
메서드, 속성, 이벤트, 생성자 및 필드가 통칭 하 여 멤버 라고 합니다. 멤버는 궁극적으로 프레임 워크 기능 프레임 워크의 최종 사용자에 게 노출 되는 의미입니다.  
  
 멤버는 가상 또는 비가상, 구체적인 또는 추상 정적 또는 인스턴스 수 및 내게 필요한 옵션의 몇 가지 다른 범위를 가질 수 있습니다. 모든이 다양성이 놀라운 표현을 제공 하지만 동시에 프레임 워크 디자이너 부분 주의 해야 합니다.  
  
 이 장에서 모든 형식의 멤버를 디자인할 때 수행 해야 하는 기본 지침을 제공 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [멤버 오버로드](../../../docs/standard/design-guidelines/member-overloading.md)  
 [속성 디자인](../../../docs/standard/design-guidelines/property.md)  
 [생성자 디자인](../../../docs/standard/design-guidelines/constructor.md)  
 [이벤트 디자인](../../../docs/standard/design-guidelines/event.md)  
 [필드 디자인](../../../docs/standard/design-guidelines/field.md)  
 [확장명 메서드](../../../docs/standard/design-guidelines/extension-methods.md)  
 [연산자 오버로드](../../../docs/standard/design-guidelines/operator-overloads.md)  
 [매개 변수 디자인](../../../docs/standard/design-guidelines/parameter-design.md)  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
