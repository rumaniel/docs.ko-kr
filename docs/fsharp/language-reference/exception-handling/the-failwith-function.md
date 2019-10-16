---
title: 예외 failwith 함수
description: "' Failwith ' 함수에서 예외를 F# 생성 하는 방법에 대해 알아봅니다."
ms.date: 05/16/2016
ms.openlocfilehash: f2c86362d5bdde7bab55751f019965a5f4ca6236
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630331"
---
# <a name="exceptions-the-failwith-function"></a>예외 failwith 함수

함수 `failwith` 는 예외를 F# 생성 합니다.

## <a name="syntax"></a>구문

```fsharp
failwith error-message-string
```

## <a name="remarks"></a>설명

이전 구문의 *오류 메시지 문자열* 은 리터럴 문자열 또는 형식의 `string`값입니다. 예외의 `Message` 속성이 됩니다.

에 의해 `failwith` 생성 되는 예외는 코드 `System.Exception` 에서 `Failure` F# 이름을 가진 참조 인 예외입니다. 다음 코드에서는를 사용 `failwith` 하 여 예외를 throw 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6001.fs)]

## <a name="see-also"></a>참고자료

- [예외 처리](index.md)
- [예외 형식](exception-types.md)
- [예외: `try...with` 식입니다.](the-try-with-expression.md)
- [예외: `try...finally` 식입니다.](the-try-finally-expression.md)
- [예외: `raise` 함수](the-raise-function.md)
