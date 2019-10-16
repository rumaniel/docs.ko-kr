---
title: C# 6의 새로운 기능 - C# 가이드
description: C# 버전 6의 새로운 기능을 알아봅니다.
ms.date: 12/12/2018
ms.openlocfilehash: da40b4c9d4af0094fdd907c542e971ba55086e0f
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971377"
---
# <a name="whats-new-in-c-6"></a>C# 6의 새로운 기능

C#의 6.0 릴리스에는 개발자의 생산성을 개선하는 많은 기능이 추가되었습니다. 이러한 기능의 전반적인 영향은 더 읽기 쉬운 더 간결한 코드를 작성한다는 것입니다. 많은 일반적인 사례에 대한 더 적은 의례가 구문에 포함됩니다. 더 적은 의례로 디자인 의도를 더 쉽게 파악할 수 있습니다. 이러한 기능을 자세히 알아보세요. 생산성을 높이고 더 가독성이 높은 코드를 작성할 수 있을 것입니다. 언어의 구문보다 기능에 더 집중할 수 있습니다.

이 문서의 나머지 부분에서는 이러한 각 기능을 간략히 설명하고 이러한 기능을 살펴볼 수 있는 링크를 제공합니다. 또한 자습서 섹션의 [C# 6에 대한 대화형 살펴보기](../tutorials/exploration/csharp-6.yml)에서 기능을 살펴볼 수도 있습니다.

## <a name="read-only-auto-properties"></a>읽기 전용 auto 속성

*읽기 전용 auto 속성*은 변경할 수 없는 형식을 만드는 더 간결한 구문을 제공합니다. get 접근자만 사용하여 auto 속성을 선언합니다.

[!code-csharp[ReadOnlyAutoProperty](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoProperty)]

`FirstName` 및 `LastName` 속성은 동일한 클래스의 생성자 본문에서만 설정할 수 있습니다.

[!code-csharp[ReadOnlyAutoPropertyConstructor](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoPropertyConstructor)]

다른 메서드에서 `LastName`을 설정하려고 하면 `CS0200` 컴파일 오류가 생성됩니다.

```csharp
public class Student
{
    public string LastName { get;  }

    public void ChangeName(string newLastName)
    {
        // Generates CS0200: Property or indexer cannot be assigned to -- it is read only
        LastName = newLastName;
    }
}
```

이 기능은 변경할 수 없는 형식을 만들기 위한 실제 언어 지원을 구현하고, 더 간결하고 편리한 auto 속성 구문을 사용합니다.

이 구문을 추가해도 액세스 가능 메서드가 제거되지 않으면 [이진 호환 가능 변경](version-update-considerations.md#binary-compatible-changes)입니다.

## <a name="auto-property-initializers"></a>Auto 속성 이니셜라이저

‘Auto 속성 이니셜라이저’를 통해 속성 선언의 일부로 auto 속성의 초기 값을 선언할 수 있습니다. 

[!code-csharp[Initialization](../../../samples/snippets/csharp/new-in-6/newcode.cs#Initialization)]

`Grades` 멤버는 선언된 위치에서 초기화됩니다. 따라서 더 쉽게 정확히 한 번 초기화를 수행할 수 있습니다. 초기화가 속성 선언의 일부이므로 `Student` 개체에 대한 public 인터페이스를 통해 스토리지를 균등하게 할당하기 쉽습니다.

## <a name="expression-bodied-function-members"></a>식 본문 함수 멤버

개발자가 작성하는 많은 멤버는 단일 식이 될 수 있는 단일 명령문입니다. 대신 식 본문 멤버를 작성하세요. 이 내용은 메서드 및 읽기 전용 속성에 적용됩니다. 예를 들어 `ToString()`의 재정의가 좋은 예입니다.

[!code-csharp[ToStringExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#ToStringExpressionMember)]

또한 읽기 전용 속성에 이 구문을 사용할 수 있습니다.

[!code-csharp[FullNameExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

기존 멤버를 식 본문 멤버로 변경하는 것은 [이진 호환 가능 변경](version-update-considerations.md#binary-compatible-changes)입니다.

## <a name="using-static"></a>using static

*using static* 향상된 기능을 사용하여 단일 클래스의 정적 메서드를 가져올 수 있습니다. 사용 중인 클래스를 지정합니다.

[!code-csharp[UsingStaticMath](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStaticMath)]

<xref:System.Math>에는 인스턴스 메서드가 포함되어 있지 않습니다. `using static`을 사용하여 정적 및 인스턴스 메서드가 둘 다 포함된 클래스에 대한 클래스의 정적 메서드를 가져올 수도 있습니다. 가장 유용한 예 중 하나는 <xref:System.String>입니다.

[!code-csharp[UsingStatic](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStatic)]

> [!NOTE]
> static using 문에서는 정규화된 클래스 이름 `System.String`을 사용해야 합니다.  대신 `string` 키워드를 사용할 수 없습니다.

`static using` 문에서 가져온 확장 메서드는 확장 메서드 호출 구문을 사용하여 호출될 때만 범위 내에 있습니다. 정적 메서드로 호출될 때는 범위 내에 있지 않습니다. 일반적으로 LINQ 쿼리에서 이를 확인할 수 있습니다. <xref:System.Linq.Enumerable> 또는 <xref:System.Linq.Queryable>을 가져와 LINQ 패턴을 가져올 수 있습니다.

[!code-csharp[UsingStaticLinq](../../../samples/snippets/csharp/new-in-6/newcode.cs#usingStaticLinq)]

일반적으로 확장 메서드는 확장 메서드 호출 식을 사용하여 호출합니다. 정적 메서드 호출 구문을 사용하여 호출하는 경우는 드물지만 이 경우 클래스 이름을 추가하면 모호함이 해소됩니다.

`static using` 지시문은 모든 중첩 형식도 가져옵니다. 한정 없이 중첩 형식을 참조할 수 있습니다.

## <a name="null-conditional-operators"></a>Null 조건 연산자

*null 조건 연산자*를 사용하면 null 확인이 훨씬 더 쉽고 유연합니다. 멤버 액세스 `.`를 `?.`로 바꾸세요.

[!code-csharp[NullConditional](../../../samples/snippets/csharp/new-in-6/program.cs#NullConditional)]

이전 예제에서 person 개체가 `null`인 경우 `first` 변수에 `null`이 할당됩니다. 그렇지 않은 경우 `FirstName` 속성의 값이 할당됩니다. 가장 중요한 점은 `?.`는 `person` 변수가 `null`일 경우 이 코드 줄이 `NullReferenceException`을 생성하지 않음을 의미한다는 것입니다. 대신 이 코드 줄은 단락되고 `null`을 반환합니다. 또한 배열 또는 인덱서 액세스에 null 조건 연산자를 사용할 수도 있습니다. 인덱스 식에서 `[]`를 `?[]`로 바꾸세요.

다음 식은 `person` 값에 관계없이 `string`을 반환합니다. 이 구문을 *null 결합* 연산자와 함께 사용하여 속성 중 하나가 `null`일 경우 기본값을 할당합니다. 식이 단락되면 반환된 `null` 값은 전체 식과 일치하도록 형식화됩니다.

[!code-csharp[NullCoalescing](../../../samples/snippets/csharp/new-in-6/program.cs#NullCoalescing)]

또한 `?.`를 사용하여 메서드를 조건부로 호출할 수도 있습니다. null 조건 연산자와 함께 멤버 함수를 사용하는 가장 일반적인 경우는 `null`일 수 있는 대리자(또는 이벤트 처리기)를 안전하게 호출하는 것입니다.  `?.` 연산자를 통해 대리자의 `Invoke` 메서드를 호출하여 멤버에 액세스합니다. [대리자 패턴](../delegates-patterns.md#handling-null-delegates) 문서에서 예제를 볼 수 있습니다.

`?.` 연산자 규칙을 적용하면 연산자의 왼쪽이 한 번만 계산됩니다. 이렇게 하면 이벤트 처리기 사용 예제를 비롯한 많은 관용구를 구현할 수 있습니다.

```csharp
// preferred in C# 6:
this.SomethingHappened?.Invoke(this, eventArgs);
```

또한 왼쪽이 한 번만 계산되도록 하면 `?.` 왼쪽에서 메서드 호출을 포함한 모든 식을 사용할 수 있습니다.

## <a name="string-interpolation"></a>문자열 보간

C# 6에서는 새 [문자열 보간](../language-reference/tokens/interpolated.md) 기능을 통해 문자열에 식을 포함할 수 있습니다. 문자열 앞에 `$`를 추가하고 `{` 및 `}` 사이에 서수 대신 식을 사용하기만 하면 됩니다.

[!code-csharp[stringInterpolation](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

이 예제에서는 대체 식에 속성을 사용합니다. 모든 식을 사용할 수 있습니다. 예를 들어 보간의 일부로 학생의 성적 점수 평균을 계산할 수 있습니다.

[!code-csharp[stringInterpolationFormat](../../../samples/snippets/csharp/new-in-6/newcode.cs#stringInterpolationFormat)]

이전 코드 줄은 소수 자릿수가 두 개인 부동 소수점 숫자로 `Grades.Average()` 값의 형식을 지정합니다.

일반적으로 특정 문화권을 사용하여 생성된 문자열의 서식을 지정해야 할 수 있습니다. 문자열 보간에 의해 생성된 개체가 암시적으로 <xref:System.FormattableString?displayProperty=nameWithType>으로 변환될 수 있다는 사실을 참고하세요. <xref:System.FormattableString> 인스턴스에는 복합 형식 문자열 및 문자열로 변환하기 전에 식을 계산한 결과가 포함됩니다. 문자열 형식을 지정할 때 <xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> 메서드를 사용하여 문화권을 지정합니다. 다음 예에서는 독일(de-DE) 문화권을 사용하여 문자열을 생성합니다. (기본적으로 독일 문화권은 ',' 문자를 소수 구분 기호로 사용하고 '.' 문자를 천 단위 구분 기호로 사용합니다.)

```csharp
FormattableString str = $"Average grade is {s.Grades.Average()}";
var gradeStr = str.ToString(new System.Globalization.CultureInfo("de-DE"));
```

문자열 보간을 시작하려면 [C#의 문자열 보간](../tutorials/exploration/interpolated-strings.yml) 대화형 자습서, [문자열 보간](../language-reference/tokens/interpolated.md) 문서 및 [C#의 문자열 보간](../tutorials/string-interpolation.md) 자습서를 참조하세요.

## <a name="exception-filters"></a>예외 필터

*예외 필터*는 지정된 catch 절을 적용해야 하는 경우를 결정하는 절입니다. 예외 필터에 사용된 식이 `true`로 계산되면 catch 절은 예외에 대한 일반적인 처리를 수행합니다. 식이 `false`로 계산되면 `catch` 절을 건너뜁니다. 한 가지 사용 예는 예외에 대한 정보를 검사하여 `catch` 절이 예외를 처리할 수 있는지 결정하는 것입니다.

[!code-csharp[ExceptionFilter](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#ExceptionFilter)]

## <a name="the-nameof-expression"></a>`nameof` 식

[nameof](../language-reference/operators/nameof.md) 식은 기호 이름으로 계산됩니다. 변수, 속성 또는 멤버 필드의 이름이 필요할 때마다 도구를 작동하는 것이 좋습니다. `nameof`의 가장 일반적인 사용 예 중 하나는 예외를 일으킨 기호의 이름을 제공하는 것입니다.

[!code-csharp[nameof](../../../samples/snippets/csharp/new-in-6/NewCode.cs#UsingStaticString)]

또 다른 사용 예는 `INotifyPropertyChanged` 인터페이스를 구현하는 XAML 기반 애플리케이션에서 사용하는 것입니다.

[!code-csharp[nameofNotify](../../../samples/snippets/csharp/new-in-6/viewmodel.cs#nameofNotify)]

## <a name="await-in-catch-and-finally-blocks"></a>Catch 및 Finally 블록의 Await

C# 5에는 `await` 식을 배치할 수 있는 위치에 대한 여러 제한 사항이 있었습니다. 이제 C# 6에서는 `catch` 또는 `finally` 식에서 `await`를 사용할 수 있습니다. 이 방법이 로깅 시나리오에서 가장 일반적을 사용됩니다.

[!code-csharp[AwaitFinally](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#AwaitFinally)]

`catch` 및 `finally` 절 내부에 `await` 지원을 추가하기 위한 구현 세부 정보에 따라 동작이 동기 코드에 대한 동작과 일치합니다. `catch` 또는 `finally` 절에서 실행되는 코드가 throw되면 실행은 다음 바깥쪽 블록에서 적합한 `catch` 절을 검색합니다. 현재 예외가 있는 경우 해당 예외가 손실됩니다. `catch` 및 `finally` 절에서 대기된 식에서도 같은 작업이 수행됩니다. 적합한 `catch`가 검색되고 현재 예외(있는 경우)가 손실됩니다.  

> [!NOTE]
> 이 동작 때문에 새 예외가 추가되지 않도록 `catch` 및 `finally` 절을 신중하게 작성하는 것이 좋습니다.

## <a name="initialize-associative-collections-using-indexers"></a>인덱서를 사용하여 연결 컬렉션 초기화

*인덱스 이니셜라이저*는 컬렉션 이니셜라이저를 인덱스 사용과 더 일관되도록 하는 두 가지 기능 중 하나입니다. C#의 이전 릴리스에서는 키 및 값 쌍을 중괄호로 묶어 <xref:System.Collections.Generic.Dictionary%602>를 포함하여 시퀀스 스타일 컬렉션에서 *컬렉션 이니셜라이저*를 사용할 수 있습니다.

[!code-csharp[ListInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#CollectionInitializer)]

<xref:System.Collections.Generic.Dictionary%602> 컬렉션 및 액세스 가능한 `Add` 메서드가 둘 이상의 인수를 허용하는 다른 형식에서 이를 사용할 수 있습니다. 새로운 구문은 컬렉션에 인덱스를 사용하여 할당을 지원합니다.

[!code-csharp[DictionaryInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#DictionaryInitializer)]

이 기능은 여러 버전에 대한 시퀀스 컨테이너를 대신한 것과 비슷한 구문을 사용하여 연관 컨테이너를 초기화할 수 있음을 의미합니다.

## <a name="extension-add-methods-in-collection-initializers"></a>컬렉션 이니셜라이저의 확장 `Add` 메서드

컬렉션을 더 쉽게 초기화하도록 하는 또 다른 기능은 `Add` 메서드에 *확장 메서드*를 사용하는 기능입니다. 이 기능은 Visual Basic의 패리티를 위해 추가되었습니다. 이 기능은 의미상으로 새 항목을 추가하기 위해 다른 이름을 가진 메서드가 포함된 사용자 지정 컬렉션 클래스가 있는 경우 가장 유용합니다.

## <a name="improved-overload-resolution"></a>향상된 오버로드 확인

이 마지막 기능은 알지 못하는 기능일 수 있습니다. C# 컴파일러의 이전 버전에서 람다 식을 포함하는 일부 메서드 호출이 모호한 것으로 확인될 수 있는 구문이 있었습니다. 이 메서드를 살펴봅니다.

[!code-csharp[AsyncMethod](../../../samples/snippets/csharp/new-in-6/overloads.cs#AsyncMethod)]

C#의 이전 버전에서는 메서드 그룹 구문을 통한 해당 메서드 호출이 실패합니다.

[!code-csharp[MethodGroup](../../../samples/snippets/csharp/new-in-6/overloads.cs#MethodGroup)]

이전 컴파일러에서는 `Task.Run(Action)` 및 `Task.Run(Func<Task>())`를 제대로 구분할 수 없습니다. 이전 버전에서는 람다 식을 인수로 사용해야 했습니다.

[!code-csharp[Lambda](../../../samples/snippets/csharp/new-in-6/overloads.cs#Lambda)]

C# 6 컴파일러에서는 `Task.Run(Func<Task>())`가 더 나은 선택인지 제대로 결정합니다.

### <a name="deterministic-compiler-output"></a>deterministic 컴파일러 출력

`-deterministic` 옵션은 컴파일러가 동일한 원본 파일의 연속적인 컴파일을 위해 바이트 단위의 동일한 출력 어셈블리를 생성하도록 지시합니다.

기본적으로 컴파일이 실행될 때마다 고유한 출력이 생성됩니다. 컴파일러는 임의의 숫자에서 생성된 GUID와 타임스탬프를 추가합니다. 바이트별 출력을 비교하여 빌드 간 일관성을 유지하려면 이 옵션을 사용합니다.

자세한 내용은 [-deterministic 컴파일러 옵션](../language-reference/compiler-options/deterministic-compiler-option.md) 문서를 참조하세요.
