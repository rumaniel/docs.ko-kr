---
title: C# 7.0의 새로운 기능 - C# 가이드
description: C# 언어 버전 7.0의 새로운 기능을 살펴봅니다.
ms.date: 02/20/2019
ms.assetid: fd41596d-d0c2-4816-b94d-c4d00a5d0243
ms.openlocfilehash: 0f26a9647503ebb667d961fefaa05a25a71ec6f5
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926568"
---
# <a name="whats-new-in-c-70"></a>C# 7.0의 새로운 기능

C# 7.0에서는 C# 언어에 많은 새로운 기능을 추가합니다.

- [`out` 변수](#out-variables)
  - `out` 값을 사용되는 메서드에 대한 인수로 인라인으로 선언할 수 있습니다.
- [튜플](#tuples)
  - 여러 public 필드가 포함된 간단한 명명되지 않은 형식을 만들 수 있습니다. 컴파일러 및 IDE 도구는 이러한 형식의 의미 체계를 이해합니다.
- [삭제](#discards)
  - 삭제는 할당된 값에 신경 쓰지 않을 때 할당에서 사용되는 임시 쓰기 전용 변수입니다. 매개 변수는 `out` 매개 변수를 사용하여 메서드를 호출할 때뿐만 아니라 튜플 및 사용자 정의 형식을 분해할 때 특히 유용합니다.
- [패턴 일치](#pattern-matching)
  - 임의 형식 및 해당 형식의 멤버 값에 따라 분기 논리를 만들 수 있습니다.
- [`ref` local 및 return](#ref-locals-and-returns)
  - 메서드 지역 변수와 반환 값은 다른 스토리지에 대한 참조일 수 있습니다.
- [로컬 함수](#local-functions)
  - 함수를 다른 함수 내부에 중첩하여 범위와 표시 여부를 제한할 수 있습니다.
- [추가 식 본문 멤버](#more-expression-bodied-members)
  - 식을 사용하여 작성할 수 있는 멤버 목록이 증가했습니다.
- [`throw` 식](#throw-expressions)
  - `throw` 문이었기 때문에 이전에 허용되지 않은 코드 구문에서 예외를 throw할 수 있습니다.
- [일반화된 비동기 반환 형식](#generalized-async-return-types)
  - `async` 한정자를 사용하여 선언된 메서드는 `Task` 및 `Task<T>` 외에 다른 형식을 반환할 수 있습니다.
- [숫자 리터럴 구문 개선 사항](#numeric-literal-syntax-improvements)
  - 새로운 토큰으로 숫자 상수의 가독성이 향상됩니다.

이 문서의 나머지 부분에서는 해당 기능에 대한 개요를 제공합니다. 각 기능의 배경과 원리를 알아봅니다. 구문을 알아봅니다. `dotnet try` 글로벌 도구를 사용하여 환경에서 다음과 같은 기능을 탐색할 수 있습니다.

1. [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) 글로벌 도구를 설치합니다.
1. [dotnet/try-samples](https://github.com/dotnet/try-samples) 리포지토리를 복제합니다.
1. 현재 디렉터리를 *try-samples* 리포지토리의 *csharp7* 하위 디렉터리로 설정합니다.
1. `dotnet try`를 실행합니다.

## <a name="out-variables"></a>`out` 변수

`out` 매개 변수를 지원하는 기존 구문이 이 버전에서 개선되었습니다. 이제 개별 선언 문을 작성하는 대신 메서드 호출의 인수 목록에서 `out` 변수를 선언할 수 있습니다.

[!code-csharp[OutVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVariableDeclarations "Out variable declarations")]

위에 나와 있는 대로 쉽게 구별할 수 있도록 `out` 변수의 형식을 지정할 수 있습니다. 그러나 이 언어는 암시적 형식 지역 변수를 지원하지 않습니다.

[!code-csharp[OutVarVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVarVariableDeclarations "Implicitly typed Out variable")]

- 코드를 읽기가 더 쉽습니다.
  - 위의 다른 줄이 아니라 사용하는 위치에서 out 변수를 선언합니다.
- 초기 값을 할당할 필요가 없습니다.
  - 메서드 호출에서 사용되는 위치에 `out` 변수를 선언하여 변수가 할당되기 전에 실수로 사용할 수 없습니다.

## <a name="tuples"></a>튜플

C#에서는 디자인 의도를 설명하는 데 사용되는 클래스 및 구조체에 대한 다양한 구문을 제공합니다. 하지만 다양한 구문에는 이점이 거의 없는데 추가 작업이 필요한 경우가 있습니다. 일반적으로 두 개 이상의 데이터 요소가 포함된 간단한 구조체가 필요한 메서드를 작성할 수 있습니다. 이러한 시나리오를 지원하기 위해 *튜플*이 C#에 추가되었습니다. 튜플은 데이터 멤버를 나타내는 여러 필드가 포함된 간단한 데이터 구조입니다.
필드는 유효성이 검사되지 않고 자체 메서드를 정의할 수 없습니다.

> [!NOTE]
> 튜플은 C# 7.0 이전부터 사용할 수 있었지만 비효율적이었고 언어 지원이 없었습니다.
> 즉, 튜플 요소는 `Item1`, `Item2` 등으로만 참조될 수 있었습니다. C# 7.0은 새롭고 보다 효율적인 튜플 유형을 사용하여 튜플의 필드에 대해 의미론적 이름을 사용할 수 있는 튜플에 대한 언어 지원을 소개합니다.

각 멤버에 값을 할당하고 필요에 따라 튜플의 각 멤버에 의미 체계 이름을 입력하여 튜플을 만들 수 있습니다.

[!code-csharp[NamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#NamedTuple "Named tuple")]

`namedLetters` 튜플에는 `Alpha` 및 `Beta`라는 필드가 포함됩니다. 이러한 이름은 컴파일 시간에만 존재하며 런타임 시 리플렉션을 통해 튜플을 검사하는 경우 보존되지 않습니다.

튜플 할당에서 할당의 오른쪽에 필드의 이름을 지정할 수도 있습니다.

[!code-csharp[ImplicitNamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#ImplicitNamedTuple "Implicitly named tuple")]

메서드에서 반환된 튜플의 멤버를 패키지 해제하려는 경우가 있을 수 있습니다.  이 작업을 수행하려면 튜플에서 각 값에 대한 개별 변수를 선언합니다. 이 패키지 해제 작업을 튜플 *분해*라고 합니다.

[!code-csharp[CallingWithDeconstructor](~/samples/snippets/csharp/new-in-7/program.cs#CallingWithDeconstructor "Deconstructing a tuple")]

.NET에 있는 형식에 대한 비슷한 분해를 제공할 수도 있습니다. `Deconstruct` 메서드를 클래스의 멤버로 작성합니다. 해당 `Deconstruct` 메서드는 추출하려는 각 속성에 대한 `out` 인수 집합을 제공합니다. `X` 및 `Y` 좌표를 추출하는 분해자 메서드를 제공하는 이 `Point` 클래스를 살펴봅니다.

[!code-csharp[PointWithDeconstruction](~/samples/snippets/csharp/new-in-7/point.cs#PointWithDeconstruction "Point with deconstruction method")]

튜플에 `Point`을 할당하여 개별 필드를 추출할 수 있습니다.

[!code-csharp[DeconstructPoint](~/samples/snippets/csharp/new-in-7/program.cs#DeconstructPoint "Deconstruct a point")]

[튜플 문서](../tuples.md)에서 튜플에 대해 자세히 알아볼 수 있습니다.

## <a name="discards"></a>버림

종종 튜플을 분해하거나 `out` 매개 변수로 메서드를 호출할 때 값을 신경 쓰지 않고 사용하지 않을 변수를 정의해야 합니다. C#은 *버림*에 대한 지원을 추가하여 이 시나리오를 처리합니다. 무시는 이름이 `_`(밑줄 문자)인 쓰기 전용 변수입니다. 단일 변수에 버리려는 모든 값을 할당할 수 있습니다. 버림은 할당 문과 별도로 분리되는 할당되지 않은 변수와 같습니다. 코드에서 버림을 사용할 수 없습니다.

다음 시나리오에서는 버림이 지원되지 않습니다.

- 튜플이나 사용자 정의 형식을 분해할 때.
- [out](../language-reference/keywords/out-parameter-modifier.md) 매개 변수로 메서드를 호출할 때.
- [is](../language-reference/keywords/is.md) 및 [switch](../language-reference/keywords/switch.md) 문을 사용한 패턴 일치 작업에서.
- 할당 값을 버림으로 명시적으로 지정할 때 독립 실행형 식별자인 경우.

다음 예제에서는 서로 다른 2년간의 도시 데이터가 포함된 6 튜플을 반환하는 `QueryCityDataForYears` 메서드를 정의합니다. 예제의 메서드 호출은 메서드에 의해 반환된 두 개의 채우기 값에만 관련되어 있으므로 튜플을 해체할 때 튜플의 나머지 값을 버림으로 처리합니다.

[!code-csharp[Tuple-discard](~/samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

자세한 내용은 [버림](../discards.md)을 참조하세요.

## <a name="pattern-matching"></a>패턴 일치

*패턴 일치*는 개체 형식이 아닌 속성에 대한 메서드 디스패치를 구현할 수 있는 기능입니다. 개체 형식에 따른 메서드 디스패치에 이미 익숙할 수 있습니다. 개체 기반 프로그래밍에서 가상 및 재정의 메서드는 개체 형식에 따라 메서드 디스패치를 구현하기 위해 언어 구문을 제공합니다. 기본 및 파생 클래스는 서로 다른 구현을 제공합니다.
패턴 일치 식은 이 개념을 확장하므로 상속 계층 구조를 통해 관련되지 않은 형식 및 데이터 요소에서 비슷한 디스패치 패턴을 쉽게 구현할 수 있습니다.

패턴 일치는 `is` 식과 `switch` 식을 지원합니다. 각 식을 통해 개체 및 관련 속성을 검사하여 해당 개체가 검색된 패턴을 충족하는지 확인할 수 있습니다. `when` 키워드를 사용하여 패턴에 대한 추가 규칙을 지정합니다.

`is` 패턴 식은 친숙한 [`is` 연산자](../language-reference/keywords/is.md#pattern-matching-with-is)를 확장하여 해당 형식에 대한 개체를 쿼리하고 하나의 명령에서 결과를 할당합니다. 다음 코드는 변수가 `int`인지 검사하고, 그럴 경우 현재 합계에 추가합니다.

```csharp
if (input is int count)
    sum += count;
```

앞서 간단한 예제에서는 `is` 식의 개선 사항을 보여줍니다. 참조 형식뿐만 아니라 값 형식에 대해 테스트할 수 있고, 올바른 형식의 새로운 변수에 성공적인 결과를 할당할 수 있습니다.

switch 일치 식에는 이미 C# 언어의 일부인 `switch` 문에 기반을 둔 친숙한 구문이 있습니다. 업데이트된 switch 문에는 몇 가지 새로운 구문이 포함됩니다.

- `switch` 식의 관리 형식은 더 이상 정수 형식, `Enum` 형식, `string` 또는 해당 형식 중 하나에 해당하는 nullable 형식으로 제한되지 않습니다. 모든 형식을 사용할 수 있습니다.
- 각 `case` 레이블에서 `switch` 식 형식을 테스트할 수 있습니다. `is` 식과 마찬가지로 해당 형식에 새 변수를 할당할 수 있습니다.
- `when` 절을 해당 변수의 추가 테스트 조건에 추가할 수 있습니다.
- 이제 `case` 레이블의 순서가 중요합니다. 일치하는 첫 번째 분기가 실행됩니다. 다른 분기는 건너뜁니다.

다음 코드에서는 이 새로운 기능을 보여줍니다.

```csharp
public static int SumPositiveNumbers(IEnumerable<object> sequence)
{
    int sum = 0;
    foreach (var i in sequence)
    {
        switch (i)
        {
            case 0:
                break;
            case IEnumerable<int> childSequence:
            {
                foreach(var item in childSequence)
                    sum += (item > 0) ? item : 0;
                break;
            }
            case int n when n > 0:
                sum += n;
                break;
            case null:
                throw new NullReferenceException("Null found in sequence");
            default:
                throw new InvalidOperationException("Unrecognized type");
        }
    }
    return sum;
}
```

- `case 0:`은 친숙한 상수 패턴입니다.
- `case IEnumerable<int> childSequence:`는 형식 패턴입니다.
- `case int n when n > 0:`은 추가 `when` 조건을 포함한 형식 패턴입니다.
- `case null:`은 null 패턴입니다.
- `default:`는 친숙한 기본 사례입니다.

[C#의 패턴 일치](../pattern-matching.md)에서 패턴 일치에 대해 자세히 알아볼 수 있습니다.

## <a name="ref-locals-and-returns"></a>Ref local 및 return

이 기능을 통해 다른 곳에 정의된 변수에 대한 참조를 사용 및 반환하는 알고리즘이 가능해집니다. 한 가지 예는 큰 매트릭스를 사용하고 특정 특징을 가진 하나의 위치를 찾는 것입니다. 다음 메서드는 **참조**를 행렬의 해당 스토리지에 반환합니다.

[!code-csharp[FindReturningRef](~/samples/snippets/csharp/new-in-7/MatrixSearch.cs#FindReturningRef "Find returning by reference")]

다음 코드에서처럼 반환 값을 `ref`로 선언하고 행렬에서 해당 값을 수정할 수 있습니다.

[!code-csharp[AssignRefReturn](~/samples/snippets/csharp/new-in-7/Program.cs#AssignRefReturn "Assign ref return")]

C# 언어에는 `ref` 로컬 및 반환을 잘못 사용하지 않도록 방지하는 몇 가지 규칙이 있습니다.

- `ref` 키워드를 메서드 서명 및 메서드의 모든 `return` 문에 추가해야 합니다.
  - 그러면 메서드가 메서드 전체에서 참조별로 반환되도록 합니다.
- `ref return`은 값 변수 또는 `ref` 변수에 할당될 수 있습니다.
  - 호출자는 반환 값을 복사할지 여부를 제어합니다. 반환 값을 할당할 때 `ref` 한정자를 생략하면 호출자가 스토리지에 대한 참조가 아닌 값의 복사본을 요청한다는 것을 나타냅니다.
- 표준 메서드 반환 값을 `ref` 로컬 변수에 할당할 수 없습니다.
  - 이로 인해 `ref int i = sequence.Count();` 같은 문이 허용되지 않습니다.
- 메서드 실행보다 길게 수명이 연장되지 않는 변수에 `ref`를 반환할 수 없습니다.
  - 즉, 로컬 변수 또는 비슷한 범위의 변수에 참조를 반환할 수 없습니다.
- `ref` local 및 return은 비동기 메서드와 함께 사용할 수 없습니다.
  - 컴파일러는 비동기 메서드가 반환될 때 참조된 변수가 최종 값으로 설정되었는지 여부를 알 수 없습니다.

ref local 및 ref return을 추가하면 값을 복사하거나 역참조 작업을 여러 번 수행하는 경우를 방지하여 더 효율적인 알고리즘이 가능해집니다.

`ref`를 반환 값에 추가하는 것은 [소스 호환 가능 변경](version-update-considerations.md#source-compatible-changes)입니다. 기존 코드는 컴파일되지만, 참조 반환 값은 할당 시 복사됩니다. 호출자는 반환 값 스토리지를 `ref` 지역 변수로 업데이트하여 반환을 참조로 저장해야 합니다.

자세한 내용은 [ref 키워드](../language-reference/keywords/ref.md) 문서를 참조하세요.

## <a name="local-functions"></a>로컬 함수

클래스에 대한 대부분의 디자인에는 한 위치에서만 호출되는 메서드가 포함됩니다. 이러한 추가 private 메서드는 각 메서드를 작고 집중되게 유지합니다. *로컬 함수*를 사용하면 다른 메서드의 컨텍스트 내부에서 메서드를 선언할 수 있습니다. 로컬 함수를 통해 클래스 readers는 로컬 메서드가 선언된 컨텍스트에서만 호출된다는 것을 더 쉽게 알 수 있습니다.

로컬 함수는 일반적으로 공용 반복기 메서드 및 공용 비동기 메서드에 사용됩니다. 두 메서드 형식 모두 프로그래머가 예상한 것보다 늦게 오류를 보고하는 코드를 생성합니다. 반복기 메서드에서 모든 예외는 반환된 시퀀스를 열거하는 코드를 호출할 경우에만 관찰됩니다. 비동기 메서드에서 모든 예외는 반환된 `Task`가 대기 상태일 경우에만 관찰됩니다. 다음 예제에서는 로컬 함수를 사용하여 반복기 구현으로부터 매개 변수 유효성 검사를 분리하는 방법을 보여줍니다.

[!code-csharp[22_IteratorMethodLocal](~/samples/snippets/csharp/new-in-7/Iterator.cs#IteratorMethodLocal "Iterator method with local function")]

`async` 메서드에서 같은 방법을 사용하면 인수 유효성 검사에서 발생하는 예외가 비동기 작업이 시작되기 전에 throw됩니다.

[!code-csharp[TaskExample](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#TaskExample "Task returning method with local function")]

> [!NOTE]
> 로컬 함수가 지원하는 일부 디자인은 *람다 식*을 사용하여 완료할 수 있습니다. 관심 있는 사용자는 [차이점을 자세히 확인](../local-functions-vs-lambdas.md)할 수 있습니다.

## <a name="more-expression-bodied-members"></a>추가 식 본문 멤버

C# 6에서는 멤버 함수의 [식 본문 멤버](csharp-6.md#expression-bodied-function-members) 및 읽기 전용 속성을 추가했습니다. C# 7.0에서는 식으로 구현될 수 있는 허용 멤버를 확장합니다. C# 7.0에서는 *속성* 및 *인덱서*에 대한 *생성자*, *종료자* 및 `get`/`set` 접근자를 구현할 수 있습니다. 다음 코드는 각각에 대한 예제를 보여 줍니다.

[!code-csharp[ExpressionBodiedMembers](~/samples/snippets/csharp/new-in-7/expressionmembers.cs#ExpressionBodiedEverything "new expression-bodied members")]

> [!NOTE]
> 이 예제에는 종료자가 필요하지 않지만 구문을 보여 주기 위해 표시됩니다. 관리되지 않는 리소스를 릴리스해야 하는 경우가 아니면 클래스에서 종료자를 구현하면 안 됩니다. 관리되지 않는 리소스를 직접 관리하지 않고 <xref:System.Runtime.InteropServices.SafeHandle> 클래스를 사용하는 것도 고려해야 합니다.

식 본문 멤버의 새 위치는 C# 언어의 중요한 마일스톤을 나타냅니다. 이러한 기능은 오픈 소스 [Roslyn](https://github.com/dotnet/Roslyn) 프로젝트에서 작업하는 커뮤니티 멤버에 의해 구현되었습니다.

메서드를 식 본문 멤버로 변경하는 것은 [이진 호환 가능 변경](version-update-considerations.md#binary-compatible-changes)입니다.

## <a name="throw-expressions"></a>Throw 식

C#에서 `throw`는 항상 문이었습니다. `throw`는 식이 아닌 명령문이므로 이 명령문을 사용할 수 없는 C# 구문이 있었습니다. 이러한 구문에는 조건식, null 병합 식 및 몇몇 람다 식이 포함되었습니다. 식 본문 멤버가 추가됨에 따라 `throw` 식이 유용할 수 있는 추가 위치도 추가됩니다. 이러한 구문을 작성할 수 있도록 C# 7.0에서는 [*throw 식*](../language-reference/keywords/throw.md#the-throw-expression)을 추가합니다.

이렇게 추가하면 자세한 식 기반 코드를 쉽게 작성할 수 있습니다. 오류 검사를 위해 명령문을 추가할 필요는 없습니다.

## <a name="generalized-async-return-types"></a>일반화된 비동기 반환 형식

비동기 메서드에서 `Task` 개체를 반환하면 특정 경로에 성능 병목 현상이 발생할 수 있습니다. `Task`는 참조 형식이므로 이를 사용하는 것은 개체 할당을 의미합니다. `async` 한정자로 선언된 메서드가 캐시된 결과를 반환하거나 동기적으로 완료된 경우 코드의 성능이 중요한 섹션에서 추가 할당에 상당한 시간이 소요될 수 있습니다. 연속 루프에서 이러한 할당이 발생하면 부담이 될 수 있습니다.

새로운 언어 기능을 통해 비동기 메서드 반환 형식이 `Task`, `Task<T>` 및 `void`에 제한되지 않게 되었습니다. 반환된 형식은 비동기 패턴을 충족해야 합니다. 즉, `GetAwaiter` 메서드에 액세스할 수 있어야 합니다. 한 가지 구체적인 예로 이 새로운 언어 기능을 사용할 수 있도록 `ValueTask` 형식이 .NET Framework에 추가되었습니다.

[!code-csharp[UsingValueTask](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#UsingValueTask "Using ValueTask")]

> [!NOTE]
> <xref:System.Threading.Tasks.ValueTask%601> 형식을 사용하려면 NuGet 패키지 [`System.Threading.Tasks.Extensions`](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/)를 추가해야 합니다.

이 개선 사항은 라이브러리 작성자가 성능이 중요한 코드에서 `Task`를 할당하지 않도록 방지하는 데 유용합니다.

## <a name="numeric-literal-syntax-improvements"></a>숫자 리터럴 구문 개선 사항

숫자 상수를 잘못 읽으면 코드를 처음 읽을 때 이해하기가 더 어려울 수 있습니다. 비트 마스크 또는 다른 기호 값은 잘못 이해하기 쉽습니다. C# 7.0에는 의도한 용도에 맞게 가장 읽기 쉬운 방식으로 숫자를 작성할 수 있는 *이진 리터럴* 및 *숫자 구분 기호*라는 두 가지 새로운 기능이 포함됩니다.

비트 마스크를 만들 때 또는 숫자의 이진 표현이 가장 읽기 쉬운 코드를 만들 때마다 해당 숫자를 이진으로 작성하세요.

[!code-csharp[ThousandSeparators](~/samples/snippets/csharp/new-in-7/Program.cs#ThousandSeparators "Thousands separators")]

상수의 시작 부분에 있는 `0b`는 숫자가 이진 숫자로 작성되었음을 나타냅니다. 이진 숫자는 길어질 수 있으므로 위의 이진 상수에 표시된 대로 `_`을 숫자 구분 기호로 추가하면 비트 패턴을 더 쉽게 확인할 수 있습니다. 숫자 구분 기호는 상수 내의 어디에나 나타날 수 있습니다. 기본 10개 숫자의 경우 일반적으로 숫자 구분 기호가 천 단위 구분 기호로 사용됩니다.

[!code-csharp[LargeIntegers](~/samples/snippets/csharp/new-in-7/Program.cs#LargeIntegers "Large integer")]

숫자 구분 기호는 `decimal`, `float` 및 `double` 형식에서도 사용할 수 있습니다.

[!code-csharp[OtherConstants](~/samples/snippets/csharp/new-in-7/Program.cs#OtherConstants "non-integral constants")]

함께 사용하면 숫자 상수를 훨씬 더 읽기 쉽게 선언할 수 있습니다.
