---
title: '예외: raise 함수'
description: F# ' Raise ' 함수를 사용 하 여 오류 또는 예외 조건이 발생 했음을 나타내는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: e0cc8da8310203c537b8081af8a225671bd8c6a3
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630295"
---
# <a name="exceptions-the-raise-function"></a>예외: raise 함수

`raise` 함수는 오류 또는 예외 조건이 발생 했음을 나타내는 데 사용 됩니다. 오류에 대 한 정보는 예외 개체에서 캡처됩니다.

## <a name="syntax"></a>구문

```fsharp
raise (expression)
```

## <a name="remarks"></a>설명

함수 `raise` 는 예외 개체를 생성 하 고 스택 해제 프로세스를 시작 합니다. 스택 해제 프로세스는 CLR (공용 언어 런타임)에 의해 관리 되므로이 프로세스의 동작은 다른 .NET 언어와 동일 합니다. 스택 해제 프로세스는 생성 된 예외와 일치 하는 예외 처리기를 검색 하는 것입니다. 검색은 현재 `try...with` 식 (있는 경우)에서 시작 됩니다. `with` 블록의 각 패턴은 순서 대로 확인 됩니다. 일치 하는 예외 처리기가 있으면 예외가 처리 된 것으로 간주 됩니다. 그렇지 않으면 스택이 해제 되 고 `with` 일치 하는 처리기가 발견 될 때까지 호출 체인의 블록이 검사 됩니다. 호출 `finally` 체인에서 발생 하는 모든 블록은 스택이 해제 될 때 순서 대로 실행 됩니다.

함수 `raise` 는 C# 또는 C++의 `throw` 에 해당 합니다. Catch `reraise` 처리기에서를 사용 하 여 호출 체인을 통해 동일한 예외를 전파 합니다.

다음 코드 예제에서는 `raise` 함수를 사용 하 여 예외를 생성 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5801.fs)]

다음 예제와 같이 함수를사용하여.net예외를발생시킬수도있습니다.`raise`

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5802.fs)]

## <a name="see-also"></a>참고자료

- [예외 처리](index.md)
- [예외 형식](exception-types.md)
- [예외: `try...with` 식입니다.](the-try-with-expression.md)
- [예외: `try...finally` 식입니다.](the-try-finally-expression.md)
- [예외: `failwith` 함수](the-failwith-function.md)
- [예외: `invalidArg` 함수](the-invalidArg-function.md)
