---
title: '방법: (Visual Basic) 값을 반환 하지 않는 프로시저 호출'
ms.date: 07/20/2015
helpviewer_keywords:
- procedure calls [Visual Basic], returning values
- Visual Basic code, procedures
- procedures [Visual Basic], calling
ms.assetid: 259b49a3-a3c1-4254-ba8c-73cdc4127703
ms.openlocfilehash: 6e3ce2a184ca5411a6a016929a16bf3d67e669ca
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61864236"
---
# <a name="how-to-call-a-procedure-that-does-not-return-a-value-visual-basic"></a>방법: (Visual Basic) 값을 반환 하지 않는 프로시저 호출
`Sub` 프로시저가 호출 코드에 값을 반환 하지 않습니다. 호출 명시적으로 독립 실행형 호출 문을 사용 하 여 합니다. 식 내에서 해당 이름을 사용 하 여 호출할 수 없습니다.  
  
### <a name="to-call-a-sub-procedure"></a>Sub 프로시저를 호출 하려면  
  
1. 이름을 지정 합니다 `Sub` 프로시저입니다.  
  
2. 괄호로 묶어 인수 목록에 프로시저 이름 뒤에. 인수가 없는 경우에 필요에 따라 괄호를 생략할 수 있습니다. 그러나 괄호를 사용 하 여 쉽게 코드 읽을 수 있습니다.  
  
3. 쉼표로 구분 하 여 괄호 안에 인수 목록의 인수를 배치 합니다. 같은 순서로 인수를 지정 해야 하는 `Sub` 프로시저는 해당 매개 변수를 정의 합니다.  
  
     다음 예제에서는 Visual Basic <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> 응용 프로그램 창을 활성화 하는 함수입니다. <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> 창 제목이 유일한 인수로 변수로 사용 합니다. 호출 코드에 값을 반환 하지 않습니다. 이 예제에서는 throw Notepad 프로세스를 실행 하지 않는 경우는 <xref:System.ArgumentException>합니다. `Shell` 절차에서는 응용 프로그램을 지정 된 경로 가정 합니다.  
  
     [!code-vb[VbVbalrCatRef#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCatRef/VB/Class1.vb#11)]  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Interaction.Shell%2A>
- <xref:System.ArgumentException>
- [절차](./index.md)
- [Sub 프로시저](./sub-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Sub 문](../../../../visual-basic/language-reference/statements/sub-statement.md)
- [방법: 프로시저 만들기](./how-to-create-a-procedure.md)
- [방법: 값을 반환 하는 프로시저 호출](./how-to-call-a-procedure-that-returns-a-value.md)
- [방법: Visual Basic의 이벤트 처리기를 호출 합니다.](./how-to-call-an-event-handler.md)
