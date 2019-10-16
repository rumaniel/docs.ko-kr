---
title: 클라우드에 최적화된 응용 프로그램 내의 Microsoft 기술
description: 기존.NET 응용 프로그램을 Azure 클라우드와 Windows 컨테이너를 사용하여 최신화 | 클라우드에 최적화된 응용 프로그램 내의 Microsoft 기술
ms.date: 04/28/2018
ms.openlocfilehash: 915aa99d2331c5b9c46eabef3335fb809baa9370
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69578226"
---
# <a name="microsoft-technologies-in-cloud-optimized-applications"></a>클라우드에 최적화된 응용 프로그램 내의 Microsoft 기술

다음 목록은 클라우드에 최적화된 앱의 요구 사항으로 인식되는 도구와 기술, 솔루션을 설명합니다. 우선 순위에 따라 클라우드 최적화 요소를 단계적 또는 선택적으로 채택할 수 있습니다.

- **클라우드 인프라**: 계산 플랫폼과 운영 체제, 네트워크, 저장소를 제공하는 인프라입니다. Microsoft Azure는 이 수준에 위치합니다.

- **런타임**: 이 계층은 응용 프로그램을 실행 하기 위한 환경을 제공 합니다. 컨테이너를 사용 하는 경우이 계층은 일반적으로 Linux 호스트나 Windows 호스트에서 실행 되는 [Docker 엔진](https://docs.docker.com/engine/)을 기반으로 합니다. Windows[컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/about/) 는 windows Server 2016부터 지원 됩니다. Windows 컨테이너는 Windows에서 실행 되는 기존 .NET Framework 응용 프로그램에 가장 적합 한 선택입니다.)

- **관리 되는 클라우드**: 관리 되는 클라우드 옵션을 선택 하면 기본 인프라, Vm, OS 패치 및 네트워킹 구성을 관리 하 고 지 원하는 데 따른 비용과 복잡성을 피할 수 있습니다. IaaS를 사용 하 여 마이그레이션하도록 선택 하는 경우 이러한 모든 작업과 관련 비용을 담당 하 게 됩니다. 관리 되는 클라우드 옵션에서 개발 하는 응용 프로그램 및 서비스만 관리 합니다. 클라우드 서비스 공급자는 일반적으로 다른 모든 항목을 관리 합니다. Azure에서 관리 되는 클라우드 서비스의 예로는 [Azure SQL Database](https://azure.microsoft.com/services/sql-database), [Azure Redis Cache](https://azure.microsoft.com/services/cache/), [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), [Azure Storage](https://azure.microsoft.com/services/storage/), [Azure Database for MySQL](https://azure.microsoft.com/services/mysql/), [Azure Database for PostgreSQL](https://azure.microsoft.com/services/postgresql/), azure Active가 있습니다. [ 디렉터리](https://azure.microsoft.com/services/active-directory/)및 관리 되는 계산 서비스 (예: [VM scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Azure App Service](https://azure.microsoft.com/services/app-service/)및 [Azure Kubernetes Service](https://azure.microsoft.com/services/container-service/))

- **응용 프로그램 개발**: 컨테이너에서 실행 되는 응용 프로그램을 빌드할 때 많은 언어를 선택할 수 있습니다. 이 가이드는 [.net](https://www.microsoft.com/net)에 중점을 둔 반면, Node.js, Python, 스프링/Java 또는 Go와 같은 다른 언어를 사용 하 여 컨테이너 기반 앱을 개발할 수 있습니다.

- **모니터링, 원격 분석, 로깅 및 감사**: 클라우드에서 실행 되는 응용 프로그램 및 컨테이너를 모니터링 하 고 감사 하는 기능은 클라우드 최적화 응용 프로그램에 매우 중요 합니다. [Azure 애플리케이션 정보](https://azure.microsoft.com/services/application-insights/) 및 [Microsoft Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) 는 클라우드 최적화 앱에 대 한 모니터링 및 감사를 제공 하는 Microsoft의 주요 도구입니다.

- **프로 비전**: 자동화 도구를 통해 인프라를 프로 비전 하 고 응용 프로그램을 여러 환경 (프로덕션, 테스트, 스테이징)에 배포할 수 있습니다. Chef 및 퍼핏와 같은 도구를 사용 하 여 응용 프로그램의 구성 및 환경을 관리할 수 있습니다. 이 계층은 보다 간단 하 고 직접적인 방법을 사용 하 여 구현할 수도 있습니다. 예를 들어 Azure CLI (Azure 명령줄 인터페이스) 도구를 사용 하 여 직접 배포한 후 [Azure DevOps Services](https://azure.microsoft.com/services/devops/)에서 연속 배포 및 릴리스 관리 파이프라인을 사용할 수 있습니다.

- **응용 프로그램 수명 주기**: [Azure DevOps Services](https://azure.microsoft.com/services/devops/) 및 기타 도구 (예: Jenkins)는 릴리스 관리를 포함 하 여 CI/CD 파이프라인을 구현 하는 데 도움이 되는 빌드 자동화 서버입니다.

이 챕터의 다음 섹션과 관련 연습은 특히 런타임 계층 (Windows 컨테이너)에 대 한 세부 정보에 중점을 둡니다. 이 지침에서는 Windows Server 2016 이상 버전의 Vm 및 Azure Container Instances Windows 컨테이너를 배포 하는 방법에 대해 설명 합니다. 또한 Azure Kubernetes Service와 같은 Azure App Service 및 orchestrator와 같은 고급 PaaS 플랫폼을 설명 합니다.

## <a name="monolithic-applications-can-be-cloud-optimized"></a>모놀리식 응용 프로그램은 클라우드로 최적화할 *수 있습니다* .

모놀리식 응용 프로그램 (마이크로 서비스를 기반으로 하지 않는 응용 프로그램)은 클라우드 최적화 응용 프로그램 일 *수 있습니다* . 컨테이너, 지속적인 업데이트 및 DevOps의 조합을 사용 하 여 클라우드 컴퓨팅 모델을 활용 하는 모놀리식 응용 프로그램을 빌드하고 운영할 수 있습니다. 기존 모놀리식 응용 프로그램이 비즈니스 목표에 적합 한 경우이 응용 프로그램을 현대화 하 고 클라우드 최적화로 만들 수 있습니다.

마찬가지로, 모놀리식 응용 프로그램을 클라우드 최적화 응용 프로그램으로 사용할 수 있는 경우 N 계층 응용 프로그램과 같은 복잡 한 아키텍처는 클라우드 최적화 응용 프로그램으로 현대화 수도 있습니다.

>[!div class="step-by-step"]
>[이전](reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications.md)
>[다음](what-about-cloud-native-applications.md)
