---
title: 속성(F#)
description: 'F # 속성을 개체에 연결 된 값을 나타내는 멤버에 알아봅니다.'
ms.date: 05/16/2016
ms.openlocfilehash: 75d21415b44ccc1c26ef5f478d5f5de20c3412e8
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197927"
---
# <a name="properties"></a>속성

*속성* 은 개체에 연결 된 값을 나타내는 멤버입니다.

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

속성이 나타내는 "에" 개체 지향 프로그래밍에서 개체 인스턴스를 사용 하 여 또는 형식의 정적 속성에 대 한 연결 된 데이터를 나타내는 관계입니다.

속성에 대 한 백업 저장소 라고도 하는 내부 값을 명시적으로 지정 하려는 여부 또는 백업 저장소를 자동으로 생성 하도록 컴파일러에 허용 하려는 경우에 따라 두 가지 방법으로 속성을 선언할 수 있습니다. 일반적으로 속성 값 또는 변수에 대 한 간단한 래퍼만 경우에 명시적 속성 구현이 trivial이 아닌 경우 및 방법을 자동을 사용 해야 합니다. 속성을 명시적으로 선언, 사용 된 `member` 키워드입니다. 이 선언적 구문을 지정 하는 구문을 사용 하 여 다음 합니다 `get` 하 고 `set` 라고도 하는 메서드를 *접근자*. 읽기/쓰기, 읽기 및 쓰기 전용 속성에 대 한 다양 한 형태의 구문 섹션에 표시 된 명시적 구문이 사용 됩니다. 읽기 전용 속성에 대 한 정의을 `get` 메서드를 쓰기 전용 속성에 대 한 정의을 `set` 메서드. 속성을 둘 다 포함 하는 경우 사용자에 게 유의 `get` 및 `set` 접근자는 대체 구문을 사용 하 여 특성 및 다음 코드에 표시 된 대로 각 접근자에 대 한 다른 액세스 가능성 한정자를 지정할 수 있습니다.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3201.fs)]

모두 포함 하는 읽기/쓰기 속성을 `get` 및 `set` 메서드를 순서 `get` 및 `set` 되돌릴 수 있습니다. 또는 구문에 대 한 표시를 제공할 수 있습니다 `get` 만 및에 표시 된 구문은 `set` 만 결합 된 구문을 사용 하는 대신 합니다. 이렇게 쉽게 개별 주석 `get` 또는 `set` 메서드를 수행 해야 할 것입니다. 이 방법은 결합 된 구문을 사용 하 여 다음 코드에 표시 됩니다.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3203.fs)]

개인 값 속성에 대 한 데이터 라고 하는 보류 *백업 저장소*합니다. 백업 저장소를 자동으로 만드는 컴파일러를 하려면 키워드 사용 `member val`를 자체 식별자를 생략 한 다음 속성을 초기화 하는 식을 제공 합니다. 속성에 mutable로 경우 `with get, set`합니다. 예를 들어, 다음 클래스 형식에는 두 가지 자동으로 구현 된 속성이 포함 됩니다. `Property1` 읽기 전용인 지 고 기본 생성자에 제공 되는 인수를 초기화 하 고 `Property2` 설정 가능한 속성을 빈 문자열로 초기화 됩니다.

```fsharp
type MyClass(property1 : int) =
member val Property1 = property1
member val Property2 = "" with get, set
```

자동으로 구현 된 속성 포함 되므로 형식 초기화 하는 것과 마찬가지로 다른 멤버 정의 하기 전에 포함 되어야 합니다 `let` 바인딩 및 `do` 바인딩 형식 정의입니다. 속성에 액세스할 때마다 없습니다 및를 초기화 하면 자동으로 구현 된 속성을 초기화 하는 식만 평가 note 합니다. 이 동작은 명시적으로 구현 된 속성의 동작과 대조적입니다. 효과적으로 즉, 이러한 속성을 초기화 하는 코드는 클래스의 생성자에 추가 됩니다. 이러한 차이 보여 주는 다음 코드를 살펴보세요.

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

```
class1.AutoProperty = 1853799794
class1.AutoProperty = 1853799794
class1.ExplicitProperty = 978922705
class1.ExplicitProperty = 1131210765
```

앞의 코드의 출력 임을 보여 줍니다 AutoProperty 값 없습니다 변경 반복적으로 호출 하는 경우는 ExplicitProperty를 호출할 때마다를 변경 하는 반면. 명시적 속성의 getter 메서드를 자동으로 구현 된 속성에 대 한 식이 계산 될 때마다 하지 않는다는 보여줍니다.

>[!WARNING]
Entity Framework와 같은 일부 라이브러리가 (`System.Data.Entity`) 자동으로 구현 된 속성의 초기화를 사용 하 여 제대로 작동 하지 않는 기본 클래스 생성자의 사용자 지정 작업을 수행 합니다. 이러한 경우 명시적 속성을 사용 하 여 시도 하세요.

속성은 클래스, 구조체, 구별 된 공용 구조체, 레코드, 인터페이스 및 형식 확장의 멤버일 수 있습니다 및 개체 식에 정의할 수도 있습니다.

특성 속성에 적용할 수 있습니다. 특성 속성에 적용할 특성을 속성 앞에 있는 별도 줄에 작성 합니다. 자세한 내용은 [특성](../attributes.md)을 참조하세요.

기본적으로 속성은 공용입니다. 액세스 가능성 한정자 속성에도 적용할 수 있습니다. 액세스 가능성 한정자를 적용 하려면 추가 속성의 이름 바로 앞에 둘 다에 적용 되어야 하는 경우는 `get` 및 `set` 메서드를 추가 하기 전에 `get` 및 `set` 다른 액세스 가능성은 경우에 키워드 각 접근자에 필요합니다. *접근성 한정자* 다음 중 하나일 수 있습니다: `public`, `private`, `internal`합니다. 자세한 내용은 [액세스 제어](../access-control.md)를 참조하세요.

속성 구현이 속성에 액세스할 때마다 실행 됩니다.

## <a name="static-and-instance-properties"></a>정적 및 인스턴스 속성

속성은 인스턴스 속성 또는 정적 수 있습니다. 정적 속성 인스턴스 없이 호출할 수 있습니다 및 개별 개체를 사용 하 여 하지 형식과 연결 된 값에 사용 됩니다. 정적 속성에 대 한 자체 식별자를 생략 합니다. 자체 식별자가 인스턴스 속성 필요 합니다.

다음 정적 속성 정의 정적 필드에 시나리오를 토대로 `myStaticValue` 속성에 대 한 백업 저장소입니다.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3204.fs)]

속성 일 수도 있습니다 배열 형식의 호출 되는 경우 *인덱싱된 속성*합니다. 자세한 내용은 [Indexed Properties](indexed-properties.md)합니다.

## <a name="type-annotation-for-properties"></a>속성의 형식 주석

대부분의 경우에서 컴파일러는 백업 저장소의 형식에서 속성의 형식을 유추 하는 데 충분 한 정보가 있지만 형식 주석을 추가 하 여 형식을 명시적으로 설정할 수 있습니다.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3205.fs)]

## <a name="using-property-set-accessors"></a>속성을 사용 하 여 set 접근자

제공 하는 속성을 설정할 수 있습니다 `set` 를 사용 하 여 접근자를 `<-` 연산자입니다.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3206.fs)]

출력은 **20**합니다.

## <a name="abstract-properties"></a>추상 속성

속성은 abstract 일 수 있습니다. 메서드의 경우와 마찬가지로 `abstract` 속성과 연결 된 가상 디스패치가 임을 의미 합니다. 추상 속성은 동일한 클래스에서 정의 하지 않고 즉, 실제로 추상 수 있습니다. 이러한 속성을 포함 하는 클래스는 추상 클래스 이므로 합니다. 또는 추상 속성 이며 가상 경우 정의가 있어야 같은 클래스에는 방금 의미할 수 있습니다. 추상 속성 개인 아니어야 하 고도 해야 다른 하나의 접근자 abstract 이면 추상 일. 추상 클래스에 대 한 자세한 내용은 참조 하세요. [추상 클래스](../abstract-classes.md)합니다.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3207.fs)]

## <a name="see-also"></a>참고자료

- [멤버](index.md)
- [메서드](methods.md)
