---
title: 선언된 요소 참조(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic]
- references [Visual Basic], declared elements
- qualified names [Visual Basic]
ms.assetid: d6301709-f4cc-4b7a-b8ba-80898f14ab46
ms.openlocfilehash: 616599e15c0d3d4c2177622d6820269bcff3ea39
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592804"
---
# <a name="references-to-declared-elements-visual-basic"></a>선언된 요소 참조(Visual Basic)
코드에서 선언 된 요소를 참조 하는 경우 Visual Basic 컴파일러에서는 해당 이름의 적절 한 선언 참조 이름과 일치 합니다. 동일한 이름을 가진 둘 이상의 요소가 선언 된 경우 참조 하는 데는 이러한 요소는 제어할 수 있습니다 *한정* 이름입니다.  
  
 컴파일러는 이름 선언에 대 한 이름 참조를 일치 시 키 려 합니다 *가장 좁은 범위*합니다. 즉, 코드 참조를 만들기를 시작 하 고 다음 요소가 포함 된 수준을 통해 바깥쪽으로 작동 합니다.  
  
 다음 예제에서는 이름이 같은 두 변수에 대 한 참조를 보여 줍니다. 이 예제에서는 두 변수를 선언, 각각의 명명 된 `totalCount`, 다른 모듈에서 범위 수준에서 `container`합니다. 때 절차 `showCount` 표시 `totalCount` 한정자 없이 Visual Basic 컴파일러에서는 범위가, 즉 로컬 선언 내에서 선언에 대 한 참조를 확인 `showCount`합니다. 모듈인 `totalCount` 포함 하는 모듈을 사용 하 여 `container`, 컴파일러는 광범위 한 범위에서 선언에 대 한 참조를 확인 합니다.  
  
```vb  
' Assume these two modules are both in the same assembly.  
Module container  
    Public totalCount As Integer = 1  
    Public Sub showCount()  
        Dim totalCount As Integer = 6000  
        ' The following statement displays the local totalCount (6000).  
        MsgBox("Unqualified totalCount is " & CStr(totalCount))  
        ' The following statement displays the module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
Module callingModule  
    Public Sub displayCount()  
        container.showCount()  
        ' The following statement displays the containing module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
```  
  
## <a name="qualifying-an-element-name"></a>요소 이름 한정  
 이 검색 프로세스를 재정의 하 고 광범위 한 범위에서 선언 된 이름은 해야 지정 하려는 경우 *한정* 더 넓은 범위의 포함 하는 요소 이름입니다. 일부 경우에는 포함 하는 요소를 정하는 데도 해야 합니다.  
  
 대상 요소 정의 된 위치를 식별 하는 정보를 사용 하 여 원본 문에서 이전 이름 수단을 정규화 합니다. 이 정보는 호출을 *한정 문자열*합니다. 하나를 포함할 수 있습니다 또는 자세한 네임 스페이스 및 모듈의 경우, 클래스 또는 구조입니다.  
  
 모듈, 클래스 또는 구조 대상 요소를 포함 하는 한정 문자열 지정 명확 해야 합니다. 컨테이너 다른 포함 하는 요소를 일반적으로 네임 스페이스에 있을 수 있습니다. 여러 요소를 포함 하는 한정 문자열에 포함 해야 합니다.  
  
#### <a name="to-access-a-declared-element-by-qualifying-its-name"></a>해당 이름을 정규화 하 여 선언 된 요소에 액세스 하려면  
  
1. 요소에 정의 된 위치를 결정 합니다. 이 네임 스페이스 또는 네임 스페이스의 계층 구조가 포함 될 수 있습니다. 가장 낮은 수준의 네임 스페이스 내에서 요소 모듈, 클래스 또는 구조에 포함 되어야 합니다.  
  
    ```vb  
    ' Assume the following hierarchy exists outside your code.  
    Namespace outerSpace  
        Namespace innerSpace  
            Module holdsTotals  
                Public Structure totals  
                    Public thisTotal As Integer  
                    Public Shared grandTotal As Long  
                End Structure  
            End Module  
        End Namespace  
    End Namespace  
    ```  
  
2. 대상 요소의 위치에 따라 한정 경로 확인 합니다. 최상위 네임 스페이스를 사용 하 여 시작한 계속 가장 낮은 수준의 네임 스페이스에는 모듈, 클래스 또는 대상 요소를 포함 하는 구조를 사용 하 여 종료 합니다. 경로의 각 요소는 다음에 오는 요소를 포함 해야 합니다.  
  
     `outerSpace` → `innerSpace` → `holdsTotals` → `totals`  
  
3. 대상 요소의 한정 문자열을 준비 합니다. 에 마침표 (`.`) 경로 있는 모든 요소 뒤 합니다. 응용 프로그램에서 한정 문자열의 모든 요소에 액세스할 수 있어야 합니다.  
  
    ```vb  
    outerSpace.innerSpace.holdsTotals.totals.  
    ```  
  
4. 식 또는 대입문은 일반적인 방법으로 대상 요소에 참조를 작성 합니다.  
  
    ```vb  
    grandTotal = 9000  
    ```  
  
5. 대상 요소 이름 한정 문자열 앞에 야 합니다. 이름을 마침표 바로 다음에 나와야 (`.`) 모듈, 클래스 또는 구조 요소를 포함 하는 다음과 같습니다.  
  
    ```vb  
    ' Assume the following module is part of your code.  
    Module accessGrandTotal  
        Public Sub setGrandTotal()  
            outerSpace.innerSpace.holdsTotals.totals.grandTotal = 9000  
        End Sub  
    End Module  
    ```  
  
6. 컴파일러는 대상 요소 참조를 일치 시킬 수의 선택을 취소 하 고 명확한 선언의 찾을 한정 문자열을 사용 합니다.  
  
 응용 프로그램에 동일한 이름을 가진 둘 이상의 프로그래밍 요소에 액세스 하는 경우 이름 참조를 한정할 수도 수 있습니다. 예를 들어, 합니다 <xref:System.Windows.Forms> 및 <xref:System.Web.UI.WebControls> 네임 스페이스 모두 포함을 `Label` 클래스 (<xref:System.Windows.Forms.Label?displayProperty=nameWithType> 및 <xref:System.Web.UI.WebControls.Label?displayProperty=nameWithType>). 응용 프로그램 모두를 사용 하거나 자체 정의 하는 경우 `Label` 클래스를 서로 다른 구별 해야 `Label` 개체입니다. 변수 선언에 네임 스페이스 또는 가져오기 별칭을 포함 합니다. 다음 예제에서는 가져오기 별칭을 사용 합니다.  
  
```vb  
' The following statement must precede all your declarations.  
Imports win = System.Windows.Forms, web = System.Web.UI.WebControls  
' The following statement references the Windows.Forms.Label class.  
Dim winLabel As New win.Label()  
```  
  
## <a name="members-of-other-containing-elements"></a>포함 된 요소의 다른 멤버  
 다른 클래스 또는 구조체의 비공유 멤버를 사용 하는 경우 먼저 변수 또는 클래스 또는 구조체의 인스턴스를 가리키는 식과 멤버 이름을 정규화 해야 합니다. 다음 예에서 `demoClass` 라는 클래스의 인스턴스가 `class1`합니다.  
  
```vb  
Dim demoClass As class1 = New class1()  
demoClass.someSub[(argumentlist)]  
```  
  
 클래스 이름 자체를 사용 하 여 없는 멤버를 한정할 수 없습니다 [공유](../../../../visual-basic/language-reference/modifiers/shared.md)합니다. 개체 변수에 인스턴스를 먼저 만들어야 합니다 (이 경우 `demoClass`) 변수 이름으로 참조 해야 합니다.  
  
 클래스 또는 구조체에는 `Shared` 멤버 클래스 또는 구조체 이름 또는 변수 또는 인스턴스를 가리키는 식과 해당 멤버를 한정할 수 있습니다.  
  
 모듈에는 별도 모든 인스턴스가 및 모든 해당 멤버는 `Shared` 기본적으로 합니다. 따라서 모듈 이름 사용 하 여 모듈 멤버를 한정할 수입니다.  
  
 다음 예제에서는 모듈 멤버 프로시저에 대 한 정규화 된 참조를 보여 줍니다. 이 예제에서는 두 개의 선언 `Sub` 이라는 프로시저 `perform`, 서로 다른 모듈 프로젝트에. 각각 고유한 모듈 내에서 한정 하지 않고 지정할 수 있지만 다른 곳에서 참조 하는 경우에 한정 되어야 합니다. 마지막에서 참조 하므로 `module3` 맞지 않을 `perform`, 컴파일러가 해당 참조를 확인할 수 없습니다.  
  
```vb  
' Assume these three modules are all in the same assembly.  
Module module1  
    Public Sub perform()  
        MsgBox("module1.perform() now returning")  
    End Sub  
End Module  
Module module2  
    Public Sub perform()  
        MsgBox("module2.perform() now returning")  
    End Sub  
    Public Sub doSomething()  
        ' The following statement calls perform in module2, the active module.  
        perform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
    End Sub  
End Module  
Module module3  
    Public Sub callPerform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
        ' The following statement makes an unresolvable name reference  
        ' and therefore generates a COMPILER ERROR.  
        perform() ' INVALID statement  
    End Sub  
End Module  
```  
  
## <a name="references-to-projects"></a>프로젝트에 대 한 참조  
 사용 하도록 [공용](../../../../visual-basic/language-reference/modifiers/public.md) 다른 프로젝트에 정의 된 요소를 먼저 설정 해야를 *참조* 해당 프로젝트의 어셈블리 또는 형식 라이브러리입니다. 참조를 설정 하려면 **참조 추가** 에 **프로젝트** 메뉴나 사용 합니다 [/reference (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/reference.md) 명령줄 컴파일러 옵션.  
  
 예를 들어,.NET Framework의 XML 개체 모델을 사용할 수 있습니다. 대 한 참조를 설정 하는 경우는 <xref:System.Xml> 네임 스페이스를 선언 하 고 수와 같은 해당 클래스 중 하나를 사용 하 여 <xref:System.Xml.XmlDocument>입니다. 다음 예제에서는 <xref:System.Xml.XmlDocument>합니다.  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As System.Xml.XmlDocument  
```  
  
## <a name="importing-containing-elements"></a>요소가 포함 된 가져오기  
 사용할 수는 [Imports 문 (.NET Namespace 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 에 *가져오기* 사용 하려면 클래스나 모듈을 포함 하는 네임 스페이스입니다. 이 옵션을 사용 하면 이름을 정규화 하지 않고 가져온된 네임 스페이스에 정의 된 요소를 참조할 수 있습니다. 다음 예제에서는 가져올 이전 예제를 다시 작성 된 <xref:System.Xml> 네임 스페이스입니다.  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As XmlDocument  
```  
  
 또한 합니다 `Imports` 문에서 정의할 수 있습니다는 *가져오기 별칭* 가져온된 네임 스페이스 각각에 대 한 합니다. 이 소스 코드를 더 간결 하 고 읽기 쉽게 가능 합니다. 다음 예제에서는 이전 예제를 사용 하 여 다시 작성 `xD` 별칭으로는 <xref:System.Xml> 네임 스페이스입니다.  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports xD = System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As xD.XmlDocument  
```  
  
 `Imports` 문을 해도 다른 프로젝트의 요소를 응용 프로그램에 사용할 수 있습니다. 즉, 참조 설정의 위치를 차지 하지 않습니다. 방금 네임 스페이스를 가져오면 해당 네임 스페이스에 정의 된 이름을 정규화 하는 요구 사항을 제거 합니다.  
  
 사용할 수도 있습니다는 `Imports` 을 모듈, 클래스, 구조체 및 열거형을 가져오기 위한 문입니다. 다음 한정자 없이 가져온 요소의 멤버를 사용할 수 있습니다. 그러나 비공유 멤버의 클래스 및 구조 변수 또는 클래스 또는 구조체의 인스턴스로 평가 되는 식으로 항상 정규화 해야 합니다.  
  
## <a name="naming-guidelines"></a>명명 지침  
 동일한 이름을 가진 두 개 이상의 프로그래밍 요소를 정의 하는 경우는 *모호성 이름을* 컴파일러에서 해당 이름에 대 한 참조를 확인 하려고 할 때 발생할 수 있습니다. 둘 이상의 정의가 인지 범위 또는 정의가 없는 범위에 있으면 참조를 확인할 수 없는 합니다. 예를 들어이 도움말 페이지에서 "정규화 된 참조 예"를 참조 하십시오.  
  
 모든 요소에 고유한 이름을 제공 하 여 이름 모호성을 방지할 수 있습니다. 다음 네임 스페이스, 모듈 또는 클래스를 사용 하 여 이름을 한정 하지 않고도 모든 요소에 대 한 참조를 만들 수 있습니다. 실수로 잘못 된 요소를 참조 하는 가능성을 줄일 수도.  
  
## <a name="shadowing"></a>섀도잉  
 동일한 이름을 공유 하는 두 가지 프로그래밍 요소를 숨길 수 중 하나, 또는 *섀도*, 다른 하나입니다. 숨겨진된 요소 참조를 사용할 수 없는 경우 대신, 숨겨진된 요소 이름을 사용 하는 코드를 Visual Basic 컴파일러는 섀도잉 요소 확인 합니다. 예제를 사용 하 여 더 자세한 내용은 참조 하세요. [Visual Basic의 숨김 기능](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [선언 요소 이름](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [선언 요소의 특징](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
- [변수](../../../../visual-basic/programming-guide/language-features/variables/index.md)
- [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [New 연산자](../../../../visual-basic/language-reference/operators/new-operator.md)
- [공용](../../../../visual-basic/language-reference/modifiers/public.md)
