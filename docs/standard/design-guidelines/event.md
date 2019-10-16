---
title: 이벤트 디자인
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- pre-events
- events [.NET Framework], design guidelines
- member design guidelines, events
- event handlers [.NET Framework], event design guidelines
- post-events
- signatures, event handling
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
author: KrzysztofCwalina
ms.openlocfilehash: 530c68ea5342263acd07f8dc8a8c8ce889652503
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026447"
---
# <a name="event-design"></a>이벤트 디자인
이벤트는 자주 사용 하는 형식의 콜백 (사용자 코드를 호출 하기 위해 프레임 워크를 사용할 수 있는 구문)입니다. 대리자, 가상 멤버 및 인터페이스 기반 플러그 인을 수행 하는 멤버를 포함 하는 다른 콜백 메커니즘입니다. 유용성 연구에서 데이터는 대부분의 개발자는 더 편리한 다른 콜백 메커니즘을 사용 하는 것 보다 이벤트를 사용 하는 것을 나타냅니다. 이벤트는 Visual Studio 및 다양 한 언어와 원활 하 게 통합 됩니다.  
  
 두 개의 그룹 이벤트에는 반드시:의 상태가 사전 이벤트 및 상태 변경 후에 발생 하는 이벤트를 호출 하는 시스템 변경 하기 전에 발생 하는 이벤트 후 이벤트를 호출 합니다. 사전 이벤트의 예로 `Form.Closing`, 폼이 닫히기 전에 발생 하는 합니다. 이후 이벤트의 예로 `Form.Closed`, 폼을 닫은 후 발생 하는 합니다.  
  
 **✓ DO** "발생" 이라는 용어를 사용 하 여 이벤트 보다는 "발생" 시키는"또는"트리거"입니다.  
  
 **✓ DO** 사용 <xref:System.EventHandler%601?displayProperty=nameWithType> 수동으로 이벤트 처리기로 사용할 새 대리자를 만드는 대신 합니다.  
  
 **✓ CONSIDER** 의 서브 클래스를 사용 하 여 <xref:System.EventArgs> 이벤트 인수로 제외 이벤트 데이터를 이벤트 처리 메서드를 필요가 없습니다 확실히 경우에서 사용할 수 있습니다는 `EventArgs` 직접 입력 합니다.  
  
 사용 하 여 API를 제공 하는 경우 `EventArgs` 직접 있습니다 됩니다 수 호환성을 중단 하지 않고 이벤트를 사용 하 여 수행 하도록 데이터를 추가 합니다. 서브 클래스를 사용 하는 경우에 하는 경우 처음에 완전히 빈 됩니다 필요할 때 하위 클래스에 속성을 추가할 수 있습니다.  
  
 **✓ DO** 보호 된 가상 메서드를 사용 하 여 각 이벤트를 발생 시킵니다. 만 비정적 이벤트 봉인 되지 않은 클래스, 구조체, 봉인 된 클래스 또는 정적 이벤트에 적용 됩니다.  
  
 메서드의 용도 파생된 클래스 재정의 사용 하 여 이벤트를 처리 하는 방법을 제공 하는 것입니다. 파생된 클래스에서 기본 클래스 이벤트를 처리 하는 방법을 더 유연 하 고 더 빠르고, 더 자연 스러운 경우 재정의 규칙에 따라 메서드의 이름을 "On"로 시작 해야 하 고 이벤트의 이름으로와 야 합니다.  
  
 파생된 클래스는 재정의에서 메서드의 기본 구현을 호출 하지 않도록 선택할 수 있습니다. 제대로 작동 하려면 기본 클래스에 필요한 메서드의 처리를 포함 하 여이 준비 됩니다.  
  
 **✓ DO** 하나의 매개 변수는 이벤트를 발생 시키는 보호 된 메서드를 사용 합니다.  
  
 매개 변수 이름은 `e` 및 이벤트 인수 클래스로 입력 해야 합니다.  
  
 **X DO NOT** 비정적 이벤트를 발생 시킬 때 보낸 사람으로 null을 전달 합니다.  
  
 **✓ DO** 정적 이벤트를 발생 시킬 때 보낸 사람으로 null을 전달 합니다.  
  
 **X DO NOT** 이벤트를 발생 시키는 경우 이벤트 데이터 매개 변수와 null을 전달 합니다.  
  
 전달 해야 `EventArgs.Empty` 모든 데이터 이벤트 처리 메서드를 전달 하지 않을 경우. 개발자는이 매개 변수가 null 일 수 없습니다.  
  
 **✓ CONSIDER** 최종 사용자가 취소할 수 있는 이벤트를 발생 합니다. 이 사전 이벤트에만 적용 됩니다.  
  
 사용 하 여 <xref:System.ComponentModel.CancelEventArgs?displayProperty=nameWithType> 또는 최종 사용자가 이벤트를 취소할 수 있도록 이벤트 인수로 해당 하위 클래스입니다.  
  
### <a name="custom-event-handler-design"></a>사용자 지정 이벤트 처리기 디자인  
 경우에는 `EventHandler<T>` 같은 프레임 워크를 제네릭을 지원 하지 않는 clr 버전을 사용 해야 하는 경우 사용할 수 없습니다. 이러한 경우를 디자인 하는 사용자 지정 이벤트 처리기 대리자를 개발 해야 합니다.  
  
 **✓ DO** 이벤트 처리기에 대 한 void의 반환 형식을 사용 합니다.  
  
 이벤트 처리기에 여러 이벤트 처리 가능한 여러 개체에서 메서드를 호출할 수 있습니다. 이벤트 처리 메서드가 값을 반환할 수, 각 이벤트 호출에 대 한 여러 개의 반환 값은입니다.  
  
 **✓ DO** 사용 `object` 이벤트 처리기의 첫 번째 매개 변수 형식으로 버전을 호출 `sender`합니다.  
  
 **✓ DO** 사용 <xref:System.EventArgs?displayProperty=nameWithType> 또는 해당 하위 클래스의 이벤트 처리기의 두 번째 매개 변수 형식으로 버전을 호출 `e`합니다.  
  
 **X DO NOT** 이벤트 처리기에 두 개 이상의 매개 변수가 있어야 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
