---
title: If...Then...Else 문(Visual Basic)
ms.date: 04/16/2018
f1_keywords:
- vb.ElseIf
- vb.Then
- vb.If
- vb.EndIf
helpviewer_keywords:
- ElseIf statement [Visual Basic], If...Then...Else
- Then statement [Visual Basic], If...Then...Else
- control flow [Visual Basic], branching
- execution [Visual Basic], conditional
- TypeOf...Is expression, and If...Then...Else statements
- If...Then...Else statements
- If statement [Visual Basic], If...Then...Else
- If statement [Visual Basic]
- Is operator [Visual Basic], in If...Then...Else statements
- If Operator [Visual Basic]
- branching [Visual Basic], conditional
- If function [Visual Basic], and If...Then...Else statements
- Else statement [Visual Basic]
ms.assetid: 790068a2-1307-4e28-8a72-be5ebda099e9
ms.openlocfilehash: db81a1c41809b563d5f9d0777c3feb064c5e540b
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400708"
---
# <a name="ifthenelse-statement-visual-basic"></a>If...Then...Else 문(Visual Basic)

식의 값에 따라 문 그룹을 조건부로 실행합니다.

## <a name="syntax"></a>구문

```vb
' Multiline syntax:
If condition [ Then ]
    [ statements ]
[ ElseIf elseifcondition [ Then ]
    [ elseifstatements ] ]
[ Else
    [ elsestatements ] ]
End If

' Single-line syntax:
If condition Then [ statements ] [ Else [ elsestatements ] ]
```

## <a name="quick-links-to-example-code"></a>예제 코드에 대 한 빠른 링크

이 문서에는 `If`다음을 사용 하는 방법을 보여 주는 몇 가지 예가 포함 되어 있습니다. `Then`... `Else` 문:

- [여러 줄 구문 예제](#multi-line)
- [중첩 구문 예제](#nested)
- [한 줄 구문 예제](#single-line)

## <a name="parts"></a>요소

`condition` \
필수 요소. 식. 는 `True` `Boolean`또는 `False`로 계산 하거나 암시적으로로 변환할 수 있는 데이터 형식으로 계산 되어야 합니다.

식이 [Nothing](../../../visual-basic/language-reference/nothing.md)으로 계산 되 `False`는 null을 [허용](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md) `Boolean` 하는 변수인 경우 조건은 식이 인 것 처럼 처리 되 고 `ElseIf` 블록이 있는 경우에는 블록을 평가 하 고 `Else` 블록은 다음과 같이 처리 됩니다. 존재 하는 경우 실행 됩니다.

`Then` \
한 줄 구문에 필요 합니다. 여러 줄 구문에서 선택 사항입니다.

`statements` \
선택 사항입니다. 뒤 `If`에 하나 이상의 문이 있습니다. `Then` 가 `condition` 로 평가`True`되는 경우 실행 되는입니다.

`elseifcondition` \
가 있는 `ElseIf` 경우 필수입니다. 식. 는 `True` `Boolean`또는 `False`로 계산 하거나 암시적으로로 변환할 수 있는 데이터 형식으로 계산 되어야 합니다.

`elseifstatements` \
선택 사항입니다. 뒤 `ElseIf`에 하나 이상의 문이 있습니다. `Then` 가 `elseifcondition` 로 평가`True`되는 경우 실행 되는입니다.

`elsestatements` \
선택 사항입니다. 이전 `condition` 또는 `elseifcondition` 식이 로`True`계산 되지 않는 경우 실행 되는 하나 이상의 문입니다.

`End If` \
여러 줄 버전의 `If`를 종료 합니다. `Then`... `Else` 블록.

## <a name="remarks"></a>설명

### <a name="multiline-syntax"></a>여러 줄 구문

`If`... `Then`... 문이 발견 되 면가 테스트 됩니다. `condition` `Else` `condition` 가 이면`True`다음 문이`Then` 실행 됩니다. `condition` 가 이면`False`각 문(있는`ElseIf` 경우)이 순서 대로 평가 됩니다. 가 발견 되 면 연결 `ElseIf` 된 바로 다음에 오는 문이 실행 됩니다. `True` `elseifcondition` 가로 `elseifcondition` `True`계산 되지 `Else` 않거나 문이 없으면 다음 문이 실행 됩니다. `ElseIf` `Then`, 또는 `ElseIf` `End If`다음에 오는 문을 실행 한 후에는 다음 문을 사용 하 여 실행이 계속 됩니다. `Else`

`ElseIf` And`Else` 절은 모두 선택 사항입니다. 원하는 수 `ElseIf` `If`의 절을 원하는 개수 만큼 포함할 수 있습니다. `Then`... 문 이지만 절 뒤 `Else` 에는 절이 나타나지 않습니다 `ElseIf`. `Else` `If`... `Then`... `Else` 문은 서로 중첩 될 수 있습니다.

여러 줄 구문 `If` 에서 문은 첫째 줄에서 유일한 문 이어야 합니다. `ElseIf`, 및문은`End If` 줄 레이블 앞에만 올 수 있습니다. `Else` `If`... `Then`... 블록은 `End If` 문으로 끝나야 합니다. `Else`

> [!TIP]
> [Select ... Case 문은](../../../visual-basic/language-reference/statements/select-case-statement.md) 가능한 값이 여러 개 있는 단일 식을 평가할 때 더 유용할 수 있습니다.

### <a name="single-line-syntax"></a>한 줄 구문

True 인 경우 코드를 실행 하는 단일 조건에 대해 한 줄 구문을 사용할 수 있습니다. 그러나 여러 줄로 구성 된 구문은 더 많은 구조와 유연성을 제공 하며 읽기, 유지 관리 및 디버깅 하기가 더 쉽습니다.

`Then` 키워드 다음에 나오는 항목을 검사 하 여 문이 한 줄 `If`인지 여부를 확인 합니다. 주석이 아닌 다른 항목이 같은 줄 `Then` 에 표시 되는 경우이 문은 한 줄 `If` 로 된 문으로 처리 됩니다. 가 없으면 여러 줄 `If`의 시작 이어야 합니다. `Then` `Then`... `Else`.

한 줄 구문에서 다음의 `If`결과로 실행 되는 문이 여러 개 있을 수 있습니다. `Then` 결정. 모든 문은 같은 줄에 있고 콜론으로 구분 해야 합니다.

## <a name="multiline-syntax-example"></a>여러 줄 구문 예제

<a name="multi-line"></a>

다음 예제에서는 ...의 여러 줄로 된 `If`구문을 사용 하는 방법을 보여 줍니다. `Then`... `Else` 문.

[!code-vb[VbVbalrStatements#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class6.vb#101)]

## <a name="nested-syntax-example"></a>중첩 구문 예제

<a name="nested"></a>

다음 예제에는 중첩 `If`된 ... `Then`... `Else` 문.

[!code-vb[VbVbalrStatements#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class6.vb#102)]

## <a name="single-line-syntax-example"></a>한 줄 구문 예제

<a name="single-line"></a>다음 예제에서는 한 줄의 구문을 사용 하는 방법을 보여 줍니다.

[!code-vb[VbVbalrStatements#103](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class6.vb#103)]

## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Interaction.Choose%2A>
- <xref:Microsoft.VisualBasic.Interaction.Switch%2A>
- [#If...Then...#Else 지시문](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [Select...Case 문](../../../visual-basic/language-reference/statements/select-case-statement.md)
- [중첩 제어 구조](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
- [판단 구조](../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)
- [Visual Basic 논리 및 비트 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
- [If 연산자](../../../visual-basic/language-reference/operators/if-operator.md)
