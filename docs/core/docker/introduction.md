---
title: Docker 소개
description: 이 문서에서는 .NET Core 애플리케이션 컨텍스트에서 Docker를 소개하고 간략하게 설명합니다.
ms.date: 03/20/2019
ms.custom: mvc, seodec18
ms.openlocfilehash: 5da71215e3b539f10993677d23d89e2b8a49cb39
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799358"
---
# <a name="introduction-to-net-and-docker"></a>.NET 및 Docker 소개

.NET Core는 Docker 컨테이너에서 쉽게 실행할 수 있습니다. 컨테이너는 호스트 시스템의 나머지 부분에서 애플리케이션을 격리한 채 커널만 공유하고 애플리케이션에 제공된 리소스를 사용하도록 지원하는 경량 방식을 제공합니다. Docker에 익숙하지 않은 경우에는 Docker의 [개요 문서](https://docs.docker.com/engine/docker-overview/)를 읽어 보는 것이 좋습니다.

Docker를 설치하는 방법에 대한 자세한 내용은 [Docker Desktop: Community Edition](https://www.docker.com/products/docker-desktop)의 다운로드 페이지를 참조하세요.

## <a name="docker-basics"></a>Docker 기본 사항

익숙해져야 하는 몇 가지 개념이 있습니다. Docker 클라이언트에는 이미지 및 컨테이너를 관리하는 데 사용하는 명령줄 인터페이스 프로그램이 있습니다. 앞에서 언급한 대로 시간을 내 [Docker 개요](https://docs.docker.com/engine/docker-overview/) 문서를 읽어 봐야 합니다. 

### <a name="images"></a>이미지

이미지는 컨테이너의 기본을 형성하는 파일 시스템 변경 사항의 정렬된 컬렉션입니다. 이미지는 읽기 전용이며 이미지에는 상태가 없습니다. 많은 경우, 이미지는 다른 이미지를 기반으로 하지만, 일부 사용자 지정이 사용됩니다. 예를 들어 애플리케이션을 위한 새 이미지를 생성하는 경우 이미 .NET Core 런타임이 포함된 기존 이미지를 기반으로 하게 됩니다.

컨테이너는 이미지에서 생성되므로, 이미지는 컨테이너가 시작될 때 실행되는 실행 매개 변수(예: 시작 실행 파일) 세트를 가집니다.

### <a name="containers"></a>컨테이너

컨테이너는 실행 가능한 이미지 인스턴스입니다. 이미지를 빌드할 때 애플리케이션 및 종속성을 배포하며 그런 다음, 여러 컨테이너를 각각 서로 격리된 상태로 인스턴스화할 수 있습니다. 각 컨테이너 인스턴스에는 고유한 파일 시스템, 메모리 및 네트워크 인터페이스가 있습니다.

### <a name="registries"></a>레지스트리

컨테이너 레지스트리는 이미지 리포지토리의 컬렉션입니다. 레지스트리 이미지를 기반으로 한 이미지를 만들 수 있습니다. 레지스트리의 이미지에서 곧바로 컨테이너를 생성할 수 있습니다. [Docker 컨테이너, 이미지 및 레지스트리 간의 관계](../../architecture/microservices/container-docker-introduction/docker-containers-images-registries.md)는 [컨테이너화된 애플리케이션이나 마이크로 서비스를 설계 및 빌드](../../architecture/microservices/architect-microservice-container-applications/index.md)할 때 중요한 개념입니다. 이 접근 방식은 개발과 배포 간의 시간을 크게 줄여 줍니다.

Docker에는 [Docker 허브](https://hub.docker.com/)에서 호스트하는, 사용 가능한 공용 레지스트리가 있습니다. [.NET Core 관련 이미지](https://hub.docker.com/_/microsoft-dotnet-core/)는 Docker 허브에 나열됩니다. 

MCR(Microsoft 컨테이너 레지스트리)은 Microsoft가 제공하는 컨테이너 이미지의 공식 소스입니다. MCR은 Azure CDN에서 빌드되어 글로벌 복제 이미지를 제공합니다. 그러나 MCR은 공용 웹 사이트가 없으며, Microsoft가 제공하는 컨테이너 이미지에 대해 배우는 기본적인 방법은 [Microsoft Docker 허브 페이지](https://hub.docker.com/_/microsoft-dotnet-core/)를 통하는 것입니다.

### <a name="dockerfile"></a>Dockerfile

**Dockerfile**은 이미지를 생성하는 명령 세트를 정의하는 파일입니다. **Dockerfile**의 각 명령은 이미지에 계층을 생성합니다. 대부분의 경우 이미지를 다시 빌드할 때는 변경된 계층만 다시 빌드됩니다. **Dockerfile**은 다른 사용자에게 배포할 수 있으며, 그러면 생성할 때와 동일한 방식으로 새 이미지를 다시 생성할 수 있습니다. 이 기능을 사용하여 이미지를 생성하는 방법에 대한 ‘명령’을 배포할 수 있지만, 이미지를 배포하는 기본 방법은 레지스트리에 이미지를 게시하는 것입니다. 

## <a name="net-core-images"></a>.NET Core 이미지

공식 .NET Core Docker 이미지는 MCR(Microsoft 컨테이너 레지스트리)에 게시되며 [Microsoft .NET Core Docker 허브 리포지토리](https://hub.docker.com/_/microsoft-dotnet-core/)에서 찾을 수 있습니다. 각 리포지토리에는 사용할 수 있는 .NET(SDK 또는 Runtime)과 OS가 다양하게 조합된 이미지가 포함되어 있습니다. 

Microsoft는 특정 시나리오를 위한 맞춤형 이미지를 제공합니다. 예를 들어 [ASP.NET Core 리포지토리](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/)는 프로덕션에서 ASP.NET Core 앱을 실행하기 위해 빌드된 이미지를 제공합니다.

## <a name="azure-services"></a>Azure 서비스

다양한 Azure 서비스에서 컨테이너를 지원합니다. 애플리케이션을 위한 Docker 이미지를 생성하여 다음 서비스 중 하나에 배포합니다.

* [AKS(Azure Kubernetes Service)](https://azure.microsoft.com/services/kubernetes-service/)\
Kubernetes를 사용하여 Linux 컨테이너를 확장 및 오케스트레이션합니다.

* [Azure App Service](https://azure.microsoft.com/services/app-service/containers/)\
PaaS 환경에서 Linux 컨테이너를 사용하여 웹앱 또는 API를 배포합니다.

* [Azure Container Instances](https://azure.microsoft.com/services/container-instances/)\
더 높은 수준의 관리 서비스 없이 클라우드에서 컨테이너를 호스트합니다.

* [Azure Batch](https://azure.microsoft.com/services/batch/)\
컨테이너를 사용하여 반복적인 컴퓨팅 작업을 실행합니다.

* [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)\
Windows Server 컨테이너를 사용하여 .NET 애플리케이션 및 마이크로 서비스를 이동하고 전환하고 현대화합니다.

* [Azure Container Registry](https://azure.microsoft.com/services/container-registry/)\
모든 형식의 Azure 배포에서 컨테이너 이미지 저장 및 관리합니다.

## <a name="next-steps"></a>다음 단계

* [.NET Core 애플리케이션을 컨테이너화하는 방법 알아보기](build-docker-netcore-container.md)
* [ASP.NET Core 애플리케이션을 컨테이너화하는 방법을 알아봅니다.](/aspnet/core/host-and-deploy/docker/building-net-docker-images)
* [ASP.NET Core 마이크로 서비스 알아보기 자습서 확인해 보기](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
* [Visual Studio의 컨테이너 도구에 대해 알아보기](/visualstudio/containers/overview)
