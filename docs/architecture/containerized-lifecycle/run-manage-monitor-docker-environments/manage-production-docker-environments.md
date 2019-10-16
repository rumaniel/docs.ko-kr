---
title: 프로덕션 Docker 환경 관리
description: 컨테이너 기반 프로덕션 환경 관리의 핵심 내용을 알아봅니다.
ms.date: 02/15/2019
ms.openlocfilehash: 26e7a3319afe593d75e2384d023c901a389245dc
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834501"
---
# <a name="manage-production-docker-environments"></a>프로덕션 Docker 환경 관리

클러스터 관리 및 오케스트레이션은 호스트 그룹을 제어하는 프로세스입니다. 여기에는 클러스터의 호스트를 추가 및 제거하고, 호스트 및 컨테이너의 현재 상태 정보를 얻고, 프로세스를 시작 및 중지하는 작업이 포함됩니다. 클러스터 관리 및 오케스트레이션은 일정 예약과 밀접하게 관련되어 있습니다.스케줄러에서 서비스 일정을 예약하려면 클러스터의 각 호스트에 대한 액세스 권한이 필요하기 때문입니다. 이러한 이유로 두 목적에 동일한 도구를 사용하는 경우가 많습니다.

## <a name="container-service-and-management-tools"></a>Container Service 및 관리 도구

Container Service는 인기 있는 오픈 소스 컨테이너 클러스터링 및 오케스트레이션 솔루션을 신속하게 배포할 수 있습니다. Container Service는 Docker 이미지를 사용하여 애플리케이션 컨테이너를 완벽하게 이식할 수 있습니다. Container Service를 사용하면 Azure Resource Manager 템플릿 또는 Azure Portal에서 DC/OS(Mesosphere 및 Apache Mesos 기반) 및 Docker Swarm 클러스터를 배포하여 애플리케이션 규모를 컨테이너 수천, 심지어 수만 개로 확장할 수 있습니다.

Azure Virtual Machine Scale Sets를 사용하여 이러한 클러스터를 배포하면 클러스터가 Azure 네트워킹 및 스토리지 기능을 활용합니다. Container Service에 액세스하려면 Azure 구독이 필요합니다. Container Service를 사용하면 오케스트레이션 레이어 포함되는 애플리케이션 이식성을 유지하면서도 Azure의 엔터프라이즈급 기능을 활용할 수 있습니다.

표 6-1에는 오케스트레이터, 스케줄러 및 클러스터링 플랫폼과 관련된 일반적인 관리 도구가 나열되어 있습니다.

**표 6-1**. Docker 관리 도구

| 관리 도구 | 설명 | 관련 오케스트레이터 |
|------------------|-------------|-----------------------|
| [컨테이너용 Azure Monitor](https://docs.microsoft.com/azure/monitoring/monitoring-container-insights-overview) | Azure 전용 Kubernetes 관리 도구 | AKS(Azure Kubernetes Services) |
| [Kubernetes 웹 UI(대시보드)](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) | 로컬 Kubernetes 클러스터를 모니터링 및 관리할 수 있는 Kubernetes 관리 도구 | AKS(Azure Kubernetes Service)<br/>로컬 Kubernetes |
| [Service Fabric용 Azure Portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal)<br/>[Azure Service Fabric Explorer](https://docs.microsoft.com/azure/service-fabric/service-fabric-visualizing-your-cluster) | Azure, 온 프레미스, 로컬 개발 및 기타 클라우드에서 Service Fabric 클러스터를 관리할 수 있는 온라인 데스크톱 버전 | Azure Service Fabric |
| [컨테이너 모니터링(Azure Monitor)](https://docs.microsoft.com/azure/azure-monitor/insights/containers) | 일반 컨테이너 관리 y 모니터링 솔루션 [컨테이너용 Azure Monitor](https://docs.microsoft.com/azure/monitoring/monitoring-container-insights-overview)를 통해 Kubernetes 클러스터를 관리할 수 있습니다. | Azure Service Fabric<br/>AKS(Azure Kubernetes Service)<br/>Mesosphere DC/OS 및 기타 |

## <a name="azure-service-fabric"></a>Azure Service Fabric

클러스터를 배포하고 관리하는 또 다른 옵션은 Azure Service Fabric입니다. [Service Fabric](https://azure.microsoft.com/services/service-fabric/)은 컨테이너 오케스트레이션뿐 아니라 확장성이 뛰어난 마이크로서비스 애플리케이션을 빌드할 수 있는 개발자 프로그래밍 모델을 포함하고 있는 Microsoft 마이크로서비스 플랫폼입니다. Service Fabric은 Linux 및 Windows 컨테이너에서 Docker를 지원하며 Windows 및 Linux 서버에서 실행할 수 있습니다.

다음은 Service Fabric 관리 도구입니다.

- [Service Fabric용 Azure Portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal) 클러스터 관련 작업(클러스터 만들기/업데이트/삭제 또는 인프라(VM, 부하 분산 장치, 네트워킹 등) 구성)

- [Azure Service Fabric Explorer](https://docs.microsoft.com/azure/service-fabric/service-fabric-visualizing-your-cluster)는 노드/VM 관점과 애플리케이션 및 서비스 관점에서 Service Fabric 클러스터에 대한 인사이트와 특정 작업을 제공하는 특수 웹 UI 및 데스크톱 다중 플랫폼 도구입니다.

>[!div class="step-by-step"]
>[이전](run-microservices-based-applications-in-production.md)
>[다음](monitor-containerized-application-services.md)
