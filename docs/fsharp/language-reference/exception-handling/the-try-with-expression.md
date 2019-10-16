---
title: 예외 try...with 식
description: F# ' 시도 ... '를 사용 하는 방법을 알아봅니다. 예외 처리를 위한 식 사용.
ms.date: 05/16/2016
ms.openlocfilehash: e4d615086a93e26b76cca460e797659ca13792b5
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630253"
---
# <a name="exceptions-the-trywith-expression"></a>예외 try...with 식

이 항목에서는 `try...with` F# 언어의 예외 처리에 사용 되는 식인 식에 대해 설명 합니다.

## <a name="syntax"></a>구문

```fsharp
try
    expression1
with
| pattern1 -> expression2
| pattern2 -> expression3
...
```

## <a name="remarks"></a>설명

식은에서 F#예외를 처리 하는 데 사용 됩니다. `try...with` 의 `try...catch` C#문과 비슷합니다. 위의 구문에서 *expression1* 의 코드는 예외를 생성할 수 있습니다. `try...with` 식은 값을 반환 합니다. 예외가 throw 되지 않으면 전체 식이 *expression1*의 값을 반환 합니다. 예외가 throw 되 면 각 *패턴* 은 예외와 함께 차례로 비교 되 고 첫 번째 일치 하는 패턴의 경우 해당 분기에 대 한 *예외 처리기*라고 하는 해당 *식이*실행 되 고 전체 식이 실행 됩니다. 해당 예외 처리기에서 식의 값을 반환 합니다. 일치 하는 패턴이 없는 경우 예외는 일치 하는 처리기가 발견 될 때까지 호출 스택을 전파 합니다. 예외 처리기의 각 식에서 반환 되는 값의 형식은 `try` 블록의 식에서 반환 된 형식과 일치 해야 합니다.

오류가 발생 하는 경우에도 일반적으로 각 예외 처리기의 식에서 반환 될 수 있는 유효한 값이 없음을 의미 합니다. 자주 패턴은 식의 형식을 옵션 형식으로 하는 것입니다. 다음 코드 예제에서는이 패턴을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5601.fs)]

예외는 .NET 예외 일 수도 있고 예외 일 F# 수도 있습니다. 키워드를 `exception` 사용 F# 하 여 예외를 정의할 수 있습니다.

다양 한 패턴을 사용 하 여 예외 형식 및 기타 조건에 대 한 필터링을 수행할 수 있습니다. 옵션은 다음 표에 요약 되어 있습니다.

|무늬|설명|
|-------|-----------|
|:? *exception-type*|지정 된 .NET 예외 형식과 일치 합니다.|
|:? *예외-* *식별자* 형식|지정 된 .NET 예외 형식과 일치 하지만 예외에 명명 된 값을 제공 합니다.|
|*예외-이름* (*인수*)|는 F# 예외 형식과 일치 하 고 인수를 바인딩합니다.|
|*identifier*|모든 예외를 일치 시키고 이름을 예외 개체에 바인딩합니다. 와 동일 **합니다.** _식별자_ 로 서의 예외|
|*조건* 에 대 한 *식별자*|조건이 true 이면 모든 예외와 일치 합니다.|

## <a name="examples"></a>예

다음 코드 예제에서는 다양 한 예외 처리기 패턴을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5602.fs)]

> [!NOTE]
> `try...with` 구문은 식`try...finally` 에서 분리 된 식입니다. 따라서 코드에 `with` 블록과 `finally` 블록이 모두 필요한 경우에는 두 식을 중첩 해야 합니다.

> [!NOTE]
> 비동기 워크플로 및 `try...with` 기타 계산 식에서를 사용할 수 있으며,이 경우 사용자 지정 된 버전 `try...with` 의 식이 사용 됩니다. 자세한 내용은 [비동기 워크플로](../asynchronous-workflows.md)및 [계산 식](../computation-expressions.md)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [예외 처리](index.md)
- [예외 형식](exception-types.md)
- [예외: `try...finally` 식입니다.](the-try-finally-expression.md)
