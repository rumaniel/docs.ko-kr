---
title: On Error 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.OnError
helpviewer_keywords:
- Visual Basic code, control flow
- Resume Next statement [Visual Basic]
- errors [Visual Basic], trapping
- error handling, On Error statement
- Next statement [Visual Basic], On Error
- control flow [Visual Basic], branching
- Error keyword [Visual Basic]
- execution [Visual Basic], conditional
- Resume statement [Visual Basic], and On Error statement
- Error statement [Visual Basic], and On Error statement
- GoTo statement [Visual Basic], and On Error statement
- branching [Visual Basic], on error
- conditional statements [Visual Basic], On Error
- On Error statement [Visual Basic], syntax
- On keyword [Visual Basic]
- run-time errors [Visual Basic], handling
- On Error statement [Visual Basic]
ms.assetid: ff947930-fb84-40cf-bd66-1ea219561d5c
ms.openlocfilehash: 4474b217147aca74f2c6e5376c8f55318a05bf4a
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046509"
---
# <a name="on-error-statement-visual-basic"></a>On Error 문(Visual Basic)
오류 처리 루틴을 사용 하도록 설정 하 고 프로시저 내에서 루틴의 위치를 지정 합니다. 를 사용 하 여 오류 처리 루틴을 사용 하지 않도록 설정할 수도 있습니다. `On Error` 문은 비구조적 오류 처리에 사용 되며 구조적 예외 처리 대신 사용할 수 있습니다. [구조적 예외 처리](../../../standard/exceptions/index.md) 는 .net에 기본 제공 되며, 일반적으로 더 효율적 이므로 응용 프로그램에서 런타임 오류를 처리할 때 권장 됩니다.

 오류 처리 또는 예외 처리를 사용 하지 않을 경우 발생 하는 런타임 오류는 심각한 오류입니다. 오류 메시지가 표시 되 고 실행이 중지 됩니다.

> [!NOTE]
> 키워드는 이전 버전과의 호환성을 위해 지원 되는 [오류 문에서](../../../visual-basic/language-reference/statements/error-statement.md)도 사용 됩니다. `Error`

## <a name="syntax"></a>구문

```vb
On Error { GoTo [ line | 0 | -1 ] | Resume Next }
```

## <a name="parts"></a>요소

|용어|정의|
|---|---|
|`GoTo`*줄*|필요한 *줄* 인수에 지정 된 줄에서 시작 하는 오류 처리 루틴을 사용 하도록 설정 합니다. *줄* 인수는 줄 레이블이나 줄 번호입니다. 런타임 오류가 발생 하는 경우 지정 된 줄로 분기를 제어 하 여 오류 처리기를 활성화 합니다. 지정 된 줄은 `On Error` 문과 같은 프로시저에 있거나 컴파일 타임 오류가 발생 합니다.|
|`GoTo 0`|현재 프로시저에서 활성화 된 오류 처리기를 비활성화 하 고로 `Nothing`다시 설정 합니다.|
|`GoTo -1`|현재 프로시저에서 활성화 된 예외를 비활성화 하 고로 `Nothing`다시 설정 합니다.|
|`Resume Next`|런타임 오류가 발생할 때 제어가 오류가 발생 한 문 바로 다음에 오는 문으로 이동 하 고 해당 지점에서 실행이 계속 되도록 지정 합니다. 개체에 액세스할 `On Error GoTo` 때가 아닌이 폼을 사용 합니다.|

## <a name="remarks"></a>설명

> [!NOTE]
> 구조화 되지 않은 예외 처리 및 `On Error` 문을 사용 하는 대신 가능한 경우 코드에서 구조적 예외 처리를 사용 하는 것이 좋습니다. 자세한 내용은 [Try...Catch...Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)을 참조하세요.

 "활성화 된" 오류 처리기는 `On Error` 문에 의해 설정 되는 오류 처리기입니다. "활성" 오류 처리기는 오류를 처리 하는 프로세스에 있는 활성화 된 처리기입니다.

 오류 처리기가 활성화 되어 있는 동안 오류가 발생 하는 경우 (오류 `Resume`발생과 `Exit Function`, `Exit Sub`, 또는 `Exit Property` 문 사이) 현재 프로시저의 오류 처리기에서 오류를 처리할 수 없습니다. 호출 하는 프로시저로 제어가 반환 됩니다.
  
 호출 하는 프로시저에 활성화 된 오류 처리기가 있으면 오류를 처리 하도록 활성화 됩니다. 호출 하는 프로시저의 오류 처리기도 활성 상태인 경우에는 사용 되지만 비활성화 된 오류 처리기가 발견 될 때까지 이전 호출 프로시저를 통해 제어가 다시 전달 됩니다. 이러한 오류 처리기를 찾을 수 없는 경우 오류는 실제로 발생 한 지점에서 치명적입니다.
  
 오류 처리기가 호출 프로시저로 제어를 다시 전달할 때마다 해당 프로시저는 현재 프로시저가 됩니다. 프로시저의 오류 처리기에서 오류를 처리 한 후에는 `Resume` 문에 지정 된 지점에서 현재 프로시저의 실행이 다시 시작 됩니다.
  
> [!NOTE]
> 오류 처리 루틴은 `Sub` 프로시저 `Function` 또는 프로시저가 아닙니다. 줄 레이블이나 줄 번호로 표시 되는 코드 섹션입니다.
  
## <a name="number-property"></a>Number 속성
 오류 처리 루틴은 `Number` `Err` 개체의 속성 값을 사용 하 여 오류의 원인을 확인 합니다. 루틴은 다른 오류가 발생 하기 전이나 오류를 발생 시킬 `Err` 수 있는 프로시저를 호출 하기 전에 개체의 관련 속성 값을 테스트 하거나 저장 해야 합니다. `Err` 개체의 속성 값에는 가장 최근의 오류만 반영 됩니다. 와 `Err.Number` 관련 된 오류 메시지는에 `Err.Description`포함 되어 있습니다.  
  
## <a name="throw-statement"></a>Throw 문  
 `Err.Raise` 메서드에서 발생 하는 오류는 `Exception` 속성을 <xref:System.Exception> 클래스의 새로 만든 인스턴스로 설정 합니다. 파생 된 예외 형식의 `Throw` 예외 발생을 지원 하기 위해 문은 언어로 지원 됩니다. 이는 throw 되는 예외 인스턴스인 단일 매개 변수를 사용 합니다. 다음 예제에서는 기존 예외 처리 지원과 함께 이러한 기능을 사용할 수 있는 방법을 보여 줍니다.

 [!code-vb[VbVbalrErrorHandling#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#17)]  
  
 `On Error GoTo` 문은 예외 클래스에 관계 없이 모든 오류를 트래핑 합니다.
  
## <a name="on-error-resume-next"></a>오류 다시 시작 다음
 `On Error Resume Next`실행 시 오류가 발생 한 문 바로 다음에 오는 문을 실행 하거나 문을 포함 하 `On Error Resume Next` 는 프로시저에서 가장 최근의 호출 바로 다음에 오는 문으로 실행을 계속 합니다. 이 문을 사용 하면 런타임 오류에도 불구 하 고 실행을 계속할 수 있습니다. 프로시저 내의 다른 위치로 제어를 전송 하는 대신 오류가 발생 하는 오류 처리 루틴을 저장할 수 있습니다. 다른 프로시저가 호출 될 때 `On Error Resume Next` 문이비활성화되므로해당루틴내에서인라인오류를처리하려는경우호출된각루틴에서문을실행해야합니다.`On Error Resume Next`
  
> [!NOTE]
> 합니다 `On Error Resume Next` 구문에 더 적합할 수 있습니다 `On Error GoTo` 다른 개체에 액세스 하는 동안 발생 한 오류를 처리 하는 경우. 개체 `Err` 와의 각 상호 작용 후에 확인 하면 코드에서 액세스 된 개체에 대 한 모호성을 제거 합니다. 오류 코드 `Err.Number`를 배치 하는 개체와 원래 오류를 생성 한 개체 (에 `Err.Source`지정 된 개체)를 확인할 수 있습니다.

## <a name="on-error-goto-0"></a>On Error GoTo 0
 `On Error GoTo 0`현재 프로시저에서 오류 처리를 사용 하지 않도록 설정 합니다. 오류 처리 코드의 시작으로 줄 0을 지정 하지 않습니다. 프로시저에 번호가 0 인 줄이 포함 된 경우에도 마찬가지입니다. `On Error GoTo 0` 문이 없으면 프로시저 종료 시 오류 처리기가 자동으로 비활성화 됩니다.

## <a name="on-error-goto--1"></a>On Error GoTo-1
 `On Error GoTo -1`현재 프로시저에서 예외를 사용 하지 않도록 설정 합니다. 프로시저에-1로 번호가 지정 된 줄이 포함 된 경우에도 줄 1은 오류 처리 코드의 시작으로 지정 되지 않습니다. `On Error GoTo -1` 문이 없으면 프로시저를 종료할 때 예외가 자동으로 비활성화 됩니다.

 오류가 발생 하지 않은 경우 오류 처리 코드가 실행 되지 않도록 하려면 다음 조각과 같이 오류 `Exit Sub`처리 `Exit Function`루틴 바로 `Exit Property` 앞에, 또는 문을 추가 합니다.

 [!code-vb[VbVbalrErrorHandling#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#18)]

 여기에서 오류 처리 코드는 `Exit Sub` 문 뒤에 오는 `End Sub` 문 앞에 프로시저 흐름과 구분 됩니다. 프로시저의 아무 곳에 나 오류 처리 코드를 넣을 수 있습니다.

## <a name="untrapped-errors"></a>포착 되지 않은 오류
 개체를 실행 파일로 실행 하는 경우 개체의 포착 되지 않은 오류는 제어 응용 프로그램으로 반환 됩니다. 개발 환경 내에서 적절 한 옵션이 설정 된 경우에만 포착 되지 않은 오류가 제어 응용 프로그램으로 반환 됩니다. 디버깅 중에 설정 해야 하는 옵션에 대 한 설명, 설정 하는 방법 및 호스트가 클래스를 만들 수 있는지 여부는 호스트 응용 프로그램의 설명서를 참조 하세요.

 다른 개체에 액세스 하는 개체를 만드는 경우 다시 전달 되는 처리 되지 않은 오류를 처리 해야 합니다. 사용할 수 없는 경우의 `Err.Number` 오류 코드를 고유한 오류 중 하나에 매핑한 다음 개체의 호출자에 게 다시 전달 합니다. `VbObjectError` 상수에 오류 코드를 추가 하 여 오류를 지정 해야 합니다. 예를 들어 오류 코드가 1052 인 경우 다음과 같이 할당 합니다.

 [!code-vb[VbVbalrErrorHandling#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#19)]

> [!CAUTION]
> Windows Dll (동적 연결 라이브러리)을 호출 하는 동안 발생 하는 시스템 오류는 예외를 발생 시 키 지 않으며 Visual Basic 오류 트래핑으로 트랩할 수 없습니다. DLL 함수를 호출 하는 경우 각 반환 값에 성공 또는 실패 (API 사양에 따라)를 확인 하 고, 실패 시 `Err` 개체의 `LastDLLError` 속성에서 값을 확인 해야 합니다.

## <a name="example"></a>예제
 이 예에서는 먼저 `On Error GoTo` 문을 사용 하 여 프로시저 내에서 오류 처리 루틴의 위치를 지정 합니다. 이 예에서는 0으로 나누려고 시도 하면 오류 번호 6이 생성 됩니다. 오류는 오류 처리 루틴에서 처리 되 고 컨트롤은 오류를 발생 시킨 문으로 반환 됩니다. `On Error GoTo 0` 문은 오류 트래핑을 해제 합니다. 그런 다음 `On Error Resume Next` 문을 사용 하 여 다음 문에 의해 생성 된 오류에 대 한 컨텍스트를 특정에 대해 알 수 있도록 오류 트래핑을 지연 시킵니다. 는 오류를 처리 한 후 `Err` 개체의 속성을 지우는 데 사용 됩니다.`Err.Clear`

 [!code-vb[VbVbalrErrorHandling#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#20)]

## <a name="requirements"></a>요구 사항
 **네임스페이스:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)

 **어셈블리** Visual Basic 런타임 라이브러리(Microsoft.VisualBasic.dll)

## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Number%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Description%2A>
- <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>
- [End 문](../../../visual-basic/language-reference/statements/end-statement.md)
- [Exit 문](../../../visual-basic/language-reference/statements/exit-statement.md)
- [Resume 문](../../../visual-basic/language-reference/statements/resume-statement.md)
- [오류 메시지](../../../visual-basic/language-reference/error-messages/index.md)
- [Try...Catch...Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
