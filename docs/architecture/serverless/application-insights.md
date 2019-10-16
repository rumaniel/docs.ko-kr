---
title: Application Insights 서버 리스 앱
description: Application Insights는 개발자가 웹 앱, 모바일 앱, 데스크톱 앱 및 마이크로 서비스의 문제를 감지, 심사 및 진단할 수 있도록 하는 서버 리스 진단 플랫폼입니다.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 1f5b99fba448c2c1c12139524ffdcd3708b3c956
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577726"
---
# <a name="telemetry-with-application-insights"></a>Application Insights 원격 분석

[Application Insights](https://docs.microsoft.com/azure/application-insights) 는 개발자가 웹 앱, 모바일 앱, 데스크톱 앱 및 마이크로 서비스의 문제를 감지, 심사 및 진단할 수 있도록 하는 서버 리스 진단 플랫폼입니다. 포털에서 스위치를 대칭 이동 하 여 함수 앱에 대 한 Application Insights를 켤 수 있습니다. Application Insights는 서버를 구성 하거나 사용자 고유의 데이터베이스를 설정 하지 않고도 이러한 모든 기능을 제공 합니다. 모든 Application Insights 기능을 앱과 자동으로 통합 하는 서비스로 제공 됩니다.

![Application Insights 로고](./media/application-insights-logo.png)

기존 앱에 Application Insights을 추가 하는 것은 응용 프로그램의 설정에 계측 키를 추가 하는 것 만큼 쉽습니다. Application Insights를 사용 하 여 다음을 수행할 수 있습니다.

* 함수 호출 수, 함수를 실행 하는 데 걸리는 시간, 예외 등의 메트릭에 따라 사용자 지정 차트 및 경고 만들기
* 오류 및 서버 예외 분석
* 작업 별로 성능을 자세히 살펴보고 타사 종속성을 호출 하는 데 걸리는 시간을 측정 합니다.
* 함수 앱을 호스트 하는 모든 서버에서 CPU 사용량, 메모리 및 비율 모니터링
* 함수 앱에 대 한 요청 수 및 대기 시간을 포함 하 여 메트릭의 라이브 스트림 보기
* [분석](https://docs.microsoft.com/azure/application-insights/app-insights-analytics) 을 사용 하 여 함수 데이터에서 사용자 지정 차트 검색, 쿼리 및 만들기

![메트릭 탐색기](./media/metrics-explorer.png)

기본 제공 원격 분석 외에도 사용자 지정 원격 분석을 생성할 수 있습니다. 다음 코드 조각은 함수 앱에 설정 된 계측 키를 사용 하 여 사용자 지정 원격 분석 클라이언트를 만듭니다.

```csharp
public static TelemetryClient telemetry = new TelemetryClient()
{
    InstrumentationKey = Environment.GetEnvironmentVariable("APPINSIGHTS_INSTRUMENTATIONKEY")
};
```

다음 코드는 [Azure Table Storage](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview) 인스턴스에 새 행을 삽입 하는 데 걸리는 시간을 측정 합니다.

```csharp
var operation = TableOperation.Insert(entry);
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
await table.ExecuteAsync(operation);
telemetry.TrackDependency("AzureTableStorageInsert", "Insert", startTime, timer.Elapsed, true);
```

결과 성능 그래프가 다음과 같이 표시 됩니다.

![사용자 지정 원격 분석](./media/custom-telemetry.png)

사용자 지정 원격 분석은 새 행을 삽입 하는 평균 시간을 32.6 밀리초로 표시 합니다.

Application Insights는 서버 리스 응용 프로그램에 대 한 자세한 원격 분석을 강력 하 고 편리한 방법으로 기록 합니다. 제공 된 추적 및 로깅 수준에 대 한 모든 권한을 가집니다. 이벤트, 종속성 및 페이지 보기와 같은 사용자 지정 통계를 추적할 수 있습니다. 마지막으로, 강력한 분석을 통해 중요 한 질문을 하 고 차트 및 고급 정보를 생성 하는 쿼리를 작성할 수 있습니다.

자세한 내용은 [Azure Functions 모니터링](https://docs.microsoft.com/azure/azure-functions/functions-monitoring)을 참조 하세요.

>[!div class="step-by-step"]
>[이전](azure-functions.md)
>[다음](logic-apps.md)
