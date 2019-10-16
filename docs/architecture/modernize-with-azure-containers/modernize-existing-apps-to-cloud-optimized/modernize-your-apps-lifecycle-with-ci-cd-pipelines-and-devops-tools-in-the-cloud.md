---
title: 클라우드에서 DevOps 도구와 CI/CD 파이프라인을 사용하여 앱의 수명 주기 최신화
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | 클라우드에서 DevOps 도구와 CI/CD 파이프라인를 사용하여 앱의 수명 주기 최신화
ms.date: 04/30/2018
ms.openlocfilehash: 75ac3fa06f442570a0a5043a88409b3fdebb5810
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72318560"
---
# <a name="modernize-your-apps-lifecycle-with-cicd-pipelines-and-devops-tools-in-the-cloud"></a>클라우드에서 DevOps 도구와 CI/CD 파이프라인을 사용하여 앱의 수명 주기 최신화

오늘날의 비즈니스는 시장에서 경쟁력을 갖기 위해 빠른 속도로 혁신해야 합니다. 높은 수준의 최신 응용 프로그램을 제공하려면 이러한 혁신을 주기적으로 구현하기 위해 중요한 DevOps 도구와 프로세스가 필요합니다. 적절한 DevOps 도구를 사용하여 개발자는 지속적인 배포를 간소화하고 사용자에게 혁신적인 응용 프로그램을 보다 신속하게 전달할 수 있습니다.

지속적인 통합과 배포 방법이 잘 정립되더라도 컨테이너를 도입하는 경우, 특히 다중 컨테이너 응용 프로그램을 사용하여 작업하는 경우에는 새로운 고려 사항이 발생하게 됩니다.

Azure DevOps Services는 공식 Azure DevOps Services 배포 작업을 통해 다양 한 환경에 대 한 다중 컨테이너 응용 프로그램의 지속적인 통합 및 배포를 지원 합니다.

- [Azure Web App for Containers에 배포](https://docs.microsoft.com/azure/devops/pipelines/apps/cd/deploy-docker-webapp?tabs=dotnet-core)

- [Azure Kubernetes Service에 배포](https://docs.microsoft.com/azure/devops/pipelines/apps/cd/deploy-aks?tabs=dotnet-core)

그러나 Azure DevOps Services 스크립트 기반 작업을 사용 하 여 [Docker Swarm](https://blogs.msdn.microsoft.com/jcorioland/2016/11/29/full-ci-cd-pipeline-to-deploy-multi-containers-application-on-azure-container-service-docker-swarm-using-visual-studio-team-services/) 또는 DC/OS에 배포할 수도 있습니다.

배포 민첩성을 계속 유지 하기 위해 이러한 도구는 개발 및 CI/CD 솔루션을 선택 하 여 컨테이너 워크 로드에 대 한 뛰어난 개발 및 테스트 프로덕션 환경 배포 환경을 제공 합니다.

그림 4-12은 Azure Container Service에서 Kubernetes 클러스터에 배포 하는 연속 배포 파이프라인을 보여 줍니다.

![Kubernetes 클러스터에 배포 하는 Azure DevOps Services의 스크린샷](./media/modernize-your-apps-lifecycle-with-ci-cd-pipelines-and-devops-tools-in-the-cloud/deploy-mvc-app-container-kubernetes.png)

**그림 4-12.** Azure DevOps Services 연속 배포 파이프라인, Kubernetes 클러스터에 배포

>[!div class="step-by-step"]
>[이전](modernize-your-apps-with-monitoring-and-telemetry.md)
>[다음](migrate-to-hybrid-cloud-scenarios.md)
