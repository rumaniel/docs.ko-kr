---
title: 내구성이 있는 Azure 함수-서버 리스 앱
description: 지속적인 Azure 함수는 코드에서 상태 저장 워크플로를 사용 하도록 Azure Functions 런타임을 확장 합니다.
author: cecilphillip
ms.author: cephilli
ms.date: 06/26/2018
ms.openlocfilehash: f7ee74926d6658042120113b49dc763383881423
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577516"
---
# <a name="durable-azure-functions"></a>지속 가능한 Azure Functions

Azure Functions를 사용 하 여 서버를 사용 하지 않는 응용 프로그램을 만드는 경우 일반적으로 작업은 상태 비저장 방식으로 실행 되도록 설계 됩니다. 이 디자인을 선택 하는 이유는 플랫폼이 확장 될 때 코드가 실행 되는 서버를 파악 하기 어렵기 때문입니다. 또한 지정 된 지점에서 활성 상태인 인스턴스 수를 파악 하기 어렵습니다. 그러나 프로세스의 현재 상태를 알고 있어야 하는 응용 프로그램의 클래스가 있습니다. 온라인 스토어에 주문을 제출 하는 프로세스를 고려 합니다. 체크 아웃 작업은 프로세스의 상태를 알고 있어야 하는 여러 작업으로 구성 된 워크플로 일 수 있습니다. 이러한 정보에는 제품 인벤토리에 포함 될 수 있으며, 고객이 계정에 크레딧을 보유 하 고 있는 경우 신용 카드를 처리 하는 결과도 여기에 포함 될 수 있습니다. 이러한 작업은 자체 내부 워크플로 또는 타사 시스템의 서비스 일 수도 있습니다.

현재 내부 및 외부 시스템 간의 응용 프로그램 상태를 조정 하는 데 도움이 되는 다양 한 패턴이 있습니다. 이는 중앙 집중식 큐 시스템, 분산 키-값 저장소 또는 공유 데이터베이스를 사용 하 여 해당 상태를 관리 하는 솔루션에서 일반적으로 발생 합니다. 그러나 이제 프로 비전 하 고 관리 해야 하는 모든 추가 리소스를 제공 합니다. 서버를 사용 하지 않는 환경에서는 코드를 사용 하 여 이러한 리소스를 수동으로 조정 해야 할 수 있습니다. Azure Functions는 Durable Functions 이라는 상태 저장 함수를 만드는 대안을 제공 합니다.

Durable Functions은 코드에서 상태 저장 워크플로를 정의할 수 있도록 하는 Azure Functions 런타임에 대 한 확장입니다. Durable Functions 확장은 워크플로를 작업으로 분리 하 여 상태를 관리 하 고, 진행률 검사점을 만들고, 서버 전체에서 함수 호출의 분포를 처리할 수 있습니다. 백그라운드에서는 Azure Storage 계정을 사용 하 여 실행 기록을 유지 하 고, 작업 함수를 예약 하 고, 응답을 검색 합니다. 서버를 사용 하지 않는 코드는 해당 저장소 계정에서 지속형 정보와 상호 작용 해서는 안 되며 일반적으로 개발자가 상호 작용 해야 하는 것은 아닙니다.

## <a name="triggering-a-stateful-workflow"></a>상태 저장 워크플로 트리거

Durable Functions의 상태 저장 워크플로는 두 개의 기본 구성 요소로 나눌 수 있습니다. 오케스트레이션 및 작업 트리거 트리거 및 바인딩은 서버를 시작 하 고 입력을 수신 하 고 결과를 반환할 때 서버를 사용 하지 않는 함수를 알리도록 설정 하기 위해 Azure Functions에서 사용 하는 핵심 구성 요소입니다.

### <a name="working-with-the-orchestration-client"></a>오케스트레이션 클라이언트 작업

오케스트레이션은 Azure Functions에서 트리거된 작업의 다른 스타일과 비교할 때 고유 합니다. Durable Functions를 사용 하면 작업을 완료 하는 데 몇 시간 또는 며칠 정도 걸릴 수 있는 함수를 실행할 수 있습니다. 이러한 유형의 동작은 실행 중인 오케스트레이션의 상태를 확인 하거나, 미리 종료 하거나, 외부 이벤트에 대 한 알림을 보낼 수 있어야 합니다.

이러한 경우 Durable Functions 확장은 오케스트레이션 함수와 상호 작용할 `DurableOrchestrationClient` 수 있도록 하는 클래스를 제공 합니다. `OrchestrationClientAttribute` 바인딩을 사용 하 여 오케스트레이션 클라이언트에 액세스할 수 있습니다. 일반적으로이 특성은 `HttpTrigger` 또는 `ServiceBusTrigger`와 같은 다른 트리거 형식에 포함 시킬 수 있습니다. 원본 함수가 트리거된 후에는 orchestration 클라이언트를 사용 하 여 orchestrator 함수를 시작할 수 있습니다.

```csharp
[FunctionName("KickOff")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "POST")]HttpRequestMessage req,
    [OrchestrationClient ] DurableOrchestrationClient<orchestrationClient>)
{
    OrderRequestData data = await req.Content.ReadAsAsync<OrderRequestData>();

    string instanceId = await orchestrationClient.StartNewAsync("PlaceOrder", data);

    return orchestrationClient.CreateCheckStatusResponse(req, instanceId);
}
```

### <a name="the-orchestrator-function"></a>Orchestrator 함수

Azure Functions의 OrchestrationTriggerAttribute를 사용 하 여 함수에 주석을 달아 오 케 스트레이 터 함수로 함수를 표시 합니다. 상태 저장 워크플로를 구성 하는 다양 한 작업을 관리 해야 합니다.

Orchestrator 함수는 OrchestrationTriggerAttribute 이외의 바인딩을 사용할 수 없습니다. 이 특성은 DurableOrchestrationContext의 매개 변수 형식에만 사용할 수 있습니다. 함수 시그니처의 입력 deserialization은 지원 되지 않으므로 다른 입력을 사용할 수 없습니다. Orchestration 클라이언트에서 제공 하는 입력을 가져오려면 getinput\<T\> 메서드를 사용 해야 합니다.

또한 오케스트레이션 함수의 반환 형식은 void, Task 또는 JSON serializable 값 이어야 합니다.

> *오류 처리 코드를 간결 하 게 유지 했습니다.*

```csharp
[FunctionName("PlaceOrder")]
public static async Task<string> PlaceOrder([OrchestrationTrigger] DurableOrchestrationContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    await context.CallActivityAsync<bool>("CheckAndReserveInventory", orderData);
    await context.CallActivityAsync<string>("ProcessPayment", orderData);

    string trackingNumber = await context.CallActivityAsync<string>("ScheduleShipping", orderData);
    await context.CallActivityAsync<string>("EmailCustomer", trackingNumber);

    return trackingNumber;
}
```

오케스트레이션의 여러 인스턴스를 동시에 시작 하 고 실행할 수 있습니다. 에서 메서드 `StartNewAsync` 를 호출 하면 오케스트레이션의 새 인스턴스가 시작됩니다.`DurableOrchestrationClient` 메서드는 오케스트레이션이 시작 `Task<string>` 될 때 완료 되는를 반환 합니다. 오케스트레이션이 30 초 내 `TimeoutException` 에 시작 되지 않은 경우 형식의 예외가 throw 됩니다.

`Task<string>` 완료`StartNewAsync` 된는 오케스트레이션 인스턴스의 고유 ID를 포함 해야 합니다. 이 인스턴스 ID는 특정 오케스트레이션에 대 한 작업을 호출 하는 데 사용할 수 있습니다. 오케스트레이션은 상태 또는 송신 이벤트 알림에 대해 쿼리할 수 있습니다.

### <a name="the-activity-functions"></a>작업 함수

활동 함수는 워크플로를 만들기 위해 오케스트레이션 함수 내에 함께 구성 된 불연속 작업입니다. 다음은 대부분의 실제 작업을 수행 하는 위치입니다. 비즈니스 논리, 장기 실행 프로세스 및 더 큰 솔루션에 대 한 퍼즐 조각을 나타냅니다.

는 `ActivityTriggerAttribute` 형식의`DurableActivityContext`함수 매개 변수에 주석을 추가 하는 데 사용 됩니다. 주석을 사용 하면 함수가 활동 함수로 사용 될 것 이라는 것을 런타임에 알립니다. 작업 함수에 대 한 입력 값은 `GetInput<T>` `DurableActivityContext` 매개 변수의 메서드를 사용 하 여 검색 됩니다.

오케스트레이션 함수와 마찬가지로 작업 함수의 반환 형식은 void, Task 또는 JSON serializable 값 이어야 합니다.

작업 함수 내에서 throw 되는 처리 되지 않은 예외는 호출 오 케 스트레이 터 함수로 전송 되 고로 `TaskFailedException`표시 됩니다. 이 시점에서 오류를 catch 하 여 오 케 스트레이 터에 기록할 수 있으며 작업을 다시 시도할 수 있습니다.

```csharp
[FunctionName("CheckAndReserveInventory")]
public static bool CheckAndReserveInventory([ActivityTrigger] DurableActivityContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    // Connect to inventory system and try to reserve items
    return true;
}
```

## <a name="recommended-resources"></a>권장 리소스

* [Durable Functions](https://docs.microsoft.com/azure/azure-functions/durable-functions-overview)
* [Durable Functions에 대 한 바인딩](https://docs.microsoft.com/azure/azure-functions/durable-functions-bindings)
* [Durable Functions에서 인스턴스 관리](https://docs.microsoft.com/azure/azure-functions/durable-functions-instance-management)

>[!div class="step-by-step"]
>[이전](event-grid.md)
>[다음](orchestration-patterns.md)
