---
title: 참조 셀
description: 참조 셀 F# 이 참조 의미 체계를 사용 하 여 변경 가능한 값을 만들 수 있는 저장소 위치인 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 2bca7797b272c0e7d5bf54df07041dc08e33709a
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216776"
---
# <a name="reference-cells"></a>참조 셀

*참조 셀* 은 참조 의미 체계를 사용 하 여 변경 가능한 값을 만들 수 있는 저장소 위치입니다.

## <a name="syntax"></a>구문

```fsharp
ref expression
```

## <a name="remarks"></a>설명

값 앞에 `ref` 연산자를 사용하여 값을 캡슐화하는 새 참조 셀을 만들 수 있습니다. 이는 변경 가능한 변수이므로 참조 셀을 만든 다음 내부 값을 변경할 수 있습니다.

참조 셀은 단순한 주소가 아니라 실제 값을 저장하는 위치입니다. `ref` 연산자를 사용하여 참조 셀을 만들면 캡슐화되고 변경 가능한 값으로 내부 값의 복사본이 만들어집니다.

`!`(느낌표) 연산자를 사용하여 참조 셀을 역참조할 수 있습니다.

다음 코드 예제에서는 참조 셀을 선언하고 사용하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2201.fs)]

출력은 `50`입니다.

참조 셀은 다음과 같이 선언되는 `Ref` 제네릭 레코드 형식의 인스턴스입니다.

```fsharp
type Ref<'a> =
{ mutable contents: 'a }
```

형식 `'a ref`는 `Ref<'a>`와 같은 의미입니다. IDE의 컴파일러와 IntelliSense에서는 이 형식을 전자와 같이 표시하지만 그 내부 정의는 후자와 같습니다.

`ref` 연산자는 새 참조 셀을 만드는 데 사용됩니다. 다음 코드는 `ref` 연산자의 선언입니다.

```fsharp
let ref x = { contents = x }
```

다음 표에는 참조 셀에 사용할 수 있는 기능이 나와 있습니다.

|연산자, 멤버 또는 필드|설명|형식|정의|
|--------------------------|-----------|----|----------|
|`!`(역참조 연산자)|내부 값을 반환합니다.|`'a ref -> 'a`|`let (!) r = r.contents`|
|`:=`(할당 연산자)|내부 값을 변경합니다.|`'a ref -> 'a -> unit`|`let (:=) r x = r.contents <- x`|
|`ref`(연산자)|값을 새 참조 셀로 캡슐화합니다.|`'a -> 'a ref`|`let ref x = { contents = x }`|
|`Value`속성|내부 값을 가져오거나 설정합니다.|`unit -> 'a`|`member x.Value = x.contents`|
|`contents`(레코드 필드)|내부 값을 가져오거나 설정합니다.|`'a`|`let ref x = { contents = x }`|

내부 값에 액세스하는 데는 여러 가지 방법이 있습니다. 역참조 연산자(`!`)를 통해 반환되는 값은 할당 가능한 값이 아닙니다. 따라서 내부 값을 수정하는 경우에는 할당 연산자(`:=`)를 대신 사용해야 합니다.

`Value` 속성과 `contents` 필드는 둘 다 할당 가능한 값입니다. 따라서 다음 코드에서와 같이 이들 속성과 필드를 사용하여 내부 값에 액세스하거나 내부 값을 변경할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2203.fs)]

출력은 다음과 같습니다.

```console
10
10
11
12
```

필드 `contents`는 다른 ML 버전과의 호환성을 위해 제공되며 컴파일 과정에서 이 필드로 인해 경고가 발생합니다. 경고가 발생하지 않도록 하려면 `--mlcompatibility` 컴파일러 옵션을 사용해야 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.

C#프로그래머는의에서 `ref` 와 C# `ref` 동일한 것이 아니라는 것을 F#알고 있어야 합니다. 에서 F# 동등한 구문은 [byref 배열과 같은](byrefs.md)입니다 .이는 참조 셀과는 다른 개념입니다.

로 `mutable`표시 된 값은 클로저로 캡처한 `'a ref` 경우 자동으로 승격 될 수 있습니다. [값](./values/index.md)을 참조 하십시오.

## <a name="see-also"></a>참고 항목

- [F# 언어 참조](index.md)
- [매개 변수 및 인수](parameters-and-arguments.md)
- [기호 및 연산자 참조](./symbol-and-operator-reference/index.md)
- [값](./values/index.md)
