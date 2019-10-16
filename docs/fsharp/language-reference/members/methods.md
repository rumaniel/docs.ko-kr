---
title: 메서드
description: F# 메서드가 개체 및 형식의 기능과 동작을 노출 하 고 구현 하는 데 사용 되는 형식과 연결 된 함수인 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 13503690a59ace13dacba93b6fce9ea3240c5cc2
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627445"
---
# <a name="methods"></a>메서드

*메서드* 는 형식과 연결 된 함수입니다. 개체 지향 프로그래밍에서 메서드는 개체 및 형식의 기능과 동작을 노출 하 고 구현 하는 데 사용 됩니다.

## <a name="syntax"></a>구문

```fsharp
// Instance method definition.
[ attributes ]
member [inline] self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Static method definition.
[ attributes ]
static member [inline] method-name parameter-list [ : return-type ] =
    method-body

// Abstract method declaration or virtual dispatch slot.
[ attributes ]
abstract member method-name : type-signature

// Virtual method declaration and default implementation.
[ attributes ]
abstract member method-name : type-signature
[ attributes ]
default self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Override of inherited virtual method.
[ attributes ]
override self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Optional and DefaultParameterValue attributes on input parameters
[ attributes ]
[ modifier ] member [inline] self-identifier.method-name ([<Optional; DefaultParameterValue( default-value )>] input) [ : return-type ]
```

## <a name="remarks"></a>설명

이전 구문에서 다양 한 형식의 메서드 선언 및 정의를 볼 수 있습니다. 더 긴 메서드 본문에서 줄 바꿈이 등호 (=) 뒤에 오면 전체 메서드 본문이 들여쓰기 됩니다.

모든 메서드 선언에 특성을 적용할 수 있습니다. 메서드 정의의 구문 앞에는 일반적으로 별도의 줄에 나열 됩니다. 자세한 내용은 [특성](../attributes.md)을 참조하세요.

메서드를 표시할 `inline`수 있습니다. `inline`에 대한 내용은 [인라인 함수](../functions/inline-functions.md)를 참조하세요.

인라인이 아닌 메서드는 형식 내에서 재귀적으로 사용할 수 있습니다. 키워드를 `rec` 명시적으로 사용할 필요가 없습니다.

## <a name="instance-methods"></a>인스턴스 메서드

인스턴스 메서드는 `member` 키워드와 *자체 식별자*로 선언 된 다음 마침표 (.)와 메서드 이름 및 매개 변수를 사용 하 여 선언 됩니다. `let` 바인딩의 경우와 마찬가지로 *매개 변수 목록은* 패턴이 될 수 있습니다. 일반적으로 메서드 매개 변수를 다른 .NET Framework 언어로 만들 F# 때 메서드가 표시 되는 방식으로 튜플 형식으로 묶습니다. 그러나 커리 된 형식 (공백으로 구분 된 매개 변수)도 일반적 이며 다른 패턴도 지원 됩니다.

다음 예에서는 비추상 인스턴스 메서드의 정의와 사용을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3401.fs)]

인스턴스 메서드 내에서 let 바인딩을 사용 하 여 정의 된 필드에 액세스 하는 데 자체 식별자를 사용 하지 않습니다. 다른 멤버 및 속성에 액세스할 때 자체 식별자를 사용 합니다.

## <a name="static-methods"></a>정적 메서드

키워드 `static` 는 인스턴스를 사용 하지 않고 메서드를 호출 하 고 개체 인스턴스와 연결 하지 않도록 지정 하는 데 사용 됩니다. 그렇지 않으면 메서드는 인스턴스 메서드입니다.

다음 섹션의 예제에서는 키워드로 선언 된 필드 `let` , `member` 키워드로 선언 된 속성 멤버 및 `static` 키워드를 사용 하 여 선언 된 정적 메서드를 보여 줍니다.

다음 예제에서는 정적 메서드를 정의 하 고 사용 하는 방법을 보여 줍니다. 이러한 메서드 정의가 이전 섹션의 `SomeType` 클래스에 있다고 가정 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3402.fs)]

## <a name="abstract-and-virtual-methods"></a>추상 메서드 및 가상 메서드

키워드 `abstract` 는 메서드에 가상 디스패치 슬롯이 있고 클래스에 정의가 없을 수 있음을 나타냅니다. *가상 디스패치 슬롯* 은 런타임에 개체 지향 형식의 가상 함수 호출을 조회 하는 데 사용 되는 내부적으로 유지 관리 되는 함수 테이블의 항목입니다. 가상 디스패치 메커니즘은 개체 지향 프로그래밍의 중요 한 기능인 *다형성*을 구현 하는 메커니즘입니다. 정의가 없는 추상 메서드를 하나 이상 포함 하는 클래스는 *추상 클래스*입니다. 즉, 해당 클래스의 인스턴스를 만들 수 없습니다. 추상 클래스에 대 한 자세한 내용은 [추상 클래스](../abstract-classes.md)를 참조 하세요.

추상 메서드 선언에는 메서드 본문이 포함 되지 않습니다. 대신 메서드 이름 뒤에 콜론 (:) 및 메서드에 대 한 형식 시그니처입니다. 메서드의 형식 시그니처는 매개 변수 이름을 제외 하 고 Visual Studio Code 편집기에서 메서드 이름 위에 마우스 포인터를 놓으면 IntelliSense에서 표시 하는 것과 동일 합니다. 형식 시그니처는 대화형으로 작업할 때 인터프리터 fsi.exe에도 표시 됩니다. 메서드의 형식 시그니처는 매개 변수의 형식을 나열 하 고 그 뒤에 반환 형식이 오는 적절 한 구분 기호를 사용 하 여 구성 됩니다. 커리 된 매개 변수는 `->` 로 구분 되며 튜플 매개 변수 `*`는로 구분 됩니다. 반환 값은 항상 `->` 기호로 인수에서 구분 됩니다. 함수 형식이 매개 변수인 경우와 같이 괄호를 사용 하 여 복잡 한 매개 변수를 그룹화 하거나 튜플이 두 매개 변수가 아닌 단일 매개 변수로 처리 되는 경우를 나타낼 수 있습니다.

또한 클래스에 정의를 추가 하 고이 항목의 구문 블록과 같이 `default` 키워드를 사용 하 여 추상 메서드 기본 정의를 지정할 수 있습니다. 동일한 클래스에 정의가 있는 추상 메서드는 다른 .NET Framework 언어의 가상 메서드와 동일 합니다. 정의가 존재 하는지 여부에 관계 없이 키워드 `abstract` 는 클래스에 대 한 가상 함수 테이블에 새 디스패치 슬롯을 만듭니다.

기본 클래스에서 해당 추상 메서드를 구현 하는지 여부에 관계 없이 파생 클래스는 추상 메서드 구현을 제공할 수 있습니다. 파생 클래스에서 추상 메서드를 구현 하려면 `override` 또는 `default` 키워드를 사용 하는 경우를 제외 하 고 파생 클래스에서 이름과 시그니처가 동일한 메서드를 정의 하 고 메서드 본문을 제공 합니다. 키워드 `override` 와`default` 는 정확히 동일한 의미를 의미 합니다. 새 `override` 메서드가 기본 클래스 구현을 재정의 하는 경우를 사용 하 `default` 고, 원래 추상 선언과 동일한 클래스에서 구현을 만들 때를 사용 합니다. 기본 클래스에서 abstract `abstract` 로 선언 된 메서드를 구현 하는 메서드에는 키워드를 사용 하지 마십시오.

다음 예제에서는 .NET Framework 가상 메서드에 해당 `Rotate` 하는 기본 구현이 있는 추상 메서드를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3403.fs)]

다음 예제에서는 기본 클래스 메서드를 재정의 하는 파생 클래스를 보여 줍니다. 이 경우 재정의는 메서드가 아무 작업도 수행 하지 않도록 동작을 변경 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3404.fs)]

## <a name="overloaded-methods"></a>오버로드된 메서드

오버 로드 된 메서드는 지정 된 형식에서 이름이 같지만 인수가 다른 메서드입니다. 에서 F#선택적 인수는 오버 로드 된 메서드 대신 일반적으로 사용 됩니다. 그러나 인수가 커리 된 형식이 아닌 튜플 형식인 경우에는 오버 로드 된 메서드를 해당 언어로 사용할 수 있습니다.

## <a name="optional-arguments"></a>선택적 인수

F# 4.1부터 메서드에서 기본 매개 변수 값을 사용 하 여 선택적 인수를 사용할 수도 있습니다.  이는 코드와 C# 의 상호 운용성을 용이 하 게 하는 데 도움이 됩니다.  다음 예에서는 구문을 보여 줍니다.

```fsharp
// A class with a method M, which takes in an optional integer argument.
type C() =
    __.M([<Optional; DefaultParameterValue(12)>] i) = i + 1
```

에 `DefaultParameterValue` 전달 된 값은 입력 형식과 일치 해야 합니다.  위의 샘플 `int`에서이는입니다.  에 `DefaultParameterValue` 정수가 아닌 값을 전달 하려고 하면 컴파일 오류가 발생 합니다.

## <a name="example-properties-and-methods"></a>예제: 속성 및 메서드

다음 예제에는 필드, 전용 함수, 속성 및 정적 메서드의 예제가 있는 형식이 포함 되어 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3406.fs)]

## <a name="see-also"></a>참고자료

- [멤버](index.md)
