---
title: 패턴 일치 기능을 사용하여 데이터 형식 확장
description: 이 고급 자습서에서는 패턴 일치 기술을 사용하여 개별적으로 생성된 데이터 및 알고리즘을 사용하여 기능을 만드는 방법을 보여 줍니다.
ms.date: 03/13/2019
ms.custom: mvc
ms.openlocfilehash: 036a6bcda04771eb8cf3699af8756e83bb144389
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332358"
---
# <a name="tutorial-using-pattern-matching-features-to-extend-data-types"></a>자습서: 패턴 일치 기능을 사용하여 데이터 형식 확장

C# 7에서는 기본 패턴 일치 기능을 도입했습니다. 이 기능은 새로운 식과 패턴을 포함하여 C# 8에서 확장됩니다. 다른 라이브러리에 있을 수 있는 형식을 확장한 것처럼 동작하는 기능을 작성할 수 있습니다. 패턴의 또 다른 용도는 확장되는 형식의 기초 기능이 아닌 애플리케이션에 필요한 기능을 만드는 것입니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
>
> - 패턴 일치를 사용해야 하는 상황을 인식합니다.
> - 패턴 일치 식을 사용하여 형식 및 속성 값에 따라 동작을 구현합니다.
> - 패턴 일치를 다른 기술과 결합하여 완전한 알고리즘을 만듭니다.

## <a name="prerequisites"></a>전제 조건

C# 8.0 컴파일러를 포함하여 .NET Core를 실행하도록 머신을 설정해야 합니다. C# 8 컴파일러는 [Visual Studio 2019 버전 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 또는 [.NET CORE 3.0 SDK](https://dotnet.microsoft.com/download)부터 사용할 수 있습니다.

이 자습서에서는 Visual Studio 또는 .NET Core CLI를 포함하여 C# 및 .NET에 익숙하다고 가정합니다.

## <a name="scenarios-for-pattern-matching"></a>패턴 일치 시나리오

최신 개발에는 종종 여러 소스의 데이터를 통합하고 해당 데이터의 정보와 인사이트를 단일 결합 애플리케이션에서 제공하는 작업이 포함됩니다. 여러분과 팀에는 들어오는 데이터를 나타내는 모든 형식에 대한 제어 또는 액세스 권한이 없습니다.

클래식 개체 지향 디자인의 경우 여러 데이터 소스의 각 데이터 형식을 나타내는 형식을 애플리케이션에서 민들어야 합니다. 그런 다음, 애플리케이션은 이 새로운 형식을 사용하고, 상속 계층 구조를 빌드하고, 가상 메서드를 만들고, 추상화를 구현합니다. 해당 기술이 적용되고 때때로 가장 적합한 도구가 됩니다. 경우에 따라 더 적은 코드를 작성할 수 있습니다. 데이터를 조작하는 작업에서 데이터를 분리하는 기술을 사용하여 보다 명확한 코드를 작성할 수 있습니다.

이 자습서에서는 단일 시나리오에 대해 여러 외부 소스에서 들어오는 데이터를 사용하는 애플리케이션을 만들고 살펴봅니다. **패턴 일치**가 원래 시스템에 포함되지 않은 데이터를 사용하고 처리하는 효율적인 방법을 어떻게 제공하는지 확인합니다.

교통량을 관리하는 데 통행료 및 최대 사용 시간 가격을 사용하는 주요 도시 지역을 살펴보겠습니다. 형식에 따라 차량의 통행료를 계산하는 애플리케이션을 작성합니다. 나중에 차량 탑승자 수에 따른 가격이 개선 사항에 통합됩니다. 추가로 시간 및 요일에 따른 가격이 개선 사항에 추가됩니다.

이 간단한 설명을 통해 이 시스템을 모델링하기 위한 개체 계층 구조를 빠르게 설명했을 수 있습니다. 그러나 데이터는 다른 차량 등록 관리 시스템 같은 다양한 출처에서 수집됩니다. 이 시스템은 해당 데이터를 모델링하는 여러 가지 클래스를 제공하지만 사용자가 사용할 수 있는 단일 개체 모델이 없습니다. 이 자습서에서는 다음 코드와 같이 해당 외부 시스템의 차량 데이터를 모델링하는 데 이 간단한 클래스를 사용합니다.

[!code-csharp[ExternalSystems](~/samples/csharp/tutorials/patterns/start/toll-calculator/ExternalSystems.cs)]

시작 코드는 [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/patterns/start) GitHub 리포지토리에서 다운로드할 수 있습니다. 차량 클래스는 여러 가지 시스템에서 가져오고 서로 다른 네임스페이스에 포함됨을 알 수 있습니다. `System.Object` 이외의 공용 기본 클래스는 활용할 수 없습니다.

## <a name="pattern-matching-designs"></a>패턴 일치 디자인

이 자습서에서 사용된 시나리오는 패턴 일치가 해결하기에 적합한 종류의 문제를 중점적으로 살펴봅니다.

- 사용해야 하는 개체는 목표와 일치하는 개체 계층 구조에 없습니다. 관련 없는 시스템에 포함된 클래스를 사용 중일 수 있습니다.
- 추가할 기능은 이 클래스에 대한 핵심 추상화에 포함되지 않습니다. 차량에 따른 통행료는 차량 형식에 따라 변경되지만 통행료는 차량의 핵심 기능이 아닙니다. 

데이터의 모양과 해당 데이터에 대한 작업을 분리해서 설명하면 C#의 패턴 일치 기능을 더 쉽게 사용할 수 있습니다.  

## <a name="implement-the-basic-toll-calculations"></a>기본 통행료 계산 구현

가장 기본적인 통행료 계산에는 차량 형식만 사용됩니다.

- `Car`는 2.00 USD입니다.
- `Taxi`는 3.50 USD입니다.
- `Bus`는 5.00 USD입니다.
- `DeliveryTruck`은 10.00 USD입니다.

새 `TollCalculator` 클래스를 만들고 차량 형식에 대한 패턴 일치를 구현하여 통행료 액수를 얻습니다. 다음 코드에서는 `TollCalculator`의 초기 구현을 보여줍니다.

```csharp
using System;
using CommercialRegistration;
using ConsumerVehicleRegistration;
using LiveryRegistration;

namespace toll_calculator
{
    public class TollCalculator
    {
        public decimal CalculateToll(object vehicle) =>
            vehicle switch
        {
            Car c           => 2.00m,
            Taxi t          => 3.50m,
            Bus b           => 5.00m,
            DeliveryTruck t => 10.00m,
            { }             => throw new ArgumentException(message: "Not a known vehicle type", paramName: nameof(vehicle)),
            null            => throw new ArgumentNullException(nameof(vehicle))
        };
    }
}
```

앞의 코드는 **형식 패턴**을 테스트하는 **switch 식**([`switch`](../language-reference/keywords/switch.md) 문과 같지 않음)을 사용합니다. **switch 식**은 앞의 코드에 있는 `vehicle` 변수로 시작하고 그 뒤에 `switch` 키워드가 옵니다. 다음은 중괄호로 묶인 모든 **스위치 암(arm)** 을 제공합니다. `switch` 식은 `switch` 문을 둘러싸는 구문을 다르게 구체화합니다. `case` 키워드가 생략되고 각 암(arm)의 결과는 식입니다. 마지막 두 개의 암(arm)은 새 언어 기능을 보여 줍니다. `{ }` 사례는 이전 암(arm)과 일치하지 않는 null이 아닌 개체와 일치합니다. 이 암(arm)은 이 메서드에 전달된 잘못된 형식을 catch합니다.  `{ }` 사례는 각 차량 형식에 대한 사례를 따라야 합니다. 순서가 반대로 된 경우 `{ }` 사례가 우선적으로 적용됩니다. 마지막으로 `null`이 이 메서드에 전달될 때 `null` 패턴이 검색됩니다. 다른 형식 패턴은 올바른 형식의 null이 아닌 개체와만 일치하므로 `null` 패턴이 마지막일 수 있습니다.

`Program.cs`에서 다음 코드를 사용하여 이 코드를 테스트할 수 있습니다.

```csharp
using System;
using CommercialRegistration;
using ConsumerVehicleRegistration;
using LiveryRegistration;

namespace toll_calculator
{
    class Program
    {
        static void Main(string[] args)
        {
            var tollCalc = new TollCalculator();

            var car = new Car();
            var taxi = new Taxi();
            var bus = new Bus();
            var truck = new DeliveryTruck();

            Console.WriteLine($"The toll for a car is {tollCalc.CalculateToll(car)}");
            Console.WriteLine($"The toll for a taxi is {tollCalc.CalculateToll(taxi)}");
            Console.WriteLine($"The toll for a bus is {tollCalc.CalculateToll(bus)}");
            Console.WriteLine($"The toll for a truck is {tollCalc.CalculateToll(truck)}");

            try
            {
                tollCalc.CalculateToll("this will fail");
            }
            catch (ArgumentException e)
            {
                Console.WriteLine("Caught an argument exception when using the wrong type");
            }
            try
            {
                tollCalc.CalculateToll(null);
            }
            catch (ArgumentNullException e)
            {
                Console.WriteLine("Caught an argument exception when using null");
            }
        }
    }
}
```

해당 코드는 시작 프로젝트에 포함되지만 주석으로 처리됩니다. 주석을 제거하면 작성한 내용을 테스트할 수 있습니다.

먼저 패턴을 사용하여 코드 및 데이터가 구분되는 알고리즘을 만드는 방법을 확인하겠습니다. `switch` 식은 형식을 테스트하고 결과에 따라 다른 값을 생성합니다. 이는 시작에 불과합니다.

## <a name="add-occupancy-pricing"></a>점유 가격 추가

통행료 징수 기관은 차량이 최대 탑승자 수로 이동하도록 권장하려고 합니다. 차량에 더 적은 승객이 있는 경우 추가 요금을 청구하기로 했으며, 더 낮은 가격을 제공하여 최대 탑승자 차량을 장려합니다.

- 승객이 없는 승용차와 택시에는 0.50 USD의 추가 통행료가 부과됩니다.
- 승객이 2명인 승용차와 택시는 $0.50의 할인을 받습니다.
- 승객이 3명 이상인 승용차와 택시는 1.00 USD의 할인을 받습니다.
- 최대 탑승자 수의 50% 미만이 탑승한 버스는 2.00 USD의 추가 요금이 부과됩니다.
- 탑승자 수가 90%를 초과하는 버스는 1.00 USD의 할인을 받습니다.

이 규칙은 동일한 switch 식에서 **속성 패턴**을 사용하여 구현할 수 있습니다. 속성 패턴은 형식이 결정된 후 개체의 속성을 검사합니다. `Car` 사례 1개는 다른 사례 4개로 확장됩니다.

```csharp
vehicle switch
{
    Car { Passengers: 0}        => 2.00m + 0.50m,
    Car { Passengers: 1 }       => 2.0m,
    Car { Passengers: 2}        => 2.0m - 0.50m,
    Car c                       => 2.00m - 1.0m,

    // ...
};
```

처음 3개 사례는 형식을 `Car`로 테스트한 다음, `Passengers` 속성 값을 확인합니다. 둘 다 일치하는 경우 해당 식이 계산되고 반환됩니다.

또한 비슷한 방식으로 택시에 대한 사례를 확장합니다.

```csharp
vehicle switch
{
    // ...

    Taxi { Fares: 0}  => 3.50m + 1.00m,
    Taxi { Fares: 1 } => 3.50m,
    Taxi { Fares: 2}  => 3.50m - 0.50m,
    Taxi t            => 3.50m - 1.00m,

    // ...
};
```

앞의 예제에서는 `when` 절이 마지막 사례에서 생략되었습니다.

다음으로, 다음 예제와 같이 버스 사례를 확장하여 점유 규칙을 구현합니다.

```csharp
vehicle switch
{
    // ...

    Bus b when ((double)b.Riders / (double)b.Capacity) < 0.50 => 5.00m + 2.00m,
    Bus b when ((double)b.Riders / (double)b.Capacity) > 0.90 => 5.00m - 1.00m,
    Bus b => 5.00m,

    // ...
};
```

통행료 징수 기관은 배달 트럭의 승객 수에 관심이 없습니다. 대신 다음과 같이 트럭의 중량 등급을 기준으로 요금을 조정합니다.

- 5000lbs를 초과하는 트럭에는 5.00 USD가 추가로 부과됩니다.
- 3000lbs 미만의 경량 트럭에는 $2.00 할인이 제공됩니다.

해당 규칙은 다음 코드로 구현됩니다.

```csharp
vehicle switch
{
    // ...

    DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
    DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
    DeliveryTruck t => 10.00m,
};
```

앞의 코드는 스위치 암(arm)의 `when` 절을 표시합니다. `when` 절을 사용하여 속성에서 같음 이외의 조건을 테스트합니다. 완료되면 다음과 같은 메서드가 생성됩니다.

```csharp
vehicle switch
{
    Car { Passengers: 0}        => 2.00m + 0.50m,
    Car { Passengers: 1}        => 2.0m,
    Car { Passengers: 2}        => 2.0m - 0.50m,
    Car c                       => 2.00m - 1.0m,

    Taxi { Fares: 0}  => 3.50m + 1.00m,
    Taxi { Fares: 1 } => 3.50m,
    Taxi { Fares: 2}  => 3.50m - 0.50m,
    Taxi t            => 3.50m - 1.00m,

    Bus b when ((double)b.Riders / (double)b.Capacity) < 0.50 => 5.00m + 2.00m,
    Bus b when ((double)b.Riders / (double)b.Capacity) > 0.90 => 5.00m - 1.00m,
    Bus b => 5.00m,

    DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
    DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
    DeliveryTruck t => 10.00m,
    
    { }     => throw new ArgumentException(message: "Not a known vehicle type", paramName: nameof(vehicle)),
    null    => throw new ArgumentNullException(nameof(vehicle))
};
```

대부분의 이 스위치 암(arm)은 **재귀 패턴**의 예입니다. 예를 들어 `Car { Passengers: 1}`은 속성 패턴 내의 상수 패턴을 표시합니다.

중첩된 스위치를 사용하여 이 코드의 반복 횟수를 줄일 수 있습니다. `Car` 및 `Taxi`에는 둘 다 앞의 예제에 있는 서로 다른 암(arm) 4개가 포함됩니다. 두 경우에 모두 속성 패턴에 제공되는 형식 패턴을 만들 수 있습니다. 이 기술이 다음 코드에 나옵니다.

```csharp
public decimal CalculateToll(object vehicle) =>
    vehicle switch
    {
        Car c => c.Passengers switch
        {
            0 => 2.00m + 0.5m,
            1 => 2.0m,
            2 => 2.0m - 0.5m,
            _ => 2.00m - 1.0m
        },

        Taxi t => t.Fares switch
        {
            0 => 3.50m + 1.00m,
            1 => 3.50m,
            2 => 3.50m - 0.50m,
            _ => 3.50m - 1.00m
        },

        Bus b when ((double)b.Riders / (double)b.Capacity) < 0.50 => 5.00m + 2.00m,
        Bus b when ((double)b.Riders / (double)b.Capacity) > 0.90 => 5.00m - 1.00m,
        Bus b => 5.00m,

        DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
        DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
        DeliveryTruck t => 10.00m,

        { }  => throw new ArgumentException(message: "Not a known vehicle type", paramName: nameof(vehicle)),
        null => throw new ArgumentNullException(nameof(vehicle))
    };
```

앞의 샘플에서 재귀 식을 사용하면 속성 값을 테스트하는 자식 암(arm)이 포함된 `Car` 및 `Taxi` 암(arm)을 반복하지 않습니다. 해당 암(arm)은 불연속 값이 아닌 속성 범위를 테스트하므로 이 기술은 `Bus` 및 `DeliveryTruck` 암(arm)에 사용되지 않습니다.

## <a name="add-peak-pricing"></a>최대 가격 추가

마지막 기능을 위해 통행료 징수 기관은 시간에 따른 최대 가격을 추가하려고 합니다. 아침 및 저녁 교통 체증 시간 중에 통행료는 2배로 부과됩니다. 해당 규칙은 아침에는 도시로 들어오고 저녁 교통 체증 시간에는 나가는 한 방향의 교통량에만 영향을 줍니다. 평일 중 다른 시간에 통행료는 50% 증가합니다. 늦은 밤과 이른 아침에는 통행료가 25% 감소합니다. 주말에는 시간과 관계없이 정상 요금입니다.

이 기능에 대해 패턴 일치를 사용하지만 패턴 일치를 다른 기술과 통합하게 됩니다. 방향, 요일 및 시간의 모든 조합을 설명하는 단일 패턴 일치 식을 빌드할 수 있습니다. 복잡한 식이 생성됩니다. 읽기 힘들고 이해하기 어려운 식입니다. 따라서 식의 정확성을 보장하기 어렵습니다. 대신, 해당 메서드를 결합하여 모든 상태를 간결하게 설명하는 값 튜플을 빌드합니다. 그런 다음, 패턴 일치를 사용하여 통행료의 승수를 계산합니다. 튜플에는 다음 세 가지 불연속 조건이 포함됩니다.

- 요일은 주중 또는 주말입니다.
- 통행료가 징수되는 시간대.
- 방향은 도시 진입 또는 도시 진출입니다.

다음 표는 입력 값과 최대 가격 승수의 조합을 보여 줍니다.

| Day        | Time         | 방향 | 할증 |
| ---------- | ------------ | --------- |--------:|
| 주중    | 아침 교통 체증 | 인바운드   | x 2.00  |
| 주중    | 아침 교통 체증 | 아웃바운드  | x 1.00  |
| 주중    | 주간      | 인바운드   | x 1.50  |
| 주중    | 주간      | 아웃바운드  | x 1.50  |
| 주중    | 저녁 교통 체증 | 인바운드   | x 1.00  |
| 주중    | 저녁 교통 체증 | 아웃바운드  | x 2.00  |
| 주중    | 야간    | 인바운드   | x 0.75  |
| 주중    | 야간    | 아웃바운드  | x 0.75  |
| 주말    | 아침 교통 체증 | 인바운드   | x 1.00  |
| 주말    | 아침 교통 체증 | 아웃바운드  | x 1.00  |
| 주말    | 주간      | 인바운드   | x 1.00  |
| 주말    | 주간      | 아웃바운드  | x 1.00  |
| 주말    | 저녁 교통 체증 | 인바운드   | x 1.00  |
| 주말    | 저녁 교통 체증 | 아웃바운드  | x 1.00  |
| 주말    | 야간    | 인바운드   | x 1.00  |
| 주말    | 야간    | 아웃바운드  | x 1.00  |

세 가지 변수의 조합은 16가지입니다. 일부 조건을 결합하여 마지막 switch 식을 단순화합니다.

통행료를 징수하는 시스템은 통행료가 징수된 시간에 <xref:System.DateTime> 구조체를 사용합니다. 앞의 표에서 변수를 만드는 멤버 메서드를 작성합니다. 다음 함수는 패턴 일치 switch 식을 사용하여 <xref:System.DateTime>이 주말 또는 주중을 나타내는지 여부를 표시합니다.

```csharp
private static bool IsWeekDay(DateTime timeOfToll) =>
    timeOfToll.DayOfWeek switch
    {
        DayOfWeek.Monday    => true,
        DayOfWeek.Tuesday   => true,
        DayOfWeek.Wednesday => true,
        DayOfWeek.Thursday  => true,
        DayOfWeek.Friday    => true,
        DayOfWeek.Saturday  => false,
        DayOfWeek.Sunday    => false
    };
```

해당 메서드는 작동하지만 반복적입니다. 다음 코드와 같이 단순화할 수 있습니다.

[!code-csharp[IsWeekDay](~/samples/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#IsWeekDay)]

다음으로, 시간을 블록으로 분류하는 비슷한 함수를 추가합니다.

[!code-csharp[GetTimeBand](~/samples/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#GetTimeBand)]

이전 메서드는 패턴 일치를 사용하지 않습니다. `if` 문의 친숙한 계단식 배열을 사용하는 것이 더 이해하기 쉽습니다. 개인 `enum`을 추가하여 각 시간 범위를 불연속 값으로 변환합니다.

이 메서드를 만든 후 **튜플 패턴**과 함께 다른 `switch` 식을 사용하여 할증 가격을 계산할 수 있습니다. 모든 16개 암(arm)을 사용하여 `switch` 식을 작성할 수 있습니다.

[!code-csharp[FullTuplePattern](~/samples/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#TuplePatternOne)]

위 코드는 작동하지만 단순화할 수 있습니다. 주말에 대한 8개 조합에는 모두 동일한 통행료가 포함됩니다. 8개 모두를 다음 줄로 바꿀 수 있습니다.

```csharp
(false, _, _) => 1.0m,
```

인바운드 및 아웃바운드 교통량은 둘 다 주중 주간 및 야간 시간 동안 동일한 승수를 포함합니다. 해당하는 4개의 스위치 암(arm)은 다음 두 줄로 바꿀 수 있습니다.

```csharp
(true, TimeBand.Overnight, _) => 0.75m,
(true, TimeBand.Daytime, _)   => 1.5m,
```

해당하는 두 줄이 변경된 후 코드는 다음과 같이 표시됩니다.

```csharp
public decimal PeakTimePremium(DateTime timeOfToll, bool inbound) =>
    (IsWeekDay(timeOfToll), GetTimeBand(timeOfToll), inbound) switch
    {
        (true, TimeBand.MorningRush, true)  => 2.00m,
        (true, TimeBand.MorningRush, false) => 1.00m,
        (true, TimeBand.Daytime,     _)     => 1.50m,
        (true, TimeBand.EveningRush, true)  => 1.00m,
        (true, TimeBand.EveningRush, false) => 2.00m,
        (true, TimeBand.Overnight,   _)     => 0.75m,
        (false, _,                   _)     => 1.00m,
    };
```

마지막으로 정규 가격을 납부하는 두 번의 교통 체증 시간을 제거할 수 있습니다. 해당 암(arm)을 제거하면 마지막 스위치 암(arm)에서 `false`를 삭제(`_`)로 바꿀 수 있습니다. 완료된 메서드는 다음과 같습니다.

[!code-csharp[SimplifiedTuplePattern](../../../samples/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#FinalTuplePattern)]

이 예제는 패턴 일치의 장점 중 하나를 강조 표시합니다. 패턴 분기는 순서대로 평가됩니다. 이전 분기가 이후 사례 중 하나를 처리하도록 분기를 재배열하는 경우 컴파일러는 접근할 수 없는 코드에 대해 경고합니다. 이 언어 규칙을 사용하면 코드가 변경되지 않는다는 확신과 함께 앞의 단순화 작업을 더 쉽게 수행할 수 있습니다.

패턴 일치는 일부 유형의 코드를 더 쉽게 읽을 수 있도록 해주며 클래스에 코드를 추가할 수 없을 때 개체 지향 기술에 대한 대안을 제공합니다. 클라우드에서는 데이터와 기능이 별도로 구분되지 않습니다. 데이터의 모양과 데이터에 대한 작업을 반드시 함께 설명할 필요는 없습니다.   이 자습서에서는 원래 함수와 완전히 다른 방식으로 기존 데이터를 사용했습니다. 해당 형식을 확장할 수 없더라도 패턴 일치를 통해 해당 형식을 재정의하는 기능을 작성할 수 있었습니다.

## <a name="next-steps"></a>다음 단계

완료된 코드는 [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/patterns/finished) GitHub 리포지토리에서 다운로드할 수 있습니다. 혼자 패턴을 살펴보고 이 기술을 일반적인 코딩 활동에 추가하세요. 이 기술을 학습하면 다른 방법으로 문제에 접근하고 새 기능을 만들 수 있습니다.
