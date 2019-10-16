---
title: '조건식: if ... 그런 다음 ... 사람이'
description: 에서 F# 조건 식을 작성 하 여 다른 코드 분기를 실행 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: d9763f37cd9170c42e968282b54a3ce925e92591
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083028"
---
# <a name="conditional-expressions-ifthenelse"></a>조건식:`if...then...else`

`if...then...else` 식은 다른 코드 분기를 실행 하 고 지정 된 부울 식에 따라 다른 값으로 평가 됩니다.

## <a name="syntax"></a>구문

```fsharp
if boolean-expression then expression1 [ else expression2 ]
```

## <a name="remarks"></a>설명

이전 구문에서 *expression1* 는 부울 식이로 `true`계산 될 때 실행 되 고, 그렇지 않으면 *식* 1이 실행 됩니다.

다른 언어 `if...then...else` 와 달리 구문은 문이 아니라 식입니다. 즉,를 실행 하는 분기의 마지막 식 값인 값을 생성 합니다. 각 분기에서 생성 되는 값의 형식은 일치 해야 합니다. 명시적 `else` 분기가 없는 경우 해당 `unit`형식은입니다. 따라서 `then` 분기의 형식이가 아닌 `unit`다른 형식인 경우 반환 형식이 같은 `else` 분기가 있어야 합니다. 식을 함께 연결 하는 경우 대신 `else if`키워드 `elif` 를 사용할 수 있습니다. `if...then...else`

## <a name="example"></a>예제

다음 예에서는 `if...then...else` 식을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4501.fs)]

```console
10 is less than 20
What is your name? John
How old are you? 9
You are only 9 years old and already learning F#? Wow!
```

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
