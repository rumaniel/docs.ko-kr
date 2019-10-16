---
title: 예외 형식
description: 예외 형식을 정의 하 고 사용 F# 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 8545fab50ff6338d1f1621710a838a200f9ac705
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630319"
---
# <a name="exception-types"></a>예외 형식

에 F#는 .net 예외 형식 및 F# 예외 형식 이라는 두 가지 범주의 예외가 있습니다. 이 항목에서는 예외 형식을 정의 하 고 F# 사용 하는 방법에 대해 설명 합니다.

## <a name="syntax"></a>구문

```fsharp
exception exception-type of argument-type
```

## <a name="remarks"></a>설명

이전 구문에서 *예외 형식은* 새 F# 예외 형식의 이름이 고, *인수 형식은* 이 형식의 예외를 발생 시킬 때 제공할 수 있는 인수의 형식을 나타냅니다. *인수 형식*에 튜플 형식을 사용 하 여 여러 인수를 지정할 수 있습니다.

F# 예외에 대 한 일반적인 정의는 다음과 유사 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5501.fs)]

다음과 같이 `raise` 함수를 사용 하 여이 형식의 예외를 생성할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5502.fs)]

다음 예제와 같이 F# `try...with` 식의 필터에서 직접 예외 형식을 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5503.fs)]

에서 `exception` F# 키워드를 사용 하 여 정의 하는 예외 형식은에서 `System.Exception`상속 되는 새 형식입니다.

## <a name="see-also"></a>참고자료

- [예외 처리](index.md)
- [예외: `raise` 함수](the-raise-function.md)
- [예외 계층](https://msdn.microsoft.com/library/z4c5tckx.aspx)
