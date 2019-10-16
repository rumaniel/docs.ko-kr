---
title: 예외 try...finally 식
description: F# ' 시도 ... finally ' 식을 사용 하면 코드 블록에서 예외를 throw 하는 경우에도 정리 코드를 실행할 수 있습니다.
ms.date: 05/16/2016
ms.openlocfilehash: 0ddb64ac13b307404864ec5b54f26fd8a7a3d7d8
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083000"
---
# <a name="exceptions-the-tryfinally-expression"></a>예외 try...finally 식

식 `try...finally` 에서는 코드 블록에서 예외를 throw 하는 경우에도 정리 코드를 실행할 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
try
    expression1
finally
    expression2
```

## <a name="remarks"></a>설명

*Expression1를*실행 하는 동안 예외가 생성 되었는지 여부에 관계 없이 앞의 구문을 사용 하 여 식에서코드를실행할수`try...finally` 있습니다.

식 *2* 의 형식은 전체 식의 값에 영향을 주지 않습니다. 예외가 발생 하지 않는 경우 반환 되는 형식은 *expression1*의 마지막 값입니다. 예외가 발생 하면 값이 반환 되지 않고 제어 흐름이 호출 스택에 있는 다음 일치 하는 예외 처리기에 전송 됩니다. 예외 처리기를 찾을 수 없는 경우 프로그램이 종료 됩니다. 일치 하는 처리기의 코드가 실행 되거나 프로그램이 종료 되기 전에 `finally` 분기의 코드가 실행 됩니다.

다음 코드에서는 `try...finally` 식을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5701.fs)]

콘솔에 대 한 출력은 다음과 같습니다.

```console
Closing stream
Exception handled.
```

출력에서 볼 수 있듯이 외부 예외가 처리 되기 전에 스트림이 닫히고 파일 `test.txt` 에 텍스트가 `test1`포함 됩니다 .이는 예외가 전송 된 경우에도 버퍼가 플러시 되었고 디스크에 기록 되었음을 나타냅니다. 외부 예외 처리기에 대 한 제어입니다.

`try...with` 구문은 구문`try...finally` 에서 별도의 구문입니다. 따라서 코드에 `with` 블록과 `finally` 블록이 모두 필요한 경우 다음 코드 예제와 같이 두 구문을 중첩 해야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5702.fs)]

시퀀스 식과 비동기 워크플로를 포함 하는 계산 식의 컨텍스트에서 ...를 시도 합니다.  **finally** 식에는 사용자 지정 구현이 있을 수 있습니다. 자세한 내용은 [계산 식](../computation-expressions.md)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [예외 처리](index.md)
- [예외: `try...with` 식입니다.](the-try-with-expression.md)
