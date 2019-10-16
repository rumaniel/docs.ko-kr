---
title: '연습: COM 개체를 사용 하 여 상속 구현 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- inheritance [Visual Basic], COM reusability
- base classes [Visual Basic], COM reusability
- inheritance [Visual Basic], walkthroughs
- derived classes [Visual Basic], COM reusability
ms.assetid: f8e7263a-de13-48d1-b67c-ca1adf3544d9
ms.openlocfilehash: 7cbf71d7a2bbd1e94864e785894fdea41d522486
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053340"
---
# <a name="walkthrough-implementing-inheritance-with-com-objects-visual-basic"></a>연습: COM 개체를 사용 하 여 상속 구현 (Visual Basic)

이전 버전의 Visual Basic에서 만든 `Public` 개체를 비롯 하 여 COM 개체의 클래스에서 Visual Basic 클래스를 파생할 수 있습니다. COM 개체에서 상속 된 클래스의 속성 및 메서드는 다른 기본 클래스의 속성 및 메서드를 재정의 하거나 오버 로드 하는 것 처럼 재정의 하거나 오버 로드할 수 있습니다. COM 개체 로부터의 상속은 다시 컴파일하지 않으려는 기존 클래스 라이브러리가 있는 경우에 유용 합니다.

다음 절차에서는 Visual Basic 6.0를 사용 하 여 클래스가 포함 된 COM 개체를 만든 다음이 개체를 기본 클래스로 사용 하는 방법을 보여 줍니다.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-build-the-com-object-that-is-used-in-this-walkthrough"></a>이 연습에서 사용 되는 COM 개체를 빌드하려면

1. Visual Basic 6.0에서 새 ActiveX DLL 프로젝트를 엽니다. 이라는 `Project1` 프로젝트가 생성 됩니다. 이라는 `Class1`클래스가 있습니다.

2. **프로젝트 탐색기**에서 **Project1**를 마우스 오른쪽 단추로 클릭 한 다음 **Project1 속성**을 클릭 합니다. **프로젝트 속성** 대화 상자가 표시 됩니다.

3. **프로젝트 속성** 대화 상자의 `ComObject1` **일반** 탭에서 **프로젝트 이름** 필드에를 입력 하 여 프로젝트 이름을 변경 합니다.

4. **프로젝트 탐색기**에서를 마우스 오른쪽 단추로 클릭 `Class1`한 다음 **속성**을 클릭 합니다. 클래스에 대 한 **속성** 창이 표시 됩니다.

5. 속성을로 `MathFunctions`변경 합니다. `Name`

6. **프로젝트 탐색기**에서를 마우스 오른쪽 단추로 클릭 `MathFunctions`한 다음 **코드 보기**를 클릭 합니다. **코드 편집기** 가 표시 됩니다.

7. 속성 값을 보유할 지역 변수를 추가 합니다.

    ```vb
    ' Local variable to hold property value
    Private mvarProp1 As Integer
    ```

8. 속성 `Let` 및 속성 `Get` 속성 프로시저를 추가 합니다.

    ```vb
    Public Property Let Prop1(ByVal vData As Integer)
       'Used when assigning a value to the property.
       mvarProp1 = vData
    End Property
    Public Property Get Prop1() As Integer
       'Used when retrieving a property's value.
       Prop1 = mvarProp1
    End Property
    ```

9. 함수를 추가 합니다.

    ```vb
    Function AddNumbers(
       ByVal SomeNumber As Integer,
       ByVal AnotherNumber As Integer) As Integer

       AddNumbers = SomeNumber + AnotherNumber
    End Function
    ```

10. **파일** 메뉴에서 **ComObject1 만들기** 를 클릭 하 여 COM 개체를 만들고 등록 합니다.

    > [!NOTE]
    > Visual Basic를 사용 하 여 만든 클래스를 COM 개체로 노출할 수도 있지만이 클래스는 진정한 COM 개체가 아니므로이 연습에서 사용할 수 없습니다. 자세한 내용은 참조 하세요 [.NET Framework 애플리케이션의 COM 상호 운용성](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)합니다.

## <a name="interop-assemblies"></a>Interop 어셈블리

다음 절차에서는 비관리 코드 (예: COM 개체)와 Visual Studio가 사용 하는 관리 코드 간의 브리지 역할을 하는 interop 어셈블리를 만듭니다. Visual Basic 생성 하는 interop 어셈블리는 com 개체와 상호 작용 하는 것과 같은 COM 개체 작업에 대 한 세부 정보 (예: *interop 마샬링*)를 처리 합니다. Visual Basic 응용 프로그램의 참조는 실제 COM 개체가 아닌 interop 어셈블리를 가리킵니다.

### <a name="to-use-a-com-object-with-visual-basic-2005-and-later-versions"></a>Visual Basic 2005 이상 버전에서 COM 개체를 사용 하려면

1. 새 Visual Basic Windows 애플리케이션 프로젝트를 엽니다.

2. **프로젝트** 메뉴에서 **참조 추가**를 클릭합니다.

     **참조 추가** 대화 상자가 표시됩니다.

3. **COM** 탭에서 **구성 요소 이름** 목록을 두 `ComObject1` 번 클릭 하 고 **확인**을 클릭 합니다.

4. **프로젝트** 메뉴에서 **새 항목 추가**를 클릭합니다.

     **새 항목 추가** 대화 상자가 표시됩니다.

5. **템플릿** 창에서 **클래스**를 클릭 합니다.

     기본 파일 이름인 `Class1.vb`는 **이름** 필드에 표시 됩니다. 이 필드를 MathClass로 변경 하 고 **추가**를 클릭 합니다. 그러면 이라는 `MathClass`클래스가 만들어지고 해당 코드가 표시 됩니다.

6. 다음 코드를의 `MathClass` 맨 위에 추가 하 여 COM 클래스에서 상속 합니다.

     [!code-vb[VbVbalrInterop#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#31)]

7. 에 `MathClass`다음 코드를 추가 하 여 기본 클래스의 public 메서드를 오버 로드 합니다.

     [!code-vb[VbVbalrInterop#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#32)]

8. 다음 코드를에 `MathClass`추가 하 여 상속 된 클래스를 확장 합니다.

     [!code-vb[VbVbalrInterop#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#33)]

새 클래스는 COM 개체의 기본 클래스 속성을 상속 하 고, 메서드를 오버 로드 하 고, 클래스를 확장 하는 새 메서드를 정의 합니다.

### <a name="to-test-the-inherited-class"></a>상속 된 클래스를 테스트 하려면

1. 시작 폼에 단추를 추가 하 고 두 번 클릭 하 여 해당 코드를 확인 합니다.

2. 단추의 `Click` 이벤트 처리기 프로시저에서 다음 코드를 추가 하 여의 `MathClass` 인스턴스를 만들고 오버 로드 된 메서드를 호출 합니다.

     [!code-vb[VbVbalrInterop#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#34)]

3. F5 키를 눌러 프로젝트를 실행 합니다.

폼 `AddNumbers` 에서 단추를 클릭 하면 메서드가 먼저 데이터 형식 번호를 사용 하 여 `Short` 호출 되 고 Visual Basic 기본 클래스에서 적절 한 메서드를 선택 합니다. 에 대 한 `AddNumbers` 두 번째 호출은에서 `MathClass`오버 로드 메서드로 전달 됩니다. 세 번째 호출은 클래스를 `SubtractNumbers` 확장 하는 메서드를 호출 합니다. 기본 클래스의 속성이 설정 되 고 값이 표시 됩니다.

## <a name="next-steps"></a>다음 단계

오버 로드 `AddNumbers` 된 함수가 COM 개체의 기본 클래스에서 상속 된 메서드와 동일한 데이터 형식으로 표시 되는 것을 알 수 있습니다. 이는 Visual Basic 6.0에서 기본 클래스 메서드의 인수와 매개 변수가 16 비트 정수로 정의 되어 있지만 이후 버전의 Visual Basic에서 형식의 `Short` 16 비트 정수로 노출 되기 때문입니다. 새 함수는 32 비트 정수를 허용 하 고 기본 클래스 함수를 오버 로드 합니다.

COM 개체를 사용 하는 경우 매개 변수의 크기 및 데이터 형식을 확인 해야 합니다. 예를 들어 Visual Basic 6.0 컬렉션 개체를 인수로 허용 하는 COM 개체를 사용 하는 경우 Visual Basic의 이후 버전에서 컬렉션을 제공할 수 없습니다.

COM 클래스에서 상속 된 속성 및 메서드를 재정의할 수 있습니다. 즉, 기본 COM 클래스에서 상속 된 속성이 나 메서드를 대체 하는 로컬 속성 또는 메서드를 선언할 수 있습니다. 상속 된 COM 속성을 재정의 하는 규칙은 다음과 같은 예외를 제외 하 고 다른 속성 및 메서드를 재정의 하는 규칙과 비슷합니다.

- COM 클래스에서 상속 된 속성 또는 메서드를 재정의 하는 경우 상속 된 다른 모든 속성과 메서드를 재정의 해야 합니다.

- 매개 변수를 `ByRef` 사용 하는 속성은 재정의할 수 없습니다.

## <a name="see-also"></a>참고자료

- [.NET Framework 응용 프로그램의 COM 상호 운용성](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)
- [Inherits 문](../../../visual-basic/language-reference/statements/inherits-statement.md)
- [Short 데이터 형식](../../../visual-basic/language-reference/data-types/short-data-type.md)
