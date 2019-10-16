---
title: Docker 앱에 대한 개발 워크플로
description: Docker 기반 애플리케이션 개발 워크플로의 세부 정보를 확인하세요. 먼저 단계별로 살펴보고 Dockerfile 최적화에 대한 세부 정보를 알아본 후 Visual Studio 사용 시 사용 가능한 간소화된 워크플로를 마지막으로 확인하세요.
ms.date: 01/07/2019
ms.openlocfilehash: f7c7252edc82400e2af4b96a75ed040e11df392f
ms.sourcegitcommit: 10db6551ea3c971470cf5d2cc21ba1cbcefe5c55
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72031874"
---
# <a name="development-workflow-for-docker-apps"></a>Docker 앱에 대한 개발 워크플로

애플리케이션 개발 수명 주기는 개발자의 컴퓨터에서 시작되며, 여기서 개발자는 선호하는 언어를 사용하여 로컬로 애플리케이션 코드를 작성하고 테스트합니다. 개발자가 어떤 언어, 프레임워크, 플랫폼을 선택하든 이 워크플로를 사용하면 개발자는 항상 Docker 컨테이너를 로컬에서 개발하고 테스트하게 됩니다.

각 컨테이너(Docker 이미지의 인스턴스)는 다음 구성 요소를 포함합니다.

- 운영 체제 선택(예: Linux 배포판, Windows Nano Server 또는 Windows Server Core).

- 개발 중에 추가된 파일(예: 소스 코드 및 애플리케이션 바이너리).

- 구성 정보(예: 환경 설정 및 종속성).

## <a name="workflow-for-developing-docker-container-based-applications"></a>Docker 컨테이너 기반 애플리케이션을 개발하기 위한 워크플로

이 섹션에서는 Docker 컨테이너 기반 애플리케이션에 대한 *내부 루프* 개발 워크플로를 설명합니다. 내부 루프 워크플로란 프로덕션 배포까지 포함되는 광범위한 DevOps 워크플로를 고려하지 않고 개발자의 컴퓨터에서 수행되는 개발 작업에만 집중한다는 의미입니다. 환경을 설정하는 초기 단계는 한 번만 수행되므로 포함되지 않습니다.

애플리케이션은 개발자 고유의 서비스와 추가 라이브러리(종속성)로 구성됩니다. 다음은 그림 5-1처럼 일반적으로 Docker 애플리케이션을 빌드할 때 수행하는 기본 단계입니다.

![Docker 앱 개발 프로세스: 1 - 앱 코딩, 2 - Dockerfile 작성, 3 - Dockerfile에 정의된 이미지 만들기, 4 - (선택 사항) docker-compose.yml 파일에 서비스 작성, 5 - container 또는 docker-compose 앱 실행, 6 - 앱 또는 마이크로 서비스 테스트, 7 - 리포지토리에 푸시하고 반복. ](./media/image1.png)

**그림 5-1.** Docker 컨테이너화된 앱 개발을 위한 단계별 워크플로

이 섹션에서는 전체 프로세스를 자세히 설명하고 모든 주요 단계는 Visual Studio 환경을 중심으로 설명합니다.

편집기/CLI 개발 접근 방식을 사용하는 경우(예: macOS 또는 Windows에서 Visual Studio Code와 Docker CLI 사용) 일반적으로 Visual Studio를 사용할 때보다 모든 단계를 더 자세히 알아야 합니다. CLI 환경에서 작업하는 방법에 대한 자세한 내용은 eBook [컨테이너화된 Docker 애플리케이션 수명 주기와 Microsoft 플랫폼 및 도구](https://aka.ms/dockerlifecycleebook/)를 참조하세요.

Visual Studio 2017을 사용하는 경우 이러한 단계의 상당 부분이 자동으로 처리되므로 생산성이 대폭 향상됩니다. Visual Studio 2017을 사용하고 다중 컨테이너 애플리케이션을 대상으로 하는 경우에 특히 그렇습니다. 예를 들어 마우스 클릭 한 번이면 Visual Studio가 애플리케이션의 구성을 사용하여 Dockerfile 및 docker-compose.yml 파일을 프로젝트에 추가합니다. Visual Studio에서 애플리케이션을 실행하면 Visual Studio가 Docker 이미지를 작성하고 Docker에서 바로 다중 컨테이너 애플리케이션을 실행하며, 심지어 여러 컨테이너를 한꺼번에 디버깅할 수도 있습니다. 이러한 기능은 개발 속도를 향상합니다.

그러나 Visual Studio가 이러한 단계를 자동으로 처리한다고 해서 Docker 내부에서 발생하는 일에 대해 전혀 몰라도 된다는 뜻은 아닙니다. 따라서 다음 지침에서는 각 단계를 자세히 설명합니다.

![1 - 앱 코딩](./media/image2.png)

## <a name="step-1-start-coding-and-create-your-initial-application-or-service-baseline"></a>1단계: 코딩을 시작하고 초기 애플리케이션 또는 서비스 기준 만들기

Docker 애플리케이션 개발은 Docker 없이 애플리케이션을 개발하는 방법과 비슷합니다. 다른 점은 Docker를 개발하는 동안 로컬 환경의 Docker 컨테이너 내에서 실행되는 애플리케이션을 배포하고 테스트한다는 점입니다(Docker를 사용하는 Linux VM 환경 또는 Windows 컨테이너를 사용하는 Windows 환경).

### <a name="set-up-your-local-environment-with-visual-studio"></a>Visual Studio를 사용하여 로컬 환경 설정

시작하려면 다음 지침에 설명된 대로 Windows용 [Docker CE(Community Edition)](https://docs.docker.com/docker-for-windows/)를 설치합니다.

[Windows용 Docker CE 시작](https://docs.docker.com/docker-for-windows/)

또한 그림 5-2에서 표시된 대로 **.NET Core 플랫폼 간 개발** 워크로드가 설치된 Visual Studio 2017 버전 15.7 이상이 필요합니다.

![Visual Studio 설치 중 .NET Core 플랫폼 간 개발 워크로드 선택.](./media/image3.png)

**그림 5-2**. Visual Studio 2017 설정 중 **.NET Core 플랫폼 간 개발** 워크로드 선택

심지어 애플리케이션에서 Docker를 사용하도록 설정하고 Docker에 배포 및 테스트하기 전에도 일반 .NET에서 애플리케이션 코딩을 시작할 수 있습니다(컨테이너를 사용하려는 경우 일반적으로 .NET Core). 하지만 되도록이면 빨리 Docker에서 작업을 시작하는 것이 좋습니다. 실제로 사용하게 될 환경이고 문제를 최대한 신속하게 검색할 수 있기 때문입니다. 이렇게 하도록 권장하는 이유는 Visual Studio를 사용하면 거의 투명한 것처럼 느껴지는 Docker를 손쉽게 작업할 수 있기 때문입니다. 가장 대표적인 예로 Visual Studio에서 다중 컨테이너 애플리케이션을 디버깅하는 경우를 들 수 있습니다.

### <a name="additional-resources"></a>추가 자료

- **Windows용 Docker CE 시작** \
  <https://docs.docker.com/docker-for-windows/>

- **Visual Studio 2017** \
  [https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017)

![2 - Dockerfile 작성](./media/image4.png)

## <a name="step-2-create-a-dockerfile-related-to-an-existing-net-base-image"></a>2단계. 기존 .NET 기본 이미지와 관련된 Dockerfile 만들기

Visual Studio에서 자동으로 배포하든 아니면 Docker CLI(docker run 및 docker-compose 명령)를 사용하여 수동으로 배포하든, 빌드하려는 각 사용자 지정 이미지에 대한 Dockerfile과 배포할 각 컨테이너에 대한 Dockerfile이 필요합니다. 애플리케이션이 단일 사용자 지정 서비스를 포함하는 경우 단일 Dockerfile이 필요합니다. 애플리케이션이 여러 서비스를 포함하는 경우(마이크로 서비스 아키텍처처럼) 서비스마다 하나의 Dockerfile이 필요합니다.

Dockerfile은 애플리케이션 또는 서비스의 루트 폴더에 배치됩니다. 컨테이너의 애플리케이션 또는 서비스를 설정하고 실행하는 방법을 Docker에 알려주는 명령을 포함하고 있습니다. 코드를 사용하여 수동으로 Dockerfile을 만들어서 .NET 종속성과 함께 프로젝트에 추가할 수 있습니다.

Visual Studio와 Docker용 도구를 사용하면 마우스 클릭 몇 번으로 이 작업을 처리할 수 있습니다. Visual Studio 2017에서 새 프로젝트를 만들 때 그림 5-3처럼 **컨테이너(Docker) 지원 사용**이라는 옵션이 있습니다.

![Visual Studio 2017에서 새 ASP.NET Core 프로젝트를 만들 때 Docker 지원 활성화 확인란](./media/image5.png)

**그림 5-3**. Visual Studio 2017에서 새 ASP.NET Core 프로젝트를 만들 때 Docker 지원 활성화

그림 5-4에 표시된 대로 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, **추가** > **Docker 지원** 을 선택하여 기존 ASP.NET Core 웹앱 프로젝트에서 Docker 지원을 사용할 수도 있습니다.

![Visual Studio에서 Docker 지원 메뉴 옵션 추가](./media/image6.png)

**그림 5-4**. 기존 Visual Studio 2017 프로젝트에서 Docker 지원을 사용하도록 설정

이 작업은 필수 구성을 포함한 프로젝트에 *Dockerfile*을 추가하고 ASP.NET Core 프로젝트에서만 사용할 수 있습니다.

마찬가지로 Visual Studio는 **추가 > 컨테이너 오케스트레이터 지원** 옵션을 사용하여 전체 솔루션용 docker-compose.yml 파일을 추가할 수도 있습니다. 4단계에서 이 옵션을 더 자세히 살펴보겠습니다.

### <a name="using-an-existing-official-net-docker-image"></a>기존의 공식 .NET Docker 이미지 사용

일반적으로 [Docker Hub](https://hub.docker.com/) 레지스트리 같은 공식 리포지토리에서 얻을 수 있는 기본 이미지를 기반으로 컨테이너에 대한 사용자 지정 이미지를 빌드합니다. Visual Studio에서 Docker 지원을 사용하도록 설정하면 내부에서 이와 같은 일이 발생합니다. Dockerfile은 기존 `aspnetcore` 이미지를 사용합니다.

앞에서 선택하는 프레임워크 및 운영 체제에 따라 어떤 Docker 이미지와 리포지토리를 사용할 수 있는지 설명했습니다. 예를 들어 ASP.NET Core(Linux 또는 Windows)를 사용하려는 경우 사용할 이미지는 `mcr.microsoft.com/dotnet/core/aspnet:2.2`입니다. 따라서 컨테이너에 사용할 기본 Docker 이미지만 지정하면 됩니다. 이렇게 하려면 `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`을 Dockerfile에 추가하세요. 이 작업은 Visual Studio가 자동으로 수행하지만, 버전을 업데이트하려면 직접 이 값을 업데이트합니다.

버전 번호가 있는 Docker Hub의 공식 .NET 이미지 리포지토리를 사용하면 모든 컴퓨터에서(개발, 테스트 및 프로덕션 포함) 동일한 언어 기능을 사용할 수 있습니다.

다음 예제에서는 ASP.NET Core 컨테이너에 대한 샘플 Dockerfile을 보여줍니다.

```Dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
ARG source
WORKDIR /app
EXPOSE 80
COPY ${source:-obj/Docker/publish} .
ENTRYPOINT ["dotnet", " MySingleContainerWebApp.dll "]
```

이 예에서 이미지는 공식 ASP.NET Core Docker 버전 2.2 이미지(Linux 및 Windows용 다중 아키텍처)를 기반으로 합니다. 이것은 설정 `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`입니다. (이 기본 이미지에 대한 자세한 내용은 [.NET Core Docker 이미지](https://hub.docker.com/_/microsoft-dotnet-core/) 페이지를 참조하세요.) 또한 Dockerfile에서, 런타임에 사용할 TCP 포트(이 예에서는 EXPOSE 설정을 사용하여 구성한 대로 포트 80)에서 수신 대기하라고 Docker에 지시해야 합니다.

사용하는 언어 및 프레임워크에 따라 Dockerfile에서 추가 구성 설정을 지정할 수 있습니다. 예를 들어 `["dotnet", "MySingleContainerWebApp.dll"]`이 포함된 ENTRYPOINT 줄은 Docker에 .NET Core 애플리케이션을 실행하라고 알려줍니다. SDK 및 .NET Core CLI(dotnet CLI)를 사용하여 .NET 애플리케이션을 빌드하고 실행하는 경우 이 설정이 달라집니다. 결론적으로 ENTRYPOINT 줄 및 기타 설정은 개발자가 애플리케이션에 대해 선택하는 언어 및 플랫폼에 따라 달라집니다.

### <a name="additional-resources"></a>추가 자료

- **.NET Core 애플리케이션에 대한 Docker 이미지 작성** \
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](../../../core/docker/building-net-docker-images.md)

- **고유의 이미지 빌드**. 공식 Docker 설명서에 있습니다.\
  <https://docs.docker.com/engine/tutorials/dockerimages/>

- **Staying up-to-date with .NET Container Images(.NET 컨테이너 이미지를 최신 상태로 유지)**  \
  <https://devblogs.microsoft.com/dotnet/staying-up-to-date-with-net-container-images/>

- **Using .NET and Docker Together(.NET 및 Docker 함께 사용) - DockerCon 2018 업데이트** \
  <https://devblogs.microsoft.com/dotnet/using-net-and-docker-together-dockercon-2018-update/>

### <a name="using-multi-arch-image-repositories"></a>다중 아키텍처 이미지 리포지토리 사용

단일 리포지토리는 Linux 이미지 및 Windows 이미지 같은 플랫폼 변형을 포함할 수 있습니다. 이 기능을 통해 Microsoft 같은 공급업체(기본 이미지 작성자)는 여러 플랫폼(즉, Linux 및 Windows)을 처리하는 단일 리포지토리를 만들 수 있습니다. 예를 들어 Docker Hub 레지스트리에서 제공되는 [dotnet/core](https://hub.docker.com/_/microsoft-dotnet-core/) 리포지토리는 동일한 리포지토리 이름을 사용하여 Linux 및 Windows Nano Server에 대한 지원을 제공합니다.

태그를 지정하는 경우 다음과 같이 명시적인 플랫폼을 대상으로 지정합니다.

- `microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim` \
  대상: Linux의 .NET Core 2.2 런타임 전용

- `microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-1809` \
  대상: Windows Nano Server의 .NET Core 2.2 런타임 전용

그러나 동일한 이미지 이름을 지정하고 동일한 태그를 지정하는 경우 다중 아키텍처 이미지(예: `aspnetcore` 이미지)는 다음 예제와 같이 사용자가 배포하는 Docker 호스트 OS에 따라 Linux 또는 Windows 버전을 사용합니다.

- `microsoft/dotnet:2.2-aspnetcore-runtime` \
  다중 아키텍처: Docker 호스트OS에 따라 Linux 또는 Windows Nano Server의 .NET Core 2.2 런타임 전용

이와 같이, Windows 호스트에서 이미지를 끌어오면 Windows 변형을 끌어오고, Linux 호스트에서 동일한 이미지 이름을 끌어오면 Linux 변형을 끌어옵니다.

### <a name="multi-stage-builds-in-dockerfile"></a>Dockerfile의 다단계 빌드

Dockerfile은 배치 스크립트와 비슷합니다. 명령줄에서 머신을 설정해야 하는 경우에 수행하는 작업과 유사합니다.

초기 컨텍스트를 설정하는 기본 이미지로 시작되고, 호스트 OS를 기반으로 하는 시작 파일 시스템과 같습니다. OS는 아니지만 컨테이너 내 “OS”처럼 생각할 수 있습니다.

각 명령줄을 실행하면 파일 시스템에 이전 레이어에서 변경된 새 레이어가 생성되므로 이를 결합하면 결과 파일 시스템이 생성됩니다.

모든 새 레이어가 이전 레이어를 "기반"으로 생성되는 것은 아니며 각 명령이 실행될 때마다 결과 이미지 크기가 증가하므로 애플리케이션을 빌드하고 게시하는 데 필요한 SDK 등을 포함해야 할 경우 이미지가 매우 커질 수 있습니다.

그래서 다단계 빌드가 들어가면(Docker 17.05 이상) 엄청난 효과를 발휘하는 것입니다.

핵심 개념은 단계에서 Dockerfile 실행 프로세스를 구분할 수 있다는 것입니다. 단계는 하나 이상의 명령이 실행되기 전 초기 이미지이며, 마지막 단계에서 최종 이미지 크기가 결정됩니다.

즉, 다단계 빌드는 생성 과정을 여러 "단계"로 분할한 후 최종 이미지를 어셈블하여 중간 단계에서 관련 디렉터리만 취할 수 있게 해줍니다. 이 기능을 사용할 때의 일반적인 전략은 다음과 같습니다.

1. 애플리케이션을 빌드하고 폴더에 게시하는 데 필요한 모든 것이 들어 있는 기본 SDK 이미지(크기는 중요하지 않음)를 사용합니다.

2. 작은 런타임 전용의 기본 이미지를 사용하고 이전 단계의 게시 폴더를 복사하여 작은 최종 이미지를 생성합니다.

다단계 과정을 이해하는 가장 좋은 방법은 Dockerfile을 한 줄씩 자세히 살펴보는 것이므로 프로젝트에 Docker 지원을 추가할 때 Visual Studio에서 만든 초기 Dockerfile부터 살펴보고 나중에 몇 가지 최적화를 알아보도록 하겠습니다.

초기 Dockerfile의 모습은 다음과 같을 수 있습니다.

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
 6  WORKDIR /src
 7  COPY src/Services/Catalog/Catalog.API/Catalog.API.csproj …
 8  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.AspNetCore.HealthChecks …
 9  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions.HealthChecks …
10  COPY src/BuildingBlocks/EventBus/IntegrationEventLogEF/ …
11  COPY src/BuildingBlocks/EventBus/EventBus/EventBus.csproj …
12  COPY src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.csproj …
13  COPY src/BuildingBlocks/EventBus/EventBusServiceBus/EventBusServiceBus.csproj …
14  COPY src/BuildingBlocks/WebHostCustomization/WebHost.Customization …
15  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
16  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
17  RUN dotnet restore src/Services/Catalog/Catalog.API/Catalog.API.csproj
18  COPY . .
19  WORKDIR /src/src/Services/Catalog/Catalog.API
20  RUN dotnet build Catalog.API.csproj -c Release -o /app
21
22  FROM build AS publish
23  RUN dotnet publish Catalog.API.csproj -c Release -o /app
24
25  FROM base AS final
26  WORKDIR /app
27  COPY --from=publish /app .
28  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

이를 한 줄씩 자세히 설명하면 다음과 같습니다.

- **줄 #1:** "작은" 런타임 전용 기본 이미지로 단계를 시작하고 참조를 위해 이를 **base**라고 명명합니다.

- **줄 #2:** 이미지에 **/app** 디렉터리를 만듭니다.

- **줄 #3:** 포트 **80**을 공개합니다.

- **줄 #5:** 빌드/게시를 위해 "큰" 이미지를 사용하여 새 단계를 시작합니다. 참조를 위해 이를 **build**라고 명명합니다.

- **줄 #6:** 이미지에 **/src** 디렉터리를 만듭니다.

- **줄 #7:** 패키지를 나중에 복원할 수 있도록 16번째 줄까지 참조된 **.csproj** 프로젝트 파일을 복사합니다.

- **줄 #17:** **Catalog.API** 프로젝트 및 참조된 프로젝트의 패키지를 복원합니다.

- **줄 #18:** **솔루션의 모든 디렉터리 트리**( **.dockerignore** 파일에 포함된 파일/디렉터리는 예외)를 이미지의 **/src** 디렉터리로 복사합니다.

- **줄 #19:** 현재 폴더를 **Catalog.API** 프로젝트로 변경합니다.

- **줄 #20:** 프로젝트(및 기타 프로젝트 종속성)를 빌드하고 이미지의 **/app** 디렉터리에 출력합니다.

- **줄 #22:** build에서 이어지는 새 단계를 시작합니다. 참조를 위해 이를 **publish**라고 명명합니다.

- **줄 #23:** 프로젝트(및 종속성)를 게시하고 이미지의 **/app** 디렉터리에 출력합니다.

- **줄 #25:** **base**에서 이어지는 새 단계를 시작하고 이를 **final**이라고 명명합니다.

- **줄 #26:** 현재 디렉터리를 **/app**으로 변경합니다.

- **줄 #27:** **publish** 단계에서 현재 디렉터리로 **/app** 디렉터리를 복사합니다.

- **줄 #28:** 컨테이너가 시작될 때 실행할 명령을 정의합니다.

이제 전체 프로세스 성능을 높이는 몇 가지 최적화를 살펴보겠습니다. eShopOnContainers의 경우 Linux 컨테이너의 전체 솔루션을 빌드하는 데 약 22분 정도 걸립니다.

상당히 간단한 Docker의 레이어 캐시 기능을 활용할 것인데, 기본 이미지와 명령이 이전에 실행된 것과 동일한 경우 명령을 실행할 필요 없이 결과 레이어만 사용하므로 시간이 절약됩니다.

그러면 **build** 단계를 중점적으로 살펴보겠습니다. 5-6줄은 거의 동일하지만 7-17줄은 eShopOnContainers의 각 서비스마다 다르므로 매번 실행해야 합니다. 하지만 7-16줄을 다음과 같이 변경할 경우

```Dockerfile
COPY . .
```

모든 서비스에 동일해집니다. 전체 솔루션이 복사되고 더 큰 레이어가 생성됩니다. 단,

1. 복사 프로세스는 처음에만 실행되고(그리고 파일이 변경되어 다시 빌드하는 경우) 다른 모든 서비스에 캐시를 사용합니다.

2. 중간 단계에서 더 큰 이미지가 생성되므로 최종 이미지 크기는 달라지지 않습니다.

다음으로 중요한 최적화는 17줄에서 실행된 `restore` 명령과 관련이 있습니다. 이 명령도 역시 eShopOnContainers의 각 서비스마다 다릅니다. 이 줄을 다음과 같이 변경할 경우

```Dockerfile
RUN dotnet restore
```

현재 전략으로 전체 솔루션의 패키지를 복원하려면 15번을 반복해야 하는 것과는 달리 단 한 번에 패키지를 복원할 수 있습니다.

하지만 `dotnet restore`는 폴더에 단일 프로젝트나 솔루션 파일이 있을 경우에만 실행되므로 이 방법은 약간 복잡하며 너무 세세한 부분까지 접근하지 않고 이 작업을 처리하는 방법은 다음과 같습니다.

1. **.dockerignore**에 다음 줄을 추가합니다.

   - `*.sln` - 기본 폴더 트리의 모든 솔루션 파일 무시

   - `!eShopOnContainers-ServicesAndWebApps.sln` - 이 솔루션 파일만 포함

2. `dotnet restore`에 `/ignoreprojectextensions:.dcproj` 인수를 포함하여 docker-compose 프로젝트를 무시하고 eShopOnContainers-ServicesAndWebApps 솔루션의 패키지만 복원하도록 합니다.

마지막 최적화를 보겠습니다. 20줄 바로 다음에 오는 23줄에서 애플리케이션을 빌드하므로 20줄은 불필요하며 시간이 오래 걸리는 명령을 또 한 번 실행해야 합니다.

결과 파일은 다음과 같습니다.

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS publish
 6  WORKDIR /src
 7  COPY . .
 8  RUN dotnet restore /ignoreprojectextensions:.dcproj
 9  WORKDIR /src/src/Services/Catalog/Catalog.API
10  RUN dotnet publish Catalog.API.csproj -c Release -0 /app
11
12  FROM base AS final
13  WORKDIR /app
14  COPY --from=publish /app
15  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

### <a name="creating-your-base-image-from-scratch"></a>기본 이미지를 처음부터 새로 만들기

개발자 고유의 Docker 기본 이미지를 처음부터 새로 만들 수 있습니다. 이 시나리오는 Docker를 시작하는 분들에게는 권장하지 않지만, 자신만의 고유한 기본 이미지 비트를 설정하고 싶은 분들은 그렇게 하셔도 됩니다.

### <a name="additional-resources"></a>추가 자료

- **다중 아키텍처 .NET Core 이미지**.\
  <https://github.com/dotnet/announcements/issues/14>

- **기본 이미지 만들기**. 공식 Docker 설명서입니다.\
  <https://docs.docker.com/develop/develop-images/baseimages/>

![3 - Dockerfile에 정의된 이미지 만들기](./media/image7.png)

## <a name="step-3-create-your-custom-docker-images-and-embed-your-application-or-service-in-them"></a>3단계. 고유의 사용자 지정 Docker 이미지를 만들고 그 안에 애플리케이션 또는 서비스 포함

애플리케이션의 서비스마다 관련 이미지를 만들어야 합니다. 애플리케이션이 단일 서비스 또는 웹 애플리케이션으로 구성된 경우 단일 이미지만 필요합니다.

Docker 이미지는 Visual Studio에서 자동으로 빌드됩니다. 다음 단계는 편집기/CLI 워크플로에만 필요하며 내부적으로 발생하는 동작에 대한 이해를 돕기 위해 설명되었습니다.

개발자는 완료된 기능 또는 변경 내용을 소스 제어 시스템(예: GitHub)으로 푸시할 때까지 로컬로 개발 및 테스트해야 합니다. 즉, Docker 이미지를 만들고 로컬 Docker 호스트(Windows 또는 Linux VM)에 컨테이너를 배포한 후 로컬 컨테이너에 대해 실행, 테스트 및 디버그해야 합니다.

로컬 환경에서 Docker CLI 및 Dockerfile을 사용하여 사용자 지정 이미지를 만들려면 그림 5-5처럼 docker build 명령을 사용합니다.

![Docker 이미지 빌드 진행률 화면](./media/image8.png)

**그림 5-5**. 사용자 지정 Docker 이미지 만들기

필요에 따라 프로젝트 폴더에서 직접 docker 빌드를 실행하는 대신, 먼저 `dotnet publish`를 실행하여 필수 .NET 라이브러리와 이진 파일로 배포 가능 폴더를 생성한 다음, `docker build` 명령을 사용할 수 있습니다.

그러면 이름이 `cesardl/netcore-webapi-microservice-docker:first`인 Docker 이미지가 생성됩니다. 이 경우 첫 번째는 특정 버전을 나타내는 태그입니다. 구성된 Docker 애플리케이션에 대해 만들어야 하는 사용자 지정 이미지마다 이 단계를 반복할 수 있습니다.

또한 애플리케이션이 여러 컨테이너로 구성된 경우(즉, 다중 컨테이너 애플리케이션인 경우) `docker-compose up --build` 명령을 사용하여 관련 docker-compose.yml 파일에 노출된 메타데이터를 통해 단일 명령으로 모든 관련 이미지를 만들 수 있습니다.

그림 5-6처럼 docker images 명령을 사용하여 로컬 리포지토리에서 기존 이미지를 찾을 수 있습니다.

![docker images 명령의 이미지 목록 화면 보기](./media/image9.png)

**그림 5-6.** docker images 명령을 사용하여 기존 이미지 보기

### <a name="creating-docker-images-with-visual-studio"></a>Visual Studio로 Docker 이미지 만들기

Visual Studio를 사용하여 Docker가 지원되는 프로젝트를 만드는 경우 이미지를 명시적으로 만들지 마세요. 대신 **F5**(또는 **Ctrl-F5**) 키를 눌러 Docker화된 애플리케이션 또는 서비스를 실행하면 자동으로 이미지가 만들어집니다. 이 단계는 Visual Studio에서 자동으로 실행되며 사용자에게는 보이지 않지만 내부적으로 어떤 일이 발생하는지 알아두어야 합니다.

![4 - (선택 사항) docker-compose.yml 파일에 서비스 작성](./media/image10.png)

## <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application"></a>4단계. 다중 컨테이너 Docker 애플리케이션을 빌드할 때 docker compose.yml 파일에서 서비스 정의

[docker compose.yml](https://docs.docker.com/compose/compose-file/) 파일을 사용하여 배포 명령을 통해 구성된 애플리케이션으로 배포할 관련 서비스 집합을 정의할 수 있습니다. 또한 해당 종속성 관계 및 런타임 구성을 구성합니다.

docker-compose.yml 파일을 사용하려면 기본 또는 루트 솔루션 폴더에 다음 예제와 비슷한 콘텐츠가 있는 파일을 만들어야 합니다.

```yml
version: '3.4'

services:

  webmvc:
    image: eshop/web
    environment:
      - CatalogUrl=http://catalog.api
      - OrderingUrl=http://ordering.api
    ports:
      - "80:80"
    depends_on:
      - catalog.api
      - ordering.api

  catalog.api:
    image: eshop/catalog.api
    environment:
      - ConnectionString=Server=sql.data;Port=1433;Database=CatalogDB;…
    ports:
      - "81:80"
    depends_on:
      - sql.data

  ordering.api:
    image: eshop/ordering.api
    environment:
      - ConnectionString=Server=sql.data;Database=OrderingDb;…
    ports:
      - "82:80"
    extra_hosts:
      - "CESARDLBOOKVHD:10.0.75.1"
    depends_on:
      - sql.data

  sql.data:
    image: mssql-server-linux:latest
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
```

이 docker-compose.yml 파일은 단순화되고 병합된 버전입니다. 항상 필요한 각 컨테이너에 대한 정적인 구성 데이터(사용자 지정 이미지처럼)와 연결 문자열처럼 배포 환경에 종속된 구성 정보를 포함합니다. 이후 섹션에서는 환경 및 실행 유형(디버그 또는 릴리스)에 따라 docker-compose.yml 구성을 여러 docker-compose 파일로 분할하고 값을 재정의하는 방법을 알아보겠습니다.

docker-compose.yml 파일 예제에서는 컨테이너로 실행되는 SQL Server for Linux를 기반으로 `webmvc` 서비스(웹 애플리케이션), 2개의 마이크로 서비스(`ordering.api` 및 `basket.api`), 1개의 데이터 원본 컨테이너, `sql.data`의 총 4개 서비스를 정의합니다. 각 서비스는 컨테이너로 배포되므로 각 서비스에 Docker 이미지가 필요합니다.

docker-compose.yml 파일은 사용되는 컨테이너뿐 아니라 개별적으로 구성되는 방법까지 지정합니다. 예를 들어 .yml 파일의 `webmvc` 컨테이너 정의는 다음과 같은 일을 합니다.

- 미리 빌드된 `eshop/web:latest` 이미지를 사용합니다. 그러나 docker-compose 파일의 빌드: 섹션을 기반으로 한 추가 구성을 사용하여 docker-compose 실행의 일부로 빌드되도록 이미지를 구성할 수도 있습니다.

- 두 환경 변수(CatalogUrl 및 OrderingUrl)를 초기화합니다.

- 컨테이너에 노출된 포트 80을 호스트 컴퓨터의 포트 80으로 전달합니다.

- depends_on 설정을 사용하여 웹앱을 카탈로그 및 주문 서비스와 연결합니다. 이렇게 하면 서비스는 이러한 서비스가 시작될 때까지 대기합니다.

이후 섹션에서 마이크로 서비스 및 다중 컨테이너 앱을 구현하는 방법을 알아볼 때 docker-compose.yml 파일을 다시 한 번 살펴보겠습니다.

### <a name="working-with-docker-composeyml-in-visual-studio-2017"></a>Visual Studio 2017에서 docker-compose.yml 파일 작업

앞서 말한 것처럼 Visual Studio 2017(15.8 버전부터)은 프로젝트에 Dockerfile을 추가하는 것 외에도 Docker Compose에 대한 오케스트레이터 지원을 솔루션에 추가할 수 있습니다.

그림 5-7에 나와 있는 것처럼 컨테이너 오케스트레이터 지원을 처음으로 추가하면 Visual Studio가 프로젝트용 Dockerfile을 만들고 몇 가지 글로벌 `docker-compose*.yml` 파일을 사용하여 솔루션에 새로운(서비스 섹션) 프로젝트를 만든 후 이러한 파일에 프로젝트를 추가합니다. 그런 다음, docker-compose.yml 파일을 열고 추가 기능을 업데이트할 수 있습니다.

docker-compose.yml 파일에 포함할 각 프로젝트에서 이 작업을 반복해서 수행해야 합니다.

이러한 작성 과정에서 Visual Studio는 Docker Compose 및 Service Fabric 오케스트레이터를 지원합니다.

![ASP.NET Core 프로젝트에 오케스트레이터 지원을 추가하는 바로 가기 메뉴 옵션](./media/image21.png)

**그림 5-7**. ASP.NET Core 프로젝트를 마우스 오른쪽 단추로 클릭하여 Visual Studio 2017에 Docker 지원 추가

Visual Studio에서 솔루션에 오케스트레이터 지원을 추가하면 그림 5-8처럼 추가된 docker-compose.yml 파일을 포함하는 새 노드(`docker-compose.dcproj` 프로젝트 파일에 있는)가 솔루션 탐색기에 표시됩니다.

![솔루션 탐색기의 docker-compose 노드](./media/image11.png)

**그림 5-8**. Visual Studio 2017 솔루션 탐색기에 추가된 **docker-compose** 트리 노드

`docker-compose up` 명령을 사용하여 단일 docker-compose.yml 파일이 있는 다중 컨테이너 애플리케이션을 배포할 수 있습니다. 그러나 Visual Studio에서 그룹으로 추가하므로 개발자는 환경(개발 또는 프로덕션) 및 실행 형식(릴리스 또는 디버그)에 따라 값을 재정의할 수 있습니다. 이 기능에 대한 내용은 이후 섹션에서 설명하겠습니다.

![5 - 컨테이너 또는 작성된 앱 실행](./media/image12.png)

## <a name="step-5-build-and-run-your-docker-application"></a>5단계. Docker 애플리케이션을 빌드하고 실행

애플리케이션에 단일 컨테이너만 있는 경우 애플리케이션을 Docker 호스트(VM 또는 실제 서버)에 배포하여 실행할 수 있습니다. 그러나 애플리케이션에 여러 서비스가 있는 경우에는 단일 CLI 명령(docker-compose up)을 사용하여 또는 이 명령을 내부적으로 실행하는 Visual Studio를 사용하여 구성된 애플리케이션으로 배포할 수 있습니다. 다양한 옵션을 살펴보겠습니다.

### <a name="option-a-running-a-single-container-application"></a>옵션 A: 단일 컨테이너 애플리케이션 실행

#### <a name="using-docker-cli"></a>Docker CLI 사용

그림 5-9처럼 `docker run` 명령을 사용하여 Docker 컨테이너를 실행할 수 있습니다.

```console
  docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

위의 명령이 실행될 때마다 지정된 이미지에서 새 컨테이너 인스턴스가 생성됩니다. `--name` 매개 변수를 사용하여 컨테이너에 이름을 지정한 다음, `docker start {name}`(또는 컨테이너 ID나 자동 이름)을 사용하여 기존의 컨테이너 인스턴스를 실행할 수 있습니다.

![docker run 명령을 사용하여 Docker 컨테이너를 실행할 때의 화면 보기](./media/image13.png)

**그림 5-9**. docker run 명령을 사용하여 Docker 컨테이너 실행

이 경우 이 명령은 컨테이너의 내부 포트 5000을 호스트 컴퓨터의 포트 80에 바인딩합니다. 즉, 호스트가 포트 80에서 수신 대기하고 컨테이너의 포트 5000에 전달합니다.

표시된 해시는 컨테이너 ID이며, `--name` 옵션이 사용되지 않은 경우 임의의 가독성 있는 이름도 할당됩니다.

#### <a name="using-visual-studio"></a>Visual Studio 사용

컨테이너 오케스트레이터 지원을 추가하지 않은 경우 Visual Studio에서 **Ctrl-F5**를 눌러 단일 컨테이너 앱을 실행할 수도 있고, **F5** 키를 사용하여 컨테이너 내에서 애플리케이션을 디버깅할 수도 있습니다. 컨테이너는 docker run을 사용하여 로컬로 실행됩니다.

### <a name="option-b-running-a-multi-container-application"></a>옵션 B: 다중 컨테이너 애플리케이션 실행

대부분의 엔터프라이즈 시나리오에서 Docker 애플리케이션은 여러 서비스로 구성되며, 따라서 그림 5-10처럼 다중 컨테이너 애플리케이션을 실행해야 합니다.

![여러 Docker 컨테이너가 있는 VM](./media/image14.png)

**그림 5-10**. Docker 컨테이너가 배포된 VM

#### <a name="using-docker-cli"></a>Docker CLI 사용

Docker CLI를 사용하여 다중 컨테이너 애플리케이션을 실행하려면 `docker-compose up` 명령을 사용하세요. 이 명령은 솔루션 수준에서 **docker-compose.yml** 파일을 사용하여 다중 컨테이너 애플리케이션을 배포합니다. 그림 5-11은 기본 솔루션 디렉터리에서 명령을 실행할 때의 결과를 보여주며, docker-compose.yml 파일이 포함되어 있습니다.

![docker-compose up 명령을 실행할 때의 화면 보기](./media/image15.png)

**그림 5-11**. docker-compose up 명령을 실행할 때의 결과 예제

docker-compose up 명령을 실행하면 그림 5-10에 나와 있는 것처럼 애플리케이션 및 관련 컨테이너가 Docker 호스트에 배포됩니다.

#### <a name="using-visual-studio"></a>Visual Studio 사용

Visual Studio 2017을 사용하여 다중 컨테이너 애플리케이션을 실행하는 방법이 더 이상 간단할 수 없습니다. 평상시처럼 **Ctrl-F5**를 눌러 실행하거나 **F5** 키를 눌러 디버깅하여 **docker-compose** 프로젝트를 시작 프로젝트로 설정하기만 하면 됩니다.  Visual Studio가 필요한 모든 설정을 처리하므로 평상시처럼 중단점을 만들고 최종적으로 "원격 서버"에서 실행되는 독립 프로세스를 디버깅할 수 있습니다.

앞서 언급했듯이, 솔루션 내의 프로젝트에 Docker 솔루션 지원을 추가할 때마다 해당 프로젝트가 전역(솔루션 수준) docker-compose.yml 파일에서 구성되며, 따라서 전체 솔루션을 한꺼번에 실행 또는 디버그할 수 있습니다. Visual Studio는 Docker 솔루션 지원이 사용되는 각 프로젝트에 대해 하나의 컨테이너를 시작하고, 모든 내부 단계(dotnet 게시, dotnet 빌드 등)를 자동으로 수행합니다.

모든 단조로운 작업을 엿보려면 파일을 살펴보세요

`{root solution folder}\obj\Docker\docker-compose.vs.debug.g.yml`

여기서 중요한 점은, 그림 5-12처럼 Visual Studio 2017에는 F5 키 작업에 대한 추가 **Docker** 명령이 있다는 것입니다. 이 옵션을 통해 솔루션 수준에서 docker-compose.yml 파일에 정의된 모든 컨테이너를 실행하여 다중 컨테이너 애플리케이션을 디버깅할 수 있습니다. 다중 컨테이너 솔루션을 디버그하는 기능이 있다는 것은 서로 다른 프로젝트(컨테이너)마다 하나씩 여러 중단점을 지정할 수 있으며, Visual Studio에서 디버깅할 때 여러 프로젝트에서 정의되어 여러 컨테이너에서 실행되는 중단점에서 중지된다는 의미입니다.

![docker-compose 프로젝트를 실행 중인 Visual Studio 디버그 도구 모음](./media/image16.png)

**그림 5-12**. Visual Studio 2017에서 다중 컨테이너 앱 실행

### <a name="additional-resources"></a>추가 자료

- **원격 Docker 호스트에 ASP.NET 컨테이너 배포** \
  <https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker>

### <a name="a-note-about-testing-and-deploying-with-orchestrators"></a>오케스트레이터를 사용하여 테스트 및 배포하는 내용에 대한 메모

docker-compose up 및 docker run 명령(또는 Visual Studio에서 컨테이너를 실행하고 디버깅)은 개발 환경에서 컨테이너를 테스트하기에 충분합니다. 하지만 프로덕션 배포의 경우에는 이 접근법을 사용하지 말고 [Kubernetes](https://kubernetes.io/) 또는 [Service Fabric](https://azure.microsoft.com/services/service-fabric/) 같은 오케스트레이터를 대상으로 해야 합니다. Kubernetes를 사용 중인 경우 [pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/)로 컨테이너와 [서비스](https://kubernetes.io/docs/concepts/services-networking/service/)를 정리하여 연결해야 합니다. 또한 [배포](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)를 사용하여 pod 생성 및 수정을 정리해야 합니다.

![6 - 앱 또는 마이크로 서비스 테스트](./media/image17.png)

## <a name="step-6-test-your-docker-application-using-your-local-docker-host"></a>6단계. 로컬 Docker 호스트를 사용하여 Docker 애플리케이션 테스트

이 단계는 애플리케이션에서 하는 일에 따라 달라집니다. 단일 컨테이너 또는 서비스로 배포되는 간단한 .NET Core 웹 애플리케이션에서는 그림 5-13처럼 Docker 호스트에서 브라우저를 열고 해당 사이트로 이동하여 서비스에 액세스할 수 있습니다. (Dockerfile의 구성이 컨테이너를 호스트에 있는 80 이외의 포트로 매핑하는 경우 호스트 포트를 URL에 포함합니다.)

![API 엔드포인트 응답의 브라우저 보기](./media/image18.png)

**그림 5-13**. localhost를 사용하여 로컬로 Docker 애플리케이션을 테스트하는 예제

localhost가 Docker 호스트 IP를 가리키지 않는 경우(Docker CE를 사용하는 경우 기본적으로 Docker 호스트 IP를 가리켜야 함) 서비스를 탐색하려면 머신 네트워크 카드의 IP 주소를 사용합니다.

브라우저에서 이 URL은 우리가 살펴보고 있는 특정 컨테이너 예제에 대한 포트 80을 사용합니다. 그러나 내부적으로는 요청이 포트 5000으로 리디렉션됩니다. 왜냐하면 이전 단계에서 설명했듯이 docker run 명령을 사용하여 이와 같은 방법으로 배포되었기 때문입니다.

그림 5-14처럼 터미널에서 curl을 사용하여 애플리케이션을 테스트할 수도 있습니다. Windows에 설치된 Docker에서 기본 Docker 호스트 IP는 머신의 실제 IP 주소와는 별개로 항상 10.0.75.1입니다.

![curl을 사용하는 API 엔드포인트 응답의 화면 보기](./media/image19.png)

**그림 5-14**. curl을 사용하여 로컬로 Docker 애플리케이션을 테스트하는 예제

### <a name="testing-and-debugging-containers-with-visual-studio-2017"></a>Visual Studio 2017을 사용하여 컨테이너 테스트 및 디버깅

Visual Studio 2017을 사용하여 컨테이너를 실행하고 디버깅할 때 컨테이너 없이 실행할 때와 거의 동일한 방법으로 .NET 애플리케이션을 디버그할 수 있습니다.

### <a name="testing-and-debugging-without-visual-studio"></a>Visual Studio 없이 디버깅 및 테스트

편집기/CLI 방식을 사용하여 개발하는 경우 컨테이너를 디버깅하기가 훨씬 어려우며 추적을 생성하여 디버그하는 것이 좋습니다.

### <a name="additional-resources"></a>추가 자료

- **로컬 Docker 컨테이너에서 앱 디버그** \
  [https://docs.microsoft.com/visualstudio/containers/edit-and-refresh](/visualstudio/containers/edit-and-refresh)

- **Steve Lasker. Docker를 사용하여 ASP.NET Core 앱 빌드, 디버그, 배포.** 비디오. \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T115>

## <a name="simplified-workflow-when-developing-containers-with-visual-studio"></a>Visual Studio를 사용하여 컨테이너를 개발할 때의 간소화된 워크플로

Visual Studio를 사용하면 편집기/CLI 방식을 사용할 때보다 워크플로가 훨씬 간단합니다. Dockerfile 및 docker-compose.yml 파일과 관련하여 Docker에 필요한 대부분의 단계는 그림 5-15처럼 숨겨져 있거나 Visual Studio를 통해 간소화됩니다.

![Visual Studio를 사용하는 간편한 컨테이너 개발 워크플로: 1 - 앱 코딩, 2 - 프로젝트에 Docker 지원 추가(한 번만), 3 - 컨테이너 또는 docker-compose 앱 실행, 4 - 앱 또는 마이크로 서비스 테스트, 5 - 리포지토리에 푸시하고 반복.](./media/image20.png)

**그림 5-15**. Visual Studio를 사용하여 배포할 때의 간소화된 워크플로

또한 2단계(프로젝트에 Docker 지원 추가)를 한 번만 수행하면 됩니다. 따라서 다른 개발에서 .NET을 사용하여 수행하는 일반적인 개발 작업과 워크플로가 비슷합니다. 내부에서 어떤 동작이 발생하는지(이미지 빌드 프로세스, 사용하는 기본 이미지, 컨테이너 배포 등) 알아야 하며, 때로는 Dockerfile 또는 docker-compose.yml 파일을 편집하여 동작을 사용자 지정해야 합니다. 하지만 Visual Studio를 사용하여 대부분의 작업이 대폭 간소화되므로 개발자의 생산성이 크게 향상됩니다.

### <a name="additional-resources"></a>추가 자료

- **Steve Lasker. Visual Studio 2017을 사용한 .NET Docker 개발** \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T111>

## <a name="using-powershell-commands-in-a-dockerfile-to-set-up-windows-containers"></a>DockerFile에서 PowerShell 명령을 사용하여 Windows 컨테이너 설정

[Windows 컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/about/index)를 사용하면 Docker 생태계의 나머지 부분과 동일한 도구로 기존 Windows 애플리케이션을 Docker 이미지로 변환하고 배포할 수 있습니다. Windows 컨테이너를 사용하려면 다음 예제와 같이 Dockerfile에서 PowerShell 명령을 실행합니다.

```Dockerfile
FROM microsoft/windowsservercore
LABEL Description="IIS" Vendor="Microsoft" Version="10"
RUN powershell -Command Add-WindowsFeature Web-Server
CMD [ "ping", "localhost", "-t" ]
```

이 예에서는 PowerShell 명령(RUN 설정)을 통해 Windows Server Core 기본 이미지(FROM 설정)를 사용하고 IIS를 설치합니다. 비슷한 방법으로 PowerShell 명령을 사용하여 ASP.NET 4.x, .NET 4.6 또는 다른 Windows 소프트웨어 같은 추가 구성 요소를 설치할 수도 있습니다. 예를 들어 Dockerfile의 다음 명령은 ASP.NET 4.5를 설치합니다.

```Dockerfile
RUN powershell add-windowsfeature web-asp-net45
```

### <a name="additional-resources"></a>추가 자료

- **aspnet-docker/Dockerfile.** Windows 기능을 포함하도록 dockerfile에서 실행되는 PowerShell 명령 예제.\
  <https://github.com/Microsoft/aspnet-docker/blob/master/4.7.1-windowsservercore-ltsc2016/runtime/Dockerfile>

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](../multi-container-microservice-net-applications/index.md)
