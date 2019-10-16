---
title: 레코드
description: 레코드가 명명 F# 된 값의 단순 집계를 나타내는 방법, 선택적으로 멤버를 사용 하는 방법에 대해 알아봅니다.
ms.date: 06/09/2019
ms.openlocfilehash: 874c5fa30a36f2778f7a43266316deb8c59d1d72
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216790"
---
# <a name="records"></a>레코드

레코드는 명명된 값의 간단한 집계(경우에 따라 멤버가 포함된)를 나타냅니다. 구조체 또는 참조 형식 중 하나일 수 있습니다.  기본적으로 참조 형식입니다.

## <a name="syntax"></a>구문

```fsharp
[ attributes ]
type [accessibility-modifier] typename =
    { [ mutable ] label1 : type1;
      [ mutable ] label2 : type2;
      ... }
    [ member-list ]
```

## <a name="remarks"></a>설명

위의 구문에서 *typename* 은 레코드 형식의 이름이 고, *label1* 및 *label2* 는 값의 이름이 며, *이름 이라고 하*고, *type1* 및 *type2* 는 이러한 값의 형식입니다. *멤버 목록은* 해당 형식에 대 한 멤버의 선택적 목록입니다.  `[<Struct>]` 특성을 사용 하 여 참조 형식인 레코드가 아닌 구조체 레코드를 만들 수 있습니다.

다음은 몇 가지 예입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1901.fs)]

각 레이블이 별도의 줄에 있으면 세미콜론은 선택 사항입니다.

*레코드 식*이라고 하는 식에서 값을 설정할 수 있습니다. 컴파일러는 사용 되는 레이블에서 형식을 유추 합니다 (레이블이 다른 레코드 형식과 충분히 다른 경우). 중괄호 ({})는 레코드 식을 묶습니다. 다음 코드에서는 레이블이 `x` `y` 인 세 개의 float 요소와로 레코드를 초기화 하는 레코드 식을 보여 줍니다. `z`

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1907.fs)]

레이블이 같은 다른 형식이 있을 수 있는 경우에는 약식 형식을 사용 하지 마십시오.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1903.fs)]

가장 최근에 선언 된 형식의 레이블은 이전에 선언 된 형식 보다 우선적으로 적용 되므로 앞의 예제 `mypoint3D` 에서는 `Point3D`로 유추 됩니다. 다음 코드와 같이 레코드 형식을 명시적으로 지정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1908.fs)]

클래스 형식과 마찬가지로 레코드 형식에 대해 메서드를 정의할 수 있습니다.

## <a name="creating-records-by-using-record-expressions"></a>레코드 식을 사용 하 여 레코드 만들기

레코드에 정의 된 레이블을 사용 하 여 레코드를 초기화할 수 있습니다. 이를 수행 하는 식을 *레코드 식*이라고 합니다. 중괄호를 사용 하 여 레코드 식을 묶고 세미콜론을 구분 기호로 사용 합니다.

다음 예제에서는 레코드를 만드는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1904.fs)]

레코드 식의 마지막 필드와 형식 정의에서 세미콜론은 모두 필드가 한 줄에 있는지 여부에 관계 없이 선택적 요소입니다.

레코드를 만들 때는 각 필드에 대 한 값을 제공 해야 합니다. 모든 필드에 대 한 초기화 식에서 다른 필드의 값을 참조할 수는 없습니다.

다음 코드에서의 `myRecord2` 형식은 필드 이름에서 유추 됩니다. 필요에 따라 형식 이름을 명시적으로 지정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

다른 형태의 레코드 생성은 기존 레코드를 복사 하 고 일부 필드 값을 변경 해야 하는 경우에 유용할 수 있습니다. 다음 코드 줄에서는이를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

레코드 식의 이러한 형태를 *복사 및 업데이트 레코드 식*이라고 합니다.

기본적으로 레코드를 변경할 수 없습니다. 그러나 복사 및 업데이트 식을 사용 하 여 수정 된 레코드를 쉽게 만들 수 있습니다. 변경할 수 있는 필드를 명시적으로 지정할 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1909.fs)]

레코드 필드에 DefaultValue 특성을 사용 하지 마세요. 기본 값으로 초기화 되는 필드를 사용 하 여 레코드의 기본 인스턴스를 정의한 다음, 복사 및 업데이트 레코드 식을 사용 하 여 기본값과 다른 필드를 설정 하는 것이 더 나은 방법입니다.

```fsharp
// Rather than use [<DefaultValue>], define a default record.
type MyRecord =
    { Field1 : int
      Field2 : int }

let defaultRecord1 = { Field1 = 0; Field2 = 0 }
let defaultRecord2 = { Field1 = 1; Field2 = 25 }

// Use the with keyword to populate only a few chosen fields
// and leave the rest with default values.
let rr3 = { defaultRecord1 with Field2 = 42 }
```

## <a name="creating-mutually-recursive-records"></a>상호 재귀 레코드 만들기

언젠가는 레코드를 만들 때 나중에 정의 하려는 다른 형식에 종속 시킬 수 있습니다. 이는 상호 재귀 되도록 레코드 형식을 정의 하지 않는 한 컴파일 오류입니다.

상호 재귀 레코드 정의는 `and` 키워드를 사용 하 여 수행 됩니다. 이렇게 하면 2 개 이상의 레코드 형식을 연결할 수 있습니다.

예를 들어 다음 코드는 `Person` 및 `Address` 형식을 상호 재귀로 정의 합니다.

```fsharp
// Create a Person type and use the Address type that is not defined
type Person =
  { Name: string
    Age: int
    Address: Address }
// Define the Address type which is used in the Person record
and Address =
  { Line1: string
    Line2: string
    PostCode: string
    Occupant: Person }
```

`and` 키워드를 사용 하지 않고 이전 예제를 정의 하는 경우에는 컴파일되지 않습니다. 키워드 `and` 는 상호 재귀 정의에 필요 합니다.

## <a name="pattern-matching-with-records"></a>레코드와 패턴 일치

패턴 일치에 레코드를 사용할 수 있습니다. 일부 필드를 명시적으로 지정 하 고 일치가 발생할 때 할당 되는 다른 필드에 대 한 변수를 제공할 수 있습니다. 다음 코드 예제에서는 그 구체적인 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1910.fs)]

이 코드의 출력은 다음과 같습니다.

```console
Point is at the origin.
Point is on the x-axis. Value is 100.000000.
Point is at (10.000000, 0.000000, -1.000000).
```

## <a name="differences-between-records-and-classes"></a>레코드와 클래스의 차이점

레코드 필드는 자동으로 속성으로 노출 되 고 레코드를 만들고 복사 하는 데 사용 된다는 점에서 클래스와 다릅니다. 또한 레코드 생성은 클래스 생성과 다릅니다. 레코드 형식에서 생성자를 정의할 수 없습니다. 대신이 항목에서 설명 하는 생성 구문이 적용 됩니다. 클래스는 생성자 매개 변수, 필드 및 속성 간에 직접적인 관계가 없습니다.

Union 및 구조체 형식과 마찬가지로 레코드는 구조적 같음 의미 체계를 포함 합니다. 클래스에는 참조 같음 의미 체계가 있습니다. 다음 코드 예제에서는 이 작업을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1911.fs)]

이 코드의 출력은 다음과 같습니다.

```console
The records are equal.
```

클래스를 사용 하 여 동일한 코드를 작성 하는 경우 두 개의 값이 힙에 두 개의 개체를 나타내고 주소만 비교 되므로 (클래스 형식이 메서드를 `System.Object.Equals` 재정의 하지 않는 경우) 두 클래스 개체는 같지 않습니다.

레코드에 대 한 참조 일치가 필요한 경우에는 레코드 `[<ReferenceEquality>]` 위에 특성을 추가 합니다.

## <a name="see-also"></a>참고 항목

- [F# 형식](fsharp-types.md)
- [클래스](classes.md)
- [F# 언어 참조](index.md)
- [Reference-Equality](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.referenceequalityattribute-class-%5bfsharp%5d)
- [패턴 일치](pattern-matching.md)
