---
title: 기호 및 연산자 참조
description: 기호 및 연산자에 사용 되는 방법을 알아봅니다는 F# 프로그래밍 언어입니다.
ms.date: 02/11/2019
ms.openlocfilehash: 14ea7a66f7e9a79d24b62a4aa0564eecb891ee1a
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67306193"
---
# <a name="symbol-and-operator-reference"></a>기호 및 연산자 참조

> [!NOTE]
> 이 문서의 API 참조 링크를 통해 MSDN으로 이동됩니다.  docs.microsoft.com API 참조가 완전하지 않습니다.

이 항목에는 F# 언어에서 사용되는 기호와 연산자의 표가 나와 있습니다.

## <a name="table-of-symbols-and-operators"></a>기호 및 연산자 표

다음 표에서는 F# 언어에서 사용되는 기호에 대해 설명하고, 추가 정보를 제공하는 항목의 링크를 제공하며, 일부 기호 사용 방식을 간략하게 설명합니다. 기호는 ASCII 문자 집합 순서에 따라 정렬되어 있습니다.

|기호 또는 연산자|링크|설명|
|------------------|-----|-----------|
|`!`|[참조 셀](../reference-cells.md)<br /><br />[계산 식](../computation-expressions.md)|<ul><li>참조 셀을 역참조합니다.<br /></li><li>키워드 뒤에서 워크플로가 제어하는 키워드 동작의 수정된 버전을 나타냅니다.<br /></li></ul>|
|`!=`|해당 사항 없음.|<ul><li>F#에서 사용되지 않습니다. 다름 연산에서는 `<>`를 사용합니다.<br /></li></ul>|
|`"`|[리터럴](../literals.md)<br /><br />[문자열](../strings.md)|<ul><li>텍스트 문자열을 구분합니다.<br /></li></ul>|
|`"""`|[문자열](../strings.md)|축자 텍스트 문자열을 구분합니다. 문자열에서 작은따옴표를 사용하여 따옴표 문자를 나타낼 수 있다는 점에서 `@"..."`와는 다릅니다.|
|`#`|[컴파일러 지시문](../compiler-directives.md)<br /><br />[유연한 형식](../flexible-types.md)|<ul><li>전처리기 또는 컴파일러 지시문에 `#light` 등의 접두사를 추가합니다.<br /></li><li>형식에 사용하는 경우 형식 또는 해당 파생 형식 중 하나를 참조하는 *유연한 형식*을 나타냅니다.<br /></li></ul>|
|`$`|추가 정보가 제공되지 않습니다.|<ul><li>특정 컴파일러 생성 변수 및 함수 이름에 내부적으로 사용됩니다.<br /></li></ul>|
|`%`|[산술 연산자](arithmetic-operators.md)<br /><br />[코드 인용](../code-quotations.md)|<ul><li>정수 나머지를 계산합니다.<br /></li><li>형식화된 코드 인용에 식을 연결하는 데 사용됩니다.<br /></li></ul>|
|`%%`|[코드 인용](../code-quotations.md)|<ul><li>형식화되지 않은 코드 인용에 식을 연결하는 데 사용됩니다.<br /></li></ul>|
|`%?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이 면 정수 나머지를 계산 합니다.<br /></li></ul>|
|`&`|[일치 식](../match-expressions.md)|<ul><li>다른 언어와 상호 작용할 때 사용하기 위해 변경할 수 있는 값의 주소를 계산합니다.<br /></li><li>AND 패턴에 사용됩니다.<br /></li></ul>|
|`&&`|[부울 연산자](boolean-operators.md)|<ul><li>부울 AND 연산을 수행합니다.<br /></li></ul>|
|`&&&`|[비트 연산자](bitwise-operators.md)|<ul><li>비트 AND 연산을 계산합니다.<br /></li></ul>|
|`'`|[리터럴](../literals.md)<br /><br />[자동 일반화](../generics/automatic-generalization.md)|<ul><li>단일 문자 리터럴을 구분합니다.<br /></li><li>제네릭 형식 매개 변수를 나타냅니다.<br /></li></ul>|
|<code>&#96;&#96;...&#96;&#96;</code>|추가 정보가 제공되지 않습니다.|<ul><li>일반적으로는 유효한 식별자가 아닌 언어 키워드 등의 식별자를 구분합니다.<br /></li></ul>|
|`( )`|[단위 형식](../unit-type.md)|<ul><li>단위 형식의 단일 값을 나타냅니다.<br /></li></ul>|
|`(...)`|[튜플](../tuples.md)<br /><br />[연산자 오버로드](../operator-overloading.md)|<ul><li>식을 계산하는 순서를 나타냅니다.<br /></li><li>튜플을 구분합니다.<br /></li><li>연산자 정의에 사용됩니다.<br /></li></ul>|
|`(*...*)`||<ul><li>여러 줄로 표시될 수 있는 주석을 구분합니다.<br /></li></ul>|
|<code>(&#124;...&#124;)</code>|[활성 패턴](../active-patterns.md)|<ul><li>활성 패턴을 구분합니다. *바나나 클립*이라고도 합니다.<br /></li></ul>|
|`*`|[산술 연산자](arithmetic-operators.md)<br /><br />[튜플](../tuples.md)<br /><br />[측정 단위](../units-of-measure.md)|<ul><li>이항 연산자로 사용하는 경우 좌변과 우변을 곱합니다.<br /></li><li>형식의 경우 튜플의 쌍을 나타냅니다.<br /></li><li>측정 단위 형식에서 사용됩니다.<br /></li></ul>|
|`*?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 좌변과 우변을 곱합니다.<br /></li></ul>|
|`**`|[산술 연산자](arithmetic-operators.md)|<ul><li>지수 연산을 계산합니다. `x ** y`는 `x`의 `y`제곱을 나타냅니다.<br /></li></ul>|
|`+`|[산술 연산자](arithmetic-operators.md)|<ul><li>이항 연산자로 사용하는 경우 좌변과 우변을 더합니다.<br /></li><li>단항 연산자로 사용하는 경우에는 양의 수량을 나타냅니다. 공식적으로 이 항목은 부호가 변경되지 않은 동일 값을 생성합니다.<br /></li></ul>|
|`+?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 좌변과 우변을 더합니다.<br /></li></ul>|
|`,`|[튜플](../tuples.md)|<ul><li>튜플의 요소나 형식 매개 변수를 구분합니다.<br /></li></ul>|
|`-`|[산술 연산자](arithmetic-operators.md)|<ul><li>이항 연산자로 사용하는 경우 좌변에서 우변을 뺍니다.<br /></li><li>단항 연산자로 사용하는 경우 부정 연산을 수행합니다.<br /></li></ul>|
|`-?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 좌변에서 우변을 뺍니다.<br /></li></ul>|
|`->`|[함수](../functions/index.md)<br /><br />[일치 식](../match-expressions.md)|<ul><li>함수 형식에서는 인수와 반환 값을 구분합니다.<br /></li><li>시퀀스 식에서 식을 생성하며, `yield` 키워드와 동일합니다.<br /></li><li>일치 식에서 사용됩니다.<br /></li></ul>|
|`.`|[멤버](../members/index.md)<br /><br />[기본 형식](../primitive-types.md)|<ul><li>멤버에 액세스하고 개별 이름을 정규화된 이름으로 구분합니다.<br /></li><li>부동 소수점 수로 소수점을 지정합니다.<br /></li></ul>|
|`..`|[루프: `for...in` Expression](../loops-for-in-expression.md)|<ul><li>범위를 지정합니다.<br /></li></ul>|
|`.. ..`|[루프: `for...in` Expression](../loops-for-in-expression.md)|<ul><li>증분을 포함하여 범위를 지정합니다.<br /></li></ul>|
|`.[...]`|[배열](../arrays.md)|<ul><li>배열 요소에 액세스합니다.<br /></li></ul>|
|`/`|[산술 연산자](arithmetic-operators.md)<br /><br />[측정 단위](../units-of-measure.md)|<ul><li>좌변(분자)으로 우변(분모)을 나눕니다.<br /></li><li>측정 단위 형식에서 사용됩니다.<br /></li></ul>|
|`/?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 좌변으로 우변을 나눕니다.<br /></li></ul>|
|`//`||<ul><li>한 줄로 된 주석의 시작을 나타냅니다.<br /></li></ul>|
|`///`|[XML 문서](../xml-documentation.md)|<ul><li>XML 주석을 나타냅니다.<br /></li></ul>|
|`:`|[함수](../functions/index.md)|<ul><li>형식 주석에서 매개 변수 또는 멤버 이름을 해당 형식에서 분리합니다.<br /></li></ul>|
|`::`|[목록](../lists.md)<br /><br />[일치 식](../match-expressions.md)|<ul><li>목록을 만듭니다. 왼쪽의 요소가 오른쪽의 목록 앞에 추가됩니다.<br /></li><li>패턴 일치에서 목록의 파트를 구분하는 데 사용됩니다.<br /></li></ul>|
|`:=`|[참조 셀](../reference-cells.md)|<ul><li>참조 셀에 값을 할당합니다.<br /></li></ul>|
|`:>`|[캐스팅 및 변환](../casting-and-conversions.md)|<ul><li>특정 형식을 계층 구조의 상위 수준 형식으로 변환합니다.<br /></li></ul>|
|`:?`|[일치 식](../match-expressions.md)|<ul><li>반환 `true` 값 (하위 형식인 경우 포함); 지정 된 형식과 일치 하는 경우, 그렇지 `false` (형식 테스트 연산자).<br /></li></ul>|
|`:?>`|[캐스팅 및 변환](../casting-and-conversions.md)|<ul><li>특정 형식을 계층 구조의 하위 수준 형식으로 변환합니다.<br /></li></ul>|
|`;`|[자세한 구문](../verbose-syntax.md)<br /><br />[목록](../lists.md)<br /><br />[레코드](../records.md)|<ul><li>식을 구분합니다(대개 자세한 구문에서 사용됨).<br /></li><li>목록의 요소를 구분합니다.<br /></li><li>레코드의 필드를 구분합니다.<br /></li></ul>|
|`<`|[산술 연산자](arithmetic-operators.md)|<ul><li>작음 연산을 계산합니다.<br /></li></ul>|
|`<?`|[null 허용 연산자](nullable-operators.md)|우변이 nullable 형식이면 작음 연산을 계산합니다.|
|`<<`|[함수](../functions/index.md)|<ul><li>두 번째 함수가 먼저 실행되도록 두 함수를 역순으로 작성합니다(역방향 컴퍼지션 연산자).<br /></li></ul>|
|`<<<`|[비트 연산자](bitwise-operators.md)|<ul><li>좌변의 수량 비트를 우변에 지정된 비트 수만큼 좌변으로 시프트합니다.<br /></li></ul>|
|`<-`|[값](../values/index.md)|<ul><li>변수에 값을 할당합니다.<br /></li></ul>|
|`<...>`|[자동 일반화](../generics/automatic-generalization.md)|<ul><li>형식 매개 변수를 구분합니다.<br /></li></ul>|
|`<>`|[산술 연산자](arithmetic-operators.md)|<ul><li>좌변이 우변과 같지 않으면 `true`를 반환하고 같으면 false를 반환합니다.<br /></li></ul>|
|`<>?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 "같지 않음" 연산을 계산합니다.<br /></li></ul>|
|`<=`|[산술 연산자](arithmetic-operators.md)|<ul><li>좌변이 우변 이하이면 `true`를 반환하고 이상이면 `false`를 반환합니다.<br /></li></ul>|
|`<=?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 "작거나 같음" 연산을 계산합니다.<br /></li></ul>|
|<code>&lt;&#124;</code>|[함수](../functions/index.md)|<ul><li>우변의 식 결과를 좌변의 함수에 전달합니다(역방향 파이프 연산자).<br /></li></ul>|
|<code>&lt;&#124;&#124;</code>|[연산자&#40; &#60;&#124;&#124; &#41;&#60;'T1,'T2,'U&#62; 함수](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-%5bhh-%5d%5b%27t1%2c%27t2%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>우변의 두 인수 튜플을 좌변의 함수에 전달합니다.<br /></li></ul>|
|<code>&lt;&#124;&#124;&#124;</code>|[연산자&#40; &#60;&#124;&#124;&#124; &#41;&#60;'T1,'T2,'T3,'U&#62; 함수](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-%5bhhh-%5d%5b%27t1%2c%27t2%2c%27t3%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>우변의 세 인수 튜플을 좌변의 함수에 전달합니다.<br /></li></ul>|
|`<@...@>`|[코드 인용](../code-quotations.md)|<ul><li>형식화된 코드 인용을 구분합니다.<br /></li></ul>|
|`<@@...@@>`|[코드 인용](../code-quotations.md)|<ul><li>형식화되지 않은 코드 인용을 구분합니다.<br /></li></ul>|
|`=`|[산술 연산자](arithmetic-operators.md)|<ul><li>좌변이 우변과 같으면 `true`를 반환하고 같지 않으면 `false`를 반환합니다.<br /></li></ul>|
|`=?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 "같음" 연산을 계산합니다.<br /></li></ul>|
|`==`|해당 사항 없음.|<ul><li>F#에서 사용되지 않습니다. 같음 연산에는 `=`를 사용합니다.<br /></li></ul>|
|`>`|[산술 연산자](arithmetic-operators.md)|<ul><li>좌변이 우변보다 크면 `true`를 반환하고 작거나 같으면 `false`를 반환합니다.<br /></li></ul>|
|`>?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이 면 "보다 큼" 작업을 계산 합니다.<br /></li></ul>|
|`>>`|[함수](../functions/index.md)|<ul><li>두 함수를 작성합니다(정방향 컴퍼지션 연산자).<br /></li></ul>|
|`>>>`|[비트 연산자](bitwise-operators.md)|<ul><li>좌변의 수량 비트를 우변에 지정된 자릿수만큼 우변으로 시프트합니다.<br /></li></ul>|
|`>=`|[산술 연산자](arithmetic-operators.md)|<ul><li>반환 `true` 왼쪽 오른쪽; 보다 크거나 그렇지 않은 경우 반환 `false`합니다.<br /></li></ul>|
|`>=?`|[null 허용 연산자](nullable-operators.md)|<ul><li>우변이 nullable 형식이면 "크거나 같음" 연산을 계산합니다.<br /></li></ul>|
|`?`|[매개 변수 및 인수](../parameters-and-arguments.md)|<ul><li>선택적 인수를 지정합니다.<br /></li><li>동적 메서드 및 속성 호출을 위한 연산자로 사용됩니다. 고유한 구현을 제공해야 합니다.<br /></li></ul>|
|`? ... <- ...`|추가 정보가 제공되지 않습니다.|<ul><li>동적 속성 설정 위한 연산자로 사용됩니다. 고유한 구현을 제공해야 합니다.<br /></li></ul>|
|`?>=`, `?>`, `?<=`, `?<`, `?=`, `?<>`, `?+`, `?-`, `?*`, `?/`|[null 허용 연산자](nullable-operators.md)|<ul><li>? 접미사가 없는 해당 연산자와 같습니다. nullable 형식은 좌변입니다.<br /></li></ul>|
|`>=?`, `>?`, `<=?`, `<?`, `=?`, `<>?`, `+?`, `-?`, `*?`, `/?`|[null 허용 연산자](nullable-operators.md)|<ul><li>? 접미사가 없는 해당 연산자와 같습니다. nullable 형식은 우변입니다.<br /></li></ul>|
|`?>=?`, `?>?`, `?<=?`, `?<?`, `?=?`, `?<>?`, `?+?`, `?-?`, `?*?`, `?/?`|[null 허용 연산자](nullable-operators.md)|<ul><li>바깥쪽 물음표가 없는 해당 연산자와 동일합니다. 좌변과 우변이 모두 nullable 형식입니다.<br /></li></ul>|
|`@`|[목록](../lists.md)<br /><br />[문자열](../strings.md)|<ul><li>두 목록을 연결합니다.<br /></li><li>문자열 리터럴 앞에 배치하면 이스케이프 문자를 해석하지 않고 문자열을 축자로 해석함을 나타냅니다.<br /></li></ul>|
|`[...]`|[목록](../lists.md)|<ul><li>목록의 요소를 구분합니다.<br /></li></ul>|
|<code>[&#124;...&#124;]</code>|[배열](../arrays.md)|<ul><li>배열의 요소를 구분합니다.<br /></li></ul>|
|`[<...>]`|[특성](../attributes.md)|<ul><li>특성을 구분합니다.<br /></li></ul>|
|`\`|[문자열](../strings.md)|<ul><li>다음 문자를 이스케이프합니다. 문자 및 문자열 리터럴에 사용됩니다.<br /></li></ul>|
|`^`|[정적으로 확인된 형식 매개 변수](../generics/statically-resolved-type-parameters.md)<br /><br />[문자열](../strings.md)|<ul><li>런타임이 아닌 컴파일 타임에 확인해야 하는 형식 매개 변수를 지정합니다.<br /></li><li>문자열을 연결합니다.<br /></li></ul>|
|`^^^`|[비트 연산자](bitwise-operators.md)|<ul><li>배타적 비트 OR 연산을 계산합니다.<br /></li></ul>|
|`_`|[일치 식](../match-expressions.md)<br /><br />[제네릭](../generics/index.md)|<ul><li>와일드카드 패턴을 나타냅니다.<br /></li><li>익명 제네릭 매개 변수를 지정합니다.<br /></li></ul>|
|<code>&#96;</code>|[자동 일반화](../generics/automatic-generalization.md)|<ul><li>제네릭 형식 매개 변수를 나타내기 위해 내부적으로 사용됩니다.<br /></li></ul>|
|`{...}`|[시퀀스](../sequences.md)<br /><br />[레코드](../records.md)|<ul><li>시퀀스 식과 계산 식을 구분합니다.<br /></li><li>레코드 정의에 사용됩니다.<br /></li></ul>|
|<code>&#124;</code>|[일치 식](../match-expressions.md)|<ul><li>개별 일치 케이스, 구분된 개별 공용 구조체 케이스 및 열거형 값을 구분합니다.<br /></li></ul>|
|<code>&#124;&#124;</code>|[부울 연산자](boolean-operators.md)|<ul><li>부울 OR 연산을 계산합니다.<br /></li></ul>|
|<code>&#124;&#124;&#124;</code>|[비트 연산자](bitwise-operators.md)|<ul><li>비트 OR 연산을 계산합니다.<br /></li></ul>|
|<code>&#124;></code>|[함수](../functions/index.md)|<ul><li>좌변의 결과를 우변의 함수에 전달합니다(정방향 파이프 연산자).<br /></li></ul>|
|<code>&#124;&#124;></code>|[연산자&#40; &#124;&#124;&#62; &#41;&#60;'T1,'T2,'U&#62; 함수](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-hh%5d-%5d%5b%27t1%2c%27t2%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>좌변의 두 인수 튜플을 우변의 함수에 전달합니다.<br /></li></ul>|
|<code>&#124;&#124;&#124;></code>|[연산자&#40; &#124;&#124;&#124;&#62; &#41;&#60;'T1,'T2,'T3,'U&#62; 함수](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-hhh%5d-%5d%5b%27t1%2c%27t2%2c%27t3%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>좌변의 세 인수 튜플을 우변의 함수에 전달합니다.<br /></li></ul>|
|`~~`|[연산자 오버로드](../operator-overloading.md)|<ul><li>단항 부정 연산자에 대한 오버로드를 선언하는 데 사용됩니다.<br /></li></ul>|
|`~~~`|[비트 연산자](bitwise-operators.md)|<ul><li>비트 NOT 연산을 계산합니다.<br /></li></ul>|
|`~-`|[연산자 오버로드](../operator-overloading.md)|<ul><li>단항 빼기 연산자 오버로드를 선언하는 데 사용됩니다.<br /></li></ul>|
|`~+`|[연산자 오버로드](../operator-overloading.md)|<ul><li>단항 더하기 연산자에 대한 오버로드를 선언하는 데 사용됩니다.<br /></li></ul>|

## <a name="operator-precedence"></a>연산자 우선 순위

다음 표에는 F# 언어의 연산자 및 기타 식 키워드의 우선 순위 순서가 최저 우선 순위부터 최고 우선 순위 순서로 나와 있습니다. 또한 해당하는 경우에는 결합성도 표시되어 있습니다.

|연산자|결합성|
|--------|-------------|
|`as`|오른쪽|
|`when`|오른쪽|
|<code>&#124;</code> (파이프)|왼쪽|
|`;`|오른쪽|
|`let`|결합성 없음|
|`function`, `fun`, `match`, `try`|결합성 없음|
|`if`|결합성 없음|
|`not`|오른쪽|
|`->`|오른쪽|
|`:=`|오른쪽|
|`,`|결합성 없음|
|`or`, <code>&#124;&#124;</code>|왼쪽|
|`&`, `&&`|왼쪽|
|`:>`, `:?>`|오른쪽|
|`<`*op*, `>`*op*, `=`, <code>&#124;</code>*op*, `&`*op*, `&`<br /><br />(`<<<`, `>>>`, <code>&#124;&#124;&#124;</code>, `&&&` 포함)|왼쪽|
|`^`*연산자*<br /><br />(`^^^` 포함)|오른쪽|
|`::`|오른쪽|
|`:?`|결합성 없음|
|`-`*연산자*, `+`*연산자*|이러한 기호의 중위 사용에 적용됨|
|`*`*연산자*, `/`*연산자*, `%`*연산자*|왼쪽|
|`**`*연산자*|오른쪽|
|`f x`(함수 적용)|왼쪽|
|<code>&#124;</code> (패턴 일치)|오른쪽|
|전위 연산자(`+`*연산자*, `-`*연산자*, `%`, `%%`, `&`, `&&`, `!`*연산자*, `~`*연산자*)|왼쪽|
|`.`|왼쪽|
|`f(x)`|왼쪽|
|`f<`*형식*`>`|왼쪽|

F#에서는 사용자 지정 연산자 오버로드를 지원합니다. 즉, 고유한 연산자를 정의할 수 있습니다. 위의 표에서 *연산자*는 유효한 모든 연산자 문자 시퀀스(기본 제공 또는 사용자 정의)일 수 있으며 비어 있을 수도 있습니다. 따라서 이 표를 참조하여 원하는 수준의 우선 순위를 적용하기 위해 사용자 지정 연산자에 사용할 문자의 순서를 결정할 수 있습니다. 선행 `.` 문자는 컴파일러에서 우선 순위를 결정할 때 무시됩니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](../index.md)
- [연산자 오버로드](../operator-overloading.md)
