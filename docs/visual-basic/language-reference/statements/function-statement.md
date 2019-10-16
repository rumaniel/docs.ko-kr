---
title: Function 문(Visual Basic)
ms.date: 05/12/2018
f1_keywords:
- vb.Function
helpviewer_keywords:
- procedures [Visual Basic], creating
- Function procedures [Visual Basic], Function statement syntax
- functions [Visual Basic], function procedures
- ParamArray keyword [Visual Basic], Function statements
- Private keyword [Visual Basic], Function statements
- declarations [Visual Basic], procedures
- procedures [Visual Basic], declaration
- Public keyword [Visual Basic], in Function statement
- ByVal keyword [Visual Basic], Function statements
- procedures [Visual Basic], recursive
- Implements keyword [Visual Basic], Function statements
- procedures [Visual Basic], returning values
- Exit statement [Visual Basic], in Function procedures
- recursive procedures
- As keyword [Visual Basic], in Function statement
- Optional keyword [Visual Basic], Function statements
- Function statement [Visual Basic]
- Visual Basic code, Function procedures
- procedures [Visual Basic], function
- ByRef keyword [Visual Basic], Function statements
- Friend keyword [Visual Basic], Function statements
- End keyword [Visual Basic], Function statements
- Handles keyword [Visual Basic], Function statements
ms.assetid: a4497077-0f46-4ede-a27f-9e8670df52b9
ms.openlocfilehash: 3a6184164fdc6f2517caf45f7b5e1455c9299666
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754725"
---
# <a name="function-statement-visual-basic"></a>Function 문(Visual Basic)

선언 하 고 이름, 매개 변수를 정의 하는 코드는 `Function` 프로시저입니다.

## <a name="syntax"></a>구문

```
[ <attributelist> ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async | Iterator ]
Function name [ (Of typeparamlist) ] [ (parameterlist) ] [ As returntype ] [ Implements implementslist | Handles eventlist ]
    [ statements ]
    [ Exit Function ]
    [ statements ]
End Function
```

## <a name="parts"></a>요소

- `attributelist`

  선택 사항입니다. 참조 [특성 목록](attribute-list.md)합니다.

- `accessmodifier`

  선택 사항입니다. 다음 중 하나일 수 있습니다.

  - [공용](../../../visual-basic/language-reference/modifiers/public.md)

  - [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)

  - [Friend](../../../visual-basic/language-reference/modifiers/friend.md)

  - [전용](../../../visual-basic/language-reference/modifiers/private.md)

  - [Protected Friend](../../language-reference/modifiers/protected-friend.md)

  - [Private Protected](../../language-reference/modifiers/private-protected.md)

  [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.

- `proceduremodifiers`

  선택 사항입니다. 다음 중 하나일 수 있습니다.

  - [오버로드](../../../visual-basic/language-reference/modifiers/overloads.md)

  - [재정의](../../../visual-basic/language-reference/modifiers/overrides.md)

  - [재정의 가능](../../../visual-basic/language-reference/modifiers/overridable.md)

  - [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)

  - [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)

  - `MustOverride Overrides`

  - `NotOverridable Overrides`

- `Shared`

  선택 사항입니다. 참조 [공유](../../../visual-basic/language-reference/modifiers/shared.md)합니다.

- `Shadows`

  선택 사항입니다. 참조 [그림자](../../../visual-basic/language-reference/modifiers/shadows.md)합니다.

- `Async`

  선택 사항입니다. 참조 [비동기](../../../visual-basic/language-reference/modifiers/async.md)합니다.

- `Iterator`

  선택 사항입니다. 참조 [반복기](../../../visual-basic/language-reference/modifiers/iterator.md)합니다.

- `name`

  필수 요소. 프로시저의 이름입니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.

- `typeparamlist`

  선택 사항입니다. 제네릭 프로시저에 대 한 형식 매개 변수의 목록입니다. 참조 [유형 목록](type-list.md)합니다.

- `parameterlist`

  선택 사항입니다. 이 절차의 매개 변수를 나타내는 로컬 변수 이름의 목록입니다. 참조 [매개 변수 목록](parameter-list.md)합니다.

- `returntype`

  필요한 경우 `Option Strict` 는 `On`합니다. 이 프로시저에 의해 반환 되는 값의 데이터 형식입니다.

- `Implements`

  선택 사항입니다. 하나 이상의이 절차를 구현 함을 나타냅니다 `Function` 절차,이 절차의 포함 하는 클래스 또는 구조체에서 구현 된 인터페이스에 정의 된 각각. 참조 [문을 구현](implements-statement.md)합니다.

- `implementslist`

  `Implements`가 제공된 경우 필수입니다. 구현할 `Function` 프로시저 목록입니다.

  `implementedprocedure [ , implementedprocedure ... ]`

  각 `implementedprocedure`에는 다음과 같은 구문과 요소가 있습니다.

  `interface.definedname`

  |파트|설명|
  |---|---|
  |`interface`|필수 요소. 이 프로시저에 의해 구현 된 인터페이스의 이름을 클래스 또는 구조체를 포함 합니다.|
  |`definedname`|필수 요소. 프로시저가 `interface`에 정의되는 이름입니다.|

- `Handles`

  선택 사항입니다. 이 절차에서 하나 이상의 특정 이벤트를 처리할 수 있는지를 나타냅니다. 참조 [처리](handles-clause.md)합니다.

- `eventlist`

  `Handles`가 제공된 경우 필수입니다. 이 프로시저에서 처리 하는 이벤트 목록입니다.

  `eventspecifier [ , eventspecifier ... ]`

  각 `eventspecifier`에는 다음과 같은 구문과 요소가 있습니다.

  `eventvariable.event`

  |파트|설명|
  |---|---|
  |`eventvariable`|필수 요소. 클래스 또는 구조의 이벤트를 발생 시키는 데이터 형식으로 선언 하는 개체 변수입니다.|
  |`event`|필수 요소. 이 프로시저에서 처리 하는 이벤트의 이름입니다.|

- `statements`

  선택 사항입니다. 이 프로시저 내에서 실행할 문 블록입니다.

- `End Function`

  이 프로시저의 정의 종료합니다.

## <a name="remarks"></a>설명

프로시저 내에서 실행 되는 모든 코드 여야 합니다. 차례로 각 프로시저에는 클래스, 구조체 또는 포함 하는 클래스, 구조체 또는 모듈 이라고 하는 모듈 내에서 선언 됩니다.

호출 코드에 값을 반환 하려면 사용을 `Function` 프로시저 그렇지 않은 경우 사용을 `Sub` 프로시저입니다.

## <a name="defining-a-function"></a>함수 정의

정의할 수는 `Function` 모듈 수준 에서만 프로시저입니다. 따라서 함수에 대 한 선언 컨텍스트 클래스, 구조체, 모듈 또는 인터페이스 여야 하며 소스 파일, 네임 스페이스, 프로시저 또는 블록 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](declaration-contexts-and-default-access-levels.md)을 참조하세요.

`Function` 프로시저는 기본적으로 공용 액세스 합니다. 액세스 한정자를 사용 하 여 해당 액세스 수준을 조정할 수 있습니다.

`Function` 프로시저는 프로시저에서 반환 된 값의 데이터 형식을 선언할 수 있습니다. 모든 데이터 형식 또는 열거형, 구조체, 클래스 또는 인터페이스의 이름을 지정할 수 있습니다. 지정 하지 않으면 합니다 `returntype` 매개 변수, 프로시저 반환 `Object`합니다.

이 절차를 사용 하는 경우는 `Implements` 있어야 키워드를 포함 하는 클래스 또는 구조체는 `Implements` 바로 뒤에 오는 문을 해당 `Class` 또는 `Structure` 문입니다. 합니다 `Implements` 각 인터페이스에 지정 된 문에 포함 해야 `implementslist`합니다. 그러나 사용 되는 인터페이스는 다음과 같이 정의 됩니다. 이름을 합니다 `Function` (에서 `definedname`)이이 프로시저의 이름과 일치할 필요는 없습니다 (에서 `name`).

> [!NOTE]
> 식 인라인 함수를 정의 하려면 람다 식을 사용할 수 있습니다. 자세한 내용은 [함수 식을](../../../visual-basic/language-reference/operators/function-expression.md) 하 고 [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)합니다.

## <a name="returning-from-a-function"></a>함수에서 반환

경우는 `Function` 프로시저가 호출 코드에 반환 되 면 실행이 프로시저를 호출한 문 뒤에 오는 문을 사용 하 여 계속 합니다.

함수에서 값을 반환 하는 함수 이름에 값을 할당 하거나 포함을 `Return` 문입니다.

`Return` 문을 동시에 반환 값을 할당 하 고 다음 예와 같이 함수를 종료 합니다.

[!code-vb[VbVbalrStatements#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#24)]

함수 이름에 반환 값을 할당 하는 다음 예제에서는 `myFunction` 를 사용 하 여는 `Exit Function` 문을 반환 합니다.

[!code-vb[VbVbalrStatements#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#23)]

합니다 `Exit Function` 하 고 `Return` 문을 사용 하면 즉시 종료를 `Function` 프로시저입니다. 임의 개수의 `Exit Function` 하 고 `Return` 문을 프로시저에서 아무 곳 이나 나타날 수 있으며 함께 사용할 수 있습니다 `Exit Function` 및 `Return` 문.

사용 하는 경우 `Exit Function` 값을 할당 하지 않고 `name`, 프로시저에 지정 된 데이터 형식에 대 한 기본값을 반환 합니다. `returntype`합니다. 하는 경우 `returntype` 프로시저가 반환 하는 지정 되지 않은 `Nothing`에 대 한 기본 값인 `Object`합니다.

## <a name="calling-a-function"></a>함수 호출

호출을 `Function` 식에서 괄호 안에 인수 목록 뒤에 프로시저 이름을 사용 하 여 프로시저입니다. 모든 인수를 제공 하지 하는 경우에 괄호를 생략할 수 있습니다. 그러나 코드는 항상 괄호를 포함 하는 경우 더 쉽게 읽을 수 있습니다.

호출을 `Function` 라이브러리를 호출 하는 동일한 방식으로 같은 함수는 프로시저 `Sqrt`를 `Cos`, 또는 `ChrW`합니다.

사용 하 여 함수를 호출할 수도 있습니다는 `Call` 키워드입니다. 이 경우 반환 값은 무시 됩니다. 사용 된 `Call` 키워드는 대부분의 경우에 권장 되지 않습니다. 자세한 내용은 [Call 문을](call-statement.md)합니다.

Visual Basic에는 산술 식 내부 효율성을 높이기 위해 경우에 따라 다시 정렬 합니다. 따라서 사용 하지 않아야 하면를 `Function` 함수 같은 식에서 변수의 값을 변경할 때 산술 식에는 프로시저입니다.

## <a name="async-functions"></a>비동기 함수

합니다 *비동기* 기능을 사용 하면 명시적 콜백을 사용 하거나 여러 개의 함수 또는 람다 식에서 코드를 수동으로 분할 하지 않고 비동기 함수를 호출할 수 있습니다.

사용 하는 함수를 표시 하는 경우는 [비동기](../../../visual-basic/language-reference/modifiers/async.md) 한정자를 사용할 수는 [Await](../../../visual-basic/language-reference/operators/await-operator.md) 함수에 연산자입니다. 도달 하면 컨트롤이 `Await` 식에는 `Async` 함수 호출자에 게 제어가 반환 및 대기 중인된 작업이 완료 될 때까지 함수 진행이 일시 중단 합니다. 작업이 완료 되 면 실행 함수에서 다시 시작할 수 있습니다.

> [!NOTE]
> `Async` 아직 완료 되지 않은 첫 번째 대기 중이 던된 개체 발생 하거나 프로시저가 호출자에 게 반환 또는 끝에 도달할 때를 `Async` 프로시저 중 먼저 발생 합니다.

`Async` 함수는 반환 형식으로 지정할 수 있습니다 <xref:System.Threading.Tasks.Task%601> 또는 <xref:System.Threading.Tasks.Task>합니다. 예는 `Async` 의 반환 형식을 가진 함수 <xref:System.Threading.Tasks.Task%601> 아래에 제공 됩니다.

`Async` 모든 함수를 선언할 수 없습니다 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) 매개 변수입니다.

A [Sub 문](sub-statement.md) 사용 하 여 표시할 수도 있습니다는 `Async` 한정자입니다. 이 주로 이벤트 처리기에 대 한 값을 반환할 수 없습니다. `Async` `Sub` 프로시저 대기할 수 없습니다 및 호출자는 `Async` `Sub` 절차에서 throw 된 예외를 catch 할 수 없습니다는 `Sub` 프로시저입니다.

에 대 한 자세한 내용은 `Async` 함수를 참조 하세요 [Async 및 Await를 사용한 비동기 프로그래밍](../../../visual-basic/programming-guide/concepts/async/index.md)하십시오 [비동기 프로그램의 제어 흐름](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md), 및 [비동기 반환 형식](../../../visual-basic/programming-guide/concepts/async/async-return-types.md).

## <a name="iterator-functions"></a>반복기 함수

*반복기* 함수 목록 또는 배열로 같은 컬렉션에 사용자 지정 반복을 수행 합니다. 반복기 함수를 사용 하는 [생성](yield-statement.md) 문을 한 번에 각 요소를 반환 합니다. 경우는 [Yield](yield-statement.md) 문에 도달할 때 코드의 현재 위치가 기억 됩니다. 다음에 반복기 함수가 호출되면 해당 위치에서 실행이 다시 시작됩니다.

사용 하 여 클라이언트 코드에서 반복기를 호출 하는 [각각에 대 한 중... 다음](for-each-next-statement.md) 문입니다.

반복기 함수의 반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>하십시오 <xref:System.Collections.IEnumerator>, 또는 <xref:System.Collections.Generic.IEnumerator%601>.

자세한 내용은 [반복기](../../programming-guide/concepts/iterators.md)를 참조하세요.

## <a name="example"></a>예제

다음 예제에서는 합니다 `Function` 이름, 매개 변수 및 코드의 본문을 형성 하는 declare 문을 `Function` 프로시저입니다. `ParamArray` 한정자를 사용 하면 가변 개수의 인수를 수락 하는 함수입니다.

[!code-vb[VbVbalrStatements#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#25)]

## <a name="example"></a>예제

다음 예제에서는 앞의 예제에서 선언 된 함수를 호출 합니다.

[!code-vb[VbVbalrStatements#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#26)]

## <a name="example"></a>예제

다음 예에서 `DelayAsync` 되는 `Async` `Function` 반환 형식이 있는 <xref:System.Threading.Tasks.Task%601>합니다. `DelayAsync` 에는 정수를 반환하는 `Return` 문이 포함됩니다. 따라서 함수 선언의 `DelayAsync` 의 반환 형식이 있어야 `Task(Of Integer)`합니다. 반환 형식 이므로 `Task(Of Integer)`를 평가 합니다 `Await` 식 `DoSomethingAsync` 정수가 생성 합니다. 본이 방침에 설명 되어이: `Dim result As Integer = Await delayTask`합니다.

`startButton_Click` 절차는의 예는 `Async Sub` 프로시저입니다. 때문에 `DoSomethingAsync` 되는 `Async` 함수에 대 한 호출에 대 한 작업 `DoSomethingAsync` 다음 문을 보여 주듯이 대기할 수 있어야 합니다: `Await DoSomethingAsync()`합니다. 합니다 `startButton_Click` `Sub` 프로시저를 사용 하 여 정의 되어야 합니다는 `Async` 한정자 있기 때문에 `Await` 식입니다.

[!code-vb[csAsyncMethod#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncmethod/vb/mainwindow.xaml.vb#1)]

## <a name="see-also"></a>참고자료

- [Sub 문](sub-statement.md)
- [Function 프로시저](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)
- [매개 변수 목록](parameter-list.md)
- [Dim 문](dim-statement.md)
- [Call 문](call-statement.md)
- [Of](of-clause.md)
- [매개 변수 배열](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)
- [방법: 제네릭 클래스 사용](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [프로시저 문제 해결](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)
- [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
- [함수 식](../../../visual-basic/language-reference/operators/function-expression.md)
