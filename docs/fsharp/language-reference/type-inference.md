---
title: 형식 유추
description: F# 컴파일러가 값, 변수, 매개 변수 및 반환 값의 형식을 유추 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 4b18c1a67a8b7ddadb4fb334ea4736e9fd29feb0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630189"
---
# <a name="type-inference"></a>형식 유추

이 항목에서는 F# 컴파일러가 값, 변수, 매개 변수 및 반환 값의 형식을 유추 하는 방법에 대해 설명 합니다.

## <a name="type-inference-in-general"></a>일반 형식 유추

형식 유추의 개념은 컴파일러가 형식을 추론을 결론 내릴 수 없는 경우를 제외 하 F# 고 구문 형식을 지정할 필요가 없다는 것입니다. 명시적 형식 정보를 생략 하 F# 는 것은가 동적으로 형식화 된 언어 이거나의 F# 값이 약하게 형식화 된 것을 의미 하지 않습니다. F#는 정적으로 형식화 된 언어입니다. 즉, 컴파일러가 컴파일하는 동안 각 구문에 대해 정확한 형식을 추론 합니다. 컴파일러가 각 구문의 형식을 추론 하는 데 충분 한 정보가 없는 경우 일반적으로 코드의 임의 위치에 명시적 형식 주석을 추가 하 여 추가 형식 정보를 제공 해야 합니다.

## <a name="inference-of-parameter-and-return-types"></a>매개 변수 및 반환 형식 유추

매개 변수 목록에서 각 매개 변수의 형식을 지정 하지 않아도 됩니다. 및 F# 는 정적으로 형식화 된 언어 이므로 컴파일 시간에 모든 값과 식에는 정적 형식이 있습니다. 명시적으로 지정 하지 않은 형식에 대해 컴파일러는 컨텍스트를 기반으로 형식을 유추 합니다. 형식을 지정 하지 않으면 제네릭 형식으로 유추 됩니다. 코드에서 값을 일관 되지 않은 방식으로 사용 하는 경우 값의 모든 사용을 충족 하는 유추 된 단일 형식이 없는 경우 컴파일러에서 오류를 보고 합니다.

함수의 반환 형식은 함수에서 마지막 식의 형식에 따라 결정 됩니다.

예를 들어 다음 코드에서는 `a` 리터럴이 `100` 형식이 `int` `int`기 때문에 매개 `b` 변수 형식과 및 반환 형식이 모두로 유추 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet301.fs)]

리터럴을 변경 하 여 형식 유추에 영향을 줄 수 있습니다. `uint32` `b` `uint32` `a`접미사 `100` 를추가하여a를만들면,및`u`반환 값의 형식이로 유추 됩니다.

특정 형식만 사용 하는 함수 및 메서드와 같이 형식에 대 한 제한을 암시 하는 다른 구문을 사용 하 여 형식 유추에 영향을 줄 수도 있습니다.

또한 다음 예제와 같이 함수 또는 메서드 매개 변수나 식의 변수에 명시적 형식 주석을 적용할 수 있습니다. 서로 다른 제약 조건 간에 충돌이 발생 하면 오류가 발생 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet302.fs)]

모든 매개 변수 뒤에 형식 주석을 제공 하 여 함수의 반환 값을 명시적으로 지정할 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet303.fs)]

형식 주석이 매개 변수에 유용 하 게 사용 되는 일반적인 경우는 매개 변수가 개체 형식이 고 멤버를 사용 하려는 경우입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet304.fs)]

## <a name="automatic-generalization"></a>자동 일반화

함수 코드가 매개 변수의 형식에 종속 되지 않는 경우 컴파일러는 매개 변수를 제네릭인 것으로 간주 합니다. 이를 *자동 일반화*라고 하며, 복잡성을 늘리지 않고 제네릭 코드를 작성 하는 것이 강력 하 게 지원 될 수 있습니다.

예를 들어 다음 함수는 모든 형식의 두 매개 변수를 튜플로 결합 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet305.fs)]

형식은로 유추 됩니다.

```fsharp
'a -> 'b -> 'a * 'b
```

## <a name="additional-information"></a>추가 정보

형식 유추는 F# 언어 사양에 자세히 설명 되어 있습니다.

## <a name="see-also"></a>참고자료

- [자동 일반화](./generics/automatic-generalization.md)
