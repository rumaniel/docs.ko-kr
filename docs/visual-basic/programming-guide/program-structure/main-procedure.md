---
title: Visual Basic의 Main 프로시저
ms.date: 07/20/2015
f1_keywords:
- vb.Main
helpviewer_keywords:
- Main procedure
- Main method [Visual Basic]
- main function
ms.assetid: f0db283e-f283-4464-b521-b90858cc1b44
ms.openlocfilehash: 19c6fcb04a373d782db3deafc732f69bf20e7f0e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962769"
---
# <a name="main-procedure-in-visual-basic"></a>Visual Basic의 Main 프로시저
모든 Visual Basic 응용 프로그램은 라는 `Main`프로시저를 포함 해야 합니다. 이 절차는 응용 프로그램에 대 한 시작 지점 및 전반적인 제어 역할을 합니다. .NET Framework는 응용 프로그램 `Main` 을 로드 하 고 제어를 전달할 준비가 되었을 때 프로시저를 호출 합니다. Windows Forms 응용 프로그램을 만드는 경우를 제외 하 고 자체적으로 `Main` 실행 되는 응용 프로그램에 대 한 프로시저를 작성 해야 합니다.

 `Main`먼저 실행 되는 코드를 포함 합니다. 에서는 `Main`프로그램이 시작 될 때 먼저 로드 되는 폼을 확인 하 고, 응용 프로그램의 복사본이 이미 시스템에서 실행 되 고 있는지 확인 하 고, 응용 프로그램에 대 한 변수 집합을 설정 하거나, 응용 프로그램에 필요한 데이터베이스를 열 수 있습니다.

## <a name="requirements-for-the-main-procedure"></a>주 절차에 대 한 요구 사항
 자체 (일반적으로 확장명 .exe)에서 실행 되는 파일은 프로시저를 `Main` 포함 해야 합니다. 라이브러리 (예: 확장명 .dll)는 자체에서 실행 되지 않으며 `Main` 프로시저가 필요 하지 않습니다. 만들 수 있는 다양 한 프로젝트 형식에 대 한 요구 사항은 다음과 같습니다.

- 콘솔 응용 프로그램은 자체적으로 실행 되며 하나 `Main` 이상의 프로시저를 제공 해야 합니다.

- Windows Forms 응용 프로그램은 자체적으로 실행 됩니다. 그러나 Visual Basic 컴파일러는 이러한 응용 프로그램에서 `Main` 프로시저를 자동으로 생성 하므로 작성 하지 않아도 됩니다.

- 클래스 라이브러리에는 `Main` 프로시저가 필요 하지 않습니다. 여기에는 Windows 컨트롤 라이브러리 및 웹 컨트롤 라이브러리가 포함 됩니다. 웹 응용 프로그램은 클래스 라이브러리로 배포 됩니다.

## <a name="declaring-the-main-procedure"></a>Main 프로시저 선언
 프로시저를 `Main` 선언 하는 방법에는 네 가지가 있습니다. 인수를 사용할 수 있으며 값을 반환할 수 있습니다.

> [!NOTE]
> 클래스에서를 `Main` 선언 하는 경우 키워드를 `Shared` 사용 해야 합니다. 모듈 `Main` 에서는 일 `Shared`필요가 없습니다.

- 가장 간단한 방법은 인수를 사용 하지 `Sub` 않거나 값을 반환 하지 않는 프로시저를 선언 하는 것입니다.

    ```vb
    Module mainModule
        Sub Main()
            MsgBox("The Main procedure is starting the application.")
            ' Insert call to appropriate starting place in your code.
            MsgBox("The application is terminating.")
        End Sub
    End Module
    ```

- `Main`는 운영 체제에서 `Integer` 프로그램의 종료 코드로 사용 하는 값을 반환할 수도 있습니다. 다른 프로그램은 Windows ERRORLEVEL 값을 검사 하 여이 코드를 테스트할 수 있습니다. 종료 코드를 반환 하려면를 프로시저 대신 `Main` `Function` `Sub` 프로시저로 선언 해야 합니다.

    ```vb
    Module mainModule
        Function Main() As Integer
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' Insert call to appropriate starting place in your code.
            ' On return, assign appropriate value to returnValue.
            ' 0 usually means successful completion.
            MsgBox("The application is terminating with error level " &
                 CStr(returnValue) & ".")
            Return returnValue
        End Function
    End Module
    ```

- `Main`는 `String` 배열을 인수로 사용할 수도 있습니다. 배열의 각 문자열은 프로그램을 호출 하는 데 사용 되는 명령줄 인수 중 하나를 포함 합니다. 값에 따라 다른 작업을 수행할 수 있습니다.

    ```vb
    Module mainModule
        Function Main(ByVal cmdArgs() As String) As Integer
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' See if there are any arguments.
            If cmdArgs.Length > 0 Then
                For argNum As Integer = 0 To UBound(cmdArgs, 1)
                    ' Insert code to examine cmdArgs(argNum) and take
                    ' appropriate action based on its value.
                Next
            End If
            ' Insert call to appropriate starting place in your code.
            ' On return, assign appropriate value to returnValue.
            ' 0 usually means successful completion.
            MsgBox("The application is terminating with error level " &
                 CStr(returnValue) & ".")
            Return returnValue
        End Function
    End Module
    ```

- 다음과 같이 명령줄 `Main` 인수를 검사 하지만 종료 코드를 반환 하지 않도록 선언할 수 있습니다.

    ```vb
    Module mainModule
        Sub Main(ByVal cmdArgs() As String)
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' See if there are any arguments.
            If cmdArgs.Length > 0 Then
                For argNum As Integer = 0 To UBound(cmdArgs, 1)
                    ' Insert code to examine cmdArgs(argNum) and take
                    ' appropriate action based on its value.
                Next
            End If
            ' Insert call to appropriate starting place in your code.
            MsgBox("The application is terminating.")
        End Sub
    End Module
    ```
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>
- <xref:System.Array.Length%2A>
- <xref:Microsoft.VisualBasic.Information.UBound%2A>
- [Visual Basic 프로그램의 구조](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)
- [/main](../../../visual-basic/reference/command-line-compiler/main.md)
- [공유](../../../visual-basic/language-reference/modifiers/shared.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Integer 데이터 형식](../../../visual-basic/language-reference/data-types/integer-data-type.md)
- [String 데이터 형식](../../../visual-basic/language-reference/data-types/string-data-type.md)
