---
title: 인덱서
description: 하나 이상의 인수를 사용하여 참조된 속성인 인덱싱된 속성을 구현하는 방법 및 C# 인덱서에 대해 알아봅니다.
ms.date: 06/20/2016
ms.assetid: 0e9496da-e766-45a9-b92b-91820d4a350e
ms.openlocfilehash: a13163cb6bd835dfdd16c83c905c134eb8a86e7d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197602"
---
# <a name="indexers"></a>인덱서

*인덱서*는 속성과 비슷합니다. 다양한 방식으로 인덱서는 [속성](properties.md)과 동일한 언어 기능을 기반으로 합니다. 인덱서는 *인덱싱된* 속성, 즉 하나 이상의 인수로 참조된 속성을 사용하도록 설정합니다. 이러한 인수는 일부 값 컬렉션에 인덱스를 제공합니다.

## <a name="indexer-syntax"></a>인덱서 구문

변수 이름과 대괄호를 통해 인덱서에 액세스합니다. 인덱서 인수를 대괄호 안에 넣습니다.

```csharp
var item = someObject["key"];
someObject["AnotherKey"] = item;
```

`this` 키워드를 속성 이름으로 사용하고 대괄호 내에서 인수를 선언하여 인덱서를 선언합니다. 이 선언은 앞 단락에 표시된 사용법과 일치합니다.

```csharp
public int this[string key]
{
    get { return storage.Find(key); }
    set { storage.SetAt(key, value); }
}
```

이 초기 예제에서 속성 및 인덱서 구문 간의 관계를 확인할 수 있습니다. 이 유사성은 인덱서에 대한 대부분의 구문 규칙에 적용됩니다. 인덱서에는 유효한 모든 액세스 한정자(public, protected internal, protected, internal, private 또는 private protected)를 사용할 수 있습니다. sealed, virtual 또는 abstract일 수 있습니다. 속성과 마찬가지로, 인덱서의 get 및 set 접근자에 대해 다양한 액세스 한정자를 지정할 수 있습니다.
읽기 전용 인덱서(set 접근자 생략) 또는 쓰기 전용 인덱서(get 접근자 생략)를 지정할 수도 있습니다.

속성 작업에서 배운 거의 모든 내용을 인덱서에 적용할 수 있습니다. 해당 규칙의 유일한 예외는 *자동 구현 속성*입니다. 컴파일러가 항상 인덱서에 올바른 스토리지를 생성할 수 있는 것은 아닙니다.

항목 집합의 항목을 참조하는 인수의 존재 여부로 인덱서와 속성을 구분합니다. 각 인덱서의 인수 목록이 고유하기만 하면 형식에 여러 인덱서를 정의할 수 있습니다. 클래스 정의에 하나 이상의 인덱서를 사용할 수 있는 다양한 시나리오를 살펴보겠습니다. 

## <a name="scenarios"></a>시나리오

API가 해당 컬렉션에 대한 인수가 정의되는 일부 컬렉션을 모델링하는 경우 형식에 *인덱서*를 정의합니다. 인덱서는 .NET Core Framework의 일부인 컬렉션 형식에 직접 매핑될 수도 있고, 매핑되지 않을 수도 있습니다. 형식에 컬렉션 모델링 이외의 다른 책임이 있을 수도 있습니다.
인덱서를 사용하면 해당 추상화의 값이 저장 또는 계산되는 방법의 내부 세부 정보를 노출하지 않고 형식의 추상화와 일치하는 API를 제공할 수 있습니다.

*인덱서*를 사용하기 위한 몇 가지 일반적인 시나리오를 살펴보겠습니다. [인덱서에 대한 샘플 폴더](https://github.com/dotnet/samples/tree/master/csharp/indexers)에 액세스할 수 있습니다. 다운로드 지침은 [샘플 및 자습서](../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

### <a name="arrays-and-vectors"></a>배열 및 벡터

인덱서를 만들기 위한 가장 일반적인 시나리오 중 하나는 형식이 배열 또는 벡터를 모델링하는 경우입니다. 인덱서를 만들어 정렬된 데이터 목록을 모델링할 수 있습니다. 

사용자 고유의 인덱서를 만드는 경우 해당 컬렉션에 대한 스토리지를 요구 사항에 맞게 정의할 수 있다는 장점이 있습니다. 너무 커서 한 번에 메모리에 로드할 수 없는 기록 데이터를 형식이 모델링하는 시나리오를 가정합니다. 사용량에 따라 컬렉션의 섹션을 로드 및 언로드해야 합니다. 다음 예제에서는 이 동작을 모델링합니다. 존재하는 데이터 요소 수를 보고합니다. 필요에 따라 데이터 섹션이 포함될 페이지를 만듭니다. 최신 요청에 필요한 페이지의 공간을 만들기 위해 메모리에서 페이지를 제거합니다.

```csharp
public class DataSamples
{
    private class Page
    {
        private readonly List<Measurements> pageData = new List<Measurements>();
        private readonly int startingIndex;
        private readonly int length;
        private bool dirty;
        private DateTime lastAccess;

        public Page(int startingIndex, int length)
        {
            this.startingIndex = startingIndex;
            this.length = length;
            lastAccess = DateTime.Now;

            // This stays as random stuff:
            var generator = new Random();
            for(int i=0; i < length; i++)
            {
                var m = new Measurements
                {
                    HiTemp = generator.Next(50, 95),
                    LoTemp = generator.Next(12, 49),
                    AirPressure = 28.0 + generator.NextDouble() * 4
                };
                pageData.Add(m);
            }
        }
        public bool HasItem(int index) =>
            ((index >= startingIndex) &&
            (index < startingIndex + length));

        public Measurements this[int index]
        {
            get
            {
                lastAccess = DateTime.Now;
                return pageData[index - startingIndex];
            }
            set
            {
                pageData[index - startingIndex] = value;
                dirty = true;
                lastAccess = DateTime.Now;
            }
        }

        public bool Dirty => dirty;
        public DateTime LastAccess => lastAccess;
    }

    private readonly int totalSize;
    private readonly List<Page> pagesInMemory = new List<Page>();

    public DataSamples(int totalSize)
    {
        this.totalSize = totalSize;
    }

    public Measurements this[int index]
    {
        get
        {
            if (index < 0)
                throw new IndexOutOfRangeException("Cannot index less than 0");
            if (index >= totalSize)
                throw new IndexOutOfRangeException("Cannot index past the end of storage");

            var page = updateCachedPagesForAccess(index);
            return page[index];
        }
        set
        {
            if (index < 0)
                throw new IndexOutOfRangeException("Cannot index less than 0");
            if (index >= totalSize)
                throw new IndexOutOfRangeException("Cannot index past the end of storage");
            var page = updateCachedPagesForAccess(index);

            page[index] = value;
        }
    }

    private Page updateCachedPagesForAccess(int index)
    {
        foreach (var p in pagesInMemory)
        {
            if (p.HasItem(index))
            {
                return p;
            }
        }
        var startingIndex = (index / 1000) * 1000;
        var newPage = new Page(startingIndex, 1000);
        addPageToCache(newPage);
        return newPage;
    }

    private void addPageToCache(Page p)
    {
        if (pagesInMemory.Count > 4)
        {
            // remove oldest non-dirty page:
            var oldest = pagesInMemory
                .Where(page => !page.Dirty)
                .OrderBy(page => page.LastAccess)
                .FirstOrDefault();
            // Note that this may keep more than 5 pages in memory
            // if too much is dirty
            if (oldest != null)
                pagesInMemory.Remove(oldest);
        }
        pagesInMemory.Add(p);
    }
}
```

이 디자인 구문에 따라 전체 데이터 집합을 메모리 내 컬렉션에 로드할 필요가 없는 모든 종류의 컬렉션을 모델링할 수 있습니다. `Page` 클래스는 공용 인터페이스의 일부가 아닌 중첩된 private 클래스입니다. 이러한 세부 정보는 이 클래스의 모든 사용자로부터 숨겨집니다.

### <a name="dictionaries"></a>사전

또 다른 일반적인 시나리오는 사전 또는 맵을 모델링해야 하는 경우입니다. 이 시나리오는 형식이 키, 일반적으로 텍스트 키에 따라 값을 저장하는 경우입니다. 이 예제에서는 해당 옵션을 관리하는 [람다 식](delegates-overview.md)에 명령줄 인수를 매핑하는 사전을 만듭니다. 다음 예제에서는 명령줄 옵션을 `Action` 대리자에 매핑하는 `ArgsActions` 클래스와 해당 옵션을 발견할 경우 `ArgsActions`를 사용하여 각 `Action`을 실행하는 `ArgsProcessor` 클래스 등 두 개의 클래스를 보여 줍니다.

```csharp
public class ArgsProcessor
{
    private readonly ArgsActions actions;

    public ArgsProcessor(ArgsActions actions)
    {
        this.actions = actions;
    }

    public void Process(string[] args)
    {
        foreach(var arg in args)
        {
            actions[arg]?.Invoke();
        }
    }

}
public class ArgsActions
{
    readonly private Dictionary<string, Action> argsActions = new Dictionary<string, Action>();

    public Action this[string s]
    {
        get
        {
            Action action;
            Action defaultAction = () => {} ;
            return argsActions.TryGetValue(s, out action) ? action : defaultAction;
        }
    }

    public void SetOption(string s, Action a)
    {
        argsActions[s] = a;
    }
}
```

이 예제에서 `ArgsAction` 컬렉션은 기본 컬렉션과 거의 같도록 매핑됩니다.
`get`은 지정된 옵션이 구성되었는지 여부를 확인합니다. 구성된 경우 해당 옵션과 연결된 `Action`을 반환합니다. 구성되지 않은 경우 아무 작업도 수행하지 않는 `Action`을 반환합니다. public 접근자는 `set` 접근자를 포함하지 않습니다. 대신, public 메서드를 옵션 설정에 사용하는 디자인입니다.

### <a name="multi-dimensional-maps"></a>다차원 맵

여러 인수를 사용하는 인덱서를 만들 수 있습니다. 또한 이러한 인수는 같은 형식으로 제한되지 않습니다. 두 가지 예제를 살펴보겠습니다.   

첫 번째 예제는 Mandelbrot 집합의 값을 생성하는 클래스를 보여 줍니다. 집합 뒤의 수학에 대한 자세한 내용은 [이 문서](https://en.wikipedia.org/wiki/Mandelbrot_set)를 참조하세요. 인덱서는 두 개의 double을 사용하여 X, Y 평면의 한 지점을 정의합니다.
get 접근자는 한 지점이 집합에 없는 것으로 확인될 때까지 반복 횟수를 계산합니다. 최대 반복 횟수에 도달하면 지점이 집합에 있고 클래스의 maxIterations 값이 반환됩니다. Mandelbrot 집합에 대해 잘 알려진 컴퓨터 생성 이미지는 한 지점이 집합 외부에 있음을 확인하는 데 필요한 반복 횟수의 색을 정의합니다.

```csharp
public class Mandelbrot
{
    readonly private int maxIterations;

    public Mandelbrot(int maxIterations)
    {
        this.maxIterations = maxIterations;
    }

    public int this [double x, double y]
    {
        get
        {
            var iterations = 0;
            var x0 = x;
            var y0 = y;

            while ((x*x + y * y < 4) &&
                (iterations < maxIterations))
            {
                var newX = x * x - y * y + x0;
                y = 2 * x * y + y0;
                x = newX;
                iterations++;
            }
            return iterations;
        }
    }
}
```

Mandelbrot 집합은 실수 값의 모든 (x, y) 좌표에서 값을 정의합니다.
그러면 무한 개수의 값을 포함할 수 있는 사전이 정의됩니다. 따라서 집합 뒤에는 스토리지가 없습니다. 대신, 이 클래스는 코드에서 `get` 접근자를 호출할 때 각 지점의 값을 계산합니다. 사용되는 기본 스토리지는 없습니다.

인덱서가 서로 다른 형식의 여러 인수를 사용하는 인덱서의 마지막 사용 방법을 살펴보겠습니다. 기록 온도 데이터를 관리하는 프로그램을 가정합니다. 이 인덱서는 도시 및 날짜를 사용하여 해당 위치의 상한 및 하한 온도를 설정하거나 가져옵니다.

```csharp
using DateMeasurements = 
    System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>;
using CityDataMeasurements = 
    System.Collections.Generic.Dictionary<string, System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>>;

public class HistoricalWeatherData
{
    readonly CityDataMeasurements storage = new CityDataMeasurements();

    public Measurements this[string city, DateTime date]
    {
        get
        {
            var cityData = default(DateMeasurements);

            if (!storage.TryGetValue(city, out cityData))
                throw new ArgumentOutOfRangeException(nameof(city), "City not found");

            // strip out any time portion:
            var index = date.Date;
            var measure = default(Measurements);
            if (cityData.TryGetValue(index, out measure))
                return measure;
            throw new ArgumentOutOfRangeException(nameof(date), "Date not found");
        }
        set
        {
            var cityData = default(DateMeasurements);

            if (!storage.TryGetValue(city, out cityData))
            {
                cityData = new DateMeasurements();
                storage.Add(city, cityData);
            }

            // Strip out any time portion:
            var index = date.Date;
            cityData[index] = value;
        }
    }
}
```

이 예제에서는 도시(`string`) 및 날짜(`DateTime`)의 두 인수에 대한 날씨 데이터를 매핑하는 인덱서를 만듭니다. 내부 스토리지는 두 개의 `Dictionary` 클래스를 사용하여 2차원 사전을 나타냅니다. 공용 API는 더 이상 기본 스토리지를 나타내지 않습니다. 대신, 기본 스토리지가 다양한 핵심 컬렉션 형식을 사용해야 하는 경우에도 인덱서의 언어 기능을 사용하여 추상화를 나타내는 공용 인터페이스를 만들 수 있습니다.

일부 개발자에게 친숙하지 않을 수 있는 이 코드의 두 부분이 있습니다. 다음 두 개의 `using` 문을 살펴보세요.

```csharp
using DateMeasurements = System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>;
using CityDataMeasurements = System.Collections.Generic.Dictionary<string, System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>>;
```

두 문은 생성된 제네릭 형식의 *별칭*을 만듭니다. 이러한 문을 통해 나중에 코드에서 `Dictionary<DateTime, Measurements>` 및 `Dictionary<string, Dictionary<DateTime, Measurements> >`의 제네릭 구문이 아니라 더 설명적인 `DateMeasurements` 및 `CityDateMeasurements` 이름을 사용할 수 있습니다. 이 구문의 경우 `=` 기호의 오른쪽에 정규화된 형식 이름을 사용해야 합니다.

두 번째 방법은 컬렉션에 인덱싱하는 데 사용되는 `DateTime` 개체의 시간 부분을 제거하는 것입니다. .NET Framework는 날짜 전용 형식을 포함하지 않습니다.
개발자는 `DateTime` 형식을 사용하지만 `Date` 속성을 사용하여 해당 날짜의 `DateTime` 개체가 모두 같도록 합니다.

## <a name="summing-up"></a>요약

해당 속성이 단일 값이 아니라 각 개별 항목이 인수 집합으로 식별되는 값 컬렉션을 나타내는, 속성과 유사한 요소가 클래스에 있을 경우 항상 인덱서를 만들어야 합니다. 이러한 인수는 참조해야 하는 컬렉션의 항목을 고유하게 식별할 수 있습니다.
인덱서는 [속성](properties.md) 개념을 확장하며, 이 경우 멤버가 클래스 외부의 데이터 항목처럼 처리되지만 부가적으로 메서드처럼 처리됩니다. 인덱서를 사용하면 인수가 항목 집합을 나타내는 속성에서 단일 항목을 찾을 수 있습니다.
