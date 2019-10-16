---
title: '방법: 부호 없는 형식을 사용 하는 Windows 함수 호출 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- Windows functions [Visual Basic], calling
- unsigned data types [Visual Basic]
- UShort data type [Visual Basic], using
- functions [Visual Basic], calling Windows functions
- ULong data type [Visual Basic], using
- UInteger data type [Visual Basic], using
- data types [Visual Basic], using
- unsigned types [Visual Basic]
- data types [Visual Basic], unsigned
- data types [Visual Basic], numeric
- unsigned types [Visual Basic], using
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
ms.openlocfilehash: 97075fb6149ed8c0ce06318d0e5bb6f01b841f30
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053320"
---
# <a name="how-to-call-a-windows-function-that-takes-unsigned-types-visual-basic"></a>방법: 부호 없는 형식을 사용 하는 Windows 함수 호출 (Visual Basic)

부호 없는 정수 형식의 멤버를 포함 하는 클래스, 모듈 또는 구조체를 사용 하는 경우 Visual Basic를 사용 하 여 이러한 멤버에 액세스할 수 있습니다.

## <a name="to-call-a-windows-function-that-takes-an-unsigned-type"></a>부호 없는 형식을 사용 하는 Windows 함수를 호출 하려면

1. [Declare 문을](../../../visual-basic/language-reference/statements/declare-statement.md) 사용 하 여 함수를 포함 하는 라이브러리, 해당 라이브러리에 있는 이름, 호출 하는 시퀀스의 정의, 호출 시 문자열을 변환 하는 방법에 대 한 Visual Basic를 알려 줍니다.

2. `UInteger` 문에서는`ULong`,, 또는 를`Byte` 부호 없는 형식의 각 매개 변수에 적합 하 게 사용 합니다. `UShort` `Declare`

3. 호출 하는 Windows 함수 설명서를 참조 하 여 사용 하는 상수의 이름과 값을 확인 합니다. 이러한 중 상당수는 Winuser.h 파일에 정의 되어 있습니다.

4. 코드에서 필요한 상수를 선언 합니다. 많은 Windows 상수는 32 비트 부호 없는 값 이며, 이러한 `As UInteger`값을 선언 해야 합니다.

5. 일반적인 방법으로 함수를 호출 합니다. 다음 예제에서는 부호 없는 정수 인수 `MessageBox`를 사용 하는 Windows 함수를 호출 합니다.

    ```vb
    Public Class windowsMessage
        Private Declare Auto Function mb Lib "user32.dll" Alias "MessageBox" (
            ByVal hWnd As Integer,
            ByVal lpText As String,
            ByVal lpCaption As String,
            ByVal uType As UInteger) As Integer
        Private Const MB_OK As UInteger = 0
        Private Const MB_ICONEXCLAMATION As UInteger = &H30
        Private Const IDOK As UInteger = 1
        Private Const IDCLOSE As UInteger = 8
        Private Const c As UInteger = MB_OK Or MB_ICONEXCLAMATION
        Public Function messageThroughWindows() As String
            Dim r As Integer = mb(0, "Click OK if you see this!",
                "Windows API call", c)
            Dim s As String = "Windows API MessageBox returned " &
                 CStr(r)& vbCrLf & "(IDOK = " & CStr(IDOK) &
                 ", IDCLOSE = " & CStr(IDCLOSE) & ")"
            Return s
        End Function
    End Class
    ```

     다음 코드를 사용 하 `messageThroughWindows` 여 함수를 테스트할 수 있습니다.

    ```vb
    Public Sub consumeWindowsMessage()
        Dim w As New windowsMessage
        w.messageThroughWindows()
    End Sub
    ```

    > [!CAUTION]
    > `UInteger` ,`ULong`, 및 데이터`SByte` 형식은 [언어 독립성 및 언어 독립적 구성 요소](../../../standard/language-independence-and-language-independent-components.md) (cls)의 일부가 아니므로 cls 규격 코드는이를 사용 하는 구성 요소를 사용할 수 없습니다. `UShort`

    > [!IMPORTANT]
    > Windows API (응용 프로그래밍 인터페이스)와 같은 비관리 코드에 대 한 호출을 수행 하면 잠재적인 보안 위험에 대 한 코드를 노출 합니다.

    > [!IMPORTANT]
    > Windows API를 호출 하려면 부분 신뢰 상황에서 실행에 영향을 줄 수 있는 비관리 코드 권한이 필요 합니다. 자세한 내용은 <xref:System.Security.Permissions.SecurityPermission> 하 고 [코드 액세스 권한](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h846e9b3(v=vs.100))합니다.

## <a name="see-also"></a>참고자료

- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [Integer 데이터 형식](../../../visual-basic/language-reference/data-types/integer-data-type.md)
- [UInteger 데이터 형식](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)
- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)
- [연습: Windows API 호출](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
