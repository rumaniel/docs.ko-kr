---
title: 컨테이너화된 애플리케이션 서비스 모니터링
description: 컨테이너 아키텍처 모니터링의 주요 특징을 알아봅니다.
ms.date: 02/15/2019
ms.openlocfilehash: e14553d510751d8a75020a1b6beb9fd7bc29596e
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68673460"
---
# <a name="monitor-containerized-application-services"></a>컨테이너화된 애플리케이션 서비스 모니터링

여러 컨테이너와 마이크로서비스로 분할된 애플리케이션은 전체 애플리케이션의 동작을 모니터링하고 분석할 수 있는 방법이 있어야 합니다.

## <a name="azure-monitor"></a>Azure Monitor

[Azure Monitor](https://azure.microsoft.com/services/monitor/)는 라이브 애플리케이션을 모니터링하는 확장 가능한 분석 서비스입니다. 이 서비스를 사용하면 성능 이슈를 감지하고 진단하여 사용자가 실제로 앱에서 무엇을 하는지 파악할 수 있습니다. 이 서비스는 개발자가 서비스 또는 애플리케이션의 성능과 사용 편의성을 지속적으로 개선할 수 있도록 도와줄 의도로 설계되었습니다. Azure Monitor는 .NET, Java, Node.js, 온-프레미스 또는 클라우드에 호스트되는 다른 여러 플랫폼을 비롯한 다양한 플랫폼에서 웹/서비스 및 독립 실행형 앱과 함께 작동합니다.

### <a name="additional-resources"></a>추가 자료

- **Azure Monitor 개요** \
  <https://docs.microsoft.com/azure/azure-monitor/overview>

- **Application Insights란?** \
  <https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview>

- **Azure Monitor 메트릭이란?** \
  <https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-metrics>

- **Azure Monitor의 컨테이너 모니터링 솔루션** \
  <https://docs.microsoft.com/azure/azure-monitor/insights/containers>

## <a name="security-and-backup-services"></a>서비스 보안 및 백업

애플리케이션 및 인프라가 비즈니스 요구 사항을 지원하도록 최상의 상태를 유지하려면 여러 가지 지원 업무를 처리해야 하며, 마이크로서비스 영역에서는 상황이 점점 복잡해지고 있습니다. 따라서 조치를 취해야 할 때 상위 수준 보기와 세부 정보 보기를 모두 사용할 수 있는 방법이 필요합니다.

Azure 도구는 클라우드 리소스와 온-프레미스 리소스의 네 가지 중요한 측면을 관리하고 살펴볼 수 있는 통합 보기를 제공합니다.

- **보안**. [Azure Security Center](https://azure.microsoft.com/services/security-center/)를 사용합니다.
  - 가상 머신, 앱 및 워크로드의 보안을 완벽하게 살펴보고 제어할 수 있습니다.
  - 보안 정책 관리를 중앙 집중화하고 기존 프로세스 및 도구를 통합합니다.
  - 고급 분석을 사용하여 실제 위협을 감지합니다.

- **백업**. [Azure Backup](https://azure.microsoft.com/services/backup/)을 사용합니다.
  - 많은 비용이 발생하는 업무 중단을 방지하고, 규정 준수 목표를 충족하고, 랜섬웨어 및 사람의 오류로부터 데이터를 보호합니다.
  - 전송 및 저장 시 백업 데이터의 암호화를 유지합니다.
  - 다단계 인증을 기반으로 액세스 권한을 부여하여 단 사용을 방지합니다.

- **온-프레미스 리소스**. [진정으로 일관적인 하이브리드 클라우드](https://azure.microsoft.com/resources/truly-consistent-hybrid-cloud-with-microsoft-azure/)를 사용합니다.

>[!div class="step-by-step"]
>[이전](manage-production-docker-environments.md)
>[다음](../key-takeaways/index.md)
