---
title: 이벤트(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- events [Visual Basic], about events
- events [Visual Basic]
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
ms.openlocfilehash: 65b4f5633e589ae02e9ed495074000181864428a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956366"
---
# <a name="events-visual-basic"></a>이벤트(Visual Basic)
Visual Studio 프로젝트를 순서 대로 실행 되는 일련의 프로시저로 시각화할 수도 있지만 실제로 대부분의 프로그램은 이벤트 구동 방식입니다. 즉, 실행 흐름이 *이벤트*라는 외부 발생에 의해 결정 됩니다.  
  
 이벤트는 중요한 문제가 발생했음을 애플리케이션에 알리는 신호입니다. 예를 들어 사용자가 폼의 컨트롤을 클릭하면 폼이 `Click` 이벤트를 발생시키고 이벤트를 처리하는 프로시저를 호출할 수 있습니다. 또한 이벤트는 개별 작업이 통신할 수 있도록 합니다. 예를 들어 애플리케이션이 주 애플리케이션과는 별도로 정렬 작업을 수행한다고 가정해 봅니다. 사용자가 정렬을 취소하면 애플리케이션은 정렬 프로세스를 중지하도록 지시하는 취소 이벤트를 전송할 수 있습니다.  
  
## <a name="event-terms-and-concepts"></a>이벤트 용어 및 개념  
 이 섹션에서는 Visual Basic 이벤트에 사용 되는 용어 및 개념에 대해 설명 합니다.  
  
### <a name="declaring-events"></a>이벤트 선언  
 다음 예제와 같이 `Event` 키워드를 사용하여 클래스, 구조체, 모듈 및 인터페이스를 사용하여 이벤트를 선언합니다.  
  
 [!code-vb[VbVbalrEvents#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#24)]  
  
### <a name="raising-events"></a>이벤트 발생  
 이벤트는 중요한 문제가 발생했음을 알리는 메시지와 같습니다. 메시지를 브로드캐스트하는 동작을 이벤트 *발생*이라고 합니다. Visual Basic에서 다음 예제와 같이 `RaiseEvent` 문을 사용 하 여 이벤트를 발생 시킵니다.  
  
 [!code-vb[VbVbalrEvents#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#25)]  
  
 선언된 클래스, 모듈 또는 구조체의 범위 내에서 이벤트가 발생되어야 합니다. 예를 들어 파생 클래스는 기본 클래스에서 상속된 이벤트를 발생시킬 수 없습니다.  
  
### <a name="event-senders"></a>이벤트 전송자  
 이벤트를 발생시킬 수 있는 개체는 *이벤트 소스*라고도 하는 *이벤트 전송자*입니다. 폼, 컨트롤 및 사용자 정의 개체는 이벤트 전송자에 속합니다.  
  
### <a name="event-handlers"></a>이벤트 처리기  
 *이벤트 처리기*는 해당 이벤트가 발생할 때 호출되는 프로시저입니다. 서명이 일치하는 모든 유효한 서브루틴을 이벤트 처리기로 사용할 수 있습니다. 그러나 함수는 이벤트 처리기로 사용할 수 없습니다. 이벤트 소스에 값을 반환할 수 없기 때문입니다.  
  
 Visual Basic는 이벤트 보낸 사람의 이름, 밑줄 및 이벤트 이름을 결합 하는 이벤트 처리기에 표준 명명 규칙을 사용 합니다. 예를 들어 `button1`이라는 단추의 `Click` 이벤트의 이름은 `Sub button1_Click`으로 지정됩니다.  
  
> [!NOTE]
> 사용자 고유의 이벤트에 대해 이벤트 처리기를 정의하는 경우 이러한 명명 규칙을 사용하는 것이 좋지만 필수는 아닙니다. 유효한 어떤 서브루틴 이름도 사용 가능합니다.  
  
## <a name="associating-events-with-event-handlers"></a>이벤트를 이벤트 처리기에 연결  
 이벤트 처리기를 사용하려면 먼저 `Handles` 또는 `AddHandler` 문을 사용하여 이벤트 처리기를 이벤트에 연결해야 합니다.  
  
### <a name="withevents-and-the-handles-clause"></a>WithEvents 및 Handles 절  
 `WithEvents` 문 및 `Handles` 절은 이벤트 처리기를 지정하는 선언적 방법을 제공합니다. `WithEvents` 키워드로 선언된 개체에 의해 발생된 이벤트는 다음 그림과 같이 해당 이벤트에 대한 `Handles` 문을 사용하는 모든 프로시저에 의해 처리될 수 있습니다.  
  
 [!code-vb[VbVbalrEvents#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#1)]  
  
 `WithEvents` 문 및 `Handles` 절은 선언적 구문을 사용하여 이벤트 처리를 보다 쉽게 코딩하고 읽고 디버그할 수 있도록 하므로 이벤트 처리기에 가장 적합합니다. 그러나 `WithEvents` 변수를 사용할 때는 다음과 같은 제한 사항이 적용됩니다.  
  
- `WithEvents` 변수를 개체 변수로 사용할 수 없습니다. 즉, `Object`로 선언할 수 없습니다. 따라서 변수를 선언할 때는 클래스 이름을 지정해야 합니다.  
  
- 공유 이벤트는 클래스 인스턴스에 연결 되지 않으므로를 사용 `WithEvents` 하 여 shared 이벤트를 선언적으로 처리할 수 없습니다. 마찬가지로 `WithEvents` 또는 `Handles`를 사용하여 `Structure`의 이벤트를 처리할 수 없습니다. 두 경우 모두 `AddHandler` 문을 사용해서 해당 이벤트를 처리할 수 있습니다.  
  
- `WithEvents` 변수 배열을 만들 수 없습니다.  
  
 `WithEvents` 변수는 단일 이벤트 처리기로 하나 이상의 이벤트 종류를 처리하거나, 하나 이상의 이벤트 처리기로 동일한 종류의 이벤트를 처리하도록 할 수 있습니다.  
  
 `Handles` 절은 이벤트를 이벤트 처리기와 연결하는 표준 방법이지만 컴파일 타임에 이벤트를 이벤트 처리기와 연결하도록 제한됩니다.  
  
 양식이 나 컨트롤과 연결 된 이벤트와 같은 일부 경우에는 빈 이벤트 처리기를 자동으로 스텁 하 여 이벤트에 연결 Visual Basic. 예를 들어 디자인 모드에서 폼의 명령 단추를 두 번 클릭 하면 다음 코드와 같이 명령 단추에 대해 빈 이벤트 처리기 `WithEvents` 와 변수를 Visual Basic 만듭니다.  
  
 [!code-vb[VbVbalrEvents#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#26)]  
  
### <a name="addhandler-and-removehandler"></a>AddHandler 및 RemoveHandler  
 `AddHandler` 문은 둘 다 이벤트 처리기를 지정할 수 있다는 측면에서 `Handles` 절과 비슷합니다. 그러나 `AddHandler`를 `RemoveHandler`와 함께 사용하면 `Handles` 절보다 유연성이 높아져서 이벤트와 연결된 이벤트 처리기를 동적으로 추가, 제거 및 변경할 수 있습니다. 공유 이벤트 또는 구조체의 이벤트를 처리하려는 경우 `AddHandler`를 사용해야 합니다.  
  
 `AddHandler`는 두 개의 인수, 즉 컨트롤과 같은 이벤트 전송자의 이벤트 이름과 대리자로 평가되는 식을 사용합니다. `AddressOf` 문은 항상 대리자에 대한 참조를 반환하므로 `AddHandler`를 사용할 경우 대리자 클래스를 명시적으로 지정할 필요가 없습니다. 다음 예제에서는 개체에 의해 발생하는 이벤트와 이벤트 처리기를 연결합니다.  
  
 [!code-vb[VbVbalrEvents#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#28)]  
  
 이벤트 처리기에서 이벤트의 연결을 끊는 `RemoveHandler`는 `AddHandler`와 동일한 구문을 사용합니다. 예를 들어:  
  
 [!code-vb[VbVbalrEvents#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#29)]  
  
 다음 예제에서 이벤트 처리기는 이벤트와 연결되고 이벤트가 발생합니다. 이벤트 처리기는 이벤트를 catch하고 메시지를 표시합니다.  
  
 그런 다음 첫 번째 이벤트 처리기가 제거되고 다른 이벤트 처리기가 이벤트와 연결됩니다. 이벤트가 다시 발생하면 다른 메시지가 표시됩니다.  
  
 마지막으로 두 번째 이벤트 처리기가 제거되고 세 번째로 해당 이벤트가 발생합니다. 해당 이벤트와 연결된 이벤트 처리기가 더 이상 없으므로 아무 작업도 수행되지 않습니다.  
  
 [!code-vb[VbVbalrEvents#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class2.vb#38)]  
  
## <a name="handling-events-inherited-from-a-base-class"></a>기본 클래스에서 상속된 이벤트 처리  
 기본 클래스에서 특성을 상속하는 클래스인 *파생 클래스*는 `Handles MyBase` 문을 사용하여 기본 클래스에 의해 발생된 이벤트를 처리할 수 있습니다.  
  
### <a name="to-handle-events-from-a-base-class"></a>기본 클래스의 이벤트를 처리하려면  
  
- 이벤트 처리기 프로시저의 선언 줄에 `Handles MyBase.`*eventname* 문을 추가하여 파생 클래스에서 이벤트 처리기를 선언합니다. 여기서 *eventname*은 처리하는 기본 클래스의 이벤트 이름입니다. 예를 들어:  
  
     [!code-vb[VbVbalrEvents#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#12)]  
  
## <a name="related-sections"></a>관련 단원  
  
|제목|설명|  
|-----------|-----------------|  
|[연습: 이벤트 선언 및 발생](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)|클래스의 이벤트를 선언하고 발생시키는 방법에 대한 단계별 설명을 제공합니다.|  
|[연습: 이벤트 처리](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)|이벤트 처리기 프로시저를 작성하는 방법을 보여 줍니다.|  
|[방법: 차단을 방지 하기 위해 사용자 지정 이벤트 선언](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)|이벤트 처리기를 비동기적으로 호출할 수 있는 사용자 지정 이벤트를 정의하는 방법을 보여 줍니다.|  
|[방법: 메모리를 절약하는 사용자 지정 이벤트 선언](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)|이벤트가 처리될 때만 메모리를 사용하는 사용자 지정 이벤트를 정의하는 방법을 보여 줍니다.|  
|[Visual Basic에서 상속된 이벤트 처리기 관련 문제 해결](../../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)|상속된 구성 요소의 이벤트 처리기에서 발생하는 일반적인 문제에 대해 설명합니다.|  
|[이벤트](../../../../standard/events/index.md)|.NET Framework의 이벤트 모델 개요를 제공합니다.|  
|[Windows Forms에서 이벤트 처리기 만들기](../../../../framework/winforms/creating-event-handlers-in-windows-forms.md)|Windows Forms 개체와 관련된 이벤트로 작업하는 방법을 설명합니다.|  
|[대리자](../../../../visual-basic/programming-guide/language-features/delegates/index.md)|Visual Basic의 대리자에 대해 간략하게 설명합니다.|
