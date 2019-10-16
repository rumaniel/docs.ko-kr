---
title: F#구성 요소 디자인 지침
description: 쓰기에 대 한 지침을 알아보려면 F# 다른 호출자가 사용 하기 위한 구성 요소입니다.
ms.date: 05/14/2018
ms.openlocfilehash: c61e4cd9098388b356c71c325d66c760fa866cf0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61902163"
---
# <a name="f-component-design-guidelines"></a>F#구성 요소 디자인 지침

이 문서에 대 한 구성 요소 디자인 지침의 집합이 F# 기반 프로그래밍을 F# 구성 요소 디자인 지침, Microsoft Research v14, 및 [다른 버전](https://fsharp.org/specs/component-design-guidelines/) 원래 큐 레이트 하 고 유지 관리 하는 F# Software Foundation입니다.

이 문서에 잘 알고 있다면 가정 F# 프로그래밍입니다. 덕분에 많은 F# 이 가이드의 다양 한 버전에 대 한 유용한 피드백와 작성 글에 대 한 커뮤니티입니다.

## <a name="overview"></a>개요

이 문서는 관련 된 문제 중 일부를 살펴보고 F# 구성 요소 디자인 및 코딩 합니다. 구성 요소를 다음 중 하나를 의미 합니다.

* 계층에 F# 프로젝트 내에서 외부 소비자에 게 지정 된 프로젝트입니다.
* 사용 하기 위한 라이브러리 F# 어셈블리 경계를 넘어 코드입니다.
* 어셈블리 경계에 걸쳐 모든.NET 언어에서 사용 하기 위한 라이브러리입니다.
* 라이브러리와 같은 패키지 리포지토리를 통해 배포를 위한 [NuGet](https://nuget.org)합니다.

이 문서에 설명 된 방법에 따라 합니다 [good의 다섯 가지 원칙 F# 코드](index.md#five-principles-of-good-f-code), 따라서 기능을 활용 하 고 적절 하 게 프로그래밍 개체입니다.

방법론을에 관계 없이 구성 요소 및 라이브러리 디자이너 개발자가 가장 쉽게 사용할 수 있는 API를 작성 하려고 할 때 많은 실용적이 고 사용할 수 있는 문제를 향하도록 합니다. 에 대해 인식 하 고 응용 프로그램을 [.NET 라이브러리 디자인 지침](../../standard/design-guidelines/index.md) 일관 된 즐겁게 사용할 수 있는 Api 집합을 만들기 위한 유도 합니다.

## <a name="general-guidelines"></a>일반 지침

에 적용 되는 몇 가지 유니버설 지침 F# 라이브러리를 라이브러리에 대 한 대상에 관계 없이 합니다.

### <a name="learn-the-net-library-design-guidelines"></a>.NET 라이브러리 디자인 지침에 알아봅니다.

종류에 관계 없이 F# 코딩 수행 하는에 대 한 실무 지식이 있어야 합니다 [.NET 라이브러리 디자인 지침](../../standard/design-guidelines/index.md)합니다. 대부분의 다른 F# 를.NET 프로그래머에 게 이러한 지침을 숙지 되며.NET 코드에 대 한 준수를 예상 합니다.

첫 번째는 유용한 다양 한 디자인 지침에 대 한 참조 지점.NET 라이브러리 디자인 지침을 이름, 클래스 및 인터페이스 디자인, 멤버 디자인 (속성, 메서드, 이벤트 등)에 대 한 일반적인 지침을 제공 합니다.

### <a name="add-xml-documentation-comments-to-your-code"></a>코드에 XML 문서 주석 추가

공용 Api에 대 한 XML 설명서 라이브러리에 대 한 파일을 이러한 형식 및 멤버 및 사용 설명서 작성을 사용 하 여 때 유용한 Intellisense 및 Quickinfo 사용자가 액세스할 수를 확인 합니다. 참조 된 [XML 문서](../language-reference/xml-documentation.md) xmldoc 주석 내의 추가 태그에 사용할 수 있는 다양 한 xml 태그에 대 한 합니다.

```fsharp
/// A class for representing (x,y) coordinates
type Point =

    /// Computes the distance between this point and another
    member DistanceTo: otherPoint:Point -> float
```

약식 XML 주석을 사용할 수 있습니다 (`/// comment`), 또는 표준 XML 주석 (`///<summary>comment</summary>`).

### <a name="consider-using-explicit-signature-files-fsi-for-stable-library-and-component-apis"></a>안정적인 라이브러리 및 Api 구성 요소에 대 한 명시적 서명 파일 (.fsi)를 사용 하는 것이 좋습니다.

명시적 서명 파일을 사용 하는 F# 는 전체 공용 제공을 명확히 구분 공개 문서도 라이브러리의 노출 및 내부를 확인 하는 데 도움이 공용 API의 간결한 요약을 제공 하는 라이브러리 구현 세부 정보입니다. 서명 파일 공용 API를 구현 및 서명 파일에 대해 적용할 변경 사항을 요구 하 여 변화 하는 마찰을 추가 하는 note 합니다. 결과적으로, 서명 파일은 일반적으로 도입 될 API 그 수에 더 이상 크게 변경 해야 하는 경우입니다.

### <a name="always-follow-best-practices-for-using-strings-in-net"></a>.NET에서 문자열 사용에 대 한 모범 사례를 따르고 항상

따릅니다 [.NET에서 문자열 사용에 대 한 모범 사례](../../standard/base-types/best-practices-strings.md) 지침입니다. 특히, 항상 명시적 *문화적 의도* 변환 및 문자열 비교 (있는 경우).

## <a name="guidelines-for-f-facing-libraries"></a>에 대 한 지침 F#-연결 라이브러리

이 섹션에서는 공용 개발을 위한 권장 사항 표시 F#-연결 라이브러리입니다. 사용할 수 있는 공용 Api를 노출 하는 라이브러리, 즉 F# 개발자입니다. 다양 한 라이브러리 디자인 권장 사항에 맞게 해당는 F#입니다. 특정 권장 사항가 없으면.NET 라이브러리 디자인 지침에는 대체 (fallback) 지침.

### <a name="naming-conventions"></a>명명 규칙

#### <a name="use-net-naming-and-capitalization-conventions"></a>.NET 명명 및 대/소문자 규칙을 사용 하 여

다음 표에서.NET 이름 지정 및 대/소문자 규칙을 따릅니다. 작은 추가 포함 하는 F# 를 생성 합니다.

| 구문 | 사례 | 파트 | 예제 | 노트 |
|-----------|------|------|----------|-------|
| 구체적인 형식 | PascalCase | 명사 adjective / | 목록, Double, 복잡 한 | 구체적인 형식은 구조체, 클래스, 열거형, 대리자, 레코드 및 공용 구조체입니다. 형식 이름은 일반적으로 OCaml에서 소문자 있지만 F# 는 형식에 대 한.NET 명명 체계를 채택 했습니다.
| DLL           | PascalCase |                 | Fabrikam.Core.dll |  |
| 공용 구조체 태그     | PascalCase | 명사 | 일부 추가, 성공 | 공용 Api에서 접두사를 사용 하지 마세요. 필요에 따라 내부와 같은 경우에 접두사를 사용 하 여 `type Teams = TAlpha | TBeta | TDelta.` |
| 이벤트(event)          | PascalCase | 동사 | ValueChanged / ValueChanging |  |
| 예외     | PascalCase |      | WebException | 이름을 "Exception" 끝나야 합니다. |
| 필드          | PascalCase | 명사 | CurrentName  | |
| 인터페이스 형식 |  PascalCase | 명사 adjective / | IDisposable | 이름 "I"로 시작 해야 합니다. |
| 메서드 |  PascalCase |  동사 | ToString | |
| 네임스페이스 | PascalCase | | Microsoft.FSharp.Core | 일반적으로 사용 하 여 `<Organization>.<Technology>[.<Subnamespace>]`, 하지만 기술을 조직 으로부터 독립적인 경우 조직은 삭제 합니다. |
| 매개 변수 | camelCase | 명사 |  typeName, 변환, 범위 | |
| 값 (내부) 수 | camelCase 또는 PascalCase | 명사 / 동사 |  getValue, myTable |
| 값 (외부)를 사용 합니다. | camelCase 또는 PascalCase | 명사/동사  | List.map Dates.Today | let 바인딩 값 기존의 함수형 디자인 패턴을 따를 경우 공용 많습니다. 그러나 일반적으로 사용 하 여 PascalCase 때 식별자는 다른.NET 언어에서 사용할 수 있습니다. |
| 속성  | PascalCase  | 명사 adjective /  | IsEndOfFile, BackColor  | 부울 속성 일반적으로 사용할 수 있으며 긍정적인 IsEndOfFile, 없습니다 IsNotEndOfFile 같이 해야 합니다.

#### <a name="avoid-abbreviations"></a>약어를 방지 합니다.

.NET 지침에는 약어를 사용 하지 못하도록 (예를 들어 "사용 `OnButtonClick` 대신 `OnBtnClick`"). 일반적인 약어와 같은 `Async` "비동기"에 대 한 허용 됩니다. 이 지침은 함수형 프로그래밍;에 대 한 경우에 따라 무시 됩니다. 예를 들어 `List.iter` "반복"에 대 한 약어를 사용 합니다. 이러한 이유로 보다 심층적 정확해 경향이 약어를 사용 하 여 F#에서F# 프로그래밍, 하지만 공용 구성 요소 디자인에서 일반적으로 계속 피해 야 합니다.

#### <a name="avoid-casing-name-collisions"></a>이름 충돌을 대/소문자를 방지 합니다.

.NET 지침 예를 들어 일부 클라이언트 언어 (예: Visual Basic)는 대/소문자 이름 충돌을 명확 하 게 대/소문자가 단독으로 사용할 수 없습니다.

#### <a name="use-acronyms-where-appropriate"></a>적합 한 머리글자어 사용

XML과 같은 머리 글자어 약어 않으며 소문자로 시작된 양식 (Xml)에.NET 라이브러리에서 널리 사용 됩니다. 유명한, 잘 알려진 머리글자어 사용 되어야 합니다.

#### <a name="use-pascalcase-for-generic-parameter-names"></a>PascalCase를 사용 하 여 제네릭 매개 변수 이름에 대 한

PascalCase를 사용 하 여 제네릭 매개 변수 이름에 대 한 포함 하 여 공용 Api에 대 한 수행 F#-라이브러리를 연결 합니다. 특히과 같은 이름을 사용 `T`, `U`, `T1`, `T2` 임의의 제네릭 매개 변수 및 특정 이름을 적합 한 다음에 대 한 F#-연결 라이브러리와 같은 이름을 사용 하 여 `Key`, `Value`, `Arg` (하지만 하지 예를 들어 `TKey`).

#### <a name="use-either-pascalcase-or-camelcase-for-public-functions-and-values-in-f-modules"></a>PascalCase 또는 camelCase를 사용 하 여 공용 함수 및 값에 대 한 F# 모듈

camelCase 사용할 수 있도록 설계는 공용 함수는 정규화 되지 않은 (예를 들어 `invalidArg`), (예를 들어 List.map) "표준 컬렉션 기능"입니다. 두이 경우 모두에서 함수 이름을 훨씬 언어에서 키워드 처럼 작동 합니다.

### <a name="object-type-and-module-design"></a>개체, 형식 및 모듈 디자인

#### <a name="use-namespaces-or-modules-to-contain-your-types-and-modules"></a>네임 스페이스 또는 모듈을 사용 하 여 형식 및 모듈에 포함

각 F# 구성 요소에서 파일 네임 스페이스 선언 또는 모듈 선언 중 하나를 시작 해야 합니다.

```fsharp
namespace Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
     ...

module CommonOperations =
    ...
```

또는

```fsharp
module Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
    ...

module CommonOperations =
    ...
```

모듈 및 네임 스페이스를 사용 하 여 최상위 수준에서 코드를 구성할 수 간의 차이 다음과 같습니다.

* 네임 스페이스에는 여러 파일 걸쳐 있을 수 있습니다.
* 네임 스페이스를 포함할 수 없습니다 F# 는 내부 모듈 내에서 있지 않는 한 함수
* 지정 된 모든 모듈에 대 한 코드를 단일 파일에 포함 되어야 합니다.
* 최상위 모듈에 포함 될 수 있습니다 F# 함수는 내부 모듈에 대 한 필요 없이

최상위 네임 스페이스 또는 모듈 간의 선택 코드의 컴파일된 형태에 영향을 줍니다 및 따라서는 뷰에 영향을 기타.NET 언어에서 API 결국 사용 해야 외부 F# 코드입니다.

#### <a name="use-methods-and-properties-for-operations-intrinsic-to-object-types"></a>개체 형식에 내장 된 작업에 대 한 메서드 및 속성 사용

개체를 사용할 때는 메서드와 해당 유형에 대 한 속성으로 구현 하는 사용할 수 있는 기능을 확인 하는 것이 좋습니다.

```fsharp
type HardwareDevice() =

    member this.ID = ...

    member this.SupportedProtocols = ...

type HashTable<'Key,'Value>(comparer: IEqualityComparer<'Key>) =

    member this.Add(key, value) = ...

    member this.ContainsKey(key) = ...

    member this.ContainsValue(value) = ...
```

필요한 지정된 된 멤버에 대 한 기능 대량의 반드시 해당 멤버에서 구현 되지 하지만 기능을 사용할 수 있는 부분 이어야 합니다.

#### <a name="use-classes-to-encapsulate-mutable-state"></a>변경 가능한 상태를 캡슐화 할 클래스를 사용 합니다.

F#에 수행할 수 있는 상태는 이미 클로저, 시퀀스 식, 비동기 계산 등의 다른 언어 구문으로 캡슐화 되지 해야 합니다.

```fsharp
type Counter() =
    // let-bound values are private in classes.
    let mutable count = 0

    member this.Next() =
        count <- count + 1
        count
```

#### <a name="use-interfaces-to-group-related-operations"></a>인터페이스를 사용 하 여 그룹화 관련 작업

인터페이스 형식을 사용 하 여 작업 집합을 나타냅니다. 이 함수는 튜플 또는 함수의 레코드 등의 기타 옵션에는 것이 좋습니다.

```fsharp
type Serializer =
    abstract Serialize<'T>: preserveRefEq: bool -> value: 'T -> string
    abstract Deserialize<'T>: preserveRefEq: bool -> pickle: string -> 'T
```

우선적으로:

```fsharp
type Serializer<'T> = {
    Serialize: bool -> 'T -> string
    Deserialize: bool -> string -> 'T
}
```

인터페이스는 새로운 함수는 일반적으로 제공을 달성 하기 위해 사용할 수 있는.net에서 최고급 개념입니다. 또한 이러한 수 수 형식을 인코딩하는 데 존재 레코드 함수 일 수 없습니다. 프로그램에 있습니다.

#### <a name="use-a-module-to-group-functions-which-act-on-collections"></a>컬렉션에 대해 작동 하는 그룹 함수 모듈을 사용 합니다.

컬렉션 형식을 정의 하는 경우와 같은 표준 작업 집합이 제공 고려해 야 `CollectionType.map` 고 `CollectionType.iter`) 새 컬렉션 형식에 대 한 합니다.

```fsharp
module CollectionType =
    let map f c =
        ...
    let iter f c =
        ...
```

이러한 모듈을 포함 하는 경우 FSharp.Core 있는 함수에 대 한 표준 명명 규칙을 따릅니다.

#### <a name="use-a-module-to-group-functions-for-common-canonical-functions-especially-in-math-and-dsl-libraries"></a>수치 연산 및 DSL 라이브러리에서 특히 일반적이 고 정식 함수에 대 한 모듈 그룹 기능을 사용 하 여

예를 들어 `Microsoft.FSharp.Core.Operators` 최상위 함수의 자동으로 열린된 컬렉션입니다 (같은 `abs` 및 `sin`) FSharp.Core.dll에서 제공 합니다.

통계 라이브러리 함수를 사용 하 여 모듈에 포함 될 수 있습니다 마찬가지로 `erf` 및 `erfc`, 여기서이 모듈은 자동으로 또는 명시적으로 열어야 합니다.

#### <a name="consider-using-requirequalifiedaccess-and-carefully-apply-autoopen-attributes"></a>RequireQualifiedAccess를 사용 하 여 고려 하 고 신중 하 게 AutoOpen 특성 적용

추가 된 `[<RequireQualifiedAccess>]` 모듈을 열 수 있습니다 하 액세스를 정규화 하는 모듈의 요소에 대 한 참조가 필요 명시적 특성을 모듈을 나타냅니다. 예를 들어를 `Microsoft.FSharp.Collections.List` 모듈에이 특성이 있습니다.

이 함수 및 모듈의 값 이름이 다른 모듈에서 이름이 충돌할 가능성이 있는 경우에 유용 합니다. 정규화 된 액세스가 필요한 장기적 유지 관리성 및 라이브러리의 진화를 크게 증가할 수 있습니다.

추가 된 `[<AutoOpen>]` 특성을 모듈에 포함 된 네임 스페이스가 열릴 때 모듈을 열 수를 의미 합니다. `[<AutoOpen>]` 어셈블리를 참조할 때 자동으로 열리는 모듈을 표시 하기 위해 어셈블리에도 특성이 적용 될 수 있습니다.

예를 들어 통계 라이브러리 **MathsHeaven.Statistics** 포함 될 수 있습니다는 `module MathsHeaven.Statistics.Operators` 함수를 포함 하 `erf` 고 `erfc`입니다. 이 모듈을 표시 하는 것이 적합 `[<AutoOpen>]`합니다. 즉, `open MathsHeaven.Statistics` 는 또한이 모듈을 열고 이름을 가져올 `erf` 고 `erfc` 범위로 합니다. 또 다른 좋은 사용 `[<AutoOpen>]` 확장 메서드를 포함 하는 모듈입니다.

과 용 `[<AutoOpen>]` 잠재 고객 오염된 네임 스페이스 및 특성을 신중 하 게 사용 해야 합니다. 특정 도메인에 적절히 사용 하는 특정 라이브러리에 대 한 `[<AutoOpen>]` 유용성을 향상 시킬 수 있습니다.

#### <a name="consider-defining-operator-members-on-classes-where-using-well-known-operators-is-appropriate"></a>잘 알려진 연산자를 사용 하는 적절 한 클래스에서 연산자 멤버를 정의 하는 것이 좋습니다.

경우에 따라 클래스 벡터와 같은 수학적 구문을 모델링 하는 데 사용 됩니다. 도메인 모델링 되는 잘 알려진 연산자에 있는 경우 유용 내장 함수를 클래스 멤버로 정의 합니다.

```fsharp
type Vector(x: float) =

    member v.X = x

    static member (*) (vector: Vector, scalar: float) = Vector(vector.X * scalar)

    static member (+) (vector1: Vector, vector2: Vector) = Vector(vector1.X + vector2.X)

let v = Vector(5.0)

let u = v * 10.0
```

이 설명서는 이러한 형식에 대 한 일반.NET 설명서에 해당합니다. 그러나 또한에 중요할 수 있습니다 F# 이러한 형식을 함께에서 사용할 수 있도록 코딩 F# 함수와 List.sumBy 같은 멤버 제약 조건과 함께 메서드.

#### <a name="consider-using-compiledname-to-provide-a-net-friendly-name-for-other-net-language-consumers"></a>CompiledName를 사용 하 여 제공 하는 합니다. 다른.NET 언어 소비자 NET 이름

하나의 스타일 이름을 지정 하려는 경우에 따라 F# 소비자 (소문자로 표시 되도록 정적 멤버와 같은 모듈 기반 함수 처럼)에 있으 나 다른 스타일 이름에 대 한 어셈블리로 컴파일할 때. 사용할 수는 `[<CompiledName>]` 에 대 한 다른 스타일을 제공 하는 특성 아닌 F# 어셈블리를 사용 하는 코드입니다.

```fsharp
type Vector(x:float, y:float) =

    member v.X = x
    member v.Y = y

    [<CompiledName("Create")>]
    static member create x y = Vector (x, y)

let v = Vector.create 5.0 3.0
```

사용 하 여 `[<CompiledName>]`에 대 한.NET 명명 규칙을 사용할 수 있습니다 아닌 F# 어셈블리의 소비자입니다.

#### <a name="use-method-overloading-for-member-functions-if-doing-so-provides-a-simpler-api"></a>이렇게 하면 간단한 API를 제공 하는 경우 멤버 함수에 대 한 메서드 오버 로드 사용

메서드 오버 로드는 하지만 다른 옵션이 나 인수가 유사한 기능을 수행 해야 할 수 있는 API를 간소화 하기 위한 강력한 도구입니다.

```fsharp
type Logger() =

    member this.Log(message) =
        ...
    member this.Log(message, retryPolicy) =
        ...
```

F#, 인수의 형식 보다는 수의 인수 오버 로드에 더 일반적입니다.

#### <a name="hide-the-representations-of-record-and-union-types-if-the-design-of-these-types-is-likely-to-evolve"></a>이러한 종류의 디자인 변경 될 수 있으므로 공용 구조체 형식과 레코드의 표현을 숨기기

구체적인 표현의 개체를 노출 하지 마십시오. 예를 들어 구체적인 표현을 <xref:System.DateTime> 값이.NET 라이브러리 디자인의 외부, 공용 API에서 노출 되지 않습니다. 런타임 시 공용 언어 런타임 실행 전체에서 사용 되는 커밋된 구현을 알고 있습니다. 그러나 컴파일된 코드 자체는 선택 하지 않습니다 구체적인 표현에 대 한 종속성입니다.

#### <a name="avoid-the-use-of-implementation-inheritance-for-extensibility"></a>확장성에 대 한 구현 상속을 사용 하지 못하도록

F#를 구현 상속은 거의 사용 되지 않습니다. 또한 상속 계층 구조는 종종 복잡 하 고 새 요구 사항을 도착할 때 변경 하기가 어렵습니다. 상속 구현에 여전히 존재 F# 호환성 및 것이 문제를 위한 최선의 솔루션 하지만 대안 기법의에서 찾아야 할 드문 경우에 F# 인터페이스와 같은 다형성을 디자인할 때 프로그램 구현입니다.

### <a name="function-and-member-signatures"></a>함수 및 멤버 시그니처

#### <a name="use-tuples-for-return-values-when-returning-a-small-number-of-multiple-unrelated-values"></a>소수의 관련 없는 여러 값을 반환 하는 경우 반환 값에 대 한 튜플을 사용합니다

반환 형식에 튜플을 사용의 좋은 예는 다음과 같습니다.

```fsharp
val divrem: BigInteger -> BigInteger -> BigInteger * BigInteger
```

에 대 한 많은 구성 요소가 포함 된 형식을 반환 하거나 구성 요소 식별이 가능한 단일 엔터티를 관련 된 경우 튜플을 대신 명명 된 형식을 사용 하 여 고려해 야 합니다.

#### <a name="use-asynct-for-async-programming-at-f-api-boundaries"></a>사용 하 여 `Async<T>` 비동기 프로그래밍에 대 한 F# API 경계

라는 해당 동기 작업 인지 `Operation` 반환 하는 `T`, 다음 비동기 작업 이름을 지정 해야 `AsyncOperation` 반환 하는 경우 `Async<T>` 또는 `OperationAsync` 반환 하는 경우 `Task<T>`합니다. Begin/End 메서드를 노출 하는 자주 사용 되는.NET 형식을 사용 하는 것이 좋습니다에 대 한 `Async.FromBeginEnd` 제공 하는 외관 확장 메서드를 작성 하는 F# .NET Api에 비동기 프로그래밍 모델입니다.

```fsharp
type SomeType =
    member this.Compute(x:int): int =
        ...
    member this.AsyncCompute(x:int): Async<int> =
        ...

type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        ...
```

### <a name="exceptions"></a>예외

참조 [오류 관리](conventions.md#error-management) 에 예외, 결과 및 옵션의 적절 한 사용에 대해 알아봅니다.

### <a name="extension-members"></a>확장 멤버

#### <a name="carefully-apply-f-extension-members-in-f-to-f-components"></a>신중 하 게 적용 F# 에서 확장 멤버 F#에서F# 구성 요소

F#일반적으로 대부분의 해당 모드를 사용 하 여 형식과 연결 된 기본 작업의 클로저에 작업에 대 한 확장 멤버에만 사용 해야 합니다. 일반적 용도 중 하나를 더 자연 스러운 수 있는 Api를 제공 하는 것 F# 다양 한.NET 형식:

```fsharp
type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        Async.FromBeginEnd(this.BeginReceive, this.EndReceive)

type System.Collections.Generic.IDictionary<'Key,'Value> with
    member this.TryGet key =
        let ok, v = this.TryGetValue key
        if ok then Some v else None
```

### <a name="union-types"></a>공용 구조체 형식

#### <a name="use-discriminated-unions-instead-of-class-hierarchies-for-tree-structured-data"></a>클래스 계층 구조 대신 구별 된 공용 구조체를 사용 하 여 트리 구조의 데이터에 대 한

트리 구조는 재귀적으로 정의 합니다. 이 상속을 사용 하 여 불편 하지만 구별 된 공용 구조체를 사용 하 여 세련 된입니다.

```fsharp
type BST<'T> =
    | Empty
    | Node of 'T * BST<'T> * BST<'T>
```

또한 구별 된 공용 구조체를 사용 하 여 트리 형태의 데이터를 나타내는 패턴 일치에서 exhaustiveness에서 이점을 얻을 수 있습니다.

#### <a name="use-requirequalifiedaccess-on-union-types-whose-case-names-are-not-sufficiently-unique"></a>사용 하 여 `[<RequireQualifiedAccess>]` 공용 구조체 형식의 경우 이름이 충분히 고유 하지 않습니다.

이름이 같은 구별 된 공용 구조체 케이스와 같은 다른 작업에 가장 적합 한 이름을 여기서는 도메인의 상황이 발생할 수 있습니다. 사용할 수 있습니다 `[<RequireQualifiedAccess>]` 를 혼란 스러운 오류 섀도잉 인해 순서에 따라 달라 집니다 방지 하기 위해 경우 대/소문자를 구분 하 `open` 문

#### <a name="hide-the-representations-of-discriminated-unions-for-binary-compatible-apis-if-the-design-of-these-types-is-likely-to-evolve"></a>이러한 형식의 디자인 발전 시킬 가능성이 있는 경우 이진 호환 되는 Api에 대 한 구별 된 공용 구조체의 표현을 숨기기

공용 구조체 형식은 F# 는 간결한 프로그래밍 모델에 대 한 forms 패턴 일치 합니다. 이전에 설명한 대로 이러한 종류의 디자인 변경 될 수 있으므로 경우 구체적인 데이터 표현을 노출 하지 마십시오.

예를 들어 구별 된 공용 구조체의 표시를 숨길 수 있습니다는 private 또는 internal 선언을 사용 하 여 또는 서명 파일을 사용 하 여 합니다.

```fsharp
type Union =
    private
    | CaseA of int
    | CaseB of string
```

구별 된 공용 구조체를 무차별적으로 표시 하는 경우 것 버전 하기가 라이브러리 사용자 코드를 중단 하지 않고 있습니다. 대신, 형식의 값에 대 한 패턴 일치를 허용 하도록 하나 이상의 활성 패턴을 노출 하는 것이 좋습니다.

활성 패턴을 제공 하는 대체 방법을 제공 F# 고객에 게 노출 방지 하는 동안 일치 하는 패턴으로 F# 공용 구조체 형식을 직접.

### <a name="inline-functions-and-member-constraints"></a>인라인 함수 및 멤버 제약 조건

#### <a name="define-generic-numeric-algorithms-using-inline-functions-with-implied-member-constraints-and-statically-resolved-generic-types"></a>인라인 함수를 사용 하 여 정적으로 확인 된 제네릭 형식 제약 조건이 암시적된 멤버와 일반 숫자 알고리즘을 정의

산술 멤버 제약 조건 및 F# 비교 제약 조건은 표준에 대 한 F# 프로그래밍 합니다. 예를 들어, 다음 코드를 고려하세요.

```fsharp
let inline highestCommonFactor a b =
    let rec loop a b =
        if a = LanguagePrimitives.GenericZero<_> then b
        elif a < b then loop a (b - a)
        else loop (a - b) b
    loop a b
```

이 함수는 다음과 같습니다.

```fsharp
val inline highestCommonFactor : ^T -> ^T -> ^T
                when ^T : (static member Zero : ^T)
                and ^T : (static member ( - ) : ^T * ^T -> ^T)
                and ^T : equality
                and ^T : comparison
```

수학 라이브러리의 공용 API에 대 한 적합 한 함수입니다.

#### <a name="avoid-using-member-constraints-to-simulate-type-classes-and-duck-typing"></a>형식 클래스 및 덕 형식 지정을 시뮬레이션 하기 위해 멤버 제약 조건을 사용 하지 마십시오

"덕 형식 지정"를 사용 하 여 시뮬레이션할 수 있습니다 F# 멤버 제약 조건입니다. 그러나 멤버는 사용 하 여이 아닌 일반 사용 해야 F#에서F# 라이브러리 디자인 합니다. 즉, 알 수 없는 또는 비표준 암시적 제약 조건을 기반으로 하는 라이브러리 디자인 고정적인 해지고 하나의 특정 프레임 워크 패턴에 연결 하는 사용자 코드를 발생 시키는 경향이 있습니다.

또한이 방식으로 멤버 제약 조건의 사용량이 매우 긴 컴파일 시간이 발생할 수 있는 가능성이 있습니다.

### <a name="operator-definitions"></a>연산자 정의

#### <a name="avoid-defining-custom-symbolic-operators"></a>기호화 된 사용자 지정 연산자를 정의 하지 마십시오.

사용자 지정 연산자 일부 상황에서 필수적인 및 표기 장치가 구현 코드의 큰 본문이 매우 유용 합니다. 라이브러리의 새 사용자에 대 한 명명 된 함수를 사용 하기 쉽게 많습니다. 또한 기호화 된 사용자 지정 연산자 문서 하기가 수 및 사용자를 찾을 IDE 및 검색 엔진의 기존 제한으로 인해 연산자에 대 한 도움말을 조회 하기가 더 어렵습니다.

결과적으로, 명명 된 함수의 멤버와 기능을 게시 하 고 또한 cognitive 비용 있는 것을 확인 하 고 설명서 표기법 상의 이점을 능가 하는 경우에이 기능에 대 한 연산자를 노출 하는 것이 좋습니다.

### <a name="units-of-measure"></a>측정 단위

#### <a name="carefully-use-units-of-measure-for-added-type-safety-in-f-code"></a>신중 하 게 측정 단위를 사용 하 여 추가 형식 안전성에 대 한 F# 코드

측정 단위에 대 한 입력 추가 정보는 다른.NET 언어에서 볼 때 지워집니다. .NET 구성 요소, 도구 및 리플렉션 형식-sans-단위를 볼 수 있도록 주의 합니다. 예를 들어 C# 소비자가 표시 됩니다 `float` 대신 `float<kg>`합니다.

### <a name="type-abbreviations"></a>형식 약어

#### <a name="carefully-use-type-abbreviations-to-simplify-f-code"></a>신중 하 게 형식 약어를 사용 하 여 단순화 하기 위해 F# 코드

.NET 구성 요소, 도구 및 리플렉션 형식에 대 한 약식된 이름이 표시 되지 않습니다. 형식 약어의 중요 한 사용 현황에 나타날 것 보다 훨씬 더 복잡할 실제로, 소비자가 혼동을 줄 수는 도메인을 만들 수도 있습니다.

#### <a name="avoid-type-abbreviations-for-public-types-whose-members-and-properties-should-be-intrinsically-different-to-those-available-on-the-type-being-abbreviated"></a>해당 멤버 및 속성 약어로 표시 되는 형식에서 사용할 수 있는 본질적으로 달라 야 하는 공용 형식에 대 한 형식 약어를 방지 합니다.

이 경우 약어로 중인 형식을 정의 하 고 실제 형식의 표현에 대해 너무 많이 표시 됩니다. 대신, 단일 사례 구별된 된 공용 구조체 또는 클래스 형식 약어를 래핑하는 것이 좋습니다 (또는 성능 필수 이면 약어를 래핑할 구조체 형식을 사용 하 여).

특수 사례로 다중 맵을 정의 하 고 싶어 하는 예를 들어는 F# 지도, 예를 들어:

```fsharp
type MultiMap<'Key,'Value> = Map<'Key,'Value list>
```

그러나이 형식에 대해 논리 점 표기법 작업이 맵에서 연산과 동일 하 게 하지 않습니다 – 예를 들어 하다는 lookup 연산자 매핑. [키] 반환 키 예외가 발생 하는 것이 아니라 사전에 없는 경우 빈 목록입니다.

## <a name="guidelines-for-libraries-for-use-from-other-net-languages"></a>다른.NET 언어에서 사용 하기 위해 라이브러리에 대 한 지침

다른.NET 언어에서 사용 하기 위한 라이브러리를 디자인할 때을 준수 하는 것이 중요 합니다 [.NET 라이브러리 디자인 지침](../../standard/design-guidelines/index.md)합니다. 이 문서에서는 이러한 라이브러리는로 레이블이 지정 바닐라.NET 라이브러리와는 반대로 F#-연결 라이브러리를 사용 하는 F# 제한 없이 생성 합니다. .NET Framework의 나머지 부분과 일치 친숙 하 고 자연 스러운 Api 사용을 최소화 하 여 제공 의미 바닐라.NET 라이브러리 디자인 F#-공용 API의 특정 구문입니다. 규칙은 다음 섹션에 설명 되어 있습니다.

### <a name="namespace-and-type-design-for-libraries-for-use-from-other-net-languages"></a>Namespace 및 형식 디자인 (다른.NET 언어에서 사용 하기 위한 라이브러리)

#### <a name="apply-the-net-naming-conventions-to-the-public-api-of-your-components"></a>구성 요소의 공용 API를.NET 명명 규칙을 적용 합니다.

약식된 이름이.NET 글자를 대문자로 표시 지침을 사용 하 여 특별 한 주의 해야 합니다.

```fsharp
type pCoord = ...
    member this.theta = ...

type PolarCoordinate = ...
    member this.Theta = ...
```

#### <a name="use-namespaces-types-and-members-as-the-primary-organizational-structure-for-your-components"></a>구성 요소에 대 한 기본 조직 구조와 네임 스페이스, 형식 및 멤버를 사용 하 여

로 시작 해야 공용 기능을 포함 하는 모든 파일을 `namespace` 선언 및 네임 스페이스에만 공용 엔터티 형식 이어야 합니다. 사용 하지 않는 F# 모듈.

구현 코드, 형식 유틸리티 및 유틸리티 함수를 포함 하려면 public이 아닌 모듈을 사용 합니다.

정적 형식은 이어야 합니다. 기본 모듈을 통해 API의 향후 진화를 위한 내에서 사용할 수 없습니다는 오버 로드 및 다른.NET API 디자인 개념을 사용할 수 있으므로 F# 모듈.

예를 들어, 다음 공용 API 대신:

```fsharp
module Fabrikam

module Utilities =
    let Name = "Bob"
    let Add2 x y = x + y
    let Add3 x y z = x + y + z
```

대신 고려 합니다.

```fsharp
namespace Fabrikam

[<AbstractClass; Sealed>]
type Utilities =
    static member Name = "Bob"
    static member Add(x,y) = x + y
    static member Add(x,y,z) = x + y + z
```

#### <a name="use-f-record-types-in-vanilla-net-apis-if-the-design-of-the-types-wont-evolve"></a>사용 하 여 F# 형식의 디자인 않습니다 진화 하는 경우 바닐라.NET Api에서에서 레코드 종류

F#레코드 종류는 간단한.NET 클래스를 컴파일합니다. 이러한 Api의 일부 간단 하 고 안정적인 유형에 대해 적합합니다. 사용을 고려해 야 합니다 `[<NoEquality>]` 및 `[<NoComparison>]` 특성을 인터페이스의 자동 생성 되지 않도록 합니다. 또한 공용 필드에 이러한 노출으로 한 바닐라.NET Api의에서 변경 가능한 레코드 필드를 사용 하지 마십시오. 항상 클래스는 API의 향후 진화를 위한 유연한 옵션을 제공 하는 것이 좋습니다.

예를 들어, 다음 F# 하는 공용 API를 노출 하는 코드를 C# 소비자:

F#:

```fsharp
[<NoEquality; NoComparison>]
type MyRecord =
    { FirstThing: int
        SecondThing: string }
```

C#: 

```csharp
public sealed class MyRecord
{
    public MyRecord(int firstThing, string secondThing);
    public int FirstThing { get; }
    public string SecondThing { get; }
}
```

#### <a name="hide-the-representation-of-f-union-types-in-vanilla-net-apis"></a>표현의 숨기기 F# 바닐라.NET Api에서에서 공용 구조체 형식

F#공용 구조체 형식을 자주 사용 되지 않는 구성 요소 경계에 대해서도 F#에서F# 코딩 합니다. 구성 요소 및 라이브러리 내에서 내부적으로 사용 하는 경우에 뛰어난 구현 장치 됩니다.

바닐라.NET API를 디자인할 때에 개인 선언 또는 서명 파일을 사용 하 여 공용 구조체 형식의 표현을 숨기기 하는 것이 좋습니다.

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True
```

또한 원하는 위해 내부적으로 멤버를 사용 하 여 공용 구조체 표현을 사용 하는 형식을 보강할 수 있습니다. NET 지향 API입니다.

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True

    /// A public member for use from C#
    member x.Evaluate =
        match x with
        | And(a,b) -> a.Evaluate && b.Evaluate
        | Not a -> not a.Evaluate
        | True -> true

    /// A public member for use from C#
    static member CreateAnd(a,b) = And(a,b)
```

#### <a name="design-gui-and-other-components-using-the-design-patterns-of-the-framework"></a>GUI 디자인과 프레임 워크의 디자인 패턴을 사용 하 여 다른 구성 요소

여러 다른 프레임 워크는 WinForms, WPF, ASP.NET 등.NET에서 사용할 수 있습니다. 이러한 프레임 워크에서 사용 하 여 구성 요소를 디자인 하는 경우 각각에 대 한 이름 지정 및 디자인 규칙 사용 해야 합니다. 예를 들어 WPF 프로그래밍에 대 한 디자인 하는 클래스에 대 한 WPF 디자인 패턴을 채택 합니다. 사용자 인터페이스 프로그래밍에서 모델에 대 한 이벤트와 같은 디자인 패턴을 사용 하 고 같은 알림 기반 컬렉션 <xref:System.Collections.ObjectModel>합니다.

### <a name="object-and-member-design-for-libraries-for-use-from-other-net-languages"></a>개체 및 멤버 디자인 (다른.NET 언어에서 사용 하기 위한 라이브러리)

#### <a name="use-the-clievent-attribute-to-expose-net-events"></a>CLIEvent 특성을 사용 하 여.NET 이벤트를 노출 하려면

생성을 `DelegateEvent` 특정.NET을 사용 하 여 대리자 개체를 사용 하는 형식 및 `EventArgs` (아닌 `Event`만 사용 하는 `FSharpHandler` 기본적으로 형식으로) 다른.NET 언어에 익숙한 방식으로 이벤트를 게시 되도록 합니다.

```fsharp
type MyBadType() =
    let myEv = new Event<int>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish

type MyEventArgs(x: int) =
    inherit System.EventArgs()
    member this.X = x

    /// A type in a component designed for use from other .NET languages
type MyGoodType() =
    let myEv = new DelegateEvent<EventHandler<MyEventArgs>>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish
```

#### <a name="expose-asynchronous-operations-as-methods-which-return-net-tasks"></a>.NET 작업을 반환 하는 메서드로 비동기 작업 노출

작업은 활성 비동기 계산을 나타내는.NET에서 사용 됩니다. 보다 작은 구성 하는 일반적인 작업은 F# `Async<T>` 개체에 "이미 실행" 작업을 나타내며를 구성할 수 함께 수행 하는 병렬 컴퍼지션 또는 취소 신호 전파를 숨기는 방식 때문 및 다른 상황에 맞는 매개 변수입니다.

그러나 그럼에도 불구 하 고, 작업을 반환 하는 메서드는.NET에서 비동기 프로그래밍의 표준 표현 합니다.

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =

    let compute (x: int): Async<int> = async { ... }

    member this.ComputeAsync(x) = compute x |> Async.StartAsTask
```

자주 수행 하면 명시적 취소 토큰을 적용할 수도 있습니다.

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =
    let compute(x: int): Async<int> = async { ... }
    member this.ComputeAsTask(x, cancellationToken) = Async.StartAsTask(compute x, cancellationToken)
```

#### <a name="use-net-delegate-types-instead-of-f-function-types"></a>대신.NET 대리자 형식을 사용 하 여 F# 형식 함수

여기서 "F# 형식 함수"와 같은 "화살표" 형식은 의미 `int -> int`합니다.

다음과 같이 변경 하는 대신

```fsharp
member this.Transform(f: int->int) =
    ...
```

방법

```fsharp
member this.Transform(f: Func<int,int>) =
    ...
```

F# 함수 형식으로 표시 됩니다 `class FSharpFunc<T,U>` 다른.NET 언어에 있으며 대리자 유형을 이해 하는 언어 기능 및 도구에 덜 적합 합니다. .NET Framework 3.5 이상을 대상으로 하는 고차 메서드를 작성할 때 합니다 `System.Func` 고 `System.Action` 대리자는.NET 개발자가 원활한 방식으로 이러한 Api를 사용할 수 있도록 게시할 오른쪽 Api. (.NET Framework 2.0을 대상으로 하는 경우 시스템에 정의 된 대리자 형식 보다 제한적인는와 같은 미리 정의 된 대리자 형식을 사용 하는 것이 좋습니다 `System.Converter<T,U>` 또는 특정 대리자 형식을 정의 합니다.)

한편,.NET의 대리자는 자연 스러운 F#-연결 라이브러리 (다음 섹션을 참조 F#-연결 라이브러리). 모든 구현을 사용 하 여를 작성 하는 고차 메서드 바닐라.NET 라이브러리를 개발 하는 경우 일반적인 구현 전략 것 결과적으로, F# 형식 함수를 만든 다음 대리자를 사용 하 여 실제 F#구현입니다.

#### <a name="use-the-trygetvalue-pattern-instead-of-returning-f-option-values-and-prefer-method-overloading-to-taking-f-option-values-as-arguments"></a>TryGetValue 패턴을 사용 하 여 반환 하는 대신 F# 값, 옵션 및 메서드 기록에 오버 로드 하는 것이 좋습니다. F# 값을 인수로 옵션

사용에 대 한 일반적인 패턴을 F# api에서 옵션 유형을 좋음 바닐라에 구현 된 표준.NET을 사용 하 여.NET Api 디자인 기술을 합니다. 반환 하는 대신는 F# 옵션 값, bool 반환 형식 및 패턴을 "TryGetValue"와 같이 out 매개 변수를 사용 하는 것이 좋습니다. 및 수행 하는 대신 F# 옵션 값을 매개 변수로, 메서드 오버 로드 또는 선택적 인수를 사용 하는 것이 좋습니다.

```fsharp
member this.ReturnOption() = Some 3

member this.ReturnBoolAndOut(outVal: byref<int>) =
    outVal <- 3
    true

member this.ParamOption(x: int, y: int option) =
    match y with
    | Some y2 -> x + y2
    | None -> x

member this.ParamOverload(x: int) = x

member this.ParamOverload(x: int, y: int) = x + y
```

#### <a name="use-the-net-collection-interface-types-ienumerablet-and-idictionarykeyvalue-for-parameters-and-return-values"></a>.NET 컬렉션 인터페이스를 사용 하 여 형식을 IEnumerable\<T\> 및 IDictionary\<키, 값\> 매개 변수 및 반환 값

.NET 배열과 같은 구체적 컬렉션 형식의 사용 하지 않도록 `T[]`, F# 형식 `list<T>`, `Map<Key,Value>` 및 `Set<T>`, 및.NET 구체적 컬렉션 형식은 같은 `Dictionary<Key,Value>`. .NET 라이브러리 디자인 지침과 같은 다양 한 컬렉션 형식을 사용 하는 경우에 대 한 적절 한 조언을 `IEnumerable<T>`입니다. 배열의 일부 사용 (`T[]`) 성능 기준에 일부 경우에 적합 합니다. 특히 유의 `seq<T>` 는 F# 별칭 `IEnumerable<T>`, 이므로 seq 종종는 바닐라.NET API에 대 한 적절 한 형식입니다.

대신 F# 를 나열 합니다.

```fsharp
member this.PrintNames(names: string list) =
    ...
```

사용 하 여 F# 시퀀스:

```fsharp
member this.PrintNames(names: seq<string>) =
    ...
```

#### <a name="use-the-unit-type-as-the-only-input-type-of-a-method-to-define-a-zero-argument-method-or-as-the-only-return-type-to-define-a-void-returning-method"></a>메서드의 유일한 입력된 형식으로 단위 유형을 사용 하 여 0 인수 메서드를 정의 또는 유일한으로 void 반환 메서드를 정의 하는 형식 반환

단위 형식의 다른 사용 하지 마세요. 다음은 좋은입니다.

```fsharp
✔ member this.NoArguments() = 3

✔ member this.ReturnVoid(x: int) = ()
```

이 잘못 되었습니다.

```fsharp
member this.WrongUnit( x: unit, z: int) = ((), ())
```

#### <a name="check-for-null-values-on-vanilla-net-api-boundaries"></a>바닐라.NET API 경계에 null 값에 대 한 확인

F#구현 코드를 변경할 수 없는 디자인 패턴 및 사용에 대 한 null 리터럴의 제한으로 인해 더 적은 수의 null 값이 있고 경향이 F# 형식입니다. 다른.NET 언어 종종 null 값으로 훨씬 더 자주 사용 합니다. 이 인해 F# 는 바닐라.NET API를 노출 하는 코드에서 API 경계에서 null에 대 한 매개 변수를 확인 하 고에 대 한 자세한 흐름에서 이러한 값을 방지 해야 합니다 F# 구현 코드. 합니다 `isNull` 함수나에 패턴 일치는 `null` 패턴을 사용할 수 있습니다.

```fsharp
let checkNonNull argName (arg: obj) =
    match arg with
    | null -> nullArg argName
    | _ -> ()

let checkNonNull` argName (arg: obj) =
    if isNull arg then nullArg argName
    else ()
```

#### <a name="avoid-using-tuples-as-return-values"></a>튜플 반환 값으로 사용 하지 마십시오

대신 데이터를 집계를 보유 하 고 있거나 out 매개 변수를 사용 하 여 여러 값을 반환 하는 명명 된 형식을 반환 하는 것이 좋습니다. 튜플과 구조체.net에서 있어도 (구조체 튜플에 대 한 C# 언어 지원 포함)는 가장 자주 제공 하지는 이상적인 및 예상 되는 API를.NET 개발자 용.

#### <a name="avoid-the-use-of-currying-of-parameters"></a>매개 변수 (currying)를 사용 하지 않도록

대신,.NET 호출 규칙을 사용 하 여 `Method(arg1,arg2,…,argN)`입니다.

```fsharp
member this.TupledArguments(str, num) = String.replicate num str
```

팁: 모든.NET 언어에서 사용 하기 위한 라이브러리 디자인할 경우 몇 가지 실험적 맬웨어에 실제로 작업을 수행 하는 C# 및 Visual Basic 프로그래밍 "느낌 오른쪽" 이러한 언어에서 라이브러리 되도록 합니다. 또한 라이브러리 및 해당 설명서 개발자에 게 예상 대로 표시 되는지 확인 하려면 Visual Studio 개체 브라우저 및.NET Reflector와 같은 도구를 사용할 수 있습니다.

## <a name="appendix"></a>부록

### <a name="end-to-end-example-of-designing-f-code-for-use-by-other-net-languages"></a>디자인의 종단 간 예제 F# 다른.NET 언어 사용에 대 한 코드

다음 클래스를 고려 합니다.

```fsharp
open System

type Point1(angle,radius) =
    new() = Point1(angle=0.0, radius=0.0)
    member x.Angle = angle
    member x.Radius = radius
    member x.Stretch(l) = Point1(angle=x.Angle, radius=x.Radius * l)
    member x.Warp(f) = Point1(angle=f(x.Angle), radius=x.Radius)
    static member Circle(n) =
        [ for i in 1..n -> Point1(angle=2.0*Math.PI/float(n), radius=1.0) ]
```

유추 된 F# 형식의이 클래스는 다음과 같습니다.

```fsharp
type Point1 =
    new : unit -> Point1
    new : angle:double * radius:double -> Point1
    static member Circle : n:int -> Point1 list
    member Stretch : l:double -> Point1
    member Warp : f:(double -> double) -> Point1
    member Angle : double
    member Radius : double
```

하는 방법에 살펴보겠습니다이 F# 형식이 다른.NET 언어를 사용 하 여 프로그래머에 나타납니다. 예를 들어, 대략적인 C# "서명"는 다음과 같습니다.

```csharp
// C# signature for the unadjusted Point1 class
public class Point1
{
    public Point1();

    public Point1(double angle, double radius);

    public static Microsoft.FSharp.Collections.List<Point1> Circle(int count);

    public Point1 Stretch(double factor);

    public Point1 Warp(Microsoft.FSharp.Core.FastFunc<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

확인 방법에 대 한 중요 한 요소가 몇 가지 F# 나타냅니다 여기 생성 합니다. 예를 들어:

* 인수 이름 같은 메타 데이터 유지 되었습니다.

* F#될 두 개의 인수를 사용 하는 메서드와 C# 메서드를 두 개의 인수를 사용 합니다.

* 함수 및 목록에서 해당 형식에 대 한 참조 되는 F# 라이브러리입니다.

다음 코드에는 이러한 작업을 고려해 야 하는이 코드를 조정 하는 방법을 보여 줍니다.

```fsharp
namespace SuperDuperFSharpLibrary.Types

type RadialPoint(angle:double, radius:double) =

    /// Return a point at the origin
    new() = RadialPoint(angle=0.0, radius=0.0)

    /// The angle to the point, from the x-axis
    member x.Angle = angle

    /// The distance to the point, from the origin
    member x.Radius = radius

    /// Return a new point, with radius multiplied by the given factor
    member x.Stretch(factor) =
        RadialPoint(angle=angle, radius=radius * factor)

    /// Return a new point, with angle transformed by the function
    member x.Warp(transform:Func<_,_>) =
        RadialPoint(angle=transform.Invoke angle, radius=radius)

    /// Return a sequence of points describing an approximate circle using
    /// the given count of points
    static member Circle(count) =
        seq { for i in 1..count ->
                RadialPoint(angle=2.0*Math.PI/float(count), radius=1.0) }
```

유추 된 F# 코드의 종류는 다음과 같습니다.

```fsharp
type RadialPoint =
    new : unit -> RadialPoint
    new : angle:double * radius:double -> RadialPoint
    static member Circle : count:int -> seq<RadialPoint>
    member Stretch : factor:double -> RadialPoint
    member Warp : transform:System.Func<double,double> -> RadialPoint
    member Angle : double
    member Radius : double
```

C# 시그니처는 이제 다음과 같습니다.

```csharp
public class RadialPoint
{
    public RadialPoint();

    public RadialPoint(double angle, double radius);

    public static System.Collections.Generic.IEnumerable<RadialPoint> Circle(int count);

    public RadialPoint Stretch(double factor);

    public RadialPoint Warp(System.Func<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

바닐라.NET 라이브러리의 일부는 다음과 같이이 형식을 사용 하 여 준비를 수정 합니다.

* 여러 개의 이름을 조정: `Point1`, `n`, `l`, 및 `f` 되었습니다 `RadialPoint`를 `count`를 `factor`, 및 `transform`, 각각.

* 반환 형식을 사용한 `seq<RadialPoint>` 대신 `RadialPoint list` 사용 하 여 목록 생성을 변경 하 여 `[ ... ]` 사용 하 여 시퀀스 생성 `IEnumerable<RadialPoint>`합니다.

* .NET 대리자 형식을 사용한 `System.Func` 대신는 F# 함수 유형입니다.

따라서 C# 코드에서 사용 하기 훨씬 편리한 있습니다.
