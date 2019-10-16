---
title: Docker 애플리케이션에 대한 외부 루프 DevOps 워크플로의 단계
description: Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 애플리케이션 수명 주기
ms.date: 02/15/2019
ms.openlocfilehash: 9fdc5acfd375e4f2266859f061ef1c854286b914
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68673780"
---
# <a name="creating-cicd-pipelines-in-azure-devops-services-for-a-net-core-20-application-on-containers-and-deploying-to-a-kubernetes-cluster"></a>Azure DevOps 서비스에서 컨테이너의 .NET Core 2.0 애플리케이션에 대한 CI/CD 파이프라인 만들기 및 Kubernetes 클러스터에 배포

그림 5-12에서는 코드 관리, 코드 컴파일, Docker 이미지 빌드, Docker 레지스트리로 Docker 이미지 푸시, 마지막으로 Azure의 Kubernetes 클러스터에 배포하는 과정을 다루는 엔드투엔드 DevOps 시나리오를 볼 수 있습니다.

![워크플로: 개발 머신에서 시작합니다. 리포지토리에 푸시하면 사용자 이미지를 사용하여 빌드/CI 작업이 시작됩니다. 이 이미지는 Docker 레지스트리로 푸시되어 CD/배포 작업에 사용되고, 마지막으로, AKS에 푸시됩니다.](media/docker-workflow-ci-cd-aks.png)

**그림 5-12**. Docker 이미지를 만들어서 Azure의 Kubernetes 클러스터에 배포하는 CI/CD 시나리오

두 파이프라인(빌드/CI 및 릴리스/CD)이 Docker 레지스트리(예: Docker Hub 또는 Azure Container Registry)를 통해 연결되는 것을 강조해야 합니다. Docker가 없는 기존 CI/CD 프로세스와 다른 주요 차이점 중 하나는 Docker 레지스트리입니다.

그림 5-13처럼 첫 번째 단계는 빌드/CI 파이프라인입니다. Azure DevOps Services에서 코드를 컴파일하고, Docker 이미지를 만들고, Docker Hub 또는 Azure Container Registry 같은 Docker 레지스트리로 푸시하는 빌드/CI 파이프라인을 만들 수 있습니다.

![Azure DevOps의 브라우저 보기, 빌드 프로세스 작업 정의](media/build-ci-pipeline-azure-devops-push-to-docker-registry.png)

**그림 5-13**. Docker 이미지를 빌드하여 Docker 레지스트리로 푸시하는 Azure DevOps의 빌드/CI 파이프라인

두 번째 단계는 배포/릴리스 파이프라인을 만드는 것입니다. Azure DevOps Services에서는 그림 5-14처럼 Azure DevOps Services에 대한 Kubernetes 작업을 사용하여 Kubernetes 클러스터를 대상으로 하는 배포 파이프라인을 쉽게 만들 수 있습니다.

![Azure DevOps의 브라우저 보기, Kubernetes에 배포 작업 정의](media/release-cd-pipeline-azure-devops-deploy-to-kubernetes.png)

**그림 5-14**. Kubernetes 클러스터에 배포하는 Azure DevOps Services의 릴리스/CD 파이프라인

> [!연습] Kubernetes에 eShopModernized 배포:
>
> Kubernetes에 배포하는 Azure DevOps CI/CD 파이프라인의 구체적인 연습은 다음 게시물을 참조하세요. \
><https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

>[!div class="step-by-step"]
>[이전](docker-application-outer-loop-devops-workflow.md)
>[다음](../run-manage-monitor-docker-environments/index.md)
