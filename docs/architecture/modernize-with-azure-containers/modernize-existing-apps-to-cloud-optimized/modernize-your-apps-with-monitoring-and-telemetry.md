---
title: 모니터링 및 원격 분석을 사용하여 앱을 최신화
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | 모니터링 및 원격 분석을 사용하여 앱을 최신화
ms.date: 04/30/2018
ms.openlocfilehash: cdd7738606b086e980c4a50348166a7e23e15fa5
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72318485"
---
# <a name="modernize-your-apps-with-monitoring-and-telemetry"></a>모니터링 및 원격 분석을 사용하여 앱을 최신화

프로덕션 환경에서 응용 프로그램을 실행하는 경우 응용 프로그램 성능에 대한 통찰력이 중요합니다. 높은 수준으로 실행되고 있읍니까? 사용자에게 오류를 발생시키거나 아니면 안정적이고 신뢰할 수 있는 응용 프로그램입니까? 다양한 성능 모니터링과 강력한 알림, 대시보드가 있어야 응용 프로그램이 사용할 수 있고 기대한 대로 실행되는지 확인할 수 있습니다. 또한 문제가 있다면 신속하게 확인하여 얼마나 많은 고객이 영향을 받는지 확인하고, 문제를 찾아서 해결하기 위해 근본 원인을 분석하는 작업을 해야 합니다.

## <a name="monitor-your-application-with-application-insights"></a>Application Insights를 사용 하 여 응용 프로그램 모니터링

Application Insights는 여러 플랫폼에서 작업 하는 웹 개발자를 위한 확장 가능한 APM (응용 프로그램 성능 관리) 서비스입니다. 라이브 웹 응용 프로그램을 모니터링 하는 데 사용 합니다. Application Insights에서 성능 변칙을 자동으로 검색 합니다. 여기에는 문제를 진단 하 고 사용자가 앱에서 실제로 수행 하는 작업을 이해 하는 데 도움이 되는 강력한 분석 도구가 포함 되어 있습니다. Application Insights은 지속적으로 성능과 유용성을 향상 시킬 수 있도록 설계 되었습니다. 이는 온-프레미스 또는 클라우드에서 호스트 되는지에 관계 없이 .NET, node.js 및 J2EE를 비롯 한 다양 한 플랫폼에서 앱에 사용할 수 있습니다. Application Insights는 DevOps 프로세스와 통합 되며 다양 한 개발 도구에 대 한 연결 지점이 있습니다.

그림 4-10에서는 응용 프로그램을 Application Insights 모니터링 하는 방법 및 해당 정보를 대시보드에 표시 하는 방법을 보여 줍니다.

![Application Insights 모니터링 대시보드의 스크린샷](./media/modernize-your-apps-with-monitoring-and-telemetry/application-insights-monitoring-dashboard.png)

**그림 4-10.** Application Insights 모니터링 대시보드

## <a name="monitor-your-docker-infrastructure-with-log-analytics-and-its-container-monitoring-solution"></a>Log Analytics 및 해당 컨테이너 모니터링 솔루션을 사용 하 여 Docker 인프라 모니터링

[Azure Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) 는 [Microsoft Azure 전체 모니터링 솔루션](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)의 일부입니다. [OMS (Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)의 서비스 이기도 합니다. Log Analytics는 클라우드 및 온-프레미스 환경 (온-프레미스 용 OMS)을 모니터링 하 여 가용성과 성능을 유지 합니다. 클라우드 및 온-프레미스 환경에서 리소스에 의해 생성 된 데이터를 수집 하 고 다른 모니터링 도구를 통해 여러 원본에 걸쳐 분석을 제공 합니다.

Azure 인프라 로그와 관련 하 여 Azure 서비스로 Log Analytics, 다른 Azure 서비스 ( [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor)를 통해), azure Vm, Docker 컨테이너, 온-프레미스 또는 기타 클라우드 인프라에서 로그 및 메트릭 데이터를 수집 합니다. Log Analytics은이 데이터를 기반으로 하는 유연한 로그 검색 및 기본 제공 분석을 제공 합니다. 이 도구는 다양 한 원본에서 데이터를 분석 하는 데 사용할 수 있는 다양 한 도구를 제공 하며, 모든 로그에서 복잡 한 쿼리를 허용 하 고 지정 된 조건에 따라 사전에 경고할 수 있습니다. 중앙 Log Analytics 리포지토리에서 사용자 지정 데이터를 수집 하 여 쿼리하고 시각화할 수도 있습니다. 또한 Log Analytics 기본 제공 솔루션을 활용 하 여 인프라의 보안 및 기능에 대 한 정보를 즉시 얻을 수 있습니다.

모든 브라우저에서 실행 되는 OMS 포털 또는 Azure Portal를 통해 Log Analytics에 액세스할 수 있으며, 수집 된 데이터를 분석 하 고 작업 하는 구성 설정 및 여러 도구에 대 한 액세스를 제공 합니다.

Log Analytics의 [컨테이너 모니터링 솔루션](https://docs.microsoft.com/azure/log-analytics/log-analytics-containers) 을 사용 하 여 단일 위치에서 Docker 및 Windows 컨테이너 호스트를 보고 관리할 수 있습니다. 이 솔루션은 실행 중인 컨테이너, 실행 중인 컨테이너 이미지 및 컨테이너가 실행 되는 위치를 보여 줍니다. 컨테이너에 사용 되는 명령을 포함 하 여 자세한 감사 정보를 볼 수 있습니다. Docker 또는 Windows 호스트를 원격으로 볼 필요 없이 중앙 집중식 로그를 보고 검색 하 여 컨테이너 문제를 해결할 수도 있습니다. 잡음이 있을 수 있으며 호스트에서 초과 리소스를 소비 하는 컨테이너를 찾을 수 있습니다. 또한 컨테이너에 대해 중앙 집중식 CPU, 메모리, 저장소, 네트워크 사용량 및 성능 정보를 볼 수 있습니다. Windows를 실행 하는 컴퓨터에서 Windows Server, Hyper-v 및 Docker 컨테이너의 로그를 중앙 집중화 하 고 비교할 수 있습니다. 이 솔루션은 다음 컨테이너 orchestrator 지원 합니다.

- Docker Swarm

- DC/OS

- Kubernetes

- Red Hat OpenShift

그림 4-11은 다양 한 컨테이너 호스트와 에이전트 및 OMS 간의 관계를 보여 줍니다.

![Log Analytics 컨테이너 모니터링 솔루션의 스크린샷](./media/modernize-your-apps-with-monitoring-and-telemetry/log-analytics-container-monitoring-solution.png)

**그림 4-11.** Log Analytics 컨테이너 모니터링 솔루션

Log Analytics 컨테이너 모니터링 솔루션을 사용 하 여 다음을 수행할 수 있습니다.

- 단일 위치의 모든 컨테이너 호스트에 대 한 정보를 참조 하세요.

- 실행 중인 컨테이너, 실행 중인 이미지 및 실행 중인 위치를 확인 합니다.

- 컨테이너에 대 한 작업에 대 한 감사 내역을 확인 하세요.

- Docker 호스트에 대 한 원격 로그인 없이 중앙 집중식 로그를 보고 검색 하 여 문제를 해결 합니다.

- "잡음이 있는 환경"이 될 수 있는 컨테이너를 찾고 호스트에서 리소스를 과도 하 게 사용 합니다.

- 컨테이너에 대 한 중앙 집중식 CPU, 메모리, 저장소, 네트워크 사용량 및 성능 정보를 확인 합니다.

### <a name="additional-resources"></a>추가 자료

- **Microsoft Azure의 모니터링 개요**

<https://docs.microsoft.com/azure/azure-monitor/overview>

- **Application Insights란?**

<https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview>

- **Log Analytics 이란?**

<https://docs.microsoft.com/azure/log-analytics/log-analytics-overview>

- **Azure Monitor의 컨테이너 모니터링 솔루션**

<https://docs.microsoft.com/azure/azure-monitor/insights/containers>

- **Azure Monitor 개요**

<https://docs.microsoft.com/azure/azure-monitor/overview>

- **OMS (Operations Management Suite) 란?**

<https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview>

>[!div class="step-by-step"]
>[이전](build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud.md)
>[다음](modernize-your-apps-lifecycle-with-ci-cd-pipelines-and-devops-tools-in-the-cloud.md)
