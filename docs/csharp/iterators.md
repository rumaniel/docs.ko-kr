---
title: 반복기
description: 기본 제공 C# 반복기를 사용하는 방법 및 사용자 지정 반복기 메서드를 만드는 방법을 알아봅니다.
ms.date: 06/20/2016
ms.assetid: 5cf36f45-f91a-4fca-a0b7-87f233e108e9
ms.openlocfilehash: e816af698a39a4b44aefa92017efdbc9e3c8cc1d
ms.sourcegitcommit: 438919211260bb415fc8f96ca3eabc33cf2d681d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2019
ms.locfileid: "59613436"
---
# <a name="iterators"></a>반복기

작성하는 거의 모든 프로그램에서 컬렉션을 반복해야 하는 경우가 있습니다. 컬렉션에 있는 모든 항목을 조사하는 코드를 작성합니다.

또한 해당 클래스의 요소에 대해 반복기를 생성하는 메서드인 반복기 메서드를 만듭니다. 이러한 메서드는 다음과 같은 경우에 사용할 수 있습니다.

+ 컬렉션의 각 항목에 대한 작업 수행.
+ 사용자 지정 컬렉션 열거.
+ [LINQ](linq/index.md) 또는 다른 라이브러리 확장.
+ 데이터가 반복기 메서드를 통해 효율적으로 흐르는 데이터 파이프라인 만들기.

C# 언어는 이러한 두 시나리오에 대한 기능을 제공합니다. 이 문서에서는 해당 기능에 대한 개요를 제공합니다.

이 자습서는 여러 단계로 구성됩니다. 각 단계 후에 애플리케이션을 실행하고 진행 상황을 확인할 수 있습니다. 이 항목에 대한 [전체 샘플을 보거나 다운로드](https://github.com/dotnet/samples/blob/master/csharp/iterators)할 수도 있습니다. 다운로드 지침은 [샘플 및 자습서](../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

## <a name="iterating-with-foreach"></a>foreach로 반복 처리

컬렉션 열거는 간단합니다. `foreach` 키워드는 컬렉션을 열거하여 컬렉션의 각 요소에 대해 포함된 문을 한 번 실행합니다.

```csharp
foreach (var item in collection)
{
   Console.WriteLine(item.ToString());
}
```

아주 간단합니다. 컬렉션의 모든 내용을 반복하려면 `foreach` 문만 있으면 됩니다. 하지만 `foreach` 문이 마법은 아닙니다. 이 문은 컬렉션을 반복하는 데 필요한 코드를 생성하기 위해 .NET Core 라이브러리에 정의된 두 개의 제네릭 인터페이스인 `IEnumerable<T>` 및 `IEnumerator<T>`를 사용합니다. 이 메커니즘은 아래에 더 자세히 설명되어 있습니다.

이러한 인터페이스 둘 다에는 제네릭이 아닌 인터페이스 `IEnumerable` 및 `IEnumerator`도 있습니다. 최신 코드에는 [제네릭](programming-guide/generics/index.md) 버전이 기본적으로 사용됩니다.

## <a name="enumeration-sources-with-iterator-methods"></a>반복기 메서드를 사용하는 열거형 소스

C# 언어의 또 다른 유용한 기능을 통해 열거형 소스를 만드는 메서드를 작성할 수 있습니다. 이러한 메서드를 *반복기 메서드*라고 합니다. 반복기 메서드는 요청될 때 시퀀스에서 개체를 생성하는 방법을 정의합니다. `yield return` 상황별 키워드를 사용하여 반복기 메서드를 정의합니다.

이 메서드를 작성하여 0에서 9 사이의 정수 시퀀스를 생성할 수 있습니다.

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    yield return 0;
    yield return 1;
    yield return 2;
    yield return 3;
    yield return 4;
    yield return 5;
    yield return 6;
    yield return 7;
    yield return 8;
    yield return 9;
}
```

위의 코드에서는 반복기 메서드에서 여러 개의 고유 `yield return` 문을 사용할 수 있다는 사실을 강조하기 위해 고유 `yield return` 문을 보여 줍니다.
다른 언어 구문을 사용하여 반복기 메서드의 코드를 단순화할 수 있으며 종종 그렇게 합니다. 아래의 메서드 정의는 정확히 동일한 시퀀스의 숫자를 생성합니다.

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;
}
```

둘 중 하나를 결정할 필요가 없습니다. 메서드의 요구를 충족하는 데 필요한 만큼 `yield return` 문을 사용할 수 있습니다.

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;

    yield return 50;

    index = 100;
    while (index++ < 110)
        yield return index;
}
```

이 구문은 기본 구문입니다. 반복기 메서드를 작성하는 실제 예제를 살펴보겠습니다. IoT 프로젝트를 진행하고 있고 디바이스 센서는 매우 큰 데이터 스트림을 생성한다고 가정합니다. 데이터를 파악하려면 N번째 데이터 요소마다 샘플링하는 메서드를 작성할 수 있습니다. 이 작은 반복기 메서드면 충분합니다.

```csharp
public static IEnumerable<T> Sample(this IEnumerable<T> sourceSequence, int interval)
{
    int index = 0;
    foreach (T item in sourceSequence)
    {
        if (index++ % interval == 0)
            yield return item;
    }
}
```

반복기 메서드에는 한 가지 중요한 제한이 있습니다. `return` 문과 `yield return` 문 둘 다를 동일한 메서드에서 사용할 수 없습니다. 다음 코드는 컴파일되지 않습니다.

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;

    yield return 50;

    // generates a compile time error:
    var items = new int[] {100, 101, 102, 103, 104, 105, 106, 107, 108, 109 };
    return items;
}
```

일반적으로 이 제한은 문제가 되지 않습니다. 메서드 전체에서 `yield return`을 사용하거나, 원래 메서드를 여러 메서드로 분리하여 일부는 `return`을 사용하고 일부는 `yield return`을 사용할 수 있습니다.

모든 위치에서 `yield return`을 사용하기 위해 마지막 메서드를 약간 수정할 수 있습니다.

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;

    yield return 50;

    var items = new int[] {100, 101, 102, 103, 104, 105, 106, 107, 108, 109 };
    foreach (var item in items)
        yield return item;
}
```

경우에 따라 반복기 메서드를 두 개의 다른 메서드로 분할하는 것이 정답일 수 있습니다. 하나는 `return`을 사용하고 다른 하나는 `yield return`을 사용합니다. 부울 인수에 따라 빈 컬렉션 또는 처음 5개의 홀수를 반환하려는 상황을 가정해 보세요. 다음과 같은 두 메서드로 작성할 수 있습니다.

```csharp
public IEnumerable<int> GetSingleDigitOddNumbers(bool getCollection)
{
    if (getCollection == false)
        return new int[0];
    else
        return IteratorMethod();
}

private IEnumerable<int> IteratorMethod()
{
    int index = 0;
    while (index++ < 10)
        if (index % 2 == 1)
            yield return index;
}
```

위의 메서드를 살펴보세요. 첫 번째 메서드는 표준 `return` 문을 사용하여 빈 컬렉션 또는 두 번째 메서드에서 만든 반복기를 반환합니다. 두 번째 메서드는 `yield return` 문을 사용하여 요청된 시퀀스를 만듭니다.

## <a name="deeper-dive-into-foreach"></a>`foreach` 심층 분석

`foreach` 문은 `IEnumerable<T>` 및 `IEnumerator<T>` 인터페이스를 사용하여 컬렉션의 모든 요소에서 반복하는 표준 관용구로 확장됩니다. 또한 개발자가 리소스를 제대로 관리하지 못해 발생하는 오류를 최소화합니다.

컴파일러는 첫 번째 예제에 표시된 `foreach` 루프를 다음과 유사한 구문으로 변환합니다.

```csharp
IEnumerator<int> enumerator = collection.GetEnumerator();
while (enumerator.MoveNext())
{
    var item = enumerator.Current;
    Console.WriteLine(item.ToString());
}
```

위의 구문은 버전 5 이상의 C# 컴파일러에서 생성된 코드를 나타냅니다. 버전 5 이전에는 `item` 변수의 범위가 달랐습니다.

```csharp
// C# versions 1 through 4:
IEnumerator<int> enumerator = collection.GetEnumerator();
int item = default(int);
while (enumerator.MoveNext())
{
    item = enumerator.Current;
    Console.WriteLine(item.ToString());
}
```

이전 동작에서는 람다 식과 관련된 버그를 진단하기가 어렵고 미묘할 수 있기 때문에 변경되었습니다. 람다 식에 대한 자세한 내용은 [람다 식](./programming-guide/statements-expressions-operators/lambda-expressions.md)을 참조하세요.

컴파일러에서 생성되는 정확한 코드는 약간 더 복잡하며 `GetEnumerator()`에서 반환된 개체가 `IDisposable` 인터페이스를 구현하는 상황을 처리합니다. 전체 확장에서는 다음과 더 유사한 코드를 생성합니다.

```csharp
{
    var enumerator = collection.GetEnumerator();
    try
    {
        while (enumerator.MoveNext())
        {
            var item = enumerator.Current;
            Console.WriteLine(item.ToString());
        }
    } finally
    {
        // dispose of enumerator.
    }
}
```

열거자가 삭제되는 방식의 `enumerator` 형식의 특성에 따라 달라집니다. 일반적인 경우 `finally` 절은 다음과 같이 확장됩니다.

```csharp
finally
{
   (enumerator as IDisposable)?.Dispose();
}
```

그러나 `enumerator`의 형식이 sealed 형식이고 `enumerator`의 형식에서 `IDisposable`로의 암시적 변환이 없는 경우 `finally` 절은 빈 블록으로 확장됩니다.

```csharp
finally
{
}
```

`enumerator`의 형식에서 `IDisposable`로의 암시적 변환이 있고 `enumerator` 형식이 nullable이 아닌 값 형식인 경우 `finally` 절은 다음과 같이 확장됩니다.

```csharp
finally
{
   ((IDisposable)enumerator).Dispose();
}
```

다행히도 이러한 세부 정보를 모두 기억할 필요가 없습니다. `foreach` 문에서 이러한 차이를 모두 처리합니다. 컴파일러는 이러한 구문에 대한 올바른 코드를 생성합니다.
