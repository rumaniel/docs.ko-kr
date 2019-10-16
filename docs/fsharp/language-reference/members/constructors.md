---
title: 생성자
description: 에서 F# 생성자를 정의 하 고 사용 하 여 클래스 및 구조체 개체를 만들고 초기화 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 6769ec7fc6768090d8ae68e21946a58829b6eea0
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736843"
---
# <a name="constructors"></a>생성자

이 문서에서는 생성자를 정의 하 고 사용 하 여 클래스 및 구조체 개체를 만들고 초기화 하는 방법을 설명 합니다.

## <a name="construction-of-class-objects"></a>클래스 개체 생성

클래스 형식의 개체에는 생성자가 있습니다. 생성자에는 두 가지 종류가 있습니다. 하나는 매개 변수가 형식 이름 바로 뒤에 괄호 안에 표시 되는 기본 생성자입니다. `new` 키워드를 사용 하 여 다른 선택적 추가 생성자를 지정 합니다. 이러한 추가 생성자는 기본 생성자를 호출 해야 합니다.

기본 생성자에는 `let` 클래스 `do` 정의의 시작 부분에 표시 되는 및 바인딩이 포함 되어 있습니다. 바인딩은 클래스의 전용 필드와 메서드를 선언 하 `do` 고, 바인딩은 코드를 실행 합니다. `let` 클래스 생성자의 바인딩에 `let` 대 한 자세한 내용은 [ `let` 클래스의 바인딩](let-bindings-in-classes.md)을 참조 하세요. 생성자의 바인딩에 대 `do` 한 자세한 내용은 [ `do` 클래스의 바인딩](do-bindings-in-classes.md)을 참조 하세요.

호출 하려는 생성자가 기본 생성자 인지 아니면 추가 생성자 인지에 관계 없이 `new` 식을 사용 하거나 선택적 `new` 키워드를 사용 하 여 개체를 만들 수 있습니다. 인수를 순서 대로 나열 하 고 쉼표로 구분한 다음 괄호로 묶거나 명명 된 인수 및 값을 괄호로 묶어 생성자 인수를 사용 하 여 개체를 초기화 합니다. 명명 된 생성자 인수를 사용 하는 것과 같이 속성 이름을 사용 하 고 값을 할당 하 여 개체를 생성 하는 동안 개체에 대 한 속성을 설정할 수도 있습니다.

다음 코드는 생성자를 포함 하는 클래스와 개체를 만드는 다양 한 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3501.fs)]

출력은 다음과 같습니다.

```console
Initialized object that has coordinates (1, 2, 3)
Initialized object that has coordinates (4, 5, 6)
Initialized object that has coordinates (7, 8, 9)
Initialized object that has coordinates (0, 0, 0)
```

## <a name="construction-of-structures"></a>구조 생성

구조체는 클래스의 모든 규칙을 따릅니다. 따라서 기본 생성자를 사용 하 고를 사용 `new`하 여 추가 생성자를 제공할 수 있습니다. 그러나 구조체와 클래스 사이에는 중요 한 차이점이 있습니다. 구조체에는 기본 생성자가 정의 되지 않은 경우에도 매개 변수가 없는 생성자 (인수 없이 하나)가 있을 수 있습니다. 매개 변수가 없는 생성자는 모든 필드를 해당 형식에 대 한 기본값 (일반적으로 0 또는 그에 해당 하는 값)으로 초기화 합니다. 구조체에 대해 정의 하는 모든 생성자에는 매개 변수가 없는 생성자와 충돌 하지 않도록 하나 이상의 인수가 있어야 합니다.

또한 구조체는 키워드를 `val` 사용 하 여 만든 필드를 포함 하는 경우가 많습니다. 클래스는 이러한 필드를 포함할 수도 있습니다. 다음 코드에 표시 된 것 처럼 키워드를 `val` 사용 하 여 정의 된 필드가 있는 구조체와 클래스는 레코드 식을 사용 하 여 추가 생성자에서 초기화 될 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3502.fs)]

자세한 내용은 [명시적 필드: `val` 키워드](explicit-fields-the-val-keyword.md)입니다.

## <a name="executing-side-effects-in-constructors"></a>생성자에서 의도 하지 않은 결과 실행

클래스의 기본 생성자는 `do` 바인딩에서 코드를 실행할 수 있습니다. 그러나 `do` 바인딩을 사용 하지 않고 추가 생성자에서 코드를 실행 해야 하는 경우는 어떻게 되나요? 이렇게 하려면 키워드를 `then` 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3503.fs)]

기본 생성자의 부작용은 계속 실행 됩니다. 따라서 출력은 다음과 같습니다.

```console
Created a person object.
Created a person object.
Created an invalid person object.
```

## <a name="self-identifiers-in-constructors"></a>생성자의 자체 식별자

다른 멤버의 경우에는 각 멤버의 정의에서 현재 개체의 이름을 제공 합니다. 생성자 매개 변수 바로 뒤에 키워드를 `as` 사용 하 여 클래스 정의의 첫 번째 줄에 자체 식별자를 넣을 수도 있습니다. 다음 예제에서는이 구문을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3504.fs)]

추가 생성자에서 생성자 매개 변수 바로 뒤에 `as` 절을 추가 하 여 자체 식별자를 정의할 수도 있습니다. 다음 예제에서는이 구문을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3505.fs)]

개체를 완전히 정의 하기 전에 사용 하려고 하면 문제가 발생할 수 있습니다. 따라서 자체 식별자를 사용 하면 컴파일러에서 경고를 내보내고 추가 검사를 삽입 하 여 개체를 초기화 하기 전에 개체의 멤버에 액세스할 수 없도록 할 수 있습니다. 기본 생성자의 `do` 바인딩이나 추가 생성자의 `then` 키워드 뒤에 있는 자체 식별자만 사용 해야 합니다.

자체 식별자의 이름은 일 `this`필요가 없습니다. 유효한 식별자 일 수 있습니다.

## <a name="assigning-values-to-properties-at-initialization"></a>초기화할 때 속성에 값 할당

생성자의 인수 목록에 폼 `property = value` 의 할당 목록을 추가 하 여 초기화 코드에서 클래스 개체의 속성에 값을 할당할 수 있습니다. 이는 다음 코드 예제에 나와 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

이전 코드의 다음 버전에서는 단일 생성자 호출에서 일반 인수, 선택적 인수 및 속성 설정의 조합을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3507.fs)]

## <a name="constructors-in-inherited-class"></a>상속 된 클래스의 생성자

생성자가 있는 기본 클래스에서 상속 하는 경우 상속 절에서 해당 인수를 지정 해야 합니다. 자세한 내용은 [생성자 및 상속](../inheritance.md#constructors-and-inheritance)을 참조 하세요.

## <a name="static-constructors-or-type-constructors"></a>정적 생성자 또는 형식 생성자

개체를 만들기 위한 코드를 지정 하는 것 `let` 외 `do` 에도 형식 수준에서 초기화를 수행 하기 위해 형식을 처음 사용 하기 전에 실행 되는 클래스 형식으로 정적 및 바인딩을 작성할 수 있습니다. 자세한 내용은 클래스의 [ `let` 바인딩](let-bindings-in-classes.md) 및 [ `do` 클래스의 바인딩](do-bindings-in-classes.md)을 참조 하세요.

## <a name="see-also"></a>참조

- [멤버](index.md)
