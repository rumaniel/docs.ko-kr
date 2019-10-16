---
title: 정적으로 확인된 형식 매개 변수
description: F# 정적으로 확인 된 형식 매개 변수를 사용 하는 방법에 대해 설명 합니다 .이 매개 변수는 컴파일 시간에 런타임에 대신 실제 형식으로 바뀝니다.
ms.date: 05/16/2016
ms.openlocfilehash: bc3310192cdaa5ae4862b8aee46b6152f61da38a
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71082920"
---
# <a name="statically-resolved-type-parameters"></a>정적으로 확인된 형식 매개 변수

*정적으로 확인 된 형식 매개 변수* 는 컴파일 타임에 런타임에 대신 실제 형식으로 대체 되는 형식 매개 변수입니다. 앞에 캐럿 (^) 기호가 있습니다.

## <a name="syntax"></a>구문

```fsharp
ˆtype-parameter
```

## <a name="remarks"></a>설명

F# 언어에는 두 가지 종류의 형식 매개 변수가 있습니다. 첫 번째 종류는 표준 제네릭 형식 매개 변수입니다. 이러한는 및 `'T` `'U`에서와 같이 아포스트로피 (')로 표시 됩니다. 다른 .NET Framework 언어의 제네릭 형식 매개 변수와 같습니다. 다른 종류는 정적으로 확인 되며 및 `^T` `^U`에서와 같이 캐럿 기호로 표시 됩니다.

정적으로 확인 된 형식 매개 변수는 멤버 제약 조건과 함께 사용 됩니다 .이 제약 조건은 형식 인수를 사용 하기 위해 특정 멤버를 포함 해야 하도록 지정할 수 있는 제약 조건입니다. 일반 제네릭 형식 매개 변수를 사용 하 여 이러한 종류의 제약 조건을 만들 수 있는 방법은 없습니다.

다음 표에서는 두 종류의 형식 매개 변수 간의 유사점과 차이점을 요약 하 여 보여 줍니다.

|기능|제네릭|정적으로 해결 됨|
|-------|-------|-------------------|
|구문|`'T`, `'U`|`^T`, `^U`|
|해결 시간|런타임|컴파일 시간|
|멤버 제약 조건|멤버 제약 조건과 함께 사용할 수 없습니다.|멤버 제약 조건과 함께 사용할 수 있습니다.|
|코드 생성|표준 제네릭 형식 매개 변수가 있는 형식 (또는 메서드)으로 인해 단일 제네릭 형식 또는 메서드가 생성 됩니다.|필요한 각 형식에 대해 하나씩, 형식 및 메서드의 여러 인스턴스화가 생성 됩니다.|
|형식과 함께 사용|형식에 사용할 수 있습니다.|는 형식에 사용할 수 없습니다.|
|인라인 함수와 함께 사용|아니요. 인라인 함수는 표준 제네릭 형식 매개 변수를 사용 하 여 매개 변수화 할 수 없습니다.|예. 인라인이 아닌 함수 또는 메서드에서는 정적으로 확인 된 형식 매개 변수를 사용할 수 없습니다.|

많은 F# 핵심 라이브러리 함수, 특히 연산자는 정적으로 형식 매개 변수를 확인 합니다. 이러한 함수 및 연산자는 인라인으로 되어 숫자 계산을 위한 효율적인 코드 생성을 생성 합니다.

연산자를 사용 하거나 정적으로 확인 된 형식 매개 변수를 사용 하는 다른 함수를 사용 하는 인라인 메서드 및 함수는 정적으로 확인 된 형식 매개 변수를 사용할 수도 있습니다. 대개 형식 유추는 정적으로 확인 된 형식 매개 변수를 갖도록 이러한 인라인 함수를 유추 합니다. 다음 예제에서는 정적으로 확인 된 형식 매개 변수를 갖도록 유추 되는 연산자 정의를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet401.fs)]

의 `(+@)` 확인 된 형식은 둘 다 `(+)` 의 사용을 기반으로 하며 `(*)`, 둘 다 형식 유추를 통해 정적으로 확인 된 형식 매개 변수에 대 한 멤버 제약 조건을 유추 합니다. F# 인터프리터와 같이 확인 된 형식은 다음과 같습니다.

```fsharp
^a -> ^c -> ^d
when (^a or ^b) : (static member ( + ) : ^a * ^b -> ^d) and
(^a or ^c) : (static member ( * ) : ^a * ^c -> ^b)
```

출력은 다음과 같습니다.

```console
2
1.500000
```

4\.1부터 F# 정적으로 확인 된 형식 매개 변수 시그니처에서 구체적 형식 이름을 지정할 수도 있습니다.  이전 버전의 언어에서 형식 이름은 실제로 컴파일러에서 유추 될 수 있지만 실제로 시그니처에는 지정할 수 없습니다.  4\.1의 F# 경우 정적으로 확인 된 형식 매개 변수 시그니처에서 구체적 형식 이름을 지정할 수도 있습니다. 예를 들면 다음과 같습니다.

```fsharp
let inline konst x _ = x

type CFunctor() = 
    static member inline fmap (f: ^a -> ^b, a: ^a list) = List.map f a
    static member inline fmap (f: ^a -> ^b, a: ^a option) =
        match a with
        | None -> None
        | Some x -> Some (f x)

    // default implementation of replace
    static member inline replace< ^a, ^b, ^c, ^d, ^e when ^a :> CFunctor and (^a or ^d): (static member fmap: (^b -> ^c) * ^d -> ^e) > (a, f) =
        ((^a or ^d) : (static member fmap : (^b -> ^c) * ^d -> ^e) (konst a, f))

    // call overridden replace if present
    static member inline replace< ^a, ^b, ^c when ^b: (static member replace: ^a * ^b -> ^c)>(a: ^a, f: ^b) =
        (^b : (static member replace: ^a * ^b -> ^c) (a, f))

let inline replace_instance< ^a, ^b, ^c, ^d when (^a or ^c): (static member replace: ^b * ^c -> ^d)> (a: ^b, f: ^c) =
        ((^a or ^c): (static member replace: ^b * ^c -> ^d) (a, f))

// Note the concrete type 'CFunctor' specified in the signature
let inline replace (a: ^a) (f: ^b): ^a0 when (CFunctor or  ^b): (static member replace: ^a *  ^b ->  ^a0) =
    replace_instance<CFunctor, _, _, _> (a, f)
```

## <a name="see-also"></a>참고자료

- [제네릭](index.md)
- [형식 유추](../type-inference.md)
- [자동 일반화](automatic-generalization.md)
- [제약 조건](constraints.md)
- [인라인 함수](../functions/inline-functions.md)
