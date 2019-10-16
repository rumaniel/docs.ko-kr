---
title: let 바인딩
description: 식별자와 값 또는 함수 F# 를 연결 하는 ' let ' 바인딩을 사용 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 654631c7d1c48d8737e6098c98efee54cfdd91be
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630644"
---
# <a name="let-bindings"></a>let 바인딩

*바인딩은* 식별자를 값 또는 함수와 연결 합니다. `let` 키워드를 사용 하 여 값 또는 함수에 이름을 바인딩합니다.

## <a name="syntax"></a>구문

```fsharp
// Binding a value:
let identifier-or-pattern [: type] =expressionbody-expression
// Binding a function value:
let identifier parameter-list [: return-type ] =expressionbody-expression
```

## <a name="remarks"></a>설명

`let` 키워드는 하나 이상의 이름에 대 한 값 또는 함수 값을 정의 하는 바인딩 식에 사용 됩니다. 가장 간단한 형태의 `let` 식은 다음과 같이 이름을 단순 값에 바인딩합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1101.fs)]

새 줄을 사용 하 여 식별자에서 식을 구분 하는 경우 다음 코드와 같이 식의 각 줄을 들여씁니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1102.fs)]

이름 대신 이름을 포함 하는 패턴 (예: 다음 코드와 같이 튜플)을 지정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1103.fs)]

*본문 식은* 이름이 사용 되는 식입니다. Body 식이 해당 줄에 표시 되 고 `let` 키워드의 첫 번째 문자를 사용 하 여 정확히 줄 위로 들여쓰기 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1104.fs)]

`let` 바인딩은 모듈 수준, 클래스 형식 정의 또는 함수 정의에서와 같은 로컬 범위에서 나타날 수 있습니다. 모듈 `let` 의 최상위 수준 또는 클래스 형식에서 바인딩에는 본문 식이 필요 하지 않지만 다른 범위 수준에는 body 식이 필요 합니다. 다음 코드에 나와 있는 것 처럼 `let` 바인딩 이름은 정의 지점 후에 사용할 수 있지만 바인딩이 나타나기 전의 시점에는 사용할 수 없습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1105.fs)]

## <a name="function-bindings"></a>함수 바인딩

함수 바인딩은 함수 이름 및 매개 변수를 포함 하는 것을 제외 하 고 다음 코드에 표시 된 것과 같이 값 바인딩에 대 한 규칙을 따릅니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1106.fs)]

일반적으로 매개 변수는 튜플 패턴과 같은 패턴입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1107.fs)]

`let` 바인딩 식은 마지막 식의 값으로 계산 됩니다. 따라서 다음 코드 예제에서의 `result` 값은로 `300`계산 되는에서 `100 * function3 (1, 2)`계산 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1109.fs)]

자세한 내용은 [함수](index.md)를 참조하세요.

## <a name="type-annotations"></a>형식 주석

콜론 (:)을 포함 하 여 매개 변수의 형식을 지정할 수 있습니다. 다음에 형식 이름이 오고 모두 괄호로 묶여 있습니다. 마지막 매개 변수 뒤에 콜론과 형식을 추가 하 여 반환 값의 형식을 지정할 수도 있습니다. 정수를 매개 변수 형식 `function1`으로 사용 하는에 대 한 전체 형식 주석은 다음과 같습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1108.fs)]

명시적 형식 매개 변수가 없는 경우 형식 유추를 사용 하 여 함수 매개 변수의 형식을 결정 합니다. 여기에는 매개 변수의 형식을 제네릭으로 자동으로 일반화 하는 작업이 포함 될 수 있습니다.

자세한 내용은 [자동 일반화](../generics/automatic-generalization.md) 및 [형식 유추](../type-inference.md)를 참조 하세요.

## <a name="let-bindings-in-classes"></a>클래스의 let 바인딩

`let` 바인딩은 클래스 형식에 표시 될 수 있지만 구조체 또는 레코드 형식에는 표시 되지 않습니다. 클래스 형식에 let 바인딩을 사용 하려면 클래스에 기본 생성자가 있어야 합니다. 생성자 매개 변수는 클래스 정의의 형식 이름 뒤에 나와야 합니다. 클래스 형식의 `do` 바인딩은 해당 클래스 형식에 대 한 전용 필드 및 멤버를 정의 하 고, 형식의 바인딩과 함께 형식의 기본 생성자에 대 한 코드를 구성 합니다. `let` 다음 코드 예제에서는 전용 필드 `MyClass` `field1` 와 `field2`를 사용 하는 클래스를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1110.fs)]

`field1` 및`field2` 의 범위는 선언 된 형식으로 제한 됩니다. 자세한 내용은 클래스 [및](../classes.md) 클래스의 [`let`바인딩](../members/let-bindings-in-classes.md)을 참조하세요.

## <a name="type-parameters-in-let-bindings"></a>Let 바인딩의 형식 매개 변수

모듈 수준, 형식 또는 계산 식의 바인딩은명시적형식매개변수를가질수있습니다.`let` 함수 정의 내에서와 같이 식의 let 바인딩에는 형식 매개 변수를 사용할 수 없습니다. 자세한 내용은 [제네릭](../generics/index.md)을 참조하세요.

## <a name="attributes-on-let-bindings"></a>Let 바인딩의 특성

다음 코드와 같이 모듈의 최상위 `let` 바인딩에 특성을 적용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1111.fs)]

## <a name="scope-and-accessibility-of-let-bindings"></a>Let 바인딩의 범위 및 접근성

Let 바인딩을 사용 하 여 선언 된 엔터티의 범위는 바인딩이 표시 된 후 포함 하는 범위 (예: 함수, 모듈, 파일 또는 클래스)의 일부분으로 제한 됩니다. 따라서 let 바인딩에서 범위에 이름을 제공 하는 것으로 간주 될 수 있습니다. 모듈의 let 바인딩 값 또는 함수는 모듈의 public 함수로 컴파일되기 때문에 모듈의 클라이언트가 액세스할 수 있는 한 모듈의 클라이언트에서 액세스할 수 있습니다. 이와 대조적으로 클래스의 let 바인딩은 클래스 전용입니다.

일반적으로 모듈의 함수는 클라이언트 코드에서 사용 될 때 모듈의 이름으로 한정 되어야 합니다. 예를 들어 모듈 `Module1` 에 함수가 `function1`있는 경우 사용자는 함수를 참조 `Module1.function1` 하도록 지정 합니다.

모듈의 사용자는 가져오기 선언을 사용 하 여 모듈 이름으로 한정 되지 않고 해당 모듈 내의 함수를 사용할 수 있도록 만들 수 있습니다. 위에서 언급 한 예제에서 모듈의 사용자는이 경우에는 가져오기 선언을 `Module1` 사용 하 여 모듈을 열고, 그 이후에는를 `function1` 직접 참조 합니다.

```fsharp
module Module1 =
    let function1 x = x + 1.0

module Module2 =
    let function2 x =
        Module1.function1 x

open Module1

let function3 x =
    function1 x
```

일부 모듈에는 [RequireQualifiedAccess](https://msdn.microsoft.com/library/8b9b6ade-0471-4413-ac5d-638cd0de5f15)특성이 있습니다. 즉, 표시 되는 함수는 모듈 이름으로 한정 되어야 합니다. 예를 들어 F# 목록 모듈에는이 특성이 있습니다.

모듈 및 access control에 대 한 자세한 내용은 [모듈](../modules.md) 및 [Access Control](../access-control.md)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [함수](index.md)
- [클래스의 `let` 바인딩](../members/let-bindings-in-classes.md)
