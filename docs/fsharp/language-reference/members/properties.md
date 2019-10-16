---
title: 속성
description: 개체와 F# 연결 된 값을 나타내는 멤버인 속성에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: c71d61e033501c2d535b5582c82d36ed8cb2241b
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216423"
---
# <a name="properties"></a>속성

*속성* 은 개체와 연결 된 값을 나타내는 멤버입니다.

## <a name="syntax"></a>구문

```fsharp
// Property that has both get and set defined.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with [accessibility-modifier] get() =
    get-function-body
and [accessibility-modifier] set parameter =
    set-function-body

// Alternative syntax for a property that has get and set.
[ attributes-for-get ]
[ static ] member [accessibility-modifier-for-get] [self-identifier.]PropertyName =
    get-function-body
[ attributes-for-set ]
[ static ] member [accessibility-modifier-for-set] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName =
    get-function-body

// Alternative syntax for property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with get() =
    get-function-body

// Property that has set only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Automatically implemented properties.
[ attributes ]
[ static ] member val [accessibility-modifier] PropertyName = initialization-expression [ with get, set ]
```

## <a name="remarks"></a>설명

속성은 개체에 연결 된 데이터를 나타내는 개체 지향 프로그래밍의 "있음" 관계를 나타냅니다. 정적 속성의 경우에는 형식을 사용 합니다.

속성에 대 한 기본 값 (백업 저장소 라고도 함)을 명시적으로 지정 하는지 아니면 컴파일러가 자동으로 백업 저장소를 생성할 수 있는지에 따라 두 가지 방법으로 속성을 선언할 수 있습니다. 일반적으로 속성에 특수 한 구현이 있는 경우 보다 명시적인 방법을 사용 하 고 속성이 값 또는 변수에 대 한 간단한 래퍼 일 때 자동으로 사용 해야 합니다. 속성을 명시적으로 선언 하려면 `member` 키워드를 사용 합니다. 이 선언적 구문 뒤에는 `get` 및 `set` 메서드 (명명 된 *접근자*)를 지정 하는 구문이 있습니다. 구문 섹션에 표시 된 다양 한 형식의 명시적 구문은 읽기/쓰기, 읽기 전용 및 쓰기 전용 속성에 사용 됩니다. 읽기 전용 속성의 경우 `get` 메서드만 정의 합니다. 쓰기 전용 속성의 경우 `set` 메서드만 정의 합니다. 속성에 및 `get` `set` 접근자가 모두 있는 경우에는 다음 코드에 표시 된 것 처럼 대체 구문을 사용 하 여 각 접근자에 대해 다른 특성 및 액세스 가능성 한정자를 지정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3201.fs)]

`get` 및 `get` `set` 메서드를 모두 포함 하는 읽기/쓰기 속성의 경우 및의 순서를 반대로 바꿀 수 있습니다. `set` 또는 결합 된 구문을 사용 하는 대신에 `get` 대해서만 표시 되는 구문 `set` 및에 대해 표시 된 구문도 제공할 수 있습니다. 이렇게 하면 개별 `get` 또는 `set` 메서드를 쉽게 주석으로 처리할 수 있습니다. 다음 코드에서는 조합 된 구문 사용에 대 한 대안을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3203.fs)]

속성의 데이터를 포함 하는 전용 값을 *백업 저장소*라고 합니다. 컴파일러가 백업 저장소를 자동으로 만들도록 하려면 키워드 `member val`를 사용 하 여 자체 식별자를 생략 한 다음 속성을 초기화 하는 식을 제공 합니다. 속성을 변경할 수 있으면를 포함 `with get, set`합니다. 예를 들어 다음 클래스 형식은 자동으로 구현 된 두 개의 속성을 포함 합니다. `Property1`는 읽기 전용 이며 기본 생성자에 제공 된 인수로 초기화 되며, `Property2` 는 설정 가능한 속성은 빈 문자열로 초기화 됩니다.

```fsharp
type MyClass(property1 : int) =
member val Property1 = property1
member val Property2 = "" with get, set
```

자동으로 구현 된 속성은 형식 초기화의 일부 이므로 형식 정의에서 `let` `do` 바인딩과 바인딩과 마찬가지로 다른 멤버 정의 앞에 포함 되어야 합니다. 자동으로 구현 된 속성을 초기화 하는 식은 초기화 시에만 계산 되며 속성에 액세스할 때마다 계산 되지 않습니다. 이 동작은 명시적으로 구현 된 속성의 동작과는 대조적입니다. 이는 실제로 이러한 속성을 초기화 하는 코드가 클래스의 생성자에 추가 된다는 것을 의미 합니다. 이러한 차이를 표시 하는 다음 코드를 고려 합니다.

```fsharp
type MyClass() =
    let random  = new System.Random()
    member val AutoProperty = random.Next() with get, set
    member this.ExplicitProperty = random.Next()

let class1 = new MyClass()

printfn "class1.AutoProperty = %d" class1.AutoProperty
printfn "class1.AutoProperty = %d" class1.AutoProperty
printfn "class1.ExplicitProperty = %d" class1.ExplicitProperty
printfn "class1.ExplicitProperty = %d" class1.ExplicitProperty
```

**출력**

```console
class1.AutoProperty = 1853799794
class1.AutoProperty = 1853799794
class1.ExplicitProperty = 978922705
class1.ExplicitProperty = 1131210765
```

이전 코드의 출력에서는 반복적으로 호출 될 때 AutoProperty 값이 변경 되지 않은 반면 ExplicitProperty가 호출 될 때마다 변경 되는 것을 보여 줍니다. 이는 명시적 속성에 대 한 getter 메서드와 마찬가지로 자동으로 구현 된 속성에 대 한 식이 매번 계산 되지 않는 것을 보여 줍니다.

>[!WARNING]
>자동으로 구현 된 속성을 초기화 하는 경우`System.Data.Entity`제대로 작동 하지 않는 기본 클래스 생성자에서 사용자 지정 작업을 수행 하는 Entity Framework ()와 같은 몇 가지 라이브러리가 있습니다. 이러한 경우에는 명시적 속성을 사용 하십시오.

속성은 클래스, 구조체, 구분 된 공용 구조체, 레코드, 인터페이스 및 형식 확장의 멤버일 수 있으며 개체 식에 정의할 수도 있습니다.

속성에 특성을 적용할 수 있습니다. 속성에 특성을 적용 하려면 속성 앞에 별도의 줄에 특성을 씁니다. 자세한 내용은 [특성](../attributes.md)을 참조하세요.

기본적으로 속성은 public입니다. 액세스 가능성 한정자는 속성에도 적용할 수 있습니다. 액세스 가능성 한정자를 적용 `get` 하려면 및 `set` 메서드에 둘 다 적용 될 경우 속성 이름 바로 앞에 추가 하 고, 다른 액세스 가능성이 다른 경우 및 `set` 키워드 앞에 `get` 추가 합니다. 각 접근자에 필요 합니다. *액세스 가능성 한정자* 는, `public` `private`, `internal`중 하나일 수 있습니다. 자세한 내용은 [액세스 제어](../access-control.md)를 참조하세요.

속성에 액세스할 때마다 속성 구현이 실행 됩니다.

## <a name="static-and-instance-properties"></a>정적 및 인스턴스 속성

속성은 정적 또는 인스턴스 속성 일 수 있습니다. 정적 속성은 인스턴스 없이 호출할 수 있으며 개별 개체가 아닌 형식과 연결 된 값에 사용 됩니다. 정적 속성의 경우 자체 식별자를 생략 합니다. 인스턴스 속성에는 자체 식별자가 필요 합니다.

다음 정적 속성 정의는 속성의 백업 저장소 인 정적 필드가 `myStaticValue` 있는 시나리오를 기반으로 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3204.fs)]

속성은 배열과 같을 수도 있으며,이 경우 *인덱싱된 속성*이라고 합니다. 자세한 내용은 [인덱싱된 속성](indexed-properties.md)을 참조 하세요.

## <a name="type-annotation-for-properties"></a>속성에 대 한 형식 주석

대부분의 경우 컴파일러는 백업 저장소의 형식에서 속성의 형식을 유추할 수 있는 충분 한 정보를 갖지만 형식 주석을 추가 하 여 명시적으로 형식을 설정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3205.fs)]

## <a name="using-property-set-accessors"></a>속성 집합 접근자 사용

연산자를 `set` `<-` 사용 하 여 접근자를 제공 하는 속성을 설정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3206.fs)]

출력은 **20**입니다.

## <a name="abstract-properties"></a>추상 속성

속성은 abstract 일 수 있습니다. 메서드와 마찬가지로, `abstract` 속성에 연결 된 가상 디스패치가 있음을 의미 합니다. 추상 속성은 실제로 추상 속성이 될 수 있습니다. 즉, 동일한 클래스에 정의가 없을 수 있습니다. 따라서 이러한 속성을 포함 하는 클래스는 추상 클래스입니다. 또는 abstract는 속성이 가상 임을 의미할 수 있으며,이 경우 정의가 동일한 클래스에 있어야 합니다. 추상 속성은 private이 아니어야 하며 한 접근자가 abstract 인 경우 다른 접근자도 추상 이어야 합니다. 추상 클래스에 대 한 자세한 내용은 [추상 클래스](../abstract-classes.md)를 참조 하세요.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3207.fs)]

## <a name="see-also"></a>참고 항목

- [멤버](index.md)
- [메서드](methods.md)
