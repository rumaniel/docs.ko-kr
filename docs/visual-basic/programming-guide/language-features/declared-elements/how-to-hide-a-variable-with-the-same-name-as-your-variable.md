---
title: '방법: 변수와 이름이 같은 변수를 숨깁니다 (Visual Basic).'
ms.date: 07/20/2015
helpviewer_keywords:
- qualification [Visual Basic], of element names
- declarations [Visual Basic], elements
- element names [Visual Basic], qualification
- references [Visual Basic], declared elements
- declaration statements [Visual Basic], declared elements
- declaring elements [Visual Basic]
- referencing declared elements [Visual Basic]
- declared elements [Visual Basic], referencing
- declared elements [Visual Basic], about declared elements
ms.assetid: e39c0752-f19f-4d2e-a453-00df1b5fc7ee
ms.openlocfilehash: 487e0a15ba6b52f92ab39fe0bae4ab15fa92707f
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68629992"
---
# <a name="how-to-hide-a-variable-with-the-same-name-as-your-variable-visual-basic"></a>방법: 변수와 이름이 같은 변수를 숨깁니다 (Visual Basic).

변수를 숨기 *는 방식으로* 숨길 수 있습니다. 즉, 동일한 이름의 변수를 사용 하 여 변수를 다시 정의 합니다. 다음 두 가지 방법으로 숨기려는 변수를 숨길 수 있습니다.

- **범위를 통한 숨김** 숨기려는 변수를 포함 하는 영역의 영역 영역 안에서 다시 선언할 하 여 범위를 숨길 수 있습니다.

- **상속을 통한 숨김** 숨기려는 변수가 클래스 수준에서 정의 되는 경우 상속을 통해 파생 클래스의 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) 키워드로 다시 선언할 하 여 숨길 수 있습니다.

## <a name="two-ways-to-hide-a-variable"></a>변수를 숨기는 두 가지 방법

#### <a name="to-hide-a-variable-by-shadowing-it-through-scope"></a>범위를 통해 변수를 숨겨 변수를 숨기려면

1. 숨기려는 변수를 정의 하는 영역을 확인 하 고 변수를 사용 하 여이를 다시 정의할 영역을 결정 합니다.

    |변수의 영역|재정의할 수 있는 하위 영역|
    |-----------------------|-------------------------------------------|
    |Module|모듈 내의 클래스|
    |클래스|클래스 내의 하위 클래스<br /><br /> 클래스 내의 프로시저|

    해당 프로시저 내의 블록에서 프로시저 변수를 다시 정의할 수 없습니다. 예 `If`를 들어 ... `End If` 생성`For` 또는 루프

2. 아직 없는 경우 영역을 만듭니다.

3. 영역 내에서 숨김 변수를 선언 하는 [Dim 문을](../../../../visual-basic/language-reference/statements/dim-statement.md) 작성 합니다.

    영역 내의 코드가 변수 이름을 참조 하는 경우 컴파일러는 숨기는 변수에 대 한 참조를 확인 합니다.

    다음 예제에서는 범위를 통한 숨김과 숨김을 무시 하는 참조를 보여 줍니다.

    ```vb
    Module shadowByScope
        ' The following statement declares num as a module-level variable.
        Public num As Integer
        Sub show()
            ' The following statement declares num as a local variable.
            Dim num As Integer
            ' The following statement sets the value of the local variable.
            num = 2
            ' The following statement displays the module-level variable.
            MsgBox(CStr(shadowByScope.num))
        End Sub
        Sub useModuleLevelNum()
            ' The following statement sets the value of the module-level variable.
            num = 1
            show()
        End Sub
    End Module
    ```

    앞의 예제에서는 모듈 수준 `num` 및 프로시저 수준 (프로시저 `show`)에서 모두 변수를 선언 합니다. 지역 `num` 변수는 내에서 `show`모듈 수준 변수 `num` 를 숨기 므로 지역 변수는 2로 설정 됩니다. 그러나 `num` 프로시저`useModuleLevelNum` 에서 숨길 지역 변수는 없습니다. 따라서는 모듈 수준 변수의 값을 1로 설정합니다.`useModuleLevelNum`

    `num` 내의 `MsgBox` 호출은`show` 모듈 이름으로 한정 하 여 숨김 메커니즘을 무시 합니다. 따라서 지역 변수 대신 모듈 수준 변수를 표시 합니다.

#### <a name="to-hide-a-variable-by-shadowing-it-through-inheritance"></a>상속을 통해 변수를 숨겨 변수를 숨기려면

1. 숨기려는 변수가 클래스에서 선언 되 고 클래스 수준 (프로시저 외부)에 선언 되어 있어야 합니다. 그렇지 않으면 상속을 통해 숨길 수 없습니다.

2. 이미 존재 하지 않는 경우 변수의 클래스에서 파생 된 클래스를 정의 합니다.

3. 파생 클래스 내에서 변수를 선언 `Dim` 하는 문을 작성 합니다. 선언에 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) 키워드를 포함 합니다.

    파생 클래스의 코드가 변수 이름을 참조 하는 경우 컴파일러는 변수에 대 한 참조를 확인 합니다.

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

섀도잉 시 이름이 같은 변수의 버전이 두 개 이상 도입 되었습니다. 코드 문이 변수 이름을 참조 하는 경우 컴파일러가 참조를 확인 하는 버전은 코드 문의 위치 및 한정 된 문자열이 있는지 여부와 같은 요소에 따라 달라 집니다. 이로 인해 숨겨진 변수의 의도 하지 않은 버전을 참조 하는 위험이 늘어날 수 있습니다. 숨겨진 변수에 대 한 모든 참조를 정규화 하 여이 위험을 낮출 수 있습니다.

## <a name="see-also"></a>참고자료

- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Visual Basic에서 숨김](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
- [숨기기와 재정의의 차이점](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)
- [방법: 상속 된 변수 숨기기](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)
- [방법: 파생 클래스에 의해 숨겨진 변수에 액세스](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)
- [재정의](../../../../visual-basic/language-reference/modifiers/overrides.md)
- [Me, My, MyBase 및 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [상속 기본 사항](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
