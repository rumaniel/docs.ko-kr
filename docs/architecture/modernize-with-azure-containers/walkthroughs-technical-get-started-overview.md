---
title: 기술 개요와 실습
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | 기술 개요와 실습
ms.date: 04/28/2018
ms.openlocfilehash: 190b33c4307b09bab0543d481e66ac9328074a0d
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69660893"
---
# <a name="walkthroughs-and-technical-get-started-overview"></a>기술 개요와 실습

이 전자책의 분량이 너무 방대해지는 것을 피하고자, 추가적인 기술 설명서와 실습의 전체 내용은 GitHub 리포지토리를 활용하도록 구성되어 있습니다. 이 장에서 설명하는 실습 온라인 시리즈에서는 Windows 컨테이너를 기반으로 하는 다양한 환경의 단계별 설치와 Azure 배포에 대해 설명합니다.

다음 섹션에서는 각 연습에 대 한 설명, 목표 및 상위 수준 비전에 대해 설명 하 고 관련 작업에 대 한 다이어그램을 제공 합니다. *EShopModernizing* apps GitHub 리포지토리 wiki <https://github.com/dotnet-architecture/eShopModernizing/wiki>의에서 연습 자체를 다운로드할 수 있습니다.

## <a name="technical-walkthrough-list"></a>기술 연습 목록

다음 시작 연습은 컨테이너를 사용 하 여 리프트 앤 시프트 하 고 Azure에서 여러 배포 옵션을 사용 하 여 이동할 수 있는 샘플 앱에 대 한 일관적이 고 포괄적인 기술 지침을 제공 합니다.

다음 각 연습은 GitHub <https://github.com/dotnet-architecture/eShopModernizing>에서 제공 되는 새로운 Sample eShopLegacy 및 eShopModernizing apps를 사용 합니다.

- **EShop 레거시 앱 둘러보기 (현대화에 대 한 기준 앱)**

- **Windows 컨테이너를 사용 하 여 기존 ASP.NET 웹 앱 (WebForms & MVC) 컨테이너 화**

- **Windows 컨테이너를 사용 하 여 기존 WCF 서비스 (N 계층 앱) 컨테이너 화**

- **Azure Vm에 Windows 컨테이너 기반 앱 배포**

- **Azure Container Service에서 Kubernetes에 Windows 컨테이너 기반 앱 배포**

## <a name="walkthrough-1-tour-of-eshop-legacy-apps"></a>연습 1: EShop 레거시 앱 둘러보기

### <a name="technical-walkthrough-availability"></a>기술 연습 가용성

EShopModernizing GitHub 리포지토리 wiki에서 전체 기술 연습을 사용할 수 있습니다.

[eShopModernizing wiki 연습](https://github.com/dotnet-architecture/eShopModernizing/wiki)

### <a name="overview"></a>개요

이 연습에서는 세 가지 샘플 레거시 응용 프로그램의 초기 구현을 탐색할 수 있습니다. 처음 두 샘플 웹 앱에는 모놀리식 아키텍처가 있으며 클래식 ASP.NET를 사용 하 여 만들었습니다. 한 응용 프로그램은 ASP.NET 4.x MVC를 기반으로 합니다. 두 번째 응용 프로그램은 ASP.NET 4. x Web Forms를 기반으로 합니다.
세 번째 앱은 클라이언트 WinForms 앱 및 [WCF (서버 쪽 Windows Communication Foundation)](../../framework/wcf/whats-wcf.md) 서비스로 구성 된 3 계층 앱입니다.

이러한 모든 응용 프로그램은 [EShopModernizing GitHub](https://github.com/dotnet-architecture/eShopModernizing)리포지토리에서 사용할 수 있습니다.

### <a name="goals"></a>목표

이 연습의 주요 목표는 단순히 이러한 앱과 해당 코드 및 구성을 익히는 것입니다. 테스트 목적으로 SQL database를 사용 하지 않고 모의 데이터를 생성 하 고 사용 하도록 앱을 구성할 수 있습니다. 이 선택적 구성은 분리 된 방식으로 종속성 주입을 기반으로 합니다.

### <a name="scenario-1-aspnet-web-apps"></a>시나리오 1: ASP.NET 웹 앱

아래 그림은 원래 레거시 ASP.NET 웹 응용 프로그램의 간단한 시나리오를 보여 줍니다.

![원래 레거시 ASP.NET 웹 응용 프로그램의 간단한 아키텍처 시나리오](./media/image5-1.png)

비즈니스 도메인 관점에서 두 앱은 모두 동일한 카탈로그 관리 기능을 제공 합니다. EShop enterprise 팀의 멤버는 앱을 사용 하 여 제품 카탈로그를 보고 편집 합니다.

다음 그림은 초기 앱 스크린샷을 보여 줍니다.

![ASP.NET MVC 및 ASP.NET Web Forms 응용 프로그램 (기존/레거시 기술)](./media/image5-2.png)

ASP.NET 4.x 이전 버전의 종속성 (MVC의 경우 또는 Web Forms의 경우)은 ASP.NET Core MVC를 사용 하 여 코드를 완전히 다시 작성 하지 않는 한 .NET Core에서 이러한 응용 프로그램을 실행 하지 않음을 의미 합니다.

### <a name="scenario-2-wcf-service-and-winforms-client-app-3-tier-app"></a>시나리오 2: WCF 서비스 및 WinForms 클라이언트 앱 (3 계층 앱)

아래 그림은 원본 3 계층 레거시 응용 프로그램의 간단한 시나리오를 보여 줍니다.

![WCF 서비스 및 WinForms 클라이언트 앱을 사용 하는 원래 레거시 3 계층 앱의 단순한 아키텍처 시나리오](./media/image5-1.5.png)

### <a name="benefits"></a>이점

이 연습의 이점은 다음과 같습니다. 코드 및 초기 앱에 대해 알아보세요.

### <a name="next-steps"></a>다음 단계

GitHub wiki에서이 콘텐츠를 자세히 살펴보세요.

- [기본 ASP.NET MVC 및 Web Forms "레거시" 앱 둘러보기](https://github.com/dotnet-architecture/eShopModernizing/wiki/01.-Tour-on-the-ASP.NET-MVC-and-WebForms-apps-implementation-code)
- [기본 WCF 서비스 및 WinForms (3 계층) "레거시" 앱 둘러보기](https://github.com/dotnet-architecture/eShopModernizing/wiki/21.-Tour-on-the-WCF-service-and-WinForms-apps)

## <a name="walkthrough-2-containerize-your-existing-net-applications-with-windows-containers"></a>연습 2: Windows 컨테이너를 사용 하 여 기존 .NET 응용 프로그램 컨테이너 화

### <a name="overview"></a>개요

Windows 컨테이너를 사용 하 여 MVC, Web Forms 또는 WCF를 기반으로 하는 것과 같은 기존 .NET 응용 프로그램을 프로덕션, 개발 및 테스트 환경에 배포할 수 있습니다.

### <a name="goals"></a>목표

이 연습의 목표는 기존 .NET Framework 응용 프로그램을 컨테이너 화 하기 위한 몇 가지 옵션을 보여 주는 것입니다. 다음과 같은 작업을 수행할 수 있습니다.

- [Docker 용 Visual studio 2017 Tools](/aspnet/core/host-and-deploy/docker/visual-studio-tools-for-docker) (visual studio 2017 이상 버전)를 사용 하 여 응용 프로그램을 컨테이너 화.

- [Dockerfile](https://docs.docker.com/engine/reference/builder/)을 수동으로 추가한 다음 [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)를 사용 하 여 응용 프로그램을 컨테이너 화.

- [Img2Docker](https://github.com/docker/communitytools-image2docker-win) 도구 (Docker의 오픈 소스 도구)를 사용 하 여 응용 프로그램을 컨테이너 화.

이 연습에서는 Docker 접근 방법에 대 한 Visual Studio 2017 도구에 중점을 두는 반면, Dockerfiles을 사용 하는 것과 관련해 서는 다른 두 가지 방법이 매우 유사 합니다.

### <a name="scenario-1-containerized-aspnet-web-apps"></a>시나리오 1: 컨테이너 화 된 ASP.NET web apps

아래 그림은 컨테이너 화 된 eShop 레거시 web apps 응용 프로그램에 대 한 시나리오를 보여줍니다.

![개발 환경에서 컨테이너 화 된 ASP.NET 응용 프로그램의 간소화 된 아키텍처 다이어그램](./media/image5-3.png)

### <a name="scenario-2-containerized-wcf-service"></a>시나리오 2: 컨테이너 화 된 WCF 서비스

아래 그림은 컨테이너 화 된 WCF 서비스를 사용 하는 3 계층 앱의 시나리오를 보여줍니다.

![개발 환경에서 컨테이너 화 된 WCF 서비스의 간소화 된 아키텍처 다이어그램](./media/image5-3.5.png)

### <a name="benefits"></a>이점

컨테이너에서 모놀리식 응용 프로그램을 실행 하면 다음과 같은 이점이 있습니다. 먼저 응용 프로그램에 대 한 이미지를 만듭니다. 이 시점부터 모든 배포가 동일한 환경에서 실행 됩니다. 모든 컨테이너는 동일한 OS 버전을 사용 하 고, 동일한 버전의 종속성을 설치 하 고, 동일한 .NET framework 버전을 사용 하며, 동일한 프로세스를 사용 하 여 빌드됩니다. 기본적으로 Docker 이미지를 사용 하 여 응용 프로그램의 종속성을 제어 합니다. 컨테이너를 배포할 때 종속성이 응용 프로그램과 함께 이동 합니다.

추가 혜택을 통해 개발자는 Windows 컨테이너에서 제공 하는 일관 된 환경에서 응용 프로그램을 실행할 수 있습니다. 특정 버전에만 표시 되는 문제는 스테이징 또는 프로덕션 환경에서 표시 하는 대신 즉시 발견 될 수 있습니다. 응용 프로그램이 컨테이너에서 실행 되는 경우 개발 팀의 멤버가 사용 하는 개발 환경의 차이점

컨테이너 화 된 응용 프로그램에는 flatter 스케일 아웃 곡선이 있습니다. 컨테이너 화 된 apps를 사용 하면 컴퓨터 당 일반 응용 프로그램 배포와 비교 했을 때 VM 또는 물리적 컴퓨터에서 컨테이너를 기반으로 더 많은 응용 프로그램 및 서비스 인스턴스를 사용할 수 있습니다. 이는 특히 Kubernetes와 같은 orchestrator을 사용 하는 경우 더 높은 밀도와 필요한 리소스의 수를 줄입니다.

이상적인 상황에서 컨테이너 화는 응용 프로그램 코드 (C\#)를 변경할 필요가 없습니다. 대부분의 시나리오에서는 Docker 배포 메타 데이터 파일 (Dockerfiles 및 Docker Compose 파일)만 필요 합니다.

### <a name="next-steps"></a>다음 단계

GitHub wiki에서이 콘텐츠를 자세히 살펴보세요.

- [Windows 컨테이너 및 Docker를 사용 하 여 .NET Framework 웹 앱을 컨테이너 화 하는 방법](https://github.com/dotnet-architecture/eShopModernizing/wiki/02.-How-to-containerize-the-.NET-Framework-web-apps-with-Windows-Containers-and-Docker)
- [WCF 서비스에 Docker 지원 추가](https://github.com/dotnet-architecture/eShopModernizing/wiki/22.-Adding-Docker-Support)

## <a name="walkthrough-3-deploy-your-windows-containers-based-app-to-azure-vms"></a>연습 3: Azure Vm에 Windows 컨테이너 기반 앱 배포

### <a name="technical-walkthrough-availability"></a>기술 연습 가용성

EShopModernizing GitHub 리포지토리 wiki에서 전체 기술 연습을 사용할 수 있습니다.<https://github.com/dotnet-architecture/eShopModernizing/wiki/06.-Deploying-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)>

### <a name="overview"></a>개요

Azure에서 Windows Server 2016 VM (가상 머신)의 Docker 호스트에 배포 하면 개발/테스트/스테이징 환경을 신속 하 게 설정할 수 있습니다. 또한 테스터 또는 비즈니스 사용자가 앱의 유효성을 검사할 수 있는 일반적인 장소를 제공 합니다. Vm은 또한 유효한 IaaS (Infrastructure as a Service) 프로덕션 환경으로 사용할 수 있습니다.

### <a name="goals"></a>목표

이 연습의 목표는 windows Server 2016 이상 버전을 기반으로 하는 Azure Vm에 Windows 컨테이너를 배포할 때 사용할 수 있는 여러 대안을 보여 주는 것입니다.

### <a name="scenarios"></a>시나리오

이 연습에서는 몇 가지 시나리오에 대해 설명 합니다.

#### <a name="scenario-a-deploy-to-an-azure-vm-from-a-dev-pc-through-docker-engine-connection"></a>시나리오 A: Docker 엔진 연결을 통해 개발 PC에서 Azure VM에 배포

![Docker 엔진 연결을 통해 개발 PC에서 Azure VM에 배포](./media/image5-4.png)

**그림 5-4.** Docker 엔진 연결을 통해 개발 PC에서 Azure VM에 배포

#### <a name="scenario-b-deploy-to-an-azure-vm-through-a-docker-registry"></a>시나리오 B: Docker 레지스트리를 통해 Azure VM에 배포

![Docker 레지스트리를 통해 Azure VM에 배포](./media/image5-5.png)

**그림 5-5.** Docker 레지스트리를 통해 Azure VM에 배포

#### <a name="scenario-c-deploy-to-an-azure-vm-from-cicd-pipelines-in-azure-devops-services"></a>시나리오 C: Azure DevOps Services의 CI/CD 파이프라인에서 Azure VM에 배포

![Azure DevOps Services의 CI/CD 파이프라인에서 Azure VM에 배포](./media/image5-6.png)

**그림 5-6.** Azure DevOps Services의 CI/CD 파이프라인에서 Azure VM에 배포

### <a name="azure-vms-for-windows-containers"></a>Windows 용 Azure Vm 컨테이너

Windows 용 Azure Vm 컨테이너는 Docker 엔진이 설정 된 Windows Server 2016, Windows 10 이상 버전을 기반으로 하는 Vm입니다. 대부분의 경우 Windows Server 2016은 Azure Vm에서 사용 됩니다.

Azure는 현재 **컨테이너와 Windows Server 2016**라는 VM을 제공 합니다. 이 VM을 사용 하 여 Windows Server Core 또는 Windows Nano Server를 통해 새 Windows Server 컨테이너 기능을 사용해 볼 수 있습니다. 컨테이너 OS 이미지가 설치 된 다음 VM을 Docker에서 사용할 준비가 되었습니다.

### <a name="benefits"></a>이점

Windows 컨테이너를 온-프레미스 Windows Server 2016 Vm에 배포할 수 있지만, Azure에 배포 하는 경우 즉시 사용 가능한 Windows Server 컨테이너 Vm을 사용 하 여 쉽게 시작할 수 있습니다. 테스터에 게 액세스할 수 있는 일반적인 온라인 위치와 Azure 가상 머신 확장 집합을 통한 자동 확장성도 얻을 수 있습니다.

### <a name="next-steps"></a>다음 단계

GitHub wiki에서이 콘텐츠를 자세히 살펴보세요.

<https://github.com/dotnet-architecture/eShopModernizing/wiki/06.-Deploying-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)>

## <a name="walkthrough-4-deploy-your-windows-containers-based-apps-to-azure-container-instances-aci"></a>연습 4: Azure Container Instances (ACI)에 Windows 컨테이너 기반 앱 배포

### <a name="technical-walkthrough-availability"></a>기술 연습 가용성

EShopModernizing GitHub 리포지토리 wiki에서 전체 기술 연습을 사용할 수 있습니다.

[ACI에 앱 배포 (Azure Container Instances)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

### <a name="overview"></a>개요

[ACI (Azure Container Instances)](https://docs.microsoft.com/azure/container-instances/) 는 컨테이너의 단일 인스턴스를 배포할 수 있는 컨테이너 개발/테스트/스테이징 환경을 준비 하는 가장 빠른 방법입니다.

### <a name="goals"></a>목표

이 연습에서는 Azure Container Instances (ACI)에 Windows 컨테이너를 배포할 때의 주요 시나리오와 ACI에 eShopModernizing Apps를 배포할 수 있는 방법을 보여 줍니다.

### <a name="scenarios"></a>시나리오

앱 (MVC 앱, WebForms 앱 또는 WCF 서비스) 중 하나 또는 모두를 배포 하는 것과 같이 eShopModernizing 앱을 ACI에 배포 하는 것에 대 한 변형이 있을 수 있습니다. 아래에 표시 된 다음 시나리오에서는 ASP.NET MVC 앱과 SQL Server 컨테이너를 ACI (Azure Container Instances)에 컨테이너에 배포 하는 것을 볼 수 있습니다.

![개발 환경에서 ACI에 배포](./media/image5-3.5.6.png)

### <a name="benefits"></a>이점

Azure Container Instances를 사용 하면 가상 머신을 프로 비전 하거나 상위 수준 서비스를 채택 하지 않고도 Azure에서 Docker 컨테이너를 쉽게 만들고 관리할 수 있습니다. ACI를 사용 하면 Azure에서 Windows 컨테이너를 직접 배포 하 고 몇 초 내에 FQDN (정규화 된 도메인 이름)을 사용 하 여 인터넷에 노출할 수 있습니다. Docker 허브 또는 Azure 컨테이너와 같은 Docker 레지스트리에서 Windows 컨테이너 이미지가 준비 된 경우 레지스트리).

### <a name="considerations"></a>고려 사항

Docker 이미지가 있어야 하기 때문에 전체 .NET Framework/ASP.NET SQL Server 또는 ACI (Azure Container Instances)로 Windows 컨테이너를 배포 하는 것은 일반 Docker 호스트 (예: windows 컨테이너를 사용 하는 Windows Server 2016)에 배포 하는 만큼 빠르지 않습니다. 다운로드 (Docker 레지스트리에서 끌어온) 및 SQL 컨테이너 이미지 (15.1 GB) 및 ASP.NET 컨테이너 이미지 (13.9 g b)의 크기 마다 크기가 크게 증가 하지만 자체 Docker 호스트를 유지 관리 하는 것 보다 훨씬 저렴 합니다 (영구적으로 온라인 상태로 유지 됨). Windows 컨테이너 VM이 있는 windows Server 2016) azure에서 Kubernetes (AKS)와 같은 전체 orchestrator를 언급 하지 않습니다. 즉, 프로덕션 배포에 적합 한 선택입니다.

기본적으로 Azure Container Instances를 사용 하는 것은 개발/테스트 시나리오 및 CI/CD 파이프라인에 매우 매력적인 옵션입니다.

## <a name="next-steps"></a>다음 단계

GitHub wiki에서이 콘텐츠를 자세히 살펴보세요.

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

## <a name="walkthrough-5-deploy-your-windows-containers-based-apps-to-kubernetes-in-azure-container-service"></a>연습 5: Azure Container Service에서 Kubernetes에 Windows 컨테이너 기반 앱 배포

### <a name="technical-walkthrough-availability"></a>기술 연습 가용성

EShopModernizing GitHub 리포지토리 wiki에서 전체 기술 연습을 사용할 수 있습니다.

<https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

### <a name="overview"></a>개요

Windows 컨테이너를 기반으로 하는 응용 프로그램은 플랫폼을 신속 하 게 사용 하 여 IaaS Vm에서 훨씬 더 멀리 이동 해야 합니다. 이는 높은 확장성 및 자동화 된 확장성을 쉽게 구현 하 고 자동화 된 배포 및 버전 관리를 대폭 개선 하는 데 필요 합니다. [Azure Container service](https://azure.microsoft.com/services/container-service/)에서 사용할 수 있는 orchestrator [Kubernetes](https://kubernetes.io/)를 사용 하 여 이러한 목표를 달성할 수 있습니다.

### <a name="goals"></a>목표

이 연습의 목표는 Azure Container Service에서 Windows 컨테이너 기반 응용 프로그램을 Kubernetes ( *K8s*라고도 함)에 배포 하는 방법을 배우는 것입니다. Kubernetes를 처음부터 배포 하는 과정은 다음 두 단계로 진행 됩니다.

1. Azure Container Service에 Kubernetes 클러스터를 배포 합니다.

2. 응용 프로그램 및 관련 리소스를 Kubernetes 클러스터에 배포 합니다.

### <a name="scenarios"></a>시나리오

#### <a name="scenario-a-deploy-directly-to-a-kubernetes-cluster-from-a-dev-environment"></a>시나리오 A: 개발 환경에서 Kubernetes 클러스터에 직접 배포

![개발 환경에서 Kubernetes 클러스터에 직접 배포](./media/image5-7.png)

**그림 5-7.** 개발 환경에서 Kubernetes 클러스터에 직접 배포

#### <a name="scenario-b-deploy-to-a-kubernetes-cluster-from-cicd-pipelines-in-azure-devops-services"></a>시나리오 B: Azure DevOps Services의 CI/CD 파이프라인에서 Kubernetes 클러스터에 배포

![Azure DevOps Services의 CI/CD 파이프라인에서 Kubernetes 클러스터에 배포](./media/image5-8.png)

**그림 5-8.** Azure DevOps Services의 CI/CD 파이프라인에서 Kubernetes 클러스터에 배포

### <a name="benefits"></a>이점

Kubernetes의 클러스터에 배포 하는 데는 많은 이점이 있습니다. 가장 큰 혜택은 사용 하려는 컨테이너 인스턴스 수에 따라 응용 프로그램을 확장 하 고 (기존 노드의 내부 확장성) 클러스터의 노드 또는 Vm 수에 따라 응용 프로그램을 확장할 수 있는 프로덕션 준비 환경을 얻는 것입니다. 클러스터의 글로벌 확장성).

Azure Container Service는 Azure 전용의 인기 있는 오픈 소스 도구 및 기술을 최적화 합니다. 컨테이너와 응용 프로그램 구성 모두에 대 한 이식성을 제공 하는 오픈 솔루션이 제공 됩니다. 크기, 호스트 수 및 orchestrator 도구-컨테이너 서비스를 선택 하 여 다른 모든 항목을 처리 합니다.

Kubernetes를 통해 개발자는 물리적 컴퓨터와 가상 컴퓨터에 대 한 고려에서 다음과 같은 기능을 용이 하 게 하는 컨테이너 중심 인프라를 계획 하는 과정을 진행할 수 있습니다.

- 여러 컨테이너를 기반으로 하는 응용 프로그램

- 컨테이너 인스턴스 및 수평 자동 크기 조정 복제

- 이름 지정 및 검색 (예: 내부 DNS)

- 부하 분산

- 롤링 업데이트

- 비밀 배포

- 응용 프로그램 상태 검사

## <a name="next-steps"></a>다음 단계

GitHub wiki에서이 콘텐츠를 자세히 살펴보세요.<https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

## <a name="walkthrough-6-deploy-your-windows-containers-based-apps-to-azure-app-service-for-containers"></a>연습 6: 컨테이너에 대 한 Azure App Service에 Windows 컨테이너 기반 앱 배포

### <a name="technical-walkthrough-availability"></a>기술 연습 가용성

EShopModernizing GitHub 리포지토리 wiki에서 전체 기술 연습을 사용할 수 있습니다.

<https://github.com/dotnet-architecture/eShopModernizing/wiki/Deploy-Windows-Container-to-Azure-App-Service>

### <a name="overview"></a>개요

Windows 컨테이너를 사용 하는 간단한 컨테이너 화 된 응용 프로그램을 컨테이너에 대 한 Azure App Service 쉽게 배포할 수 있습니다. 이는 대부분의 Windows 컨테이너 기반 응용 프로그램에 권장 되는 방법입니다.

### <a name="goals"></a>목표

이 연습의 목표는 Windows 컨테이너 기반 응용 프로그램을 배포 하 여 레지스트리 (Docker 허브 또는 Azure Container Registry)에서 컨테이너에 대 한 Azure App Service 하는 방법을 배우는 것입니다.

### <a name="scenario"></a>시나리오

![컨테이너의 Azure App Service에 Windows 컨테이너 기반 앱 배포](./media/image5-11.png)

### <a name="benefits"></a>이점

컨테이너의 Azure App Service에 배포 하면 Azure App Service의 PaaS 이점과 쌍을 이루는 컨테이너의 이점이 제공 됩니다. App service는 수직 및 수평으로 쉽게 확장할 수 있으며 변화 하는 요구에 맞게 자동 크기 조정을 구성할 수 있습니다. 가동 중지 시간 없이 업데이트를 수행할 수 있으며, 레지스트리에서 연속 배포를 구성 하는 것도 쉽게 구성할 수 있습니다.

## <a name="next-steps"></a>다음 단계

GitHub wiki에서이 콘텐츠를 자세히 살펴보세요.<https://github.com/dotnet-architecture/eShopModernizing/wiki/Deploy-Windows-Container-to-Azure-App-Service>

> [!div class="step-by-step"]
> [이전](modernize-existing-apps-to-cloud-optimized/migrate-to-hybrid-cloud-scenarios.md)
> [다음](conclusions.md) <!-- Next Chapter -->
