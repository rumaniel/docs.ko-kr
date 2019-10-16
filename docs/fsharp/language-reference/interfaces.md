---
title: 인터페이스
description: 인터페이스가 다른 F# 클래스에서 구현 하는 관련 멤버의 집합을 지정 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 8f054a668ad0fbc2453a45883e8052471280eca3
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627654"
---
# <a name="interfaces"></a>인터페이스

*인터페이스* 는 다른 클래스에서 구현 하는 관련 멤버의 집합을 지정 합니다.

## <a name="syntax"></a>구문

```fsharp
// Interface declaration:
[ attributes ]
type [accessibility-modifier] interface-name =
    [ interface ]     [ inherit base-interface-name ...]
    abstract member1 : [ argument-types1 -> ] return-type1
    abstract member2 : [ argument-types2 -> ] return-type2
    ...
[ end ]

// Implementing, inside a class type definition:
interface interface-name with
    member self-identifier.member1argument-list = method-body1
    member self-identifier.member2argument-list = method-body2

// Implementing, by using an object expression:
[ attributes ]
let class-name (argument-list) =
    { new interface-name with
        member self-identifier.member1argument-list = method-body1
        member self-identifier.member2argument-list = method-body2
        [ base-interface-definitions ]
    }
    member-list
```

## <a name="remarks"></a>설명

인터페이스 선언은 멤버가 구현 되지 않는다는 점을 제외 하 고 클래스 선언과 비슷합니다. 대신 모든 멤버는 키워드 `abstract`에 의해 표시 된 대로 추상적입니다. 추상 메서드에는 메서드 본문을 제공 하지 않습니다. 그러나 `default` 키워드와 함께 멤버의 개별 정의를 메서드로 포함 하 여 기본 구현을 제공할 수도 있습니다. 이렇게 하려면 다른 .NET 언어의 기본 클래스에서 가상 메서드를 만드는 것과 동일 합니다. 이러한 가상 메서드는 인터페이스를 구현 하는 클래스에서 재정의할 수 있습니다.

인터페이스에 대 한 기본 액세스 `public`가능성은입니다.

필요에 따라 일반 F# 구문을 사용 하 여 각 메서드 매개 변수에 이름을 지정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet24032.fs)]

위의 `ISprintable` 예제 `string` 에서 메서드에는 이름이`format`인 형식의 단일 매개 변수가 있습니다. `Print`

인터페이스를 구현 하는 방법에는 개체 식 사용, 클래스 형식 사용 등 두 가지가 있습니다. 두 경우 모두 클래스 형식 또는 개체 식은 인터페이스의 추상 메서드에 대 한 메서드 본문을 제공 합니다. 구현은 인터페이스를 구현 하는 각 형식에만 적용 됩니다. 따라서 다른 형식에 대 한 인터페이스 메서드는 서로 다를 수 있습니다.

간단한 구문을 `interface` 사용 `end`하는 경우 정의의 시작과 끝을 표시 하는 및 키워드는 선택 사항입니다. 이러한 키워드를 사용 하지 않는 경우 컴파일러는 사용 하는 구문을 분석 하 여 형식이 클래스 인지 또는 인터페이스 인지를 유추 하려고 합니다. 멤버를 정의 하거나 다른 클래스 구문을 사용 하는 경우 형식은 클래스로 해석 됩니다.

.NET 코딩 스타일은 모든 인터페이스를 대문자로 `I`시작 하는 것입니다.

## <a name="implementing-interfaces-by-using-class-types"></a>클래스 형식을 사용 하 여 인터페이스 구현

다음 코드에 표시 된 것 처럼 `interface` 키워드, 인터페이스 이름 `with` 및 키워드를 사용 하 여 클래스 형식에서 하나 이상의 인터페이스를 구현 하 고 인터페이스 멤버 정의를 구현할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2801.fs)]

인터페이스 구현은 상속 되므로 파생 된 클래스는이를 다시 구현할 필요가 없습니다.

## <a name="calling-interface-methods"></a>인터페이스 메서드 호출

인터페이스 메서드는 인터페이스를 통해 인터페이스를 구현 하는 형식의 개체를 통해 호출할 수 없습니다. 따라서 이러한 메서드를 호출 하려면 `:>` 연산자 `upcast` 또는 연산자를 사용 하 여 인터페이스 형식으로 업 캐스트 할 수 있습니다.

형식의 `SomeClass`개체가 있을 때 인터페이스 메서드를 호출 하려면 다음 코드와 같이 개체를 인터페이스 형식에 업 캐스트 해야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2802.fs)]

다른 방법은 다음 예제와 같이 업캐스팅 하 고 인터페이스 메서드를 호출 하는 개체에 대 한 메서드를 선언 하는 것입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2803.fs)]

## <a name="implementing-interfaces-by-using-object-expressions"></a>개체 식을 사용 하 여 인터페이스 구현

개체 식은 인터페이스를 구현 하는 간단한 방법을 제공 합니다. 명명 된 형식을 만들 필요가 없고 인터페이스 메서드를 지 원하는 개체를 추가 메서드 없이 사용 하려는 경우에 유용 합니다. 다음 코드에서는 개체 식을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2804.fs)]

## <a name="interface-inheritance"></a>인터페이스 상속

인터페이스는 하나 이상의 기본 인터페이스에서 상속할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2805.fs)]

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [개체 식](object-expressions.md)
- [클래스](classes.md)
