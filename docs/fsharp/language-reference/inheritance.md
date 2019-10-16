---
title: 상속
description: "' Inherit ' 키워드 F# 를 사용 하 여 상속 관계를 지정 하는 방법을 알아봅니다."
ms.date: 05/16/2016
ms.openlocfilehash: 5ab891a93528427a66e4eb8f7bfeccbf6e4d2c7e
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627658"
---
# <a name="inheritance"></a>상속

상속은 개체 지향 프로그래밍에서 "is-a" 관계 또는 구성은을 모델링 하는 데 사용 됩니다.

## <a name="specifying-inheritance-relationships"></a>상속 관계 지정

클래스 선언에서 키워드를 `inherit` 사용 하 여 상속 관계를 지정 합니다. 다음 예제에서는 기본 구문 형식을 보여 줍니다.

```fsharp
type MyDerived(...) =
    inherit MyBase(...)
```

클래스에는 직접 기본 클래스가 최대 하나만 있을 수 있습니다. `inherit` 키워드를 사용 하 여 기본 클래스를 지정 하지 않는 경우 클래스는에서 `System.Object`암시적으로 상속 됩니다.

## <a name="inherited-members"></a>상속 된 멤버

클래스가 다른 클래스에서 상속 하는 경우 파생 클래스의 메서드 및 멤버를 파생 클래스의 직접 멤버인 것 처럼 파생 클래스의 사용자가 사용할 수 있습니다.

모든 let 바인딩과 생성자 매개 변수는 클래스에 전용 이므로 파생 클래스에서 액세스할 수 없습니다.

키워드 `base` 는 파생 클래스에서 사용할 수 있으며 기본 클래스 인스턴스를 참조 합니다. 자체 식별자와 같이 사용 됩니다.

## <a name="virtual-methods-and-overrides"></a>가상 메서드 및 재정의

가상 메서드 (및 속성) F# 는 다른 .net 언어와 비교할 때 약간 다르게 작동 합니다. 새 가상 멤버를 선언 하려면 키워드를 `abstract` 사용 합니다. 해당 메서드에 대 한 기본 구현을 제공 하는지 여부에 관계 없이이 작업을 수행 합니다. 따라서 기본 클래스에서 가상 메서드의 전체 정의는 다음 패턴을 따릅니다.

```fsharp
abstract member [method-name] : [type]

default [self-identifier].[method-name] [argument-list] = [method-body]
```

파생 된 클래스에서이 가상 메서드의 재정의는 다음 패턴을 따릅니다.

```fsharp
override [self-identifier].[method-name] [argument-list] = [method-body]
```

기본 클래스에서 기본 구현을 생략 하면 기본 클래스는 추상 클래스가 됩니다.

다음 코드 예제에서는 기본 클래스의 새 가상 메서드 `function1` 선언과 파생 클래스에서 재정의 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2601.fs)]

## <a name="constructors-and-inheritance"></a>생성자 및 상속

기본 클래스에 대 한 생성자는 파생 클래스에서 호출 해야 합니다. 기본 클래스 생성자에 대 한 인수는 `inherit` 절의 인수 목록에 표시 됩니다. 사용 되는 값은 파생 클래스 생성자에 제공 된 인수에서 결정 되어야 합니다.

다음 코드에서는 파생 클래스가 상속 절의 기본 클래스 생성자를 호출 하는 기본 클래스와 파생 클래스를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2602.fs)]

여러 생성자의 경우 다음 코드를 사용할 수 있습니다. 파생 클래스 생성자의 첫 번째 줄은 `inherit` 절이 고, 필드는 `val` 키워드를 사용 하 여 선언 된 명시적 필드로 표시 됩니다. 자세한 내용은 [명시적 필드: `val` 키워드](./members/explicit-fields-the-val-keyword.md)입니다.

```fsharp
type BaseClass =
    val string1 : string
    new (str) = { string1 = str }
    new () = { string1 = "" }

type DerivedClass =
    inherit BaseClass

    val string2 : string
    new (str1, str2) = { inherit BaseClass(str1); string2 = str2 }
    new (str2) = { inherit BaseClass(); string2 = str2 }

let obj1 = DerivedClass("A", "B")
let obj2 = DerivedClass("A")
```

## <a name="alternatives-to-inheritance"></a>상속의 대안

형식을 약간만 수정 해야 하는 경우에는 개체 식을 상속 대신 사용 하는 것이 좋습니다. 다음 예에서는 새 파생 형식을 만드는 대신 개체 식을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2603.fs)]

개체 식에 대 한 자세한 내용은 [개체 식](object-expressions.md)을 참조 하세요.

개체 계층 구조를 만들 때 상속 대신 구별 된 공용 구조체를 사용 하는 것이 좋습니다. 또한 구별 된 공용 구조체는 일반적인 전체 형식을 공유 하는 여러 개체의 다양 한 동작을 모델링할 수 있습니다. 단일의 구별 된 공용 구조체는 서로 조금씩 변형 된 여러 파생 클래스의 필요성을 없앨 수 있습니다. 구별 된 공용 구조체에 대 한 자세한 내용은 [구별 된 공용 구조체](discriminated-unions.md)를 참조 하세요.

## <a name="see-also"></a>참고자료

- [개체 식](object-expressions.md)
- [F# 언어 참조](index.md)
