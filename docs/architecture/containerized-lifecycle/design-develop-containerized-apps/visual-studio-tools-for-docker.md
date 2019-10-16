---
title: Windows의 Visual Studio Tools for Docker
description: Visual Studio 2017 버전 15.7 이상에서 사용할 수 있는 Docker 도구를 알아봅니다.
ms.date: 02/15/2019
ms.custom: vs-dotnet
ms.openlocfilehash: 2b6fdc33f9cf850cf9e52fca4a1a9754cd412567
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68673880"
---
# <a name="use-docker-tools-in-visual-studio-2017-on-windows"></a>Windows에서 Visual Studio 2017의 Docker 도구 사용

Visual Studio 2017 버전 15.7 이상에 포함된 Docker 도구를 사용하는 경우 개발자 워크플로는 Visual Studio Code 및 Docker CLI를 사용할 때와 비슷하지만(실제로 동일한 Docker CLI 기반), 더 쉽게 시작할 수 있고, 프로세스가 더 간단하고, 빌드/실행/구성 작업의 생산성이 향상됩니다. 또한 Visual Studio의 일반적인 `F5` 및 `Ctrl+F5` 키를 통해 컨테이너를 실행하고 디버그할 수 있습니다. 컨테이너가 솔루션 수준에서 동일한 `docker-compose.yml` 파일에 정의된 경우 솔루션 전체를 디버그할 수도 있습니다.

## <a name="configure-your-local-environment"></a>로컬 환경 구성

최신 버전의 Windows용 Docker를 사용하면 다음 참고 자료에 설명된 것처럼 설정 방법이 간단하므로 이전보다 훨씬 쉽게 Docker 애플리케이션을 개발할 수 있습니다.

> [!TIP]
> Windows용 Docker 설치 방법에 대한 자세한 내용은 <https://docs.docker.com/docker-for-windows/>를 참조하세요.

## <a name="docker-support-in-visual-studio-2017"></a>Visual Studio 2017의 Docker 지원

두 가지 수준의 Docker 지원을 프로젝트에 추가할 수 있습니다. ASP.NET Core 프로젝트에서는 Docker 지원을 설정하여 `Dockerfile` 파일을 프로젝트에 추가할 수 있습니다. 그 다음 수준은 솔루션 수준에서 `Dockerfile`을 프로젝트에 추가하고(없는 경우) `docker-compose.yml` 파일을 추가하는 컨테이너 오케스트레이션 지원입니다. Docker Compose를 통한 컨테이너 오케스트레이션 지원은 Visual Studio 2017 버전 15.0~15.7에서 기본적으로 추가됩니다. 컨테이너 오케스트레이션 지원은 Visual Studio 2017 버전 15.8 이상에서 제공하는 옵트인 기능입니다. 버전 15.8 이상에서는 Docker Compose 및 Service Fabric을 지원합니다.

**추가 > Docker 지원** 및 **추가 > 컨테이너 오케스트레이터 지원** 명령은 그림 4-31처럼 **솔루션 탐색기**에서 ASP.NET Core 프로젝트의 프로젝트 노드를 오른쪽 단추로 클릭하면 나타나는 메뉴(또는 팝업 메뉴)에 있습니다.

![Visual Studio에서 Docker 지원 메뉴 옵션 추가](./media/add-docker-support-menu.png)

**그림 4-31**. Visual Studio 2017 프로젝트에 Docker 지원 추가

### <a name="add-docker-support"></a>Docker 지원 추가

**솔루션 탐색기**에서 **추가** > **Docker 지원**을 선택하여 기존 ASP.NET Core 프로젝트에 Docker 지원을 추가할 수 있습니다. 프로젝트를 만드는 동안 그림 4-32처럼 **새 프로젝트**에서 **확인**을 클릭하면 열리는 **새 ASP.NET Core 웹 애플리케이션** 대화 상자에서 **Docker 지원 사용**을 선택하여 Docker를 지원할 수 있습니다.

![Visual Studio에서 새 ASP.NET Core 웹앱에 Docker 지원 사용](./media/enable-docker-support-visual-studio.png)

**그림 4-32**. Visual Studio 2017에서 프로젝트를 만드는 동안 Docker 지원을 사용하도록 설정

Docker 지원을 추가하거나 사용하도록 설정하면 Visual Studio가 프로젝트에 *Dockerfile* 파일을 추가합니다.

> [!NOTE]
> 그림 4-33처럼 ASP.NET 프로젝트(.NET Core가 아닌 .NET Framework 프로젝트)에 사용할 프로젝트를 만드는 동안 Docker Compose 지원을 사용하도록 설정하면 컨테이너 오케스트레이션 지원도 추가됩니다.

![ASP.NET 프로젝트에 Docker Compose 지원 사용](media/enable-docker-compose-support.png)

**그림 4-33**. Visual Studio 2017에서 ASP.NET 프로젝트에 Docker Compose 지원 사용

### <a name="add-container-orchestration-support"></a>컨테이너 오케스트레이션 지원 추가

다중 컨테이너 솔루션을 작성하려면 프로젝트에 컨테이너 오케스트레이션 지원을 추가합니다. 이렇게 하면 동일한 *docker-compose.yml* 파일에 정의된 컨테이너 그룹(전체 솔루션)을 동시에 실행하고 디버그할 수 있습니다.

컨테이너 오케스트레이션 지원을 추가하려면 **솔루션 탐색기**에서 솔루션 또는 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **추가 > 컨테이너 오케스트레이션 지원**을 선택합니다. 그런 다음, 컨테이너를 관리할 **Docker Compose** 또는 **Service Fabric**을 선택합니다.

프로젝트에 컨테이너 오케스트레이션 지원을 추가한 후에는 그림 4-34처럼 **솔루션 탐색기**에서 Dockerfile이 프로젝트에 추가되고 **docker-compose** 폴더가 솔루션에 추가된 것을 볼 수 있습니다.

![Visual Studio의 솔루션 탐색기 내의 Docker 파일](media/docker-support-solution-explorer.png)

**그림 4-34**. Visual Studio 2017 솔루션 탐색기의 Docker 파일

*docker-compose.yml*이 이미 있는 경우에는 Visual Studio에서 이 파일에 필수 구성 코드 줄을 추가합니다.

## <a name="configure-docker-tools"></a>Docker 도구 구성

주 메뉴에서 **도구 > 옵션**을 선택하고, **컨테이너 도구 > 설정**을 확장합니다. 그러면 컨테이너 도구 설정이 표시됩니다.

![다음을 보여주는 Visual Studio Docker 도구 옵션: 프로젝트 로드 시 필요한 Docker 이미지를 자동으로 끌어오기, 백그라운드에서 자동으로 컨테이너 시작, 솔루션이 닫히면 자동으로 컨테이너 종료, 신뢰할 수 있는 SSL 인증서에는 메시지를 표시하지 않기](./media/visual-studio-docker-tools-options.png)

**그림 4-35**. Docker 도구 옵션

다음 표는 이러한 옵션을 설정하는 방법을 결정하는 데 도움이 될 수 있습니다.

| name | 기본 설정 | 적용 대상 | 설명 |
| -----|:---------------:|:----------:| ----------- |
| 프로젝트 로드 시 필요한 Docker 이미지를 자동으로 끌어오기 | 켜기 | Docker Compose | 프로젝트를 로드할 때 성능을 향상하기 위해 Visual Studio는 백그라운드에서 Docker 끌어오기 작업을 수행합니다. 이렇게 하면 코드를 실행할 준비가 되었을 때 이미지가 이미 다운로드되어 있거나 다운로드 중입니다. 단순히 프로젝트를 로드하고 코드를 검색하려는 경우에는 불필요한 컨테이너 이미지를 다운로드하지 않도록 이 기능을 끄면 됩니다. |
| 백그라운드에서 자동으로 컨테이너 시작 | 켜기 | Docker Compose | 마찬가지로 성능을 향상하기 위해 Visual Studio는 개발자가 컨테이너를 빌드하고 실행할 때 볼륨 탑재가 완료된 컨테이너를 만듭니다. 컨테이너를 만드는 시기를 제어하려면 이 기능을 끕니다. |
| 솔루션이 닫히면 자동으로 컨테이너 종료 | 켜기 | Docker Compose | 솔루션을 닫거나 Visual Studio를 닫은 후에도 솔루션의 컨테이너를 계속 실행하려면 이 기능을 끕니다. |
| 신뢰할 수 있는 localhost SSL 인증서에는 메시지를 표시하지 않기 | 끄기 | ASP.NET Core 2.2 프로젝트 | localhost SSL 인증서를 신뢰할 수 없는 경우 이 확인란을 선택하지 않으면 프로젝트를 실행할 때마다 Visual Studio가 메시지를 표시합니다. |

> [!WARNING]
> localhost SSL 인증서를 신뢰할 수 없고 메시지를 표시하지 않는 확인란을 선택하면 런타임에 앱 또는 서비스에서 HTTPS 웹 요청이 실패할 수 있습니다. 이 경우 **메시지 표시 안 함** 확인란을 선택 취소하고, 프롬프트에서 신뢰를 표시합니다.

> [!TIP]
> 서비스 구현 및 Visual Studio Tools for Docker 사용에 대한 자세한 내용은 다음 문서를 참조하세요.
>
>로컬 Docker 컨테이너에서 앱 디버깅: <https://docs.microsoft.com/azure/vs-azure-tools-docker-edit-and-refresh>
>
>Visual Studio를 사용하여 컨테이너 레지스트리에 ASP.NET 컨테이너 배포: <https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker>

>[!div class="step-by-step"]
>[이전](docker-apps-inner-loop-workflow.md)
>[다음](set-up-windows-containers-with-powershell.md)
