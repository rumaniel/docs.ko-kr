---
title: '람다 식: 흥미로운 키워드'
description: F# ' 재미 ' 키워드를 사용 하 여 익명 함수인 람다 식을 정의 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 9818724686dd83a7e352fb36819289fa19b002df
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630670"
---
# <a name="lambda-expressions-the-fun-keyword-f"></a>람다 식: 흥미로운 키워드 (F#)

`fun` 키워드는 람다 식, 즉 익명 함수를 정의 하는 데 사용 됩니다.

## <a name="syntax"></a>구문

```fsharp
fun parameter-list -> expression
```

## <a name="remarks"></a>설명

*매개 변수 목록은* 일반적으로 이름 및 매개 변수의 형식으로 구성 됩니다. 일반적으로 *매개 변수 목록은* 모든 F# 패턴으로 구성 될 수 있습니다. 가능한 패턴의 전체 목록은 [패턴 일치](../pattern-matching.md)를 참조 하세요. 유효한 매개 변수 목록에는 다음 예제가 포함 됩니다.

```fsharp
// Lambda expressions with parameter lists.
fun a b c -> ...
fun (a: int) b c -> ...
fun (a : int) (b : string) (c:float) -> ...

// A lambda expression with a tuple pattern.
fun (a, b) -> …

// A lambda expression with a list pattern.
fun head :: tail -> …
```

*식은* 함수의 본문 이며,의 마지막 식은 반환 값을 생성 합니다. 유효한 람다 식의 예는 다음과 같습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet301.fs)]

## <a name="using-lambda-expressions"></a>람다 식 사용

람다 식은 목록 또는 다른 컬렉션에 대 한 작업을 수행 하 고 함수를 정의 하는 추가 작업을 방지 하려는 경우에 특히 유용 합니다. 많은 F# 라이브러리 함수는 함수 값을 인수로 사용 하 고, 이러한 경우에는 람다 식을 사용 하는 것이 특히 편리할 수 있습니다. 다음 코드는 목록 요소에 람다 식을 적용 합니다. 이 경우 익명 함수는 목록의 모든 요소에 1을 추가 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet302.fs)]

## <a name="see-also"></a>참고자료

- [함수](index.md)
