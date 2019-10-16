---
title: Azure Event Grid 서버 리스 앱
description: Azure Event Grid는 이벤트 당 종 량 제 모델을 통해 안정적으로 이벤트를 전달 하 고 라우팅할 수 있는 서버 리스 솔루션입니다.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 4970130ede0c96c645129ee6c8c7d54cb1114042
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577576"
---
# <a name="event-grid"></a>Event Grid

[Azure Event Grid](/azure/event-grid/overview) 는 이벤트 기반 응용 프로그램에 대 한 서버 리스 인프라를 제공 합니다. 모든 원본에서 Event Grid에 게시 하 고 모든 플랫폼에서 메시지를 사용할 수 있습니다. 또한 Event Grid는 응용 프로그램과의 통합을 간소화 하기 위해 Azure 리소스의 이벤트를 기본적으로 지원 합니다. 예를 들어 blob storage 이벤트를 구독 하 여 파일이 업로드 될 때 앱에 알릴 수 있습니다. 그러면 응용 프로그램은 다른 클라우드 또는 온-프레미스 응용 프로그램에서 사용 하는 사용자 지정 event grid 메시지를 게시할 수 있습니다. Event Grid은 대규모 확장을 안정적으로 처리할 수 있도록 작성 되었습니다. 필요한 인프라를 설정 하는 오버 헤드 없이 메시지를 게시 하 고 구독할 수 있는 이점을 얻을 수 있습니다.

![Event Grid 로고](./media/event-grid-logo.png)

Event grid의 주요 기능은 다음과 같습니다.

* 완전히 관리 되는 이벤트 라우팅입니다.
* 대규모로 거의 실시간으로 이벤트를 전달 합니다.
* Azure 내부 및 외부 모두에서 광범위 한 범위를 제공 합니다.

## <a name="scenarios"></a>시나리오

Event Grid는 여러 가지 시나리오를 다룹니다. 이 섹션에서는 가장 일반적인 세 가지 방법에 대해 설명 합니다.

### <a name="ops-automation"></a>Ops 자동화

![Ops 자동화](./media/ops-automation.png)

Event Grid는 인프라가 프로 비전 될 때 [Azure Automation](https://docs.microsoft.com/azure/automation) 에 게 알려 자동화를 가속화 하 고 정책 적용을 간소화 하는 데 도움이 됩니다.

### <a name="application-integration"></a>응용 프로그램 통합

![응용 프로그램 통합](./media/app-integration.png)

Event Grid를 사용 하 여 앱을 다른 서비스에 연결할 수 있습니다. 표준 HTTP 프로토콜을 사용 하는 경우에도 레거시 앱을 쉽게 수정 하 여 Event Grid 메시지를 게시할 수 있습니다. 웹 후크는 다른 서비스 및 플랫폼에서 Event Grid 메시지를 사용 하는 데 사용할 수 있습니다.

### <a name="serverless-apps"></a>서버 리스 앱

![서버 리스 앱](./media/serverless-apps.png)

Event Grid Azure Functions, Logic Apps 또는 사용자 지정 코드를 트리거할 수 있습니다. Event Grid를 사용할 경우의 주요 혜택은 이벤트 발생 시 *푸시* 메커니즘을 사용 하 여 메시지를 보내는 것입니다. 밀어넣기 아키텍처는 더 적게 사용 되는 리소스를 사용 하며 *폴링* 메커니즘 보다 효율적으로 확장 됩니다. 폴링은 정기적으로 업데이트를 확인 해야 합니다.

## <a name="event-grid-vs-other-azure-messaging-services"></a>Event Grid 및 기타 Azure 메시징 서비스

Azure는 [Event Hubs](https://docs.microsoft.com/azure/event-hubs) 및 [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging)를 비롯 한 여러 메시징 서비스를 제공 합니다. 각는 특정 사용 사례 집합을 해결 하도록 설계 되었습니다. 다음 다이어그램에서는 서비스 간의 차이점에 대 한 개략적인 개요를 제공 합니다.

![Azure 메시징 비교](./media/azure-messaging-services.png)

자세히 비교 하려면 [메시징 서비스 비교](https://docs.microsoft.com/azure/event-grid/compare-messaging-services)를 참조 하세요.

## <a name="performance-targets"></a>성능 목표

Event Grid 사용 하 여 다음과 같은 성능 보장을 활용할 수 있습니다.

* 99 번째 백분위 수에서 종단 간 대기 시간을 초이 합니다.
* 99.99% 가용성.
* 지역별 초당 1000만 이벤트 수입니다.
* 1억 지역 당 구독.
* 50-ms 게시자 대기 시간입니다.
* 1 일의 보장 된 배달에 대해 지 수 백오프를 사용 하 여 24 시간을 다시 시도 합니다.
* 투명 한 지역 장애 조치 (failover)

## <a name="event-grid-schema"></a>Event Grid 스키마

Event Grid 표준 스키마를 사용 하 여 사용자 지정 이벤트를 래핑합니다. 스키마는 사용자 지정 데이터 요소를 래핑하는 봉투 (envelope)와 같습니다. 메시지 Event Grid 예는 다음과 같습니다.

```json
[{
    "id": "03e24f21-a955-43cc-8921-1f61a6081ce0",
    "eventType": "myCustomEvent",
    "subject": "foo/bar/12",
    "eventTime": "2018-09-22T10:36:01+00:00",
    "data": {
        "favoriteColor": "blue",
        "favoriteAnimal": "panther",
        "favoritePlanet": "Jupiter"
    },
    "dataVersion": "1.0"
}]
```

메시지에 대 한 모든 내용은 속성을 `data` 제외 하 고 표준입니다. 메시지를 검사 하 고 `eventType` 및 `dataVersion` 를 사용 하 여 페이로드의 사용자 지정 부분을 deserialize 할 수 있습니다.

## <a name="azure-resources"></a>: Azure 리소스

Event Grid를 사용할 경우의 주요 혜택은 Azure에서 자동으로 생성 되는 메시지입니다. Azure에서 리소스는 다양 한 이벤트를 구독할 수 있는 *토픽* 에 자동으로 게시 됩니다. 다음 표에서는 자동으로 사용할 수 있는 리소스 유형, 메시지 유형 및 이벤트를 보여 줍니다.

| Azure 리소스 | 이벤트 유형 | 설명 |
| -------------- | ---------- | ----------- |
| Azure 구독 | Microsoft.Resources.ResourceWriteSuccess | 리소스 만들기 또는 업데이트 작업이 성공 하면 발생 합니다. |
| | Microsoft.Resources.ResourceWriteFailure | 리소스 만들기 또는 업데이트 작업이 실패할 때 발생 합니다. |
| | Microsoft.Resources.ResourceWriteCancel | 리소스 만들기 또는 업데이트 작업이 취소 될 때 발생 합니다. |
|  | Microsoft.Resources.ResourceDeleteSuccess | 리소스 삭제 작업이 성공 하면 발생 합니다. |
|  | Microsoft.Resources.ResourceDeleteFailure | 리소스 삭제 작업이 실패 하는 경우 발생 합니다. |
| | Microsoft.Resources.ResourceDeleteCancel | 리소스 삭제 작업이 취소 되 면 발생 합니다. 이 이벤트는 템플릿 배포가 취소 될 때 발생 합니다. |
| Blob Storage | Microsoft.Storage.BlobCreated | Blob을 만들 때 발생 합니다. |
| | Microsoft.Storage.BlobDeleted | Blob이 삭제 될 때 발생 합니다. |
| 이벤트 허브 | Microsoft.EventHub.CaptureFileCreated | 캡처 파일을 만들 때 발생 합니다.
| IoT Hub | Microsoft.Devices.DeviceCreated | 장치가 IoT hub에 등록 될 때 게시 됩니다. |
| | Microsoft.Devices.DeviceDeleted | IoT hub에서 장치를 삭제할 때 게시 됩니다. |
| 리소스 그룹 | Microsoft.Resources.ResourceWriteSuccess | 리소스 만들기 또는 업데이트 작업이 성공 하면 발생 합니다. |
| | Microsoft.Resources.ResourceWriteFailure | 리소스 만들기 또는 업데이트 작업이 실패할 때 발생 합니다. |
| | Microsoft.Resources.ResourceWriteCancel | 리소스 만들기 또는 업데이트 작업이 취소 될 때 발생 합니다. |
| | Microsoft.Resources.ResourceDeleteSuccess | 리소스 삭제 작업이 성공 하면 발생 합니다. |
| | Microsoft.Resources.ResourceDeleteFailure | 리소스 삭제 작업이 실패 하는 경우 발생 합니다. |
| | Microsoft.Resources.ResourceDeleteCancel | 리소스 삭제 작업이 취소 되 면 발생 합니다. 이 이벤트는 템플릿 배포가 취소 될 때 발생 합니다. |

자세한 내용은 [Azure Event Grid 이벤트 스키마](https://docs.microsoft.com/azure/event-grid/event-schema)를 참조 하세요.

온-프레미스에서 실행 되는 응용 프로그램을 비롯 한 모든 종류의 응용 프로그램에서 Event Grid에 액세스할 수 있습니다.

## <a name="conclusion"></a>결론

이 장에서는 Azure Functions, Logic Apps 및 Event Grid으로 구성 된 Azure 서버를 사용 하지 않는 플랫폼에 대해 알아보았습니다. 이러한 리소스를 사용 하 여 완전히 서버를 사용 하지 않는 앱 아키텍처를 빌드하거나 다른 클라우드 리소스 및 온-프레미스 서버와 상호 작용 하는 하이브리드 솔루션을 만들 수 있습니다. 서버를 사용 하지 않는 데이터 플랫폼 (예: [AZURE SQL](https://docs.microsoft.com/azure/sql-database) 또는 [CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction))과 결합 하 여 완전히 관리 되는 클라우드 네이티브 응용 프로그램을 빌드할 수 있습니다.

## <a name="recommended-resources"></a>권장 리소스

* [App service 계획](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)
* [Application Insights](https://docs.microsoft.com/azure/application-insights)
* [Application Insights 분석](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)
* [Microsoft 서버 리스를 사용 하 여 앱을 클라우드로 가져오기 Azure Functions](https://channel9.msdn.com/events/Connect/2017/E102)
* [Azure Event Grid](https://docs.microsoft.com/azure/event-grid/overview)
* [Azure Event Grid 이벤트 스키마](https://docs.microsoft.com/azure/event-grid/event-schema)
* [Azure Event Hubs](https://docs.microsoft.com/azure/event-hubs)
* [Azure Functions 설명서](https://docs.microsoft.com/azure/azure-functions)
* [Azure Functions 트리거 및 바인딩 개념](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)
* [Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps)
* [Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging)
* [Azure Table Storage](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)
* [1. x 및 2.x 함수를 비교 합니다.](https://docs.microsoft.com/azure/azure-functions/functions-versions)
* [Azure 온-프레미스 데이터 게이트웨이를 사용 하 여 온-프레미스 데이터 원본에 연결](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)
* [Azure Portal에서 첫 번째 함수를 만듭니다.](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)
* [Azure CLI를 사용 하 여 첫 번째 함수 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli)
* [Visual Studio를 사용 하 여 첫 번째 함수 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio)
* [함수 지원 언어](https://docs.microsoft.com/azure/azure-functions/supported-languages)
* [모니터 Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring)
* [Azure Functions 프록시 작업](https://docs.microsoft.com/azure/azure-functions/functions-proxies)

>[!div class="step-by-step"]
>[이전](logic-apps.md)
>[다음](durable-azure-functions.md)
