---
title: 개체 식
description: 사용 하는 방법을 알아봅니다 F# 명명 된 형식을 새 만들려면 개체 식 추가 코드와 오버 헤드를 방지 하려는 경우 필요 합니다.
ms.date: 02/08/2019
ms.openlocfilehash: 63f2c1d7128721b7b8c744e4cf02d73c2a8b4a07
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61666295"
---
# <a name="object-expressions"></a>개체 식

*식을 개체* 동적으로 생성 하는 익명 개체 형식의 새 인스턴스를 만드는 식입니다 되는 기존의 기본 형식, 인터페이스 또는 인터페이스의 집합 기반 합니다.

## <a name="syntax"></a>구문

```fsharp
// When typename is a class:
{ new typename [type-params]arguments with
    member-definitions
    [ additional-interface-definitions ]
}
// When typename is not a class:
{ new typename [generic-type-args] with
    member-definitions
    [ additional-interface-definitions ]
}
```

## <a name="remarks"></a>설명

위 구문에는 *typename* 은 기존 클래스 유형 또는 인터페이스 형식입니다. *형식-params* 선택적 제네릭 형식 매개 변수를 설명 합니다. 합니다 *인수* 생성자 매개 변수를 필요로 하는 클래스 형식에만 사용 됩니다. 합니다 *멤버 정의* 기본 클래스 또는 인터페이스에서 추상 메서드의 구현 또는 기본 클래스 메서드를 재정의 합니다.

다음 예제에서는 여러 다른 유형의 개체 식 보여 줍니다.

```fsharp
// This object expression specifies a System.Object but overrides the
// ToString method.
let obj1 = { new System.Object() with member x.ToString() = "F#" }
printfn "%A" obj1

// This object expression implements the IFormattable interface.
let delimiter(delim1: string, delim2: string, value: string) =
    { new System.IFormattable with
        member x.ToString(format: string, provider: System.IFormatProvider) =
            if format = "D" then
                delim1 + value + delim2
            else
                value }

let obj2 = delimiter("{","}", "Bananas!");

printfn "%A" (System.String.Format("{0:D}", obj2))

// Define two interfaces
type IFirst =
  abstract F : unit -> unit
  abstract G : unit -> unit

type ISecond =
  inherit IFirst
  abstract H : unit -> unit
  abstract J : unit -> unit

// This object expression implements both interfaces.
let implementer() =
    { new ISecond with
        member this.H() = ()
        member this.J() = ()
      interface IFirst with
        member this.F() = ()
        member this.G() = () }
```

## <a name="using-object-expressions"></a>개체 식 사용

추가 코드와 명명 된 형식을 새로 만드는 데 필요한는 오버 헤드를 방지 하려면 개체 식을 사용 합니다. 개체 식을 사용 하 여 프로그램에서 생성 하는 형식의 수를 최소화 하는 경우 코드 줄의 수를 줄일 수 있으며 형식의 불필요 한 확산을 방지할 수 있습니다. 다양 한 형식을 특정 상황을 처리할 수만 만드는 대신 기존 형식을 사용자 지정 하거나 특정 사례에 대 한 인터페이스의 적절 한 구현을 제공 하는 개체 식을 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
