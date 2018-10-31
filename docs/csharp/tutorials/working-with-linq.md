---
title: LINQ 작업
description: 이 자습서에서는 LINQ를 사용하여 시퀀스를 생성하고, LINQ 쿼리에서 사용할 메서드를 작성하고, 즉시 계산 및 지연 계산 간을 구분하는 방법을 알아봅니다.
ms.date: 03/28/2017
ms.assetid: 0db12548-82cb-4903-ac88-13103d70aa77
ms.openlocfilehash: dc5f6cc4fd38b32f54a576a3947187cbed4e70e8
ms.sourcegitcommit: 2eb5ca4956231c1a0efd34b6a9cab6153a5438af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49086754"
---
# <a name="working-with-linq"></a>LINQ 작업

## <a name="introduction"></a>소개

이 자습서에서는 .NET Core 및 C# 언어의 다양한 기능에 대해 설명합니다. 다음을 배울 수 있습니다.

*   LINQ를 사용하여 시퀀스를 생성하는 방법
*   LINQ 쿼리에서 쉽게 사용할 수 있는 메서드를 작성하는 방법
*   즉시 계산 및 지연 계산을 구분하는 방법

모든 마술사들이 기본적으로 익히는 기술 중 하나인 [파로 셔플](https://en.wikipedia.org/wiki/Faro_shuffle)을 보여 주는 응용 프로그램을 빌드하여 이러한 기술을 살펴봅니다. 간단히 말해서 파로 셔플은 카드 데크를 정확히 절반으로 분할한 다음 각 절반의 각 카드를 교차로 섞어 원래 데크 순서로 다시 빌드하는 기술입니다.

마술사들은 카드를 섞은 후에 모든 카드가 알려진 위치로 들어가고 순서가 반복 패턴을 가지게 되므로 이 기술을 사용합니다. 

이 자습서에서는 데이터 시퀀스 조작 과정을 가볍게 살펴봅니다. 빌드할 응용 프로그램은 카드 데크를 생성하고 섞은 다음 매번 섞는 시퀀스를 작성합니다. 또한 업데이트된 순서를 원래 순서와 비교할 것입니다.

이 자습서는 여러 단계로 구성됩니다. 각 단계 후에 응용 프로그램을 실행하고 진행 상황을 확인할 수 있습니다. [완료된 샘플](https://github.com/dotnet/samples/blob/master/csharp/getting-started/console-linq)은 GitHub의 dotnet/samples 리포지토리에서도 확인할 수 있습니다. 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

## <a name="prerequisites"></a>전제 조건

.NET Core를 실행하도록 컴퓨터에 설정해야 합니다. [.NET Core](https://www.microsoft.com/net/core) 페이지에서 설치 지침을 확인할 수 있습니다. Windows, Ubuntu Linux, OS X 또는 Docker 컨테이너에서 이 응용 프로그램을 실행할 수 있습니다. 선호하는 코드 편집기를 설치해야 합니다. 아래 설명에서는 오픈 소스 플랫폼 간 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용합니다. 그러나 익숙한 어떤 도구도 사용 가능합니다.

## <a name="create-the-application"></a>응용 프로그램 만들기

첫 번째 단계에서는 새 응용 프로그램을 만듭니다. 명령 프롬프트를 열고 응용 프로그램에 대한 새 디렉터리를 만듭니다. 해당 디렉터리를 현재 디렉터리로 지정합니다. 명령 프롬프트에 명령 `dotnet new console`을 입력합니다. 이렇게 하면 기본 "Hello World" 응용 프로그램에 대한 시작 파일이 만들어집니다.

이전에 C#을 사용해본 적이 없으면 [이 자습서](console-teleprompter.md)에서 C# 프로그램의 구조를 확인하세요. 해당 부분을 읽고 여기로 돌아와 LINQ에 대해 자세히 알아볼 수 있습니다. 

## <a name="creating-the-data-set"></a>데이터 집합 만들기

먼저 카드 데크를 만들어 보겠습니다. 두 개의 소스(4개 카드 세트에 대해 1개, 13개 값에 대해 1개)가 있는 LINQ 쿼리를 사용하여 이 작업을 수행합니다. 이러한 소스를 52개 카드 데크로 조합합니다. `foreach` 루프 내의 `Console.WriteLine` 문이 카드를 표시합니다.

쿼리는 다음과 같습니다.

```csharp
var startingDeck = from s in Suits()
                   from r in Ranks()
                   select new { Suit = s, Rank = r };

foreach (var c in startingDeck)
{
    Console.WriteLine(c);
}
```

여러 `from` 절이 `SelectMany`를 생성합니다. 그러면 첫 번째 시퀀스의 각 요소를 두 번째 시퀀스의 각 요소와 조합하는 단일 시퀀스가 만들어집니다. 이 순서는 현재 목적에 따라 매우 중요합니다. 첫 번째 소스 시퀀스(Suites)의 첫 번째 요소는 두 번째 시퀀스(Values)의 모든 요소와 조합됩니다. 그 결과 첫 번째 세트의 13개 카드가 생성됩니다. 이 프로세스는 첫 번째 시퀀스(Suites)의 각 요소에 대해 반복됩니다. 최종 결과는 카드 데크를 세트별로 정렬한 후 다시 값별로 정렬한 상태입니다.

다음으로 Suits() 및 Ranks() 메서드를 빌드해야 합니다. 시퀀스를 문자열 열거형으로 생성하는 정말 간단한 *반복기 메서드*부터 시작해 보겠습니다.

```csharp
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

이러한 두 메서드는 `yield return` 구문을 활용하여 실행 시 시퀀스를 생성합니다. 컴파일러는 `IEnumerable<T>`을 구현하는 개체를 빌드하고 요청 시 문자열 시퀀스를 생성합니다.

이를 컴파일하려면 파일 맨 위에 다음 두 줄을 추가해야 합니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
```

계속해서 지금 빌드한 샘플을 실행합니다. 데크에 있는 52개의 모든 카드가 표시됩니다. 디버거에서 이 샘플을 실행하면 `Suits()` 및 `Values()` 메서드가 실행되는 방식을 확인할 수 있어서 매우 유용하다는 것을 알게 될 것입니다. 각 시퀀스의 각 문자열이 필요할 때만 생성된다는 것도 명확히 알 수 있습니다.

![52개의 카드를 작성하는 앱을 표시하는 콘솔 창](./media/working-with-linq/console.png)

## <a name="manipulating-the-order"></a>순서 조작

다음에는 순서 섞기를 수행할 수 있는 유틸리티 메서드를 빌드해 보겠습니다. 첫 번째 단계는 데크를 하나로 분할하는 것입니다. LINQ API에 속하는 `Take()` 및 `Skip()` 메서드가 이 기능을 제공합니다.

```csharp
var top = startingDeck.Take(26);
var bottom = startingDeck.Skip(26);
```

순서 섞기 메서드는 표준 라이브러리에 들어 있지 않으므로 직접 작성해야 합니다. 이 새 메서드는 LINQ 기반 프로그램에서 사용하게 되는 몇 가지 기법을 보여 주므로 이 메서드의 각 부분을 단계별로 설명해 보겠습니다.

이 메서드에 대한 시그니처는 *확장 메서드*를 만듭니다.

```csharp
public static IEnumerable<T> InterleaveSequenceWith<T>
    (this IEnumerable<T> first, IEnumerable<T> second)
```

확장 메서드는 특수한 용도의 *정적 메서드*입니다. 이 메서드에 첫 번째 인수에 대한 `this` 한정자가 추가되는 것을 볼 수 있습니다. 즉, 마치 첫 번째 인수 형식의 멤버 메서드인 것처럼 이 메서드를 호출합니다.

확장 메서드는 `static` 클래스 내부에서만 선언할 수 있으므로 이 기능을 위해 `extensions`라는 새 정적 클래스를 만들어 보겠습니다. 이 자습서를 계속 진행하면서 확장 메서드를 더 추가하게 될 것이며 이러한 메서드도 같은 클래스에 포함될 것입니다.

또한 이 메서드 선언은 입력 및 출력 형식이 `IEnumerable<T>`인 표준 관용구를 따릅니다. 이러한 방식에서는 LINQ 메서드가 서로 사슬처럼 연결되어 좀 더 복잡한 쿼리를 수행할 수 있도록 합니다.

```csharp
using System.Collections.Generic;

namespace LinqFaroShuffle
{
    public static class Extensions
    {
        public static IEnumerable<T> InterleaveSequenceWith<T>
            (this IEnumerable<T> first, IEnumerable<T> second)
        {
            // implementation coming.
        }
    }
}
```

한 번에 두 시퀀스를 열거하고 요소를 인터리브하여 하나의 개체를 만들게 됩니다.  두 시퀀스에 작동하는 LINQ 메서드를 작성하려면 `IEnumerable` 작동 방식을 이해해야 합니다.

`IEnumerable` 인터페이스는 한 가지 메서드인 `GetEnumerator()`를 포함합니다. `GetEnumerator()`에서 반환된 개체에는 다음 요소로 이동하기 위한 메서드와 시퀀스의 현재 요소를 검색하는 속성이 있습니다. 이러한 두 멤버를 사용하여 컬렉션을 열거하고 요소를 반환합니다. 이 Interleave 메서드는 반복기 메서드이므로, 컬렉션을 빌드하고 반환하는 대신, 위에 표시된 `yield return` 구문을 사용합니다. 

해당 메서드의 구현은 다음과 같습니다.

[!CODE-csharp[InterleaveSequenceWith](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet1)]

이 메서드를 작성했으므로 `Main` 메서드로 돌아가 데크 순서를 한 번 섞습니다.

```csharp
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

데크가 원래 순서로 돌아가는 데 몇 번을 섞어야 하는지 살펴보겠습니다. 두 시퀀스가 서로 같은지 확인하는 메서드를 작성해야 합니다. 이 메서드를 만든 후에는 데크 순서를 섞는 코드를 루프에 배치하고 데크가 원래 순서로 돌아갈 때를 확인해야 합니다.

두 시퀀스가 서로 같은지를 확인하는 메서드를 작성하는 작업은 간단합니다. 데크를 섞기 위해 작성한 메서드와 비슷한 구조를 갖습니다. 그렇지만 이 경우는 각 요소를 반환하지 말고 각 시퀀스의 일치하는 요소를 비교합니다. 전체 시퀀스가 열거된 경우 모든 요소가 일치하면 시퀀스도 같습니다.

[!CODE-csharp[SequenceEquals](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet2)]

다음에서는 두 번째 Linq 관용구인 터미널 메서드를 보여 줍니다. 여기서는 시퀀스를 입력으로 사용하고(또는 이 경우 두 개의 시퀀스) 단일 스칼라 값을 반환합니다. 이러한 메서드를 사용한다면 항상 쿼리의 마지막 메서드로 사용합니다. (그래서 이러한 이름을 갖습니다.) 

이 메서드를 사용하여 데크가 원래 순서로 돌아갈 때를 확인하면 작동 방식을 확인할 수 있습니다. 순서 섞기 코드를 루프 내에 포함하고, `SequenceEquals()` 메서드를 적용하여 시퀀스가 원래 순서가 될 때 중지합니다. 이 메서드는 시퀀스 대신 단일 값을 반환하므로 어떤 쿼리에서든지 항상 마지막 메서드로 사용되는 것을 확인할 수 있습니다.

```csharp
var times = 0;
var shuffle = startingDeck;

do
{
    shuffle = shuffle.Take(26).InterleaveSequenceWith(shuffle.Skip(26));

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }

    Console.WriteLine();
    times++;
} while (!startingDeck.SequenceEquals(shuffle));

Console.WriteLine(times);
```

샘플을 실행하고, 8회 반복 후 원래 구성으로 돌아갈 때까지 각 순서 섞기에서 데크가 재정렬되는 방식을 확인합니다.

## <a name="optimizations"></a>최적화

지금까지 빌드한 샘플은 ‘외부 순서 섞기’를 실행합니다. 즉, 맨 위 및 맨 아래 카드가 실행할 때마다 항상 같은 위치에 있습니다. 한 가지 부분을 변경하여 52장 카드가 모두 위치를 바꾸는 ‘내부 순서 섞기’를 실행해 보겠습니다. 내부 순서 섞기의 경우 반으로 나눈 아래쪽 부분의 첫 번째 카드가 데크의 첫 번째 카드가 되도록 데크를 인터리빙합니다. 즉, 반으로 나눈 위쪽 부분의 마지막 카드가 맨 아래 카드가 됩니다. 이를 위해 한 줄만 변경하면 됩니다. 데크의 위쪽 절반과 아래쪽 절반의 순서를 변경하도록 순서 섞기 호출을 업데이트합니다.

```csharp
shuffle = shuffle.Skip(26).InterleaveSequenceWith(shuffle.Take(26));
```

프로그램을 다시 실행합니다. 그러면 데크가 자체적으로 순서를 변경하는 데 52회 반복된다는 것을 알 수 있습니다. 또한 프로그램이 계속 실행될 때 몇 가지 심각한 성능 저하를 알 수 있습니다.

그 이유로는 여러 가지가 있습니다. 주요 원인 중 하나인 비효율적인 *지연 계산* 사용을 살펴 보겠습니다.

LINQ 쿼리는 느리게 계산됩니다. 요소가 요청될 때만 시퀀스가 생성됩니다. 일반적으로 이것이 LINQ의 큰 장점입니다. 그러나 이러한 프로그램에서 사용하면 실행 시간이 기하급수적으로 늘어납니다.

원래 데크는 LINQ 쿼리를 사용하여 생성되었습니다. 각 순서 섞기는 이전 데크에 대해 세 개의 LINQ 쿼리를 수행하여 생성됩니다. 이러한 모든 쿼리는 느리게 수행됩니다. 즉, 시퀀스가 요청될 때마다 다시 수행됩니다. 52번째 반복에 도달할 때까지 원래 데크를 아주 여러 번 다시 생성하게 됩니다. 이 동작을 보여 주기 위해 로그를 작성해 보겠습니다. 그런 후에 문제를 해결해 보겠습니다.

해당 쿼리가 실행되었음을 표시하기 위해 쿼리에 추가될 수 있는 로그 메서드는 다음과 같습니다.

[!CODE-csharp[LogQuery](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet3)]

그런 후 로그 메시지를 사용하여 각 쿼리의 정의를 계측합니다.

```csharp
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
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26)
            .LogQuery("Bottom Half"))
            .LogQuery("Shuffle");
        */

        shuffle = shuffle.Skip(26)
            .LogQuery("Bottom Half")
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

쿼리에 액세스할 때마다 로깅하지는 않고, 원래 쿼리를 만들 때만 로깅합니다. 프로그램을 실행하는 데 여전히 오래 걸리지만 이제 이유를 확인할 수 있습니다. 로깅을 켠 상태로 외부 순서 섞기를 실행하다가 지치면 내부 순서 섞기로 다시 전환합니다. 여전히 지연 계산 효과가 나타날 것입니다. 한 번 실행에서 모든 값 및 세트 생성을 비롯한 2592개의 쿼리가 실행됩니다.

이러한 모든 실행을 피하도록 이 프로그램을 업데이트하는 쉬운 방법이 있습니다. LINQ 메서드 `ToArray()` 및 `ToList()`가 있습니다. 이러한 메서드는 쿼리를 실행한 다음 결과를 각각 배열 또는 목록으로 저장합니다. 이러한 메서드를 사용하여 소스 쿼리를 다시 실행하는 대신 쿼리의 데이터 결과를 캐시합니다.  `ToArray()`를 호출하여 카드 데크를 생성하는 쿼리를 추가한 후 퀴리를 다시 실행합니다.

[!CODE-csharp[Main](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet1)]

다시 실행합니다. 그러면 외부 순서 섞기가 30개 쿼리로 줄어듭니다. 내부 순서 섞기를 다시 실행해도 비슷하게 개선된 것을 볼 수 있을 것입니다. (이제 162개의 쿼리가 실행됨)

이 예제에서 모든 쿼리가 즉시 실행되어야 한다고 잘못 생각하지 마세요. 이 예제는 지연 계산이 성능 문제를 일으킬 수 있는 사용 사례를 중점적으로 나타내도록 고안되었습니다. 카드 데크의 각 새 배열이 이전 배열에서 만들어지기 때문입니다. 지연 계산을 사용한다는 것은 각 새 데크 구성이 원래 데크에서 빌드되며, 심지어 `startingDeck`를 빌드한 코드를 실행하는 것을 의미합니다. 이로 인해 많은 양의 추가 작업이 발생합니다. 

실제로 즉시 계산을 사용할 때 성능이 더 좋아지는 알고리즘도 있고, 지연 계산을 사용할 때 성능이 더 좋아지는 알고리즘도 있습니다. (일반적으로 지연 계산은 데이터베이스 엔진과 같이 데이터 소스가 별도 프로세스일 때 사용하면 더 좋습니다. 이러한 경우 지연 계산은 좀 더 복잡한 쿼리를 통해 데이터베이스 프로세스에 대해 단일 왕복만 실행하도록 합니다.) LINQ는 지연 및 즉시 계산을 모두 가능하게 합니다. 계산해 보고 최상의 방법을 선택합니다.

## <a name="preparing-for-new-features"></a>새 기능 준비

이 샘플에 대해 작성한 코드는 작업을 수행하는 간단한 프로토타입을 만드는 예제입니다. 이러한 방식은 문제 영역을 탐색할 수 있는 좋은 방법이며 많은 기능에서 최선의 영구적인 해결책이 될 수 있습니다. 카드에 대해 *익명 형식*을 사용했으며 각 카드는 문자열로 표현됩니다.

*익명 형식*은 생산성 측면에서 여러 장점이 있습니다. 저장소를 나타내기 위해 클래스를 직접 정의하지 않아도 됩니다. 컴파일러가 형식을 생성합니다. 컴파일러에서 생성된 형식은 단순 데이터 개체에 대한 많은 모범 사례를 활용합니다. 이러한 형식은 *변경할 수 없습니다*. 즉, 생성된 후에는 해당 속성을 변경할 수 없습니다. 익명 형식은 어셈블리의 내부 형식이므로 해당 어셈블리에 대한 공용 API의 일부로 표시되지 않습니다. 익명 형식은 또한 서식 문자열과 해당 값을 반환하는 `ToString()` 메서드의 재정의도 포함합니다.

익명 형식에도 단점은 있습니다. 액세스 가능한 이름이 없으므로 반환 값 또는 인수로 사용할 수 없습니다. 이러한 익명 형식을 사용하는 모든 메서드는 제네릭 메서드입니다. 응용 프로그램이 더 많은 기능으로 커지면 `ToString()`의 재정의가 사용자가 원하는 방식이 아닐 수도 있습니다. 

또한 이 샘플은 각 카드의 세트 및 순서로 문자열을 사용합니다. 확장하기도 쉽습니다. C# 형식 시스템은 해당 값에 대해 `enum` 형식을 사용하여 더 나은 코드를 만드는 데 도움을 줄 수 있습니다.

세트부터 시작하세요. `enum`을 사용할 완벽한 시점입니다.

[!CODE-csharp[Suit enum](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet2)]

또한 `Suits()` 메서드는 형식 및 구현을 변경합니다.

[!CODE-csharp[Suit IEnumerable](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet4)]

다음에는 카드 순서에 대해 같은 변경을 수행합니다.

[!CODE-csharp[Rank enum](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet3)]

또한 순서를 생성하는 메서드도 변경합니다.

[!CODE-csharp[Rank IEnumerable](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet5)]

최종 정리 과정으로, 익명 형식에 의존하는 대신 카드를 나타내는 형식을 만들어 보겠습니다. 익명 형식은 간단한 로컬 형식으로 유용하지만 이 예제에서는 카드 게임을 하는 것이 주요 개념 중 하나입니다. 따라서 구체적인 형식을 띠어야 합니다.

[!CODE-csharp[PlayingCard](../../../samples/csharp/getting-started/console-linq/playingcard.cs?name=snippet1)]

이 형식은 *자동 구현된 읽기 전용 속성*을 사용합니다. 이러한 속성은 생성자에서 설정되며 수정할 수 없습니다. 또한 문자열 출력 서식을 보다 쉽게 지정할 수 있도록 하는 [문자열 보간](../language-reference/tokens/interpolated.md) 기능도 사용합니다.

시작 데크를 생성하는 쿼리가 새 형식을 사용하도록 업데이트합니다.

```csharp
var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                    from r in Ranks().LogQuery("Value Generation")
                    select new PlayingCard(s, r))
                    .LogQuery("Starting Deck")
                    .ToArray();
```

컴파일하고 다시 실행합니다. 출력은 조금 더 간결해지며 코드는 좀 더 명확하고 보다 쉽게 확장될 수 있습니다.

## <a name="conclusion"></a>결론

이 샘플에서는 LINQ에서 사용되는 일부 메서드를 통해 LINQ 지원 코드에서 쉽게 사용할 수 있는 자체 메서드를 만드는 방법을 보여 줬습니다. 또한 지연 계산과 즉시 계산 간의 차이점 그리고 이러한 결정이 성능에 미칠 수 있는 결과도 보여 주었습니다.

마술사의 한 가지 기술에 대해서도 약간 배웠습니다. 마술사들은 데크에서 모든 카드가 이동하는 위치를 제어할 수 있으므로 파로 셔플 기술을 사용합니다. 일부 마술에서 마술사는 청중 중 한 명에게 데크 맨 위에 카드를 놓아 달라고 부탁한 후 몇 번 섞은 다음 해당 카드의 위치를 알아냅니다. 특정 방식으로 데크를 셋팅해야 하는 마술도 있습니다. 마술사는 마술을 하기 전에 데크를 셋팅합니다. 그런 후 외부 순서 섞기를 사용해서 데크를 5번 섞습니다. 무대에서 무작위로 섞인 데크를 보여준 다음 3번 더 섞은 후 원하는 방식과 정확히 일치하게 데크를 셋팅할 수 있습니다.
