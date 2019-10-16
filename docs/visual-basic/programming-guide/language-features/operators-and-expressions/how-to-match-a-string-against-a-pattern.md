---
title: '방법: 패턴에 대해 문자열 일치 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- comparison operators [Visual Basic], comparing strings
- pattern matching
- strings [Visual Basic], comparing
- string comparison [Visual Basic], operators
- Visual Basic code, operators
- pattern matching [Visual Basic], string comparison
- string comparison [Visual Basic]
- Like operator [Visual Basic], pattern matching
- pattern matching, empty strings
- operators [Visual Basic], comparison
ms.assetid: 19a83804-b5af-4739-928b-ac93e64e457f
ms.openlocfilehash: 0bac0869d9e319071abb31dd0576edf0450aa198
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054159"
---
# <a name="how-to-match-a-string-against-a-pattern-visual-basic"></a>방법: 패턴에 대해 문자열 일치 (Visual Basic)

[문자열 데이터 형식의](../../../../visual-basic/language-reference/data-types/string-data-type.md) 식이 패턴을 충족 하는지 확인 하려는 경우 [Like 연산자](../../../../visual-basic/language-reference/operators/like-operator.md)를 사용할 수 있습니다.

`Like`두 개의 피연산자를 사용 합니다. 왼쪽 피연산자는 문자열 식이고 오른쪽 피연산자는 일치에 사용할 패턴이 포함 된 문자열입니다. `Like`문자열 식이 `Boolean` 패턴을 충족 하는지 여부를 나타내는 값을 반환 합니다.

문자열 식의 각 문자를 특정 문자, 와일드 카드 문자, 문자 목록 또는 문자 범위에 대해 일치 시킬 수 있습니다. 패턴 문자열의 사양 위치는 문자열 식에서 일치 시킬 문자의 위치에 해당 합니다.

## <a name="to-match-a-character-in-the-string-expression-against-a-specific-character"></a>문자열 식의 문자를 특정 문자와 일치 시키려면

패턴 문자열에 특정 문자를 직접 입력 합니다. 특정 특수 문자는 대괄호 (`[ ]`)로 묶어야 합니다. 자세한 내용은 [Like 연산자](../../../../visual-basic/language-reference/operators/like-operator.md)를 참조 하세요.

다음 예제에서는가 단일 `myString` 문자 `H`를 정확 하 게 구성 하는지 테스트 합니다.

[!code-vb[VbVbalrOperators#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#70)]

## <a name="to-match-a-character-in-the-string-expression-against-a-wildcard-character"></a>와일드 카드 문자를 기준으로 문자열 식의 문자를 일치 시키려면

패턴 문자열에 물음표 (`?`)를 입력 합니다. 이 위치에 있는 모든 유효한 문자가 성공적으로 일치 하 게 됩니다.

다음 예제에서는가 단일 `myString` 문자 `W` 다음에 정확히 두 개의 문자로 구성 되어 있는지 여부를 테스트 합니다.

[!code-vb[VbVbalrOperators#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#71)]

## <a name="to-match-a-character-in-the-string-expression-against-a-list-of-characters"></a>문자열 식의 문자를 문자 목록과 일치 시키려면

패턴 문자열에`[ ]`대괄호 ()를 배치 하 고 대괄호 안에 문자 목록을 넣습니다. 문자를 쉼표 또는 다른 구분 기호로 구분 하지 마십시오. 목록의 모든 단일 문자가 성공적으로 일치 하 게 됩니다.

다음 예제에서는가 유효한 `myString` 모든 문자로 `A` `C` `E`구성 되어 있는지 여부를 테스트 합니다.

[!code-vb[VbVbalrOperators#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#72)]

이 일치 항목은 대/소문자를 구분 합니다.

## <a name="to-match-a-character-in-the-string-expression-against-a-range-of-characters"></a>문자열 식에서 문자 범위에 대해 문자를 일치 시키려면

패턴 문자열에`[ ]`대괄호 ()를 배치 하 고, 대괄호 안에는 범위에서 가장 낮거나 가장 높은 문자를 하이픈 (`–`)으로 구분 하 여 입력 합니다. 범위 내의 모든 단일 문자가 성공적으로 일치 하 게 됩니다.

다음 예제에서는가 문자로 `myString` `num` 구성 되어 있는지 여부를 테스트 하 고,,, `i`, `j`또는 `k` `m` `n`문자 `l`중 하나만 입력 합니다.

[!code-vb[VbVbalrOperators#73](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#73)]

이 일치 항목은 대/소문자를 구분 합니다.

## <a name="matching-empty-strings"></a>빈 문자열 일치

`Like`시퀀스 `[]` 를 길이가 0 인 문자열 (`""`)로 처리 합니다. 를 사용 `[]` 하 여 전체 문자열 식이 비어 있는지 여부를 테스트할 수 있지만 문자열 식의 특정 위치가 비어 있는지 테스트 하는 데 사용할 수는 없습니다. 빈 위치가 테스트 해야 하는 옵션 중 하나인 경우 두 번 이상 사용할 `Like` 수 있습니다.

### <a name="to-match-a-character-in-the-string-expression-against-a-list-of-characters-or-no-character"></a>문자열 식의 문자를 문자 목록에 대해 일치 하거나 문자를 검색 하지 않으려면

1. 동일한 문자열 `Like` 식에서 연산자를 두 번 호출 하 고, [or 연산자](../../../../visual-basic/language-reference/operators/or-operator.md) 또는 [OrElse 연산자](../../../../visual-basic/language-reference/operators/orelse-operator.md)중 하나를 사용 하 여 두 호출을 연결 합니다.

2. 첫 번째 `Like` 절에 대 한 패턴 문자열에서 대괄호 (`[ ]`)로 묶인 문자 목록을 포함 합니다.

3. 두 번째 `Like` 절의 패턴 문자열에서 해당 위치에 문자를 넣지 않습니다.

    다음 예에서는 정확히 3 자리 숫자에 대해 7 `phoneNum` 자리 전화 번호를 테스트 한 후 공백, 하이픈 (`–`), 마침표 (`.`) 또는 문자 없이 문자를 정확히 4 자리 숫자로 입력 합니다.

    [!code-vb[VbVbalrOperators#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#74)]

## <a name="see-also"></a>참고자료

- [비교 연산자](../../../../visual-basic/language-reference/operators/comparison-operators.md)
- [연산자 및 식](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [Like 연산자](../../../../visual-basic/language-reference/operators/like-operator.md)
- [String 데이터 형식](../../../../visual-basic/language-reference/data-types/string-data-type.md)
