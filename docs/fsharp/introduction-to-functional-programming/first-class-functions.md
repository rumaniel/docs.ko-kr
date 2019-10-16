---
title: 일급 함수
description: 에서 F#함수형 프로그래밍에 대 한 첫 번째 클래스 함수 및 중요 한 기능에 대해 알아봅니다.
ms.date: 10/29/2018
ms.openlocfilehash: 4681d32abd59cc4aade6f4cb2d062e7888bcfbbc
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68629719"
---
# <a name="first-class-functions"></a>일급 함수

함수형 프로그래밍 언어의 특성을 정의 하는 것은 함수를 첫 번째 클래스 상태로 승격 하는 것입니다. 다른 기본 제공 형식의 값으로 수행할 수 있는 함수를 사용 하 여이 작업을 수행할 수 있어야 하 고, 비슷한 노력으로이 작업을 수행할 수 있어야 합니다.

첫 번째 클래스 상태의 일반적인 측정값은 다음과 같습니다.

- 함수를 식별자에 바인딩할 수 있나요? 즉, 이름을 지정할 수 있나요?

- 함수를 데이터 구조 (예: 목록)에 저장할 수 있나요?

- 함수 호출에서 함수를 인수로 전달할 수 있나요?

- 함수 호출에서 함수를 반환할 수 있나요?

마지막 두 측정값은 *고차 작업* 또는 *고차 함수*라고 하는 항목을 정의 합니다. 고차 함수는 함수를 인수로 받아들이고 함수 호출 값으로 함수를 반환 합니다. 이러한 작업은 함수를 매핑하고 함수를 구성 하는 등의 함수형 프로그래밍 개체인 지원 합니다.

## <a name="give-the-value-a-name"></a>값에 이름을 지정 합니다.

함수가 첫 번째 클래스 값 이면 정수, 문자열 및 기타 기본 제공 형식의 이름을 지정할 때와 마찬가지로 이름을 지정할 수 있어야 합니다. 이는 함수 프로그래밍 자료에서 값에 식별자를 바인딩하는 것으로 간주 됩니다. F#[ `let` 바인딩을](../language-reference/functions/let-bindings.md) 사용 하 여 `let <identifier> = <value>`이름을 값에 바인딩합니다. 다음 코드에서는 두 가지 예를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet20.fs)]

함수 이름을 쉽게 지정할 수 있습니다. 다음 예제 `squareIt` 에서는 식별자 `squareIt` 를 [람다 식](../language-reference/functions/lambda-expressions-the-fun-keyword.md) `fun n -> n * n`에 바인딩하여 이라는 함수를 정의 합니다. 함수 `squareIt` 는 하나의 `n`매개 변수를 포함 하며 해당 매개 변수의 제곱을 반환 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet21.fs)]

F#에서는 입력이 적고 동일한 결과를 얻기 위해 다음과 같은 보다 간결한 구문을 제공 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet22.fs)]

다음에 나오는 예제에서는 대개 첫 번째 스타일 `let <function-name> = <lambda-expression>`을 사용 하 여 함수 선언과 다른 형식의 값 선언 간의 유사성을 강조 합니다. 그러나 모든 명명 된 함수를 간결한 구문으로 작성할 수도 있습니다. 일부 예제는 두 가지 방법으로 작성 됩니다.

## <a name="store-the-value-in-a-data-structure"></a>데이터 구조에 값 저장

데이터 구조에는 첫 번째 클래스 값을 저장할 수 있습니다. 다음 코드에서는 목록 및 튜플에 값을 저장 하는 예제를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet23.fs)]

튜플에 저장 된 함수 이름이 실제로 함수를 계산 하는지 확인 하기 위해 다음 예제에서는 `fst` 및 `snd` 연산자를 사용 하 여 튜플의 `funAndArgTuple`첫 번째와 두 번째 요소를 추출 합니다. 튜플의 첫 번째 요소는이 `squareIt` 고 두 번째 `num`요소는입니다. 식별자 `num` 는 이전 예제에서 `squareIt` 함수에 대 한 유효한 인수인 정수 10에 바인딩됩니다. 두 번째 식은 튜플의 첫 번째 요소를 튜플의 `squareIt num`두 번째 요소에 적용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet24.fs)]

마찬가지로 식별자 `num` 와 정수 10은 서로 바꿔 사용할 수 있으므로 식별자 `squareIt` 와 람다 식을 `fun n -> n * n`사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet25.fs)]

## <a name="pass-the-value-as-an-argument"></a>값을 인수로 전달 합니다.

값이 언어의 첫 번째 클래스 상태 이면 해당 값을 함수에 인수로 전달할 수 있습니다. 예를 들어 정수 및 문자열을 인수로 전달 하는 것이 일반적입니다. 다음 코드에서는에서 F#인수로 전달 되는 정수 및 문자열을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet26.fs)]

함수에 최고 수준의 상태가 있는 경우 동일한 방식으로 해당 함수를 인수로 전달할 수 있어야 합니다. 이는 고차 함수의 첫 번째 특징입니다.

다음 예제에서 함수 `applyIt` 에는 `op` 및 `arg`라는 두 개의 매개 변수가 있습니다. 에 대 `op` 한 매개 변수 하나를 포함 하는 함수 및에 `arg`함수에 대 한 적절 한 인수를 보내면 함수는에 `arg`적용 `op` 된 결과를 반환 합니다. 다음 예제에서 함수 인수와 정수 인수는 모두 해당 이름을 사용 하 여 동일한 방식으로 전송 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet27.fs)]

함수를 다른 함수에 인수로 보내는 기능은 맵 또는 필터 작업과 같은 함수형 프로그래밍 언어의 일반적인 추상화를 기반으로 합니다. 예를 들어, 맵 작업은 목록을 단계별로 실행 하는 함수에서 공유 하는 계산을 캡처하고 각 요소에 대 한 작업을 수행한 다음 결과 목록을 반환 하는 고차 함수입니다. 정수 목록의 각 요소를 증가 시키거나 각 요소를 제곱 하거나 문자열 목록의 각 요소를 대문자로 변경 하는 것이 좋습니다. 오류의 발생 가능성이 가장 많은 부분은 목록을 단계별로 안내 하 고 반환할 결과 목록을 작성 하는 재귀 프로세스입니다. 이 부분은 매핑 함수에서 캡처됩니다. 특정 응용 프로그램에 대 한 모든 쓰기는 각 목록 요소에 개별적으로 적용 하는 함수입니다 (대/소문자를 추가, 제곱, 변경). 이 함수는 이전 예제의로 `squareIt` `applyIt` 전송 되는 것과 마찬가지로 매핑 함수에 인수로 전송 됩니다.

F#[목록](../language-reference/lists.md), [배열](../language-reference/arrays.md)및 [시퀀스](../language-reference/sequences.md)를 비롯 한 대부분의 컬렉션 형식에 대 한 맵 메서드를 제공 합니다. 다음 예에서는 목록을 사용 합니다. 구문은 `List.map <the function> <the list>`입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet28.fs)]

자세한 내용은 [목록](../language-reference/lists.md)을 참조 하십시오.

## <a name="return-the-value-from-a-function-call"></a>함수 호출에서 값 반환

마지막으로 함수에 언어의 첫 번째 클래스 상태가 있는 경우 정수 및 문자열과 같은 다른 형식을 반환 하는 것 처럼 함수 호출의 값으로이를 반환할 수 있어야 합니다.

다음 함수는 반환 정수를 호출 하 고 표시 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet29.fs)]

다음 함수 호출은 문자열을 반환 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet30.fs)]

인라인으로 선언 된 다음 함수 호출은 부울 값을 반환 합니다. 표시 되는 값 `True`은입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet31.fs)]

함수 호출의 값으로 함수를 반환 하는 기능은 고차 함수의 두 번째 특징입니다. 다음 예제 `checkFor` 에서는 하나의 `item`인수를 사용 하 고 새 함수를 해당 값으로 반환 하는 함수로 정의 됩니다. 반환 된 함수는 목록을 인수로 `lst`사용 하 고 `item` 에서 `lst`을 검색 합니다. 이 있으면이 함수는를 반환 `true`합니다. `item` 가 없으면이 함수는를 반환 `false`합니다. `item` 이전 단원에서와 같이 다음 코드는 제공 된 목록 함수인 [list. exists](https://msdn.microsoft.com/library/15a3ebd5-98f0-44c0-8220-7dedec3e68a8)를 사용 하 여 목록을 검색 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet32.fs)]

다음 코드에서는를 `checkFor` 사용 하 여 하나의 인수를 사용 하 고 목록에서 7을 검색 하는 새 함수를 만듭니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet33.fs)]

다음 예제에서는의 함수에 F# 대 한 첫 번째 클래스 상태를 사용 하 여 두 `compose`함수 인수의 컴퍼지션을 반환 하는 함수를 선언 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet34.fs)]

> [!NOTE]
> 더 짧은 버전의 경우 "커리 된 함수" 섹션을 참조 하세요.

다음 코드에서는 두 개의 함수를에 `compose`인수로 보내고, 둘 다 동일한 형식의 단일 인수를 사용 합니다. 반환 값은 두 함수 인수의 컴퍼지션 인 새 함수입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet35.fs)]

> [!NOTE]
> F#는 함수를 구성 `<<` 하 `>>`는 및 라는 두 개의 연산자를 제공 합니다. 예 `let squareAndDouble2 = doubleIt << squareIt` 를 들어는 이전 예제 `let squareAndDouble = compose doubleIt squareIt` 에서와 동일 합니다.

함수 호출의 값으로 함수를 반환 하는 다음 예제에서는 간단한 추측 게임을 만듭니다. 게임을 만들려면 다른 사람이 추측 `makeGame` `target`하려는 값을 사용 하 여를 호출 합니다. 함수의 `makeGame` 반환 값은 한 인수 (추측)를 사용 하 여 guess가 정확한 지 여부를 보고 하는 함수입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet36.fs)]

다음 코드는를 `makeGame`호출 하 여에 `7` 대 `target`한 값을 보냅니다. 식별자 `playGame` 가 반환 된 람다 식에 바인딩되어 있습니다. 따라서는 하나의 인수를에 대 `guess`한 값으로 사용 하는 함수입니다. `playGame`

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet37.fs)]

## <a name="curried-functions"></a>커리 함수

이전 섹션의 많은 예제는 함수 선언에서 F# 암시적 *currying* 를 활용 하 여 더 간결 하 게 작성할 수 있습니다. Currying는 둘 이상의 매개 변수를 포함 하는 함수를 일련의 포함 된 함수로 변환 하는 프로세스입니다. 각 함수에는 단일 매개 변수가 있습니다. 에서 F#둘 이상의 매개 변수가 있는 함수는 기본적으로 커리 됩니다. 예를 들어 `compose` 이전 섹션에서는 다음의 간결한 스타일과 같이 세 개의 매개 변수를 사용 하 여 작성할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet38.fs)]

그러나 결과는에 `compose4curried`표시 된 것과 같이 한 매개 변수의 다른 함수를 반환 하는 하나의 매개 변수 함수를 반환 하는 하나의 매개 변수에 대 한 함수입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet39.fs)]

이 함수는 여러 가지 방법으로 액세스할 수 있습니다. 다음의 각 예에서는를 반환 하 고 18을 표시 합니다. 모든 예제에서 `compose4` 을 `compose4curried` 로 바꿀 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet40.fs)]

함수가 이전과 동일 하 게 작동 하는지 확인 하려면 원래 테스트 사례를 다시 시도 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet41.fs)]

> [!NOTE]
> 튜플에 매개 변수를 포함 하 여 currying를 제한할 수 있습니다. 자세한 내용은 [매개 변수 및 인수](../language-reference/parameters-and-arguments.md)에서 "매개 변수 패턴"을 참조 하세요.

다음 예제에서는 암시적 currying를 사용 하 여 더 짧은 버전 `makeGame`의를 작성 합니다. 함수를 `makeGame` `game` 생성 하 고 반환 하는 방법에 대 한 세부 정보는이 형식에서 더 명확 하지 않지만 원래 테스트 사례를 사용 하 여 결과가 동일한 지 확인할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet42.fs)]

Currying에 대 한 자세한 내용은 [함수](../language-reference/functions/index.md)에서 "인수 부분 적용"을 참조 하세요.

## <a name="identifier-and-function-definition-are-interchangeable"></a>식별자 및 함수 정의는 서로 바꿔 사용할 수 있습니다.

이전 예의 `num` 변수 이름은 정수 10으로 계산 되며 `num` ,가 유효한 경우 10도 유효 합니다. 함수 식별자와 해당 값의 경우에도 마찬가지입니다. 함수 이름을 사용할 수 있는 모든 위치에서는 바인딩되는 람다 식을 사용할 수 있습니다.

다음 예제에서는 라는 `Boolean` `isNegative`함수를 정의한 다음 함수 이름과 함수 정의를 서로 바꿔 사용 합니다. 다음 세 가지 예제는 모두를 반환 `False`하 고 표시 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet43.fs)]

한 단계 더 수행 하려면에 대해 `applyIt` `applyIt`바인딩되는 값을 대체 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet44.fs)]

## <a name="functions-are-first-class-values-in-f"></a>함수는 F의 First 클래스 값입니다.\#

이전 섹션의 예제에서는의 F# 함수가의 F#첫 번째 클래스 값에 대 한 조건을 충족 하는 것을 보여 줍니다.

- 식별자를 함수 정의에 바인딩할 수 있습니다.
[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet21.fs)]

- 데이터 구조에 함수를 저장할 수 있습니다.
[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet45.fs)]

- 함수를 인수로 전달할 수 있습니다.
[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet46.fs)]

- 함수를 함수 호출의 값으로 반환할 수 있습니다.
[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet32.fs)]

에 대 한 F#자세한 내용은 [ F# 언어 참조](../language-reference/index.md)를 참조 하세요.

## <a name="example"></a>예제

### <a name="description"></a>Description

다음 코드는이 항목의 모든 예제를 포함 합니다.

### <a name="code"></a>코드

[!code-fsharp[Main](~/samples/snippets/fsharp/contour/snippet47.fs)]

## <a name="see-also"></a>참고자료

- [목록](../language-reference/lists.md)
- [튜플](../language-reference/tuples.md)
- [함수](../language-reference/functions/index.md)
- [`let`바인딩하](../language-reference/functions/let-bindings.md)
- [람다 식: `fun` 키워드](../language-reference/functions/lambda-expressions-the-fun-keyword.md)
