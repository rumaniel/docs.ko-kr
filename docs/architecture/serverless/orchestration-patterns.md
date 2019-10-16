---
title: 오케스트레이션 패턴-서버 리스 앱
description: Azure 지 속성 함수 pr
author: cecilphillip
ms.author: cephilli
ms.date: 06/26/2018
ms.openlocfilehash: 18e13c5355490ef4a019ceda459114bdb6bfd539
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577406"
---
# <a name="orchestration-patterns"></a>오케스트레이션 패턴

Durable Functions를 사용 하면 서버를 사용 하지 않는 환경에서 장시간 실행 되는 불연속 작업으로 구성 된 상태 저장 워크플로를 쉽게 만들 수 있습니다. Durable Functions는 워크플로의 진행률을 추적 하 고 정기적으로 실행 기록의 검사점을 지정할 수 있으므로, 몇 가지 흥미로운 패턴을 구현 하는 데 적합 합니다.

## <a name="function-chaining"></a>함수 체인

일반적인 순차적 프로세스에서 활동은 특정 순서로 한 번 실행 해야 합니다. 필요에 따라 예정 된 작업에는 이전 함수의 출력이 필요할 수 있습니다. 작업 순서 지정에 대 한이 종속성은 실행의 함수 체인을 만듭니다.

Durable Functions를 사용 하 여이 워크플로 패턴을 구현 하는 경우의 혜택은 검사점을 수행할 수 있는 기능에서 비롯 됩니다. 서버가 충돌 하는 경우 네트워크 시간이 초과 되거나 다른 문제가 발생 하는 경우 지 속성 함수는 마지막으로 알려진 상태에서 다시 시작 하 고 다른 서버에 있는 경우에도 워크플로를 계속 실행할 수 있습니다.

```csharp
[FunctionName("PlaceOrder")]
public static async Task<string> PlaceOrder([OrchestrationTrigger] DurableOrchestrationContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    await context.CallActivityAsync<bool>("CheckAndReserveInventory", orderData);
    await context.CallActivityAsync<bool>("ProcessPayment", orderData);

    string trackingNumber = await context.CallActivityAsync<string>("ScheduleShipping", orderData);
    await context.CallActivityAsync<string>("EmailCustomer", trackingNumber);

    return trackingNumber;
}
```

위의 코드 샘플 `CallActivityAsync` 에서 함수는 데이터 센터의 가상 컴퓨터에서 지정 된 작업을 실행 하는 작업을 담당 합니다. Wait가 반환 되 고 기본 작업이 완료 되 면 실행이 기록 테이블에 기록 됩니다. 오 케 스트레이 터 함수의 코드는 작업 병렬 라이브러리의 친숙 한 구문과 async/wait 키워드를 사용할 수 있습니다.

다음 코드는 `ProcessPayment` 메서드가 표시 되는 것과 같은 간단한 예제입니다.

```csharp
[FunctionName("ProcessPayment")]
public static bool ProcessPayment([ActivityTrigger] DurableActivityContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    ApplyCoupons(orderData);
    if(IssuePaymentRequest(orderData)) {
        return true;
    }

    return false;
}
```

## <a name="asynchronous-http-apis"></a>비동기 HTTP Api

경우에 따라 워크플로는 완료 하는 데 비교적 오랜 시간이 걸리는 작업을 포함할 수 있습니다. Blob 저장소에 미디어 파일의 백업을 시작 하는 프로세스를 상상해 보세요. 미디어 파일의 크기와 양에 따라이 백업 프로세스를 완료 하는 데 몇 시간이 걸릴 수 있습니다.

이 시나리오 `DurableOrchestrationClient`에서는 실행 중인 워크플로의 상태를 확인 하는 기능이 유용 합니다. 를 사용 하 `HttpTrigger` 여 워크플로 `CreateCheckStatusResponse` 를 시작 하는 경우 메서드를 사용 하 여의 `HttpResponseMessage`인스턴스를 반환할 수 있습니다. 이 응답은 실행 중인 프로세스의 상태를 확인 하는 데 사용할 수 있는 페이로드의 URI를 클라이언트에 제공 합니다.

```csharp
[FunctionName("OrderWorkflow")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "POST")]HttpRequestMessage req,
    [OrchestrationClient ] DurableOrchestrationClient orchestrationClient)
{
    OrderRequestData data = await req.Content.ReadAsAsync<OrderRequestData>();

    string instanceId = await orchestrationClient.StartNewAsync("PlaceOrder", data);

    return orchestrationClient.CreateCheckStatusResponse(req, instanceId);
}
```

아래 샘플 결과는 응답 페이로드의 구조를 보여줍니다.

```json
{
    "id": "instanceId",
    "statusQueryGetUri": "http://host/statusUri",
    "sendEventPostUri": "http://host/eventUri",
    "terminatePostUri": "http://host/terminateUri"
}
```

기본 설정 된 HTTP 클라이언트를 사용 하 여 statusQueryGetUri에서 URI에 GET 요청을 수행 하 여 실행 중인 워크플로의 상태를 검사할 수 있습니다. 반환 된 상태 응답은 다음 코드와 유사 합니다.

```json
{
    "runtimeStatus": "Running",
    "input": {
        "$type": "DurableFunctionsDemos.OrderRequestData, DurableFunctionsDemos"
    },
    "output": null,
    "createdTime": "2018-01-01T00:22:05Z",
    "lastUpdatedTime": "2018-01-01T00:22:09Z"
}
```

프로세스가 계속 되 면 상태 응답이 **실패** 또는 **완료**로 변경 됩니다. 성공적으로 완료 되 면 페이로드의 **output** 속성은 반환 된 데이터를 포함 합니다.

## <a name="monitoring"></a>모니터링

간단한 되풀이 작업의 경우 CRON 식을 기반 `TimerTrigger` 으로 예약할 수 있는를 Azure Functions 제공 합니다. 타이머가 간단 하 고 수명이 짧은 작업에 적합 하지만 보다 유연한 예약을 수행 해야 하는 시나리오가 있을 수 있습니다. 이 시나리오는 모니터링 패턴 및 Durable Functions에서 도움이 될 수 있는 경우입니다.

Durable Functions를 사용 하면 유연한 일정 간격, 수명 관리 및 단일 오케스트레이션 함수에서 여러 모니터 프로세스를 만들 수 있습니다. 이 기능에 대 한 한 가지 사용 사례는 특정 임계값이 충족 되 면 완료 되는 주식 가격 변경에 대 한 감시자을 만드는 것입니다.

```csharp
[FunctionName("CheckStockPrice")]
public static async Task CheckStockPrice([OrchestrationTrigger] DurableOrchestrationContext context)
{
    StockWatcherInfo stockInfo = context.GetInput<StockWatcherInfo>();
    const int checkIntervalSeconds = 120;
    StockPrice initialStockPrice = null;

    DateTime fireAt;
    DateTime exitTime = context.CurrentUtcDateTime.Add(stockInfo.TimeLimit);

    while (context.CurrentUtcDateTime < exitTime)
    {
        StockPrice currentStockPrice = await context.CallActivityAsync<StockPrice>("GetStockPrice", stockInfo);

        if (initialStockPrice == null)
        {
            initialStockPrice = currentStockPrice;
            fireAt = context.CurrentUtcDateTime.AddSeconds(checkIntervalSeconds);
            await context.CreateTimer(fireAt, CancellationToken.None);
            continue;
        }

        decimal percentageChange = (initialStockPrice.Price - currentStockPrice.Price) /
                               ((initialStockPrice.Price + currentStockPrice.Price) / 2);

        if (Math.Abs(percentageChange) >= stockInfo.PercentageChange)
        {
            // Change threshold detected
            await context.CallActivityAsync("NotifyStockPercentageChange", currentStockPrice);
            break;
        }

        // Sleep til next polling interval
        fireAt = context.CurrentUtcDateTime.AddSeconds(checkIntervalSeconds);
        await context.CreateTimer(fireAt, CancellationToken.None);
    }
}
```

`DurableOrchestrationContext`의 `CreateTimer` 메서드는 다음 루프 호출에 대 한 일정을 설정 하 여 주식 가격 변경을 확인 합니다. `DurableOrchestrationContext`에는 UTC의 현재 DateTime 값을 가져오는 속성도있습니다.`CurrentUtcDateTime` 테스트를 위해 쉽게 모의이 속성 대신이 `DateTime.UtcNow` 속성을 사용 하는 것이 좋습니다.

## <a name="recommended-resources"></a>권장 리소스

* [Azure Durable Functions](https://docs.microsoft.com/azure/azure-functions/durable-functions-overview)
* [.NET Core 및 .NET Standard의 유닛 테스트](../../core/testing/index.md)

>[!div class="step-by-step"]
>[이전](durable-azure-functions.md)
>[다음](serverless-business-scenarios.md)
