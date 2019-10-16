---
title: '루프: for...to 식'
description: F# 자세한 내용은 다음을 참조 하세요. to expression은 루프 변수의 값 범위에 대해 루프를 반복 하는 데 사용 됩니다.
ms.date: 05/16/2016
ms.openlocfilehash: 910c04aa4ea6b2c637dcad147347c1c317b5e0c0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68626618"
---
# <a name="loops-forto-expression"></a>루프: for...to 식

루프 변수의 값 범위에 대해 루프를 반복 하는 데 식이사용됩니다.`for...to`

## <a name="syntax"></a>구문

```fsharp
for identifier = start [ to | downto ] finish do
    body-expression
```

## <a name="remarks"></a>설명

식별자의 형식은 *start* 및 *finish* 식의 형식에서 유추 됩니다. 이러한 식의 형식은 32 비트 정수 여야 합니다.

기술적으로 `for...to` 는 식이 명령형 프로그래밍 언어의 일반적인 문과 유사 합니다. *본문 식* 의 반환 형식은 여야 `unit`합니다. 다음 예에서는 다양 한 `for...to` 식 사용을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5101.fs)]

위 코드는 다음과 같이 출력됩니다.

```
1 2 3 4 5 6 7 8 9 10
10 9 8 7 6 5 4 3 2 1
2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18
```

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [하며 `for...in`식](loops-for-in-expression.md)
- [하며 `while...do`식](loops-while-do-expression.md)
