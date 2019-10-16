---
title: '방법: 새 변수 만들기 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- Dim statement [Visual Basic]
- variables [Visual Basic], creating
ms.assetid: 35300be3-77b0-4bef-a156-034d3cdedde0
ms.openlocfilehash: a6cb7225ea203f0b38b731795684bfb0cfdfd2d1
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630905"
---
# <a name="how-to-create-a-new-variable-visual-basic"></a>방법: 새 변수 만들기 (Visual Basic)

[Dim 문을](../../../../visual-basic/language-reference/statements/dim-statement.md)사용 하 여 변수를 만듭니다.

### <a name="to-create-a-new-variable"></a>새 변수를 만들려면

1. `Dim` 문에서 변수를 선언 합니다.

    ```vb
    Dim newCustomer
    ```

2. [Private](../../../../visual-basic/language-reference/modifiers/private.md), [Static](../../../../visual-basic/language-reference/modifiers/static.md), [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)또는 [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md)와 같은 변수의 특징에 대 한 사양을 포함 합니다. 자세한 내용은 [선언 된 요소 특성](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)을 참조 하세요.

    ```vb
    Public Static newCustomer
    ```

    선언에서 다른 키워드를 `Dim` 사용 하는 경우 키워드가 필요 하지 않습니다.

3. 규칙 및 규칙 Visual Basic 따라야 하는 변수의 이름을 사용 하 여 사양을 따릅니다. 자세한 내용은 [선언 된 요소 이름](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조 하세요.

    ```vb
    Public Static newCustomer
    ```

4. 이름 뒤에 [As](../../../../visual-basic/language-reference/statements/as-clause.md) 절을 추가 하 여 변수의 데이터 형식을 지정 합니다.

    ```vb
    Public Static newCustomer As Customer
    ```

    데이터 형식을 지정 하지 않으면 기본적 `Object`으로가 사용 됩니다.

5. 등호(`=`)를 사용 하 여 절을따르고변수의초기값을사용하여등호를따릅니다.`As`

    Visual Basic는 `Dim` 문을 실행할 때마다 변수에 지정 된 값을 할당 합니다. 초기 값을 지정 하지 않는 경우 Visual Basic는 먼저 `Dim` 문이 포함 된 코드를 입력할 때 변수의 데이터 형식에 대 한 기본 초기 값을 할당 합니다.

    변수가 참조 형식이 면 `As` 절에 [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md) 키워드를 포함 하 여 해당 클래스의 인스턴스를 만들 수 있습니다. 을 사용 `New`하지 않는 경우 변수의 초기 값은 [Nothing](../../../../visual-basic/language-reference/nothing.md)입니다.

    ```vb
    Public Static newCustomer As New Customer
    ```

## <a name="see-also"></a>참고자료

- [변수](../../../../visual-basic/programming-guide/language-features/variables/index.md)
- [변수 선언](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [선언 요소 이름](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [선언 요소의 특징](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [문(C++)](../../../../visual-basic/language-reference/statements/index.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Option Infer 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
