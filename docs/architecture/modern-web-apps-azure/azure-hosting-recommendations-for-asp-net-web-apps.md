---
title: ASP.NET Core 웹앱에 대한 Azure 호스팅 권장 사항
description: ASP.NET Core 및 Azure를 사용하여 최신 웹 애플리케이션 설계 | ASP.NET 웹앱에 대한 Azure 호스팅 권장 사항
author: ardalis
ms.author: wiwagn
ms.date: 06/06/2019
ms.openlocfilehash: ed8771a4d79b45d8fad0e5309c886c2e00402ec7
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71331995"
---
# <a name="azure-hosting-recommendations-for-aspnet-core-web-apps"></a>ASP.NET Core 웹앱에 대한 Azure 호스팅 권장 사항

> "모든 기간 업무 리더는 IT 부서를 거치지 않고 클라우드(SaaS라고도 함)에서 애플리케이션을 다운로드한 후 잡지를 구독하듯 사용료를 지불합니다. 그리고 서비스가 더 이상 필요하지 않으면 사용하지 않는 장비를 굳이 한 구석에 남겨둘 필요 없이 구독을 취소하기만 하면 됩니다.”  
> _\- Gartner 분석가 Daryl Plummer_

애플리케이션의 요구 사항 및 아키텍처가 무엇이든 Microsoft Azure는 이를 지원할 수 있습니다. 호스팅 요구 사항은 정적 웹 사이트 또는 수십 가지 서비스로 구성된 정교한 애플리케이션처럼 간단할 수 있습니다. ASP.NET Core 모놀리식 웹 애플리케이션 및 지원 서비스에 권장되는 잘 알려진 구성이 몇 가지 있습니다. 이 문서의 권장 사항은 모든 애플리케이션, 개별 프로세스 또는 데이터에 관계없이 호스팅할 리소스의 종류에 따라 그룹화되어 있습니다.

## <a name="web-applications"></a>웹 애플리케이션

웹 애플리케이션은 다음을 통해 호스팅할 수 있습니다.

- App Service Web Apps

- 컨테이너(몇 가지 옵션)

- VM(가상 머신)

이 중 App Service Web Apps는 간단한 컨테이너 기반 앱을 비롯한 대부분의 시나리오에 권장되는 방법입니다. 마이크로서비스 아키텍처의 경우 컨테이너 기반 접근 방식을 고려합니다. 애플리케이션을 실행하는 컴퓨터에 대한 더 세부적인 제어가 필요할 경우 Azure Virtual Machines를 고려합니다.

### <a name="app-service-web-apps"></a>App Service Web Apps

App Service Web Apps는 웹 애플리케이션 호스팅에 최적화된 완벽하게 관리되는 플랫폼을 제공합니다. 이는 비즈니스 논리에 집중할 수 있게 해주는 PaaS(Platform-as-a-service) 솔루션이며, Azure는 앱 실행 및 확장에 필요한 인프라를 관리합니다. App Service Web Apps의 몇 가지 주요 기능:

- DevOps 최적화(지속적인 통합 및 업데이트, 여러 환경, A/B 테스트, 스크립팅 지원)

- 세계적인 규모 및 고가용성

- SaaS 플랫폼 및 온-프레미스 데이터에 대한 연결

- 보안 및 규정 준수

- Visual Studio 통합

Azure App Service는 대부분의 웹앱에 가장 적합한 선택입니다. 배포 및 관리가 플랫폼에 통합되어 있고, 사이트가 높은 트래픽 부하를 처리하기 위해 빠르게 확장될 수 있으며, 기본 제공되는 부하 분산 및 트래픽 관리자가 고가용성을 제공합니다. 온라인 마이그레이션 도구를 사용하여 기존 사이트를 Azure App Service로 쉽게 이동하거나, 웹 애플리케이션 갤러리에서 오픈 소스 애플리케이션을 사용하거나, 원하는 프레임워크와 도구를 사용하여 새 사이트를 만들 수 있습니다. Webjob 기능을 사용하면 백그라운드 작업 처리를 App Service 웹앱에 쉽게 추가할 수 있습니다. 로컬 데이터베이스를 사용하여 온-프레미스에서 호스팅되는 기존 ASP.NET 애플리케이션이 있는 경우, Azure SQL Database가 있는 App Service Web App(또는 원하는 경우 온-프레미스 데이터베이스 서버에 대한 보안 액세스)으로 앱을 마이그레이션할 수 있는 명확한 경로가 있습니다.

![Azure App Service에 대한 온-프레미스 .NET 앱의 권장 마이그레이션 전략](./media/image1-6.png)

대부분의 경우 로컬로 호스팅된 ASP.NET 앱에서 App Service Web App으로 이동하는 과정은 간단합니다. 앱 자체의 수정은 거의 또는 전혀 필요하지 않으며, Azure App Service Web Apps에서 제공하는 다양한 기능을 신속하게 활용할 수 있습니다.

Azure App Service Web Apps는 클라우드에 최적화되지 않은 앱 외에도 많은 ASP.NET Core 앱과 같은 단순한 단일(비분산) 애플리케이션에 적합한 솔루션입니다. 이 방법에서 아키텍처는 기본적이며 이해하고 관리하기 쉽습니다.

![기본 Azure 아키텍처](./media/image1-5.png)

단일 리소스 그룹에 있는 적은 수의 리소스는 일반적으로 이러한 앱을 관리하기에 충분합니다. 일반적으로 여러 개별 프로세스로 구성된 앱이 아닌 단일 단위로 배포되는 앱은 이 [기본 아키텍처 접근 방법](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/basic-web-app)에 적절한 후보입니다. 구조적으로 단순하지만 이 방법을 사용하면 여전히 호스팅되는 앱이 수요 증가를 충족하기 위해 확장(노드당 더 많은 리소스)과 축소(더 많은 호스팅된 노드) 모두를 가능하게 합니다. 자동 크기 조정을 통해 노드 간에 수요 및 평균 로드에 따라 앱을 호스팅하는 노드 수를 자동으로 조정하도록 앱을 구성할 수 있습니다.

### <a name="app-service-web-apps-for-containers"></a>컨테이너용 App Service Web Apps

웹앱을 직접 호스팅하는 지원 외에도 [컨테이너용 App Service Web Apps](https://azure.microsoft.com/services/app-service/containers/)를 사용하여 Windows 및 Linux에서 컨테이너화된 애플리케이션을 실행할 수 있습니다. 이 서비스를 사용하면 비즈니스에 따라 확장할 수 있는 컨테이너화된 애플리케이션을 쉽게 배포하고 실행할 수 있습니다. 앱은 위에 나열된 App Service Web Apps의 모든 기능을 가지고 있습니다. 또한 Web Apps for Containers는 Docker Hub, Azure Container Registry 및 GitHub를 통해 간소화된 CI/CD를 지원합니다. Azure DevOps를 사용하여 변경 내용을 레지스티리에 게시하는 빌드 배포 파이프라인을 정의할 수 있습니다. 그런 다음, 이러한 변경 내용을 스테이징 환경에서 테스트하고 배포 슬롯을 통해 프로덕션에 자동으로 배포하여 가동 중지 시간 없이 업그레이드할 수 있습니다. 이전 버전으로 롤백하는 것은 마찬가지로 쉽게 수행할 수 있습니다.

Web Apps for Containers가 가장 적합한 몇 가지 시나리오가 있습니다. Windows 또는 Linux 컨테이너에 상관없이 컨테이너화할 수 있는 기존 앱이 있는 경우 이 도구 집합을 사용하여 쉽게 호스팅할 수 있습니다. 컨테이너를 단순히 게시한 다음, Web Apps for Containers를 구성하여 선택한 레지스트리에서 해당 이미지의 최신 버전을 가져옵니다. 이는 클래식 앱 호스팅 모델에서 클라우드에 최적화된 모델로 마이그레이션하는 "리프트 앤 시프트" 접근 방식입니다.

![컨테이너화된 온-프레미스 .NET 애플리케이션을 콘테이너용 Azure Web Apps로 마이그레이션](./media/image1-8.png)

이 방법은 개발 팀이 컨테이너 기반 개발 프로세스로 이동할 수 있는 경우에도 잘 작동합니다. 컨테이너를 사용하여 앱을 개발하는 "내부 루프"는 컨테이너를 사용하여 앱을 빌드하는 것을 포함합니다. 컨테이너 구성뿐만 아니라 코드에 대한 변경 내용은 소스 제어로 푸시되고, 자동화된 빌드는 새 컨테이너 이미지를 Docker Hub 또는 Azure Container Registry와 같은 레지스트리에 게시하는 역할을 합니다. 이러한 이미지는 다음 다이어그램과 같이 추가 개발과 프로덕션 배포를 위한 기반으로 사용됩니다.

![엔드투엔드 Docker DevOps 수명 주기 워크플로](./media/image1-7.png)

컨테이너로 개발하면, 특히 컨테이너를 프로덕션에 사용할 때 많은 이점을 누릴 수 있습니다. 로컬 개발 머신에서 빌드 및 테스트 시스템, 프로덕션에 이르기까지 실행되는 각 환경에서 앱을 호스팅하는 데 동일한 컨테이너 구성이 사용됩니다. 이는 머신 구성이나 소프트웨어 버전 차이로 인한 결함 가능성을 크게 줄입니다. 컨테이너는 어떠한 OS에서도 실행될 수 있기 때문에 개발자는 운영 체제를 비롯하여 가장 생산적인 도구를 사용할 수 있습니다. 경우에 따라 많은 컨테이너를 포함하는 분산 애플리케이션은 단일 개발 머신에서 실행하는 데 많은 리소스가 필요할 수 있습니다. 이 시나리오에서는 Kubernetes 및 다음 섹션에서 다루는 Azure Dev Spaces를 사용하여 업그레이드하는 것이 좋습니다.

대규모 애플리케이션의 일부가 자체의 작은 독립적인 *마이크로서비스*로 분할되므로, 앱 동작을 개선하기 위해 추가 디자인 패턴을 사용할 수 있습니다. 개별 서비스로 직접 작업하는 대신 *API 게이트웨이*를 사용하면 액세스를 간소화하고 클라이언트를 백 엔드에서 분리할 수 있습니다. 서로 다른 프런트 엔드에 대해 별도의 서비스 백 엔드를 사용하면 서비스를 해당 소비자와 함께 발전할 수도 있습니다. 공통 서비스는 별도의 *사이드카* 컨테이너를 통해 액세스할 수 있습니다. 여기에는 *ambassador* 패턴을 사용하는 일반적인 클라이언트 연결 라이브러리가 포함될 수 있습니다.

![마이크로서비스는 몇 가지 일반 디자인 패턴이 명시된 아키텍처를 샘플링합니다.](./media/image1-10.png)

[마이크로서비스 기반 시스템을 빌드할 때 고려해야 할 디자인 패턴에 대해 자세히 알아봅니다.](https://docs.microsoft.com/azure/architecture/microservices/design/patterns)

### <a name="azure-kubernetes-service"></a>Azure Kubernetes Service

AKS(Azure Kubernetes Service)는 컨테이너 오케스트레이션 전문 지식 없이도 컨테이너화된 애플리케이션을 빠르고 쉽게 배포 및 관리할 수 있도록 해주는 호스트된 Kubernetes 환경을 관리합니다. 또한 애플리케이션을 오프라인으로 전환하지 않고 요청 시 리소스를 프로비전, 업그레이드 및 크기 조정하여 진행 중인 작업 및 유지 관리 부담을 덜어줍니다.

AKS는 대부분의 책임을 Azure로 오프로드함으로써 Kubernetes 클러스터 관리에 대한 복잡성 및 운영 오버헤드를 줄입니다. 호스트된 Kubernetes 서비스처럼, Azure는 상태 모니터링 및 유지 관리와 같은 중요 작업을 처리합니다. 또한 사용자는 마스터가 아닌 사용자 클러스터 내 에이전트 노드에 대해서만 비용을 지불합니다. 관리되는 Kubernetes 서비스로서 AKS는 다음을 제공합니다.

- 자동화된 Kubernetes 버전 업그레이드 및 패치.
- 간편한 클러스터 크기 조정.
- 자체 복구 호스팅된 컨트롤 평면(마스터).
- 비용 절감 - 실행 중인 에이전트 풀 노드에 대해서만 지불.

이제 AKS 클러스터의 노드 관리를 처리하는 Azure를 사용하면 클러스터 업그레이드와 같은 여러 작업을 수동으로 수행하지 않아도 됩니다. Azure가 사용자를 위해 이와 같은 중요한 유지 관리 작업을 처리하므로 AKS는 클러스터에 대한 직접 액세스를 제공하지 않습니다(예: SSH 사용).

AKS를 활용하는 팀은 Azure Dev Spaces를 이용할 수도 있습니다. Azure Dev Spaces는 AKS에서 실행 중인 전체 마이크로서비스 아키텍처 또는 애플리케이션으로 직접 작업할 수 있도록 함으로써 팀이 마이크로서비스 애플리케이션의 개발과 빠른 반복에 집중할 수 있도록 도와줍니다. Azure Dev Spaces는 또한 AKS 클러스터나 다른 개발자에게 영향을 주지 않으면서 마이크로서비스 아키텍처의 일부를 독립적으로 업데이트할 수 있는 방법을 제공합니다.

![Azure Dev Spaces 워크플로 예제](./media/image1-9.gif)

Azure Dev Spaces:

- 로컬 머신 설치 시간 및 리소스 요구 사항 최소화
- 팀이 더 신속하게 반복하도록 허용
- 팀에 필요한 통합 환경 수 줄이기
- 개발/테스트 시 분산 시스템에서 특정 서비스를 모의해야 하는 필요성 제거

[Azure Dev Spaces에 대해 자세히 알아보기](https://docs.microsoft.com/azure/dev-spaces/about)

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

App Service에서 실행하려면 상당한 수정이 필요한 기존 애플리케이션의 경우, 클라우드로의 마이그레이션을 간소화하기 위해 Virtual Machines를 선택할 수 있습니다. 그러나 VM을 올바르게 구성, 보호 및 유지 관리하려면 Azure App Service보다 훨씬 더 많은 시간과 IT 전문 지식이 필요합니다. Azure Virtual Machines를 고려 중이라면 VM 환경을 패치, 업데이트 및 관리하는 데 지속적인 유지 관리 노력이 필요함을 염두에 두어야 합니다. Azure Virtual Machines는 IaaS(서비스 형태의 인프라)이며, App Service는 PaaS(Platform-as-a-Service)입니다. 또한 앱을 Windows 컨테이너로 Web App for Containers에 배포하는 것이 시나리오에 유용한 옵션인지도 고려해야 합니다.

## <a name="logical-processes"></a>논리적 프로세스

애플리케이션의 나머지 부분과 분리될 수 있는 개별 논리 프로세스는 "서버가 없는" 방식으로 Azure Functions에 별도로 배포할 수 있습니다. Azure Functions를 사용하면 코드를 실행할 애플리케이션 또는 인프라에 대한 걱정 없이 주어진 문제에 필요한 코드를 작성할 수 있습니다. C\#, F\#, Node.js, Python 및 PHP를 포함하는 다양한 프로그래밍 언어 중에서 작업에 가장 생산적인 언어를 선택할 수 있습니다. 대부분의 클라우드 기반 솔루션과 마찬가지로 사용 시간만큼 요금을 지불하고 Azure Functions를 필요에 따라 확장할 수 있습니다.

## <a name="data"></a>데이터

Azure는 다양한 데이터 스토리지 옵션을 제공하므로, 애플리케이션이 해당 데이터에 대해 적절한 데이터 공급자를 사용할 수 있습니다.

트랜잭션, 관계형 데이터의 경우 Azure SQL Database가 가장 적합한 옵션입니다. 대부분 읽기 전용인 고성능 데이터의 경우 Azure SQL Database에서 지원하는 Redis 캐시가 적합한 솔루션입니다.

구조화되지 않은 JSON 데이터는 SQL Database 열에서 Azure Storage의 Blob 또는 테이블, DocumentDB에 이르기까지 다양한 방법으로 저장할 수 있습니다. 이 중에서 DocumentDB는 최상의 쿼리 기능을 제공하며, 쿼리를 지원해야 하는 다수의 JSON 기반 문서에 권장되는 옵션입니다.

애플리케이션 동작을 오케스트레이션하는 데 사용되는 일시적인 명령 또는 이벤트 기반 데이터는 Azure Service Bus 또는 Azure Storage Queue를 사용할 수 있습니다. Azure Storage Bus는 더 많은 유연성을 제공하며 애플리케이션 내 및 애플리케이션 간의 중요한 메시징에 권장되는 서비스입니다.

## <a name="architecture-recommendations"></a>아키텍처 권장 사항

애플리케이션의 요구 사항에 따라 아키텍처가 결정됩니다. 여러 다양한 Azure 서비스를 사용할 수 있습니다. 적합한 서비스를 선택하는 것은 중요한 의사 결정입니다. Microsoft는 일반적인 시나리오에 최적화된 일반적인 아키텍처를 식별하는 데 도움이 되는 참조 아키텍처의 갤러리를 제공합니다. 애플리케이션의 요구 사항과 밀접한 관련이 있거나 적어도 시작점을 제공하는 참조 아키텍처를 찾을 수 있습니다.

그림 11-1은 참조 아키텍처의 예를 보여 줍니다. 이 다이어그램에서는 마케팅에 최적화된 Sitecore 콘텐츠 관리 시스템 웹 사이트에 권장되는 아키텍처 접근 방식을 설명합니다.

![그림 11-1](./media/image11-2.png)

**그림 11-1.** Sitecore 마케팅 웹 사이트 참조 아키텍처

**참조 - Azure 호스팅 권장 사항**

- Azure 솔루션 아키텍처\
  <https://azure.microsoft.com/solutions/architecture/>

- Azure Basic Web Application 아키텍처\
  <https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/basic-web-app>

- 마이크로서비스용 디자인 패턴\
  <https://docs.microsoft.com/azure/architecture/microservices/design/patterns>

- Azure 개발자 가이드\
  <https://azure.microsoft.com/campaigns/developer-guide/>

- 웹앱 개요\
  <https://docs.microsoft.com/azure/app-service/app-service-web-overview>

- Web App for Containers\
  <https://azure.microsoft.com/services/app-service/containers/>

- AKS(Azure Kubernetes Service) 소개\
  <https://docs.microsoft.com/azure/aks/intro-kubernetes>

>[!div class="step-by-step"]
>[이전](development-process-for-azure.md)
