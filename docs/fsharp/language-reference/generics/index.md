---
title: 제네릭
description: 코드를 반복 하지 F# 않고 다양 한 형식에서 작동 하는 코드를 작성할 수 있는 제네릭 함수 및 형식을 사용 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 5d6e57762095e44836425f90d21a6c1dc71edaaa
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666703"
---
# <a name="generics"></a>제네릭

F# 함수 값, 메서드, 속성 및 집계 형식(예: 클래스, 레코드 및 구분된 공용 구조체)은 *제네릭*일 수 있습니다. 제네릭 구문에는 형식 매개 변수가 하나 이상 포함됩니다. 형식 매개 변수는 제네릭 구문의 사용자가 일반적으로 지정합니다. 제네릭 함수 및 형식을 통해 각 형식에 대한 코드를 반복하지 않고 다양한 형식을 사용하는 코드를 작성할 수 있습니다. 컴파일러의 형식 유추 및 자동 일반화 메커니즘에서는 대개 코드를 암시적으로 제네릭으로 유추하므로 F#에서 코드를 제네릭 형식으로 지정하는 것은 간단할 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
// Explicitly generic function.
let function-name<type-parameters> parameter-list =
function-body

// Explicitly generic method.
[ static ] member object-identifer.method-name<type-parameters> parameter-list [ return-type ] =
method-body

// Explicitly generic class, record, interface, structure,
// or discriminated union.
type type-name<type-parameters> type-definition
```

## <a name="remarks"></a>설명

명시적으로 제네릭 함수 또는 형식을 선언하는 작업은 제네릭이 아닌 함수 또는 형식을 선언하는 작업과 매우 비슷합니다. 단, 함수 또는 형식 이름 뒤에 형식 매개 변수를 꺾쇠 괄호로 묶어 지정(및 사용)해야 합니다.

선언은 보통 암시적으로 제네릭인 것으로 간주됩니다. 함수 또는 형식을 작성하는 데 사용되는 모든 매개 변수의 형식을 완전하게 지정하지 않으면 컴파일러가 작성되는 코드에서 각 매개 변수, 값 및 변수의 형식을 유추하려고 합니다. 자세한 내용은 [형식 유추](../type-inference.md)를 참조하세요. 형식 또는 함수에 대한 코드에 매개 변수의 형식이 없으면 함수 또는 형식은 암시적으로 제네릭인 것으로 간주됩니다. 이 프로세스를 *자동 일반화*라고 합니다. 자동 일반화에는 몇 가지 제한이 있습니다. 예를 들어 F# 컴파일러가 제네릭 구문에 대한 형식을 유추할 수 없는 경우 컴파일러에서 *값 제한*이라는 제한을 나타내는 오류를 보고합니다. 이 경우 몇 가지 형식의 주석을 추가해야 할 수 있습니다. 자동 일반화 및 값 제한과 문제를 해결하도록 코드를 변경하는 방법에 대한 자세한 내용은 [자동 일반화](automatic-generalization.md)를 참조하세요.

이전 구문에서 *type-parameters*는 알 수 없는 형식을 나타내는 매개 변수의 쉼표로 구분 된 목록입니다. 각 매개 변수는 작은따옴표로 시작하고, 선택적으로 해당 형식 매개 변수에 사용되는 형식을 추가로 제한하는 제약 조건 절을 포함할 수 있습니다. 다양한 종류의 제약 조건 절 구문 및 제약 조건에 대한 기타 정보는 [제약 조건](constraints.md)을 참조하세요.

구문의 *type-definition*은 제네릭이 아닌 형식에 대한 형식 정의와 같습니다. 여기에는 클래스 형식에 대한 생성자 매개 변수, 선택적 `as` 절, 등호, 레코드 필드, `inherit` 절, 구분된 공용 구조체에 대한 선택 항목, `let` 및 `do` 바인딩, 멤버 정의 및 제네릭이 아닌 형식 정의에서 허용되는 기타 항목이 포함됩니다.

기타 구문 요소는 제네릭이 아닌 함수 및 형식에 대한 요소와 동일합니다. 예를 들어 *object-identifier*는 포함하는 개체 자체를 나타내는 식별자입니다.

속성, 필드 및 생성자는 바깥쪽 형식보다 더 제네릭일 수 없습니다. 또한 모듈의 값은 제네릭이 될 수 없습니다.

## <a name="implicitly-generic-constructs"></a>암시적인 제네릭 구문

F# 컴파일러가 코드에서 형식을 유추할 경우 제네릭일 수 있는 모든 함수를 제네릭으로 자동으로 처리합니다. 매개 변수 형식과 같은 형식을 명시적으로 지정하는 경우 자동 일반화가 방지됩니다.

다음 코드 예제에서 `makeList`는 해당 함수와 그 매개 변수가 명시적으로 제네릭으로 선언되지 않더라도 제네릭입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1700.fs)]

함수의 시그니처는 `'a -> 'a -> 'a list`로 유추됩니다. 이 예제의 `a` 및 `b`는 동일한 형식을 가지는 것으로 유추됩니다. 모두 이 목록에 함께 포함되며, 목록의 모든 요소가 동일한 형식이어야 하기 때문입니다.

형식 주석에 작은따옴표 구문을 사용하여 매개 변수 형식이 제네릭 형식 매개 변수임을 나타냄으로써 함수를 제네릭으로 지정할 수도 있습니다. 다음 코드에서 `function1`은 해당 매개 변수가 이 방식으로 형식 매개 변수로 선언되므로 제네릭입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1701.fs)]

## <a name="explicitly-generic-constructs"></a>명시적인 제네릭 구문

또한 꺾쇠 괄호에 형식 매개 변수를 명시적으로 선언하여(`<type-parameter>`) 함수를 제네릭으로 설정할 수도 있습니다. 다음 코드에서는 이를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1703.fs)]

## <a name="using-generic-constructs"></a>제네릭 구문 사용

제네릭 함수 또는 메서드를 사용하면 형식 인수를 지정해야 할 필요가 없습니다. 컴파일러는 형식 유추를 사용하여 적절한 형식 인수를 유추합니다. 여전히 모호한 경우 여러 개의 형식 인수를 쉼표로 구분하면서 꺾쇠 괄호에 형식 인수를 지정할 수 있습니다.

다음 코드는 이전 섹션에 정의된 함수의 사용을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1702.fs)]

> [!NOTE]
> 제네릭 형식을 이름으로 참조하는 방법에는 두 가지가 있습니다. 예를 들어 `list<int>` 및 `int list`는 단일 형식 인수 `int`를 포함하는 제네릭 형식 `list`를 참조하는 두 가지 방법입니다. 두 번째 형식은 일반적으로 기본 제공된 F# 형식(예: `list` 및 `option`)에서만 사용됩니다. 형식 인수가 여러 개 있으면 일반적으로 `Dictionary<int, string>` 구문을 사용할 수 있지만 `(int, string) Dictionary` 구문을 사용할 수도 있습니다.

## <a name="wildcards-as-type-arguments"></a>형식 인수로 와일드카드 사용

컴파일러에서 형식 인수를 유추하도록 지정하기 위해 명명된 형식 인수 대신 밑줄 또는 와일드카드 기호(`_`)를 사용할 수 있습니다. 다음 코드에서 이를 확인할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1704.fs)]

## <a name="constraints-in-generic-types-and-functions"></a>제네릭 형식 및 함수의 제약 조건

제네릭 형식 또는 함수 정의에서는, 제네릭 형식 매개 변수에 사용 가능할 수 있는 것으로 알려진 구문만 사용할 수 있습니다. 이는 컴파일 시간에 함수 및 메서드 호출의 확인을 지원하는 데 필요합니다. 형식 매개 변수를 명시적으로 선언하는 경우 특정 메서드 및 함수를 사용할 수 있다는 것을 컴파일러에 알리기 위해 명시적 제약 조건을 제네릭 형식 매개 변수에 적용할 수 있습니다. 그러나 F# 컴파일러에서 제네릭 매개 변수 형식을 유추하도록 허용하면 적절한 제약 조건이 자동으로 결정됩니다. 자세한 내용은 [제약 조건](constraints.md)을 참조하세요.

## <a name="statically-resolved-type-parameters"></a>정적으로 확인된 형식 매개 변수

F# 프로그램에서 사용할 수 있는 두 가지 종류의 형식 매개 변수가 있습니다. 첫 번째는 이전 섹션에 설명된 종류의 제네릭 형식 매개 변수입니다. 형식 매개 변수의 첫 번째 종류는 Visual Basic 및 C# 같은 언어에 사용되는 제네릭 형식 매개 변수와 동일합니다. 형식 매개 변수의 다른 종류는 F#에만 관련되며 *정적으로 확인된 형식 매개 변수*라고 합니다. 이러한 구문에 대한 내용은 [정적으로 확인된 형식 매개 변수](statically-resolved-type-parameters.md)를 참조하세요.

## <a name="examples"></a>예

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1705.fs)]

## <a name="see-also"></a>참고자료

- [언어 참조](../index.md)
- [유형](../fsharp-types.md)
- [정적으로 확인된 형식 매개 변수](statically-resolved-type-parameters.md)
- [제네릭](../../../standard/generics/index.md)
- [자동 일반화](automatic-generalization.md)
- [제약 조건](constraints.md)
