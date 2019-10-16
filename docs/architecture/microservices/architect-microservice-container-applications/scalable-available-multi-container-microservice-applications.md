---
title: 높은 확장성 및 가용성을 위한 마이크로 서비스 및 다중 컨테이너 애플리케이션 오케스트레이션
description: Kubernetes 애플리케이션 수명 주기를 개발하는 동안 높은 확장성과 가용성 및 Azure Dev Spaces의 가능성을 위해 마이크로 서비스 및 다중 컨테이너 애플리케이션을 오케스트레이션하는 옵션을 검색합니다.
ms.date: 09/20/2018
ms.openlocfilehash: f0efad0134ec95028ecd49ad8d294ae4813940e9
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834319"
---
# <a name="orchestrating-microservices-and-multi-container-applications-for-high-scalability-and-availability"></a>높은 확장성 및 가용성을 위한 마이크로 서비스 및 다중 컨테이너 애플리케이션 오케스트레이션

애플리케이션이 마이크로 서비스를 기반으로 하거나 단순히 여러 컨테이너로 분할되는 경우 프로덕션 지원 애플리케이션에 오케스트레이터를 사용해야 합니다. 이전에 소개한 대로 마이크로 서비스 기반 방법에서 각 마이크로 서비스마다 모델 및 데이터를 소유하므로 개발 및 배포 관점에서 독립적입니다. 그러나 SOA와 같은 여러 서비스로 구성된 기존 애플리케이션이 있는 경우에도 분산 시스템으로 배포해야 하는 단일 비즈니스 애플리케이션을 구성하는 여러 컨테이너 또는 서비스가 제공됩니다. 이러한 종류의 시스템은 규모 확장 및 관리가 복잡합니다. 따라서 프로덕션을 지원하고 확장성 있는 다중 컨테이너 애플리케이션을 원하는 경우 오케스트레이터가 반드시 필요합니다.

그림 4-23에서는 여러 마이크로 서비스(컨테이너)로 구성된 애플리케이션의 클러스터에 배포하는 방법을 보여 줍니다.

![클러스터에서 구성된 Docker 애플리케이션을 보여 주는 다이어그램입니다.](./media/scalable-available-multi-container-microservice-applications/composed-docker-applications-cluster.png)

**그림 4-23** 컨테이너의 클러스터

각 서비스 인스턴스에 대해 하나의 컨테이너를 사용합니다. Docker 컨테이너는 "배포 단위"이고 컨테이너는 Docker의 인스턴스입니다. 하나의 호스트가 많은 컨테이너를 처리합니다. 이는 논리적인 방법처럼 보입니다. 그러나 이처럼 구성된 애플리케이션을 부하 분산, 라우팅 및 오케스트레이션하려면 어떻게 할까요?

단일 Docker 호스트의 일반 Docker 엔진은 하나의 호스트에서 단일 이미지 인스턴스를 관리해야 하는 필요성을 충족하지만, 더 복잡한 분산 애플리케이션을 위해 여러 호스트에 배포된 여러 컨테이너를 관리하는 경우에는 부족합니다. 대부분의 경우 컨테이너를 자동으로 시작하고 이미지당 여러 인스턴스로 컨테이너를 확장하고 일시 중지하거나 필요한 경우 종료하는 관리 플랫폼이 필요하며, 네트워크 및 데이터 스토리지와 같은 리소스에 액세스하는 방법을 제어하는 것도 좋습니다.

개별 컨테이너 또는 매우 간단하게 구성된 앱을 관리하는 것 외에도, 마이크로 서비스가 있는 대규모 엔터프라이즈 애플리케이션으로 이동하려면 오케스트레이션 및 클러스터링 플랫폼으로 전환해야 합니다.

아키텍처 및 개발 관점에서 마이크로 서비스 기반 애플리케이션으로 구성된 대규모 엔터프라이즈를 구축하는 경우 고급 시나리오를 지원하는 다음 플랫폼과 제품을 이해해야 합니다.

**클러스터 및 오케스트레이터.** 대규모 마이크로 서비스 기반 애플리케이션과 같이 많은 Docker 호스트에서 애플리케이션을 확장해야 하는 경우, 기본 플랫폼의 복잡성을 추상화하여 모든 호스트를 단일 클러스터로 관리할 수 있어야 합니다. 이는 컨테이너 클러스터 및 오케스트레이터에서 제공하는 것입니다. Kubernetes는 오케스트레이터의 한 예로서 Azure Kubernetes Service를 통해 Azure에서 제공됩니다.

**스케줄러.** *예약*은 관리자가 클러스터에서 컨테이너를 시작하여 UI도 제공할 수 있는 기능을 의미합니다. 클러스터 스케줄러에는 클러스터 리소스를 효율적으로 사용하고, 사용자가 제공하는 제약 조건을 설정하며, 노드 또는 호스트 간에 컨테이너를 효율적으로 부하 분산하고, 고가용성을 제공하면서 오류에 대해 강력한 기능을 제공하기 위한 여러 가지 역할이 있습니다.

클러스터 및 스케줄러의 개념은 밀접하게 관련되어 있으므로 여러 공급업체에서 제공하는 제품은 종종 두 가지 기능의 집합을 제공합니다. 다음 목록에서는 클러스터 및 스케줄러에 가장 중요한 플랫폼 및 소프트웨어 선택 항목을 보여 줍니다. 이러한 오케스트레이터는 일반적으로 Azure와 같은 퍼블릭 클라우드에서 제공됩니다.

## <a name="software-platforms-for-container-clustering-orchestration-and-scheduling"></a>컨테이너 클러스터링, 오케스트레이션 및 예약용 소프트웨어 플랫폼

|     |   |
|-----|---|
| **Kubernetes** <br> ![Kubernetes로고 이미지입니다.](./media/scalable-available-multi-container-microservice-applications/kubernetes-container-orchestration-system-logo.png) | [*Kubernetes*](https://kubernetes.io/)는 클러스터 인프라와 컨테이너 예약에서 기능 오케스트레이션에 이르기까지 다양한 기능을 제공하는 오픈 소스 제품입니다. 이를 통해 호스트 클러스터 전체에서 애플리케이션 컨테이너의 배포, 확장 및 작업을 자동화할 수 있습니다. <br><br> *Kubernetes*는 쉽게 관리하고 검색할 수 있도록 애플리케이션 컨테이너를 논리 단위로 그룹화하는 컨테이너 중심 인프라를 제공합니다. <br><br> *Kubernetes*의 완성도는 Linux에서 높았지만, Windows에서는 그렇지 못했습니다. |
| **AKS(Azure Kubernetes Service)** <br> ![Azure Kubernetes Service 로고의 이미지입니다.](./media/scalable-available-multi-container-microservice-applications/azure-kubernetes-service-logo.png) | [AKS](https://azure.microsoft.com/services/kubernetes-service/)는 관리되는 Kubernetes 컨테이너 오케스트레이션 서비스로 Kubernetes 클러스터의 관리, 배포 및 운영을 간소화합니다. |

## <a name="using-container-based-orchestrators-in-microsoft-azure"></a>Microsoft Azure에서 컨테이너 기반 오케스트레이션 사용

여러 클라우드 공급업체에서 Microsoft Azure, Amazon EC2 Container Service 및 Google Container Engine을 포함하여 Docker 컨테이너 지원 및 Docker 클러스터/오케스트레이션 지원을 제공합니다. Microsoft Azure는 AKS(Azure Kubernetes Service)를 통해 Docker 클러스터 및 오케스트레이터 지원을 제공합니다.

## <a name="using-azure-kubernetes-service"></a>Azure Kubernetes Service 사용

Kubernetes 클러스터는 여러 Docker 호스트를 풀링하고 단일 가상 Docker 호스트로 공개하여 여러 컨테이너를 클러스터에 배포하고 여러 컨테이너 인스턴스로 스케일 아웃할 수 있습니다. 클러스터는 확장성, 상태 등 모든 복잡한 관리 작업을 처리합니다.

AKS는 컨테이너화된 애플리케이션을 실행하도록 미리 구성된 Azure의 가상 머신 클러스터의 만들기, 구성 및 관리를 단순화할 수 있는 방법을 제공합니다. 인기 있는 오픈 소스 일정 예약 및 오케스트레이션 도구의 최적화된 구성을 통해 AKS를 사용하면 기존 기술을 사용하거나 광범위한 커뮤니티 전문 분야에 집중하여 Microsoft Azure에서 컨테이너 기반 애플리케이션을 배포하고 관리할 수 있습니다.

Azure Kubernetes Service는 Azure용으로 특별히 인기 있는 Docker 클러스터링 오픈 소스 도구 및 기술의 구성을 최적화합니다. 컨테이너와 애플리케이션 구성 모두에 이식성을 제공하는 개방형 솔루션을 얻을 수 있습니다. 사용자가 크기, 호스트 수, 오케스트레이터 도구를 선택하고, AKS에서 다른 모든 작업을 처리합니다.

![Kubernetes 클러스터 구조를 보여 주는 다이어그램입니다.](./media/scalable-available-multi-container-microservice-applications/kubernetes-cluster-simplified-structure.png)

**그림 4-24** Kubernetes 클러스터의 단순화된 구조 및 토폴로지

그림 4-24에서는 마스터 노드(VM)가 클러스터 조정의 대부분을 제어하고 애플리케이션의 관점에서 단일 풀로 관리되는 나머지 노드에 컨테이너를 배포할 수 있는 Kubernetes 클러스터의 구조를 볼 수 있으며, 수천 또는 수만 개의 컨테이너로 확장할 수 있습니다.

## <a name="development-environment-for-kubernetes"></a>Kubernetes를 위한 개발 환경

개발 환경에서 Kubernetes가 [Docker Desktop](https://docs.docker.com/install/)을 설치하기만 하면 단일 개발 머신(Windows 10 또는 macOS)에서도 실행할 수 있는 [Docker를 2018년 7월에 발표](https://blog.docker.com/2018/07/kubernetes-is-now-available-in-docker-desktop-stable-channel/)했습니다. 그림 4-25와 같이 나중에 통합 테스트를 위해 클라우드(AKS)에 배포할 수 있습니다.

![AKS에 배포되는 개발 머신의 Kubernetes를 보여 주는 다이어그램입니다.](./media/scalable-available-multi-container-microservice-applications/kubernetes-development-environment.png) 

**그림 4-25** 개발 머신 및 클라우드에서 Kubernetes 실행

## <a name="getting-started-with-azure-kubernetes-service-aks"></a>AKS(Azure Kubernetes Service) 시작 

AKS를 사용하여 시작하려면 Azure 포털에서 또는 CLI를 사용하여 AKS 클러스터를 배포합니다. Azure에서 Kubernetes 클러스터를 배포하는 방법에 대한 자세한 내용은 [Azure Kubernetes Service(AKS) 클러스터 배포](https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal)를 참조하세요.

기본적으로 AKS의 일부로 설치된 소프트웨어에 대해서는 추가 비용이 없습니다. 모든 기본 옵션은 오픈 소스 소프트웨어로 구현됩니다. AKS는 Azure의 여러 가상 머신에서 사용할 수 있습니다. 선택한 컴퓨팅 인스턴스 및 사용되는 다른 기본 인프라 리소스(예: 스토리지 및 네트워킹)에 대해서만 요금이 청구됩니다. AKS 자체에 대한 추가 비용은 없습니다.

kubectl 및 원본 .yaml 파일을 기반으로 Kubernetes에 배포하는 방법에 대한 자세한 구현 정보는 [AKS(Azure Kubernetes Service)에서 eShopOnContainers 설정](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.-Setting-the-solution-up-in-AKS-(Azure-Kubernetes-Service))에 대한 게시물을 확인하세요.

## <a name="deploying-with-helm-charts-into-kubernetes-clusters"></a>Helm 차트를 사용하여 Kubernetes 클러스터에 배포

애플리케이션을 Kubernetes 클러스터에 배포할 때, 이전 섹션에서 이미 언급한 네이티브 형식(.yaml 파일)에 따라 배포 파일을 사용하여 원래 kubectl.exe CLI 도구를 사용할 수 있습니다. 그러나 복잡한 마이크로 서비스 기반 애플리케이션을 배포할 때와 같이 더 복잡한 Kubernetes 애플리케이션의 경우 [Helm](https://helm.sh/)을 사용하는 것이 좋습니다.

Helm 차트를 사용하면 가장 복잡한 Kubernetes 애플리케이션도 정의, 버전 지정, 설치, 공유, 업그레이드 또는 롤백할 수 있습니다.

더 나아가, [Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces)와 같은 Azure의 추가 Kubernetes 환경도 Helm 차트를 기반으로 하기 때문에 Helm 사용이 권장됩니다.

Microsoft, Google, Bitnami 및 Helm 기여자 커뮤니티와 협력하여 [CNCF(Cloud Native Computing Foundation)](https://www.cncf.io/)에서 Helm을 유지 관리합니다.

Helm 차트 및 Kubernetes에 대한 자세한 구현 정보는 [Helm 차트를 사용하여 AKS에 eShopOnContainers 배포](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.1-Deploying-to-AKS-using-Helm-Charts)의 게시물을 확인하세요.

## <a name="use-azure-dev-spaces-for-your-kubernetes-application-lifecycle"></a>Kubernetes 애플케이션 수명 주기에 Azure Dev Spaces 사용

[Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces)는 팀을 위해 신속하고 반복적인 Kubernetes 개발 환경을 제공합니다. 최소한의 개발 머신 설치만으로 AKS(Azure Kubernetes Service)에서 직접 컨테이너를 반복적으로 실행하고 디버그할 수 있습니다. Visual Studio, Visual Studio Code 또는 명령줄 같은 친숙한 도구를 사용하여 Windows, Mac 또는 Linux에서 개발합니다.

언급한 바와 같이, Azure Dev Spaces는 컨테이너 기반 애플리케이션을 배포할 때 Helm 차트를 사용합니다.

Azure Dev Spaces는 Visual Studio 2017 또는 Visual Studio Code를 사용하기만 하면 Azure의 글로벌 Kubernetes 클러스터에서 직접 반복하고 디버그할 수 있기 때문에 개발 팀이 Kubernetes에서 생산성을 높일 수 있습니다. Azure에 있는 Kubernetes 클러스터는 공유된 관리 Kubernetes 클러스터이므로, 팀은 함께 협력할 수 있습니다. 코드를 따로 개발한 다음, 글로벌 클러스터에 배포하고 종속성을 복제 또는 모의하지 않고 다른 구성 요소를 사용하여 엔드투엔드 테스트를 수행합니다.

그림 4-26과 같이 Azure Dev Spaces의 가장 다른 기능은 클러스터에 글로벌 배포의 나머지 부분과 통합하여 실행할 수 있는 ' 공간'을 만드는 기능입니다.

![Azure Dev Spaces에서 여러 공백을 사용하는 방법을 보여 주는 다이어그램입니다.](./media/scalable-available-multi-container-microservice-applications/use-multiple-spaces-azure-dev.png)

**그림 4-26**. Azure Dev Spaces에서 여러 공간 사용

기본적으로 Azure에 공유 개발 공간을 설정할 수 있습니다. 각 개발자는 애플리케이션에서 자신이 맡은 부분에만 집중할 수 있으며 자신의 시나리오에 의존하는 다른 모든 서비스 및 클라우드 리소스가 포함된 개발 공간에서 커밋 전 코드를 반복해서 개발할 수 있습니다. 종속성은 항상 최신 상태로 유지되며 개발자가 생산을 미러링하는 방식으로 작업합니다.

Azure Dev Spaces는 팀 작업과 분리될 걱정 없이 상대적으로 격리되어 작업할 수 있는 공간의 개념을 제공합니다. 각 개발 공간은 고유하게 작업 중인 마이크로 서비스를 사용하여 "상위" 마스터 개발 공간의 마이크로 서비스(하나 이상)를 재정의할 수 있는 계층 구조의 일부입니다.

이 기능은 URL 접두사를 기반으로 하므로 URL에서 개발 공간 접두사를 사용할 때 요청이 개발 공간에 있는 경우 대상 마이크로 서비스에서 처리됩니다. 그렇지 않으면, 계층 구조에 있는 대상 마이크로 서비스의 첫 번째 인스턴스로 전달되어 결국 맨 위에 있는 마스터 개발 공간에 도달합니다.

구체적인 예에 대한 실용적인 보기를 가져오려면 [Azure Dev Spaces의 eShopOnContainers wiki 페이지](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.1-Using-Azure-Dev-Spaces-and-AKS)를 참조할 수 있습니다.

자세한 내용은 [Azure Dev Spaces로 팀 개발](https://docs.microsoft.com/azure/dev-spaces/team-development-netcore)에 대한 문서를 확인하세요.

## <a name="additional-resources"></a>추가 자료

- **AKS(Azure Kubernetes Service) 시작** \
  <https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal>

- **Azure Dev Spaces** \
  <https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces>

- **Kubernetes** 공식 사이트. \
  <https://kubernetes.io/>

>[!div class="step-by-step"]
>[이전](resilient-high-availability-microservices.md)
>[다음](../docker-application-development-process/index.md)
