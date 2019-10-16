---
title: Docker 애플리케이션에 대한 외부 루프 DevOps 워크플로의 단계
description: DevOps 워크플로의 "외부 루프"에 대한 단계 알아보기
ms.date: 02/15/2019
ms.openlocfilehash: 5687caff0c635e7add135654a8f564b2c509cbf8
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834567"
---
# <a name="steps-in-the-outer-loop-devops-workflow-for-a-docker-application"></a>Docker 애플리케이션에 대한 외부 루프 DevOps 워크플로의 단계

그림 5-1은 DevOps 외부 루프 워크플로를 구성하는 단계를 아주 자세히 묘사하여 보여줍니다.

![이 다이어그램은 DevOps의 "외부 루프"를 보여줍니다. 코드가 리포지토리에 푸시되면 CI 파이프라인이 시작된 후 CD 파이프라인을 시작하고 해당 파이프라인에서 애플리케이션이 배포됩니다. 배포된 애플리케이션에서 수집된 메트릭은 개발 워크로드에 피드백되며, 여기서 "내부 루프"가 발생하므로 개발 팀은 사용자 및 비즈니스 요구에 응답하는 실질적인 데이터를 갖게 됩니다.](./media/image1.png)

**그림 5-1**. Microsoft 도구를 사용하는 Docker 애플리케이션에 대한 DevOps 외부 루프 워크플로

이제 이러한 각 단계를 자세히 살펴보겠습니다.

## <a name="step-1-inner-loop-development-workflow"></a>1단계: 내부 루프 개발 워크플로

이 단계는 4 장에서 자세히 설명하지만, 요약하면 여기서 외부 루프가 시작되며 이 시점에 개발자가 코드를 원본 제어 관리 시스템(예: Git)에 푸시하여 CI 파이프라인 작업을 시작합니다.

## <a name="step-2-source-code-control-integration-and-management-with-azure-devops-services-and-git"></a>2단계: Azure DevOps Services 및 Git를 사용하여 소스 코드 컨트롤 통합 및 관리

이 단계에서 버전 관리 시스템이 팀의 여러 개발자로부터 들어오는 모든 코드의 통합된 버전을 수집하게 해야 합니다.

SCC(소스 코드 제어) 및 소스 코드 관리는 대부분의 개발자에게 습관처럼 생각될 수 있지만 DevOps 수명 주기에서 Docker 애플리케이션을 만드는 경우 개발자의 머신에서 애플리케이션과 함께 Docker 이미지를 글로벌 Docker 레지스트리(예: Azure Container Registry 또는 Docker Hub)에 직접 제출해서는 안 된다는 점이 매우 중요합니다. 반대로 프로덕션 환경에 릴리스 및 배포할 Docker 이미지는 소스 코드 리포지토리(예: Git)를 기반으로 글로벌 빌드 또는 CI 파이프라인에 통합되는 소스 코드에서만 생성해야 합니다.

개발자가 생성하는 로컬 이미지는 개발자 자신의 머신 내에서 테스트용으로만 사용해야 합니다. DevOps 파이프라인을 SCC 코드에서 활성화하는 것이 중요한 것도 바로 이 때문입니다.

Azure DevOps Services 및 Team Foundation Server는 Git 및 Team Foundation 버전 관리를 지원합니다. 이들 중에서 선택하여 엔드투엔드 Microsoft 환경에서 사용할 수 있습니다. 그러나 외부 리포지토리(예: GitHub, 온-프레미스 Git 리포지토리 또는 Subversion)에서 코드를 관리하고 해당 리포지토리에 연결하여 DevOps CI 파이프라인의 시작점으로 코드를 가져올 수도 있습니다.

## <a name="step-3-build-ci-integrate-and-test-with-azure-devops-services-and-docker"></a>3단계: Azure DevOps Services 및 Docker를 사용하여 빌드, CI, 통합 및 테스트

CI는 최신 소프트웨어 테스트 및 제공을 위한 표준으로 부상 했습니다. Docker 솔루션은 개발 팀과 운영 팀 간에 관심사를 명확하게 분리합니다. Docker 이미지의 불변성 덕분에 CI를 통해 개발하고 테스트하는 내용과 프로덕션에서 실행하는 내용 간의 반복 가능한 배포가 보장됩니다. 개발자 랩톱 및 테스트 인프라 간에 배포되는 Docker 엔진을 통해 환경 간에 컨테이너를 이식할 수 있게 됩니다.

이 시점에서 올바른 코드가 제출된 버전 관리 시스템을 보유한 후 코드를 선택하고 글로벌 빌드 및 테스트를 실행하기 위해 *빌드 서비스*가 필요합니다.

이 단계(CI, 빌드, 테스트)에 대한 내부 워크플로는 코드 리포지토리(Git 등), 빌드 서버(Azure DevOps 서비스), Docker 엔진 및 Docker 레지스트리 코드 리포지토리로 구성된 CI 파이프라인을 구축하는 과정입니다.

애플리케이션을 빌드하고 CI 파이프라인을 설정하고 빌드된 "아티팩트"를 다음 단계에서 설명하는 "아티팩트 리포지토리"에 게시하기 위한 기초로 Azure DevOps Services를 사용할 수 있습니다.

배포를 위해 Docker를 사용하는 경우 배포할 "최종 아티팩트"는 애플리케이션 또는 해당 애플리케이션에 포함된 서비스를 포함하는 Docker 이미지입니다. 해당 이미지는 *Docker 레지스트리*(Azure Container Registry와 같은 프라이빗 리포지토리 또는 공식 기본 이미지에 널리 사용되는 Docker Hub 레지스트리와 같은 공용 리포지토리)에 푸시되거나 게시됩니다.

다음은 기본 개념입니다. CI 파이프라인은 Git와 같은 SCC 리포지토리에 대한 커밋에 의해 시작됩니다. 이 커밋은 그림 5-2와 같이 Azure DevOps Services가 Docker 컨테이너 내에서 빌드 작업을 실행하고 해당 작업이 성공적으로 완료되면 Docker 이미지를 Docker 레지스트리에 푸시하게 합니다.

![외부 루프의 첫 번째 부분은 코드에서 실행, 디버그 및 유효성 검사 후 빌드 및 테스트 CI 단계까지의 코드 리포지토리에 이르는 1단계 ~ 3단계를 포함합니다.](./media/image2.png)

**그림 5-2**. CI에 포함되는 단계

다음은 Docker 및 Azure DevOps Services를 사용하는 기본적인 CI 워크플로입니다.

1. 개발자가 SCC 리포지토리(Git/Azure DevOps Services, GitHub 등)에 대한 커밋을 푸시합니다.

2. Azure DevOps Services 또는 Git를 사용하는 경우 CI는 기본 제공됩니다. 즉, Azure DevOps Services에서 확인란만 선택하면 됩니다. 외부 SCC(예: GitHub)를 사용하는 경우 `webhook`에서 Git/GitHub에 대한 업데이트 또는 푸시를 Azure DevOps Services에 알립니다.

3. Azure DevOps Services는 이미지를 설명하는 Dockerfile 및 애플리케이션과 테스트 코드를 포함하여 SCC 리포지토리를 풀합니다.

4. Azure DevOps Services는 Docker 이미지를 빌드하고 빌드 번호로 해당 이미지에 레이블을 표시합니다.

5. Azure DevOps Services는 프로비저닝된 Docker Host 내에서 Docker 컨테이너를 인스턴스화하고 적절한 테스트를 실행합니다.

6. 테스트에 성공하면 먼저 "빌드 성공"을 알 수 있도록 이미지에 의미 있는 이름으로 레이블("/1.0.0" 또는 다른 레이블)을 표시한 다음, Docker 레지스트리(Docker Hub, Azure Container Registry, DTR 등)에 푸시합니다.

### <a name="implementing-the-ci-pipeline-with-azure-devops-services-and-the-docker-extension-for-azure-devops-services"></a>Azure DevOps Services 및 Azure DevOps Services용 Docker 확장을 사용하여 CI 파이프라인 구현

Visual Studio Azure DevOps Services는 CI/CD 파이프라인에 사용하여 Docker 이미지 빌드, 인증된 Docker 레지스트리에 Docker 이미지 푸시, Docker 이미지 실행, Docker CLI가 제공하는 다른 작업 실행을 수행할 수 있는 빌드 및 릴리스 템플릿을 포함합니다. 또한 다중 컨테이너 Docker 애플리케이션을 빌드, 푸시 또는 실행하는 데 사용할 수 있는 Docker Compose 작업을 추가하거나 그림 5-3과 같이 Docker Compose CLI가 제공하는 다른 작업을 실행할 수 있습니다.

![Azure DevOps의 Docker CI 파이프라인 브라우저 보기](./media/image3.png)

**그림 5-3**. 빌드 및 릴리스 템플릿과 관련 작업을 포함하는 Azure DevOps Services의 Docker CI 파이프라인

이 템플릿과 작업을 사용하여 Azure Service Fabric, Azure Kubernetes Service 및 유사한 제품에서 빌드 / 테스트 및 배포에 대해 CI/CD 아티팩트를 구성할 수 있습니다.

이러한 Visual Studio Team Services 작업을 통해 Azure 및 선호하는 Docker 레지스트리(Azure Container Registry, Docker Hub, 프라이빗 Docker DTR 또는 다른 Docker 레지스트리)에서 프로비저닝되는 Linux-Docker Host/VM을 빌드하면 Docker CI 파이프라인을 아주 일관된 방법으로 조립할 수 있습니다.

***요구 사항:***

- Azure DevOps Services 또는 온-프레미스 설치의 경우 Team Foundation Server 2015 업데이트 3 이상

- Docker 이진 파일을 포함하는 Azure DevOps Services 에이전트

  이러한 에이전트 중 하나를 만드는 쉬운 방법은 Docker를 사용하여 Azure DevOps Services 에이전트 Docker 이미지를 기반으로 컨테이너를 실행하는 것입니다.

> [!정보] Azure DevOps Services Docker CI 파이프라인 조립에 대해 더 자세히 알아보려면 다음 사이트를 방문하세요.
>
> - Visual Studio Team Services(현재 Azure DevOps Services) 에이전트를 Docker 컨테이너로 실행: \
>   <https://hub.docker.com/_/microsoft-azure-pipelines-vsts-agent>
>
> - Azure DevOps Services를 사용하여 .NET Core Linux Docker 이미지 빌드: \
>   <https://blogs.msdn.microsoft.com/stevelasker/2016/06/13/building-net-core-linux-docker-images-with-visual-studio-team-services/>
>
> - Docker 지원을 사용하여 Linux 기반 Visual Studio Team Service 빌드 머신 구축: \
>   <http://donovanbrown.com/post/2016/06/03/Building-a-Linux-Based-Visual-Studio-Team-Service-Build-Machine-with-Docker-Support>

### <a name="integrate-test-and-validate-multi-container-docker-applications"></a>다중 컨테이너 Docker 애플리케이션 통합, 테스트 및 유효성 검사

일반적으로 대부분의 Docker 애플리케이션은 단일 컨테이너가 아닌 다중 컨테이너로 구성됩니다. 마이크로서비스당 하나의 컨테이너가 있는 마이크로서비스 지향 애플리케이션이 좋은 예입니다. 그러나 마이크로서비스 방식의 패턴을 엄격하게 따르지 않으면 Docker 애플리케이션이 여러 컨테이너 또는 서비스로 구성될 가능성이 있습니다.

따라서 CI 파이프라인에서 애플리케이션 컨테이너를 빌드한 후 통합 Docker 호스트 또는 컨테이너가 배포되는 테스트 클러스터 내의 모든 컨테이너를 포함하는 애플리케이션의 전체적인 배포, 통합 및 테스트도 수행해야 합니다.

단일 호스트를 사용하는 경우 Docker-Compose와 같은 Docker 명령을 사용하여 테스트할 관련 컨테이너를 빌드 및 배포하고 단일 VM에서 Docker 환경의 유효성을 검사할 수 있습니다. 그러나 DC/OS, Kubernetes 또는 Docker Swarm 등의 다른 오케스트레이터 클러스터로 작업하는 경우 선택한 클러스터/스케줄러에 따라 다른 메커니즘 또는 오케스트레이터를 통해 컨테이너를 배포해야 합니다.

다음은 Docker 컨테이너에 대해 실행할 수 있는 몇 가지 테스트 유형입니다.

- Docker 컨테이너에 대한 단위 테스트

- 상호 관련된 애플리케이션 또는 마이크로서비스의 그룹 테스트

- 프로덕션 및 "카나리아" 릴리스에서 테스트

중요한 점은 통합 및 기능 테스트를 실행할 때 해당 테스트를 컨테이너의 외부에서 실행해야 한다는 것입니다. 컨테이너는 정적 이미지를 기반으로 하고 해당 이미지는 프로덕션에 배포할 이미지와 정확히 같아야 하기 때문에 테스트는 배포 중인 컨테이너에 포함되거나 해당 컨테이너에서 실행되지 않습니다.

여러 클러스터(테스트 클러스터, 준비 클러스터 및 프로덕션 클러스터)를 포함하는 경우와 같은 고급 시나리오를 테스트할 때 실용적인 옵션은 이미지를 여러 클러스터에서 테스트할 수 있도록 레지스트리에 게시하는 것입니다.

### <a name="push-the-custom-application-docker-image-into-your-global-docker-registry"></a>글로벌 Docker 레지스트리에 사용자 지정 애플리케이션 Docker 이미지 푸시

Docker 이미지를 테스트하고 유효성을 검사한 후 태그를 지정하고 Docker 레지스트리에 게시하는 것이 좋습니다. Docker 레지스트리는 QA 및 프로덕션 환경에 배포할 사용자 지정 테스트(일명 "성공적인 이미지")를 저장하는 중심 위치이므로 Docker 애플리케이션 수명 주기에서 중요한 부분입니다.

SCC 레지스트리(예: Git)에 저장된 애플리케이션 코드가 "신뢰할 수 있는 원본"인 이유와 유사한 원리로, Docker 레지스트리는 QA 또는 프로덕션 환경에 배포할 이진 애플리케이션 또는 비트의 "신뢰할 수 있는 원본"입니다.

일반적으로 Azure Container Registry의 프라이빗 리포지토리 또는 Docker Trusted Registry와 같은 온-프레미스 레지스트리 또는 제한된 액세스 권한을 가진 공용 클라우드 레지스트리(예: Docker Hub)에 사용자 지정 이미지에 대한 프라이빗 리포지토리가 있는 것이 좋습니다. 단, 마지막 레지스트리의 경우 코드가 오픈 소스가 아니더라도 공급업체의 보안을 신뢰해야 합니다. 어느 방법이든 사용하는 방법은 유사하며 그림 5-4와 같이 `docker push` 명령을 기반으로 합니다.

![3단계에서 통합 및 테스트(CI)를 빌드하는 경우 결과로 얻은 Docker 이미지를 프라이빗 또는 공용 레지스트리에 게시할 수 있습니다.](./media/image4.png)

**그림 5-4**. Docker 레지스트리에 사용자 지정 이미지 게시

Azure Container Registry, Amazon Web Services Container Registry, Google Container Registry, Quay Registry 등 클라우드 공급업체의 Docker 레지스트리 제품이 많이 있습니다.

Docker 작업을 사용하면 그림 5-5와 같이 다중 태그를 통해 `docker-compose.yml` 파일에 의해 정의되고 다중 태그를 포함하는 서비스 이미지 세트를 인증된 Docker 레지스트리(예: Azure Container Registry)에 푸시할 수 있습니다.

![Azure DevOps에서 이미지를 레지스트리에 푸시하기 위한 단계의 브라우저 보기](./media/image5.png)

**그림 5-5**. Azure DevOps Services를 사용하여 Docker 레지스트리에 사용자 이미지 푸시

> [!정보] Azure Container Registry에 대한 자세한 내용은 <https://aka.ms/azurecontainerregistry>를 참조하세요.

## <a name="step-4-cd-deploy"></a>4단계: CD, 배포

Docker 이미지의 불변성 덕분에 CI를 통해 개발하고 테스트하는 내용과 프로덕션에서 실행하는 내용을 이용한 반복 가능한 배포가 보장됩니다. Docker 레지스트리(프라이빗 또는 공용)에 애플리케이션 Docker 이미지를 게시한 후 Azure DevOps Services 파이프라인 작업 또는 Azure DevOps Services Release Management를 사용하여 CD 파이프라인에서 해당 이미지를 여러 환경(프로덕션, QA, 준비 등)에 배포할 수 있습니다.

그러나 이 시점에는 배포하는 Docker 애플리케이션의 종류에 따라 달라집니다. 몇 개의 컨테이너 또는 서비스로 구성되고 몇 대의 서버 또는 VM에 배포되는 모놀리식 애플리케이션과 같은 간단한 애플리케이션을 배포하는 작업은 하이퍼스케일 기능을 갖춘 마이크로서비스 지향 애플리케이션과 같은 더 복잡한 애플리케이션을 배포하는 작업과 다릅니다(구성 및 배포 관점에서). 두 시나리오를 다음 섹션에서 설명합니다.

### <a name="deploying-composed-docker-applications-to-multiple-docker-environments"></a>구성된 Docker 애플리케이션을 Docker 환경에 배포

먼저 단일 환경 또는 다중 환경(QA, 준비 및 프로덕션)에서 간단한 Docker 호스트(VM 또는 서버)를 배포하는 덜 복잡한 시나리오를 살펴보겠습니다. 이 시나리오에서는 그림 5-6과 같이 내부적으로 CD 파이프라인이 Docker-Compose를 사용하여(Azure DevOps Services 배포 작업에서) Docker 애플리케이션을 관련 컨테이너 세트와 함께 배포할 수 있습니다.

![CD 배포 단계(#4)에서는 Q&A, 준비 및 프로덕션 등 서로 다른 환경에 게시할 수 있습니다.](./media/image6.png)

**그림 5-6**. 간단한 Docker 호스트 환경 레지스트리에 애플리케이션 컨테이너 배포

그림 5-7은 작업 추가 대화 상자에서 Docker Compose를 클릭하여 Azure DevOps Services를 통해 빌드 CI를 QA/테스트 환경에 연결할 수 있는 방법을 강조합니다. 그러나 준비 또는 프로덕션 환경에 배포하는 경우 일반적으로 다중 환경(QA, 준비 및 프로덕션 등)을 처리하는 Release Management 기능을 사용합니다. 단일 Docker 호스트에 배포하는 경우 Azure DevOps Services "Docker Compose" 작업(후드 아래에서 `docker-compose up` 명령을 호출하는)을 사용합니다. AKS(Azure Kubernetes Service)에 배포하는 경우 다음 섹션에서 설명하듯이 Docker 배포 작업을 사용합니다.

![Docker Compose 작업 추가 브라우저 보기](./media/image7.png)

**그림 5-7**. Azure DevOps Services 파이프라인에서 Docker Compose 작업 추가

Azure DevOps Services에서 릴리스를 만드는 경우 입력 아티팩트 세트를 가져옵니다. 이러한 아티팩트의 목적은 모든 환경에 걸쳐 릴리스의 수명이 계속되는 동안 변하지 않도록 하는 것입니다. 컨테이너를 도입하는 경우 입력 아티팩트는 배포할 레지스트리의 이미지를 식별합니다. 이러한 이미지는 식별되는 방법에 따라 `docker-compose` 파일에서 `myimage:latest`를 참조하는 가장 명백한 경우 릴리스의 지속기간 동안 동일하게 유지된다는 보장이 없습니다.

Azure DevOps Services 템플릿을 사용하면 특정 레지스트리 이미지 다이제스트를 포함하는 빌드 아티팩트를 생성하여 동일한 이미지 이진 파일을 고유하게 식별하도록 보장할 수 있습니다. 이것이 바로 릴리스에 대한 입력으로 사용하고자 하는 기능입니다.

### <a name="managing-releases-to-docker-environments-by-using-azure-devops-services-release-management"></a>Azure DevOps Services Release Management를 사용하여 Docker 환경에 대한 릴리스 관리

Azure DevOps Services 템플릿을 통해 새 이미지를 빌드하고, Docker 레지스트리에 게시하고, Linux 또는 Windows 호스트에서 실행하고, `docker-compose`와 같은 명령을 사용하여 여러 컨테이너를 전체 애플리케이션으로 배포할 수 있습니다. 이러한 작업은 모두 그림 5-8과 같은 여러 환경에 사용하기 위한 Azure DevOps Services Release Management 기능을 통해 수행됩니다.

![Docker Compose 릴리스를 구성하는 Azure DevOps의 브라우저 보기](./media/image8.png)

**그림 5-8**. Azure DevOps Services Release Management에서 Azure DevOps Services Docker Compose 작업 구성

그러나 그림 5-6에 나와 있고 그림 5-8에서 구현되는 시나리오는 단일 Docker 호스트 및 VM에 배포되고 이미지당 단일 컨테이너 또는 인스턴스가 있는 간단한 시나리오이며, 개발 또는 테스트 시나리오용으로만 사용해야 한다는 점을 염두에 두어야 합니다. 대부분의 엔터프라이즈 프로덕션 시나리오에서는 여러 노드, 서버 및 VM 간의 부하 분산을 통해 HA(고가용성) 및 관리하기 쉬운 확장성을 갖기를 원하고 "인텔리전트 장애 조치(failover)" 기능을 더하여 서버 또는 노드에 장애가 발생한 경우 해당 서비스 및 컨테이너가 다른 호스트 서버 또는 VM으로 이동됩니다. 이 경우 컨테이너 클러스터, 오케스트레이터 및 스케줄러 등과 같은 고급 기술이 필요합니다. 따라서 해당 클러스터에 배포하는 방법은 다음 섹션에서 설명하는 고급 시나리오를 처리하는 방법입니다.

### <a name="deploying-docker-applications-to-docker-clusters"></a>Docker 클러스터에 Docker 애플리케이션 배포

분산 애플리케이션의 특성 때문에 역시 분산된 컴퓨팅 리소스가 필요합니다. 프로덕션 규모 기능을 가지려면 풀링된 리소스를 기반으로 높은 확장성 및 고가용성을 제공하는 클러스터링 기능이 있어야 합니다.

CLI 도구 또는 웹 UI에서 수동으로 컨테이너를 해당 클러스터에 배포할 수 있지만, 그러한 종류의 수동 작업을 보류하고 확장 또는 모니터링과 같은 배포 테스트 또는 관리 목적을 찾아야 합니다.

CD 관점 및 구체적으로 Azure DevOps Services 관점에서 보면 그림 5-9와 같이 컨테이너화된 애플리케이션을 컨테이너 서비스의 배포된 클러스터에 배포하는 Azure DevOps Services Release Management 환경에서 명시적으로 만들어진 배포 작업을 실행할 수 있습니다.

![또한 CD 배포 단계(#4)에서는 오케스트레이터를 통해 클러스터에 배포할 수 있습니다.](./media/image9.png)

**그림 5-9**. 컨테이너 서비스에 분산 애플리케이션 배포

처음에 특정 클러스터 또는 오케스트레이터에 배포하는 경우 전통적으로 `docker-compose.yml` 정의 파일을 기반으로 더 간단하고 사용하기 쉬운 `docker-compose` 도구 대신에 각 오케스트레이터마다 고유한 배포 스크립트 및 메커니즘을 사용할 것입니다(즉, Kubernetes와 Service Fabric의 배포 메커니즘이 서로 다름). 그러나 그림 5-10과 같은 Azure DevOps Services Docker 배포 작업 덕분에 `docker-compose.yml` 파일에서 오케스트레이터에 필요한 형식으로의 “변환”을 도구에서 수행해주므로 이제 친숙한 `docker-compose.yml` 파일만 사용하여 지원되는 오케스트레이터에 배포할 수도 있습니다.

![Kubernetes에 배포 작업을 보여주는 Azure DevOps의 작업 카탈로그 브라우저 보기](./media/add-deploy-to-kubernetes-task.png)

**그림 5-10**. 환경에 Kubernetes에 배포 작업 추가

그림 5-11은 구성에 사용할 수 있는 섹션을 사용하여 Kubernetes에 배포 작업을 편집할 수 있는 방법을 보여줍니다. 이는 클러스터에 컨테이너로 배포할 즉시 사용 가능한 사용자 지정 Docker 이미지를 검색하는 작업입니다.

![Azure DevOps의 브라우저 보기, Kubernetes에 배포 작업 정의](./media/edit-deploy-to-kubernetes-task.png)

**그림 5-11**. ACS DC/OS에 배포하는 Docker 배포 작업 정의

> [!정보] Azure DevOps Services 및 Docker를 포함하는 CD 파이프라인에 대해 자세히 알아보려면 <https://azure.microsoft.com/services/devops/pipelines>을 방문하세요.

## <a name="step-5-run-and-manage"></a>5단계: 실행 및 관리

엔터프라이즈 프로덕션 레벨에서 애플리케이션 실행 및 관리는 그 자체가 중요한 주제이고 해당 수준에서 작업하는 운영 유형과 개인(IT 운영 담당자)이 특별하고 이 영역의 범위가 크기 때문에 다음 장 전체에서 따로 설명합니다.

## <a name="step-6-monitor-and-diagnose"></a>6단계: 모니터링 및 진단

또한 이 주제는 다음 장에서 IT가 프로덕션 시스템에서 수행하는 작업의 일부로 다룹니다. 그러나 이 단계에서 얻는 인사이트는 애플리케이션의 지속적인 개선을 위해 개발 팀에게 피드백되어야 한다는 점을 강조해 둡니다. 해당 관점에서 볼 때 이는 DevOps의 일부이기도 하지만 작업과 운영은 일반적으로 IT에서 수행합니다.

모니터링 및 진단의 100%가 DevOps 범위 내에 속하는 유일한 경우는 개발 팀이 테스트 또는 베타 환경에 대해 수행하는 모니터링 프로세스와 분석뿐입니다. 이 작업은 부하 테스트를 수행하거나 베타 테스터가 새로운 버전을 체험해보는 베타 또는 QA 환경을 모니터링하는 방법으로 수행됩니다.

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](create-ci-cd-pipelines-azure-devops-services-aspnetcore-kubernetes.md)
