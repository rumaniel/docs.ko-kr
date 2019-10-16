---
title: Docker 앱을 위한 개발 환경
description: Docker 개발 수명 주기를 지원하는 가장 중요한 개발 도구 옵션을 알아봅니다.
ms.date: 02/15/2019
ms.openlocfilehash: 35236e75f47e830d0970ca9cfd074d9a69e6f85c
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214295"
---
# <a name="development-environment-for-docker-apps"></a>Docker 앱을 위한 개발 환경

## <a name="development-tools-choices-ide-or-editor"></a>개발 도구 선택: IDE 또는 편집기

개발자가 완전하고 강력한 IDE를 선호하든 아니면 가볍고 민첩한 편집기를 선호하든, Microsoft에서는 Docker 애플리케이션 개발에 필요한 모든 것을 제공해 드립니다.

### <a name="visual-studio-code-and-docker-cli-cross-platform-tools-for-mac-linux-and-windows"></a>Visual Studio Code 및 dotnet CLI(Mac, Linux 및 Windows용 플랫폼 간 도구)

모든 개발 언어를 지원하는 가벼운 플랫폼 간 편집기를 선호하는 경우 Visual Studio Code 및 Docker CLI를 사용하면 됩니다. 이러한 제품은 개발자 워크플로를 간소화하는 데 필요한 간단하면서도 강력한 환경을 제공합니다. "Mac용 Docker" 또는 "Windows용 Docker"(개발 환경)를 설치하면 Docker 개발자는 단일 Docker CLI를 사용하여 Windows 또는 Linux용 앱(런타임 환경)을 모두 빌드할 수 있습니다. 뿐만 아니라 Visual Studio Code는 Dockerfile용 IntelliSense가 포함된 Docker용 확장 및 편집기에서 Docker 명령을 실행하는 바로 가기 작업을 지원합니다.

> [!NOTE]
> Visual Studio Code를 다운로드하려면 <https://code.visualstudio.com/download>로 이동합니다.
>
> Mac 및 Windows용 Docker를 다운로드하려면 <https://www.docker.com/products/docker>로 이동합니다.

### <a name="visual-studio-with-docker-tools-windows-development-machine"></a>Docker 도구가 포함된 Visual Studio(Windows 개발 머신)

기본 제공 Docker 도구를 사용하도록 설정된 Visual Studio 2017(이상)을 사용하는 것이 좋습니다. Visual Studio가 있으면 원하는 Docker 환경에서 직접 애플리케이션을 개발하고, 실행하고, 유효성을 검사할 수 있습니다. F5 키를 눌러 Docker 호스트에서 직접 애플리케이션(단일 컨테이너 또는 여러 컨테이너)을 디버그하거나, Ctrl+F5 키를 눌러 컨테이너를 다시 빌드하지 않고 앱을 편집하고 새로 고칠 수 있습니다. 이 방법은 Windows 개발자가 Linux 또는 Windows용 Docker 컨테이너를 만들 수 있는 가장 간단하면서도 강력한 옵션입니다.

### <a name="visual-studio-for-mac-mac-development-machine"></a>Mac용 Visual Studio(Mac 개발 머신)

Docker 기반 애플리케이션을 개발할 때 [Mac용 Visual Studio](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)를 사용할 수 있습니다. Mac용 Visual Studio는 Mac용 Visual Studio Code에 비해 풍부한 IDE를 제공합니다.

## <a name="language-and-framework-choices"></a>언어 및 프레임워크 선택

Microsoft 도구를 사용하여 가장 최신 언어로 Docker 애플리케이션을 개발할 수 있습니다. 다음은 초기 목록이지만, 이 목록으로 제한되지는 않습니다.

- .NET Core 및 ASP.NET Core
- Node.js
- 이동
- Java
- Ruby
- Python

기본적으로 Linux 또는 Windows에서 Docker가 지원하는 모든 최신 언어를 사용할 수 있습니다.

>[!div class="step-by-step"]
>[이전](deploy-azure-kubernetes-service.md)
>[다음](docker-apps-inner-loop-workflow.md)
