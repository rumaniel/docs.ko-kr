---
title: '방법: Visual Basic에서 예외 기록'
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, logging
- exceptions, tracking
ms.assetid: a26c60e2-ae39-444a-aebb-33eccadc0eeb
ms.openlocfilehash: 53bf93a326123ddb1e26ef5964fa057148505116
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59307225"
---
# <a name="how-to-log-exceptions-in-visual-basic"></a>방법: Visual Basic에서 예외 기록
`My.Application.Log` 및 `My.Log` 개체를 사용하여 애플리케이션에서 발생하는 예외에 대한 정보를 기록할 수 있습니다. 이 예제에서는 `My.Application.Log.WriteException` 메서드를 사용하여 명시적으로 catch하는 예외 및 처리되지 않은 예외를 기록하는 방법을 보여 줍니다.  
  
 추적 정보를 기록하려면 `My.Application.Log.WriteEntry` 메서드를 사용합니다. 자세한 내용은 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>을 참조하세요.  
  
### <a name="to-log-a-handled-exception"></a>처리된 예외를 기록하려면  
  
1. 예외 정보를 생성하는 메서드를 만듭니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#9)]  
  
2. `Try...Catch` 블록을 사용하여 예외를 catch합니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#6)]  
  
3. 예외를 생성할 수 있는 코드를 `Try` 블록에 넣습니다.  
  
     `Dim` 및 `MsgBox` 줄의 주석 처리를 제거하여 <xref:System.NullReferenceException> 예외를 발생시킵니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#7)]  
  
4. `Catch` 블록에서 `My.Application.Log.WriteException` 메서드를 사용하여 예외 정보를 씁니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#8)]  
  
     다음 예제에서는 처리된 예외를 기록하기 위한 전체 코드를 보여 줍니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#10)]  
  
### <a name="to-log-an-unhandled-exception"></a>처리되지 않은 예외를 기록하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 선택합니다.  
  
2. **애플리케이션** 탭을 클릭합니다.  
  
3. **애플리케이션 이벤트 보기** 단추를 클릭하여 코드 편집기를 엽니다.  
  
     그러면 ApplicationEvents.vb 파일이 열립니다.  
  
4. 코드 편집기에서 ApplicationEvents.vb 파일을 엽니다. **일반** 메뉴에서 **MyApplication 이벤트**를 선택합니다.  
  
5. **선언** 메뉴에서 **UnhandledException**을 선택합니다.  
  
     주 애플리케이션이 실행되기 전에 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 이벤트가 발생합니다.  
  
6. `My.Application.Log.WriteException` 이벤트 처리기에 `UnhandledException` 메서드를 추가합니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#4)]  
  
     다음 예제에서는 처리되지 않은 예외를 기록하기 위한 전체 코드를 보여 줍니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#5)]  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [애플리케이션 로그 작업](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [방법: 로그 메시지 쓰기](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)
- [연습: My.Application.Log가 정보를 기록하는 위치 확인](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
- [연습: My.Application.Log가 정보를 기록하는 위치 변경](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)
