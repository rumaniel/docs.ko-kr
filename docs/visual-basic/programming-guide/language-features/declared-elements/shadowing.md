---
title: Visual Basic의 숨김 기능
ms.date: 07/20/2015
helpviewer_keywords:
- inheritance [Visual Basic], shadowing
- overriding, and shadowing
- shadowing
- duplicate names [Visual Basic]
- shadowing, by inheritance
- declared elements [Visual Basic], referencing
- shadowing, by scope
- declared elements [Visual Basic], hiding
- naming conflicts, shadowing
- declared elements [Visual Basic], shadowing
- shadowing, and overriding
- scope [Visual Basic], shadowing
- Shadows keyword [Visual Basic], about
- objects [Visual Basic], names
- names [Visual Basic], shadowing
ms.assetid: 54bb4c25-12c4-4181-b4a0-93546053964e
ms.openlocfilehash: 30c02cf367c461c3896a01538d03380627de294f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004860"
---
# <a name="shadowing-in-visual-basic"></a>Visual Basic의 숨김 기능
두 프로그래밍 요소가 동일한 이름을 공유 하는 경우 그 중 하나는 다른 *요소를 숨기 거 나 숨길*수 있습니다. 이러한 경우에는 숨겨진 요소를 참조할 수 없습니다. 대신, 코드에서 요소 이름을 사용 하는 경우 Visual Basic 컴파일러에서 해당 요소 이름을 숨기는 요소로 확인 합니다.  
  
## <a name="purpose"></a>용도  
 숨김의 주요 목적은 클래스 멤버의 정의를 보호 하는 것입니다. 기본 클래스는 이미 정의한 것과 동일한 이름으로 요소를 만드는 변경 될 수 있습니다. 이 경우 `Shadows` 한정자는 클래스를 통한 참조가 새 기본 클래스 요소가 아닌 사용자가 정의한 멤버로 확인 되도록 합니다.  
  
## <a name="types-of-shadowing"></a>섀도잉 유형  
 요소는 서로 다른 두 가지 방법으로 다른 요소를 숨길 수 있습니다. 섀도잉 요소는 숨겨진 요소를 포함 하는 영역의 하위 영역 내에서 선언할 수 있으며,이 경우 *범위를 통해*숨김은 수행 됩니다. 또는 파생 클래스에서 기본 클래스의 멤버를 다시 정의할 수 있습니다 .이 경우에는 *상속이 상속을 통해*수행 됩니다.  
  
### <a name="shadowing-through-scope"></a>범위를 통한 숨김  
 동일한 모듈, 클래스 또는 구조체의 프로그래밍 요소가 같은 이름을 갖지만 범위를 다르게 지정할 수 있습니다. 두 요소가 이러한 방식으로 선언 되 고 코드가 공유 하는 이름을 참조 하는 경우 범위가 좁은 요소가 다른 요소 (블록 범위는 가장 좁은)를 숨깁니다.  
  
 예를 들어 모듈은 `temp` 이라는 `Public` 변수를 정의할 수 있으며, 모듈 내의 프로시저는 `temp` 라는 지역 변수를 선언할 수 있습니다. 프로시저 내에서 `temp`에 대 한 참조는 지역 변수에 액세스 하는 반면 프로시저 외부에서 `temp`에 대 한 참조는 `Public` 변수에 액세스 합니다. 이 경우 프로시저 변수 `temp`은 모듈 변수 `temp`을 숨깁니다.  
  
 다음 그림에서는 두 변수를 보여 줍니다. 두 변수는 모두 `temp`입니다. 지역 변수 `temp`은 자체 프로시저 `p`에서 액세스할 때 멤버 변수 `temp`을 숨깁니다. 그러나 `MyClass` 키워드는 숨김을 무시 하 고 멤버 변수에 액세스 합니다.  
  
 ![범위를 통해 숨김을 보여 주는 그래픽입니다.](./media/shadowing/shadow-scope-diagram.gif)
  
 범위를 통해 숨기는 방법에 대 한 예제를 보려면 [How to: @ No__t-0 변수와 이름이 같은 변수를 숨깁니다.  
  
### <a name="shadowing-through-inheritance"></a>상속을 통한 숨김  
 파생 클래스가 기본 클래스에서 상속 된 프로그래밍 요소를 다시 정의 하는 경우 다시 정의 하는 요소는 원래 요소를 숨깁니다. 모든 형식의 선언 된 요소 또는 오버 로드 된 요소 집합을 다른 형식으로 숨길 수 있습니다. 예를 들어 `Integer` 변수는 `Function` 프로시저를 숨길 수 있습니다. 다른 프로시저를 사용 하 여 프로시저를 숨기는 경우 다른 매개 변수 목록과 다른 반환 형식을 사용할 수 있습니다.  
  
 다음 그림에서는 기본 클래스 `b`과 `b`에서 상속 되는 파생 클래스 @no__t를 보여 줍니다. 기본 클래스는 `proc` 이라는 프로시저를 정의 하 고 파생 클래스는 이름이 같은 다른 프로시저를 사용 하 여 해당 프로시저를 숨깁니다. 첫 번째 `Call` 문은 파생 클래스의 숨김 `proc`에 액세스 합니다. 그러나 `MyBase` 키워드는 숨김을 무시 하 고 기본 클래스의 숨겨진 프로시저에 액세스 합니다.  
  
 ![상속을 통한 숨기기 그래픽 다이어그램](./media/shadowing/shadowing-inherit-diagram.gif)  
  
 상속을 통한 숨김 예제는 [How to: @ No__t-0 변수와 이름이 같은 변수를 숨기고 [How: 상속 된 변수 @ no__t-0을 숨깁니다.  
  
#### <a name="shadowing-and-access-level"></a>숨김 및 액세스 수준  
 숨김 요소는 파생 클래스를 사용 하 여 코드에서 항상 액세스할 수 있는 것은 아닙니다. 예를 들어-0 @no__t 선언할 수 있습니다. 이러한 경우에는 숨김은 발생 하지 않으며, 숨김이 없는 경우 컴파일러는 동일한 요소에 대 한 참조를 확인 합니다. 이 요소는 숨기는 클래스에서 뒤로 derivational 가장 적은 수의 액세스 가능한 요소입니다. 숨겨진 요소가 프로시저인 경우 동일한 이름, 매개 변수 목록 및 반환 형식을 사용 하 여 가장 가까운 액세스 가능한 버전으로 확인 됩니다.  
  
 다음 예제에서는 세 클래스의 상속 계층 구조를 보여 줍니다. 각 클래스는 `Sub` 프로시저 `display`을 정의 하 고 각 파생 클래스는 기본 클래스의 `display` 프로시저를 숨깁니다.  
  
```vb  
Public Class firstClass  
    Public Sub display()  
        MsgBox("This is firstClass")  
    End Sub  
End Class  
Public Class secondClass  
    Inherits firstClass  
    Private Shadows Sub display()  
        MsgBox("This is secondClass")  
    End Sub  
End Class  
Public Class thirdClass  
    Inherits secondClass  
    Public Shadows Sub display()  
        MsgBox("This is thirdClass")  
    End Sub  
End Class  
Module callDisplay  
    Dim first As New firstClass  
    Dim second As New secondClass  
    Dim third As New thirdClass  
    Public Sub callDisplayProcedures()  
        ' The following statement displays "This is firstClass".  
        first.display()  
        ' The following statement displays "This is firstClass".  
        second.display()  
        ' The following statement displays "This is thirdClass".  
        third.display()  
    End Sub  
End Module  
```  
  
 위의 예제에서 파생 클래스 `secondClass`은 `Private` 프로시저를 사용 하 여-1 @no__t 합니다. @No__t-2에서 모듈 `callDisplay` @no__t를 호출 하는 경우 호출 하는 코드는 `secondClass` 외부에 있으므로 private `display` 프로시저에 액세스할 수 없습니다. 숨김은 안 되며, 컴파일러는 기본 클래스 `display` 프로시저에 대 한 참조를 확인 합니다.  
  
 그러나 추가 파생 클래스 `thirdClass` `display`을 `Public`로 선언 하므로 `callDisplay`의 코드는이를 액세스할 수 있습니다.  
  
## <a name="shadowing-and-overriding"></a>숨김 및 재정의  
 숨김과 재정의를 혼동 하지 마십시오. 파생 클래스가 기본 클래스에서 상속 하는 경우와 선언 된 요소를 다른 요소와 모두 재정의 하는 경우 둘 다 사용 됩니다. 하지만 둘 사이에는 상당한 차이점이 있습니다. 비교는 [숨김과 재정의 간의 차이점](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)을 참조 하세요.  
  
## <a name="shadowing-and-overloading"></a>숨김 및 오버 로드  
 파생 클래스에서 둘 이상의 요소를 사용 하 여 동일한 기본 클래스 요소를 숨기는 경우에는 숨기는 요소가 해당 요소의 오버 로드 된 버전이 됩니다. 자세한 내용은 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)을 참조하세요.  
  
## <a name="accessing-a-shadowed-element"></a>숨겨진 요소에 액세스  
 파생 클래스에서 요소에 액세스 하는 경우 일반적으로 `Me` 키워드로 요소 이름을 정규화 하 여 파생 클래스의 현재 인스턴스를 통해이 작업을 수행 합니다. 파생 클래스가 기본 클래스의 요소를 숨기는 경우 `MyBase` 키워드로 한정 하 여 기본 클래스 요소에 액세스할 수 있습니다.  
  
 숨겨진 요소에 액세스 하는 방법에 대 한 예제를 보려면 [How to: 파생 클래스 @ no__t-0에 의해 숨겨진 변수에 액세스 합니다.  
  
### <a name="declaration-of-the-object-variable"></a>개체 변수의 선언입니다.  
 개체 변수를 만드는 방법은 파생 클래스가 숨기는 요소 또는 숨겨진 요소에 액세스 하는지 여부에도 영향을 줄 수 있습니다. 다음 예제에서는 파생 된 클래스에서 두 개의 개체를 만들지만 한 개체가 기본 클래스로 선언 되 고 다른 개체가 파생 클래스로 선언 됩니다.  
  
```vb  
Public Class baseCls  
    ' The following statement declares the element that is to be shadowed.  
    Public z As Integer = 100  
End Class  
Public Class dervCls  
    Inherits baseCls  
    ' The following statement declares the shadowing element.  
    Public Shadows z As String = "*"  
End Class  
Public Class useClasses  
    ' The following statement creates the object declared as the base class.  
    Dim basObj As baseCls = New dervCls()  
    ' Note that dervCls widens to its base class baseCls.  
    ' The following statement creates the object declared as the derived class.  
    Dim derObj As dervCls = New dervCls()  
    Public Sub showZ()   
    ' The following statement outputs 100 (the shadowed element).  
        MsgBox("Accessed through base class: " & basObj.z)  
    ' The following statement outputs "*" (the shadowing element).  
        MsgBox("Accessed through derived class: " & derObj.z)  
    End Sub  
End Class  
```  
  
 앞의 예제에서 변수 `basObj`은 기본 클래스로 선언 됩니다. @No__t-0 개체를 할당 하는 것은 확대 변환을 구성 하므로 유효 합니다. 그러나 기본 클래스는 파생 클래스에서 `z` 변수의 섀도잉 버전에 액세스할 수 없으므로 컴파일러는-1 @no__t 원래 기본 클래스 값으로 확인 합니다.  
  
## <a name="see-also"></a>참조

- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Visual Basic 범위](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
- [확대 변환과 축소 변환](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
- [재정의](../../../../visual-basic/language-reference/modifiers/overrides.md)
- [Me, My, MyBase 및 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [상속 기본 사항](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
