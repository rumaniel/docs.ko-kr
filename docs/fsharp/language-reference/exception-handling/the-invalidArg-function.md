---
title: 예외 invalidArg 함수
description: "' Invalidarg F# ' 함수에서 인수 예외를 생성 하는 방법에 대해 알아봅니다."
ms.date: 05/16/2016
ms.openlocfilehash: 6b1c5fdb5a541da336977d3a67d471302edb36b6
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083019"
---
# <a name="exceptions-the-invalidarg-function"></a>예외 invalidArg 함수

함수 `invalidArg` 는 인수 예외를 생성 합니다.

## <a name="syntax"></a>구문

```fsharp
invalidArg parameter-name error-message-string
```

## <a name="remarks"></a>설명

이전 구문에서 매개 변수 이름은 인수가 잘못 된 매개 변수의 이름을 가진 문자열입니다. *오류 메시지-문자열* 은 리터럴 문자열 또는 형식의 `string`값입니다. 예외 개체의 `Message` 속성이 됩니다.

에 의해 `invalidArg` `System.ArgumentException` 생성 된 예외는 예외입니다. 다음 코드에서는를 사용 `invalidArg` 하 여 예외를 throw 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6101.fs)]

출력은 다음과 같은 스택 추적 (표시 되지 않음)을 따릅니다.

```console
December
January
System.ArgumentException: Month parameter out of range.
```

## <a name="see-also"></a>참고자료

- [예외 처리](index.md)
- [예외 형식](exception-types.md)
- [예외: `try...with` 식입니다.](the-try-with-expression.md)
- [예외: `try...finally` 식입니다.](the-try-finally-expression.md)
- [예외: `raise` 함수](the-raise-function.md)
- [예외: `failwith` 함수](the-failwith-function.md)
