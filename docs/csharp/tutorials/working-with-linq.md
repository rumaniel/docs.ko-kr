---
title: LINQ 작업
description: 이 자습서에서는 LINQ를 사용하여 시퀀스를 생성하고, LINQ 쿼리에서 사용할 메서드를 작성하고, 즉시 계산 및 지연 계산 간을 구분하는 방법을 알아봅니다.
ms.date: 10/29/2018
ms.assetid: 0db12548-82cb-4903-ac88-13103d70aa77
ms.openlocfilehash: 72bb7475fc6b18650e0870bf99c4b8ddbac3ec9f
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926611"
---
# <a name="working-with-linq"></a>LINQ 작업

## <a name="introduction"></a>소개

이 자습서에서는 .NET Core 및 C# 언어의 기능에 대해 설명합니다. 다음을 배울 수 있습니다.

- LINQ를 사용하여 시퀀스를 생성하는 방법
- LINQ 쿼리에서 쉽게 사용할 수 있는 메서드를 작성하는 방법
- 즉시 계산 및 지연 계산을 구분하는 방법

모든 마술사들이 기본적으로 익히는 기술 중 하나인 [파로 셔플](https://en.wikipedia.org/wiki/Faro_shuffle)을 보여 주는 애플리케이션을 빌드하여 이러한 기술을 살펴봅니다. 간단히 말해서 파로 셔플은 카드 데크를 정확히 절반으로 분할한 다음 각 절반의 각 카드를 교차로 섞어 원래 데크 순서로 다시 빌드하는 기술입니다.

마술사들은 카드를 섞은 후에 모든 카드가 알려진 위치로 들어가고 순서가 반복 패턴을 가지게 되므로 이 기술을 사용합니다.

이 자습서에서는 데이터 시퀀스 조작 과정을 간단하게 살펴봅니다. 빌드할 애플리케이션은 카드 데크를 생성하고 섞은 다음 매번 섞는 시퀀스를 작성합니다. 또한 업데이트된 순서를 원래 순서와 비교할 것입니다.

이 자습서는 여러 단계로 구성됩니다. 각 단계 후에 애플리케이션을 실행하고 진행 상황을 확인할 수 있습니다. [완료된 샘플](https://github.com/dotnet/samples/blob/master/csharp/getting-started/console-linq)은 GitHub의 dotnet/samples 리포지토리에서도 확인할 수 있습니다. 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

## <a name="prerequisites"></a>전제 조건

.NET Core를 실행하도록 컴퓨터에 설정해야 합니다. [.NET Core 다운로드](https://dotnet.microsoft.com/download) 페이지에서 설치 지침을 확인할 수 있습니다. Windows, Ubuntu Linux, OS X 또는 Docker 컨테이너에서 이 애플리케이션을 실행할 수 있습니다. 선호하는 코드 편집기를 설치해야 합니다. 아래 설명에서는 오픈 소스 플랫폼 간 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용합니다. 그러나 익숙한 어떤 도구도 사용 가능합니다.

## <a name="create-the-application"></a>애플리케이션 만들기

첫 번째 단계에서는 새 애플리케이션을 만듭니다. 명령 프롬프트를 열고 애플리케이션에 대한 새 디렉터리를 만듭니다. 해당 디렉터리를 현재 디렉터리로 지정합니다. 명령 프롬프트에 명령 `dotnet new console`을 입력합니다. 이렇게 하면 기본 "Hello World" 애플리케이션에 대한 시작 파일이 만들어집니다.

이전에 C#을 사용해본 적이 없으면 [이 자습서](console-teleprompter.md)에서 C# 프로그램의 구조를 확인하세요. 해당 부분을 읽고 여기로 돌아와 LINQ에 대해 자세히 알아볼 수 있습니다.

## <a name="creating-the-data-set"></a>데이터 집합 만들기

시작하기 전에 `dotnet new console`에서 생성된 `Program.cs` 파일의 맨 위에 다음 줄이 있는지 확인합니다.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using System.Linq;
```

이러한 세 줄(`using` 문)이 파일 맨 위에 없으면 프로그램이 컴파일되지 않습니다.

이제 필요한 참조가 모두 있으므로 카드 데크의 구성 요소를 고려합니다. 일반적으로 플레잉 카드 데크에는 네 개의 짝패가 있으며, 각 짝패에 13개의 값이 있습니다. 일반적으로 즉시 `Card` 클래스를 만들고 `Card` 개체 컬렉션을 수동으로 채우는 것을 고려할 수 있습니다. LINQ를 사용하면 일반적인 방법보다 더 간결하게 카드 데크 생성을 처리할 수 있습니다. `Card` 클래스를 만드는 대신, 각각 짝패와 순위를 나타내는 두 개의 시퀀스를 만들 수 있습니다. 순위와 짝패를 <xref:System.Collections.Generic.IEnumerable%601> 문자열로 생성하는 간단한 [*반복기 메서드*](../iterators.md#enumeration-sources-with-iterator-methods) 쌍을 만듭니다.

```csharp
// Program.cs
// The Main() method

static IEnumerable<string> Suits()
{
    yield return "clubs";
    yield return "diamonds";
    yield return "hearts";
    yield return "spades";
}

static IEnumerable<string> Ranks()
{
    yield return "two";
    yield return "three";
    yield return "four";
    yield return "five";
    yield return "six";
    yield return "seven";
    yield return "eight";
    yield return "nine";
    yield return "ten";
    yield return "jack";
    yield return "queen";
    yield return "king";
    yield return "ace";
}
```

이 코드를 `Program.cs` 파일의 `Main` 메서드 아래에 배치합니다. 이러한 두 메서드는 `yield return` 구문을 활용하여 실행 시 시퀀스를 생성합니다. 컴파일러는 <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 개체를 빌드하고 요청 시 문자열 시퀀스를 생성합니다.

이제 이러한 반복기 메서드를 사용하여 카드 데크를 만듭니다. LINQ 쿼리를 `Main` 메서드에 배치합니다. 다음과 같이 표시됩니다.

```csharp
// Program.cs
static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    // Display each card that we've generated and placed in startingDeck in the console
    foreach (var card in startingDeck)
    {
        Console.WriteLine(card);
    }
}
```

여러 `from` 절이 <xref:System.Linq.Enumerable.SelectMany%2A>를 생성합니다. 그러면 첫 번째 시퀀스의 각 요소를 두 번째 시퀀스의 각 요소와 조합하는 단일 시퀀스가 만들어집니다. 이 순서는 현재 목적에 따라 매우 중요합니다. 첫 번째 소스 시퀀스(Suites)의 첫 번째 요소는 두 번째 시퀀스(Ranks)의 모든 요소와 조합됩니다. 그 결과 첫 번째 세트의 13개 카드가 생성됩니다. 이 프로세스는 첫 번째 시퀀스(Suites)의 각 요소에 대해 반복됩니다. 최종 결과는 카드 데크를 세트별로 정렬한 후 다시 값별로 정렬한 상태입니다.

위에서 사용한 쿼리 구문에 LINQ를 작성할지, 아니면 메서드 구문을 대신 사용할지에 따라 항상 하나의 구문 형식에서 다른 구문 형식으로 전환할 수 있다는 것을 명심하세요. 쿼리 구문으로 작성된 위 쿼리는 다음과 같이 메서드 구문으로 작성할 수 있습니다.

```csharp
var startingDeck = Suits().SelectMany(suit => Ranks().Select(rank => new { Suit = suit, Rank = rank }));
```

컴파일러는 쿼리 구문으로 작성된 LINQ 문을 동등한 메서드 호출 구문으로 변환합니다. 따라서 선택한 구문과 관계없이 두 버전의 쿼리가 동일한 결과를 생성합니다. 사용자의 상황에 가장 적합한 구문을 선택합니다. 예를 들어 일부 멤버가 메서드 구문을 사용하는 데 어려움을 겪고 있는 팀에서는 쿼리 구문을 사용하는 것이 좋습니다.

계속해서 지금 빌드한 샘플을 실행합니다. 데크에 있는 52개의 모든 카드가 표시됩니다. 디버거에서 이 샘플을 실행하면 `Suits()` 및 `Ranks()` 메서드가 실행되는 방식을 확인할 수 있어서 매우 유용하다는 것을 알게 될 것입니다. 각 시퀀스의 각 문자열이 필요할 때만 생성된다는 것도 명확히 알 수 있습니다.

![52개의 카드를 작성하는 앱을 표시하는 콘솔 창](./media/working-with-linq/console-52-card-application.png)

## <a name="manipulating-the-order"></a>순서 조작

다음으로, 데크의 카드 순서를 섞는 메서드를 중심으로 살펴보겠습니다. 좋은 순서 섞기의 첫 번째 단계는 데크를 두 개로 분할하는 것입니다. LINQ API에 속하는 <xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A> 메서드가 이 기능을 제공합니다. `foreach` 루프 아래에 카드를 배치합니다.

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    // 52 cards in a deck, so 52 / 2 = 26
    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
}
```

하지만 표준 라이브러리에는 이용할 수 있는 순서 섞기 메서드가 없으므로 고유한 메서드를 작성해야 합니다. 만들려는 순서 섞기 메서드는 LINQ 기반 프로그램에서 사용할 여러 기술을 보여 주므로 단계에서 이 프로세스의 각 부분을 설명하겠습니다.

LINQ 쿼리에서 반환되는 <xref:System.Collections.Generic.IEnumerable%601>을 조작하는 방법에 몇 가지 기능을 추가하려면 [확장 메서드](../programming-guide/classes-and-structs/extension-methods.md)라는 특수한 종류의 메서드를 작성해야 합니다. 간단히 말해, 확장 메서드는 기능을 추가하려는 원래 형식을 수정하지 않고 기존 형식에 새로운 기능을 추가하는 특별한 용도의 *정적 메서드*입니다.

`Extensions.cs`라는 프로그램에 새 ‘정적’ 클래스 파일을 추가하여 확장 메서드에 새로운 홈을 제공한 다음, 첫 번째 확장 메서드 빌드를 시작합니다. 

```csharp
// Extensions.cs
using System;
using System.Collections.Generic;
using System.Linq;

namespace LinqFaroShuffle
{
    public static class Extensions
    {
        public static IEnumerable<T> InterleaveSequenceWith<T>(this IEnumerable<T> first, IEnumerable<T> second)
        {
            // Your implementation will go here soon enough
        }
    }
}
```

메서드 시그니처, 특히 매개 변수를 잠시 살펴봅니다.

```csharp
public static IEnumerable<T> InterleaveSequenceWith<T> (this IEnumerable<T> first, IEnumerable<T> second)
```

이 메서드에 첫 번째 인수에 대한 `this` 한정자가 추가되는 것을 볼 수 있습니다. 즉, 마치 첫 번째 인수 형식의 멤버 메서드인 것처럼 이 메서드를 호출합니다. 또한 이 메서드 선언은 입력 및 출력 형식이 `IEnumerable<T>`인 표준 관용구를 따릅니다. 이러한 방식에서는 LINQ 메서드가 서로 사슬처럼 연결되어 좀 더 복잡한 쿼리를 수행할 수 있도록 합니다.

데크를 절반씩 분할했으므로 이러한 절반을 조인해야 합니다. 코드에서는 이 작업을 위해 <xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A>을 통해 얻은 두 시퀀스를 동시에 모두 열거하고 요소를 *`interleaving`* 한 다음, 이제 순서가 섞인 카드 데크인 하나의 시퀀스를 만듭니다. 두 시퀀스에 작동하는 LINQ 메서드를 작성하려면 <xref:System.Collections.Generic.IEnumerable%601> 작동 방식을 이해해야 합니다.

<xref:System.Collections.Generic.IEnumerable%601> 인터페이스는 한 가지 메서드인 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>를 포함합니다. <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>에서 반환된 개체에는 다음 요소로 이동하기 위한 메서드와 시퀀스의 현재 요소를 검색하는 속성이 있습니다. 이러한 두 멤버를 사용하여 컬렉션을 열거하고 요소를 반환합니다. 이 Interleave 메서드는 반복기 메서드이므로, 컬렉션을 빌드하고 반환하는 대신, 위에 표시된 `yield return` 구문을 사용합니다.

해당 메서드의 구현은 다음과 같습니다.

[!CODE-csharp[InterleaveSequenceWith](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet1)]

이 메서드를 작성했으므로 `Main` 메서드로 돌아가 데크 순서를 한 번 섞습니다.

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
    var shuffle = top.InterleaveSequenceWith(bottom);

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }
}
```

## <a name="comparisons"></a>비교

데크가 원래 순서로 돌아가는 데 몇 번을 섞어야 할까요? 알아내려면 두 시퀀스가 서로 같은지 확인하는 메서드를 작성해야 합니다. 이 메서드를 만든 후에는 데크 순서를 섞는 코드를 루프에 배치하고 데크가 원래 순서로 돌아갈 때를 확인해야 합니다.

두 시퀀스가 서로 같은지를 확인하는 메서드를 작성하는 작업은 간단합니다. 데크를 섞기 위해 작성한 메서드와 비슷한 구조를 갖습니다. 그렇지만 이번에는 각 요소를 `yield return`하는 대신, 각 시퀀스의 일치하는 요소를 비교합니다. 전체 시퀀스가 열거된 경우 모든 요소가 일치하면 시퀀스도 같습니다.

[!CODE-csharp[SequenceEquals](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet2)]

다음에서는 두 번째 LINQ 관용구인 터미널 메서드를 보여 줍니다. 여기서는 시퀀스를 입력으로 사용하고(또는 이 경우 두 개의 시퀀스) 단일 스칼라 값을 반환합니다. 터미널 메서드를 사용하는 경우, 항상 LINQ 쿼리의 메서드 체인에서 최종 메서드이므로 이름이 “터미널”입니다.

이 메서드를 사용하여 데크가 원래 순서로 돌아갈 때를 확인하면 작동 방식을 확인할 수 있습니다. 순서 섞기 코드를 루프 내에 포함하고, `SequenceEquals()` 메서드를 적용하여 시퀀스가 원래 순서가 될 때 중지합니다. 이 메서드는 시퀀스 대신 단일 값을 반환하므로 어떤 쿼리에서든지 항상 마지막 메서드로 사용되는 것을 확인할 수 있습니다.

```csharp
// Program.cs
static void Main(string[] args)
{
    // Query for building the deck

    // Shuffling using InterleaveSequenceWith<T>();

    var times = 0;
    // We can re-use the shuffle variable from earlier, or you can make a new one
    shuffle = startingDeck;
    do
    {
        shuffle = shuffle.Take(26).InterleaveSequenceWith(shuffle.Skip(26));

        foreach (var card in shuffle)
        {
            Console.WriteLine(card);
        }
        Console.WriteLine();
        times++;

    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

지금까지 작성한 코드를 실행하고 순서를 섞을 때마다 데크가 어떻게 다시 배열되는지 확인합니다. 8번 순서 섞기(do-while 루프 반복) 후에 데크는 시작하는 LINQ 쿼리에서 처음 만들었을 때 데크의 원래 구성으로 돌아갑니다.

## <a name="optimizations"></a>최적화

지금까지 빌드한 샘플은 ‘외부 순서 섞기’를 실행합니다. 즉, 맨 위 및 맨 아래 카드가 실행할 때마다 항상 같은 위치에 있습니다.  한 가지 부분을 변경하겠습니다. 52장 카드의 위치가 모두 변경되는 ‘내부 순서 섞기’를 대신 사용하겠습니다.  내부 순서 섞기의 경우 반으로 나눈 아래쪽 부분의 첫 번째 카드가 데크의 첫 번째 카드가 되도록 데크를 인터리빙합니다. 즉, 반으로 나눈 위쪽 부분의 마지막 카드가 맨 아래 카드가 됩니다. 이는 단일 코드 줄에 대한 간단한 변경입니다. <xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A>의 위치를 전환하여 현재 순서 섞기 쿼리를 업데이트합니다. 이렇게 하면 데크의 위쪽 절반과 아래쪽 절반의 순서가 바뀝니다.

```csharp
shuffle = shuffle.Skip(26).InterleaveSequenceWith(shuffle.Take(26));
```

프로그램을 다시 실행합니다. 그러면 데크가 자체적으로 순서를 변경하는 데 52회 반복된다는 것을 알 수 있습니다. 또한 프로그램이 계속 실행될 때 몇 가지 심각한 성능 저하를 알 수 있습니다.

그 이유로는 여러 가지가 있습니다. 이 성능 저하의 주요 원인 중 하나인 비효율적인 [‘지연 계산’](../programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md) 사용을 해결할 수 있습니다. 

간단히 말해, 지연 계산은 해당 값이 필요할 때까지 문이 계산되지 않음을 나타냅니다. LINQ 쿼리는 지연 계산되는 문입니다. 요소가 요청될 때만 시퀀스가 생성됩니다. 일반적으로 이것이 LINQ의 큰 장점입니다. 그러나 이러한 프로그램에서 사용하면 실행 시간이 기하급수적으로 늘어납니다.

LINQ 쿼리를 사용하여 원래 데크를 생성했습니다. 각 순서 섞기는 이전 데크에 대해 세 개의 LINQ 쿼리를 수행하여 생성됩니다. 이러한 모든 쿼리는 느리게 수행됩니다. 즉, 시퀀스가 요청될 때마다 다시 수행됩니다. 52번째 반복에 도달할 때까지 원래 데크를 아주 여러 번 다시 생성하게 됩니다. 이 동작을 보여 주기 위해 로그를 작성해 보겠습니다. 그런 후에 문제를 해결해 보겠습니다.

`Extensions.cs` 파일에서 아래 메서드를 입력하거나 복사합니다. 이 확장 메서드는 프로젝트 디렉터리에 `debug.log`라는 새 파일을 만들고 현재 실행 중인 쿼리를 로그 파일에 기록합니다. 이 확장 메서드를 임의 쿼리에 추가하여 해당 쿼리가 실행되었음을 표시할 수 있습니다.

[!CODE-csharp[LogQuery](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet3)]

`File` 아래에 빨간색 물결이 나타나면 존재하지 않는다는 것을 의미합니다. 컴파일러가 `File`을 인식하지 못하기 때문에 컴파일되지 않습니다. 이 문제를 해결하려면 `Extensions.cs`의 첫 번째 줄 아래에 다음 코드 줄을 추가해야 합니다.

```csharp
using System.IO;
```

이렇게 하면 문제가 해결되고 빨간색 오류가 사라집니다.

그런 후 로그 메시지를 사용하여 각 쿼리의 정의를 계측합니다.

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                        from r in Ranks().LogQuery("Rank Generation")
                        select new { Suit = s, Rank = r }).LogQuery("Starting Deck");

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    Console.WriteLine();
    var times = 0;
    var shuffle = startingDeck;

    do
    {
        // Out shuffle
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26)
            .LogQuery("Bottom Half"))
            .LogQuery("Shuffle");
        */

        // In shuffle
        shuffle = shuffle.Skip(26).LogQuery("Bottom Half")
                .InterleaveSequenceWith(shuffle.Take(26).LogQuery("Top Half"))
                .LogQuery("Shuffle");

        foreach (var c in shuffle)
        {
            Console.WriteLine(c);
        }

        times++;
        Console.WriteLine(times);
    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

쿼리에 액세스할 때마다 로깅하지는 않고, 원래 쿼리를 만들 때만 로깅합니다. 프로그램을 실행하는 데 여전히 오래 걸리지만 이제 이유를 확인할 수 있습니다. 로깅을 켠 상태로 내부 순서 섞기를 실행하다가 지치면 외부 순서 섞기로 다시 전환합니다. 여전히 지연 계산 효과가 나타날 것입니다. 한 번 실행에서 모든 값 및 세트 생성을 비롯한 2592개의 쿼리가 실행됩니다.

여기서 코드 성능을 개선하여 수행하는 실행 횟수를 줄일 수 있습니다. 간단한 해결 방법은 카드 데크를 구성하는 원래 LINQ 쿼리의 결과를 ‘캐시’하는 것입니다.  현재, do-while 루프가 반복될 때마다 쿼리를 계속해서 다시 실행하고 카드 데크를 다시 구성하며 매번 순서를 변경합니다. 카드 데크를 캐시하려면 LINQ 메서드 <xref:System.Linq.Enumerable.ToArray%2A> 및 <xref:System.Linq.Enumerable.ToList%2A>를 활용합니다. 두 메서드를 쿼리에 추가하면 지정된 대로 동일한 작업을 수행하지만, 이제 호출하도록 선택한 메서드에 따라 배열이나 목록에 결과를 저장합니다. LINQ 메서드 <xref:System.Linq.Enumerable.ToArray%2A>를 두 쿼리에 모두 추가하고 프로그램을 다시 실행합니다.

[!CODE-csharp[Main](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet1)]

이제 외부 순서 섞기가 30개 쿼리로 줄었습니다. 내부 순서 섞기로 다시 실행해도 비슷하게 개선된 것을 확인할 수 있습니다. 이제 162개 쿼리가 실행됩니다.

이 예제는 지연 계산이 성능 문제를 일으킬 수 있는 사용 사례를 중점적으로 나타내도록 **작성**되었습니다. 지연 계산이 코드 성능에 영향을 줄 수 있는 위치를 확인하는 것만큼이나 모든 쿼리를 즉시 실행해야 하는 것은 아님을 이해하는 것도 중요합니다. <xref:System.Linq.Enumerable.ToArray%2A>를 사용하지 않을 경우 발생하는 성능 저하는 카드 데크의 새로운 배열이 각각 이전 배열에서 빌드되기 때문입니다. 지연 계산을 사용한다는 것은 각 새 데크 구성이 원래 데크에서 빌드되며, 심지어 `startingDeck`를 빌드한 코드를 실행하는 것을 의미합니다. 이로 인해 많은 양의 추가 작업이 발생합니다.

실제로 즉시 계산을 사용할 때 잘 실행되는 알고리즘도 있고, 지연 계산을 사용할 때 잘 실행되는 알고리즘도 있습니다. 일상적인 사용에서 지연 계산은 대체로 데이터베이스 엔진과 같이 데이터 소스가 별도 프로세스일 때 사용하는 것이 더 좋습니다. 데이터베이스의 경우 지연 계산을 통해 더 복잡한 쿼리에서 데이터베이스 프로세스로 하나의 왕복만 실행하고 나머지 코드 부분으로 돌아갈 수 있습니다. LINQ에서는 지연 계산을 실행할지, 아니면 즉시 계산을 실행할지를 유연하게 선택할 수 있으므로 프로세스를 측정하여 최상의 성능을 제공하는 계산 종류를 선택합니다.

## <a name="conclusion"></a>결론

이 프로젝트에서는 다음 내용을 설명했습니다.

- LINQ 쿼리를 사용하여 데이터를 의미 있는 시퀀스로 집계
- 고유한 사용자 지정 기능을 LINQ 쿼리에 추가하는 확장 메서드 작성
- LINQ 쿼리에서 성능 저하와 같은 성능 문제가 발생할 수 있는 코드 영역 찾기
- LINQ 쿼리와 관련된 지연 및 즉시 계산과 쿼리 성능에 미치는 영향

LINQ 외에도 마법사가 카드 속임수에 사용하는 기술에 대해 약간 알아보았습니다. 마술사는 데크에서 모든 카드가 이동하는 위치를 제어할 수 있으므로 파로 순서 섞기 기술을 사용합니다. 이제 기술을 알고 있으니, 다른 모든 사용자를 위해 망치지 마세요.

LINQ에 대한 자세한 내용은 다음을 참조하세요.

- [LINQ(Language-Integrated Query)](../programming-guide/concepts/linq/index.md)
  - [LINQ 소개](../programming-guide/concepts/linq/index.md)
  - [기본 LINQ 쿼리 작업(C#)](../programming-guide/concepts/linq/basic-linq-query-operations.md)
  - [LINQ를 통한 데이터 변환(C#)](../programming-guide/concepts/linq/data-transformations-with-linq.md)
  - [LINQ의 쿼리 구문 및 메서드 구문(C#)](../programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)
  - [LINQ를 지원하는 C# 기능](../programming-guide/concepts/linq/features-that-support-linq.md)
