---
title: 프로덕션 Docker 환경 관리
description: Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 응용 프로그램 수명 주기
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.openlocfilehash: 3bafdd9f6a6aa4f850fd28b6315e68c643d1f8c0
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50202857"
---
# <a name="manage-production-docker-environments"></a>프로덕션 Docker 환경 관리

클러스터 관리 및 오케스트레이션은 호스트 그룹을 제어 하는 과정입니다. 이 추가 하 고 호스트 및 컨테이너의 현재 상태에 대 한 정보를 가져오기 시작 하 고 프로세스를 중지 하는 클러스터에서 호스트 제거 될 수 있습니다. 클러스터 관리 및 오케스트레이션은 밀접 한 관련이 스케줄러 있어야 하므로 각 호스트에 대 한 액세스 클러스터의 서비스를 예약 하려면 예약 합니다. 따라서 동일한 도구 모두를 위해 자주 사용 됩니다.

## <a name="container-service-and-management-tools"></a>컨테이너 서비스 및 관리 도구

Container Service는 인기 있는 오픈 소스 컨테이너 클러스터링 및 오케스트레이션 솔루션의 신속한 배포를 제공합니다. Docker 이미지를 사용 하 여 응용 프로그램 컨테이너가 완전히 이식 가능한 지 확인 합니다. 컨테이너 서비스를 사용 하 여 DC/OS (powered by Mesosphere 및 Apache Mesos) 배포할 수 있으며 이러한 응용 프로그램을 수천 초 단위로 확장할 수 있도록 Azure portal 또는 Azure Resource Manager 템플릿을 사용 하는 Docker Swarm 클러스터-수많은 등의 컨테이너입니다.

Azure Virtual Machine Scale Sets를 사용 하 여 이러한 클러스터를 배포 하 고 클러스터 네트워킹 및 저장소에 대 한 Azure 제품 활용 합니다. 컨테이너 서비스에 액세스 하려면 Azure 구독이 필요 합니다. Container Service를 사용 하 여 오케스트레이션 계층에 포함 되는 응용 프로그램 이식성을 유지 하면서 Azure의 엔터프라이즈급 기능을 활용을 걸릴 수 있습니다.

표 6-1의 오 케 스트레이 터, 스케줄러 및 클러스터링 플랫폼 관련 된 일반적인 관리 도구를 나열 합니다.

표 6-1: Docker 관리 도구


| 관리 도구      | 설명           | 관련된 오 케 스트레이 터 |
|-----------------------|-----------------------|-----------------------|
| Container Service\(Azure portal의 UI 관리) | [Container Service](https://azure.microsoft.com/services/container-service/) 쉽게 이용할 수를 제공 하는 방법은 시작 [Azure에서 컨테이너 클러스터를 배포](https://docs.microsoft.com/azure/container-service/dcos-swarm/container-service-deployment) Mesosphere DC/OS, Kubernetes 및 Docker Swarm과 같은 인기 있는 오 케 스트레이 터에 따라 합니다. <br /><br /> Container Service는 해당 플랫폼의 구성을 최적화 합니다. 크기, 호스트 수 및 오 케 스트레이 터 도구 옵션을 선택 해야 하 고 나머지 컨테이너 서비스 처리 합니다. | Mesosphere DC/OS <br /><br /> Kubernetes <br /><br /> Docker Swarm |
| Docker Universal 제어 평면\(온-프레미스 또는 클라우드) | [Docker Universal 제어 평면](https://docs.docker.com/v1.11/ucp/overview/) 는 Docker에서 엔터프라이즈급 클러스터 관리 솔루션입니다. 한 곳에서 전체 클러스터를 관리할 수 있습니다. <br /><br /> Docker Universal 제어 평면 Docker Swarm, Docker Universal 제어 평면 및 Docker Trusted Registry는 Docker 데이터 센터 라는 상업용 제품의 일부로 포함 되어 있습니다. <br /><br /> Docker 데이터 센터에 온-프레미스 설치 되거나 Azure와 같은 공용 클라우드를 프로 비전 합니다. | Docker Swarm\(Container Service를 통해 지원) |
| Docker 클라우드\(Tutum; 클라우드 SaaS 라고도) | [Docker 클라우드](https://docs.docker.com/docker-cloud/) 는 빌드하고 docker 화 된 응용 프로그램 이미지를 설정 하 고 호스트 인프라를 관리 하는 데 유용한 도구를 테스트 하는 기능을 사용 하 여 오케스트레이션 기능 및 Docker 레지스트리를 제공 하는 호스팅된 관리 서비스 (SaaS) 및를 자동으로 구체적인 인프라에 이미지를 배포할 수 있도록 배포 기능을 추가 합니다. Docker Swarm 클러스터를 실행 하는 Container Service에서 인프라를 SaaS Docker 클라우드 계정에 연결할 수 있습니다. | Docker Swarm\(Container Service를 통해 지원) |
| Mesosphere Marathon\(온-프레미스 또는 클라우드) | [Marathon](https://mesosphere.github.io/marathon/docs/marathon-ui.html) Mesosphere의 DC/OS 및 Apache Mesos는 프로덕션 급 컨테이너 오케스트레이션 및 스케줄러 플랫폼입니다. <br /><br /> Mesos와 함께 작동 (DC/OS는 Apache Mesos 기반) 컨트롤 장기 실행 서비스를 제공을 [프로세스 및 컨테이너 관리를 위한 웹 UI](https://mesosphere.github.io/marathon/docs/marathon-ui.html)합니다. 웹 UI 관리 도구 제공 | Mesosphere DC/OS\(Apache Mesos 기반; Container Service를 통해 지원) |
| Google Kubernetes | [Kubernetes](https://kubernetes.io/docs/user-guide/ui/#dashboard-access) 오케스트레이션, 예약 및 클러스터 인프라에 걸쳐 있습니다. 이 컨테이너 중심 인프라를 제공 하는 호스트를 클러스터 전체에서 배포, 크기 조정 및 응용 프로그램 컨테이너의 작업을 자동화 하는 데는 오픈 소스 플랫폼입니다. | Google Kubernetes\(Container Service를 통해 지원) |

## <a name="azure-service-fabric"></a>Azure Service Fabric

클러스터 배포 및 관리에 대 한 다른 선택에는 Azure Service Fabric은입니다. [Service Fabric](https://azure.microsoft.com/services/service-fabric/) 는 개발자 뿐만 아니라 컨테이너 오케스트레이션을 포함 하는 Microsoft 마이크로 서비스 플랫폼 프로그래밍 모델 확장성이 뛰어난 마이크로 서비스 응용 프로그램을 빌드할 수 있습니다. Service Fabric에서와 같이 현재 Linux 미리 보기 버전에서는 Docker를 지원 합니다 [Linux에서 Service Fabric 미리 보기](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-anywhere), 및 Windows 컨테이너에 대 한 [다음 릴리스에서](https://docs.microsoft.com/azure/service-fabric/service-fabric-containers-overview)합니다.

다음은 서비스 패브릭 관리 도구:

-   [Service Fabric에 대 한 azure portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal) 클러스터 관련 작업 (만들기/업데이트/삭제)는 클러스터 또는 인프라 (Vm, 부하 분산 장치, 네트워킹 등)를 구성 합니다.

-   [Azure Service Fabric Explorer](https://docs.microsoft.com/azure/service-fabric/service-fabric-visualizing-your-cluster) 는 insights 및 Service Fabric 클러스터 노드/v m의 관점에서 응용 프로그램 및 서비스의 관점에서 특정 작업을 제공 하는 특수 한 웹 UI 도구입니다.


>[!div class="step-by-step"]
[이전](run-microservices-based-applications-in-production.md)
[다음](monitor-containerized-application-services.md)
