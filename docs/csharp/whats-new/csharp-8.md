---
title: C# 8.0의 새로운 기능 - C# 가이드
description: C# 8.0의 새로운 기능을 살펴봅니다.
ms.date: 09/20/2019
ms.openlocfilehash: 6b5602db6ee61b1d9db4c906d6a14ea2f918ad0a
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275775"
---
# <a name="whats-new-in-c-80"></a>C# 8.0의 새로운 기능

C#8.0은 다음 기능 및 향상된 기능을 C# 언어에 추가합니다.

- [읽기 전용 멤버](#readonly-members)
- [기본 인터페이스 메서드](#default-interface-methods)
- [패턴 일치 개선 사항](#more-patterns-in-more-places):
  - [Switch 식](#switch-expressions)
  - [속성 패턴](#property-patterns)
  - [튜플 패턴](#tuple-patterns)
  - [위치 패턴](#positional-patterns)
- [using 선언](#using-declarations)
- [정적 로컬 함수](#static-local-functions)
- [삭제 가능한 ref struct](#disposable-ref-structs)
- [nullable 참조 형식](#nullable-reference-types)
- [비동기 스트림](#asynchronous-streams)
- [인덱스 및 범위](#indices-and-ranges)
- [null 병합 할당](#null-coalescing-assignment)
- [관리되지 않는 생성 형식](#unmanaged-constructed-types)
- [중첩 식의 stackalloc](#stackalloc-in-nested-expressions)
- [보간된 약어 문자열의 향상된 기능](#enhancement-of-interpolated-verbatim-strings)

이 문서의 나머지 부분에서는 이러한 기능에 대해 간략하게 설명합니다. 심화 문서가 공개되면 해당 자습서에 대한 링크 및 개요가 제공됩니다. `dotnet try` 글로벌 도구를 사용하여 환경에서 다음과 같은 기능을 탐색할 수 있습니다.

1. [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) 글로벌 도구를 설치합니다.
1. [dotnet/try-samples](https://github.com/dotnet/try-samples) 리포지토리를 복제합니다.
1. 현재 디렉터리를 *try-samples* 리포지토리의 *csharp8* 하위 디렉터리로 설정합니다.
1. `dotnet try`를 실행합니다.

## <a name="readonly-members"></a>읽기 전용 멤버

구조체의 멤버에 `readonly` 한정자를 적용할 수 있습니다. 이것은 멤버가 상태를 수정하지 않음을 나타냅니다. 이것이 `readonly` 한정자를 `struct` 선언에 적용하는 것보다 더 세부적입니다.  다음과 같이 변경 가능한 구조체를 고려합니다.

```csharp
public struct Point
{
    public double X { get; set; }
    public double Y { get; set; }
    public double Distance => Math.Sqrt(X * X + Y * Y);

    public override string ToString() =>
        $"({X}, {Y}) is {Distance} from the origin";
}
```

대부분의 구조체와 마찬가지로 `ToString()` 메서드는 상태를 수정하지 않습니다. `readonly` 한정자를 `ToString()`의 선언에 추가하여 다음을 나타낼 수 있습니다.

```csharp
public readonly override string ToString() =>
    $"({X}, {Y}) is {Distance} from the origin";
```

`ToString`은 `readonly`로 표시되지 않은 `Distance` 속성에 액세스하므로 이전 변경은 컴파일러 경고를 생성합니다.

```console
warning CS8656: Call to non-readonly member 'Point.Distance.get' from a 'readonly' member results in an implicit copy of 'this'
```

컴파일러는 방어 복사본을 만들 필요가 있을 때 사용자에게 경고합니다.  `Distance` 속성은 상태를 변경하지 않으므로 `readonly` 한정자를 선언에 추가하여 이 경고를 수정할 수 있습니다.

```csharp
public readonly double Distance => Math.Sqrt(X * X + Y * Y);
```

`readonly` 한정자가 읽기 전용 속성에 필요합니다. 컴파일러는 `get` 접근자가 상태를 수정하지 않는다고 가정하지 않습니다. 명시적으로 `readonly`를 선언해야 합니다. 컴파일러는 `readonly` 멤버가 상태를 수정하지 않는다는 규칙을 적용합니다. 다음 메서드는 `readonly` 한정자를 제거하지 않는 한 컴파일하지 않습니다.

```csharp
public readonly void Translate(int xOffset, int yOffset)
{
    X += xOffset;
    Y += yOffset;
}
```

이 기능을 사용하여 디자인 의도를 지정할 수 있으므로 컴파일러는 이를 적용하고 디자인 의도에 따라 최적화를 수행할 수 있습니다.

## <a name="default-interface-methods"></a>기본 인터페이스 메서드

이제 인터페이스에 멤버를 추가하고 해당 멤버에 대 한 구현을 제공할 수 있습니다. 이 언어 기능을 사용하여 API 작성자는 소스 또는 이진과 해당 인터페이스의 기존 구현과의 호환성에 영향을 미치지 않고 후속 버전에서 인터페이스에 메서드를 추가할 수 있습니다. 기존 구현은 기본 구현을 *상속*합니다. 또한 이 기능을 사용하여 C#은 유사한 기능을 지원하는 Android 또는 Swift를 대상으로 하는 API와 상호 운용됩니다. 또한 기본 인터페이스 메서드는 “특성” 언어 기능과 유사한 시나리오를 사용하도록 설정합니다.

기본 인터페이스 메서드는 많은 시나리오와 언어 요소에 영향을 줍니다. 첫 번째 자습서에서는 [기본 구현으로 인터페이스 업데이트](../tutorials/default-interface-methods-versions.md)에 대해 다룹니다. 다른 자습서 및 참조 업데이트는 일반 릴리스 시점에 제공됩니다.

## <a name="more-patterns-in-more-places"></a>더 많은 곳에서 더 많은 패턴 사용

**패턴 일치**는 관련이 있으나 유형이 다른 데이터에서 셰이프 종속 기능을 사용할 수 있도록 지원하는 도구를 제공합니다. C# 7.0부터 [`is`](../language-reference/keywords/is.md) 식과 [`switch`](../language-reference/keywords/switch.md) 문을 사용하는 형식 패턴 및 상수 패턴을 위한 구문이 추가되었습니다. 이 기능은 데이터와 기능을 각각 별도로 구분하는 프로그래밍 패러다임을 지원하기 위한 조심스러운 첫 번째 단계입니다. 업계에서 마이크로 서비스와 기타 클라우드 기반 아키텍처를 도입하는 사례가 늘어남에 따라 다른 언어 도구에 대한 요구가 높아졌습니다.

C# 8.0은 코드의 더 많은 곳에서 더 많은 패턴 식을 사용할 수 있도록 이 용어를 확대합니다. 데이터와 기능을 각각 별도로 구분하는 경우 이러한 기능을 고려해 보시기 바랍니다. 알고리즘이 개체의 런타임 형식이 아닌 다른 요소에 종속되는 경우 패턴 일치를 고려해 보시기 바랍니다. 이러한 기법은 디자인을 표현할 추가적인 방법을 제공합니다.

C# 8.0에는 더 많은 곳에서 패턴을 사용할 수 있도록 지원하는 기능에 더해 **재귀 패턴**도 추가되었습니다. 패턴 식의 결과는 식입니다. 재귀 패턴은 다른 패턴 식의 출력에 적용된 패턴 식입니다.

### <a name="switch-expressions"></a>Switch 식

[`switch`](../language-reference/keywords/switch.md) 문의 결과 각각의 `case` 블록에서 값이 생성되는 경우가 종종 있습니다. **Switch 식**을 사용하면 더욱더 간결한 식 구문을 사용할 수 있습니다. `case` 및 `break` 키워드를 반복적으로 사용하고 중괄호를 적용해야 하는 경우가 줄어듭니다.  다음과 같이 무지개의 색을 나열하는 enum 예를 살펴보겠습니다.

```csharp
public enum Rainbow
{
    Red,
    Orange,
    Yellow,
    Green,
    Blue,
    Indigo,
    Violet
}
```

애플리케이션이 `R`, `G` 및 `B` 구성 요소에서 생성된 `RGBColor` 형식을 정의한 경우 switch 식을 포함하는 다음 메서드를 사용하여 `Rainbow` 값을 RGB 값으로 변환할 수 있습니다.

```csharp
public static RGBColor FromRainbow(Rainbow colorBand) =>
    colorBand switch
    {
        Rainbow.Red    => new RGBColor(0xFF, 0x00, 0x00),
        Rainbow.Orange => new RGBColor(0xFF, 0x7F, 0x00),
        Rainbow.Yellow => new RGBColor(0xFF, 0xFF, 0x00),
        Rainbow.Green  => new RGBColor(0x00, 0xFF, 0x00),
        Rainbow.Blue   => new RGBColor(0x00, 0x00, 0xFF),
        Rainbow.Indigo => new RGBColor(0x4B, 0x00, 0x82),
        Rainbow.Violet => new RGBColor(0x94, 0x00, 0xD3),
        _              => throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand)),
    };
```

여기에서 몇 가지 구문 개선 사항을 확인할 수 있습니다.

- 변수가 `switch` 키워드 앞에 옵니다. 이처럼 순서가 변경된 결과 switch 식과 switch 문을 눈으로 구분하기가 쉬워졌습니다.
- `case` 및 `:` 요소가 `=>`으로 대체되어 간결성과 직관성이 향상되었습니다.
- `default` 케이스가 `_` 무시 항목으로 대체되었습니다.
- 본문이 문이 아닌 식입니다.

기존의 `switch` 문을 사용하는 동일한 코드와 비교해 보세요.

```csharp
public static RGBColor FromRainbowClassic(Rainbow colorBand)
{
    switch (colorBand)
    {
        case Rainbow.Red:
            return new RGBColor(0xFF, 0x00, 0x00);
        case Rainbow.Orange:
            return new RGBColor(0xFF, 0x7F, 0x00);
        case Rainbow.Yellow:
            return new RGBColor(0xFF, 0xFF, 0x00);
        case Rainbow.Green:
            return new RGBColor(0x00, 0xFF, 0x00);
        case Rainbow.Blue:
            return new RGBColor(0x00, 0x00, 0xFF);
        case Rainbow.Indigo:
            return new RGBColor(0x4B, 0x00, 0x82);
        case Rainbow.Violet:
            return new RGBColor(0x94, 0x00, 0xD3);
        default:
            throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand));
    };
}
```

### <a name="property-patterns"></a>속성 패턴

**속성 패턴**을 사용하면 검사 대상 개체의 속성을 일치시킬 수 있습니다. 구매자의 주소를 기준으로 판매세를 계산하는 전자상거래 사이트를 예로 들어 보겠습니다. 판매세 계산은 `Address` 클래스의 주요 임무가 아닙니다. 판매세는 시간이 흐름에 따라 주소 형식이 변경되는 빈도보다 자주 변경될 가능성이 큽니다. 판매세의 금액은 주소의 `State` 속성에 종속됩니다. 다음 메서드는 속성 패턴을 사용하여 주소 및 가격으로부터 판매세를 컴퓨팅합니다.

```csharp
public static decimal ComputeSalesTax(Address location, decimal salePrice) =>
    location switch
    {
        { State: "WA" } => salePrice * 0.06M,
        { State: "MN" } => salePrice * 0.75M,
        { State: "MI" } => salePrice * 0.05M,
        // other cases removed for brevity...
        _ => 0M
    };
```

패턴 일치는 이 알고리즘을 표현하기 위한 더 간결한 구문을 만듭니다.

### <a name="tuple-patterns"></a>튜플 패턴

일부 알고리즘은 여러 입력을 사용합니다. **튜플 패턴**을 사용하면 [튜플](../tuples.md)로 표현되는 여러 값에 따라 전환할 수 있습니다.  다음 코드는 게임 ‘가위, 바위, 보’에 대한 전환 식을 보여 줍니다. 

```csharp
public static string RockPaperScissors(string first, string second)
    => (first, second) switch
    {
        ("rock", "paper") => "rock is covered by paper. Paper wins.",
        ("rock", "scissors") => "rock breaks scissors. Rock wins.",
        ("paper", "rock") => "paper covers rock. Paper wins.",
        ("paper", "scissors") => "paper is cut by scissors. Scissors wins.",
        ("scissors", "rock") => "scissors is broken by rock. Rock wins.",
        ("scissors", "paper") => "scissors cuts paper. Scissors wins.",
        (_, _) => "tie"
    };
```

메시지는 승자를 나타냅니다. 버리기 사례는 동률의 세 가지 조합 또는 기타 텍스트 입력을 나타냅니다.

### <a name="positional-patterns"></a>위치 패턴

일부 형식에는 해당 속성을 불연속 변수로 분해하는 `Deconstruct` 메서드가 포함됩니다. `Deconstruct` 메서드에 액세스할 수 있는 경우 **위치 패턴**을 사용하여 개체의 속성을 검사하고 패턴에 해당 속성을 사용할 수 있습니다.  `X` 및 `Y`의 불연속 변수를 만들려면 `Deconstruct` 메서드를 포함하는 다음 `Point` 클래스를 사용하는 것이 좋습니다.

```csharp
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);

    public void Deconstruct(out int x, out int y) =>
        (x, y) = (X, Y);
}
```

또한 사분면의 다양한 위치를 나타내는 다음 열거형을 고려하세요.

```csharp
public enum Quadrant
{
    Unknown,
    Origin,
    One,
    Two,
    Three,
    Four,
    OnBorder
}
```

다음 메서드는 **위치 패턴**을 사용하여 `x`와 `y`의 값을 추출합니다. 그런 다음, `when` 절을 사용하여 점의 `Quadrant`를 확인합니다.

```csharp
static Quadrant GetQuadrant(Point point) => point switch
{
    (0, 0) => Quadrant.Origin,
    var (x, y) when x > 0 && y > 0 => Quadrant.One,
    var (x, y) when x < 0 && y > 0 => Quadrant.Two,
    var (x, y) when x < 0 && y < 0 => Quadrant.Three,
    var (x, y) when x > 0 && y < 0 => Quadrant.Four,
    var (_, _) => Quadrant.OnBorder,
    _ => Quadrant.Unknown
};
```

이전 switch의 버리기 패턴은 `x` 또는 `y` 중 하나만 0인 경우에 일치합니다. expression 식은 항상 값을 생성하거나 예외를 throw해야 합니다. 일치하는 케이스가 없으면 switch 식이 예외를 throw합니다. switch 식이 가능한 모든 케이스를 포함하지 않으면 컴파일러에서 경고가 생성됩니다.

이 [패턴 일치에 대한 고급 자습서](../tutorials/pattern-matching.md)에서 패턴 일치 기법을 탐색할 수 있습니다.

## <a name="using-declarations"></a>using 선언

**using 선언**은 `using` 키워드 뒤에 오는 변수 선언입니다. using 선언은 선언되는 변수를 바깥쪽 범위의 끝에서 삭제하라고 컴파일러에 알립니다. 텍스트 파일을 쓰는 다음 코드를 예로 들어 보겠습니다.

```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using var file = new System.IO.StreamWriter("WriteLines2.txt");
    foreach (string line in lines)
    {
        if (!line.Contains("Second"))
        {
            file.WriteLine(line);
        }
    }
// file is disposed here
}
```

위 예에서 메서드의 닫는 중괄호에 도달하면 파일이 삭제됩니다. 이 지점이 바로 `file`이 선언된 범위의 끝입니다. 위 코드는 기존의 [using 문](../language-reference/keywords/using-statement.md) 문을 사용하는 다음 코드와 동일합니다.

```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using (var file = new System.IO.StreamWriter("WriteLines2.txt"))
    {
        foreach (string line in lines)
        {
            if (!line.Contains("Second"))
            {
                file.WriteLine(line);
            }
        }
    } // file is disposed here
}
```

위 예에서 `using` 문의 닫는 중괄호에 도달하면 파일이 삭제됩니다.

두 경우 모두 컴파일러가 `Dispose()`를 호출합니다. `using` 문의 식을 삭제할 수 없는 경우 컴파일러에서 오류를 생성합니다.

## <a name="static-local-functions"></a>정적 로컬 함수

이제 로컬 함수가 바깥쪽 범위의 변수를 참조하는 경우가 없도록 로컬 함수에 `static` 한정자를 추가할 수 있습니다. 이렇게 하면 `CS8421` "정적 로컬 함수는 \<variable>에 대한 참조를 포함할 수 없습니다."를 생성합니다. 

다음과 같은 코드를 생각해 볼 수 있습니다. 여기서 로컬 함수 `LocalFunction`은 바깥쪽 범위(메서드 `M`)에서 선언된 변수 `y`에 액세스합니다. 따라서 `LocalFunction`을 `static` 한정자와 함께 선언할 수 없습니다.

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

다음 코드에는 정적 로컬 함수가 포함되어 있습니다. 여기서 로컬 함수는 바깥쪽 범위의 변수에 액세스하지 않으므로 정적이 될 수 있습니다.

```csharp
int M()
{
    int y = 5;
    int x = 7;
    return Add(x, y);

    static int Add(int left, int right) => left + right;
}
```

## <a name="disposable-ref-structs"></a>삭제 가능한 ref struct

`ref` 한정자와 함께 선언된 `struct`는 인터페이스를 구현할 수 없으므로 <xref:System.IDisposable>을 구현할 수 없습니다. 따라서 `ref struct`가 삭제 가능해지려면 액세스 가능한 `void Dispose()` 메서드를 가져야 합니다. 이것은 `readonly ref struct` 선언에도 적용됩니다.

## <a name="nullable-reference-types"></a>nullable 참조 형식

nullable 주석 컨텍스트에서 참조 형식의 변수는 모두 **nullable이 아닌 참조 형식**으로 간주됩니다. 변수가 null이 될 수 있음을 나타내려면 형식 이름 뒤에 `?`를 추가하여 해당 변수를 **nullable 참조 형식**으로 선언해야 합니다.

nullable이 아닌 참조 형식의 경우, 로컬 변수가 선언될 때 null이 아닌 값으로 초기화되도록 컴파일러가 흐름 분석을 사용합니다. 필드는 생성 시점에 초기화되어야 합니다. 생성자(있는 경우)를 호출함으로써 또는 이니셜라이저에 의해 변수가 설정되지 않으면 컴파일러에서 경고를 생성합니다. 또한, nullable이 아닌 참조 형식은 null이 될 수 있는 값에 할당할 수 없습니다.

nullable 참조 형식은 할당되지 않았는지 또는 null로 초기화되었는지 검사되지 않습니다. 단, nullable 참조 형식의 변수가 액세스되거나 nullable이 아닌 참조 형식에 할당되기 전에 null에 대해 검사되도록 컴파일러가 흐름 분석을 사용합니다.

[nullable 참조 형식](../nullable-references.md) 개요에서 이 기능에 대해 자세히 알아볼 수 있습니다. [nullable 참조 형식 자습서](../tutorials/nullable-reference-types.md)를 활용하여 새 애플리케이션에서 직접 사용해 보세요. [migrating an application to use nullable reference types tutorial](../tutorials/upgrade-to-nullable-references.md)(nullable 참조 형식을 사용할 수 있도록 애플리케이션 마이그레이션 자습서)에서는 nullable 참조 형식을 사용할 수 있도록 기존 코드베이스를 마이그레이션하는 방법을 알아볼 수 있습니다.

## <a name="asynchronous-streams"></a>비동기 스트림

C# 8.0부터 스트림을 비동기식으로 만들고 사용할 수 있습니다. 비동기 스트림을 반환하는 메서드는 다음과 같은 세 가지 속성을 갖습니다.

1. `async` 한정자를 사용하여 선언되었습니다.
1. <xref:System.Collections.Generic.IAsyncEnumerable%601>를 반환합니다.
1. 비동기 스트림의 연속적인 요소를 반환하기 위해 메서드가 `yield return` 문을 포함합니다.

비동기 스트림을 사용하려면 스트림의 요소를 열거할 때 `foreach` 키워드 앞에 `await` 키워드를 사용해야 합니다. `await` 키워드를 추가하려면 비동기 스트림을 열거하는 메서드가 `async` 한정자와 함께 선언되어야 하며, 이 메서드가 `async` 메서드를 허용하는 형식을 반환해야 합니다. 일반적으로 이는 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 형식을 반환해야 함을 의미합니다. <xref:System.Threading.Tasks.ValueTask> 또는 <xref:System.Threading.Tasks.ValueTask%601> 형식도 가능합니다. 메서드는 비동기 스트림을 사용할 수도 있고 생성할 수 있습니다. 비동기 스트림을 생성한다는 것은 메서드가 <xref:System.Collections.Generic.IAsyncEnumerable%601>를 반환한다는 것을 의미합니다. 다음 코드는 0에서 19까지의 시퀀스를 생성합니다. 숫자가 생성되는 각 시점 사이에는 100ms의 대기 시간이 있습니다.

```csharp
public static async System.Collections.Generic.IAsyncEnumerable<int> GenerateSequence()
{
    for (int i = 0; i < 20; i++)
    {
        await Task.Delay(100);
        yield return i;
    }
}
```

`await foreach` 문을 사용하여 시퀀스를 열거합니다.

```csharp
await foreach (var number in GenerateSequence())
{
    Console.WriteLine(number);
}
```

[비동기 스트림 생성 및 사용](../tutorials/generate-consume-asynchronous-stream.md) 자습서에서 직접 비동기 스트림을 사용해 볼 수 있습니다.

## <a name="indices-and-ranges"></a>인덱스 및 범위

인덱스와 범위는 시퀀스에서 단일 요소 또는 범위에 액세스하기 위한 간결한 구문을 제공합니다.

이 언어 지원은 다음과 같은 두 가지 새 형식 및 두 가지 새 연산자를 사용합니다.

- <xref:System.Index?displayProperty=nameWithType>는 인덱스를 시퀀스로 표현합니다.
- 인덱스가 시퀀스의 끝을 기준으로 하도록 지정하는 끝부터 인덱스 연산자 `^`입니다.
- <xref:System.Range?displayProperty=nameWithType>는 시퀀스의 하위 범위를 나타냅니다.
- 범위의 시작과 끝을 피연산자로 지정하는 범위 연산자 `..`입니다.

인덱스에 대한 규칙을 사용하여 시작하겠습니다. `sequence`배열을 고려합니다. `0` 인덱스는 `sequence[0]`과 동일합니다. `^0` 인덱스는 `sequence[sequence.Length]`와 동일합니다. `sequence[^0]`은 `sequence[sequence.Length]`처럼 예외를 throw합니다. `n`이 어떤 숫자이든, 인덱스 `^n`은 `sequence.Length - n`과 동일합니다.

한 범위는 어떤 범위의 *시작* 및 *끝*을 지정합니다. 범위의 시작은 포함되지만 범위의 끝은 포함되지 않으므로, ‘시작’은 범위에 포함되고 ‘끝’은 범위에 포함되지 않습니다.   `[0..sequence.Length]`가 전체 범위를 나타내는 것처럼 `[0..^0]` 범위는 전체 범위를 나타냅니다.

몇 가지 예를 살펴보겠습니다. 다음과 같은 배열이 있습니다. 앞에서부터의 인덱스와 뒤에서부터의 인덱스가 주석으로 처리되어 있습니다.

```csharp
var words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

다음과 같이 `^1` 인덱스를 사용하여 마지막 단어를 가져올 수 있습니다.

```csharp
Console.WriteLine($"The last word is {words[^1]}");
// writes "dog"
```

다음 코드는 “quick”, “brown”, “fox”라는 단어를 포함하는 하위 범위를 만듭니다. 이 하위 범위에는 `words[1]`부터 `words[3]`까지 포함되며, `words[4]` 요소는 포함되지 않습니다.

```csharp
var quickBrownFox = words[1..4];
```

다음 코드는 “lazy”와 “dog”를 포함하는 하위 범위를 만듭니다. 이 하위 범위에는 `words[^2]`과 `words[^1]`이 포함되며. 끝 인덱스 `words[^0]`는 포함되지 않습니다.

```csharp
var lazyDog = words[^2..^0];
```

다음 예제는 시작만, 끝만, 그리고 시작과 끝이 모두 열린 범위를 만듭니다.

```csharp
var allWords = words[..]; // contains "The" through "dog".
var firstPhrase = words[..4]; // contains "The" through "fox"
var lastPhrase = words[6..]; // contains "the", "lazy" and "dog"
```

범위를 변수로 선언할 수도 있습니다.

```csharp
Range phrase = 1..4;
```

이렇게 변수로 선언된 범위는 `[` 문자와 `]` 문자 사이에 사용할 수 있습니다.

```csharp
var text = words[phrase];
```

배열만 인덱스와 범위를 지원합니다. [문자열](../language-reference/builtin-types/reference-types.md#the-string-type), <xref:System.Span%601> 또는 <xref:System.ReadOnlySpan%601>에도 인덱스 및 범위를 사용할 수 있습니다. 자세한 내용은 [인덱스 및 범위에 대한 형식 지원](../tutorials/ranges-indexes.md#type-support-for-indices-and-ranges)을 참조하세요.

인덱스와 범위에 대한 자세한 내용은 [인덱스 및 범위](../tutorials/ranges-indexes.md)에 대한 자습서에서 확인할 수 있습니다.

## <a name="null-coalescing-assignment"></a>null 병합 할당

C# 8.0에서 null 병합 할당 연산자 `??=`가 도입되었습니다. `??=` 연산자를 사용하여 왼쪽 피연산자가 `null`로 계산되는 경우에만 오른쪽 피연산자의 값을 왼쪽 피연산자에 대입할 수 있습니다.

```csharp
List<int> numbers = null;
int? i = null;

numbers ??= new List<int>();
numbers.Add(i ??= 17);
numbers.Add(i ??= 20);

Console.WriteLine(string.Join(" ", numbers));  // output: 17 17
Console.WriteLine(i);  // output: 17
```

자세한 내용은 [?? 및 ??= 연산자](../language-reference/operators/null-coalescing-operator.md) 문서를 참조하세요.

## <a name="unmanaged-constructed-types"></a>관리되지 않는 생성 형식

C# 7.3 이전 버전에서 생성 형식(하나 이상의 형식 인수를 포함하는 형식)은 [관리되지 않는 형식](../language-reference/builtin-types/unmanaged-types.md)일 수 없습니다. C# 8.0부터는 관리되지 않는 형식의 필드만 포함된 경우 생성된 값 형식이 관리되지 않습니다.

예를 들어 다음과 같은 제네릭 `Coords<T>` 형식의 정의를 살펴보겠습니다.

```csharp
public struct Coords<T>
{
    public T X;
    public T Y;
}
```

`Coords<int>` 형식은 C# 8.0 이상에서 관리되지 않는 형식입니다. 관리되지 않는 형식과 마찬가지로 이 형식의 변수에 대한 포인터를 만들거나 이 형식의 인스턴스에 대해 [스택에서 메모리 블록을 할당](../language-reference/operators/stackalloc.md)할 수 있습니다.

```csharp
Span<Coords<int>> coordinates = stackalloc[]
{
    new Coords<int> { X = 0, Y = 0 },
    new Coords<int> { X = 0, Y = 3 },
    new Coords<int> { X = 4, Y = 0 }
};
```

자세한 내용은 [관리되지 않는 형식](../language-reference/builtin-types/unmanaged-types.md)을 참조하세요.

## <a name="stackalloc-in-nested-expressions"></a>중첩 식의 stackalloc

C# 8.0부터 [stackalloc](../language-reference/operators/stackalloc.md) 식의 결과가 <xref:System.Span%601?displayProperty=nameWithType> 또는 <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> 형식이면 다른 식에서 `stackalloc` 식을 사용할 수 있습니다.

```csharp
Span<int> numbers = stackalloc[] { 1, 2, 3, 4, 5, 6 };
var ind = numbers.IndexOfAny(stackalloc[] { 2, 4, 6 ,8 });
Console.WriteLine(ind);  // output: 1
```

## <a name="enhancement-of-interpolated-verbatim-strings"></a>보간된 약어 문자열의 향상된 기능

[보간된](../language-reference/tokens/interpolated.md) 약어 문자열에서 `$` 및 `@` 토큰은 순서에 관계없이 사용할 수 있습니다. `$@"..."` 및 `@$"..."` 모두 유효한 보간된 약어 문자열입니다. 이전 C# 버전에서는 `$` 토큰이 `@` 토큰 앞에 나타나야 했습니다.
