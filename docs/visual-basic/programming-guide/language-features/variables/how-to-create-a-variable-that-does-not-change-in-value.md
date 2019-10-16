---
title: '방법: 값 (Visual Basic)에서 변경 되지 않는 변수 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], read-only
- variables [Visual Basic], constant value
ms.assetid: 86b59266-25df-4635-ae15-9b59c411d036
ms.openlocfilehash: d201e95463dd0431825fee03ebfd340ac80cc552
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630890"
---
# <a name="how-to-create-a-variable-that-does-not-change-in-value-visual-basic"></a>방법: 값 (Visual Basic)에서 변경 되지 않는 변수 만들기

해당 값을 변경 하지 않는 변수의 개념은 모순 되는 것 처럼 보일 수 있습니다. 그러나 상수가 적절 하지 않으며 고정 값이 있는 변수를 사용 하는 것이 유용한 경우가 있습니다. 이 경우 [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md) 키워드를 사용 하 여 멤버 변수를 정의할 수 있습니다.

다음과 같은 경우에는 [Const 문을](../../../../visual-basic/language-reference/statements/const-statement.md) 사용 하 여 상수 값을 선언 하 고 할당할 수 없습니다.

- `Const` 문이 사용 하려는 데이터 형식을 허용 하지 않습니다.

- 컴파일 시간에 값을 알 수 없습니다.

- 컴파일 시간에 상수 값을 계산할 수 없습니다.

### <a name="to-create-a-variable-that-does-not-change-in-value"></a>값이 변경 되지 않는 변수를 만들려면

1. 모듈 수준에서 [Dim 문을](../../../../visual-basic/language-reference/statements/dim-statement.md)사용 하 여 멤버 변수를 선언 하 고 [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md) 키워드를 포함 합니다.

    ```vb
    Dim ReadOnly timeStarted
    ```

    멤버 변수에만 `ReadOnly` 지정할 수 있습니다. 즉, 프로시저 외부의 모듈 수준에서 변수를 정의 해야 합니다.

2. 컴파일 시간에 단일 문에서 값을 계산할 수 있는 경우 `Dim` 문에 초기화 절을 사용 합니다. [As](../../../../visual-basic/language-reference/statements/as-clause.md) 절 뒤에 등호 (`=`)를 추가 하 고 그 뒤에 식을 추가 합니다. 컴파일러가이 식을 상수 값으로 계산할 수 있어야 합니다.

    ```vb
    Dim ReadOnly timeStarted As Date = Now
    ```

    `ReadOnly` 변수에 값을 한 번만 할당할 수 있습니다. 이렇게 하면 코드에서 해당 값을 변경할 수 없습니다.

    컴파일 시간에 값을 알 수 없거나 컴파일 타임에 단일 문에서이 값을 계산할 수 없는 경우 생성자에서 런타임에 해당 값을 할당할 수 있습니다. 이렇게 하려면 클래스 또는 구조체 수준에서 변수 `ReadOnly` 를 선언 해야 합니다. 해당 클래스 또는 구조체에 대 한 생성자에서 변수의 고정 값을 계산 하 고 생성자에서 반환 하기 전에 변수에 할당 합니다.

## <a name="see-also"></a>참고자료

- [WriteOnly](../../../../visual-basic/language-reference/modifiers/writeonly.md)
- [Const 문](../../../../visual-basic/language-reference/statements/const-statement.md)
