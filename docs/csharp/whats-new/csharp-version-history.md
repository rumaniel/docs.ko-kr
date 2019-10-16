---
title: C#의 역사 - C# 가이드
description: 이 언어의 초창기 버전은 어떤 모습이었으며 이후 어떻게 변했는가?
author: erikdietrich
ms.date: 09/20/2017
ms.openlocfilehash: bce61d7a1838753f6cc2397440208e0c02b8194a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002699"
---
# <a name="the-history-of-c"></a>C\#의 역사

이 문서에서는 C# 언어의 각 주요 릴리스에 대한 기록을 제공합니다. C# 팀은 계속해서 새로운 기능을 혁신하고 추가하고 있습니다. 예정된 릴리스에서 고려되는 기능을 비롯한 자세한 언어 기능 상태는 GitHub의 [dotnet/roslyn 리포지토리에서](https://github.com/dotnet/roslyn/blob/master/docs/Language%20Feature%20Status.md) 확인할 수 있습니다.

> [!IMPORTANT]
> C # 언어는 C# 사양이 일부 기능에 대해 *표준 라이브러리*로 정의하는 형식 및 메서드를 사용합니다. .NET 플랫폼은 다양한 패키지에서 이러한 유형과 메서드를 제공합니다. 한 가지 예는 예외 처리입니다. 모든 `throw` 문 또는 식은 throw된 개체가 <xref:System.Exception>에서 파생되는지 확인합니다. 마찬가지로 모든 `catch`는 발견되는 형식이 <xref:System.Exception>에서 파생되는지 확인합니다. 각 버전은 새 요구 사항을 추가할 수 있습니다. 이전 환경에서 최신 언어 기능을 사용하려면 특정 라이브러리를 설치해야 합니다. 이러한 종속성은 각 특정 버전에 대한 페이지에서 설명합니다. 이 종속성의 배경은 [언어 및 라이브러리 간 관계](relationships-between-language-and-library.md)에서 자세히 알아볼 수 있습니다.

C# 빌드 도구는 최신 주요 언어 릴리스가 기본 언어 버전으로 고려합니다. 주요 릴리스 사이에는 이 섹션의 다른 문서에서 상세히 설명한 포인트 릴리스가 있을 수 있습니다. 포인트 릴리스에서 최신 기능을 사용하려면 [컴파일러 언어 버전을 구성](../language-reference/configure-language-version.md)하고 해당 버전을 선택해야 합니다. C# 7.0 이후 세 가지 포인트 릴리스가 있습니다.

- [C# 7.3](csharp-7-3.md):
  - C# 7.3은 [Visual Studio 2017 버전 15.7](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) 및 [.NET Core 2.1 SDK](../../core/whats-new/dotnet-core-2-1.md)부터 사용할 수 있습니다.
- [C# 7.2](csharp-7-2.md):
  - C# 7.2는 [Visual Studio 2017 버전 15.5](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) 및 [.NET Core 2.0 SDK](../../core/whats-new/dotnet-core-2-0.md)부터 사용할 수 있습니다.
- [C# 7.1](csharp-7-1.md):
  - C# 7.1은 [Visual Studio 2017 버전 15.3](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) 및 [.NET Core 2.0 SDK](../../core/whats-new/dotnet-core-2-0.md)부터 사용할 수 있습니다.

## <a name="c-version-10"></a>C# 버전 1.0

돌이켜보면 Visual Studio.Net 2002와 함께 릴리스된 C# 버전 1.0은 Java와 매우 비슷했습니다. [ECMA에 대해 명시된 설계 목표의 일부](https://feeldotneteasy.blogspot.com/2011/01/c-design-goals.html)로 "단순하고 현대적인 범용 개체 지향 언어"를 추구했습니다.  당시에 Java와 같은 형태는 이러한 초기 설계 목표를 달성한 것을 의미했습니다.

그러나 지금 다시 C# 1.0을 돌이켜보면 조금 어지러워질 것입니다. 기본 제공 비동기 기능과 당연한 것으로 여겨지는 제네릭과 관련된 멋진 기능 중 일부가 부족했습니다. 사실, 제네릭이 아예 없었습니다.  그리고 [LINQ](../linq/index.md)는 아직 사용할 수 없습니다. 그러한 추가 사항은 나올 때까지 몇 년이 걸릴 것입니다.

C# 버전 1.0은 오늘날보다 기능이 없는 편이었습니다. 좀 더 자세한 코드를 작성해야 했습니다. 하지만 출발점이 필요했습니다. C# 버전 1.0은 Windows 플랫폼에서 Java를 대체하는 실용적인 방법이었습니다.

C# 1.0의 주요 기능에는 다음이 포함되어 있습니다.

- [클래스](../programming-guide/classes-and-structs/classes.md)
- [구조체](../programming-guide/classes-and-structs/structs.md)
- [인터페이스](../programming-guide/interfaces/index.md)
- [이벤트](../events-overview.md)
- [속성](../properties.md)
- [대리자](../delegates-overview.md)
- [식](../programming-guide/statements-expressions-operators/expressions.md)
- [문](../programming-guide/statements-expressions-operators/statements.md)
- [특성](../programming-guide/concepts/attributes/index.md)

## <a name="c-version-12"></a>C# 버전 1.2

C# 버전 1.2는 Visual Studio .NET 2003과 함께 제공됩니다. 여기에는 언어에 대한 몇 가지 작은 개선이 포함되어 있습니다. 가장 주목할 만한 점은 이 버전부터 <xref:System.Collections.IEnumerator>가 <xref:System.IDisposable>를 구현할 때 <xref:System.Collections.IEnumerator>의 <xref:System.IDisposable.Dispose%2A>라는 `foreach` 루트에서 생성된 코드입니다.

## <a name="c-version-20"></a>C# 버전 2.0

이제 흥미로운 일이 시작됩니다. Visual Studio 2005와 함께 2005년에 릴리스된 C# 2.0의 몇 가지 주요 기능을 살펴보겠습니다.

- [제네릭](../programming-guide/generics/index.md)
- [부분 형식(Partial Type)](../programming-guide/classes-and-structs/partial-classes-and-methods.md#partial-classes)
- [무명 메서드](../language-reference/operators/delegate-operator.md)
- [Nullable 값 형식](../programming-guide/nullable-types/index.md)
- [반복기](../programming-guide/concepts/iterators.md)
- [공변성(Covariance) 및 반공변성(Contravariance)](../programming-guide/concepts/covariance-contravariance/index.md)

기존 기능에 추가된 기타 C# 2.0 기능은 다음과 같습니다.

- getter/setter 별도의 액세스 가능
- 메서드 그룹 변환(대리자)
- 정적 클래스
- 대리자 유추

C#은 일반적인 OO(개체 지향) 언어로 시작되었지만 C# 버전 2.0을 통해 급격히 바뀌었습니다. C#이 자리를 잡은 후 개발자들은 몇 가지 심각한 고민을 겪었습니다. 이후 대대적인 문제가 발생했습니다.

제네릭을 사용하면 형식을 안전하게 유지하면서 임의의 형식에서 형식 및 메서드를 작동할 수 있습니다. 예를 들어 <xref:System.Collections.Generic.List%601>를 사용하면 `List<string>` 또는 `List<int>`를 사용하고 이를 반복하는 동안 해당 문자열이나 정수에 형식이 안전한 작업을 수행할 수 있습니다. 제네릭을 사용하는 것은 모든 작업에서 `ArrayList`에서 파생되거나 `Object`에서 캐스팅한 `ListInt`를 만드는 것보다 좋습니다.

C# 버전 2.0에서는 반복기라는 기능이 도입되었습니다. 간단히 말해서, 반복기를 사용하면 `List`(또는 다른 열거 가능 형식)의 모든 항목을 `foreach` 루프로 검사할 수 있습니다. 반복기를 언어의 첫 번째 클래스 부분에 사용하면 언어의 가독성과 사용자의 코드 추론 능력이 크게 향상됩니다.

그리고 이때까지 C#은 Java를 따라잡으려는 노력을 계속했습니다. Java는 이미 제네릭 및 반복기가 포함된 버전을 출시했습니다. 하지만 언어가 계속 발전함에 따라 곧 변경될 것입니다.

## <a name="c-version-30"></a>C# 버전 3.0

C# 버전 3.0은 Visual Studio 2008과 함께 2007년말에 출시되었지만 언어 기능을 완전히 갖춘 버전은 .NET Framework 버전 3.5와 함께 제공됩니다. 이 버전은 C#의 성장에 큰 변화를 가져왔습니다. C#은 진정으로 강력한 프로그래밍 언어로 자리매김했습니다. 이 버전의 몇 가지 주요 특징을 살펴보겠습니다.

- [자동 구현 속성](../programming-guide/classes-and-structs/auto-implemented-properties.md)
- [무명 형식](../programming-guide/classes-and-structs/anonymous-types.md)
- [쿼리 식](../linq/query-expression-basics.md)
- [람다 식](../programming-guide/statements-expressions-operators/lambda-expressions.md)
- [식 트리](../expression-trees.md)
- [확장 메서드](../programming-guide/classes-and-structs/extension-methods.md)
- [암시적 형식 지역 변수](../language-reference/keywords/var.md)
- [부분 메서드](../language-reference/keywords/partial-method.md)
- [개체 및 컬렉션 이니셜라이저](../programming-guide/classes-and-structs/object-and-collection-initializers.md)

되돌아보면, 이러한 특징은 대부분 필연적이고 불가분한 것입니다. 이러한 모든 특징은 전략적으로 잘 맞습니다. 일반적으로 C# 버전의 핵심 기능은 LINQ(Language-Integrated Query)라고도 하는 쿼리 식이라 생각합니다.

더 미묘한 뷰는 LINQ가 생성되는 기반인 식 트리, 람다 식 및 익명 형식을 검사합니다. 하지만 두 경우 모두 C# 3.0은 혁신적인 개념을 제공합니다. C# 3.0은 C#을 하이브리드 개체 지향/기능 언어로 전환하기 위한 토대를 마련하기 시작했습니다.

특히, 이제 무엇보다도 컬렉션에 대한 작업을 수행할 수 있는 SQL 스타일의 선언적 쿼리를 작성할 수 있습니다. 정수 목록의 평균을 계산하는 `for` 루프를 작성하는 대신 이제 간단하게 `list.Average()`로 처리할 수 있습니다. 쿼리 식과 확장 메서드의 조합은 정수 목록을 훨씬 더 효율적으로 보이게 해줍니다.

실제로 개념을 파악하고 통합하는 데는 시간이 걸렸지만 점진적으로 그 개념이 완성되었습니다. 그리고 몇 년이 지난 지금, 코드는 훨씬 더 간결하고 간단하며 기능적입니다.

## <a name="c-version-40"></a>C# 버전 4.0

Visual Studio 2010과 함께 릴리스된 C# 버전 4.0은 버전 3.0의 혁신에 따른 기대에 부응하느라 어려움을 겪을 것으로 예상되었습니다. 버전 3.0에서 C#은 Java의 그림자를 확실히 벗어나 두각을 나타내었습니다. 금세 정교해졌습니다.

다음 버전에서는 몇 가지 흥미로운 새 기능이 도입되었습니다.

- [동적 바인딩](../language-reference/keywords/dynamic.md)
- [명명된/선택적 인수](../programming-guide/classes-and-structs/named-and-optional-arguments.md)
- [제네릭 공변(covariant) 및 반공변(contravariant)](../../standard/generics/covariance-and-contravariance.md)
- [포함된 interop 형식](../../framework/interop/type-equivalence-and-embedded-interop-types.md)

포함된 interop 형식은 배포의 어려움을 완화합니다. 제네릭 공변성(Covariance)과 반공변성(Contravariance)은 제네릭을 사용하는 기능을 더 많이 제공하지만, 약간 학문적이며, 프레임워크와 라이브러리 작성자에게 가장 높은 평가를 받을 것입니다. 명명되고 선택적인 매개 변수를 사용하면 많은 메서드 오버로드를 제거하고 편리성을 제공할 수 있습니다. 그러나 이러한 기능 중 어느 것도 정확히 패러다임의 변화는 아닙니다.

주요 기능은 `dynamic` 키워드였습니다. `dynamic` 키워드는 C# 버전 4.0에 컴파일 시간에 컴파일러를 재정의하는 기능을 도입했습니다. 동적 키워드를 사용하면 JavaScript와 같이 동적으로 형식화된 언어와 유사한 구조를 만들 수 있습니다. `dynamic x = "a string"`을 만든 다음, 6을 추가하여 다음에 수행해야 할 작업을 런타임에 맡길 수 있습니다.

동적 바인딩은 오류를 유발할 수 있지만 언어 내에서 훌륭한 기능도 제공합니다.

## <a name="c-version-50"></a>C# 버전 5.0

Visual Studio 2012과 함께 릴리스된 C# 버전 5.0은 언어에 중점을 둔 버전이었습니다. 해당 버전에 대한 거의 모든 노력은 다른 획기적인 언어 개념인 비동기 프로그래밍을 위한 `async` 및 `await` 모델로 옮겨 갔습니다.  다음은 주요 기능 목록입니다.

- [비동기 멤버](../async.md)
- [호출자 정보 특성](../programming-guide/concepts/caller-information.md)

### <a name="see-also"></a>참고 항목

- [코드 프로젝트: C# 5.0의 호출자 정보 특성](https://www.codeproject.com/Tips/606379/Caller-Info-Attributes-in-Csharp)

호출자 정보 특성을 사용하면 엄청난 양의 상용구 리플렉션 코드를 사용하지 않고도 실행 중인 컨텍스트에 대한 정보를 쉽게 검색할 수 있습니다. 진단 및 로깅 작업의 용도는 매우 다양합니다.

하지만 이 릴리스의 진정한 스타는 `async`과 `await`입니다. 이러한 기능이 2012년에 출시되었을 때 C#은 언어에 첫 번째 클래스 참여자로 비동기를 적용하여 다시 업계의 판도를 바꾸었습니다. 장기 실행 작업 및 콜백 웹 구현을 처리한 적이 있다면 이 언어 기능을 좋아할 것입니다.

## <a name="c-version-60"></a>C# 버전 6.0

버전 3.0과 5.0에서 C#은 개체 지향 언어의 주요 새 기능을 추가했습니다. Visual Studio 2013과 함께 릴리스된 버전 6.0은 주요 핵심 기능 대신 C# 프로그래밍을 보다 생산적으로 만드는 많은 작은 기능을 릴리스했습니다. 다음은 몇 가지 예입니다.

- [정적 가져오기](./csharp-6.md#using-static)
- [예외 필터](./csharp-6.md#exception-filters)
- [Auto 속성 이니셜라이저](./csharp-6.md#auto-property-initializers)
- [식 본문 멤버](./csharp-6.md#expression-bodied-function-members)
- [Null 전파자](./csharp-6.md#null-conditional-operators)
- [문자열 보간](./csharp-6.md#string-interpolation)
- [nameof 연산자](./csharp-6.md#the-nameof-expression)
- [인덱스 이니셜라이저](csharp-6.md#extension-add-methods-in-collection-initializers)

기타 새로운 기능은 다음과 같습니다.

- Catch/Finally 블록의 Await
- Getter 전용 속성의 기본값

이러한 각 기능은 그 자체로 흥미롭습니다. 그러나 전체적으로 살펴보면 흥미로운 패턴을 볼 수 있습니다. 이 버전에서 C#은 언어 상용구를 제거하여 코드를 더 간결하고 읽기 쉽게 만들었습니다. 따라서 깔끔하고 간단한 코드를 좋아하는 사람들에게 이 언어 버전은 큰 선물이었습니다.

이 버전에는 또 다른 변화가 있지만 본질적으로 기존 언어 기능은 아닙니다. [Roslyn 서비스형 컴파일러](https://github.com/dotnet/roslyn)가 릴리스되었습니다. C# 컴파일러는 이제 C#으로 작성되며, 프로그래밍 작업의 일부로 컴파일러를 사용할 수 있습니다.

## <a name="c-version-70"></a>C# 버전 7.0

최신 주 버전은 Visual Studio 2017과 함께 릴리스된 C# 버전 7.0입니다. 이 버전에는 C# 6.0 방식의 혁신적이고 유용한 기능이 있지만 서비스형 컴파일러는 없습니다. 다음은 새 기능 중 일부입니다.

- [외부 변수](./csharp-7.md#out-variables)
- [튜플 및 분해](./csharp-7.md#tuples)
- [패턴 일치](./csharp-7.md#pattern-matching)
- [로컬 함수](./csharp-7.md#local-functions)
- [확장된 식 본문 멤버](./csharp-7.md#more-expression-bodied-members)
- [참조 로컬 및 반환](./csharp-7.md#ref-locals-and-returns)

이러한 기능에는 다음이 포함됩니다.

- [삭제](./csharp-7.md#discards)
- [이진 리터럴 및 자릿수 구분 기호](./csharp-7.md#numeric-literal-syntax-improvements)
- [Throw 식](./csharp-7.md#throw-expressions)

이러한 모든 기능은 개발자에게 멋진 새 기능과 이전보다 훨씬 깔끔한 코드를 작성할 수 있는 기회를 제공합니다. 하이라이트는 `out` 키워드와 함께 사용할 변수의 선언을 압축하고 튜플을 통해 여러 개의 반환 값을 허용하는 것입니다.

그러나 C#은 더욱 광범위하게 사용되고 있습니다. .NET Core는 이제 모든 운영 체제를 대상으로 하며 클라우드와 휴대성에 확실히 집중하고 있습니다.  이는 새로운 기능을 제공하는 것 외에도 언어 디자이너가 많이 생각하고 시간을 투자하게 만듭니다.

_아티클_ [_NDepend 블로그에 최초로 게시됨_](https://blog.ndepend.com/c-versions-look-language-history/) _, Erik Dietrich 및 Patrick Smacchia 제공_
