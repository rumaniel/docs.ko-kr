---
title: 인터페이스 만들기 및 구현 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [Visual Basic], walkthroughs
- interfaces [Visual Basic], testing
- interface implementation [Visual Basic], walkthrough
- interfaces [Visual Basic], creating
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
ms.openlocfilehash: 62e301e9eb366d14b58088d3e2cda3b567d17f5b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923315"
---
# <a name="walkthrough-creating-and-implementing-interfaces-visual-basic"></a>연습: 인터페이스 만들기 및 구현 (Visual Basic)

인터페이스는 속성, 메서드 및 이벤트의 특성을 설명 하지만, 구현 세부 정보는 구조체 또는 클래스까지 그대로 둡니다.  
  
 이 연습에서는 인터페이스를 선언 하 고 구현 하는 방법을 보여 줍니다.  
  
> [!NOTE]
> 이 연습에서는 사용자 인터페이스를 만드는 방법에 대 한 정보를 제공 하지 않습니다.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-define-an-interface"></a>인터페이스를 정의 하려면
  
1. 새 Visual Basic Windows 애플리케이션 프로젝트를 엽니다.  
  
2. **프로젝트** 메뉴에서 **모듈 추가** 를 클릭 하 여 프로젝트에 새 모듈을 추가 합니다.  
  
3. 새 모듈 `Module1.vb` 의 이름을로 하 고 **추가**를 클릭 합니다. 새 모듈의 코드가 표시 됩니다.  
  
4. `TestInterface` `Module1` `Interface TestInterface` 및 문`End Module` 사이에를 입력 하 고 enter 키를 눌러 내에 명명 된 인터페이스를 정의 합니다. `Module` **코드 편집기** 는 `Interface` `End Interface` 키워드를 들여쓰기 하 고 문을 추가 하 여 코드 블록을 구성 합니다.  
  
5. `Interface` 및`End Interface` 문 사이에 다음 코드를 배치 하 여 인터페이스에 대 한 속성, 메서드 및 이벤트를 정의 합니다.  
  
     [!code-vb[VbVbalrOOP#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#98)]
  
## <a name="implementation"></a>구현

 인터페이스 멤버를 선언 하는 데 사용 되는 구문은 클래스 멤버를 선언 하는 데 사용 되는 구문과 다릅니다. 이러한 차이는 인터페이스에 구현 코드가 포함 될 수 없다는 사실을 반영 합니다.  
  
### <a name="to-implement-the-interface"></a>인터페이스를 구현 하려면
  
1. `End Interface` 문 `Module1` `ImplementationClass` 뒤에문뒤에다음문을추가하여라는클래스를추가하고enter키를누릅니다.`End Module`  
  
     [!code-vb[VbVbalrOOP#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#99)]
  
     통합 개발 환경 내에서 작업 하는 경우 enter 키를 누르면 **코드 편집기** 에서 `End Class` 일치 하는 문을 제공 합니다.  
  
2. 클래스에서 구현 `Implements` 하는 `ImplementationClass`인터페이스의 이름을로 하는 다음 문을에 추가 합니다.  
  
     [!code-vb[VbVbalrOOP#100](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#100)]
  
     클래스 또는 구조체의 맨 위에 있는 다른 항목과 별도로 나열 되는 경우 `Implements` 문은 클래스 또는 구조체가 인터페이스를 구현 한다는 것을 나타냅니다.  
  
     통합 개발 환경 내에서 작업 하는 경우 enter 키를 누를 `TestInterface` 때에 필요한 클래스 멤버를 **코드 편집기** 에서 구현 하 고 다음 단계를 건너뛸 수 있습니다.  
  
3. 통합 개발 환경 내에서 작업 하지 않는 경우 인터페이스 `MyInterface`의 모든 멤버를 구현 해야 합니다. `ImplementationClass` `Event1`, 및`Prop1`를구현 하려면에 다음 코드를 추가 합니다. `Method1`  
  
     [!code-vb[VbVbalrOOP#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#101)]
  
     `Implements` 문은 구현 중인 인터페이스와 인터페이스 멤버의 이름을로 합니다.  
  
4. 속성 값을 저장 `Prop1` 한 클래스에 전용 필드를 추가 하 여의 정의를 완료 합니다.  
  
     [!code-vb[VbVbalrOOP#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#102)]
  
     Get 접근자 속성 `pval` 에서의 값을 반환 합니다.  
  
     [!code-vb[VbVbalrOOP#103](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#103)]
  
     속성 집합 접근자 `pval` 에서 값을 설정 합니다.  
  
     [!code-vb[VbVbalrOOP#104](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#104)]
  
5. 다음 코드를 추가 `Method1` 하 여의 정의를 완료 합니다.  
  
     [!code-vb[VbVbalrOOP#105](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#105)]
  
### <a name="to-test-the-implementation-of-the-interface"></a>인터페이스 구현을 테스트 하려면
  
1. **솔루션 탐색기**에서 프로젝트의 시작 폼을 마우스 오른쪽 단추로 클릭 하 고 **코드 보기**를 클릭 합니다. 편집기에서 시작 폼의 클래스를 표시 합니다. 기본적으로 시작 폼이 호출 `Form1`됩니다.  
  
2. 클래스에 다음 `testInstance` 필드를 추가 합니다. `Form1`  
  
     [!code-vb[VbVbalrOOP#120](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#120)]
  
     `Form1` 로 `testInstance` 선언하면클래스가해당이벤트를`WithEvents`처리할 수 있습니다.  
  
3. `Form1` 클래스에 다음 이벤트 처리기를 추가 하 여에서 `testInstance`발생 하는 이벤트를 처리 합니다.  
  
     [!code-vb[VbVbalrOOP#106](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#106)]
  
4. 클래스에 라는 `Test` 서브루틴을 추가 하 여 구현 클래스를 테스트 합니다. `Form1`  
  
     [!code-vb[VbVbalrOOP#107](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#107)]
  
     프로시저 `Test` 는를 구현 `MyInterface`하는 클래스의 인스턴스를 만들고, 해당 인스턴스를 `testInstance` 필드에 할당 하 고, 속성을 설정 하 고, 인터페이스를 통해 메서드를 실행 합니다.  
  
5. 시작 폼의 프로시저에서 `Test` 프로시저를 호출 `Form1 Load` 하는 코드를 추가 합니다.  
  
     [!code-vb[VbVbalrOOP#108](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#108)]
  
6. F5 키 `Test` 를 눌러 프로시저를 실행 합니다. "Prop1가 9로 설정 되었습니다." 라는 메시지가 표시 됩니다. 확인을 클릭 하면 "Method1의 X 매개 변수가 5입니다." 라는 메시지가 표시 됩니다. 확인을 클릭 하면 "이벤트를 catch 했습니다." 라는 메시지가 표시 됩니다.  
  
## <a name="see-also"></a>참고자료

- [Implements 문](../../../../visual-basic/language-reference/statements/implements-statement.md)
- [인터페이스](../../../../visual-basic/programming-guide/language-features/interfaces/index.md)
- [Interface 문](../../../../visual-basic/language-reference/statements/interface-statement.md)
- [Event 문](../../../../visual-basic/language-reference/statements/event-statement.md)
