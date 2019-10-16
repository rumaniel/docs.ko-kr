---
title: Microsoft 도구를 사용하는 Docker 애플리케이션 DevOps 워크플로
description: Microsoft 플랫폼 및 도구가 포함된 컨테이너화된 Docker 애플리케이션 수명 주기 및 Microsoft 도구를 사용하는 DevOps 워크플로
ms.date: 02/15/2019
ms.openlocfilehash: 6b138301a7e6794ce0a7b15957684b3b73e9f89f
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295074"
---
# <a name="docker-application-devops-workflow-with-microsoft-tools"></a>Microsoft 도구를 사용하는 Docker 애플리케이션 DevOps 워크플로

*Microsoft Visual Studio, Azure DevOps Services, Team Foundation Server 및 Azure Monitor는 팀에게 프로젝트를 관리하고, 컨테이너화된 애플리케이션을 신속하게 빌드, 테스트 및 배포할 수 있는 도구를 제공하는 개발 및 IT 운영을 위한 포괄적인 에코시스템입니다.*

개발 팀은 온-프레미스의 Azure DevOps Server와 클라우드의 Visual Studio 및 Visual Studio Team Services를 함께 사용하여 Windows 또는 Linux를 대상으로 하는 컨테이너화된 애플리케이션을 생산적으로 빌드, 테스트 및 릴리스할 수 있습니다.

Microsoft 도구는 Azure DevOps Services 또는 Team Foundation Server를 사용한 글로벌 빌드 및 CI(연속 통합), 테스트부터 CD(연속 배포), Docker 환경(배포, 준비, 프로덕션), Azure Monitor를 통해 개발 팀에게 서비스에 대한 분석 정보 전송까지, Docker, .NET Core 또는 다른 플랫폼 조합 등 컨테이너화된 애플리케이션의 특정 구현에 대한 파이프라인을 자동화할 수 있습니다. 모든 코드 커밋은 빌드(CI)를 시작하고 특정 컨테이너화된 환경(CD)에 자동으로 서비스를 배포할 수 있습니다.

개발자와 테스터는 Microsoft Azure의 템플릿을 사용하여 프로덕션 환경과 유사한 Docker 기반의 개발 및 배포 환경을 쉽고 빠르게 프로비전할 수 있습니다.

컨테이너화된 애플리케이션 개발의 복잡성은 비즈니스 복잡성 및 확장성 요구 사항에 따라 꾸준히 증가합니다. 이러한 복잡성의 좋은 예는 마이크로서비스 아키텍처 기반 애플리케이션입니다. 이러한 환경에서 성공하려면 프로젝트가 빌드 및 배포뿐만 아니라 원격 분석 컬렉션과 버전 관리까지 전체 수명 주기를 자동화해야 합니다. Azure DevOps Services와 Azure는 다음과 같은 기능을 제공합니다.

- Azure DevOps Services/Team Foundation Server 소스 코드 관리(Git 또는 Team Foundation 버전 제어 기반), Agile 계획(Agile, 스크럼 및 CMMI가 지원됨), CI, 릴리스 관리 및 Agile 팀에 대한 기타 도구.

- Azure DevOps Services 및 Team Foundation Server에는 마이크로서비스에 대한 CI, 빌드, 테스트, 전송 및 관리 파이프라인을 손쉽게 생성할 수 있게 해주며 점점 확대되고 있는 강력한 자사 및 타사 확장 프로그램 에코시스템이 포함됩니다.

- Azure DevOps Services에서 빌드 파이프라인의 일부로 자동화된 테스트를 실행합니다.

- Azure DevOps Services는 프로덕션 환경뿐만 아니라 A/B 실험, [카나리아 릴리스](https://martinfowler.com/bliki/CanaryRelease.html) 등의 테스트에 사용되는 여러 환경에 대한 전송으로 DevOps 수명 주기를 강화할 수 있습니다.

- 조직에서는 이미 사용법을 잘 알고 있는 도구와 Azure Resource Manager 템플릿을 사용하여 Azure 구성 요소(데이터, PaaS 등)에 대한 종속성과 함께 Azure Container Registry에 저장된 프라이빗 이미지에서 Docker 컨테이너를 쉽게 프로비저닝할 수 있습니다.

>[!div class="step-by-step"]
>[이전](../design-develop-containerized-apps/build-aspnet-core-applications-linux-containers-aks-kubernetes.md)
>[다음](docker-application-outer-loop-devops-workflow.md)
