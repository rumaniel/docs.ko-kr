---
title: With...End With 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.With
helpviewer_keywords:
- With keyword [Visual Basic]
- loop structures [Visual Basic], and With...End With statements
- execution [Visual Basic], on object
- instructions, repeating
- With...End With statements [Visual Basic]
- With statement [Visual Basic]
- With statement [Visual Basic], nesting
- objects [Visual Basic], accessing
- With block
- End keyword [Visual Basic], With...End With statements
ms.assetid: 340d5fbb-4f43-48ec-a024-80843c137817
ms.openlocfilehash: 3c6766d9084962d006fe5e5d7d5cc723c2aad441
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046637"
---
# <a name="withend-with-statement-visual-basic"></a>With...End With 문(Visual Basic)

개체 또는 구문의 멤버에 액세스할 때 문에서 단순화된 구문을 사용할 수 있도록 단일 개체를 반복적으로 참조하는 일련의 문을 실행합니다.  구조체를 사용하면 멤버 또는 호출 메서드의 값을 읽을 수만 있으며, `With...End With` 문에서 사용된 구조체의 멤버에 값을 할당하도록 시도하는 경우 오류가 발생합니다.

## <a name="syntax"></a>구문

```
With objectExpression
    [ statements ]
End With
```

## <a name="parts"></a>요소

|용어|정의|
|---|---|
|`objectExpression`|필수 요소. 개체를 평가하는 식입니다. 식은 임의적으로 복잡할 수 있으며, 한 번만 계산됩니다. 식이 기본 형식을 포함하여 모든 데이터 형식으로 계산될 수 있습니다.|
|`statements`|선택 사항입니다. `With`의 평가를 통해 생성된 개체의 멤버를 참조할 수 있는 `End With`와 `objectExpression` 사이의 하나 이상의 문입니다.|
|`End With`|필수 요소. `With` 블록의 정의를 종료합니다.|

## <a name="remarks"></a>설명

`With...End With`를 사용하여 개체의 이름을 여러 번 지정하지 않고 지정된 개체에 일련의 문을 수행할 수 있습니다. `With` 문 블록 내에서 `With` 문 개체가 앞에 오는 것처럼 기간으로 시작하는 개체의 멤버를 지정할 수 있습니다.

예를 들어, 하나의 개체에 있는 여러 속성을 변경하려면 속성을 할당할 때마다 한 번이 아닌 해당 개체를 한 번만 참조하여 `With...End With` 블록 내에 속성 할당 문을 배치합니다.

코드가 여러 문에서 동일한 개체에 액세스하는 경우 `With` 문을 사용하여 다음과 같은 이점을 얻을 수 있습니다.

- 복합 식을 여러 번 평가하거나 멤버를 여러 번 참조하기 위해 결과를 임시 변수에 할당할 필요가 없습니다.

- 반복적인 정규화 식을 제거하여 코드를 더욱 쉽게 읽을 수 있습니다.

`objectExpression`의 데이터 형식은 모든 클래스 또는 구조체 형식이거나 `Integer`와 같은 Visual Basic 기본 형식일 수도 있습니다.  `objectExpression`이 개체 이외의 모든 항목을 생성하는 경우 멤버 또는 호출 메서드의 값을 읽을 수만 있으며, `With...End With` 문에서 사용된 구조체의 멤버에 값을 할당하도록 시도하는 경우 오류가 발생합니다.  이는 구조체를 반환하고 `GetAPoint().x = 1`과 같은 함수 결과의 멤버에 즉시 액세스하여 값을 할당한 메서드를 호출한 경우 발생하는 오류와 동일합니다.  두 경우 모두 구조체가 호출 스택에만 존재하고 이러한 상황의 수정된 구조체 멤버가 프로그램의 다른 코드가 변경을 관찰할 수 있는 위치에 쓸 수 있는 방법이 없는 문제가 발생합니다.

`objectExpression`은 블록에 삽입될 때 한번 평가됩니다. `objectExpression` 블록 내에서 `With`을 다시 할당할 수 없습니다.

`With` 블록 내에서 지정된 개체의 메서드와 속성을 한정하지 않고도 해당 메서드와 속성에 액세스할 수 있습니다. 다른 개체의 메서드와 속성을 사용할 수 있지만 메서드와 속성을 해당 개체 이름으로 한정해야 합니다.

하나의 `With...End With` 문을 배치할 수 있습니다. 참조 중인 개체가 컨텍스트에서 명확하지 않은 경우 중첩 `With...End With` 문이 혼동을 줄 수 있습니다. 개체가 내부 `With` 블록 내에서 참조되면 외부 `With` 블록에 있는 개체에 대한 정규화된 참조를 제공해야 합니다.

블록 외부에서 `With` 문 블록으로 분기할 수 없습니다.

블록에 루프가 없으면 문이 한 번만 실행됩니다. 다른 종류의 제어 구조를 중첩할 수 있습니다. 자세한 내용은 [중첩 컨트롤 구조](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)를 참조 하세요.

> [!NOTE]
> 개체 이니셜라이저에서도 `With` 키워드를 사용할 수 있습니다. 자세한 내용 및 예제를 보려면 [개체 이니셜라이저: 명명 된 형식과 익명](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md) 형식 및 [익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)입니다.
>
> 인스턴스화한 개체의 필드 또는 속성을 초기화하기 위해서만 `With` 블록을 사용하는 경우 대신 개체 이니셜라이저를 사용할 것을 고려하십시오.

## <a name="example"></a>예제

다음 예제에서는 각 `With` 블록이 단일 개체에 대해 일련의 문을 실행합니다.

[!code-vb[VbVbalrWithStatement#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrwithstatement/vb/mainwindow.xaml.vb#2)]

## <a name="example"></a>예제

다음 예제에서는 `With…End With` 문을 중첩시킵니다. 중첩된 `With` 문 내에서 구문은 내부 개체를 참조합니다.

[!code-vb[VbVbalrWithStatement#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrwithstatement/vb/mainwindow.xaml.vb#1)]

## <a name="see-also"></a>참고자료

- <xref:System.Collections.Generic.List%601>
- [중첩 제어 구조](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
- [개체 이니셜라이저: 명명 된 형식과 익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
