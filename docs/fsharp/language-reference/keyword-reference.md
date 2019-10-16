---
title: 키워드 참조
description: 모든 F# 언어 키워드에 대 한 정보 링크를 찾습니다.
ms.date: 05/16/2016
ms.openlocfilehash: 8c2df9d081caae48489e3e316ca158f3b9106efb
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70107033"
---
# <a name="keyword-reference"></a>키워드 참조

이 항목에서는 모든 F# 언어 키워드에 대 한 정보 링크를 제공 합니다.

## <a name="f-keyword-table"></a>F#키워드 테이블

다음 표에서는 모든 F# 키워드를 사전순으로 보여 주고 추가 정보를 포함 하는 관련 항목에 대 한 링크와 간략 한 설명을 함께 보여 줍니다.

|키워드|링크|Description|
|-------|----|-----------|
|`abstract`|[멤버](./members/index.md)<br /><br />[추상 클래스](abstract-classes.md)|선언 된 형식에 구현이 없거나 가상 이며 기본 구현을 포함 하는 메서드를 나타냅니다.|
|`and`|[`let`바인딩하](./functions/let-bindings.md)<br /><br />[레코드](records.md)<br /><br />[멤버](./members/index.md)<br /><br />[제약 조건](./generics/constraints.md)|상호 재귀 바인딩과 레코드, 속성 선언 및 제네릭 매개 변수에 대 한 여러 제약 조건에 사용 됩니다.|
|`as`|[클래스](classes.md)<br /><br />[패턴 일치](Pattern-Matching.md)|현재 클래스 개체에 개체 이름을 지정 하는 데 사용 됩니다. 패턴 일치 내에서 전체 패턴에 이름을 지정 하는 데도 사용 됩니다.|
|`assert`|[어설션](assertions.md)|디버깅 하는 동안 코드를 확인 하는 데 사용 됩니다.|
|`base`|[클래스](classes.md)<br /><br />[상속](inheritance.md)|기본 클래스 개체의 이름으로 사용 됩니다.|
|`begin`|[자세한 구문](verbose-syntax.md)|자세한 구문에서 코드 블록의 시작을 나타냅니다.|
|`class`|[클래스](classes.md)|자세한 구문에서 클래스 정의의 시작을 나타냅니다.|
|`default`|[멤버](./members/index.md)|추상 메서드의 구현을 나타냅니다. 추상 메서드 선언과 함께 사용 되어 가상 메서드를 만듭니다.|
|`delegate`|[대리자](delegates.md)|대리자를 선언 하는 데 사용 됩니다.|
|`do`|[do 바인딩](./functions/do-bindings.md)<br /><br />[하며 `for...to`식](loops-for-to-expression.md)<br /><br />[하며 `for...in`식](loops-for-in-expression.md)<br /><br />[하며 `while...do`식](loops-while-do-expression.md)|루프 구문에서 또는 명령적 코드를 실행 하는 데 사용 됩니다.|
|`done`|[자세한 구문](verbose-syntax.md)|자세한 구문에서 루프 식의 코드 블록 끝을 나타냅니다.|
|`downcast`|[캐스팅 및 변환](casting-and-conversions.md)|상속 체인에서 더 낮은 형식으로 변환 하는 데 사용 됩니다.|
|`downto`|[하며 `for...to`식](loops-for-to-expression.md)|`for` 식에서 역방향으로 계산 하는 데 사용 됩니다.|
|`elif`|[조건식: `if...then...else`](conditional-expressions-if-then-else.md)|조건부 분기에 사용 됩니다. 의 `else if`약식입니다.|
|`else`|[조건식: `if...then...else`](conditional-expressions-if-then-else.md)|조건부 분기에 사용 됩니다.|
|`end`|[구조체](structures.md)<br /><br />[구별된 공용 구조체](discriminated-unions.md)<br /><br />[레코드](records.md)<br /><br />[형식 확장명](type-extensions.md)<br /><br />[자세한 구문](verbose-syntax.md)|형식 정의 및 형식 확장에서 멤버 정의 섹션의 끝을 나타냅니다.<br /><br />자세한 구문에서 `begin` 키워드로 시작 하는 코드 블록의 끝을 지정 하는 데 사용 됩니다.|
|`exception`|[예외 처리](./exception-handling/index.md)<br /><br />[예외 형식](./exception-handling/exception-types.md)|예외 형식을 선언 하는 데 사용 됩니다.|
|`extern`|[외부 함수](./functions/external-functions.md)|선언 된 프로그램 요소가 다른 이진 또는 어셈블리에 정의 되어 있음을 나타냅니다.|
|`false`|[기본 형식](primitive-types.md)|부울 리터럴로 사용 됩니다.|
|`finally`|[예외: `try...finally` 식입니다.](./exception-handling/the-try-finally-expression.md)|와 `try` 함께 사용 되어 예외가 발생 하는지 여부에 관계 없이 실행 되는 코드 블록을 도입 합니다.|
|`fixed`|[고정](fixed.md)|스택에서 포인터를 "고정" 하 여 가비지 수집을 방지 하는 데 사용 됩니다.|
|`for`|[하며 `for...to`식](loops-for-to-expression.md)<br /><br />[루프: for...in 식](loops-for-in-expression.md)|루프 구문에 사용 됩니다.|
|`fun`|[람다 식: `fun` 키워드](./functions/lambda-expressions-the-fun-keyword.md)|익명 함수 라고도 하는 람다 식에 사용 됩니다.|
|`function`|[일치 식](match-expressions.md)<br /><br />[람다 식: 흥미로운 키워드](./functions/lambda-expressions-the-fun-keyword.md)|단일 인수에 대 한 패턴 일치 `fun` 를 포함 하 `match` 는 람다 식의 식 및 키워드에 대 한 보다 짧은 대 안으로 사용 됩니다.|
|`global`|[네임스페이스](namespaces.md)|최상위 .NET 네임 스페이스를 참조 하는 데 사용 됩니다.|
|`if`|[조건식: `if...then...else`](conditional-expressions-if-then-else.md)|조건부 분기 구문에 사용 됩니다.|
|`in`|[루프: for...in 식](loops-for-in-expression.md)<br /><br />[자세한 구문](verbose-syntax.md)|시퀀스 식에 사용 되 고, 자세한 구문에서 바인딩에서 식을 구분 하는 데 사용 됩니다.|
|`inherit`|[상속](inheritance.md)|기본 클래스 또는 기본 인터페이스를 지정 하는 데 사용 됩니다.|
|`inline`|[함수](./functions/index.md)<br /><br />[인라인 함수](./functions/inline-functions.md)|호출자의 코드에 직접 통합 되어야 하는 함수를 나타내는 데 사용 됩니다.|
|`interface`|[인터페이스](interfaces.md)|인터페이스를 선언 하 고 구현 하는 데 사용 됩니다.|
|`internal`|[Access Control](access-control.md)|멤버가 어셈블리 외부에는 표시 되지 않고 어셈블리 내부에 표시 되도록 지정 하는 데 사용 됩니다.|
|`lazy`|[Lazy 식](lazy-expressions.md)|결과가 필요한 경우에만 수행 되는 식을 지정 하는 데 사용 됩니다.|
|`let`|[`let`바인딩하](./functions/let-bindings.md)|값 또는 함수에 이름을 연결 하거나 바인딩하는 데 사용 됩니다.|
|`let!`|[비동기 워크플로](asynchronous-workflows.md)<br /><br />[계산 식](computation-expressions.md)|비동기 계산 결과에 이름을 바인딩하는 비동기 워크플로에서 사용 되며, 계산 형식인 결과에 이름을 바인딩하는 데 사용 되는 기타 계산 식에서 사용 됩니다.|
|`match`|[일치 식](match-expressions.md)|값을 패턴과 비교 하 여 분기 하는 데 사용 됩니다.|
|`match!`|[계산 식](computation-expressions.md#match)|결과에서 계산 식과 패턴 일치에 대 한 호출을 인라인 하는 데 사용 됩니다.|
|`member`|[멤버](./members/index.md)|개체 형식에서 속성 또는 메서드를 선언 하는 데 사용 됩니다.|
|`module`|[모듈](modules.md)|이름을 관련 형식, 값 및 함수 그룹에 연결 하 여 다른 코드와 논리적으로 구분 하는 데 사용 됩니다.|
|`mutable`|[let 바인딩](./functions/let-bindings.md)|변수를 선언 하는 데 사용 됩니다. 값은 변경할 수 있습니다.|
|`namespace`|[네임스페이스](namespaces.md)|이름을 관련 형식 및 모듈의 그룹과 연결 하 여 다른 코드와 논리적으로 구분 하는 데 사용 됩니다.|
|`new`|[생성자](./members/constructors.md)<br /><br />[제약 조건](./generics/constraints.md)|를 만들거나 개체를 만들 수 있는 생성자를 선언, 정의 또는 호출 하는 데 사용 됩니다.<br /><br />제네릭 매개 변수 제약 조건에도 사용 되어 형식에 특정 생성자가 있어야 함을 표시 합니다.|
|`not`|[기호 및 연산자 참조](./symbol-and-operator-reference/index.md)<br /><br />[제약 조건](./generics/constraints.md)|실제로 키워드가 아닙니다. 그러나를 `not struct` 조합 하 여 제네릭 매개 변수 제약 조건으로 사용 합니다.|
|`null`|[Null 값](./values/null-values.md)<br /><br />[제약 조건](./generics/constraints.md)|개체가 없다는 것을 나타냅니다.<br /><br />제네릭 매개 변수 제약 조건에도 사용 됩니다.|
|`of`|[구별된 공용 구조체](discriminated-unions.md)<br /><br />[대리자](delegates.md)<br /><br />[예외 형식](./exception-handling/exception-types.md)|구분 된 공용 구조체에서 값 범주 형식 및 대리자 및 예외 선언에 사용 됩니다.|
|`open`|[선언 가져오기: `open` 키워드](import-declarations-the-open-keyword.md)|네임 스페이스 또는 모듈의 콘텐츠를 한정자 없이 사용할 수 있도록 하는 데 사용 됩니다.|
|`or`|[기호 및 연산자 참조](./symbol-and-operator-reference/index.md)<br /><br />[제약 조건](./generics/constraints.md)|부울 조건에 부울 `or` 연산자로 사용 됩니다. `||`와 같습니다.<br /><br />멤버 제약 조건에도 사용 됩니다.|
|`override`|[멤버](./members/index.md)|기본 버전과 다른 추상 또는 가상 메서드의 버전을 구현 하는 데 사용 됩니다.|
|`private`|[Access Control](access-control.md)|동일한 형식이 나 모듈의 코드에 대 한 멤버 액세스를 제한 합니다.|
|`public`|[Access Control](access-control.md)|형식 외부에서 멤버에 대 한 액세스를 허용 합니다.|
|`rec`|[함수](./functions/index.md)|함수가 재귀적 임을 나타내는 데 사용 됩니다.|
|`return`|[비동기 워크플로](Asynchronous-Workflows.md)<br /><br />[계산 식](computation-expressions.md)|계산 식의 결과로 제공할 값을 나타내는 데 사용 됩니다.|
|`return!`|[계산 식](computation-expressions.md)<br /><br />[비동기 워크플로](asynchronous-workflows.md)|계산 되는 경우 포함 하는 계산 식의 결과를 제공 하는 계산 식을 나타내는 데 사용 됩니다.|
|`select`|[쿼리 식](query-expressions.md)|추출할 필드 또는 열을 지정 하기 위해 쿼리 식에 사용 됩니다. 이는 상황별 키워드입니다. 즉, 실제로 예약어는 아니며 적절 한 컨텍스트에서 키워드 처럼 동작 합니다.|
|`static`|[멤버](./members/index.md)|형식의 인스턴스 없이 호출 될 수 있는 메서드 또는 속성 또는 형식의 모든 인스턴스 간에 공유 되는 값 멤버를 나타내는 데 사용 됩니다.|
|`struct`|[구조체](structures.md)<br /><br /> [튜플](tuples.md)<br/><br/>[제약 조건](./generics/constraints.md)|구조체 형식을 선언 하는 데 사용 됩니다.<br /><br/>구조체 튜플을 지정 하는 데 사용 됩니다.<br/><br />제네릭 매개 변수 제약 조건에도 사용 됩니다.<br /><br />모듈 정의에서 OCaml 호환성에 사용 됩니다.|
|`then`|[조건식: `if...then...else`](conditional-expressions-if-then-else.md)<br /><br />[생성자](./members/constructors.md)|조건식에 사용 됩니다.<br /><br />개체 생성 후 의도 하지 않은 결과를 수행 하는 데도 사용 됩니다.|
|`to`|[하며 `for...to`식](loops-for-to-expression.md)|범위를 `for` 나타내는 루프에 사용 됩니다.|
|`true`|[기본 형식](primitive-types.md)|부울 리터럴로 사용 됩니다.|
|`try`|[예외: Try ... with 식](./exception-handling/the-try-with-expression.md)<br /><br />[예외: Try ... finally 식](./exception-handling/the-try-finally-expression.md)|예외를 생성할 수 있는 코드 블록을 소개 하는 데 사용 됩니다. `with` 또는`finally`와 함께 사용 됩니다.|
|`type`|[F# 형식](fsharp-types.md)<br /><br />[클래스](classes.md)<br /><br />[레코드](records.md)<br /><br />[구조체](structures.md)<br /><br />[열거형](enumerations.md)<br /><br />[구별된 공용 구조체](discriminated-unions.md)<br /><br />[형식 약어](type-abbreviations.md)<br /><br />[측정 단위](units-of-measure.md)|클래스, 레코드, 구조체, 구분 된 공용 구조체, 열거형 형식, 측정 단위 또는 형식 약어를 선언 하는 데 사용 됩니다.|
|`upcast`|[캐스팅 및 변환](casting-and-conversions.md)|상속 체인에서 더 높은 형식으로 변환 하는 데 사용 됩니다.|
|`use`|[리소스 관리: `use` 키워드](resource-management-the-use-keyword.md)|리소스를 해제 `let` 하기 위해 `Dispose` 를 호출 해야 하는 값에 대신 사용 됩니다.|
|`use!`|[계산 식](computation-expressions.md)<br /><br />[비동기 워크플로](asynchronous-workflows.md)|리소스를 해제 `let!` 하기 위해 호출 해야 `Dispose` 하는 값에 대 한 비동기 워크플로 및 기타 계산 식에서 대신 사용 됩니다.|
|`val`|[명시적 필드: `val` 키워드](./members/explicit-fields-the-val-keyword.md)<br /><br />[서명](signatures.md)<br /><br />[멤버](./members/index.md)|제한 된 상황에서 값을 나타내기 위해 서명에서 사용 되거나 멤버를 선언 하는 형식에 사용 됩니다.|
|`void`|[기본 형식](primitive-types.md)|.Net `void` 유형을 나타냅니다. 다른 .NET 언어와 상호 작용할 때 사용 됩니다.|
|`when`|[제약 조건](./generics/constraints.md)|패턴 일치에 대 한 부울 조건 (*가드*)에 사용 되며 제네릭 형식 매개 변수에 대 한 제약 조건 절을 도입 하는 데 사용 됩니다.|
|`while`|[하며 `while...do`식](loops-while-do-expression.md)|루핑 구문을 소개 합니다.|
|`with`|[일치 식](match-expressions.md)<br /><br />[개체 식](object-expressions.md)<br /><br />[레코드 식 복사 및 업데이트](copy-and-update-record-expressions.md)<br /><br />[형식 확장명](type-extensions.md)<br /><br />[예외: `try...with` 식입니다.](./exception-handling/the-try-with-expression.md)|패턴 일치 식에서 `match` 키워드와 함께 사용 됩니다. 또한 개체 식에 사용 되 고, 레코드 복사 식 및 형식 확장을 사용 하 여 멤버 정의를 소개 하 고, 예외 처리기를 도입 합니다.|
|`yield`|[시퀀스](sequences.md)|시퀀스에 대 한 값을 생성 하기 위해 시퀀스 식에 사용 됩니다.|
|`yield!`|[계산 식](computation-expressions.md)<br /><br />[비동기 워크플로](asynchronous-workflows.md)|지정 된 계산 식의 결과를 포함 하는 계산 식의 결과 컬렉션에 추가 하기 위해 계산 식에 사용 됩니다.|

다음 토큰은 OCaml 언어의 F# 키워드인 때문에에 예약 되어 있습니다.

- `asr`
- `land`
- `lor`
- `lsl`
- `lsr`
- `lxor`
- `mod`
- `sig`

`--mlcompatibility` 컴파일러 옵션을 사용 하는 경우 위의 키워드를 식별자로 사용할 수 있습니다.

다음 토큰은 나중에 F# 언어를 확장 하기 위한 키워드로 예약 되어 있습니다.

- `atomic`
- `break`
- `checked`
- `component`
- `const`
- `constraint`
- `constructor`
- `continue`
- `eager`
- `event`
- `external`
- `functor`
- `include`
- `method`
- `mixin`
- `object`
- `parallel`
- `process`
- `protected`
- `pure`
- `sealed`
- `tailcall`
- `trait`
- `virtual`
- `volatile`

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [기호 및 연산자 참조](./symbol-and-operator-reference/index.md)
- [컴파일러 옵션](compiler-options.md)
