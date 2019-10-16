---
title: Docker 앱을 위한 내부 루프 개발 워크플로
description: Docker 애플리케이션 개발을 위한 "내부 루프" 워크플로에 대해 알아봅니다.
ms.date: 02/15/2019
ms.openlocfilehash: 565852511f3a837066d5da5cf0e3ab0a902dd7da
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956549"
---
# <a name="inner-loop-development-workflow-for-docker-apps"></a>Docker 앱을 위한 내부 루프 개발 워크플로

전체 DevOps 주기를 포함하는 외부 루프 워크플로를 트리거하기 전에 각 개발자의 머신에서 앱 자체 코딩, 선호하는 언어 또는 플랫폼 사용 및 로컬로 테스트를 모두 시작합니다(그림 4-21). 그러나 모든 경우 선택하는 언어, 프레임워크 또는 플랫폼과 상관없이 공통되는 중요한 지점이 있습니다. 이 특정 워크플로에서는 항상 Docker 컨테이너를 개발 및 테스트하되, 로컬로 수행합니다.

![내부 루프 개발 환경의 개념을 보여 주는 다이어그램입니다.](./media/docker-apps-inner-loop-workflow/inner-loop-development-context.png)

**그림 4-21**. 내부 루프 개발 컨텍스트

Docker 이미지의 컨테이너 또는 인스턴스는 다음 구성 요소를 포함합니다.

- 운영 체제 선택(예: Linux 배포판 또는 Windows)

- 개발자가 추가한 파일(예: 앱 이진 파일)

- 구성(예: 환경 설정 및 종속성)

- Docker에서 실행할 프로세스에 대한 지침

Docker를 프로세스로 이용하는 내부 루프 개발 워크플로를 설정할 수 있습니다(다음 섹션에서 설명). 환경을 설정하는 초기 단계는 한 번만 수행하면 되므로 포함되지 않는 것을 고려합니다.

## <a name="building-a-single-app-within-a-docker-container-using-visual-studio-code-and-docker-cli"></a>Visual Studio Code 및 Docker CLI를 사용하여 Docker 컨테이너 내에서 단일 앱 빌드

앱은 개발자 고유의 서비스와 추가 라이브러리(종속성)로 구성됩니다.

그림 4-22는 Docker 앱을 빌드할 때 일반적으로 수행해야 하는 기본 단계를 보여준 다음, 각 단계를 자세히 설명합니다.

![컨테이너화 된 앱을 만드는 데 필요한 7가지 단계를 보여 주는 다이어그램입니다.](./media/docker-apps-inner-loop-workflow/life-cycle-containerized-apps-docker-cli.png)

**그림 4-22**. Docker CLI를 사용하여 Docker 컨테이너화된 애플리케이션 수명 주기에 대한 고급 워크플로

### <a name="step-1-start-coding-in-visual-studio-code-and-create-your-initial-appservice-baseline"></a>1단계: Visual Studio Code에서 코딩을 시작하고 초기 앱/서비스 기준선 만들기

애플리케이션을 개발하는 방법은 Docker 없이 수행하는 방법과 유사합니다. 다른 점은 개발하는 동안 로컬 환경(예: Linux VM 또는 Windows)에 배치된 Docker 컨테이너 내에서 실행하는 애플리케이션 또는 서비스를 배포 및 테스트한다는 것입니다.

**로컬 환경 설정**

최신 버전의 Mac용 및 Windows용 Docker를 사용하면 이전의 어느 때보다 쉽게 Docker 애플리케이션을 개발할 수 있으며 설정도 간단합니다.

> [!TIP]
> Windows용 Docker 설정 지침은 <https://docs.docker.com/docker-for-windows/>로 이동합니다.
>
>Mac용 Docker 설정 지침은 <https://docs.docker.com/docker-for-mac/>으로 이동합니다.

또한 Docker CLI를 사용하는 동안 실제로 애플리케이션을 개발할 수 있도록 코드 편집기가 필요합니다.

Microsoft는 Windows, Linux 및 macOS에서 지원되는 경량 코드 편집기인 Visual Studio Code를 제공하고, IntelliSense에서 [다양한 언어에 대한 지원](https://code.visualstudio.com/docs/languages/overview)(JavaScript, .NET, Go, Java, Ruby, Python 및 가장 최신 언어), [디버깅](https://code.visualstudio.com/Docs/editor/debugging), [Git와의 통합](https://code.visualstudio.com/Docs/editor/versioncontrol), [확장명 지원](https://code.visualstudio.com/docs/extensions/overview) 등을 제공합니다. 이 편집기는 macOS 및 Linux 개발자에게 적합합니다. Windows에서는 Visual Studio를 사용할 수도 있습니다.

> [!TIP]
> Windows, Linux 또는 macOS에서의 Visual Studio Code 설치 지침은 <https://code.visualstudio.com/docs/setup/setup-overview/>으로 이동합니다.
>
> Mac용 Docker 설정 지침은 <https://docs.docker.com/docker-for-mac/>으로 이동합니다.

Docker CLI로 작업하고 임의의 코드 편집기를 사용하여 코드를 작성할 수 있지만, Docker 확장을 포함하는 Visual Studio Code를 사용하면 작업 영역에서 `Dockerfile` 및 `docker-compose.yml` 파일을 작성하기 쉽습니다. 또한 Visual Studio Code IDE에서 작업 및 스크립트를 실행하고 아래의 Docker CLI를 사용하여 Docker 명령을 실행할 수도 있습니다.

VS Code용 Docker 확장은 다음 기능을 제공합니다.

- 자동 `Dockerfile` 및 `docker-compose.yml` 파일 생성

- `docker-compose.yml` 및 `Dockerfile` 파일에 대한 구문 강조 표시 및 가리키기 정보

- `Dockerfile` 및 `docker-compose.yml` 파일에 대한 IntelliSense(완성판)

- `Dockerfile` 파일에 대한 린팅(오류 및 경고)

- 가장 일반적인 Docker 명령에 대한 명령 팔레트(F1) 통합

- 이미지 및 컨테이너를 관리하기 위한 탐색기 통합

- Azure App Service에 DockerHub 및 Azure 컨테이너 레지스트리의 이미지 배포

Docker 확장을 설치하려면 Ctrl+Shift+P를 누르고 `ext install`을 입력한 후 Install Extension 명령을 실행하여 Marketplace 확장 목록을 표시합니다. 그런 다음, **docker**를 입력하여 결과를 필터링한 후 그림 4-23과 같이 Docker Support 확장을 선택합니다.

![VS Code용 Docker 확장 보기](./media/docker-apps-inner-loop-workflow/install-docker-extension-vs-code.png)

**그림 4-23** Visual Studio Code에 Docker 확장 설치

### <a name="step-2-create-a-dockerfile-related-to-an-existing-image-plain-os-or-dev-environments-like-net-core-nodejs-and-ruby"></a>2단계: 기존 이미지와 관련된 DockerFile 만들기(일반 OS 또는 .NET Core, Node.js 및 Ruby와 같은 dev 환경)

빌드할 사용자 지정 이미지 및 배포할 컨테이너마다 `DockerFile`이 필요합니다. 앱이 단일 사용자 지정 서비스로 구성된 경우 단일 `DockerFile`이 필요합니다. 그러나 앱이 여러 서비스로 구성된 경우(마이크로서비스 아키텍처의 경우와 같이) 서비스마다 한 개의 `Dockerfile`이 필요합니다.

`DockerFile`은 일반적으로 앱 또는 서비스의 루트 폴더에 배치되며 Docker가 해당 앱 또는 서비스를 설정하고 실행하는 방법을 알 수 있도록 하는 데 필요한 명령을 포함합니다. 자신의 `DockerFile`을 만들고 코드(node.js, .NET Core 등)와 함께 프로젝트에 추가하거나 새로운 환경인 경우 다음 정보를 살펴봅니다.

> [!TIP]
> 컨테이너와 관련된 `Dockerfile` 및 `docker-compose.yml` 파일을 사용하는 경우 Docker 확장을 사용하여 안내를 받을 수 있습니다. 결국 이러한 종류의 파일은 이 도구 없이 작성하겠지만 Docker 확장 사용은 학습 진도를 가속화하는 좋은 시작점이 될 것입니다.

그림 4-24에서 VS Code용 Docker 확장을 사용하여 Docker-Compose 파일이 추가되는 방법을 확인할 수 있습니다.

![VS Code용 Docker 확장의 콘솔 보기](./media/docker-apps-inner-loop-workflow/add-docker-files-to-workspace-command.png)

**그림 4-24** **작업 영역에 Docker 파일 추가 명령**을 사용하여 추가한 Docker 파일

DockerFile을 추가하는 경우 사용 중인 기본 Docker 이미지가 무엇인지 지정합니다(예: `FROM mcr.microsoft.com/dotnet/core/aspnet`을 사용하여). 일반적으로 [Docker Hub 레지스트리](https://hub.docker.com/)의 공식 리포지토리에서 가져오는 기본 이미지(예: [.NET Core용 이미지](https://hub.docker.com/_/microsoft-dotnet-core/) 또는 [Node.js](https://hub.docker.com/_/node/)용 이미지) 위에 사용자 지정 이미지를 빌드합니다.

***기존의 공식 Docker 이미지 사용***

버전 번호가 있는 언어 스택의 공식 리포지토리를 사용하면 모든 머신(개발, 테스트 및 프로덕션 포함)에서 동일한 언어 기능을 사용할 수 있습니다.

다음은 .NET Core 컨테이너에 대한 샘플 DockerFile입니다.

```Dockerfile
# Base Docker image to use  
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
  
# Set the Working Directory and files to be copied to the image  
ARG source  
WORKDIR /app  
COPY ${source:-bin/Release/PublishOutput} .  
  
# Configure the listening port to 80 (Internal/Secured port within Docker host)  
EXPOSE 80  
  
# Application entry point  
ENTRYPOINT ["dotnet", "MyCustomMicroservice.dll"]
```

이 경우 이미지는 줄 `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`에 따라 버전 2.2의 공식 ASP.NET Core Docker 이미지(Linux용 및 Windows용 다중 아키텍처)를 기반으로 합니다. (이 주제에 대한 자세한 내용은 [ASP.NET Core Docker 이미지](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) 페이지 및 [.NET Core Docker 이미지](https://hub.docker.com/_/microsoft-dotnet-core/) 페이지를 참조하세요.)

DockerFile에서 Docker에 대해 런타임에 사용할 TCP 포트(예: 포트 80)를 수신 대기하도록 지시할 수도 있습니다.

사용하는 언어 및 프레임워크에 따라 Dockerfile에서 추가 구성 설정을 지정할 수 있습니다. 예를 들어 `["dotnet", "MySingleContainerWebApp.dll"]`이 포함된 `ENTRYPOINT` 줄은 Docker에 대해 .NET Core 애플리케이션을 실행하라고 알려줍니다. SDK 및 .NET Core CLI(`dotnet CLI`)를 사용하여 .NET 애플리케이션을 빌드하고 실행하는 경우 이 설정이 달라집니다. 여기서 중요한 점은 ENTRYPOINT 줄 및 기타 설정은 애플리케이션에 대해 선택하는 언어 및 플랫폼에 따라 달라진다는 것입니다.

> [!TIP]
> .NET Core 애플리케이션용 Docker 이미지 빌드에 대한 자세한 내용은 <https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images>로 이동합니다.
>
> 자신의 고유한 이미지 빌드에 대해 자세히 알아보려면 <https://docs.docker.com/engine/tutorials/dockerimages/>로 이동합니다.

**다중 아키텍처 이미지 리포지토리 사용**

리포지토리의 단일 이미지 이름은 Linux 이미지 및 Windows 이미지와 같은 플랫폼 변형을 포함할 수 있습니다. 이 기능을 통해 Microsoft와 같은 공급업체(기본 이미지 작성자)는 여러 플랫폼(즉, Linux 및 Windows)을 처리하는 단일 리포지토리를 만들 수 있습니다. 예를 들어 Docker Hub 레지스트리에서 제공되는 [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) 리포지토리는 동일한 이미지 이름을 사용하여 Linux 및 Windows Nano Server에 대한 지원을 제공합니다.

Windows 호스트에서 [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) 이미지를 풀하면 Windows 변형을 풀하고, Linux 호스트에서 동일한 이미지 이름을 풀하면 Linux 변형을 풀합니다.

***기본 이미지를 처음부터 새로 만들기***

이 [문서](https://docs.docker.com/engine/userguide/eng-image/baseimages/)에서 설명한 대로 Docker에서 자신의 고유한 Docker 기본 이미지를 처음부터 새로 만들 수 있습니다. 이 시나리오는 Docker를 이제 막 시작하는 경우 최선이 아닐 수 있지만, 자신의 고유한 기본 이미지에 대해 특정 비트를 설정하려는 경우 도움이 될 수 있습니다.

### <a name="step-3-create-your-custom-docker-images-embedding-your-service-in-it"></a>3단계: 서비스가 포함된 사용자 지정 Docker 이미지 만들기

앱을 구성하는 각 사용자 지정 서비스에 대해 관련된 이미지를 만들어야 합니다. 앱이 단일 서비스 또는 웹앱으로 구성된 경우 단일 이미지만 필요합니다.

> [!NOTE]
> "외부 루프 DevOps 워크플로"를 고려하는 경우 소스 코드를 Git 리포지토리에 푸시할 때마다(지속적인 통합) 자동화된 빌드 프로세스에 의해 이미지가 생성되므로 해당 이미지는 소스 코드에서 해당 글로벌 환경에 생성됩니다.
>
> 그러나 외부 루프 경로로 이동을 고려하기 전에 Docker 애플리케이션이 올바르게 작동하지 않을 수 있는 코드를 원본 제어 시스템(예: Git)에 푸시하지 않도록 실제로 올바르게 작동하는지 확인해야 합니다.
>
> 따라서 각 개발자는 먼저 로컬에서 전체 내부 루프 프로세스를 수행하여 테스트하고 전체 기능 또는 변경 내용을 원본 제어 시스템에 푸시하려 할 때까지 개발을 계속해야 합니다.

로컬 환경에서 DockerFile을 사용하여 이미지를 만들려면 그림 4-25에서 보여주듯이 docker build 명령을 사용할 수 있습니다(여러 컨테이너/서비스로 구성된 애플리케이션의 경우 `docker-compose up --build`를 실행할 수도 있음).

![docker build 명령의 콘솔 출력을 보여 주는 스크린샷입니다.](./media/docker-apps-inner-loop-workflow/run-docker-build-command.png)

**그림 4-25** Docker 빌드 실행

원할 경우 프로젝트 폴더에서 `docker build`를 실행하는 대신 먼저 run `dotnet publish` 명령을 사용하여 필요한 .NET 라이브러리를 포함하는 배포 가능한 폴더를 생성한 후 `docker build`를 실행할 수 있습니다.

이 예제에서는 이름 `cesardl/netcore-webapi-microservice-docker:first`를 사용하여 Docker 이미지를 만듭니다(`:first`는 특정 버전과 같은 태그임). 여러 컨테이너를 포함하도록 구성된 Docker 애플리케이션에 대해 만들어야 하는 각 사용자 지정 이미지마다 이 단계를 수행할 수 있습니다.

그림 4-26과 같이 docker images 명령을 사용하여 로컬 리포지토리(개발 머신)에서 기존 이미지를 찾을 수 있습니다.

![기존 이미지를 보여주는 docker images 명령의 콘솔 출력](./media/docker-apps-inner-loop-workflow/view-existing-images-with-docker-images.png)

**그림 4-26**. Docker 이미지를 사용하여 기존 이미지 보기

### <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-composed-docker-app-with-multiple-services"></a>4단계: 여러 서비스를 포함하도록 구성된 Docker 앱을 빌드할 때 docker-compose.yml에서 서비스 정의

`docker-compose.yml` 파일을 통해 다음 단계 섹션에서 설명하는 배포 명령을 사용하여 구성된 애플리케이션으로 배포할 관련 서비스 세트를 정의할 수 있습니다.

해당 파일을 주 또는 루트 솔루션 폴더에 만들며, 해당 파일은 이 `docker-compose.yml` 파일에 표시된 것과 유사한 콘텐츠를 포함해야 합니다.

```yml
version: '3.4'
services:
  web:
    build: .
    ports:
     - "81:80"
    volumes:
     - .:/code
    depends_on:
     - redis
  redis:
    image: redis
```

이 경우 이 파일은 웹 서비스(사용자 지정 서비스) 및 redis 서비스(인기 있는 캐시 서비스)의 두 가지 서비스를 정의합니다. 각 서비스는 컨테이너로 배포되므로 각 서비스에 대해 구체적인 Docker 이미지를 사용해야 합니다. 이 웹 서비스의 경우 이미지에서 다음을 수행해야 합니다.

- 현재 디렉터리의 DockerFile에서 빌드

- 컨테이너에 표시된 포트 80을 호스트 머신의 포트 81로 전달

- 이미지를 다시 빌드할 필요 없이 코드를 수정할 수 있도록 컨테이너에 대한 호스트 / 컨테이너 내의 코드에 프로젝트 디렉터리 탑재

- 웹 서비스를 redis 서비스에 연결

redis 서비스는 Docker Hub 레지스트리에서 풀한 [최신 공용 redis 이미지](https://hub.docker.com/_/redis/)를 사용합니다. [redis](https://redis.io/)는 인기 있는 서버 쪽 애플리케이션용 캐시 시스템입니다.

### <a name="step-5-build-and-run-your-docker-app"></a>5단계: Docker 앱을 빌드하고 실행

앱에 단일 컨테이너만 있는 경우 해당 앱을 Docker 호스트(VM 또는 실제 서버)에 배포하여 실행하기만 하면 됩니다. 그러나 앱이 여러 서비스로 구성된 경우 *앱 구성*도 수행해야 합니다. 다양한 옵션을 살펴보겠습니다.

***옵션 A: 단일 컨테이너 또는 서비스를 실행***

여기에서 보여주는 대로 Docker 실행 명령을 사용하여 Docker 이미지를 실행할 수 있습니다.

```console
docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

이 특정 배포의 경우 포트 80으로 보낸 요청을 내부 포트 5000으로 리디렉션합니다. 이제 애플리케이션은 호스트 수준의 외부 포트 80에서 수신 대기합니다.

***옵션 B: 여러 컨테이너 애플리케이션을 구성 및 실행***

대부분의 엔터프라이즈 시나리오에서 Docker 애플리케이션은 여러 서비스로 구성됩니다. 이 경우 이전에 만들었을 수 있는 docker-compose.yml 파일을 사용하는 `docker-compose up` 명령(그림 4-27)을 실행할 수 있습니다. 이 명령을 실행하면 모든 관련 컨테이너로 구성된 애플리케이션이 배포됩니다.

![docker-compose up 명령의 콘솔 출력](./media/docker-apps-inner-loop-workflow/results-docker-compose-up.png)

**그림 4-27**. "docker-compose up" 명령을 실행한 결과

`docker-compose up`을 실행한 후 그림 4-28에서 보여주듯이 애플리케이션 및 관련 컨테이너를 VM 표시의 Docker 호스트에 배포합니다.

![다중 컨테이너 애플리케이션을 실행하는 VM](./media/docker-apps-inner-loop-workflow/vm-with-docker-containers-deployed.png)

**그림 4-28**. Docker 컨테이너가 배포된 VM

### <a name="step-6-test-your-docker-application-locally-in-your-local-cd-vm"></a>6단계: Docker 호스트 테스트(로컬로, 로컬 CD VM에서)

이 단계는 앱이 수행하는 기능에 따라 달라집니다.

단일 컨테이너 또는 서비스로 배포된 간단한 .NET Core 웹 API "Hello World"에서는 DockerFile에 지정된 TCP 포트를 제공하여 서비스에 액세스하기만 하면 됩니다.

localhost가 켜지지 않은 경우 서비스로 이동하려면 이 명령을 사용하여 머신에 대한 IP 주소를 찾습니다.

```console
docker-machine {IP} {YOUR-CONTAINER-NAME}
```

Docker 호스트에서 브라우저를 열고 해당 사이트로 이동합니다. 그림 4-29와 같이 앱/서비스가 실행될 것입니다.

![localhost/API/값에서 오는 응답의 브라우저 보기](./media/docker-apps-inner-loop-workflow/test-docker-app-locally-localhost.png)

**그림 4-29**. localhost를 사용하여 로컬로 Docker 애플리케이션 테스트

포트 80을 사용하지만 앞에서 설명한 대로 내부적으로는 `docker run`을 사용하여 배포되는 방법에 따라 포트 5000으로 리디렉션됩니다.

터미널에서 CURL을 사용하여이 기능을 테스트할 수 있습니다. Windows의 Docker 설치에서 기본 IP는 그림 4-30과 같이 10.0.75.1입니다.

![CURL을 사용하여 http://10.0.75.1/API/values 에서 가져온 콘솔 출력](./media/docker-apps-inner-loop-workflow/test-docker-app-locally-curl.png)

**그림 4-30**. CURL을 사용하여 로컬로 Docker 애플리케이션 테스트

**Docker에서 실행되는 컨테이너 디버깅**

Visual Studio Code는 Node.js 및 다른 플랫폼(예: .NET Core 컨테이너)을 사용하는 경우 디버깅 Docker를 지원합니다.

또한 다음 섹션에서 설명하는 대로 Windows용 또는 Mac용 Visual Studio를 사용하는 경우 Docker의 .NET Core 또는 .NET Framework 컨테이너를 디버그할 수도 있습니다.

> [!TIP]
> Node.js Docker 컨테이너 디버깅에 대한 자세한 내용은 <https://blog.docker.com/2016/07/live-debugging-docker/> 및 <https://blogs.msdn.microsoft.com/user_ed/2016/02/27/visual-studio-code-new-features-13-big-debugging-updates-rich-object-hover-conditional-breakpoints-node-js-mono-more/>을 참조하세요.

>[!div class="step-by-step"]
>[이전](docker-apps-development-environment.md)
>[다음](visual-studio-tools-for-docker.md)
