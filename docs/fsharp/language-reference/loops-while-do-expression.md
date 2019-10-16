---
title: '루프: while...do 식'
description: 잠시 시간을 확인 하세요. do 식은 지정 된 테스트 조건이 true 인 동안 반복 실행 (반복)을 수행 하는 데 사용 됩니다.
ms.date: 05/16/2016
ms.openlocfilehash: 73526279358db101f8d07721a200920f1e87f119
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216626"
---
# <a name="loops-whiledo-expression"></a>루프: while...do 식

`while...do` 식은 지정 된 테스트 조건이 true 인 동안 반복 실행 (반복)을 수행 하는 데 사용 됩니다.

## <a name="syntax"></a>구문

```fsharp
while test-expression do
    body-expression
```

## <a name="remarks"></a>설명

*테스트 식이* 계산 됩니다. 이면 본문 식이 실행 되 고 테스트 식이 다시 계산 됩니다. `true` *본문 식* 에는 형식이 `unit`있어야 합니다. 테스트 식이 이면 반복이 `false`종료 됩니다.

다음 예에서는 `while...do` 식을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5301.fs)]

이전 코드의 출력은 1에서 20 사이의 난수 스트림으로, 마지막 값은 10입니다.

```console
13 19 8 18 16 2 10
Found a 10!
```

> [!NOTE]
> 시퀀스 식과 `while...do` 기타 계산 식에를 사용할 수 있습니다 .이 경우 사용자 지정 된 버전 `while...do` 의 식이 사용 됩니다. 자세한 내용은 [시퀀스](sequences.md), [비동기 워크플로](asynchronous-workflows.md)및 [계산 식](computation-expressions.md)을 참조 하세요.

## <a name="see-also"></a>참고 항목

- [F# 언어 참조](index.md)
- [하며 `for...in`식](loops-for-in-expression.md)
- [하며 `for...to`식](loops-for-to-expression.md)
