---
title: '방법: 사용자 지정 이벤트 접근자 구현(C# 프로그래밍 가이드)'
ms.date: 07/20/2015
helpviewer_keywords:
- accessors [C#], event accessors
- add accessor [C#]
- events [C#], add accessor
- events [C#], remove accessor
- remove accessor [C#]
ms.assetid: bf903abf-03a4-4f7b-ab6b-b7e59bc2ee1e
ms.openlocfilehash: 759a7a4518a371449723a23669816bbc0fbc0dee
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836711"
---
# <a name="how-to-implement-custom-event-accessors-c-programming-guide"></a>방법: 사용자 지정 이벤트 접근자 구현(C# 프로그래밍 가이드)
이벤트는 선언된 클래스 내에서만 호출할 수 있는 특수한 종류의 멀티캐스트 대리자입니다. 클라이언트 코드는 이벤트가 발생할 때 호출되어야 하는 메서드에 대한 참조를 제공하여 이벤트를 구독합니다. 이러한 메서드는 이벤트 접근자의 이름이 `add` 및 `remove`로 지정된다는 점을 제외하고 속성 접근자와 유사한 이벤트 접근자를 통해 대리자의 호출 목록에 추가됩니다. 대부분의 경우 사용자 지정 이벤트 접근자를 제공할 필요가 없습니다. 코드에서 사용자 지정 이벤트 접근자를 제공하지 않으면 컴파일러가 자동으로 추가합니다. 그러나 경우에 따라 사용자 지정 동작을 제공해야 할 수도 있습니다. [방법: 인터페이스 이벤트 구현](../../../csharp/programming-guide/events/how-to-implement-interface-events.md) 항목에는 이러한 사례 중 하나가 나와 있습니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 사용자 지정 add 및 remove 이벤트 접근자를 구현하는 방법을 보여 줍니다. 접근자 내의 모든 코드를 대체할 수 있지만 새 이벤트 처리기 메서드를 추가하거나 제거하기 전에 이벤트를 잠그는 것이 좋습니다.  
  
[!code-csharp[IDrawingObject.OnDraw](codesnippet/CSharp/how-to-implement-interface-events_1.cs#IDrawingObjectOnDraw)]  
  
## <a name="see-also"></a>참고 항목

- [이벤트](../../../csharp/programming-guide/events/index.md)  
- [event](../../../csharp/language-reference/keywords/event.md)