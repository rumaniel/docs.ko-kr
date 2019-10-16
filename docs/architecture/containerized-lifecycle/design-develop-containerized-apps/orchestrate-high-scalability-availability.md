---
title: 높은 확장성 및 가용성을 위한 마이크로 서비스 및 다중 컨테이너 애플리케이션 오케스트레이션
description: 실제 프로덕션 애플리케이션은 모든 컨테이너의 상태, 워크로드 및 수명 주기를 처리하는 오케스트레이터를 통해 배포하고 관리해야 합니다.
ms.date: 02/15/2019
ms.openlocfilehash: 8f2cef774acde47e9a1bb4680342b5e2c66ac154
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990493"
---
# <a name="orchestrating-microservices-and-multi-container-applications-for-high-scalability-and-availability"></a>높은 확장성 및 가용성을 위한 마이크로 서비스 및 다중 컨테이너 애플리케이션 오케스트레이션

애플리케이션이 마이크로서비스를 기반으로 하거나 여러 컨테이너로 분할되는 경우 프로덕션 지원 애플리케이션에 오케스트레이터를 사용해야 합니다. 이전에 소개한 대로 마이크로 서비스 기반 방법에서 각 마이크로 서비스마다 모델 및 데이터를 소유하므로 개발 및 배포 관점에서 독립적입니다. 그러나 SOA와 같은 여러 서비스로 구성된 기존 애플리케이션이 있는 경우에도 분산 시스템으로 배포해야 하는 단일 비즈니스 애플리케이션을 구성하는 여러 컨테이너 또는 서비스가 제공됩니다. 이러한 종류의 시스템은 규모 확장 및 관리가 복잡합니다. 따라서 프로덕션을 지원하고 확장성 있는 다중 컨테이너 애플리케이션을 원하는 경우 오케스트레이터가 반드시 필요합니다.

그림 4-6에서는 여러 마이크로서비스(컨테이너)로 구성된 애플리케이션의 클러스터에 배포하는 방법을 보여줍니다.

![클러스터로 구성된 Docker 애플리케이션: 각 서비스 인스턴스에 대해 하나의 컨테이너를 사용합니다. Docker 컨테이너는 "배포 단위"이고 컨테이너는 Docker의 인스턴스입니다. 호스트는 여러 컨테이너를 처리합니다.](./media/image6.png)

**그림 4-6** 컨테이너의 클러스터

이는 논리적인 방법처럼 보입니다. 그러나 이렇게 구성된 애플리케이션을 부하 분산, 라우팅 및 오케스트레이션하려면 어떻게 할까요?

Docker CLI(명령줄 인터페이스)는 한 호스트에서 한 컨테이너를 관리해야 한다는 요구 사항을 충족하지만, 좀 더 복잡한 분산 애플리케이션에서 여러 호스트에 배포된 여러 컨테이너를 관리하는 경우에는 이것만으로 부족합니다. 대부분의 경우 컨테이너를 자동으로 시작하고, 이미지당 여러 인스턴스로 컨테이너를 확장하고, 필요할 때 컨테이너를 일시 중지하거나 종료하고, 네트워크 및 데이터 스토리지 같은 리소스에 액세스하는 방법을 제어하는 관리 플랫폼이 필요합니다.

개별 컨테이너 또는 간단하게 구성된 앱을 관리하는 수준을 넘어서 마이크로서비스를 사용하는 대규모 엔터프라이즈 애플리케이션으로 이동하려면 오케스트레이션 및 클러스터링 플랫폼으로 전환해야 합니다.

아키텍처 및 개발 관점에서 대규모 엔터프라이즈 마이크로서비스 기반 애플리케이션을 빌드할 때 고급 시나리오를 지원하는 다음 플랫폼과 제품을 이해해야 합니다.

- **클러스터 및 오케스트레이터.** 애플리케이션을 대규모 마이크로서비스 기반 애플리케이션 같은 Docker 호스트로 확장해야 하는 경우 기본 플랫폼의 복잡성을 추상화하여 모든 호스트를 단일 클러스터로 관리할 수 있어야 합니다. 이는 컨테이너 클러스터 및 오케스트레이터에서 제공하는 것입니다. 오케스트레이터의 예로는 Azure Service Fabric 및 Kubernetes가 있습니다. Kubernetes는 Azure Kubernetes Service를 통해 Azure에서 제공됩니다.

- **스케줄러.** *일정 예약*은 관리자가 클러스터의 컨테이너를 시작하는 기능이고, 스케줄러는 이를 위한 사용자 인터페이스를 제공합니다. 클러스터 스케줄러에는 클러스터 리소스를 효율적으로 사용하고, 사용자가 제공하는 제약 조건을 설정하며, 노드 또는 호스트 간에 컨테이너를 효율적으로 부하 분산하고, 고가용성을 제공하면서 오류에 대해 강력한 기능을 제공하기 위한 여러 가지 역할이 있습니다.

클러스터 및 스케줄러의 개념은 밀접하게 관련되어 있으므로 여러 공급업체에서 제공하는 제품은 종종 두 가지 기능의 집합을 제공합니다. 아래 섹션에서는 클러스터 및 스케줄러에 가장 중요한 플랫폼 및 소프트웨어 선택 항목을 보여줍니다. 이러한 오케스트레이터는 Azure 같은 퍼블릭 클라우드에 널리 제공됩니다.

## <a name="software-platforms-for-container-clustering-orchestration-and-scheduling"></a>컨테이너 클러스터링, 오케스트레이션 및 예약용 소프트웨어 플랫폼

| 플랫폼 | 설명 |
|:---:|:---|
| **Kubernetes** <br/> ![Kubernetes 로고](./media/kubernetes-logo.png) | [*Kubernetes*](https://kubernetes.io/)는 클러스터 인프라와 컨테이너 예약에서 기능 오케스트레이션에 이르기까지 다양한 기능을 제공하는 오픈 소스 제품입니다. 이를 통해 호스트 클러스터 전체에서 애플리케이션 컨테이너의 배포, 확장 및 작업을 자동화할 수 있습니다. <br/> <br/> *Kubernetes*는 쉽게 관리하고 검색할 수 있도록 애플리케이션 컨테이너를 논리 단위로 그룹화하는 컨테이너 중심 인프라를 제공합니다. <br/> <br/> *Kubernetes*의 완성도는 Linux에서 높았지만, Windows에서는 그렇지 못했습니다. |
| **AKS(Azure Kubernetes Service)** <br/> ![Azure Kubernetes Service 로고](./media/aks-logo.png) | [AKS(Azure Kubernetes Service)](https://azure.microsoft.com/services/kubernetes-service/)는 Kubernetes 클러스터의 관리, 배포 및 운영을 간소화하는 Azure에서 관리되는 Kubernetes 컨테이너 오케스트레이션 서비스입니다. |
| **Azure Service Fabric** <br/> ![Azure Service Fabric Logo](./media/service-fabric-logo.png) | [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview)은 애플리케이션을 빌드하기 위한 Microsoft 마이크로 서비스 플랫폼입니다. 서비스의 [오케스트레이터](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-resource-manager-introduction)이며, 머신의 클러스터를 만듭니다. Service Fabric은 서비스를 컨테이너 또는 일반 프로세스로 배포할 수 있습니다. 또한 동일한 애플리케이션 및 클러스터 내의 컨테이너에 있는 서비스와 프로세스에 있는 서비스를 혼합할 수도 있습니다. <br/> <br/> *Service Fabric* 클러스터는 Azure, 온-프레미스 또는 모든 클라우드에 배포할 수 있습니다. 그러나 Azure에서의 배포는 관리 방식으로 간소화됩니다. <br/> <br/> *Service Fabric*은 [상태 저장 서비스](https://azure.microsoft.com/documentation/articles/service-fabric-reliable-services-introduction/) 및[ Reliable Actors](https://azure.microsoft.com/documentation/articles/service-fabric-reliable-actors-introduction/)와 같이 규범적 [Service Fabric 프로그래밍 모델](https://azure.microsoft.com/documentation/articles/service-fabric-choose-framework/)(추가 및 선택 사양)을 제공합니다. <br/> <br/> *Service Fabric*의 완성도는 Windows에서 높았지만(Windows에서 진화), Linux에서는 그렇지 못했습니다. <br/> <br/> 2017년 이후 Service Fabric에서 Linux 및 Windows 컨테이너를 모두 지원합니다. |
| **Azure Service Fabric Mesh** <br/> ![Azure Service Fabric Mesh 로고](./media/azure-service-fabric-mesh-logo.png) | [*Azure Service Fabric Mesh*](https://docs.microsoft.com/azure/service-fabric-mesh/service-fabric-mesh-overview)는 Service Fabric과 동일한 안정성, 중요 업무용 성능 및 규모를 제공하지만, 완전 관리형 및 서버리스 플랫폼도 제공합니다. 클러스터, VM, 스토리지 또는 네트워킹 구성을 관리할 필요가 없습니다. 애플리케이션의 개발에만 주력할 수 있습니다. <br/> <br/> *Service Fabric Mesh*는 Windows 및 Linux 컨테이너를 모두 지원하므로 원하는 프로그래밍 언어와 프레임워크를 사용하여 개발할 수 있습니다.

## <a name="using-container-based-orchestrators-in-azure"></a>Azure에서 컨테이너 기반 오케스트레이터 사용

여러 클라우드 공급업체에서 Azure, Amazon EC2 Container Service 및 Google Container Engine을 포함하여 Docker 컨테이너 지원 및 Docker 클러스터/오케스트레이션 지원을 제공합니다. Microsoft Azure는 AKS(Azure Kubernetes Service)와 Azure Service Fabric 및 Azure Service Fabric Mesh를 통해 Docker 클러스터 및 오케스트레이터 지원을 제공합니다.

## <a name="using-azure-kubernetes-service"></a>Azure Kubernetes Service 사용

Kubernetes 클러스터는 여러 Docker 호스트를 풀링하고 단일 가상 Docker 호스트로 공개하여 여러 컨테이너를 클러스터에 배포하고 여러 컨테이너 인스턴스로 스케일 아웃할 수 있습니다. 클러스터는 확장성, 상태 등 모든 복잡한 관리 작업을 처리합니다.

AKS는 컨테이너화된 애플리케이션을 실행하도록 미리 구성된 Azure의 가상 머신 클러스터의 만들기, 구성 및 관리를 단순화할 수 있는 방법을 제공합니다. 인기 있는 오픈 소스 일정 예약 및 오케스트레이션 도구의 최적화된 구성을 통해 AKS를 사용하면 기존 기술을 사용하거나 광범위한 커뮤니티 전문 분야에 집중하여 Microsoft Azure에서 컨테이너 기반 애플리케이션을 배포하고 관리할 수 있습니다.

Azure Kubernetes Service는 Azure용으로 특별히 인기 있는 Docker 클러스터링 오픈 소스 도구 및 기술의 구성을 최적화합니다. 컨테이너와 애플리케이션 구성 모두에 이식성을 제공하는 개방형 솔루션을 얻을 수 있습니다. 사용자가 크기, 호스트 수, 오케스트레이터 도구를 선택하고, AKS에서 다른 모든 작업을 처리합니다.

![Kubernetes 클러스터 구조: DNS, 스케줄러, 프록시 등을 처리하는 하나의 마스터 노드와 컨테이너를 호스트하는 여러 작업자 노드가 있습니다.](media/image36.png)

**그림 4-7**. Kubernetes 클러스터의 단순화된 구조 및 토폴로지

그림 4-7은 마스터 노드(VM)가 대부분의 클러스터 조정을 제어하며, 애플리케이션의 관점에서 단일 풀로 관리되는 나머지 노드에 컨테이너를 배포할 수 있는 Kubernetes 클러스터의 구조체를 보여줍니다. 이 규모를 수천 또는 수만 개의 컨테이너로 확장할 수 있습니다.

## <a name="development-environment-for-kubernetes"></a>Kubernetes를 위한 개발 환경

[Docker가 2018년 7월에 발표한](https://blog.docker.com/2018/07/kubernetes-is-now-available-in-docker-desktop-stable-channel/) 개발 환경에서 [Docker Desktop](https://www.docker.com/community-edition)을 설치하기만 하면 Kubernetes를 단일 개발 머신(Windows 10 또는 macOS)에서도 실행할 수 있습니다. 그림 4-8처럼 나중에 클라우드(AKS)에 배포하여 통합 테스트를 수행할 수 있습니다.

![Docker는 Docker Desktop으로 Kubernetes 클러스터에 대한 개발 머신 지원을 2018년 7월에 발표했습니다.](media/kubernetes-development-environment.png)

**그림 4-8**. 개발 머신 및 클라우드에서 Kubernetes 실행

## <a name="get-started-with-azure-kubernetes-service-aks"></a>AKS(Azure Kubernetes Service) 시작

AKS를 사용하여 시작하려면 Azure 포털에서 또는 CLI를 사용하여 AKS 클러스터를 배포합니다. Azure에 Kubernetes 클러스터를 배포하는 방법에 대한 자세한 내용은 [AKS(Azure Kubernetes Service) 클러스터 배포](https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal)를 참조하세요.

기본적으로 AKS의 일부로 설치된 소프트웨어에 대해서는 추가 비용이 없습니다. 모든 기본 옵션은 오픈 소스 소프트웨어로 구현됩니다. AKS는 Azure의 여러 가상 머신에서 사용할 수 있습니다. 선택한 컴퓨팅 인스턴스 및 사용되는 다른 기본 인프라 리소스(예: 스토리지 및 네트워킹)에 대해서만 요금이 청구됩니다. AKS 자체에 대한 추가 비용은 없습니다.

`kubectl` 및 원본 `.yaml` 파일을 기반으로 Kubernetes에 배포하는 방법에 대한 자세한 구현 정보는 [AKS(Azure Kubernetes Service)에서 eShopOnContainers 설정](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.-Setting-the-solution-up-in-AKS-(Azure-Kubernetes-Service))의 게시물을 참조하세요.

## <a name="deploy-with-helm-charts-into-kubernetes-clusters"></a>Helm 차트를 사용하여 Kubernetes 클러스터에 배포

Kubernetes 클러스터에 애플리케이션을 배포할 때 이전 섹션에서 언급한 것처럼 네이티브 형식(`.yaml` 파일)에 따라 배포 파일을 사용하여 원래 `kubectl.exe` CLI 도구를 사용할 수 있습니다. 그러나 복잡한 마이크로 서비스 기반 애플리케이션을 배포할 때와 같이 더 복잡한 Kubernetes 애플리케이션의 경우 [Helm](https://helm.sh/)을 사용하는 것이 좋습니다.

Helm 차트를 사용하면 가장 복잡한 Kubernetes 애플리케이션도 정의, 버전 지정, 설치, 공유, 업그레이드 또는 롤백할 수 있습니다.

더 나아가, [Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces)와 같은 Azure의 추가 Kubernetes 환경도 Helm 차트를 기반으로 하기 때문에 Helm 사용이 권장됩니다.

Microsoft, Google, Bitnami 및 Helm 기여자 커뮤니티와 협업하여 [CNCF(Cloud Native Computing Foundation)](https://www.cncf.io/)에서 Helm을 유지 관리합니다.

Helm 차트 및 Kubernetes에 대한 자세한 구현 정보는 [Helm 차트를 사용하여 AKS에 eShopOnContainers 배포](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.1-Deploying-to-AKS-using-Helm-Charts)의 게시물을 참조하세요.

## <a name="use-azure-dev-spaces-for-you-kubernetes-application-lifecycle"></a>Kubernetes 애플케이션 수명 주기에 Azure Dev Spaces 사용

[Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces)는 팀을 위해 신속하고 반복적인 Kubernetes 개발 환경을 제공합니다. 최소한의 개발 머신 설치만으로 AKS(Azure Kubernetes Service)에서 직접 컨테이너를 반복적으로 실행하고 디버그할 수 있습니다. Windows, Mac 또는 Linux에서 Visual Studio, Visual Studio Code 또는 명령줄과 같은 익숙한 도구를 사용하여 개발할 수 있습니다.

앞서 언급했듯이, Azure Dev Spaces는 컨테이너 기반 애플리케이션을 배포할 때 Helm 차트를 사용합니다.

Azure Dev Spaces는 Visual Studio 2017 또는 Visual Studio Code를 사용하기만 하면 Azure의 글로벌 Kubernetes 클러스터에서 직접 반복하고 디버그할 수 있기 때문에 개발 팀이 Kubernetes에서 생산성을 높일 수 있습니다. Azure에 있는 Kubernetes 클러스터는 공유된 관리 Kubernetes 클러스터이므로, 팀은 함께 협력할 수 있습니다. 코드를 따로 개발한 다음, 글로벌 클러스터에 배포하고 종속성을 복제 또는 모의하지 않고 다른 구성 요소를 사용하여 엔드투엔드 테스트를 수행합니다.

그림 4-9처럼 Azure Dev Spaces의 가장 다른 기능은 클러스터에 글로벌 배포의 나머지 부분과 통합하여 실행할 수 있는 '공간'을 만드는 기능입니다.

![Azure Dev Spaces는 새 버전의 테스트를 쉽게 하기 위해 개발 컨테이너 인스턴스와 프로덕션 마이크로 서비스를 투명하게 혼합하여 일치시킬 수 있습니다.](media/image38.png)

**그림 4-9** Azure Dev Spaces에서 여러 공간 사용

기본적으로 Azure에서 공유 개발 공간을 설정할 수 있습니다. 각 개발자는 애플리케이션의 일부에만 집중할 수 있으며, 시나리오에 종속된 다른 모든 서비스와 클라우드 리소스가 이미 포함되어 있는 개발 공간에서 "사전 커밋 코드"를 반복적으로 개발할 수 있습니다. 종속성은 항상 최신 상태로 유지되며 개발자가 생산을 미러링하는 방식으로 작업합니다.

Azure Dev Spaces는 공간이라는 개념을 제공합니다. 이 공간을 사용하면 팀 구성원을 방해할 염려 없이 격리된 상태에서 작업할 수 있습니다. 이 기능은 URL 접두사를 기반으로 합니다. 컨테이너 요청의 URL에 개발 공간 접두사를 사용하면 Azure Dev Spaces는 해당 공간(있는 경우)에 대해 배포한 특별 버전의 컨테이너를 실행합니다. 그렇지 않으면 글로벌/통합 버전을 실행합니다.

구체적인 예제를 살펴보려면 [Azure Dev Spaces의 eShopOnContainers wiki 페이지](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.2-Using-Azure-Dev-Spaces-and-AKS)를 참조하세요.

자세한 내용은 [Azure Dev Spaces로 팀 개발](https://docs.microsoft.com/azure/dev-spaces/team-development-netcore)의 문서를 참조하세요.

## <a name="additional-resources"></a>추가 자료

- **AKS(Azure Kubernetes Service) 시작** \
  <https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal>

- **Azure Dev Spaces** \
  <https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces>

- **Kubernetes.** 공식 사이트입니다. \
  <https://kubernetes.io/>

## <a name="using-azure-service-fabric"></a>Azure Service Fabric 사용

Azure Service Fabric은 Microsoft가 제품 공급 방식을 획일적인 모놀리식 "박스" 제품에서 서비스로 바꾼 이후에 제공되기 시작한 서비스입니다. Azure SQL Database, Azure Cosmos DB, Azure Service Bus 또는 Cortana의 백 엔드와 같은 대규모 서비스를 구축하고 운영한 경험을 토대로 Service Fabric이 개발되었습니다. 점점 더 많은 서비스가 도입됨에 따라 플랫폼은 시간이 지날수록 향상되었습니다. 중요한 점은 Service Fabric은 Azure뿐만 아니라 독립 실행형 Windows Server 배포에서도 실행되어야 한다는 것입니다.

Service Fabric의 목적은 서비스를 구축 및 실행하고 인프라 리소스를 효율적으로 활용하는 어려운 문제를 해결하여, 팀이 마이크로 서비스 접근 방식을 사용하여 비즈니스 문제를 해결할 수 있도록 하는 것입니다.

Service Fabric은 마이크로 서비스 접근 방식을 사용하는 애플리케이션을 빌드하는 데 도움이 되는 두 가지 폭넓은 영역을 제공합니다.

- 실패한 서비스를 배포, 확장, 업그레이드, 검색 및 다시 시작하고 서비스 위치를 검색하며 상태를 관리하고 상태를 모니터링하는 시스템 서비스를 제공하는 플랫폼. 실제 이러한 시스템 서비스를 통해 이전에 설명한 마이크로 서비스의 많은 특성을 실현할 수 있습니다.

- 마이크로 서비스로 애플리케이션을 빌드하는 데 도움이 되는 프로그래밍 API 또는 프레임워크: [Reliable Actor 및 Reliable Service](https://docs.microsoft.com/azure/service-fabric/service-fabric-choose-framework). 마이크로 서비스를 구축하는 코드를 선택할 수는 있지만 이러한 API를 사용하면 작업이 더 간단해지며 플랫폼과 보다 자세히 통합할 수 있습니다. 이러한 방식으로 상태 및 진단 정보를 얻을 수 있거나 신뢰할 수 있는 상태 관리를 이용할 수 있습니다.

Service Fabric은 서비스 구축하는 방법과 관련하여 제약이 없으며 모든 기술을 사용할 수 있습니다. 단, 마이크로 서비스를 보다 쉽게 구축할 수 있도록 해주는 기본 제공 프로그래밍 API가 제공됩니다.

그림 4-10처럼 Service Fabric에서 간단한 프로세스 또는 Docker 컨테이너로 마이크로서비스를 만들고 실행할 수 있습니다. 동일한 Service Fabric 클러스터 내에서 컨테이너 기반 마이크로 서비스와 프로세스 기반 마이크로 서비스를 함께 사용할 수도 있습니다.

![Azure Service Fabric 클러스터 비교: 마이크로서비스에 대해 하나의 프로세스를 실행하는 프로세스입니다. 마이크로서비스는 여러 컨테이너가 있는 Docker를 실행하는 컨테이너로, 마이크로서비스당 하나의 컨테이너로 실행됩니다.](./media/azure-service-fabric-cluster-types.png)

**그림 4-10** Azure Service Fabric에서 프로세스 또는 컨테이너로 마이크로 서비스 배포

Linux 및 Windows 호스트 기반 Service Fabric 클러스터는 Linux Docker 컨테이너와 Windows 컨테이너를 각각 실행할 수 있습니다.

Azure Service Fabric에서 컨테이너 지원에 대한 최신 정보는 [Service Fabric 및 컨테이너](https://docs.microsoft.com/azure/service-fabric/service-fabric-containers-overview)를 참조하세요.

Service Fabric은 물리적 구현과 다른 논리적 아키텍처(비즈니스 마이크로서비스 또는 바인딩된 컨텍스트)를 정의할 수 있는 플랫폼의 좋은 예입니다. 예를 들어 "[상태 비저장 및 상태 저장 마이크로서비스](#stateless-versus-stateful-microservices)" 섹션에 소개된 대로 [Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview)에 [상태 저장 Reliable Services](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction)를 구현하면 여러 물리적 서비스에 비즈니스 마이크로서비스 개념을 적용할 수 있습니다.

그림 4-10처럼 논리적/비즈니스 마이크로서비스 관점에서 생각해 보면, Service Fabric 상태 저장 Reliable Service를 구현할 때 일반적으로 두 가지 서비스 계층을 구현해야 합니다. 첫 번째는 여러 개의 파티션(각 파티션은 상태 저장 서비스)을 처리하는 백 엔드 상태 저장 신뢰할 수 있는 서비스입니다. 두 번째는 다중 파티션 또는 상태 저장 서비스 인스턴스에서 라우팅 및 데이터 집계를 담당하는 프런트 엔드 서비스 또는 Gateway 서비스입니다. 또한 이 Gateway 서비스는 백 엔드 서비스에 액세스하는 재시도 루프로 클라이언트 쪽 통신을 처리합니다. 사용자 지정 서비스를 구현하거나, 기본 제공 Service Fabric [역방향 프록시](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)를 사용할 수 있는 경우 Gateway 서비스라고 합니다.

![Service Fabric은 컨테이너의 여러 상태 저장 신뢰할 수 있는 서비스를 지원하는 방법이 있습니다.](./media/service-fabric-stateful-business-microservice.png)

**그림 4-11** 여러 상태 저장 서비스 인스턴스 및 사용자 지정 게이트웨이 프런트 엔드가 있는 비즈니스 마이크로서비스

어떤 경우에도 Service Fabric 상태 저장 Reliable Services를 사용하면 여러 물리적 서비스로 구성된 논리적 또는 비즈니스 마이크로서비스(바인딩된 컨텍스트)가 있습니다. 그림 4-11처럼 각 Gateway 서비스 및 Partition 서비스를 ASP.NET Web API 서비스로 구현할 수 있습니다.

Service Fabric에서는 오케스트레이터 또는 클러스터의 패키징 및 배포 단위인 [Service Fabric 애플리케이션](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-model)으로 서비스 그룹을 그룹화 및 배포할 수 있습니다. 따라서 Service Fabric 애플리케이션을 이 자치 비즈니스 및 논리적 마이크로 서비스 경계 또는 바인딩된 컨텍스트에도 매핑할 수 있으므로 이러한 서비스를 자율적으로 배포할 수 있습니다.

### <a name="service-fabric-and-containers"></a>Service Fabric 및 컨테이너

Service Fabric의 컨테이너와 관련해서는 Service Fabric 클러스터 내의 컨테이너 이미지에 서비스를 배포할 수도 있습니다. 그림 4-12처럼 거의 대부분 서비스당 하나의 컨테이너만 있습니다.

![Service Fabric 애플리케이션은 외부 데이터베이스에 액세스하는 여러 컨테이너를 실행할 수 있으며 전체 세트는 비즈니스 마이크로서비스의 논리적 경계가 됩니다.](./media/azure-service-fabric-business-microservice.png)

**그림 4-12**. Service Fabric에 여러 서비스(컨테이너)가 있는 비즈니스 마이크로 서비스

그러나 Service Fabric에서는 소위 “사이드카” 컨테이너(논리적 서비스의 일부로 함께 배포해야 하는 두 개의 컨테이너)도 가능합니다. 중요한 것은 비즈니스 마이크로 서비스가 여러 응집 요소 주위의 논리적 경계라는 것입니다. 대부분의 경우, 단일 데이터 모델을 사용하는 단일 서비스일 수 있지만 일부 다른 경우에는 여러 개의 물리적 서비스가 있을 수도 있습니다.

그림 4-13처럼 동일한 Service Fabric 애플리케이션에서 컨테이너의 서비스와 프로세스의 서비스를 혼합할 수 있습니다.

![Service Fabric 애플리케이션은 동일한 노드에서 서비스와 컨테이너를 모두 실행합니다.](./media/business-microservice-mapped-to-service-fabric-application.png)

**그림 4-13**. 컨테이너 및 상태 저장 서비스와 함께 Service Fabric 애플리케이션에 매핑된 비즈니스 마이크로 서비스

Azure Service Fabric에서 컨테이너 지원에 대한 자세한 내용은 [Service Fabric 및 컨테이너](https://docs.microsoft.com/azure/service-fabric/service-fabric-containers-overview)를 참조하세요.

## <a name="stateless-versus-stateful-microservices"></a>상태 비저장 및 상태 저장 마이크로 서비스

앞에서 설명한 대로, 각 마이크로 서비스(논리적 바인딩된 컨텍스트)는 고유한 도메인 모델(데이터 및 논리)을 소유해야 합니다. 상태 비저장 마이크로 서비스의 경우, 데이터베이스는 SQL Server와 같은 관계형 옵션을 사용하거나 Azure Cosmos DB 또는 MongoDB와 같은 NoSQL 옵션을 사용하여 외부 데이터베이스가 됩니다.

그러나 서비스 자체는 Service Fabric에서도 상태가 유지될 수 있습니다. 즉, 데이터가 마이크로 서비스 내에 있습니다. 이 데이터는 동일한 서버에 있을 뿐만 아니라 마이크로 서비스 프로세스, 메모리 내에 있으며 하드 드라이브에 보관되어 다른 노드에 복제될 수 있습니다. 그림 4-14는 다양한 방식을 보여 줍니다.

![상태 비저장 서비스에서 상태(지속성, 데이터베이스)는 마이크로서비스에서 제외됩니다. 상태 저장 서비스에서 상태는 마이크로서비스 내에 유지됩니다.](./media/stateless-vs-stateful-microservices.png)

**그림 4-14**. 상태 비저장 및 상태 저장 마이크로 서비스

상태 비저장 방식은 완벽하게 유효하며 기존의 잘 알려진 패턴과 유사하기 때문에 상태 저장 마이크로 서비스보다 쉽게 구현할 수 있습니다. 그러나 상태 비저장 마이크로 서비스는 프로세스와 데이터 원본 간에 대기 시간을 둡니다. 또한 캐시 및 대기열을 추가하여 성능을 향상시키려는 경우 더욱 복잡해집니다. 결과적으로 너무 많은 계층을 가진 복잡한 아키텍처로 끝날 수 있습니다.

반대로 [상태 저장 마이크로 서비스](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction#when-to-use-reliable-services-apis)는 도메인 논리와 데이터 간에 대기 시간이 없기 때문에 고급 시나리오에서 뛰어납니다. 대량의 데이터 처리, 게임 백 엔드, 서비스 형태의 데이터베이스 및 기타 대기 시간이 적은 시나리오는 모두 상태 저장 서비스를 활용하여 로컬 상태에서 더 빠르게 액세스할 수 있습니다.

상태 비저장 및 상태 저장 서비스는 보완적입니다. 예를 들어 그림 4-14의 오른쪽 다이어그램을 보면 상태 저장 서비스를 여러 파티션으로 분할할 수 있습니다. 이러한 파티션에 액세스하려면 파티션 키를 기반으로 각 파티션의 주소를 지정하는 방법을 알고 있는 게이트웨이 서비스로 작동하는 상태 비저장 서비스가 필요할 수 있습니다.

상태 저장 서비스에는 단점이 있습니다. 확장 방법이 매우 복잡하다는 점입니다. 일반적으로 외부 데이터베이스 시스템에 의해 구현되는 기능은 상태 저장 마이크로 서비스 간 데이터 복제 및 데이터 분할과 같은 작업을 위해 처리되어야 합니다. 그러나 이것은 [상태 저장 신뢰할 수 있는 서비스](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction#when-to-use-reliable-services-apis)가 있는 [Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-platform-architecture)과 같은 오케스트레이터가 [Reliable Services API](https://docs.microsoft.com/azure/service-fabric/service-fabric-work-with-reliable-collections) 및 [Reliable Actors](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-introduction)를 사용하여 상태 저장 마이크로 서비스의 개발 및 수명 주기를 단순화함으로써 지원할 수 있는 분야 중 하나입니다.

상태 저장 서비스를 허용하고 Actor 패턴을 지원하며 비즈니스 논리와 데이터 간의 내결함성과 대기 시간을 향상시키는 기타 마이크로 서비스 프레임워크로는 Microsoft Research의 Microsoft [Orleans](https://github.com/dotnet/orleans) 및 [Akka.NET](https://getakka.net/)이 있습니다. 두 프레임워크는 현재 Docker에 대한 지원을 개선 중입니다.

Docker 컨테이너 자체는 상태 비저장입니다. 상태 저장 서비스를 구현하려면 앞에서 언급한 추가 규범 및 상위 수준 프레임워크 중 하나가 필요합니다.

## <a name="using-azure-service-fabric-mesh"></a>Azure Service Fabric Mesh 사용

Azure Service Fabric Mesh는 개발자가 인프라를 관리하지 않고 중요 업무용 애플리케이션을 빌드하고 배포할 수 있는 완전 관리형 서비스입니다. Service Fabric Mesh를 사용하여 필요에 따라 확장 가능한 안전한 분산 마이크로 서비스 애플리케이션을 빌드하고 실행합니다.

그림 4-15처럼 Service Fabric Mesh에 호스트되는 애플리케이션은 이를 구동하는 인프라에 대한 걱정 없이 실행 및 확장됩니다.

![Docker 데스크톱에서 실행되는 다중 컨테이너 앱은 인프라에 대한 걱정 없이 Azure Service Fabric Mesh에 배포할 수 있습니다.](media/image39.png)

**그림 4-15**. Service Fabric Mesh에 마이크로 서비스/컨테이너 애플리케이션 배포

내부적으로 Service Fabric Mesh는 수천 대의 머신 클러스터로 구성됩니다. 모든 클러스터 작업은 개발자가 볼 수 없습니다. 컨테이너를 업로드하고 필요한 리소스, 가용성 요구 사항 및 리소스 제한을 지정하기만 하면 됩니다. Service Fabric Mesh는 애플리케이션 배포에서 요청한 인프라를 자동으로 할당하고 인프라 오류를 처리하여 애플리케이션의 가용성을 높입니다. 인프라가 아니라 애플리케이션의 상태 및 응답에만 신경 써야 합니다.

자세한 내용은 [Service Fabric Mesh 설명서](https://docs.microsoft.com/azure/service-fabric-mesh/)를 참조하세요.

## <a name="choosing-orchestrators-in-azure"></a>Azure에서 오케스트레이터 선택

다음 표는 워크로드 및 OS 포커스에 따라 사용할 오케스트레이터에 대한 지침을 제공합니다.

![Azure Kubernetes Services는 Windows보다 Linux에서 더 완성도가 높으며 컨테이너를 기반으로 하는 마이크로서비스를 배포하는 데 주로 사용됩니다. Azure Service Fabric(클러스터 및 메시 모두)은 Linux보다 Windows에서 더 성숙하며, 일반적으로 컨테이너를 기반으로 하는 마이크로 서비스, 일반 프로세스 및 상태 저장 서비스에 기반한 마이크로 서비스에 사용됩니다.](media/image40.png)

**그림 4-16**. Azure 지침에서 오케스트레이터 선택

>[!div class="step-by-step"]
>[이전](soa-applications.md)
>[다음](deploy-azure-kubernetes-service.md)
