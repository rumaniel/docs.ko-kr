---
title: C#의 비동기 프로그래밍
description: async, await 및 Task를 사용하여 비동기 프로그래밍을 지원하는 C# 언어에 대해 간략히 설명합니다.<T>
ms.date: 03/18/2019
ms.openlocfilehash: 4ed48a2e74dde5ae0f24ebd680ace133e05e15d4
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70167886"
---
# <a name="asynchronous-programming-with-async-and-await"></a>async 및 await를 사용한 비동기 프로그래밍

TAP(Task 비동기 프로그래밍) 모델은 비동기 코드에 대한 추상화를 제공합니다. 항상 그렇듯이 코드는 일련의 명령문으로 작성합니다. 다음 명령문이 시작되기 전에 각 명령문이 완료되는 것처럼 해당 코드를 읽을 수 있습니다. 이러한 명령문 중 일부에서 작업을 시작하고 진행 중인 작업을 나타내는 <xref:System.Threading.Tasks.Task>를 반환할 수 있으므로 컴파일러는 여러 가지 변환을 수행합니다.

이 구문의 목표는 일련의 명령문처럼 읽지만 외부 리소스 할당과 작업 완료 시점에 따라 훨씬 더 복잡한 순서로 실행되는 코드를 사용하도록 설정하는 것입니다. 사람이 비동기 작업이 포함된 프로세스에 대한 지침을 제공하는 방법과 비슷합니다. 이 문서에서는 `async` 및 `await` 키워드를 사용하여 일련의 비동기 명령이 포함된 코드를 쉽게 추론할 수 있는 방법을 알아보기 위해 아침 식사를 준비하기 위한 지침의 예를 사용합니다. 아침 식사를 준비하는 방법을 설명하기 위해 작성하는 지침은 다음 목록과 같습니다.

1. 커피 한 잔을 따릅니다.
1. 팬을 데운 다음, 계란 프라이 두 개를 만듭니다.
1. 베이컨 세 조각을 튀깁니다.
1. 빵 두 조각을 굽습니다.
1. 토스트에 버터와 잼을 바릅니다.
1. 오렌지 주스 한잔을 따릅니다.

요리에 대한 경험이 있는 경우 이러한 지침은 **비동기적으로** 실행됩니다. 계란 프라이를 위해 팬을 데우기 시작한 다음, 베이컨을 시작합니다. 토스터에 빵을 넣고 계란 프라이를 시작합니다. 프로세스의 각 단계에서 작업을 시작한 다음, 주의가 필요한 작업에 주의를 돌립니다.

아침을 요리하는 것은 병렬로 수행되지 않는 비동기 작업의 좋은 예입니다. 한 사람(또는 스레드)이 이러한 모든 작업을 처리할 수 있습니다. 아침 식사 비유를 계속하면 첫 번째 작업이 완료되기 전에 다음 작업을 시작하여 한 사람이 비동기적으로 아침 식사를 만들 수 있습니다. 누군가 보고 있는지 여부에 관계없이 요리는 계속됩니다. 계란 프라이를 위해 팬을 데우기 시작하자 말자 베이컨을 튀기기 시작할 수 있습니다. 베이컨 튀김이 시작되면 토스터에 빵을 넣을 수 있습니다.

병렬 알고리즘의 경우 여러 요리사(또는 스레드)가 필요합니다. 한 사람은 계란을 만들고 또 한 사람은 베이컨을 만드는 방식으로 진행될 것입니다. 즉 각각은 하나의 작업에만 집중할 것입니다. 각 요리사(또는 스레드)는 베이컨이 뒤집을 준비가 되거나 토스트가 나올 때까지 동기적으로 차단됩니다. 

이제 C# 문으로 작성된 동일한 명령을 고려합니다.

[!code-csharp[SynchronousBreakfast](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-starter/Program.cs#Main)]

컴퓨터에서는 사람들이 수행하는 것과 같은 방식으로 이러한 명령을 해석하지 않습니다. 다음 명령문으로 이동하기 전에 작업이 완료될 때까지 컴퓨터는 각 명령문에서 차단됩니다. 이로 인해 불만족스러운 아침 식사를 만듭니다. 이전 작업이 완료될 때까지 이후 작업을 시작할 수 없었습니다. 아침 식사를 만드는 데 훨씬 더 오래 걸리고, 일부 음식은 식은 채로 제공되었을 것입니다. 

컴퓨터에서 위의 명령을 비동기적으로 실행하게 하려면 비동기 코드를 작성해야 합니다.

이러한 문제는 현재 작성하는 프로그램에 중요합니다. 클라이언트 프로그램을 작성할 때 UI에서 사용자 입력에 응답해야 합니다. 웹에서 데이터를 다운로드하는 동안 애플리케이션에서 휴대폰이 중지된 것처럼 표시하면 안 됩니다. 서버 프로그램을 작성하는 경우 스레드가 차단되지 않도록 합니다. 이러한 스레드는 다른 요청을 처리할 수 있습니다. 비동기 대안이 있을 때 동기 코드를 사용하면 비용이 적게 드는 규모 확장 기능이 저하됩니다. 차단된 스레드에 대한 비용을 지불합니다.

성공적인 최신 애플리케이션에는 비동기 코드가 필요합니다. 언어 지원 없이 비동기 코드를 작성하는 경우 콜백, 완료 이벤트 또는 코드의 원래 의도를 모호하게 하는 다른 수단이 필요했습니다. 동기 코드의 장점은 이해하기 쉽다는 것입니다. 단계별 작업을 통해 쉽게 스캔하고 이해할 수 있습니다. 기존의 비동기 모델에서는 코드의 기본 동작이 아니라 코드의 비동기적 특성에 집중할 수 밖에 없었습니다.

## <a name="dont-block-await-instead"></a>차단하는 대신 대기

앞의 코드에서는 동기 코드를 구성하여 비동기 작업을 수행하는 잘못된 사례를 보여 줍니다. 작성한 대로 이 코드는 실행되는 스레드에서 다른 작업을 수행하지 못하도록 차단합니다. 작업이 진행되는 동안에는 중단되지 않습니다. 마치 빵을 넣은 후 토스터를 쳐다보는 것과 같습니다. 토스트가 나오기 전까지 아무하고도 대화하지 않을 것입니다. 

먼저 이 코드를 업데이트하여 작업이 실행되는 동안 스레드가 차단되지 않도록 하겠습니다. `await` 키워드는 작업을 차단하지 않는 방식으로 시작한 다음, 해당 작업이 완료되면 실행을 계속합니다. 간단한 비동기 버전의 아침 식사 준비 코드는 다음과 같습니다.

[!code-csharp[SimpleAsyncBreakfast](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-V2/Program.cs#Main)]

이 코드는 계란이나 베이컨을 요리하는 동안 차단되지 않습니다. 하지만 이 코드는 다른 작업을 시작하지 않습니다. 토스트가 토스터에 넣어져 나올 때까지 쳐다보고 있습니다. 그러나 적어도 주의를 끌려고 하는 누구에게나 응답할 수는 있습니다. 여러 주문을 받는 식당에서 요리사는 첫 번째 요리를 하는 동안 또 다른 아침 식사 준비를 시작할 수 있습니다.

시작했지만 아직 완료되지 않은 작업을 기다리는 동안 아침 식사 작업 스레드가 차단되지 않습니다. 일부 애플리케이션의 경우 이 변경만으로 충분합니다. GUI 애플리케이션은 이 변경만으로도 사용자에게 응답합니다. 그러나 지금 시나리오에서는 더 많은 작업이 필요합니다. 각 구성 요소 작업이 순차적으로 실행되지 않도록 해야 합니다. 이전 작업이 완료되기를 기다리기 전에 각 구성 요소 작업을 시작하는 것이 좋습니다.

## <a name="start-tasks-concurrently"></a>동시에 작업 시작

대부분의 시나리오에서는 독립적인 몇 가지 작업을 즉시 시작하려고 합니다. 그런 다음, 각 작업이 완료되면 준비된 다른 작업을 계속할 수 있습니다. 아침 식사 비유에서 이는 아침 식사를 더 빨리 준비하는 방법입니다. 모든 것을 거의 동시에 완료할 수 있습니다. 이에 따라 따뜻한 아침 식사가 준비됩니다.

<xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 및 관련 형식은 진행 중인 작업을 추론하는 데 사용할 수 있는 클래스입니다. 이를 통해 아침 식사를 준비하는 방법과 더 비슷한 코드를 작성할 수 있습니다. 계란, 베이컨 및 토스트 요리를 동시에 시작할 수 있을 것입니다. 각 요리에 필요한 작업이 있으므로 해당 작업에 주의를 기울이고, 다음 작업을 처리한 다음, 주의가 필요한 다른 작업을 기다립니다.

작업을 시작하고, 해당 작업을 나타내는 <xref:System.Threading.Tasks.Task> 개체를 유지합니다. 결과를 사용하기 전에 각 작업을 기다립니다(`await`).

아침 식사 코드를 이처럼 변경해 보겠습니다. 첫 번째 단계는 작업을 기다리지 않고 시작될 때 해당 작업을 저장하는 것입니다.

```csharp
Coffee cup = PourCoffee();
Console.WriteLine("coffee is ready");
Task<Egg> eggTask = FryEggs(2);
Egg eggs = await eggTask;
Console.WriteLine("eggs are ready");
Task<Bacon> baconTask = FryBacon(3);
Bacon bacon = await baconTask;
Console.WriteLine("bacon is ready");
Task<Toast> toastTask = ToastBread(2);
Toast toast = await toastTask;
ApplyButter(toast);
ApplyJam(toast);
Console.WriteLine("toast is ready");
Juice oj = PourOJ();
Console.WriteLine("oj is ready");

Console.WriteLine("Breakfast is ready!");
```

다음으로, 아침 식사를 제공하기 전에 베이컨과 달걀에 대한 `await` 문을 메서드 끝으로 이동할 수 있습니다.

```csharp
Coffee cup = PourCoffee();
Console.WriteLine("coffee is ready");
Task<Egg> eggTask = FryEggs(2);
Task<Bacon> baconTask = FryBacon(3);
Task<Toast> toastTask = ToastBread(2);
Toast toast = await toastTask;
ApplyButter(toast);
ApplyJam(toast);
Console.WriteLine("toast is ready");
Juice oj = PourOJ();
Console.WriteLine("oj is ready");

Egg eggs = await eggTask;
Console.WriteLine("eggs are ready");
Bacon bacon = await baconTask;
Console.WriteLine("bacon is ready");

Console.WriteLine("Breakfast is ready!");
```

앞의 코드가 더 잘 작동합니다. 모든 비동기 작업을 한 번에 시작합니다. 결과가 필요할 때만 각 작업을 기다립니다. 앞의 코드는 다른 마이크로서비스를 요청한 다음, 결과를 단일 페이지로 결합하는 웹 애플리케이션의 코드와 비슷할 수 있습니다. 모든 요청을 즉시 수행한 다음, 이러한 모든 작업을 기다리고(`await`) 웹 페이지를 구성합니다.

## <a name="composition-with-tasks"></a>작업 구성

 토스트를 제외한 모든 아침 식사가 동시에 준비되었습니다. 토스트를 만드는 것은 비동기 작업(빵 굽기)과 동기 작업(버터와 잼 바르기)의 구성입니다. 이 코드를 업데이트하면 중요한 개념을 알 수 있습니다.

> [!IMPORTANT]
> 동기 작업이 뒤따르는 비동기 작업으로 구성된 작업은 비동기 작업입니다. 즉 작업의 일부가 비동기이면 전체 작업이 비동기입니다.

이전 코드에서는 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체를 사용하여 실행 중인 작업을 유지할 수 있음을 보여 주었습니다. 결과를 사용하기 전에 각 작업을 기다립니다(`await`). 다음 단계는 다른 작업의 결합을 나타내는 메서드를 만드는 것입니다. 아침 식사를 제공하기 전에 빵을 구운 후에 버터와 잼을 바르는 것을 나타내는 작업을 기다리려고 합니다. 이 작업은 다음 코드를 사용하여 나타낼 수 있습니다.

[!code-csharp[ComposeToastTask](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-V3/Program.cs#ComposeToastTask)]

앞의 메서드에서 해당 시그니처에는 `async` 한정자가 있습니다. 이 경우 이 메서드에서 비동기 작업이 포함된 `await` 문을 포함하고 있다고 컴파일러에 알립니다. 이 메서드는 빵을 구운 다음, 버터와 잼을 바르는 작업을 나타내며, 이러한 세 가지 작업의 구성을 나타내는 <xref:System.Threading.Tasks.Task%601>를 반환합니다. 이제 main 코드 블록은 다음과 같습니다.

[!code-csharp[StartConcurrentTasks](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-V3/Program.cs#Main)]

앞의 변경에서는 비동기 코드를 사용하는 데 있어 중요한 기술을 보여 주었습니다. 작업을 반환하는 새 메서드로 구분하여 작업을 구성합니다. 해당 작업을 기다리는 시기를 선택할 수 있습니다. 다른 작업을 동시에 시작할 수 있습니다.

## <a name="await-tasks-efficiently"></a>효율적인 작업 대기

`Task` 클래스의 메서드를 사용하여 앞의 코드 끝에 있는 일련의 `await` 문을 향상시킬 수 있습니다. 이러한 API 중 하나인 <xref:System.Threading.Tasks.Task.WhenAll%2A>은 다음 코드와 같이 인수 목록의 모든 작업이 완료되면 완료된 <xref:System.Threading.Tasks.Task>를 반환합니다.

```csharp
await Task.WhenAll(eggTask, baconTask, toastTask);
Console.WriteLine("eggs are ready");
Console.WriteLine("bacon is ready");
Console.WriteLine("toast is ready");
Console.WriteLine("Breakfast is ready!");
```

또 다른 옵션으로, 인수가 완료되면 완료된 `Task<Task>`를 반환하는 <xref:System.Threading.Tasks.Task.WhenAny%2A>를 사용하는 것입니다. 반환된 작업은 이미 완료되었음을 알고 있으므로 기다릴 수 있습니다. 다음 코드에서는 <xref:System.Threading.Tasks.Task.WhenAny%2A>를 사용하여 첫 번째 작업이 완료될 때까지 기다린 다음, 결과를 처리하는 방법을 보여 줍니다. 완료된 작업의 결과가 처리되면 완료된 작업을 `WhenAny`에 전달된 작업 목록에서 제거합니다.

[!code-csharp[AwaitAnyTask](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-final/Program.cs#AwaitAnyTask)]

이러한 모든 변경 이후에 `Main`의 최종 버전은 다음과 같습니다.

[!code-csharp[Final](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-final/Program.cs#Main)]

이 최종 코드는 비동기입니다. 이 코드는 아침 식사를 요리하는 방법을 더 정확하게 반영하고 있습니다. 앞의 코드를 이 문서의 첫 번째 코드 샘플과 비교해 보세요. 핵심 작업은 코드를 읽어 파악할 수 있습니다. 이 코드는 이 문서의 시작 부분에 나와 있는 아침 식사 준비 지침을 읽는 것과 동일한 방식으로 읽을 수 있습니다. `async` 및 `await` 언어 기능을 사용하면 모든 사용자가 작성된 이러한 지침을 따를 수 있습니다. 가능한 한 작업을 시작하지만 작업이 완료될 때까지 기다리는 것을 차단하지 않도록 합니다.
