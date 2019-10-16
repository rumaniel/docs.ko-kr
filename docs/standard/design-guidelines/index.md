---
title: 프레임워크 디자인 지침
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- libraries, .NET Framework class library
- class library design guidelines [.NET Framework], about
- class library design guidelines [.NET Framework]
ms.assetid: 5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b
author: KrzysztofCwalina
ms.openlocfilehash: c20430f9cdcd71cc2e178d38aeed48f9fa4e75c5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026382"
---
# <a name="framework-design-guidelines"></a>프레임워크 디자인 지침
이 섹션에서는 확장 하 고.NET Framework와 상호 작용 하는 라이브러리를 디자인 하기 위한 지침을 제공 합니다. 목표는 개발에 사용 되는 프로그래밍 언어의 독립적인 통합된 프로그래밍 모델을 제공 하 여 API 일관성과 사용 편의성을 확인 하는 라이브러리 디자이너가 데 도움이 됩니다. 클래스 및.NET Framework를 확장 하는 구성 요소를 개발할 때 이러한 디자인 지침을 따르는 것이 좋습니다. 일관성 없는 라이브러리 디자인 부정적인 개발자 생산성에 영향을 줍니다 및 도입을 방지 합니다.  
  
 지침 용어를 접두사로 하는 간단한 권장 사항으로 구성 됩니다 `Do`, `Consider`를 `Avoid`, 및 `Do not`합니다. 이러한 지침은 여러 솔루션 간의 장단점을 이해 하는 클래스 라이브러리 디자이너를 돕기 위해 고안 되었습니다. 적절 한 라이브러리 디자인 이러한 지침을 위반 하는 필요로 하는 경우가 있을 수 있습니다. 이러한 경우는 드문 경우 지만 있어야 합니다. 하 고 결정 한 명확 하 고 매력적인 이유 있어야 합니다.  
  
 이러한 지침의 저서에서 발췌 한 것은 *Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과*Krzysztof Cwalina 및 Brad Abrams 여 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [명명 지침](../../../docs/standard/design-guidelines/naming-guidelines.md)  
 어셈블리, 네임 스페이스, 형식 및 클래스 라이브러리의 멤버 이름 지정에 대 한 지침을 제공 합니다.  
  
 [형식 디자인 지침](../../../docs/standard/design-guidelines/type.md)  
 정적 및 추상 클래스, 인터페이스, 열거형, 구조체 및 기타 형식 사용 하기 위한 지침을 제공 합니다.  
  
 [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)  
 디자인 하 고 속성, 메서드, 생성자, 필드, 이벤트, 연산자 및 매개 변수를 사용 하 여 지침을 제공 합니다.  
  
 [확장성을 위한 디자인](../../../docs/standard/design-guidelines/designing-for-extensibility.md)  
 서브클래싱, 이벤트, 가상 멤버 및 콜백을 사용 하 여 같은 확장성 메커니즘을 설명 하 고 가장 프레임 워크의 요구를 충족 하는 메커니즘을 선택 하는 방법에 설명 합니다.  
  
 [예외 디자인 지침](../../../docs/standard/design-guidelines/exceptions.md)  
 디자인, throw 및 catch 하면 예외에 대 한 디자인 지침을 설명 합니다.  
  
 [사용 지침](../../../docs/standard/design-guidelines/usage-guidelines.md)  
 배열, 특성, 컬렉션과 같은 일반적인 형식을 사용 하 여 serialization을 지원 하며 같음 연산자를 오버 로드에 대 한 지침을 설명 합니다.  
  
 [일반 디자인 패턴](../../../docs/standard/design-guidelines/common-design-patterns.md)  
 선택 및 종속성 속성 구현에 대 한 지침을 제공 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [개요](../../../docs/framework/get-started/overview.md)
- [개발 가이드](../../../docs/framework/development-guide.md)
