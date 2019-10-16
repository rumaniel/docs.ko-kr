---
title: '방법: 파생 클래스에 의해 숨겨진 변수에 액세스 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- qualification [Visual Basic], of element names
- base classes [Visual Basic], accessing elements
- element names [Visual Basic], qualification
- references [Visual Basic], declared elements
- declared elements [Visual Basic], referencing
- variables [Visual Basic], accessing hidden
ms.assetid: ae21a8ac-9cd4-4fba-a3ec-ecc4321ef93c
ms.openlocfilehash: 68f92142cdc435ebd82101eea83035e1d09dcf25
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630020"
---
# <a name="how-to-access-a-variable-hidden-by-a-derived-class-visual-basic"></a>방법: 파생 클래스에 의해 숨겨진 변수에 액세스 (Visual Basic)

파생 클래스의 코드가 변수에 액세스 하는 경우 컴파일러는 일반적으로 가장 가까운 액세스 가능 버전에 대 한 참조를 확인 합니다. 즉, 액세스 하는 클래스에서 derivational 가장 적은 수의 액세스 가능 버전을 찾습니다. 변수가 파생 클래스에서 정의 된 경우이 코드는 일반적으로 해당 정의에 액세스 합니다.

파생 클래스 변수가 기본 클래스의 변수를 숨기면 기본 클래스 버전을 숨깁니다. 그러나 `MyBase` 키워드를 사용 하 여 정규화 함으로써 기본 클래스 변수에 액세스할 수 있습니다.

### <a name="to-access-a-base-class-variable-hidden-by-a-derived-class"></a>파생 클래스에 의해 숨겨진 기본 클래스 변수에 액세스 하려면

- 식 또는 대입문에서 변수 이름 `MyBase` 앞에 키워드와 마침표 (`.`)를 붙입니다.

    컴파일러는 변수의 기본 클래스 버전에 대 한 참조를 확인 합니다.

    다음 예제에서는 상속을 통한 숨김을 보여 줍니다. 두 참조를 만듭니다. 하나는 숨기는 변수에 액세스 하 고 다른 하나는 숨김을 무시 합니다.

    ```vb
    Public Class shadowBaseClass
        Public shadowString As String = "This is the base class string."
    End Class
    Public Class shadowDerivedClass
        Inherits shadowBaseClass
        Public Shadows shadowString As String = "This is the derived class string."
        Public Sub showStrings()
            Dim s As String = "Unqualified shadowString: " & shadowString &
                vbCrLf & "MyBase.shadowString: " & MyBase.shadowString
            MsgBox(s)
        End Sub
    End Class
    ```

    앞의 예제에서는 기본 클래스 `shadowString` 에서 변수를 선언 하 고 파생 클래스에서 해당 변수를 숨깁니다. 파생 클래스 `showStrings` 의 프로시저는 이름이 `shadowString` 한정 되지 않은 경우 문자열의 숨김 버전을 표시 합니다. 그런 다음 `MyBase` 키워드를 사용 하 여 `shadowString` 정규화 된 버전을 표시 합니다.

## <a name="robust-programming"></a>강력한 프로그래밍

숨겨진 변수의 의도 하지 않은 버전을 참조 하는 위험을 줄이려면 숨겨진 변수에 대 한 모든 참조를 정규화 할 수 있습니다. 섀도잉 시 이름이 같은 변수의 버전이 두 개 이상 도입 되었습니다. 코드 문이 변수 이름을 참조 하는 경우 컴파일러가 참조를 확인 하는 버전은 코드 문의 위치 및 한정 된 문자열이 있는지 여부와 같은 요소에 따라 달라 집니다. 이로 인해 잘못 된 버전의 변수를 참조 하는 위험이 늘어날 수 있습니다.

## <a name="see-also"></a>참고자료

- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Visual Basic에서 숨김](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
- [숨기기와 재정의의 차이점](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)
- [방법: 변수와 이름이 같은 변수 숨기기](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)
- [방법: 상속 된 변수 숨기기](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)
- [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
- [재정의](../../../../visual-basic/language-reference/modifiers/overrides.md)
- [Me, My, MyBase 및 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [상속 기본 사항](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
