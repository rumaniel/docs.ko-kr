---
title: 클래스의 do 바인딩
description: 개체가 생성 될 때 또는 F# 형식이 처음 사용 될 때 동작을 수행 하는 클래스 정의에서 ' do ' 바인딩을 사용 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: ced4f1bb17d9e23bf51cc79b5a275cc334cca013
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627582"
---
# <a name="do-bindings-in-classes"></a>클래스의 do 바인딩

클래스 정의의 `do` 바인딩은개체가생성될때동작을수행하고,형식을처음사용할때정적바인딩에대해`do` 를 수행 합니다.

## <a name="syntax"></a>구문

```fsharp
[static] do expression
```

## <a name="remarks"></a>설명

바인딩은 또는 이후에 `let` 바인딩과 함께 표시 되지만 클래스 정의의 멤버 정의 앞에 표시 됩니다. `do` 키워드는 `do` 모듈 수준에서 바인딩에 `do` 대해 선택 사항 이지만 클래스 정의의 `do` 바인딩에는 선택 사항이 아닙니다.

지정 된 형식의 모든 개체를 `do` 생성 하는 경우 비정적 바인딩과 비정적 `let` 바인딩은 클래스 정의에 표시 되는 순서 대로 실행 됩니다. 하나의 `do` 형식에서 여러 바인딩이 발생할 수 있습니다. 비정적 바인딩과 비정적 `do` 바인딩은 기본 생성자의 본문이 됩니다. `let` 비정적 `do` 바인딩 섹션의 코드는 기본 생성자 매개 변수와 `let` 바인딩 섹션에 정의 된 모든 값 또는 함수를 참조할 수 있습니다.

클래스가 클래스 제목의 `do` `as` 키워드에 의해 정의 된 자체 식별자를 포함 하는 동안에는 비정적 바인딩이 클래스의 멤버에 액세스할 수 있습니다 .이 경우 해당 멤버의 모든 사용은 클래스의 자체 식별자로 한정 됩니다.

바인딩이 `let` 클래스의 전용 필드를 초기화 하기 때문에 멤버가 `do` 정상적으로 작동 하도록 보장 하기 위해 일반적으로 바인딩이 바인딩 후 `let` 에 `do` 배치 되므로 바인딩의 코드를 사용할 수 있습니다. 완전히 초기화 된 개체를 사용 하 여를 실행 합니다. 초기화가 완료 되기 전에 코드에서 멤버를 사용 하려고 하면 InvalidOperationException이 발생 합니다.

정적 `do` 바인딩은 바깥쪽 클래스의 정적 멤버 또는 필드를 참조할 수 있지만 인스턴스 멤버나 필드는 참조할 수 없습니다. 정적 `do` 바인딩은 클래스에 대 한 정적 이니셜라이저의 일부가 되므로 클래스를 처음 사용 하기 전에 실행이 보장 됩니다.

특성은 형식의 바인딩에 `do` 대해 무시 됩니다. `do` 바인딩에서 실행 되는 코드에 특성이 필요한 경우 기본 생성자에 적용 되어야 합니다.

다음 코드에서 클래스에는 정적 `do` 바인딩과 `do` 비정적 바인딩이 있습니다. 개체에는 두 개의 매개 변수 `a` 및 `b`가 있고 클래스의 `let` 바인딩에 두 개의 전용 필드가 정의 되어 있는 생성자가 있습니다. 두 속성도 정의 됩니다. 이러한 모든 값을 출력 하는 줄에서 볼 수 `do` 있듯이 이러한 모든 값은 비정적 바인딩 섹션의 범위 내에 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3101.fs)]

출력은 다음과 같습니다.

```console
Initializing MyType.
Initializing object 1 2 2 4 8 16
```

## <a name="see-also"></a>참고자료

- [멤버](index.md)
- [클래스](../classes.md)
- [생성자](constructors.md)
- [클래스의 `let` 바인딩](let-bindings-in-classes.md)
- [`do`바인딩하](../functions/do-Bindings.md)
