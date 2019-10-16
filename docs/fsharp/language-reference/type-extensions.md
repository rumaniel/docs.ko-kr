---
title: 형식 확장
description: 형식 확장 F# 을 사용 하 여 이전에 정의한 개체 형식에 새 멤버를 추가 하는 방법을 알아봅니다.
ms.date: 02/08/2019
ms.openlocfilehash: 5d31d87095d3381e66dc32da4b6d7bb746886406
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106850"
---
# <a name="type-extensions"></a>형식 확장

형식 확장명 ( _확대_이 라고도 함)은 이전에 정의 된 개체 형식에 새 멤버를 추가할 수 있는 기능 패밀리입니다. 세 가지 기능은 다음과 같습니다.

- 내장 형식 확장
- 선택적 형식 확장
- 확장 메서드

각각 서로 다른 시나리오에서 사용할 수 있으며 서로 다른 장단점이 있습니다.

## <a name="syntax"></a>구문

```fsharp
// Intrinsic and optional extensions
type typename with
    member self-identifier.member-name =
        body
    ...

// Extension methods
open System.Runtime.CompilerServices

[<Extension>]
type Extensions() =
    [static] member self-identifier.extension-name (ty: typename, [args]) =
        body
    ...
```

## <a name="intrinsic-type-extensions"></a>내장 형식 확장

내장 형식 확장은 사용자 정의 형식을 확장 하는 형식 확장명입니다.

내장 형식 확장은 확장 하는 형식과 동일한 파일 **및** 네임 스페이스 또는 모듈에서 정의 되어야 합니다. 다른 모든 정의는 [선택적 형식 확장이](type-extensions.md#optional-type-extensions)됩니다.

형식 선언에서 기능을 분리 하는 것이 기본 형식 확장의 경우에 따라 간단 합니다. 다음 예제에서는 내장 형식 확장을 정의 하는 방법을 보여 줍니다.

```fsharp
namespace Example

type Variant =
    | Num of int
    | Str of string
  
module Variant =
    let print v =
        match v with
        | Num n -> printf "Num %d" n
        | Str s -> printf "Str %s" s

// Add a member to Variant as an extension
type Variant with
    member x.Print() = Variant.print x
```

형식 확장을 사용 하면 다음을 구분할 수 있습니다.

- `Variant` 형식의 선언입니다.
- "셰이프"에 `Variant` 따라 클래스를 인쇄 하는 기능
- 개체 스타일 `.`표기법을 사용 하 여 인쇄 기능에 액세스 하는 방법

이 방법은 모든 항목을의 `Variant`멤버로 정의 하는 방법에 대 한 대안입니다. 본질적으로 더 나은 방법은 아니지만 일부 상황에서 기능을 보다 명확 하 게 표현할 수 있습니다.

내장 형식 확장은 사용자가 확장 하는 형식의 멤버로 컴파일되며 리플렉션을 통해 형식을 검사할 때 형식에 표시 됩니다.

## <a name="optional-type-extensions"></a>선택적 형식 확장

선택적 형식 확장은 확장 중인 형식의 원래 모듈, 네임 스페이스 또는 어셈블리 외부에 표시 되는 확장입니다.

선택적 형식 확장은 직접 정의 하지 않은 형식을 확장 하는 데 유용 합니다. 예를 들어:

```fsharp
module Extensions

open System.Collections.Generic

type IEnumerable<'T> with
    /// Repeat each element of the sequence n times
    member xs.RepeatElements(n: int) =
        seq {
            for x in xs do
                for i in 1 .. n do
                    yield x
        }
```

이제 작업 중인 범위 `RepeatElements` 에서 `Extensions` 모듈이 열리는 경우에만의 <xref:System.Collections.Generic.IEnumerable%601> 멤버인 것 처럼 액세스할 수 있습니다.

리플렉션을 통해 검사할 때 확장 형식에는 선택적 확장이 표시 되지 않습니다. 선택적 확장은 모듈에 있어야 하며 확장을 포함 하는 모듈이 열려 있거나 달리 범위에 있는 경우에만 범위에 포함 됩니다.

선택적 확장 멤버는 개체 인스턴스가 첫 번째 매개 변수로 암시적으로 전달 되는 정적 멤버로 컴파일됩니다. 그러나 이러한 사용자는 선언 된 방법에 따라 인스턴스 멤버 또는 정적 멤버인 것 처럼 작동 합니다.

선택적 확장 멤버도 또는 VB 소비자에 게 C# 표시 되지 않습니다. 다른 F# 코드 에서만 사용할 수 있습니다.

## <a name="generic-limitation-of-intrinsic-and-optional-type-extensions"></a>내장 및 선택적 형식 확장의 일반적인 제한 사항

형식 변수가 제한 되는 제네릭 형식에 대해 형식 확장을 선언할 수 있습니다. 요구 사항은 확장 선언의 제약 조건이 선언 된 형식의 제약 조건과 일치 한다는 것입니다.

그러나 제약 조건이 선언 된 형식과 형식 확장명 사이에 일치 하는 경우에도 선언 된 형식에 비해 형식 매개 변수에 대해 다른 요구 사항을 적용 하는 확장 멤버의 본문에서 제약 조건을 유추할 수 있습니다. 예를 들어:

```fsharp
open System.Collections.Generic

// NOT POSSIBLE AND FAILS TO COMPILE!
//
// The member 'Sum' has a different requirement on 'T than the type IEnumerable<'T>
type IEnumerable<'T> with
    member this.Sum() = Seq.sum this
```

선택적 형식 확장을 사용 하 여이 코드를 가져올 수 있는 방법은 없습니다.

- 인 경우 멤버는 `Sum` 형식 확장에서 정의 하는 `'T` 것과 `static member (+)`다른 제약 조건 (`static member get_Zero` 및)을 갖습니다.
- 와 `Sum` 동일한 제약 조건을 갖도록 형식 확장을 수정 하면에 대 한 `IEnumerable<'T>`정의 된 제약 조건과 더 이상 일치 하지 않습니다.
- `member this.Sum` 로`member inline this.Sum` 변경 하면 형식 제약 조건이 일치 하지 않는 오류가 발생 합니다.

필요한 것은 "공간에 배치" 되 고 형식을 확장 하는 것 처럼 표시 될 수 있는 정적 메서드입니다. 여기서는 확장 메서드가 필요 합니다.

## <a name="extension-methods"></a>확장 메서드

마지막으로, 확장 메서드 ("C# 스타일 확장 멤버" 라고도 함)를 클래스의 F# 정적 멤버 메서드로 선언할 수 있습니다.

확장 메서드는 형식 변수를 제약 하는 제네릭 형식에 대 한 확장을 정의 하려는 경우에 유용 합니다. 예를 들어:

```fsharp
namespace Extensions

open System.Runtime.CompilerServices

[<Extension>]
type IEnumerableExtensions() =
    [<Extension>]
    static member inline Sum(xs: IEnumerable<'T>) = Seq.sum xs
```

이 코드를 사용 하면가 열리거나 범위 내에 있는 `Sum` 경우이 코드 <xref:System.Collections.Generic.IEnumerable%601>는에 `Extensions` 정의 된 것 처럼 표시 됩니다.

## <a name="other-remarks"></a>기타 설명

형식 확장에는 다음과 같은 특성도 있습니다.

- 액세스할 수 있는 모든 형식을 확장할 수 있습니다.
- 내장 함수와 선택적 형식 확장은 메서드 뿐 아니라 멤버 형식을 정의할 수 있습니다. 따라서 확장명 속성도 가능 합니다 (예:).
- [구문](type-extensions.md#syntax)의 `self-identifier` 토큰은 일반 멤버와 마찬가지로 호출 중인 형식의 인스턴스를 나타냅니다.
- 확장 멤버는 정적 또는 인스턴스 멤버일 수 있습니다.
- 형식 확장의 형식 변수는 선언 된 형식의 제약 조건과 일치 해야 합니다.

형식 확장에는 다음과 같은 제한 사항이 있습니다.

- 형식 확장은 가상 또는 추상 메서드를 지원 하지 않습니다.
- 형식 확장은 재정의 메서드를 확대으로 지원 하지 않습니다.
- 형식 확장은 정적으로 [확인 된 형식 매개 변수](./generics/statically-resolved-type-parameters.md)를 지원 하지 않습니다.
- 선택적 형식 확장은 확대로 생성자를 지원 하지 않습니다.
- 형식 [약어](type-abbreviations.md)에는 형식 확장을 정의할 수 없습니다.
- 형식 확장은에 `byref<'T>` 사용할 수 없습니다 (선언할 수 있지만).
- 형식 확장은 선언 될 수 있지만 특성에는 사용할 수 없습니다.
- 같은 이름의 다른 메서드를 오버 로드 하는 확장을 정의할 수 있지만 모호한 F# 호출이 있는 경우 컴파일러는 비 확장 메서드에 대 한 우선 순위를 부여 합니다.

마지막으로 한 형식에 대해 여러 개의 내장 형식 확장이 있는 경우 모든 멤버가 고유 해야 합니다. 선택적 형식 확장의 경우 동일한 형식에 대 한 다른 형식 확장의 멤버는 동일한 이름을 가질 수 있습니다. 모호성 오류는 클라이언트 코드가 동일한 멤버 이름을 정의 하는 두 개의 서로 다른 범위를 연 경우에만 발생 합니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [멤버](./members/index.md)
