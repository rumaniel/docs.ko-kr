---
title: 개체 변수 선언(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- early binding [Visual Basic]
- declarations [Visual Basic], class
- classes [Visual Basic], declaring
- binding [Visual Basic], late and early
- object variables [Visual Basic], declaring
- variables [Visual Basic], object
- declaring variables [Visual Basic], object variables
- declaring classes [Visual Basic]
- late binding [Visual Basic]
ms.assetid: 2a5a41a3-1aa8-4236-b1f0-2382af7bf715
ms.openlocfilehash: 9e57d49965537a45bc62b9078079389efcfb2e2c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64598740"
---
# <a name="object-variable-declaration-visual-basic"></a>개체 변수 선언(Visual Basic)
개체 변수를 선언 하는 일반적인 선언문을 사용 합니다. 지정 데이터 형식에 대 한 `Object` (즉, 합니다 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)) 또는 보다 구체적인 클래스는 개체를 만들려는 합니다.  
  
 변수를 선언 `Object` 으로 선언 하는 것과 같습니다 <xref:System.Object?displayProperty=nameWithType>합니다.  
  
 특정 개체 클래스를 사용 하 여 변수를 선언 하면 모든 메서드 및 해당 클래스와 상속 된 클래스에 의해 노출 되는 속성 액세스할 수 있습니다. 사용 하 여 변수를 선언 하는 경우 <xref:System.Object>의 구성원만 액세스할 수 있습니다 합니다 <xref:System.Object> 클래스를 설정 하지 않으면 `Option Strict Off` 런타임에 바인딩을 허용 합니다.  
  
## <a name="declaration-syntax"></a>선언 구문  
 개체 변수 선언 하려면 다음 구문을 사용 합니다.  
  
```vb  
Dim variablename As [New] { objectclass | Object }  
```  
  
 지정할 수도 있습니다 [공용](../../../../visual-basic/language-reference/modifiers/public.md), [Protected](../../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../../visual-basic/language-reference/modifiers/friend.md), `Protected Friend`를 [개인](../../../../visual-basic/language-reference/modifiers/private.md), [공유](../../../../visual-basic/language-reference/modifiers/shared.md), 또는 [정적](../../../../visual-basic/language-reference/modifiers/static.md) 선언에서 합니다. 다음 예제에서는 선언을 사용할 수 있습니다.  
  
```vb  
Private objA As Object  
Static objB As System.Windows.Forms.Label  
Dim objC As System.OperatingSystem  
```  
  
## <a name="late-binding-and-early-binding"></a>초기 바인딩 및 런타임에 바인딩  
 경우에 따라 특정 클래스 알려지지 않은 코드가 실행 될 때까지 합니다. 개체 변수를 선언 해야이 경우에 `Object` 데이터 형식입니다. 모든 유형의 개체에 대 한 일반 참조를 만들고 특정 클래스는 런타임에 할당 됩니다. 이 이라고 *런타임에 바인딩*합니다. 런타임에 바인딩 추가 실행 시간이 필요 합니다. 또한 코드를 가장 최근에 할당 된 클래스의 속성과 메서드를 제한 합니다. 이 코드를 다른 클래스의 멤버에 액세스 하려고 합니다. 런타임 오류가 발생할 수 있습니다.  
  
 컴파일 시간에 특정 클래스를 알고 있는 경우 해당 클래스의 개체 변수를 선언 해야 합니다. 이것을 *초기 바인딩*이라고 합니다. 초기 바인딩 성능을 개선 하 고 모든 메서드 및 특정 클래스의 속성에 대 한 코드 액세스를 보장 합니다. 변수 경우 이전 예제에서는 선언에 `objA` 클래스의 개체에만 사용 하 여 <xref:System.Windows.Forms.Label?displayProperty=nameWithType>를 지정 해야 `As System.Windows.Forms.Label` 를 선언 합니다.  
  
### <a name="advantages-of-early-binding"></a>초기 바인딩의 장점  
 특정 클래스로 개체 변수를 선언 하면 여러 이점이 있습니다.  
  
- 자동 형식 검사  
  
- 특정 클래스의 모든 멤버에 대 한 액세스 보장  
  
- 코드 편집기에서 Microsoft IntelliSense 지원  
  
- 코드의 가독성 향상된  
  
- 코드에서 오류를 줄일 수  
  
- 에 전달 된 오류 컴파일 시간 대신 런타임에  
  
- 빠른 코드 실행  
  
## <a name="access-to-object-variable-members"></a>개체 변수 멤버에 대 한 액세스  
 때 `Option Strict` 꺼져 `On`, 메서드 및 속성 선언 된 클래스의 개체 변수에 액세스할 수 있습니다. 다음은 이에 대한 예입니다.  
  
```vb  
' Option statements must precede all other source file lines.  
Option Strict On  
' Imports statement must precede all declarations in the source file.  
Imports System.Windows.Forms  
Public Sub accessMembers()  
    Dim p As Object  
    Dim q As System.Windows.Forms.Label  
    p = New System.Windows.Forms.Label  
    q = New System.Windows.Forms.Label  
    Dim j, k As Integer  
    ' The following statement generates a compiler ERROR.  
    j = p.Left  
    ' The following statement retrieves the left edge of the label in pixels.  
    k = q.Left  
End Sub  
```  
  
 이 예제에서 `p` 는 <xref:System.Object> 클래스 자체의 멤버만 사용할 수 있으므로 `Left` 속성을 포함하지 않습니다. 반면, `q` 형식으로 선언된 <xref:System.Windows.Forms.Label>는 <xref:System.Windows.Forms.Label> 네임스페이스에 있는 <xref:System.Windows.Forms> 클래스의 모든 메서드와 속성을 사용할 수 있습니다.  
  
## <a name="flexibility-of-object-variables"></a>개체 변수의 유연성  
 상속 계층 구조의 개체를 사용할 때는 다양 한 개체 변수를 선언 하는 데 사용 하는 클래스를 해야 합니다. 이 선택 하는 경우 클래스의 멤버에 대 한 액세스에 대 한 개체 할당의 유연 하 게를 고려해 야 합니다. 예를 들어을 발생 시키는 상속 계층 구조는 <xref:System.Windows.Forms.Form?displayProperty=nameWithType> 클래스:  
  
 <xref:System.Object>  
  
 &nbsp;&nbsp;<xref:System.MarshalByRefObject>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;<xref:System.ComponentModel.Component>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.Control>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.ScrollableControl>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.ContainerControl>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.Form>  
  
 응용 프로그램 폼 클래스를 정의 하는 가정 `specialForm`, 클래스에서 상속 하는 <xref:System.Windows.Forms.Form>합니다. 특히 참조 하는 개체 변수를 선언할 수 있습니다 `specialForm`다음 예제와 같이 합니다.  
  
```vb  
Public Class specialForm  
    Inherits System.Windows.Forms.Form  
    ' Insert code defining methods and properties of specialForm.  
End Class  
Dim nextForm As New specialForm  
```  
  
 앞의 예제에서 선언과 변수를 제한 `nextForm` 클래스의 개체에 `specialForm`, 되지만 모든 메서드 및 속성을 `specialForm` 수 `nextForm`는 모든 클래스의 모든 멤버 뿐 아니라 `specialForm` 상속 합니다.  
  
 형식으로 선언 하 여 보다 일반적인 개체 변수를 만들 수 있습니다 <xref:System.Windows.Forms.Form>다음 예제와 같이 합니다.  
  
```vb  
Dim anyForm As System.Windows.Forms.Form  
```  
  
 앞의 예제에서 선언과 사용 하면 응용 프로그램의 어떠한 부분도 할당 `anyForm`합니다. 그러나 있지만 `anyForm` 클래스의 모든 멤버에 액세스할 수 있습니다 <xref:System.Windows.Forms.Form>에서 추가 메서드 또는 같은 특정 폼에 정의 된 속성 중 하나를 사용할 수 없습니다 `specialForm`합니다.  
  
 기본 클래스의 모든 멤버는 파생된 클래스를 사용할 수 있지만 파생된 클래스의 추가 멤버는 기본 클래스를 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- [개체 변수](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [개체 변수 할당](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)
- [개체 변수 값](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)
- [방법: 개체 변수를 선언 하 고 Visual Basic의 개체를 할당](../../../../visual-basic/programming-guide/language-features/variables/how-to-declare-an-object-variable-and-assign-an-object-to-it.md)
- [방법: 개체의 멤버에 액세스](../../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)
- [New 연산자](../../../../visual-basic/language-reference/operators/new-operator.md)
- [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
