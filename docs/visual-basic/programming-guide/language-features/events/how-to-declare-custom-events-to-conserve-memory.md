---
title: '방법: (Visual Basic) 메모리를 절약 하는 사용자 지정 이벤트 선언'
ms.date: 07/20/2015
helpviewer_keywords:
- declaring events [Visual Basic], custom
- events [Visual Basic], custom
- custom events [Visual Basic]
ms.assetid: 87ebee87-260c-462f-979c-407874debd19
ms.openlocfilehash: e4132f51f4dd85ad964042d05f7c5bc0a2e6e3cd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61973162"
---
# <a name="how-to-declare-custom-events-to-conserve-memory-visual-basic"></a>방법: (Visual Basic) 메모리를 절약 하는 사용자 지정 이벤트 선언
이 응용 프로그램의 메모리 사용량을 낮게 유지 하는 중요 한 몇 가지 경우가 있습니다. 사용자 지정 이벤트를 처리 하는 이벤트에 대해서만 메모리를 사용 하도록 응용 프로그램을 허용 합니다.  
  
 기본적으로 컴파일러는 클래스에서 이벤트를 선언 이벤트 정보를 저장 하는 필드에 대 한 메모리를 할당 합니다. 클래스를 사용 하지 않는 이벤트 수 있으면 메모리를 불필요 하 게 수행 합니다.  
  
 Visual Basic에서 제공 하는 이벤트의 기본 구현을 사용 하는 대신 메모리 사용량을 신중 하 게 관리 사용자 지정 이벤트를 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 클래스의 인스턴스 하나를 사용 합니다 <xref:System.ComponentModel.EventHandlerList> 에 저장 된 클래스는 `Events` 사용에서 이벤트에 대 한 정보를 저장할 필드. <xref:System.ComponentModel.EventHandlerList> 클래스는 대리자를 포함 하도록 디자인 된 최적화 된 목록 클래스입니다.  
  
 클래스 사용의 모든 이벤트는 `Events` 각 이벤트를 처리 하는 방법을 추적 하는 필드입니다.  
  
 [!code-vb[VbVbalrEvents#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#22)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ComponentModel.EventHandlerList>
- [이벤트](../../../../visual-basic/programming-guide/language-features/events/index.md)
- [방법: 차단을 방지 하는 사용자 지정 이벤트 선언](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)
