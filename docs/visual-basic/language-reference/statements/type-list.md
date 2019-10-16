---
title: 형식 목록(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- StructureConstraint
- vb.StructureConstraint
- ClassConstraint
- vb.ClassConstraint
helpviewer_keywords:
- class constraint
- constraints, Visual Basic generic types
- generic parameters
- generics [Visual Basic], constraints
- generics [Visual Basic], type list
- structure constraint
- constraints, in type parameters
- generics [Visual Basic], generic types
- parameters [Visual Basic], type
- constraints, Structure keyword
- type parameters [Visual Basic], constraints
- types [Visual Basic], generic
- parameters [Visual Basic], generic
- generics [Visual Basic], type parameters
- type parameters
- constraints, Class keyword
ms.assetid: 56db947a-2ae8-40f2-a70a-960764e9d0db
ms.openlocfilehash: aae9135207bbd3f9d0cc7c072e423a50902c372a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64751511"
---
# <a name="type-list-visual-basic"></a>형식 목록(Visual Basic)

지정 된 *형식 매개 변수* 에 대 한를 *제네릭* 프로그래밍 요소입니다. 여러 매개 변수는 쉼표로 구분 됩니다. 다음은 하나의 형식 매개 변수에 대해 구문이입니다.

## <a name="syntax"></a>구문

```
[genericmodifier] typename [ As constraintlist ]
```

## <a name="parts"></a>요소

|용어|정의|
|---|---|
|`genericmodifier`|선택 사항입니다. 제네릭 인터페이스 및 대리자에만 사용할 수 있습니다. 형식을 선언할 수 있습니다는 공변 (covariant)를 사용 하 여는 [아웃](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md) 키워드 또는 사용 하 여 반공 변 합니다 [에서](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md) 키워드입니다. [공변성(Covariance) 및 반공변성(Contravariance)](../../programming-guide/concepts/covariance-contravariance/index.md)을 참조하세요.|
|`typename`|필수 요소. 형식 매개 변수의 이름입니다. 이 자리 표시자를 해당 형식 인수에 의해 제공 되는 정의 된 형식으로 교체 합니다.|
|`constraintlist`|선택 사항입니다. 에 제공할 수 있는 데이터 형식을 제한 하는 요구 사항 목록은 `typename`합니다. 여러 제약 조건이 있으면 중괄호로 묶습니다 (`{ }`) 및 쉼표로 구분 합니다. 제약 조건 목록을 사용 하 여 정의 해야 합니다 [으로](../../../visual-basic/language-reference/statements/as-clause.md) 키워드입니다. 사용할 `As` 목록 맨 앞에 한 번만 합니다.|

## <a name="remarks"></a>설명

모든 제네릭 프로그래밍 요소는 하나 이상의 형식 매개 변수를 수행 해야 합니다. 형식 매개 변수는 특정 형식에 대 한 자리 표시자 (한 *생성 된 요소*) 클라이언트 코드는 제네릭 형식의 인스턴스를 만들 때 지정 하는 합니다. 제네릭 클래스를 정의 구조체, 인터페이스, 프로시저 하거나 위임할 수입니다.

제네릭 형식을 정의 하는 경우에 대 한 자세한 내용은 참조 하세요. [Visual Basic의 제네릭 형식](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)합니다. 형식 매개 변수 이름에 대 한 자세한 내용은 참조 하세요. [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)합니다.

## <a name="rules"></a>규칙

- **괄호입니다.** 형식 매개 변수 목록을 제공 하 고 괄호로 묶어야 목록 정의 해야 하는 경우는 [의](../../../visual-basic/language-reference/statements/of-clause.md) 키워드입니다. 사용할 `Of` 목록 맨 앞에 한 번만 합니다.

- **제약 조건입니다.** 목록을 *제약 조건* 형식에 매개 변수는 다음 항목이을 임의로 조합 하 합니다.

  - 원하는 수의 인터페이스입니다. 제공된 된 형식이 목록에서 모든 인터페이스를 구현 해야 합니다.

  - 최대 하나의 클래스입니다. 제공된 된 형식 클래스에서 상속 해야 합니다.

  - `New` 키워드입니다. 제공된 된 형식 제네릭 형식에 액세스할 수 있는 매개 변수가 없는 생성자를 노출 해야 합니다. 하나 이상의 인터페이스에서 형식 매개 변수를 제한 하는 경우에 유용 합니다. 인터페이스를 구현 하는 형식 생성자를 반드시 노출 하지 않습니다 하 고 생성자의 액세스 수준에 따라 제네릭 형식 내에서 코드 못할 액세스할 수 있습니다.

  - 중 하나는 `Class` 키워드 또는 `Structure` 키워드입니다. `Class` 키워드는 전달 된 형식 인수가 참조 형식, 문자열, 배열 또는 대리자, 예를 들어 이어야 또는 클래스에서 개체를 만들 필요를 제네릭 형식 매개 변수를 제한 합니다. `Structure` 키워드는 구조체, 열거형 또는 기본 데이터의 형식 예를 들어 제네릭 형식 매개 변수 전달 된 형식 인수가 값 형식 되도록 할 제한 합니다. 둘 다 포함할 수 없습니다 `Class` 하 고 `Structure` 동일한 `constraintlist`입니다.

  제공된 된 형식에 포함할 모든 요구 사항을 충족 해야 `constraintlist`합니다.

  각 형식 매개 변수에 대 한 제약 조건을 다른 형식 매개 변수에 대 한 제약 조건입니다.

## <a name="behavior"></a>동작

- **컴파일 타임 대체 합니다.** 제네릭 프로그래밍 요소에서 생성된 된 형식을 만들면 각 형식 매개 변수에 대해 정의 된 형식을 제공 합니다. Visual Basic 컴파일러의 모든 위치에 대 한 제공 된 형식임을 대체 `typename` 제네릭 요소 내에서.

- **제약 조건 없음입니다.** 형식 매개 변수의 모든 제약 조건을 지정 하지 않으면, 경우에 코드는 작업 및 멤버에서 지원 되는로 제한 됩니다 합니다 [Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md) 해당 형식 매개 변수에 대 한 합니다.

## <a name="example"></a>예제

다음 예제에서는 사전에 새 항목을 추가 하는 기본 함수를 포함 하는 제네릭 사전 클래스의 기본 정의 보여 줍니다.

[!code-vb[VbVbalrStatements#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#3)]

## <a name="example"></a>예제

때문에 `dictionary` 는 일반, 코드를 사용 하는 각 만들 수 다양 한 개체에서 다른 데이터 형식에서 작동 되지만 동일한 기능이 있습니다. 다음 예제에서는 만든 코드 줄을 `dictionary` 개체를 `String` 항목 및 `Integer` 키입니다.

[!code-vb[VbVbalrStatements#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#4)]

## <a name="example"></a>예제

다음 예제에서는 앞의 예제에서 생성 된 해당 기본 정의 보여 줍니다.

[!code-vb[VbVbalrStatements#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#5)]

## <a name="see-also"></a>참고자료

- [Of](../../../visual-basic/language-reference/statements/of-clause.md)
- [New 연산자](../../../visual-basic/language-reference/operators/new-operator.md)
- [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [Object 데이터 형식](../../../visual-basic/language-reference/data-types/object-data-type.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [방법: 제네릭 클래스 사용](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [공 분산 및 반공 분산](../../programming-guide/concepts/covariance-contravariance/index.md)
- [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)
- [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)
