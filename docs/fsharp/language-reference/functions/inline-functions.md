---
title: 인라인 함수
description: 호출 코드에 직접 F# 통합 된 인라인 함수를 사용 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 2830d1ada5b3005c3fcae975a44e85a7c84554f7
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630684"
---
# <a name="inline-functions"></a>인라인 함수

*인라인 함수* 는 호출 코드에 직접 통합 되는 함수입니다.

## <a name="using-inline-functions"></a>인라인 함수 사용

정적 형식 매개 변수를 사용 하는 경우 형식 매개 변수를 사용 하 여 매개 변수가 있는 모든 함수는 인라인이 되어야 합니다. 이렇게 하면 컴파일러가 이러한 형식 매개 변수를 확인할 수 있습니다. 일반 제네릭 형식 매개 변수를 사용 하는 경우에는 이러한 제한이 없습니다.

멤버 제약 조건을 사용 하도록 설정 하는 것 외에 인라인 함수는 코드를 최적화 하는 데 유용할 수 있습니다. 그러나 인라인 함수를 과도 하 게 사용할 경우 컴파일러 최적화 및 라이브러리 함수 구현에 대 한 변경 내용에 대 한 코드의 저항력이 떨어질 수 있습니다. 따라서 다른 모든 최적화 기술을 시도 하지 않는 한 최적화를 위해 인라인 함수를 사용 하지 않는 것이 좋습니다. 함수나 메서드를 인라인으로 만들면 성능이 향상 될 수 있지만 항상 그렇지는 않습니다. 따라서 지정 된 함수 인라인을 실제로 수행 하는 것이 긍정적인 효과를 갖고 있는지 확인 하기 위해 성능 측정을 사용 해야 합니다.

한정자 `inline` 는 최상위 수준, 모듈 수준 또는 클래스의 메서드 수준에서 함수에 적용 될 수 있습니다.

다음 코드 예제에서는 최상위 수준, 인라인 인스턴스 메서드 및 인라인 정적 메서드의 인라인 함수를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet201.fs)]

## <a name="inline-functions-and-type-inference"></a>인라인 함수 및 형식 유추

의 `inline` 존재는 형식 유추에 영향을 줍니다. 인라인 함수는 정적 형식 매개 변수를 사용할 수 있지만 인라인이 아닌 함수는 사용할 수 없기 때문입니다. 다음 코드 예제에서는 정적으로 확인 된 `inline` 형식 매개 변수 `float` 를 사용 하는 함수를 사용 하 여 변환 연산자를 사용 하기 때문에가 도움이 되는 경우를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet202.fs)]

한정자가 없는 경우 형식 유추는 함수에서 특정 형식을 사용 하도록 합니다 .이 경우 `int`에는입니다. `inline` 그러나 `inline` 한정자를 사용 하면 정적으로 확인 된 형식 매개 변수를 포함 하도록 함수도 유추 됩니다. `inline` 한정자를 사용 하 여 형식은 다음과 같이 유추 됩니다.

```fsharp
^a -> unit when ^a : (static member op_Explicit : ^a -> float)
```

즉, 함수는 **float**로의 변환을 지 원하는 모든 형식을 허용 합니다.

## <a name="see-also"></a>참고자료

- [함수](index.md)
- [제약 조건](../generics/constraints.md)
- [정적으로 확인된 형식 매개 변수](../generics/statically-resolved-type-parameters.md)
