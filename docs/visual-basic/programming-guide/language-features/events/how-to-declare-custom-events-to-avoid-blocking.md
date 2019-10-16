---
title: '방법: (Visual Basic)를 차단 하지 않도록 사용자 지정 이벤트 선언'
ms.date: 07/20/2015
helpviewer_keywords:
- declaring events [Visual Basic], custom
- events [Visual Basic], custom
- custom events [Visual Basic]
ms.assetid: 998b6a90-67c5-4d2c-8b11-366d3e355505
ms.openlocfilehash: 6eea47ea2c8aee697eb34ca904dad22ca88e6ce4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051899"
---
# <a name="how-to-declare-custom-events-to-avoid-blocking-visual-basic"></a>방법: (Visual Basic)를 차단 하지 않도록 사용자 지정 이벤트 선언
이 하나의 이벤트 처리기는 후속 이벤트 처리기를 차단 하지 중요 한 몇 가지 경우가 있습니다. 사용자 지정 이벤트의 이벤트 처리기를 비동기적으로 호출 하도록 이벤트를 허용 합니다.  
  
 이벤트 선언에 대 한 백업 저장소 필드는 기본적으로 모든 이벤트 처리기를 순차적으로 결합 하는 멀티 캐스트 대리자는 합니다. 이 완료 한 처리기를 사용 하는 오래 걸리는 경우 차단할 다른 처리기 완료 될 때까지 것을 의미 합니다. (때 이벤트 처리기 긴 또는 차단 작업 수행 해야 합니다.)  
  
 Visual Basic에서 제공 하는 이벤트의 기본 구현을 사용 하는 대신 이벤트 처리기를 비동기적으로 실행 하는 사용자 지정 이벤트를 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 `AddHandler` 의 각 처리기에 대 한 대리자를 추가 하는 접근자를 `Click` 이벤트를는 <xref:System.Collections.ArrayList> 에 저장 된는 `EventHandlerList` 필드.  
  
 발생 경우 코드를 `Click` 이벤트를 `RaiseEvent` 비동기적으로 사용 하 여 모든 이벤트 처리기 대리자를 호출 하는 접근자를 <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A> 메서드. 해당 메서드는 작업자 스레드에서 각 처리기를 호출 하 고 즉시 반환 하므로 처리기 서로 차단할 수 없습니다.  
  
 [!code-vb[VbVbalrEvents#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#27)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Collections.ArrayList>
- <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>
- [이벤트](../../../../visual-basic/programming-guide/language-features/events/index.md)
- [방법: 메모리를 절약하는 사용자 지정 이벤트 선언](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)
