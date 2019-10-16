---
title: F# 둘러보기
description: 이 자습서에서는 예제 코드를 사용하여 F# 프로그래밍 언어의 주요 기능을 살펴봅니다.
ms.date: 11/06/2018
ms.openlocfilehash: eba136da3cd829dcb2b0726dd4f1c24434aeba5b
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182618"
---
# <a name="tour-of-f"></a>F\# 둘러보기

F#에 대해 자세히 이해하려면 F# 코드를 읽고 작성하는 방법이 가장 좋습니다. 이 문서에서는 F# 언어의 주요 기능 중 일부를 둘러보고 컴퓨터에서 실행할 수 있는 코드 조각을 제공합니다. 개발 환경 설정에 대한 자세한 내용은 [시작하기](./tutorials/getting-started/index.md)를 참조하십시오.

F#에 함수(function)와 유형(type)이라는 두 가지 기본 개념이 있습니다.  둘러보기에서는 이 두 가지 개념에 해당하는 언어의 기능을 강조합니다.

## <a name="executing-the-code-online"></a>온라인에서 코드 실행

컴퓨터에가 설치 F# 되어 있지 않은 경우에는 [Weasembmba를 사용해 보세요 F# ](https://tryfsharp.fsbolero.io/). Fable은 F#과 유사하며 브라우저에서 직접 실행할 수 있습니다. REPL에서 다음에 나오는 예제를 보기 위해서는 Fable REPL의 왼쪽 메뉴 바에서 **Samples > Learn > Tour of F#** 를 확인하세요.

## <a name="functions-and-modules"></a>함수와 모듈

F# 프로그램의 가장 기본적인 부분은 ***모듈***로 구성된 ***함수***입니다.  [함수](./language-reference/functions/index.md)는 입력에 대한 작업으로 출력을 생성하고, F#에서 작업을 그룹화하는 기본 방식인 [모듈](./language-reference/modules.md)로 구성됩니다.  [`let` 바인딩](./language-reference/functions/let-bindings.md)을 사용하여 정의하며, 함수 이름을 지정하고 해당 인수를 정의할 수 있습니다.

[!code-fsharp[BasicFunctions](~/samples/snippets/fsharp/tour.fs#L101-L133)]

`let`바인딩은 다른 언어의 변수와 유사 하 게 값을 이름에 바인딩하는 방법 이기도 합니다.  `let`바인딩은 기본적으로 ***변경할*** 수 없습니다. 즉, 값 또는 함수를 이름에 바인딩한 후에는 내부에서 변경할 수 없습니다.  이는 ***변경할***수 있는 다른 언어의 변수와 대조적입니다. 즉, 특정 시점에 해당 값을 변경할 수 있습니다.  변경할 수 있는 바인딩이 필요한 경우 구문을 사용할 `let mutable ...` 수 있습니다.

[!code-fsharp[Immutability](~/samples/snippets/fsharp/tour.fs#L75-L94)]

## <a name="numbers-booleans-and-strings"></a>숫자, 부울 및 문자열

.NET 언어로, F# 지원 동일한 기본 [기본 형식](./language-reference/primitive-types.md) .NET에 존재 하는 합니다.

다양 한 숫자 형식은 F#의 표현 됩니다 다음과 같습니다.

[!code-fsharp[Numbers](~/samples/snippets/fsharp/tour.fs#L49-L68)]

부울 값과 기본 조건부 논리를 수행 하는 방법은 다음과 같습니다.

[!code-fsharp[Bools](~/samples/snippets/fsharp/tour.fs#L142-L152)]

그리고 다음과 같은 기본적인 [문자열](./language-reference/strings.md) 조작이 있습니다.

[!code-fsharp[Strings](~/samples/snippets/fsharp/tour.fs#L158-L180)]

## <a name="tuples"></a>튜플

[튜플](./language-reference/tuples.md) F#에서는 큰 문제가 됩니다.  값 자체로 처리 될 수 있는 명명 되지 않았지만 순서가 지정 된 값의 그룹입니다.  이러한 값을 다른 값에서 집계 된 값으로 간주 합니다.  함수에서 여러 값을 편리 하 게 반환 하거나 일부 임시 편의를 위해 값을 그룹화 하는 등의 여러 가지 용도로 사용 됩니다.

[!code-fsharp[Tuples](~/samples/snippets/fsharp/tour.fs#L186-L203)]

F# 4.1을 기준으로 만들 수도 있습니다 `struct` 튜플.  또한 `struct` 튜플 인 c # 7/Visual Basic 15 튜플로 완전히 상호 운용 됩니다.

[!code-fsharp[Tuples](~/samples/snippets/fsharp/tour.fs#L205-L218)]

튜플을 값 형식 이므로 `struct` 참조 튜플로 암시적으로 변환 하거나 그 반대로 변환할 수 없다는 점에 유의 해야 합니다.  참조와 구조체 튜플 사이에서 명시적으로 변환 해야 합니다.

## <a name="pipelines-and-composition"></a>파이프라인 및 컴퍼지션

와 같은 연산자를 파이프할 `|>` F#의 데이터를 처리 하는 경우 널리 사용 됩니다. 이러한 연산자는 함수에 대 한 "파이프라인"을 유연 하 게 설정할 수 있도록 하는 함수입니다. 다음 예제에서는 이러한 연산자를 활용 하 여 간단한 함수 파이프라인을 만드는 방법을 안내 합니다.

[!code-fsharp[Pipelines](~/samples/snippets/fsharp/tour.fs#L227-L282)]

앞의 예제 수 목록 처리 함수를 첫 번째 클래스 함수를 포함 하 여 F#의 많은 기능을 사용 하 고 [부분 응용 프로그램](./language-reference/functions/index.md#partial-application-of-arguments)합니다. 이러한 각 개념에 대 한 심층적인 이해는 다소 고급이 될 수 있지만 파이프라인을 빌드할 때 쉽게 함수를 사용 하 여 데이터를 처리할 수 있는지 명확 하 게 이해 해야 합니다.

## <a name="lists-arrays-and-sequences"></a>목록, 배열 및 시퀀스

목록, 배열 및 시퀀스는 F# 핵심 라이브러리의 세 가지 기본 컬렉션 형식입니다.

[목록은](./language-reference/lists.md) 동일한 형식의 요소에 대 한 순서가 지정 되지 않은 컬렉션입니다.  이러한 목록은 단일 항목 연결 목록입니다. 즉, 열거형을 위한 것 이며, 크기가 클 경우 임의 액세스 및 연결에 적합 하지 않습니다.  이는 일반적으로 단일 연결 목록을 사용 하 여 목록을 표시 하지 않는 다른 인기 언어의 목록과 대조 됩니다.

[!code-fsharp[Lists](~/samples/snippets/fsharp/tour.fs#L309-L359)]

[배열은](./language-reference/arrays.md) 동일한 형식의 요소에 대 한 고정 크기의 *변경* 가능한 컬렉션입니다.  요소의 빠른 임의 액세스를 지원 하며 F# 목록에서는 방금 연속 된 메모리 블록을 이기 때문에 보다 빠릅니다.

[!code-fsharp[Arrays](~/samples/snippets/fsharp/tour.fs#L368-L407)]

[시퀀스](./language-reference/sequences.md) 는 요소의 논리적 계열로, 모두 동일한 형식입니다.  이러한 형식은 목록 및 배열 보다 일반적인 형식으로, 논리적 요소 시리즈에 대 한 "뷰"가 될 수 있습니다.  ***지연***될 수도 있기 때문에이는 가능 합니다. 즉, 필요할 때만 요소를 계산할 수 있습니다.

[!code-fsharp[Sequences](~/samples/snippets/fsharp/tour.fs#L418-L452)]

## <a name="recursive-functions"></a>재귀 함수

컬렉션 또는 요소의 시퀀스로 처리는 사용 하 여 일반적으로 수행 됩니다 [재귀](./language-reference/functions/index.md#recursive-functions) F#에 있습니다.  F#에 루프 및 명령형 프로그래밍에 대 한 지원으로 재귀는 정확성을 보장 하기 위해 더 쉽기 때문에 기본 설정 합니다.

> [!NOTE]
> 다음 예에서는 `match` 식을 통해 패턴 일치를 사용 합니다.  이 기본 구문은이 문서의 뒷부분에 설명 되어 있습니다.

[!code-fsharp[RecursiveFunctions](~/samples/snippets/fsharp/tour.fs#L461-L500)]

F# 또한가 마무리 호출 최적화에 대 한 전체 지원 있습니다 빠른 루프 구문으로는 재귀 호출을 최적화할 수 있습니다.

## <a name="record-and-discriminated-union-types"></a>레코드 및 구분 된 공용 구조체 형식

레코드 및 공용 구조체 형식을 F# 코드에 사용 되는 두 가지 기본 데이터 형식이 되며 일반적으로 가장 좋은 방법은 F# 프로그램에서 데이터를 나타냅니다.  이렇게 하면 다른 언어의 클래스와 유사 하지만, 기본적인 차이점 중 하나는 구조적 같음 의미 체계가 있다는 것입니다.  즉, 이러한 값은 "기본적으로" 비교 가능 하며 같음은 매우 간단 합니다. 즉, 다른 것과 동일한 지 확인 합니다.

[레코드](./language-reference/records.md) 는 선택적 멤버 (예: 메서드)가 있는 명명 된 값의 집계입니다.  C# 또는 Java에 대해 잘 알고 있는 경우에는 구조적 같음 및 less 공식 절차을 사용 하는 pocos 또는 POJOs와 유사 하 게 사용할 수 있습니다.

[!code-fsharp[Records](~/samples/snippets/fsharp/tour.fs#L507-L559)]

F# 4.1을 기준으로 나타낼 수도 있습니다 레코드는 `struct`s입니다.  이 작업은 `[<Struct>]` 특성을 사용 하 여 수행 됩니다.

[!code-fsharp[Records](~/samples/snippets/fsharp/tour.fs#L561-L568)]

[구분 된 공용 구조체 (du)](./language-reference/discriminated-unions.md) 는 명명 된 형식이 나 사례의 수 일 수 있는 값입니다.  형식에 저장 된 데이터는 여러 개의 고유 값 중 하나일 수 있습니다.

[!code-fsharp[Unions](~/samples/snippets/fsharp/tour.fs#L575-L631)]

Du를 *단일 대/소문자 구분 된 공용 구조체*로 사용 하 여 기본 형식에 대 한 도메인 모델링에 도움이 될 수도 있습니다.  자주, 문자열 및 기타 기본 형식을 사용 하 여 무언가를 표시 하면 특정 의미가 제공 됩니다.  그러나 데이터의 기본 표시만 사용 하면 잘못 된 값이 잘못 할당 될 수 있습니다.  각 유형의 정보를 별개의 단일 사례 공용 구조체로 표현 하면이 시나리오에서 정확성을 적용할 수 있습니다.

[!code-fsharp[Unions](~/samples/snippets/fsharp/tour.fs#L633-L654)]

위의 샘플에서 보여 주는 것 처럼, 단일 대/소문자 구분 된 공용 구조체에서 내부 값을 가져오려면 명시적으로 래핑 해제 해야 합니다.

또한 Du는 재귀 정의를 지원 하 여 트리 및 본질적으로 재귀적 데이터를 쉽게 나타낼 수 있습니다.  예를 들어 및 `exists` `insert` 함수를 사용 하 여 이진 검색 트리를 나타낼 수 있는 방법은 다음과 같습니다.

[!code-fsharp[Unions](~/samples/snippets/fsharp/tour.fs#L656-L683)]

Du를 사용 하면 데이터 형식에서 트리의 재귀 구조를 나타낼 수 있으므로이 재귀적 구조에서 작업 하는 것은 간단 하며 정확성을 보장 합니다.  또한 아래와 같이 패턴 일치에서 지원 됩니다.

또한 `[<Struct>]` 특성을 사용 하 여 du `struct`를 s로 나타낼 수 있습니다.

[!code-fsharp[Unions](~/samples/snippets/fsharp/tour.fs#L685-L696)]

그러나이 작업을 수행할 때는 다음 두 가지 주요 사항을 염두에 두어야 합니다.

1. 구조체 DU는 재귀적으로 정의할 수 없습니다.
2. 구조체 DU는 각 사례에 대해 고유한 이름을 가져야 합니다.

위의 작업을 수행 하는 데 실패 하면 컴파일 오류가 발생 합니다.

## <a name="pattern-matching"></a>패턴 일치

[일치 패턴](./language-reference/pattern-matching.md) 기능은 F# 언어는 F# 형식에서 작동 하는 것에 대 한 정확성을 사용 하도록 설정 합니다.  위의 샘플에서 매우 약간의 `match x with ...` 구문을 발견 했습니다.  이 구문을 사용 하면 컴파일러가 데이터 형식의 "셰이프"를 이해할 수 있으므로 전체 패턴 일치를 통해 데이터 형식을 사용 하는 경우 가능한 모든 사례를 설명할 수 있습니다.  이는 정확성을 위해 매우 강력 하며, 일반적으로 컴파일 시간에 대 한 런타임 문제를 "리프트" 하는 데 사용 되는 영리 수 있습니다.

[!code-fsharp[PatternMatching](~/samples/snippets/fsharp/tour.fs#L705-L742)]

`_` 패턴을 사용 하는 것이 무엇 인지 알 수 있습니다.  이를 [와일드 카드 패턴](./language-reference/pattern-matching.md#wildcard-pattern)이라고 하며,이 패턴은 "무엇이 무엇 인지 걱정할 필요가 없습니다." 라는 방법입니다.  매우 편리 하지만를 사용 하 `_`는 데 익숙하지 않은 경우에는 실수로 완전 한 패턴 일치를 무시 하 고 컴파일 시간 사항을 더 이상 이점을 누릴 수 없습니다.  패턴 일치의 경우 분해 된 형식의 특정 부분을 고려 하지 않거나 패턴 일치 식에 모든 의미 있는 사례를 열거 한 경우에 가장 적합 합니다.

[활성 패턴](./language-reference/active-patterns.md) 은 패턴 일치에 사용할 수 있는 또 다른 강력한 구문입니다.  입력 데이터를 사용자 지정 형식으로 분할 하 여 패턴 일치 호출 사이트에서 분해 수 있습니다.  매개 변수화 될 수도 있으므로 파티션을 함수로 정의할 수 있습니다.  활성 패턴을 지원 하기 위해 이전 예제를 확장 하는 것은 다음과 같습니다.

[!code-fsharp[ActivePatterns](~/samples/snippets/fsharp/tour.fs#L764-L786)]

## <a name="optional-types"></a>선택적 형식

구별 된 공용 구조체 유형의 특수 경우는 옵션 종류를 F# 핵심 라이브러리의 일부는 매우 유용 합니다.

[옵션 형식은](./language-reference/options.md) 두 가지 사례 (값 또는 nothing) 중 하나를 나타내는 형식입니다.  특정 작업에서 값이 생성 될 수도 있고 그렇지 않을 수도 있는 모든 시나리오에서 사용 됩니다.  이렇게 하면 두 경우 모두를 고려 하 여 런타임 문제 보다는 컴파일 시간을 고려해 야 합니다.  이러한 기능은 종종 "없음"을 `null` 나타내는 데 사용 되는 api에서 사용 되므로 많은 상황 `NullReferenceException` 에서 걱정 하지 않아도 됩니다.

[!code-fsharp[Options](~/samples/snippets/fsharp/tour.fs#L789-L814)]

## <a name="units-of-measure"></a>측정 단위

F#의 형식 시스템의 고유한 특징 중 하나는 측정 단위를 통해 숫자 리터럴에 대 한 컨텍스트를 제공할 수 있습니다.

[측정 단위](./language-reference/units-of-measure.md) 를 사용 하 여 숫자 형식을 미터와 같은 단위에 연결 하 고 함수에서 숫자 리터럴이 아닌 단위에 대 한 작업을 수행할 수 있습니다.  이를 통해 컴파일러는 특정 컨텍스트에서 전달 된 숫자 리터럴의 형식이 적합 한지 확인할 수 있습니다. 따라서 해당 종류의 작업과 관련 된 런타임 오류가 제거 됩니다.

[!code-fsharp[UnitsOfMeasure](~/samples/snippets/fsharp/tour.fs#L817-L842)]

F# 핵심 라이브러리는 많은 SI 단위 유형 및 변환 단위를 정의합니다.  자세히 알아보려면 [Microsoft.FSharp.Data.UnitSystems.SI 네임 스페이스](https://msdn.microsoft.com/visualfsharpdocs/conceptual/microsoft.fsharp.data.unitsystems.si-namespace-%5bfsharp%5d)를 확인 하세요.

## <a name="classes-and-interfaces"></a>클래스 및 인터페이스

F#에.NET 클래스에 대 한 전체 지원을 [인터페이스](./language-reference/interfaces.md), [추상 클래스](./language-reference/abstract-classes.md)합니다 [상속](./language-reference/inheritance.md)등.

[클래스](./language-reference/classes.md) 는 속성, 메서드 및 이벤트를 [멤버로](./language-reference/members/index.md)가질 수 있는 .net 개체를 나타내는 형식입니다.

[!code-fsharp[Classes](~/samples/snippets/fsharp/tour.fs#L845-L880)]

제네릭 클래스를 정의 하는 것도 매우 간단 합니다.

[!code-fsharp[Classes](~/samples/snippets/fsharp/tour.fs#L883-L908)]

인터페이스를 구현 하려면 `interface ... with` 구문 또는 [개체 식을](./language-reference/object-expressions.md)사용할 수 있습니다.

[!code-fsharp[Classes](~/samples/snippets/fsharp/tour.fs#L911-L934)]

## <a name="which-types-to-use"></a>사용할 형식

클래스, 레코드, 구분 된 공용 구조체 및 튜플이 있으면 다음과 같은 중요 한 질문을 사용 해야 합니다.  대부분의 경우와 마찬가지로 대답은 사용자의 상황에 따라 달라 집니다.

튜플은 함수에서 여러 값을 반환 하 고 값의 임시 집계를 값 자체로 사용 하는 데 유용 합니다.

레코드는 튜플의 "프로시저 단위" 이며 명명 된 레이블과 선택적 멤버에 대 한 지원이 있습니다.  프로그램을 통해 전송 중인 데이터를 낮은 공식 절차 표현 하는 데 유용 합니다.  구조는 구조가 일치 하므로 비교와 함께 사용 하기 쉽습니다.

구별 된 공용 구조체는 많은 용도로 사용 되지만 핵심 혜택은 데이터에 포함 될 수 있는 모든 가능한 "셰이프"를 고려 하는 패턴 일치와 함께 사용할 수 있다는 것입니다.  

클래스는 정보를 표시 하 고 해당 정보를 기능에 연결 해야 하는 경우와 같이 다양 한 이유로 유용 합니다.  일반적으로 일부 데이터에 연결 된 기능을 사용 하는 경우 클래스 및 개체 지향 프로그래밍의 원리를 사용 하는 것이 큰 장점입니다.  이러한 언어는 거의 모든 항목에 대해 클래스를 C# 사용 하므로 클래스는 및 Visual Basic 상호 운용할 때 기본 데이터 형식 이기도 합니다.

## <a name="next-steps"></a>다음 단계

지금까지 살펴본 언어의 주요 기능 중 일부는 이제 첫 번째 F# 프로그램 작성을 준비 해야 합니다!  [시작](./tutorials/getting-started/index.md) 을 확인 하 여 개발 환경을 설정 하 고 일부 코드를 작성 하는 방법을 알아보세요.

자세한 정보를 얻기 위한 다음 단계는 원하는 대로 지정할 수 있지만 핵심 함수형 프로그래밍 개념에 익숙해지면 [의 F# 함수형 프로그래밍에 대해 소개](./introduction-to-functional-programming/index.md) 하는 것이 좋습니다.  이러한 강력한 프로그램 F# 빌드에 필수적인 됩니다.

또한 체크 아웃 합니다 [F# 언어 참조](./language-reference/index.md) F#에서 광범위 한 개념적 콘텐츠를 보려면.
