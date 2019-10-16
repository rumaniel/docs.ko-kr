---
title: Visual Basic의 문
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], declaring
- colons (:) [Visual Basic]
- constants [Visual Basic], defining
- underlines
- constants [Visual Basic], statements
- blue underline [Visual Basic]
- procedures [Visual Basic], statements
- variables [Visual Basic], assigning
- line breaks [Visual Basic], in code
- executable statements [Visual Basic]
- variables [Visual Basic], defining
- statements [Visual Basic], about statements
ms.assetid: fcfdee1a-82b7-4846-98f7-9ca3f5160089
ms.openlocfilehash: e66acae5e98d561883f4ad59853dfd862c8ebfee
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61946460"
---
# <a name="statements-in-visual-basic"></a>Visual Basic의 문

Visual Basic의 문은 전체 명령입니다. 키워드, 연산자, 변수, 상수 및 식을 포함할 수 있습니다. 각 문에 다음 범주 중 하나에 속합니다.

- **선언문**는 변수, 상수 또는 프로시저 이름을 지정 하 고 데이터 형식을 지정할 수도 있습니다.

- **실행 가능 문을**, 하는 작업을 시작 합니다. 이러한 문은 메서드 또는 함수를 호출할 수 있으며 루프 하거나 코드 블록에서 분기 수 있습니다. 실행 가능 문을 포함 **대입문**, 변수 또는 상수 값 이나 식을 할당입니다.

이 항목에서는 각 범주를 설명 합니다. 또한이 항목에서는 여러 문을 한 줄에 결합 하는 방법 및 여러 줄 문을 계속 하는 방법을 설명 합니다.

## <a name="declaration-statements"></a>선언문

프로시저, 변수, 속성, 배열 및 상수를 정의 하 고 이름을 선언 문을 사용 합니다. 프로그래밍 요소를 선언 하면 해당 데이터 형식, 액세스 수준 및 범위 정의할 수 있습니다. 자세한 내용은 [선언 요소의 특징](./declared-elements/declared-element-characteristics.md)합니다.

다음 예제에서는 세 가지 선언이 포함 됩니다.

[!code-vb[VbVbalrStatements#80](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#80)]

첫 번째 선언이 `Sub` 문입니다. 해당 일치와 함께 `End Sub` 라는 프로시저 선언 문을 `applyFormat`합니다. 또한 지정 하는 `applyFormat` 는 `Public`, 즉, 변수를 참조할 수 있는 모든 코드를 호출할 수 있습니다.

두 번째 선언이 `Const` 상수를 선언 하는 문을 `limit`을 지정 하 고는 `Integer` 데이터 형식과 33 값.

세 번째 선언 되는 `Dim` 변수를 선언 하는 문을 `thisWidget`합니다. 데이터 형식은 특정 개체, 즉에서 생성 된 개체는 `Widget` 클래스입니다. 변수를 사용 하는 응용 프로그램에서 제공 되는 임의의 개체 형식 또는 모든 기본 데이터 형식을 선언할 수 있습니다.

### <a name="initial-values"></a>초기 값

선언문을 포함 하는 코드를 실행 하는 경우 Visual Basic에서는 선언된 된 요소에 필요한 메모리를 예약 합니다. 요소 값을 갖는 경우 Visual Basic 데이터 형식에 대 한 기본값으로 초기화 합니다. 자세한 내용은 "동작"를 참조 하세요 [Dim 문](../../language-reference/statements/dim-statement.md)합니다.

다음 예제와 같이 해당 선언의 일부로 변수에 초기 값을 할당할 수 있습니다.

[!code-vb[VbVbalrStatements#81](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#81)]

변수는 개체 변수를 명시적으로 만들면 해당 클래스의 인스턴스를 사용 하 여 선언 하는 경우는 [새 운영자](../../../visual-basic/language-reference/operators/new-operator.md) 키워드, 다음 예제와 같이 보여 줍니다.

[!code-vb[VbVbalrStatements#82](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#82)]

실행 선언문에 도달할 때까지 선언문에 지정 된 초기 값을 변수에 할당 되지 않았는지 note 합니다. 그 전 까지는 변수의 데이터 형식에 대 한 기본값을 포함합니다.

## <a name="executable-statements"></a>실행문

실행 가능 문이 작업을 수행 합니다. 여러 문 반복 코드에서 다른 위치로 분기 프로시저를 호출 하거나 식을 계산할 수 있습니다. 대입문에는 실행 가능 문이의 특수 사례입니다.

다음 예제에서는 `If...Then...Else` 제어 구조를 다른 변수 값을 기반으로 하는 코드 블록을 실행 합니다. 각 코드 블록 내에서 `For...Next` 루프 실행 횟수를 지정된 합니다.

[!code-vb[VbVbalrStatements#83](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#83)]

합니다 `If` 문 앞의 예제에서 매개 변수의 값을 확인 `clockwise`합니다. 값이 `True`를 호출 합니다 `spinClockwise` 메서드의 `aWidget`합니다. 값이 `False`를 호출 합니다 `spinCounterClockwise` 메서드의 `aWidget`합니다. 합니다 `If...Then...Else` 제어 구조 끝나는 `End If`합니다.

합니다 `For...Next` 각 블록 내에서 루프 적절 한 메서드 호출 된 횟수 만큼의 값과 같은 `revolutions` 매개 변수입니다.

## <a name="assignment-statements"></a>대입문

대입문 대입 연산자의 오른쪽에 값을 수행 하는 할당 작업을 수행 (`=`) 하 고 다음 예제와 같이 왼쪽 요소에 저장 합니다.

[!code-vb[VbVbalrStatements#73](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#73)]

앞의 예에서 대입문은 저장 변수에 리터럴 값 42 `v`합니다.

### <a name="eligible-programming-elements"></a>사용할 수 있는 프로그래밍 요소

대입 연산자의 좌 변에 있는 프로그래밍 요소를 받아 값을 저장 하기 위해 수 있어야 합니다. 즉, 변수 또는 아닌 속성 이어야 합니다 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md), 또는 배열 요소 여야 합니다. 대입문의 컨텍스트에서 이러한 요소 라고도 함은 *lvalue*, "왼쪽 값입니다."

대입 연산자의 오른쪽에 있는 값은 리터럴, 상수, 변수, 속성, 배열 요소를 다른 식 또는 함수 호출의 조합으로 구성 될 수 있는 식에서 생성 됩니다. 다음은 이에 대한 예입니다.

[!code-vb[VbVbalrStatements#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#74)]

위의 예제에서는 변수에 저장 된 값 `y` 변수에 저장 된 값을 `z`, 다음 함수를 호출 하 여 반환 되는 값을 추가 하 고 `findResult`입니다. 이 식의 합계 값은 변수에 저장 한 다음 `x`합니다.

### <a name="data-types-in-assignment-statements"></a>대입문의 데이터 형식

숫자 값 외에도 할당 연산자를 할당할 수도 `String` 다음 예제와 같이 값입니다.

[!code-vb[VbVbalrStatements#75](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#75)]

할당할 수도 있습니다 `Boolean` 중 하나를 사용 하 여 값을 `Boolean` 리터럴 또는 `Boolean` 다음 예제와 같이 식을 보여 줍니다.

[!code-vb[VbVbalrStatements#76](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#76)]

마찬가지로, 적절 한 값의 프로그래밍 요소에 할당할 수 있습니다 합니다 `Char`, `Date`, 또는 `Object` 데이터 형식입니다. 또한 해당 인스턴스에 만들어집니다 클래스도 선언 된 요소에 개체 인스턴스를 할당할 수 있습니다.

### <a name="compound-assignment-statements"></a>복합 대입문

*복합 대입문* 먼저 프로그래밍 요소에 할당 하기 전에 식에 대 한 작업을 수행 합니다. 다음 예제에서는 다음이 연산자 중 하나를 보여 줍니다 `+=`는 오른쪽에 있는 식의 값으로 연산자의 좌 변에 있는 변수의 값을 증가 시킵니다.

[!code-vb[VbVbalrStatements#77](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#77)]

앞의 예제 값 1을 더하여 `n`, 다음에 새 값을 저장 하 고 `n`입니다. 이것은 다음 문과 동일 합니다.

[!code-vb[VbVbalrStatements#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#78)]

이러한 종류의 연산자를 사용 하 여 다양 한 복합 할당 작업을 수행할 수 있습니다. 목록과 이러한 연산자에 대 한 자세한 내용은 참조 하세요 [대입 연산자](../../../visual-basic/language-reference/operators/assignment-operators.md)합니다.

연결 대입 연산자 (`&=`) 기존의 끝에 문자열을 추가 하는 데는 다음 예제와 같이 문자열입니다.

[!code-vb[VbVbalrStatements#79](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#79)]

### <a name="type-conversions-in-assignment-statements"></a>대입문의 형식 변환

변수, 속성 또는 배열 요소에 할당 하는 값은 해당 대상 요소에 적절 한 데이터 형식 이어야 합니다. 일반적으로 대상 요소와 동일한 데이터 형식의 값을 생성 하려고 해야 합니다. 그러나 일부 형식 할당 중에 다른 형식에서 변환할 수 있습니다.

데이터 형식 간 변환에 대 한 내용은 참조 하세요 [Visual Basic의 형식 변환](./data-types/type-conversions.md)합니다. 간단히 말해, Visual Basic는 자동으로 확대 하는 다른 모든 형식에 지정 된 형식의 값을 변환 합니다. A *확대 변환* 은 하나는 항상 런타임에 성공 하 고 데이터가 손실 되지 않습니다. 예를 들어 Visual Basic 변환를 `Integer` 값을 `Double` 해당 되는 경우 때문 `Integer` 로 확대 `Double`합니다. 자세한 내용은 [Widening and Narrowing Conversions](./data-types/widening-and-narrowing-conversions.md)을 참조하세요.

*축소 변환* 런타임 시 오류 또는 데이터 손실의 위험을 수행 (확대 하지 해당). 형식 변환 함수를 사용 하 여 명시적으로 축소 변환을 수행 하거나 설정 하 여 모든 변환을 암시적으로 수행 하기 위해 컴파일러에 지시할 수 있습니다 `Option Strict Off`합니다. 자세한 내용은 [암시적 변환과 명시적 변환](./data-types/implicit-and-explicit-conversions.md)합니다.

## <a name="putting-multiple-statements-on-one-line"></a>한 줄에 여러 문 배치

콜론으로 구분 된 단일 줄에 여러 문을 포함할 수 있습니다 (`:`) 문자입니다. 다음은 이에 대한 예입니다.

[!code-vb[VbVbalrStatements#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#70)]

경우에 따라 편리 하지만이 형식의 구문 사용 하면 코드 읽고 유지 관리 하기가 어렵습니다. 따라서 하나의 문으로 줄으로 유지 하는 하는 것이 좋습니다.

## <a name="continuing-a-statement-over-multiple-lines"></a>여러 줄 문을 계속

문을 한 줄에 일반적으로 적합 하지만 너무 긴 경우 뒤에 밑줄 문자가 공백으로 구성 된 순서 줄 연속 문자를 사용 하 여 다음 줄으로 계속 수 있습니다 (`_`) 뒤에 캐리지 리턴입니다. 다음 예제에서는 `MsgBox` 실행 문은 두 줄에 걸쳐 계속 됩니다.

[!code-vb[VbVbalrStatements#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#71)]

### <a name="implicit-line-continuation"></a>암시적 줄 연속 문자

대부분의 경우 계속할 수 있습니다 문을 다음 연속 줄에서 밑줄 문자를 사용 하지 않고 (`_`). 다음 구문 요소는 암시적으로 코드의 다음 줄에서 문을 계속 합니다.

- 쉼표 뒤 (`,`). 예를 들어:

   [!code-vb[VbVbalrLineContinuation#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#1)]

- 여는 괄호 뒤 (`(`) 또는 닫는 괄호 앞 (`)`). 예를 들어:

   [!code-vb[VbVbalrLineContinuation#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#2)]

- 열린 중괄호 (`{`) 또는 닫는 중괄호 이전 (`}`). 예를 들어:

    [!code-vb[VbVbalrLineContinuation#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#3)]

    자세한 내용은 참조 하세요. [개체 이니셜라이저: 명명 된 형식과 익명 형식](./objects-and-classes/object-initializers-named-and-anonymous-types.md) 나 [컬렉션 이니셜라이저](./collection-initializers/index.md)합니다.

- 열린 후 포함 식 (`<%=`) 또는 포함 된 식의 닫기 전에 (`%>`) XML 리터럴 내에서. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#4)]

   자세한 내용은 [XML의 포함 식](./xml/embedded-expressions-in-xml.md)합니다.

- 연결 연산자 뒤 (`&`). 예를 들어:

   [!code-vb[VbVbcnConventions#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/vb/Class1.vb#9)]

   자세한 내용은 [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)합니다.

- 후 할당 연산자 (`=`, `&=`, `:=`, `+=`, `-=`를 `*=`, `/=`, `\=`, `^=`를 `<<=`, `>>=`). 예를 들어:

   [!code-vb[VbVbalrLineContinuation#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#5)]

   자세한 내용은 [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)합니다.

- 이항 연산자 (`+`, `-`, `/`, `*`, `Mod`를 `<>`, `<`를 `>`, `<=`를 `>=`, `^`, `>>`, `<<`, `And`를 `AndAlso`를 `Or`를 `OrElse`를 `Like`, `Xor`) 식 내에서. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#7)]

   자세한 내용은 [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)합니다.

- 후 합니다 `Is` 고 `IsNot` 연산자입니다. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#8)]

   자세한 내용은 [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)합니다.

- 멤버 한정자 문자 뒤 (`.`) 및 멤버 이름 앞입니다. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#5)]

   하지만 줄 연속 문자를 포함 해야 (`_`) 멤버 한정자 문자를 사용 하는 경우 다음을 `With` 문이나 형식의 초기화 목록에서 값을 제공 합니다. 대입 연산자 뒤에서 줄 바꿈 하는 것이 좋습니다 (예를 들어 `=`)을 사용할 때 `With` 문이나 개체 초기화 목록입니다. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#14)]

   자세한 내용은 참조 하세요. [사용 하 여는 중... 문을 사용 하 여 종료](../../../visual-basic/language-reference/statements/with-end-with-statement.md) 또는 [개체 이니셜라이저: 명명 된 형식과 익명 형식](./objects-and-classes/object-initializers-named-and-anonymous-types.md)합니다.

- XML 축 속성 한정자를 후 (`.` 나 `.@` 또는 `...`). 하지만 줄 연속 문자를 포함 해야 (`_`)를 사용 하는 경우 멤버 한정자를 지정 하면를 `With` 키워드입니다. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#9)]

   자세한 내용은 [XML 축 속성](../../../visual-basic/language-reference/xml-axis/index.md)합니다.

- 작음-기호 (<) 보다 이전의 큼-기호 (`>`) 특성을 지정 하는 경우. 뒤에 큼-기호 (`>`) 특성을 지정 하는 경우. 하지만 줄 연속 문자를 포함 해야 (`_`) 어셈블리 수준 또는 모듈 수준 특성을 지정 하는 경우. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#10)]

   자세한 내용은 [특성 개요](../../../visual-basic/programming-guide/concepts/attributes/index.md)합니다.

- 쿼리 연산자 앞뒤 (`Aggregate`, `Distinct`, `From`, `Group By`, `Group Join`를 `Join`, `Let`를 `Order By`, `Select`를 `Skip`, `Skip While`, `Take`, `Take While`, `Where`를 `In`를 `Into`, `On`를 `Ascending`, 및 `Descending`). 여러 키워드 이루어져 하는 쿼리 연산자 키워드 사이 줄을 바꿀 수 없습니다 (`Order By`, `Group Join`를 `Take While`, 및 `Skip While`). 예를 들어:

   [!code-vb[VbVbalrLineContinuation#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#11)]

   자세한 내용은 [쿼리](../../../visual-basic/language-reference/queries/index.md)합니다.

- 후 합니다 `In` 키워드를 `For Each` 문입니다. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#12)]

   자세한 내용은 참조 하세요. [각각에 대 한 중... 다음 문을](../../../visual-basic/language-reference/statements/for-each-next-statement.md)합니다.

- 후는 `From` 컬렉션 이니셜라이저에서 키워드입니다. 예를 들어:

   [!code-vb[VbVbalrLineContinuation#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#13)]

   자세한 내용은 [컬렉션 이니셜라이저](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)를 참조하세요.

## <a name="adding-comments"></a>주석 추가

항상 소스 코드를 작성 한 프로그래머에도 쉽게 이해할 수 없습니다. 따라서 해당 코드를 문서화를 위해 대부분의 프로그래머에 게가 포함 된 주석의 자유롭게 사용 하 여를 확인 합니다. 코드의 주석을 프로시저나 읽기 또는 나중에 작업을 모든 사용자에 게 특정 지침을 설명 합니다. Visual Basic 컴파일 중 메모를 무시 하 고 컴파일된 코드가 영향을 주지 않습니다.

주석 줄에 아포스트로피가 시작 (`'`) 또는 `REM` 뒤에 공백이 있습니다. 추가할 수 있습니다 어디서 나 코드에서 제외 하 고 문자열 내에서. 주석 문을 추가할 아포스트로피를 삽입 또는 `REM` 주석 뒤에 문 뒤 합니다. 별도 줄에 주석을 수행할 수도 있습니다. 다음 예제에서는 이러한 가능성을 보여 줍니다.

[!code-vb[VbVbalrStatements#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#72)]

## <a name="checking-compilation-errors"></a>컴파일 오류를 확인 하는 중

코드 줄을 입력 한 후 줄 (오류 메시지가 나타날 수 있음) 파란색 물결 무늬 밑줄로 표시 됩니다, 그리고 문에 구문 오류가 있습니다. 무엇이 문을 사용 하 여 작업 목록에서 또는 마우스 포인터를 사용 하 여 오류를 가리키면 찾고 기록 된 오류 메시지) (에서 확인 하 고 수정 해야 합니다. 코드에서 모든 구문 오류를 수정 하기 전에 올바르게 컴파일되도록 하려면 프로그램이 실패 합니다.

## <a name="related-sections"></a>관련 단원

|용어|정의|
|---|---|
|[할당 연산자](../../../visual-basic/language-reference/operators/assignment-operators.md)|와 같은 할당 연산자를 포함 하는 언어 참조 페이지 링크를 제공 `=`, `*=`, 및 `&=`합니다.|
|[연산자 및 식](./operators-and-expressions/index.md)|새 값을 산출 하는 연산자를 사용 하 여 요소를 결합 하는 방법을 보여 줍니다.|
|[방법: 코드에서 문 분리 및 결합](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)|단일 문에 여러 줄으로 분할 하는 방법과 같은 줄에 여러 문 배치 하는 방법을 보여 줍니다.|
|[방법: 레이블 문](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)|코드 줄 레이블을 지정 하는 방법을 보여 줍니다.|
