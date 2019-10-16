---
title: '방법: 선언 구조체 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], structures
- structure statements [Visual Basic]
- statements [Visual Basic], structure
- structures [Visual Basic], declaring
ms.assetid: d5e98381-eb81-47d4-af83-48cc534a2572
ms.openlocfilehash: a52daddaa8701ccca9bd9b5b4a48535a6ffa19ed
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61906713"
---
# <a name="how-to-declare-a-structure-visual-basic"></a>방법: 선언 구조체 (Visual Basic)
먼저 사용 하 여 구조체 선언을 [Structure 문](../../../../visual-basic/language-reference/statements/structure-statement.md)를 종료 하 고는 `End Structure` 문. 두 문 사이 선언 해야 하나 이상의 *요소*합니다. 모든 데이터 형식의 요소 수는 있지만 비공유 변수 또는 비공유, 비 사용자 정의 이벤트를 하나 이상 이어야 합니다.  
  
 구조체 선언에서는 구조 요소를 초기화할 수 없습니다. 구조체 형식 이어야 하는 변수를 선언할 때 값을 할당 하는 요소 변수를 통해 액세스 하 여.  
  
 구조체와 클래스 간의 차이점, 참조 [구조체와 클래스](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)합니다.  
  
 데모용으로 직원의 이름과 내선 전화 번호, 급여를 추적 하려는 경우를 가정해 봅시다. 구조체를 사용 하면 단일 변수에서이 작업을 수행할 수 있습니다.  
  
### <a name="to-declare-a-structure"></a>구조체를 선언 하려면  
  
1. 시작 및 끝 문장 구조를 만듭니다.  
  
     사용 하 여 구조 액세스 수준을 지정할 수 있습니다는 [공용](../../../../visual-basic/language-reference/modifiers/public.md), [Protected](../../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../../visual-basic/language-reference/modifiers/friend.md), 또는 [개인](../../../../visual-basic/language-reference/modifiers/private.md) 키워드 또는 있습니다 수 있도록 기본적으로 `Public`입니다.  
  
    ```  
    Private Structure employee  
    End Structure  
    ```  
  
2. 구조체의 본문에 요소를 추가 합니다.  
  
     구조체에는 하나 이상의 요소가 있어야 합니다. 모든 요소를 선언 하 고에 대 한 액세스 수준을 지정 해야 합니다. 사용 하는 경우는 [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md) 접근성 기본값으로 키워드 없이 `Public`합니다.  
  
    ```  
    Private Structure employee  
        Public givenName As String  
        Public familyName As String  
        Public phoneExtension As Long  
        Private salary As Decimal  
        Public Sub giveRaise(raise As Double)  
            salary *= raise  
        End Sub  
        Public Event salaryReviewTime()  
    End Structure  
    ```  
  
     합니다 `salary` 앞의 예제에서 필드는 `Private`, 즉에 포함 하는 클래스 에서도 구조체 외부에서는 액세스할 수 없습니다. 그러나 합니다 `giveRaise` 절차는 `Public`이므로 구조 외부에서 호출할 수 있습니다. 마찬가지로, 발생 시킬 수 있습니다는 `salaryReviewTime` 구조 외부에서 이벤트입니다.  
  
     변수 외에도 `Sub` 프로시저 및 이벤트에 상수를 정의할 수도 있습니다 `Function` 절차 및 구조에는 속성입니다. 에서는 하나 이상의 속성으로 지정할 수 있습니다 합니다 *속성의 기본값을*하나 이상의 인수를 사용 하는, 합니다. 사용 하 여 이벤트를 처리할 수 있습니다는 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) `Sub` 프로시저입니다. 자세한 내용은 [방법: 선언 및 Visual Basic의 기본 속성을 호출](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [기본 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)
- [복합 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [구조체](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [구조체 변수](../../../../visual-basic/programming-guide/language-features/data-types/structure-variables.md)
- [구조체 및 기타 프로그래밍 요소](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)
- [구조체와 클래스](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)
- [사용자 정의 데이터 형식](../../../../visual-basic/language-reference/data-types/user-defined-data-type.md)
