---
title: 시도 중... Catch 하는 중... 마지막 문-Visual Basic
description: Visual Basic Try/Catch/Finally 문을 사용 하 여 처리 하는 예외를 사용 하는 방법을 알아봅니다.
ms.date: 12/07/2018
f1_keywords:
- vb.Try...Catch...Finally
- vb.when
- vb.Finally
- vb.Catch
- vb.Try
helpviewer_keywords:
- Try...Catch...Finally statements
- Try statement [Visual Basic]
- try-catch exception handling, Try...Catch...Finally statements
- error handling, while running code
- Try statement [Visual Basic], Try...Catch...Finally
- Finally keyword [Visual Basic], Try...Catch...Finally
- Catch statement [Visual Basic]
- When keyword [Visual Basic]
- Visual Basic code, handling errors while running
- structured exception handling, Try...Catch...Finally statements
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
ms.custom: seodec18
ms.openlocfilehash: 126f20c86bb47e8002382e069ce6236600394aba
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65638765"
---
# <a name="trycatchfinally-statement-visual-basic"></a>Try...Catch...Finally 문(Visual Basic)

코드 블록에서 계속 코드를 실행 하는 동안 발생할 수 있는 일부 또는 모든 가능한 오류를 처리 하는 방법을 제공 합니다.

## <a name="syntax"></a>구문

```vb
Try
    [ tryStatements ]
    [ Exit Try ]
[ Catch [ exception [ As type ] ] [ When expression ]
    [ catchStatements ]
    [ Exit Try ] ]
[ Catch ... ]
[ Finally
    [ finallyStatements ] ]
End Try
```

## <a name="parts"></a>요소

|용어|정의|
|---|---|
|`tryStatements`|선택 사항입니다. 오류가 발생할 수 있는 문. 복합 문일 수 있습니다.|
|`Catch`|선택 사항입니다. 여러 `Catch` 블록을 사용할 수 있습니다. 처리 하는 동안 예외가 발생 하는 경우는 `Try` 각 차단 `Catch` 문을 사용 하 여 예외를 처리 하는지 여부를 확인 하려면 텍스트 순서 대로 검사 `exception` throw 된 예외를 나타내는입니다.|
|`exception`|선택 사항입니다. 임의의 변수 이름입니다. `exception`의 초기 값은 throw된 오류 값입니다. 사용한 `Catch` 발생 한 예외를 지정 합니다. 생략 된 `Catch` 문은 예외를 catch 합니다.|
|`type`|선택 사항입니다. 클래스 필터의 형식을 지정합니다. 경우 값 `exception` 으로 지정 된 형식의 `type` 또는 파생 형식의 식별자가 예외 개체에 바인딩됩니다.|
|`When`|선택 사항입니다. A `Catch` 문을 사용 하 여는 `When` 절에서 예외를 catch 경우에만 `expression` 로 `True`합니다. A `When` 절이 예외 형식을 확인 한 다음에 적용 됩니다 및 `expression` 예외를 나타내는 식별자를 참조할 수 있습니다.|
|`expression`|선택 사항입니다. 암시적으로 변환할 수 있어야 `Boolean`합니다. 일반 필터를 설명 하는 모든 식입니다. 일반적으로 필터링 하는 데 오류 번호입니다. 사용한 `When` 키워드는 오류가 발생 하는 상황을 지정 합니다.|
|`catchStatements`|선택 사항입니다. 연결에서 발생 하는 오류를 처리 하는 문 `Try` 블록입니다. 복합 문일 수 있습니다.|
|`Exit Try`|선택 사항입니다. 밖으로 중단 되는 키워드는 `Try...Catch...Finally` 구조입니다. 바로 다음 코드를 사용 하 여 실행을 다시 시작을 `End Try` 문입니다. `Finally` 문을 계속 실행 됩니다. 에 사용할 수 없습니다 `Finally` 블록입니다.|
|`Finally`|선택 사항입니다. A `Finally` 블록은 실행의 모든 부분을 벗어날 때 항상 실행을 `Try...Catch` 문.|
|`finallyStatements`|선택 사항입니다. 다른 모든 오류 처리를 수행한 후 실행 되는 문입니다.|
|`End Try`|종료는 `Try...Catch...Finally` 구조입니다.|

## <a name="remarks"></a>설명

특정 예외를 코드의 특정 섹션을 하는 동안 발생할 수는 예상 되는 경우에 코드를 입력 한 `Try` 차단 하 고 사용 하 여를 `Catch` 제어를 유지할 경우 예외를 처리 하는 블록.

A `Try…Catch` 문은 구성 됩니다는 `Try` 블록 뒤에 하나 이상의 `Catch` 다양 한 예외에 대 한 처리기를 지정 하는 절. 예외가 throw 되는 경우는 `Try` 차단, Visual Basic 찾습니다는 `Catch` 예외를 처리 하는 문입니다. 일치 하는 경우 `Catch` 문을 찾을 수 없습니다, Visual Basic 호출 스택 위로 등 현재 메서드를 호출 하는 메서드를 검사 합니다. 없으면 `Catch` 블록이 발견, Visual Basic 처리 되지 않은 예외 메시지가 사용자에 게 표시 하 고 프로그램의 실행을 중지 합니다.

둘 이상 사용할 수 있습니다 `Catch` 문에서 `Try…Catch` 문입니다. 이 순서는 `Catch` 절 순서 대로 검사 되므로 유효 합니다. 더 구체적인 예외를 덜 구체적인 예외보다 먼저 catch합니다.

다음 `Catch` 문 조건은 가장 덜 구체적인 하며 모든 뒤쳐지면에서 파생 되는 예외는 <xref:System.Exception> 클래스입니다. 마지막으로 이러한 종류의 일반적으로 사용 해야 `Catch` 블록을 `Try...Catch...Finally` 원하는 모든 특정 예외를 catch 한 후 구조입니다. 제어 흐름에 절대로 도달할 수는 `Catch` 이러한 변형이 하나 뒤에 오는 블록입니다.

- 합니다 `type` 는 `Exception`예를 들어: `Catch ex As Exception`

- 문이 아무런 `exception` 예를 들어 변수: `Catch`

경우는 `Try…Catch…Finally` 다른 문이 중첩 되 `Try` 블록, Visual Basic에 각 항목을 먼저 검사 `Catch` 문은 가장 안쪽에서 `Try` 블록입니다. 일치 하는 경우 `Catch` 문이 있으면, 검색을 진행 합니다 `Catch` 문 외부의 `Try…Catch…Finally` 블록.

로컬 변수를 `Try` 블록에서 사용할 수 없는 `Catch` 별도 요소 이기 때문에 차단 합니다. 둘 이상의 블록에서 변수를 사용 하려는 경우 외부 변수를 선언 합니다 `Try...Catch...Finally` 구조입니다.

> [!TIP]
> `Try…Catch…Finally` 문을 IntelliSense 코드 조각으로 사용할 수는 있습니다. 코드 조각 관리자에서 확장 **코드 패턴-If, For Each, Try Catch, 속성 등**를 차례로 **오류 처리 (예외)** 합니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.

## <a name="finally-block"></a>Finally 블록

종료 하기 전에 실행 해야 하는 하나 이상의 문이 있는 경우는 `Try` 구조체를 사용 하 여를 `Finally` 블록입니다. 컨트롤을 전달 합니다 `Finally` 블록 밖으로 전달 하기 직전는 `Try…Catch` 구조입니다. 내에서 예외가 발생 하는 경우에 마찬가지 여 `Try` 구조입니다.

`Finally` 블록은 예외가 발생 하는 경우에 실행 해야 하는 모든 코드를 실행 한 경우에 유용 합니다. 컨트롤에 전달 되는 `Finally` 블록에 관계 없이 `Try...Catch` 종료를 차단 합니다.

코드를 `Finally` 코드에서 발견 하는 경우에 블록이 실행을 `Return` 문에서 `Try` 또는 `Catch` 블록. 컨트롤에서 전달 하지 않습니다는 `Try` 또는 `Catch` 블록에서 해당 `Finally` 다음과 같은 경우 차단 합니다.

- [End 문](end-statement.md) 발견 되는 `Try` 또는 `Catch` 블록입니다.

- A <xref:System.StackOverflowException> 에서 throw 되는 `Try` 또는 `Catch` 블록입니다.

에 실행을 명시적으로 전송할 올바르지는 `Finally` 블록입니다. 전송의 실행을 `Finally` 블록이 예외 사항을 제외 하 고 잘못 되었습니다.

경우는 `Try` 문을 하나 이상 포함 하지 않는 `Catch` 블록을 포함 해야 합니다는 `Finally` 블록입니다.

> [!TIP]
> 특정 예외를 catch 하지 않은 경우는 `Using` 문 처럼는 `Try…Finally` 블록과 블록을 종료 하는 방법에 관계 없이 리소스를 삭제할 수 있습니다. 처리 되지 않은 예외를 사용 하 여도 마찬가지입니다. 자세한 내용은 [using 문](using-statement.md)을 참조하세요.

## <a name="exception-argument"></a>예외 인수

`Catch` 블록 `exception` 인수가의 인스턴스를 <xref:System.Exception> 클래스 또는 클래스에서 파생 되는 `Exception` 클래스입니다. 합니다 `Exception` 에서 발생 한 오류에 해당 하는 클래스 인스턴스는 `Try` 블록입니다.

속성을 `Exception` 개체 원인과 예외가 위치의 하는 데 도움이 됩니다. 예를 들어를 <xref:System.Exception.StackTrace%2A> 속성 오류 코드에서 발생 하는 위치를 찾을 수 있도록 예외를 발생 시킨 호출된 메서드를 보여 줍니다. <xref:System.Exception.Message%2A> 예외를 설명 하는 메시지를 반환 합니다. <xref:System.Exception.HelpLink%2A> 연결된 된 도움말 파일에 대 한 링크를 반환합니다. <xref:System.Exception.InnerException%2A> 반환 합니다 `Exception` 현재 예외를 발생 시킨 개체를 반환 합니다 `Nothing` 원본 있으면 `Exception`합니다.

## <a name="considerations-when-using-a-trycatch-statement"></a>Try 사용 시 고려 사항 중... Catch 문

사용 하 여를 `Try…Catch` 만 발생을 알리는 비정상적인 또는 예기치 않은 프로그램 이벤트는 문입니다. 이 문제의 원인은 다음과 같습니다.

- 런타임 시 예외를 catch 추가 오버 헤드를 만들고 예외를 방지 하기 위해 미리 확인 하는 보다 느려질 가능성이 있습니다.

- 경우는 `Catch` 블록을 올바르게 처리 하지 않으면, 사용자에 게 예외를 올바르게 보고 되지 않을 수 있습니다.

- 예외 처리를 사용 하면 프로그램이 더 복잡 합니다.

항상 필요 하지 않습니다는 `Try…Catch` 발생할 가능성이 있는 조건을 확인 하는 문이 있습니다. 다음 예제에서는 파일을 열기 전에 있는지 확인 합니다. throw 된 예외를 catch 하는 것에 대 한 필요를 줄여이 <xref:System.IO.File.OpenText%2A> 메서드.

[!code-vb[VbVbalrStatements#94](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#94)]

해당 코드를 확인 `Catch` 블록 스레드로부터 안전한 로깅 또는 적절 한 메시지 통해 사용자에 게 예외를 올바르게 보고할 수 있습니다. 그렇지 않으면 예외는 알 수 없는 남아 있을 수 있습니다.

## <a name="async-methods"></a>비동기 메서드

메서드를 사용 하 여 표시 하는 경우는 [비동기](../modifiers/async.md) 한정자를 사용할 수는 [Await](../operators/await-operator.md) 메서드에서 연산자입니다. 사용 하 여 문을 여 `Await` 연산자는 대기 중인된 작업이 완료 될 때까지 메서드의 실행을 일시 중단 합니다. 작업은 진행 중인 작업을 나타냅니다. 경우 연관 된 태스크는 `Await` 연산자 완료 되 면 동일한 메서드에서 실행 다시 시작 합니다. 자세한 내용은 [비동기 프로그램의 제어 흐름](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)합니다.

비동기 메서드에서 반환 하는 작업 처리 되지 않은 예외로 인해 완료 되었는지 나타내는 faulted 상태의 종료 될 수 있습니다. 취소 된 상태로 작업을 종료할 수 있습니다는 `OperationCanceledException` await 식에서 throw 됩니다. 두 가지 형식의 예외를 catch 하려면 배치 합니다 `Await` 식에서 해당 작업을 연관 된를 `Try` 블록 및 예외를 catch를 `Catch` 블록. 예제는이 항목의 뒷부분에 제공 됩니다.

여러 예외가 해당 오류에 대 한 책임 되었기 때문에 작업을 faulted 상태로 될 수 있습니다. 예를 들어 작업은 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 호출의 결과일 수 있습니다. 이러한 작업을 기다릴 때 예외가 예외 중 하나만 이며 예외를 포착는 예측할 수 없습니다. 예제는이 항목의 뒷부분에 제공 됩니다.

`Await` 식 내에 있을 수 없습니다.을 `Catch` 블록 또는 `Finally` 블록입니다.

## <a name="iterators"></a>반복기

반복기 함수 또는 `Get` 접근자 컬렉션 사용자 지정 반복을 수행 합니다. 반복기를 사용 하는 [Yield](yield-statement.md) 문을 한 번에 하나씩 컬렉션의 각 요소를 반환 합니다. 반복기 함수를 사용 하 여 호출을 [각각에 대 한 중... 다음 문을](for-each-next-statement.md)합니다.

A `Yield` 문 내에 있을 수는 `Try` 블록입니다. A `Try` 포함 된 블록을 `Yield` 문의 `Catch` 블록을 가질 수 있습니다를 `Finally` 블록. "Visual Basic에서 시도 블록" 섹션을 참조 하세요 [반복기](../../programming-guide/concepts/iterators.md) 예입니다.

A `Yield` 문 내에 있을 수 없습니다.을 `Catch` 블록 또는 `Finally` 블록입니다.

경우는 `For Each` 본문 (반복기 함수) 외부에서 예외를 throw를 `Catch` 반복기 함수에는 블록이 실행 되지 않습니다 하지만 `Finally` 반복기 함수에는 블록이 실행 됩니다. `Catch` 블록은 반복기 함수 내에서 반복기 함수 내에서 발생 하는 예외만 catch 합니다.

## <a name="partial-trust-situations"></a>부분 신뢰 상태

네트워크 공유에 호스트 된 응용 프로그램 같은 부분 신뢰 상황에서는 `Try...Catch...Finally` 호출을 포함 하는 메서드를 호출 하기 전에 발생 하는 보안 예외를 catch 하지 않습니다. 다음 예제에서는 서버 공유에 배치 하 고 여기에서 실행할 때 오류가 발생 합니다 "System.Security.SecurityException: 요청이 실패 했습니다. " 보안 예외에 대 한 자세한 내용은 참조는 <xref:System.Security.SecurityException> 클래스입니다.

[!code-vb[VbVbalrStatements#85](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#85)]

이러한 부분 신뢰 상황에서 배치 해야 합니다 `Process.Start` 문을 별도의 `Sub`합니다. 처음 호출 된 `Sub` 실패 합니다. 이 통해 `Try...Catch` 하기 전에 catch 할 수는 `Sub` 포함 하는 `Process.Start` 시작 보안 예외를 생성 합니다.

## <a name="examples"></a>예제

### <a name="the-structure-of-trycatchfinally"></a>시도의 구조는 중... Catch 하는 중... 마지막으로

다음 예제에서는의 구조를 보여 줍니다.는 `Try...Catch...Finally` 문입니다.

[!code-vb[VbVbalrStatements#86](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#86)]  

### <a name="exception-in-a-method-called-from-a-try-block"></a>Try 블록에서 호출 된 메서드 예외

다음 예제에서는 `CreateException` 메서드가 throw를 `NullReferenceException`입니다. 예외를 생성 하는 코드에 없는 경우는 `Try` 블록입니다. 따라서는 `CreateException` 메서드는 예외를 처리 하지 않습니다. 합니다 `RunSample` 때문에 메서드는 예외를 처리에 대 한 호출을 `CreateException` 메서드는을 `Try` 블록.

예제에 포함 되어 `Catch` 에서 정렬 된 여러 유형의 예외에 대 한 문을 가장 일반적인 가장 구체적인 합니다.

[!code-vb[VbVbalrStatements#91](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#91)]

### <a name="the-catch-when-statement"></a>때 Catch 문

다음 예제에서는 사용 하는 방법을 보여 줍니다는 `Catch When` 조건식에서 필터링 하기 위해. 로 평가 되 면 조건식 `True`의 코드는 `Catch` 블록이 실행 됩니다.

[!code-vb[VbVbalrStatements#92](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#92)]

### <a name="nested-try-statements"></a>중첩 된 Try 문

다음 예제에는 `Try…Catch` 에 포함 된 문에 `Try` 블록입니다. 내부 `Catch` 블록에는 예외가 throw 됩니다. 해당 `InnerException` 속성이 원래 예외를 설정 합니다. 외부 `Catch` 블록 자체 예외 및 내부 예외를 보고 합니다.

[!code-vb[VbVbalrStatements#93](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#93)]

### <a name="exception-handling-for-async-methods"></a>비동기 메서드에 대 한 예외 처리

다음 예제에서는 비동기 메서드에 대한 예외 처리를 보여 줍니다. 비동기 작업에 적용 되는 예외를 catch 하는 `Await` 식에는 `Try` 호출자 및 예외 블록에서 포착 되는 `Catch` 블록.

예제에서 `Throw New Exception` 줄의 주석 처리를 제거하여 예외 처리를 보여 줍니다. 예외에 들어갈는 `Catch` 작업의 블록 `IsFaulted` 속성이로 설정 되어 `True`, 및 태스크의 `Exception.InnerException` 예외 속성.

`Throw New OperationCancelledException` 줄의 주석 처리를 제거하여 비동기 프로세스를 취소할 수 있을 때 발생하는 동작을 보여 줍니다. 예외에서 발견 되는 `Catch` 블록과 작업의 `IsCanceled` 속성이 `True`합니다. 그러나이 예에는 적용 되지 않는 몇몇 조건 `IsFaulted` 로 설정 된 `True` 및 `IsCanceled` 로 설정 된 `False`합니다.

[!code-vb[csAsyncExceptions#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncexceptions/vb/class1.vb#1)]

### <a name="handling-multiple-exceptions-in-async-methods"></a>비동기 메서드에서 여러 예외 처리

다음 예제에서는 여러 작업에서 여러 예외가 발생할 수 있는 경우 예외 처리를 보여 줍니다. 합니다 `Try` 블록에는 `Await` 작업에 대 한 식을 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 반환 합니다. 세 개의 작업 태스크가 완료 되 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 적용 완료 됩니다.

세 작업에서 각각 예외가 발생합니다. 합니다 `Catch` 블록에 있는 예외를 반복 합니다 `Exception.InnerExceptions` 태스크의 속성은 `Task.WhenAll` 반환 합니다.

[!code-vb[csAsyncExceptions#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncexceptions/vb/class1.vb#3)]

## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:System.Exception>
- [Exit 문](exit-statement.md)
- [On Error 문](on-error-statement.md)
- [코드 조각 사용에 대한 모범 사례](/visualstudio/ide/best-practices-for-using-code-snippets)
- [예외 처리](../../../standard/parallel-programming/exception-handling-task-parallel-library.md)
- [Throw 문](throw-statement.md)
