---
title: 클래스의 let 바인딩
description: 클래스 정의에서 ' let ' 바인딩을 사용 하 여 F# 클래스의 전용 필드 및 전용 함수를 정의 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 1366ab8f1f4f606fe5947a8fc4df10de49346b3e
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216523"
---
# <a name="let-bindings-in-classes"></a>클래스의 let 바인딩

클래스 정의에서 바인딩을 사용 하 F# `let` 여 클래스에 대 한 전용 필드 및 전용 함수를 정의할 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
// Field.
[static] let [ mutable ] binding1 [ and ... binding-n ]

// Function.
[static] let [ rec ] binding1 [ and ... binding-n ]
```

## <a name="remarks"></a>설명

이전 구문은 클래스 머리글 및 상속 선언 뒤에, 그리고 멤버 정의 앞에 표시 됩니다. 구문은 클래스 외부 `let` 바인딩의 바인딩과 같지만 클래스에 정의 된 이름의 범위는 클래스로 제한 됩니다. `let` 바인딩은 전용 필드 또는 함수를 만듭니다. 데이터 또는 함수를 공개적으로 노출 하려면 속성 또는 멤버 메서드를 선언 합니다.

Static이 아닌 `let`바인딩은인스턴스 바인딩 이라고 합니다. `let` 인스턴스 `let` 바인딩은 개체가 생성 될 때 실행 됩니다. 정적 `let` 바인딩은 형식이 처음 사용 되기 전에 실행 되도록 보장 되는 클래스에 대 한 정적 이니셜라이저의 일부입니다.

인스턴스 `let` 바인딩 내의 코드는 기본 생성자의 매개 변수를 사용할 수 있습니다.

특성 및 액세스 가능성 한정자는 클래스의 `let` 바인딩에서 허용 되지 않습니다.

다음 코드 예제에서는 클래스의 여러 `let` 바인딩 형식을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3001.fs)]

출력은 다음과 같습니다.

```console
10 52 1 204
```

## <a name="alternative-ways-to-create-fields"></a>필드를 만드는 다른 방법

키워드를 `val` 사용 하 여 전용 필드를 만들 수도 있습니다. `val` 키워드를 사용 하는 경우 개체를 만들 때 필드에 값을 지정 하지 않고 대신 기본값을 사용 하 여 초기화 합니다. 자세한 내용은 [명시적 필드: Val 키워드](explicit-fields-the-val-keyword.md)입니다.

멤버 정의를 사용 하 고 키워드 `private` 를 정의에 추가 하 여 클래스에서 전용 필드를 정의할 수도 있습니다. 이는 코드를 다시 작성 하지 않고 멤버의 액세스 가능성을 변경 해야 하는 경우에 유용할 수 있습니다. 자세한 내용은 [액세스 제어](../access-control.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [멤버](index.md)
- [클래스의 `do` 바인딩](do-bindings-in-classes.md)
- [`let`바인딩하](../functions/let-bindings.md)
