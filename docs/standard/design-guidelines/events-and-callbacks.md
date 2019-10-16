---
title: 이벤트 및 콜백
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], extensibility
- methods [.NET Framework], callback
- callback methods
- callbacks
ms.assetid: 48b55c60-495f-4089-9396-97f9122bba7c
author: KrzysztofCwalina
ms.openlocfilehash: 3609d6ac4847cb081740fd698869df4976f83f8f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61960409"
---
# <a name="events-and-callbacks"></a>이벤트 및 콜백
콜백을 대리자를 통해 사용자 코드를 다시 호출 하는 프레임 워크를 사용할 수 있는 확장성 지점입니다. 이러한 대리자는 일반적으로 메서드의 매개 변수를 통해 프레임 워크에 전달 됩니다.  
  
 이벤트는 대리자 (이벤트 처리기)를 제공 하기 위한 편리 하 고 일관 된 구문을 지 콜백의 특수 사례입니다. 또한 Visual Studio의 문 완성 및 디자이너 이벤트 기반 Api를 사용 하 여 도움말을 제공 합니다. (참조 [이벤트 디자인](../../../docs/standard/design-guidelines/event.md).)  
  
 **✓ CONSIDER** 콜백을 사용 하 여 프레임 워크에서 실행할 사용자 지정 코드를 제공 하는 사용자 수 있도록 합니다.  
  
 **✓ CONSIDER** 이벤트를 사용 하 여 사용자가 개체 지향 디자인을 이해 하는 데 필요 없이 프레임 워크의 동작을 사용자 지정할 수 있도록 합니다.  
  
 **✓ DO** 더 넓은 범위의 개발자에 게 친숙 문 완성 Visual Studio와 통합 되어 있기 때문에 이벤트 일반 콜백 보다 선호 합니다.  
  
 **X AVOID** 성능에 민감한 Api에서 콜백을 사용 합니다.  
  
 **✓ DO** 새로운 `Func<...>`, `Action<...>`, 또는 `Expression<...>` 아니라 콜백과 함께 Api를 정의할 때 사용자 지정 대리자 형식이 지정 되어야 합니다.  
  
 `Func<...>` 및 `Action<...>` 제네릭 대리자를 나타냅니다. `Expression<...>` 컴파일할 수도 없지만 런타임에 호출 이후에 수 있는 함수 정의 나타내는 직렬화 되며 원격 프로세스에 전달 됩니다.  
  
 **✓ DO** 사용의 성능에 미치는 영향을 이해 하 고 측정 `Expression<...>`를 사용 하는 대신 `Func<...>` 및 `Action<...>` 대리자입니다.  
  
 `Expression<...>` 형식은 대부분의 경우 논리적으로 같습니다 `Func<...>` 고 `Action<...>` 대리자입니다. 대리자는 로컬 프로세스 시나리오에서 사용 하도록 둘 간의 주요 차이점은 유용한 및 원격 프로세스 또는 컴퓨터에 대 한 식을 평가 하는 경우 식 수는 있습니다.  
  
 **✓ DO** 대리자를 호출 하 여 임의의 코드 실행은 이해 하 고 보안, 정확성 및 호환성 영향을 줄 수입니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [확장성을 위한 디자인](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
