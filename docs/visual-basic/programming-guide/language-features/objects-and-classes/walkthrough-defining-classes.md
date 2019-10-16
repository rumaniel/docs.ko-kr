---
title: 클래스 정의 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- execution [Visual Basic], ending
- objects [Visual Basic], initializing
- Initialize event [Visual Basic]
- files [Visual Basic], closing
- programs [Visual Basic], quitting
- code, exiting
- objects [Visual Basic], creating
- program termination
- classes [Visual Basic], walkthroughs
- class modules, walkthroughs
- Terminate event [Visual Basic]
- execution [Visual Basic], stopping
ms.assetid: 07018828-2d49-4cf5-a44b-19fb15d9efea
ms.openlocfilehash: 679f4fd55f142c2c4bb63a556feb95c074960b12
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914727"
---
# <a name="walkthrough-defining-classes-visual-basic"></a>연습: 클래스 정의 (Visual Basic)

이 연습에서는 클래스를 정의 하는 방법을 보여 줍니다 .이 클래스를 사용 하 여 개체를 만들 수 있습니다. 또한 새 클래스에 속성 및 메서드를 추가 하는 방법과 개체를 초기화 하는 방법을 보여 줍니다.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-define-a-class"></a>클래스를 정의 하려면
  
1. **파일** 메뉴에서 **새 프로젝트** 를 클릭 하 여 프로젝트를 만듭니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
2. Visual Basic 프로젝트 템플릿 목록에서 Windows 응용 프로그램을 선택 하 여 새 프로젝트를 표시 합니다.  
  
3. **프로젝트** 메뉴에서 **클래스 추가** 를 클릭 하 여 프로젝트에 새 클래스를 추가 합니다. **새 항목 추가** 대화 상자가 나타납니다.  
  
4. **클래스** 템플릿을 선택 합니다.  
  
5. 새 `UserNameInfo.vb`클래스의 이름을로 지정한 다음 **추가** 를 클릭 하 여 새 클래스에 대 한 코드를 표시 합니다.  
  
     [!code-vb[VbVbalrOOP#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#5)]
  
    > [!NOTE]
    > Visual Basic **코드 편집기** 를 사용 하 여 `Class` 키워드와 새 클래스의 이름을 차례로 입력 하 여 시작 폼에 클래스를 추가할 수 있습니다. **코드 편집기** 는 해당 `End Class` 문을 제공 합니다.  
  
6. 문과 `Class` `End Class` 문 사이에 다음 코드를 추가 하 여 클래스에 대 한 전용 필드를 정의 합니다.  
  
     [!code-vb[VbVbalrOOP#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#7)]
  
     필드를로 `Private` 선언 하는 것은 클래스 내 에서만 사용할 수 있음을 의미 합니다. 보다 많은 액세스 권한을 제공 하는와 `Public` 같은 액세스 한정자를 사용 하 여 클래스 외부에서 필드를 사용할 수 있도록 설정할 수 있습니다. 자세한 내용은 [Visual Basic의 액세스 수준](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조 하세요.  
  
7. 다음 코드를 추가 하 여 클래스에 대 한 속성을 정의 합니다.  
  
     [!code-vb[VbVbalrOOP#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#8)]
  
8. 다음 코드를 추가 하 여 클래스에 대 한 메서드를 정의 합니다.  
  
     [!code-vb[VbVbalrOOP#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#9)]
  
9. 이라는 `Sub New`프로시저를 추가 하 여 새 클래스에 대 한 매개 변수가 있는 생성자를 정의 합니다.  
  
     [!code-vb[VbVbalrOOP#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#10)]
  
     생성자 `Sub New` 는이 클래스를 기반으로 하는 개체를 만들 때 자동으로 호출 됩니다. 이 생성자는 사용자 이름을 포함 하는 필드의 값을 설정 합니다.  
  
## <a name="to-create-a-button-to-test-the-class"></a>클래스를 테스트 하는 단추를 만들려면
  
1. **솔루션 탐색기** 에서 해당 이름을 마우스 오른쪽 단추로 클릭 한 다음 **디자이너 보기**를 클릭 하 여 시작 폼을 디자인 모드로 변경 합니다. 기본적으로 Windows 응용 프로그램 프로젝트의 시작 폼에는 form1.vb 라는 이름이 지정 됩니다. 그러면 기본 폼이 표시 됩니다.  
  
2. 기본 폼에 단추를 추가 하 고 두 번 클릭 하 여 `Button1_Click` 이벤트 처리기에 대 한 코드를 표시 합니다. 다음 코드를 추가 하 여 테스트 프로시저를 호출 합니다.  
  
     [!code-vb[VbVbalrOOP#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#12)]
  
## <a name="to-run-your-application"></a>애플리케이션을 실행하려면
  
1. F5 키를 눌러 응용 프로그램을 실행 합니다. 폼의 단추를 클릭 하 여 테스트 프로시저를 호출 합니다. 프로시저에서 개체의 `UserName` `Capitalize` 메서드를 호출 했기 때문에 원래는 "일, 강현수" 이라는 메시지를 표시 합니다.  
  
2. **확인**을 클릭하여 메시지 상자를 닫습니다. 이 `Button1 Click` 프로시저는 `UserName` 속성의 값을 변경 하 고의 `UserName` 새 값이 "worden, Joe" 라는 메시지를 표시 합니다.  
  
## <a name="see-also"></a>참고자료

- [개체 지향 프로그래밍(Visual Basic)](../../concepts/object-oriented-programming.md)
- [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
