---
title: '명시적 필드: Val 키워드'
description: 형식을 초기화 하지 F# 않고 클래스 또는 구조체 형식에 값을 저장 하는 위치를 선언 하는 데 사용 되는 ' val ' 키워드에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 2703d9a2734cfda1614a401ec24c6630ec31b2f1
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736828"
---
# <a name="explicit-fields-the-val-keyword"></a>명시적 필드: Val 키워드

`val` 키워드는 클래스 또는 구조체 형식의 값을 초기화하지 않고 저장할 위치를 선언하는 데 사용됩니다. 이러한 방식으로 선언 된 저장소 위치를 *명시적 필드*라고 합니다. `val` 키워드는 `member` 키워드와 함께 자동으로 구현된 속성을 선언하는 데에도 사용됩니다. 자동으로 구현 된 속성에 대 한 자세한 내용은 [속성](properties.md)을 참조 하세요.

## <a name="syntax"></a>구문

```fsharp
val [ mutable ] [ access-modifier ] field-name : type-name
```

## <a name="remarks"></a>설명

클래스 또는 구조체 형식의 필드를 정의하는 일반적인 방법은 `let` 바인딩을 사용하는 것입니다. 그러나 `let` 바인딩은 반드시 클래스 생성자의 일부로 초기화해야 한다는 문제가 있습니다. 이와 같은 초기화는 경우에 따라 불가능하거나, 필요하지 않거나, 바람직하지 않을 수 있습니다. 초기화되지 않은 필드가 필요하면 `val` 키워드를 사용할 수 있습니다.

명시적 필드는 정적이거나 정적이지 않을 수 있습니다. *액세스 한정자* 는, `public` `private`또는 `internal`일 수 있습니다. 기본적으로 명시적 필드는 public입니다. 클래스의 `let` 바인딩은 항상 private이며 바로 이 점에서 차이가 있습니다.

[DefaultValue](https://msdn.microsoft.com/library/a3a3307b-8c05-441e-b109-245511614d58) 특성은 기본 생성자가 있는 클래스 형식의 명시적 필드에 필요 합니다. 이 특성은 필드가 0으로 초기화되도록 지정합니다. 필드의 형식은 0 초기화를 지원해야 합니다. 0 초기화를 지원하는 형식은 다음 중 하나에 해당하는 형식입니다.

- 0 값이 있는 기본 형식
- null 값을 정상 값, 비정상 값 또는 값의 표현으로 지원하는 형식. 여기에는 클래스, 튜플, 레코드, 함수, 인터페이스, .NET 참조 형식, `unit` 형식 및 구별된 공용 구조체 형식이 포함됩니다.
- .NET 값 형식
- 해당 필드가 모두 기본 0 값을 지원하는 구조체

예를 들어 변경 불가능한 `someField` 필드에는 이름이 `someField@`인 .NET 컴파일 표현의 지원 필드가 있으므로 `someField` 속성을 사용하여 저장된 값에 액세스합니다.

변경 가능한 필드의 경우 .NET 컴파일 표현은 .NET 필드입니다.

> [!WARNING]
> .NET Framework 네임 스페이스 `System.ComponentModel` 는 이름이 같은 특성을 포함 합니다. 이 특성에 대한 자세한 내용은 <xref:System.ComponentModel.DefaultValueAttribute>를 참조하세요.

다음 코드에서는 기본 생성자가 있는 클래스에 명시적 필드를 사용하는 방법을 보여 주고 이와 비교하기 위해 `let` 바인딩을 사용하는 방법도 보여 줍니다. `let` 바인딩된 필드 `myInt1`은 전용 필드입니다. `let` 바인딩된 필드 `myInt1`을 멤버 메서드에서 참조하는 경우 자체 식별자 `this`가 필요하지 않습니다. 그러나 명시적 필드 `myInt2`와 `myString`을 참조할 때는 자체 식별자가 필요합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6701.fs)]

출력은 다음과 같습니다.

```console
11 12 abc
30 def
```

다음 코드에서는 기본 생성자가 없는 클래스에 명시적 필드를 사용하는 방법을 보여 줍니다. 이 경우 `DefaultValue` 특성은 필요하지 않지만 형식에 대해 정의되는 생성자에서 모든 필드를 초기화해야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6702.fs)]

출력은 `35 22`입니다.

다음 코드에서는 구조체에 명시적 필드를 사용하는 방법을 보여 줍니다. 구조체는 값 형식 이므로 해당 필드의 값을 0으로 설정 하는 매개 변수가 없는 생성자가 자동으로 포함 됩니다. 따라서 `DefaultValue` 특성이 필요하지 않습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6703.fs)]

출력은 `11 xyz`입니다.

키워드 **를 사용**하지 않고 `mutable` `mutable` 필드를 사용 하 여 구조체를 초기화 하려는 경우 할당은 할당 후 즉시 삭제 되는 구조체의 복사본에 대해 작동 합니다. 따라서 구조가 변경 되지 않습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6704.fs)]

명시적 필드는 루틴에 사용하기 위한 것이 아닙니다. 일반적으로는 가능한 경우 항상 명시적 필드 대신 클래스의 `let` 바인딩을 사용해야 합니다. 명시적 필드는 네이티브 API에 대한 플랫폼 호출에 사용할 구조체를 정의해야 하는 경우 등과 같은 특정 상호 운용성 시나리오나 COM interop 시나리오에서 유용하게 사용됩니다. 자세한 내용은 [외부 함수](../functions/external-functions.md)를 참조 하세요. 명시적 필드가 필요할 수 있는 또 다른 상황으로는 기본 생성자가 없는 클래스를 만드는 F# 코드 생성기를 사용하여 작업해야 하는 경우를 들 수 있습니다. 명시적 필드는 스레드에 정적인 변수나 그와 유사한 구문에도 유용하게 사용됩니다. 자세한 내용은 `System.ThreadStaticAttribute`을 참조하세요.

`member val` 키워드가 형식 정의에 함께 표시되는 경우 이는 자동으로 구현된 속성의 정의입니다. 자세한 내용은 [속성](properties.md)에 정의된 인터페이스의 private C++ 관련 구현입니다.

## <a name="see-also"></a>참조

- [Properties](properties.md)
- [멤버](index.md)
- [클래스의 `let` 바인딩](let-bindings-in-classes.md)
