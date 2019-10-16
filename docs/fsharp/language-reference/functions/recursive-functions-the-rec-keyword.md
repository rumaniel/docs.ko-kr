---
title: '재귀 함수: Rec 키워드'
description: "' Rec ' F# 키워드를 ' let ' 키워드와 함께 사용 하 여 재귀 함수를 정의 하는 방법을 알아봅니다."
ms.date: 05/16/2016
ms.openlocfilehash: 7edaa7206b2109c7b1a405624b9b2330968f9c52
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630658"
---
# <a name="recursive-functions-the-rec-keyword"></a>재귀 함수: Rec 키워드

키워드는 `let` 키워드와 함께 사용 되어 재귀 함수를 정의 합니다. `rec`

## <a name="syntax"></a>구문

```fsharp
// Recursive function:
let rec function-nameparameter-list =
function-body

// Mutually recursive functions:
let rec function1-nameparameter-list =
function1-body
and function2-nameparameter-list =
function2-body
...
```

## <a name="remarks"></a>설명

재귀 함수는 자신을 호출 하는 함수는 F# 언어에서 명시적으로 식별 됩니다. 이렇게 하면 함수 범위에서 정의 되는 식별자를 사용할 수 있습니다.

다음 코드에서는 *n*<sup>번째</sup> 피보나치 수를 계산 하는 재귀 함수를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet4001.fs)]

> [!NOTE]
> 실제로 위와 같은 코드는 이전에 계산 된 값의 다시 계산 기능을 포함 하기 때문에 메모리 및 프로세서 시간에 대 한 불필요 한 것입니다.

메서드는 형식 내에서 암시적으로 재귀적입니다. `rec` 키워드를 추가할 필요가 없습니다. 클래스 내의 바인딩이 암시적으로 재귀적이 지 않습니다.

## <a name="mutually-recursive-functions"></a>상호 재귀 함수

경우에 따라 함수는 서로 *재귀적*으로 사용 됩니다. 즉, 한 함수가 다른 함수를 호출 하는 원을 형성 합니다. 키워드`and` 를 사용 하 여 함께 연결 하려면 하나의 `let` 바인딩에서 이러한 함수를 함께 정의 해야 합니다.

다음 예에서는 두 개의 상호 재귀 함수를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet4002.fs)]

## <a name="see-also"></a>참고자료

- [함수](index.md)
