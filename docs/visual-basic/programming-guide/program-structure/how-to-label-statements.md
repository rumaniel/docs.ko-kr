---
title: '방법: 레이블 문 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- colons (:)
- statements [Visual Basic], labels
- ': separator character'
- Visual Basic code, labeling statements
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
ms.openlocfilehash: 9a5f2039716a18011cac3dfd9b011d5b3868c294
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054048"
---
# <a name="how-to-label-statements-visual-basic"></a>방법: 레이블 문 (Visual Basic)

문 블록은 콜론으로 구분 된 코드 줄로 구성 됩니다. 식별 문자열이 나 정수로 시작 하는 코드 줄에는 *레이블이 지정*된 것으로 간주 됩니다. 문 레이블은와 `On Error Goto`같은 문에서 사용할 수 있도록 코드 줄을 표시 하는 데 사용 됩니다.

레이블은 프로그래밍 요소를 식별 하는 식별자 (예: 올바른 Visual Basic 식별자 또는 정수 리터럴) 일 수 있습니다. 레이블은 소스 코드 줄의 시작 부분에 표시 되어야 하며, 뒤에 동일한 줄에 문이 있는지 여부에 관계 없이 콜론이와 야 합니다.

컴파일러는 줄의 시작 부분이 이미 정의 된 식별자와 일치 하는지 여부를 확인 하 여 레이블을 식별 합니다. 그렇지 않은 경우 컴파일러는 레이블로 간주 합니다.

레이블은 고유한 선언 공간을 가지 며 다른 식별자를 방해 하지 않습니다. 레이블의 범위는 메서드의 본문입니다. 모호한 상황에서는 레이블 선언이 우선적으로 적용 됩니다.

> [!NOTE]
> 레이블은 메서드 내의 실행 가능한 문에서만 사용할 수 있습니다.

## <a name="to-label-a-line-of-code"></a>코드 줄에 레이블을 만들려면

소스 코드 줄의 시작 부분에서 식별자 뒤에 콜론을 추가 합니다.

예를 들어 다음 코드 줄은 각각 및 `Jump` `120`로 레이블이 지정 됩니다.

[!code-vb[VbVbalrStatements#708](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#708)]

## <a name="see-also"></a>참고자료

- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
- [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [프로그램 구조 및 코드 규칙](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
