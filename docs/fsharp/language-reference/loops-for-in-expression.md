---
title: '루프: for...in 식'
description: F# 자세한 내용은 다음을 참조 하세요. 식 반복 구문은 열거 가능한 컬렉션에서 패턴의 일치 항목을 반복 하는 데 사용 됩니다.
ms.date: 05/16/2016
ms.openlocfilehash: 5a2ca59ca4199ece5d78010ff780e86ae2b25181
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216451"
---
# <a name="loops-forin-expression"></a>루프: for...in 식

이 루핑 구문은 범위 식, 시퀀스, 목록, 배열 또는 열거를 지 원하는 기타 구문과 같은 열거 가능한 컬렉션에서 패턴의 일치를 반복 하는 데 사용 됩니다.

## <a name="syntax"></a>구문

```fsharp
for pattern in enumerable-expression do
    body-expression
```

## <a name="remarks"></a>설명

식은 열거 가능한 컬렉션의 값을 `for each` 반복 하는 데 사용 되기 때문에 다른 .net 언어의 문과 비교할 수 있습니다. `for...in` 그러나는 `for...in` 전체 컬렉션을 반복 하는 대신 컬렉션에 대 한 패턴 일치도 지원 합니다.

열거 가능한 식은 열거 가능한 컬렉션으로 지정 하거나 `..` 연산자를 사용 하 여 정수 계열 형식에 대 한 범위로 지정할 수 있습니다. 열거 가능한 컬렉션에는 목록, 시퀀스, 배열, 집합, 맵 등이 포함 됩니다. 을 구현 `System.Collections.IEnumerable` 하는 모든 형식을 사용할 수 있습니다.

`..` 연산자를 사용 하 여 범위를 표현할 때 다음 구문을 사용할 수 있습니다.

*시작* .. *finish*

다음 코드와 같이, *skip*이라는 증분을 포함 하는 버전을 사용할 수도 있습니다.

*시작* .. *skip* . *finish*

정수 범위와 단순 카운터 변수를 패턴으로 사용 하는 경우 일반적인 동작은 각 반복에서 카운터 변수를 1 씩 증가 하는 것 이지만, 범위에 skip 값이 포함 된 경우에는 카운터가 skip 값으로 증가 합니다.

패턴에서 일치 하는 값은 본문 식에도 사용할 수 있습니다.

다음 코드 예에서는 `for...in` 식을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5201.fs)]

출력은 다음과 같습니다.

```console
1
5
100
450
788
```

다음 예제에서는 시퀀스를 반복 하는 방법과 단순 변수 대신 튜플 패턴을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5202.fs)]

출력은 다음과 같습니다.

```console
1 squared is 1
2 squared is 4
3 squared is 9
4 squared is 16
5 squared is 25
6 squared is 36
7 squared is 49
8 squared is 64
9 squared is 81
10 squared is 100
```

다음 예제에서는 간단한 정수 범위에 대해 루프를 실행 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5203.fs)]

Function1의 출력은 다음과 같습니다.

```console
1 2 3 4 5 6 7 8 9 10
```

다음 예제에서는 범위의 다른 모든 요소를 포함 하는 2의 skip을 사용 하 여 범위를 반복 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5204.fs)]

의 `function2` 출력은 다음과 같습니다.

```console
1 3 5 7 9
```

다음 예제에서는 문자 범위를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5205.fs)]

의 `function3` 출력은 다음과 같습니다.

```console
a b c d e f g h i j k l m n o p q r s t u v w x y z
```

다음 예제에서는 역방향 반복에 음수 skip 값을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5208.fs)]

의 `function4` 출력은 다음과 같습니다.

```console
10 9 8 7 6 5 4 3 2 1 ... Lift off!
```

범위의 시작과 끝은 다음 코드와 같이 함수와 같은 식일 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5206.fs)]

이 입력에 `function5` 대 한 출력은 다음과 같습니다.

```console
2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18
```

다음 예제에서는 루프에 요소가 필요 하지 않은 경우 와일드\_카드 문자 ()를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5207.fs)]

출력은 다음과 같습니다.

```console
Number of elements in list1: 5
```

`Note`시퀀스 식과 `for...in` 기타 계산 식에를 사용할 수 있습니다 .이 경우 사용자 지정 된 버전 `for...in` 의 식이 사용 됩니다. 자세한 내용은 [시퀀스](sequences.md), [비동기 워크플로](asynchronous-workflows.md)및 [계산 식](computation-expressions.md)을 참조 하세요.

## <a name="see-also"></a>참고 항목

- [F# 언어 참조](index.md)
- [하며 `for...to`식](loops-for-to-expression.md)
- [하며 `while...do`식](loops-while-do-expression.md)
