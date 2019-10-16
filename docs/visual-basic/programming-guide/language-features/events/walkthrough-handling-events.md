---
title: 이벤트 처리 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- event handling [Visual Basic], walkthroughs
- walkthroughs [Visual Basic], event handling
- variables [Visual Basic], WithEvents
- events [Visual Basic], walkthroughs
- WithEvents keyword [Visual Basic], walkthroughs
- event handlers [Visual Basic], walkthroughs
ms.assetid: f145b3fc-5ae0-4509-a2aa-1ff6934706bd
ms.openlocfilehash: 12267e0a70419298bc581421c4f3a220088d205f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956305"
---
# <a name="walkthrough-handling-events-visual-basic"></a>연습: 이벤트 처리 (Visual Basic)
이벤트를 사용 하는 방법을 보여 주는 두 항목 중 두 번째 항목입니다. 첫 번째 항목인 [연습: 이벤트](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)선언 및 발생에서는 이벤트를 선언 하 고 발생 시키는 방법을 보여 줍니다. 이 단원에서는 해당 연습의 폼과 클래스를 사용 하 여 이벤트를 처리 하는 방법을 보여 줍니다.  
  
 `Widget` 클래스 예제에서는 기존의 이벤트 처리 문을 사용 합니다. Visual Basic는 이벤트를 사용 하는 다른 기술을 제공 합니다. 연습으로이 예제를 수정 하 여 `AddHandler` 및 `Handles` 문을 사용할 수 있습니다.  
  
### <a name="to-handle-the-percentdone-event-of-the-widget-class"></a>Widget 클래스의 PercentDone 이벤트를 처리 하려면  
  
1. 에 `Form1`다음 코드를 추가 합니다.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#4)]  
  
     키워드는 변수 `mWidget` 를 사용 하 여 개체의 이벤트를 처리 하도록 지정 합니다. `WithEvents` 개체를 만들 클래스의 이름을 제공 하 여 개체의 종류를 지정 합니다.  
  
     변수는 클래스 수준 이어야 `Form1` 하므로 `WithEvents` 에서 선언 됩니다.`mWidget` 이는 위치를 지정 하는 클래스의 형식에 관계 없이 적용 됩니다.  
  
     변수 `mblnCancel` 는 `LongTask` 메서드를 취소 하는 데 사용 됩니다.  
  
## <a name="writing-code-to-handle-an-event"></a>이벤트를 처리 하는 코드 작성  
 를 사용 하 여 `WithEvents`변수를 선언 하는 즉시 변수 이름이 클래스 **코드 편집기**의 왼쪽 드롭다운 목록에 나타납니다. 를 선택 `mWidget`하면 클래스의이벤트가오른쪽드롭다운목록에표시됩니다.`Widget` 이벤트를 선택 하면 접두사 `mWidget` 와 밑줄을 사용 하 여 해당 이벤트 프로시저가 표시 됩니다. `WithEvents` 변수와 연결 된 모든 이벤트 프로시저에는 변수 이름이 접두사로 지정 됩니다.  
  
#### <a name="to-handle-an-event"></a>이벤트를 처리 하려면  
  
1. `mWidget` **코드 편집기**의 왼쪽 드롭다운 목록에서 선택 합니다.  
  
2. 오른쪽 드롭다운 `PercentDone` 목록에서 이벤트를 선택 합니다. **코드 편집기** 가 이벤트 프로시저 `mWidget_PercentDone` 를 엽니다.  
  
    > [!NOTE]
    > **코드 편집기** 는 새 이벤트 처리기를 삽입 하는 데 유용 하지만 필수는 아닙니다. 이 연습에서는 이벤트 처리기를 코드에 직접 복사 하는 것이 더 직접적입니다.  
  
3. 다음 코드를 `mWidget_PercentDone` 이벤트 처리기에 추가합니다.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#5)]  
  
     이벤트가 발생할 때마다 이벤트 프로시저는 `Label` 컨트롤에 완료율을 표시 합니다. `PercentDone` 메서드를 사용 하면 레이블을 다시 그릴 수 있으며 사용자에 게 취소 단추를 클릭할 수 있는 기회가 제공 됩니다. `DoEvents`  
  
4. `Button2_Click` 이벤트 처리기에 대 한 다음 코드를 추가 합니다.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#6)]  
  
 을 실행 `LongTask`하는 동안 사용자가 취소 단추를 클릭 하면 이벤트 처리가 발생 하는 것이 `DoEvents` 문에 의해 즉시 실행 됩니다. `Button2_Click` 클래스 수준 변수 `mblnCancel` 는 `True`로 `True`설정 되 고, 이벤트는 `mWidget_PercentDone` 이를 테스트 하 고 `ByRef Cancel` 인수를로 설정 합니다.  
  
## <a name="connecting-a-withevents-variable-to-an-object"></a>WithEvents 변수를 개체에 연결  
 `Form1`이제를 설정 하 여 `Widget` 개체의 이벤트를 처리 합니다. 모든 `Widget` 위치를 찾는 것은입니다.  
  
 디자인 타임에 변수 `WithEvents` 를 선언 하면 개체가 연결 되지 않습니다. 변수 `WithEvents` 는 다른 개체 변수와 동일 합니다. 개체를 만들고 `WithEvents` 변수를 사용 하 여 개체에 대 한 참조를 할당 해야 합니다.  
  
#### <a name="to-create-an-object-and-assign-a-reference-to-it"></a>개체를 만들고이 개체에 대 한 참조를 할당 하려면  
  
1. **코드 편집기**의 왼쪽 드롭다운 목록에서 **(Form1 이벤트)** 를 선택 합니다.  
  
2. 오른쪽 드롭다운 `Load` 목록에서 이벤트를 선택 합니다. **코드 편집기** 가 이벤트 프로시저 `Form1_Load` 를 엽니다.  
  
3. `Form1_Load` 이벤트 프로시저에 대 한 다음 코드를 추가 하 여 `Widget`를 만듭니다.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#7)]  
  
 이 코드가 실행 되 면 Visual Basic `Widget` 개체를 만들고 해당 이벤트를와 `mWidget`연결 된 이벤트 프로시저에 연결 합니다. 이 시점부터가 `Widget` `PercentDone` 이벤트를 `mWidget_PercentDone` 발생 시킬 때마다 이벤트 프로시저가 실행 됩니다.  
  
#### <a name="to-call-the-longtask-method"></a>LongTask 메서드를 호출 하려면  
  
- 다음 코드를 `Button1_Click` 이벤트 처리기에 추가합니다.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#8)]  
  
 메서드를 호출 하기 전에 완료율을 표시 하는 레이블이 초기화 되어야 하 고 메서드를 취소 하기 위한 클래스 수준 `Boolean` 플래그가로 `False`설정 되어야 합니다. `LongTask`  
  
 `LongTask`는 작업 기간 12.2 초를 사용 하 여 호출 됩니다. 이벤트 `PercentDone` 는 1 초 마다 한 번씩 발생 합니다. 이벤트가 발생할 `mWidget_PercentDone` 때마다 이벤트 프로시저가 실행 됩니다.  
  
 이 `LongTask` `LongTask` `mblnCancel` 완료되`True`면가 정상적으로 종료 되었는지 여부를 확인 하거나가로 설정 되어 있기 때문에 중지 된경우를테스트합니다.`mblnCancel` 완료율은 이전 경우에만 업데이트 됩니다.  
  
#### <a name="to-run-the-program"></a>프로그램을 실행하려면  
  
1. F5 키를 눌러 프로젝트를 실행 모드로 전환 합니다.  
  
2. **작업 시작** 단추를 클릭 합니다. `PercentDone` 이벤트가 발생할 때마다 레이블이 완료 된 작업의 백분율을 사용 하 여 업데이트 됩니다.  
  
3. 작업을 중지 하려면 **취소** 단추를 클릭 합니다. 클릭 하면 **취소** 단추의 모양이 즉시 변경 되지 않습니다. 이 `Click` 이벤트는 `My.Application.DoEvents` 문에서 이벤트를 처리할 수 있을 때까지 발생 하지 않습니다.  
  
    > [!NOTE]
    > `My.Application.DoEvents` 메서드 이벤트를 처리 하지 동일한 방식으로 폼 마찬가지로 합니다. 예를 들어이 연습에서는 **취소** 단추를 두 번 클릭 해야 합니다. 폼에서 이벤트를 직접 처리할 수 있도록 하려면 다중 스레딩을 사용할 수 있습니다. 자세한 내용은 [관리 되는 스레딩](../../../../standard/threading/index.md)을 참조 하세요.
  
 F11 키를 사용 하 여 프로그램을 실행 하 고 한 번에 한 줄씩 코드를 단계별로 실행 하는 것을 확인할 수 있습니다. 실행 `LongTask`방법을 명확 하 게 확인 한 다음 `PercentDone` 이벤트가 발생 될 때마다 잠시 다시 `Form1` 입력 하면 됩니다.  
  
 실행이 `Form1`다시 실행 `LongTask` 되는 동안 메서드가 다시 호출 된 경우에는 어떻게 되나요? 최악의 경우 이벤트가 발생 될 때마다가 호출 되 `LongTask` 면 스택 오버플로가 발생할 수 있습니다.  
  
 새 `mWidget` `Widget` `mWidget`에 대 한 참조를에 할당 하 여 변수가 다른 개체에 대 한 이벤트를 처리할 수 있습니다. `Widget` 실제로 단추를 클릭할 때마다에서 `Button1_Click` 코드를 수행할 수 있습니다.  
  
#### <a name="to-handle-events-for-a-different-widget"></a>다른 위젯의 이벤트를 처리 하려면  
  
- `Button1_Click` 프로시저에 다음 코드 줄을 추가 하 여를 읽는 `mWidget.LongTask(12.2, 0.33)`줄 바로 앞에 추가 합니다.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#9)]  
  
 위의 코드는 단추를 클릭할 `Widget` 때마다 새를 만듭니다. `LongTask` 메서드가 완료 되는 즉시에 `Widget` 대 한 참조가 해제 되 고 `Widget` 이 제거 됩니다.  
  
 변수 `WithEvents` 는 한 번에 하나의 개체 참조만 포함할 수 있으므로 다른 `Widget` 개체를에 할당 하는 경우 `mWidget`에는 이전 `Widget` 개체의 이벤트가 더 이상 처리 되지 않습니다. 가 `mWidget` 이전`Widget`에 대 한 참조를 포함 하는 유일한 개체 변수인 경우 개체가 제거 됩니다. 여러 `Widget` 개체의 이벤트를 처리 하려면 `AddHandler` 문을 사용 하 여 각 개체의 이벤트를 개별적으로 처리 합니다.  
  
> [!NOTE]
> 필요한 만큼의 `WithEvents` 변수를 선언할 수 있지만 `WithEvents` 변수 배열은 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [연습: 이벤트 선언 및 발생](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)
- [이벤트](../../../../visual-basic/programming-guide/language-features/events/index.md)
