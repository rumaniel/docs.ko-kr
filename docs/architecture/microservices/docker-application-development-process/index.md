---
title: Docker 기반 애플리케이션에 대한 개발 프로세스
description: Docker 기반 애플리케이션 개발 옵션을 개괄적으로 살펴봅니다. Windows용 Visual Studio, Mac용 Visual Studio 또는 여러 플랫폼(Windows, Mac, Linux)을 지원하는 Visual Studio Code를 사용합니다.
ms.date: 09/27/2018
ms.openlocfilehash: a32b27f3d98ed7ebf63b637ec0c979c22ee8e1e8
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295140"
---
# <a name="development-process-for-docker-based-applications"></a>Docker 기반 애플리케이션에 대한 개발 프로세스

*Visual Studio 및 Visual Studio Tools for Docker에 중점을 둔 IDE 또는 Docker CLI 및 Visual Studio Code에 중점을 둔 CLI/편집기 중 원하는 방식으로 컨테이너화된 .NET 애플리케이션을 개발하세요.*

## <a name="development-environment-for-docker-apps"></a>Docker 앱을 위한 개발 환경

### <a name="development-tool-choices-ide-or-editor"></a>개발 도구 선택: IDE 또는 편집기

완전하고 강력한 IDE를 선호하든지 아니면 간단하고 민첩한 편집기를 선호하든지 상관없이 Microsoft는 Docker 애플리케이션을 개발하는 데 사용할 수 있는 도구를 제공합니다.

**Visual Studio(Windows용)** . Visual Studio를 사용하여 Docker 기반 애플리케이션을 개발할 때에는 이미 기본 제공되는 Docker용 도구와 함께 제공되는 Visual Studio 2017 버전 15.7 이상을 사용하는 것이 좋습니다. Docker용 도구를 통해 대상 Docker 환경에서 직접 애플리케이션을 개발하고 실행할 수 있으며, 애플리케이션의 유효성을 검사할 수 있습니다. F5 키를 눌러 애플리케이션(단일 컨테이너 또는 여러 컨테이너)을 Docker 호스트에 직접 실행 및 디버그하거나, Ctrl+F5를 눌러 컨테이너를 다시 빌드하지 않고도 애플리케이션을 편집 및 새로 고칠 수 있습니다. 이는 Docker 기반 앱을 위한 가장 강력한 개발 옵션입니다.

**Mac용 Visual Studio.** macOS에서 실행되는 Xamarin Studio의 확장인 IDE로, 2017년 중반부터 Docker를 지원합니다. 이는 Mac 컴퓨터에서 작업 중인 개발자로, 강력한 IDE도 사용하고자 하는 경우에 권장되는 옵션입니다.

**Visual Studio Code 및 Docker CLI**. 개발 언어를 지원하는 간단한 플랫폼 간 편집기를 선호하는 경우 Microsoft VS Code(Visual Studio Code) 및 Docker CLI를 사용할 수 있습니다. 이는 Mac, Linux 및 Windows에 대한 플랫폼 간 개발 접근법입니다. 또한 Visual Studio Code는 Dockerfile용 IntelliSense와 같은 Docker용 확장을 지원하고 편집기에서 Docker 명령을 실행하는 바로 가기 작업도 지원합니다.

[Docker Desktop CE(Community Edition)](https://hub.docker.com/search/?type=edition&offering=community)를 설치하면 단일 Docker CLI를 사용하여 Windows용 앱과 Linux용 앱을 모두 빌드할 수 있습니다.

### <a name="additional-resources"></a>추가 자료

- **Visual Studio** - 공식 사이트입니다. \
  [https://visualstudio.microsoft.com/vs/](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)

- **Visual Studio Code**. 공식 사이트입니다. \
  <https://code.visualstudio.com/download>

- **Windows CE(Community Edition)를 위한 Docker Desktop** \
  [https://hub.docker.com/editions/community/docker-ce-desktop-windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
  
- **Mac CE(Community Edition)를 위한 Docker Desktop** \
  [https://hub.docker.com/editions/community/docker-ce-desktop-mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)

## <a name="net-languages-and-frameworks-for-docker-containers"></a>Docker 컨테이너를 위한 .NET 언어 및 프레임워크

이 가이드의 이전 섹션에서 언급했듯이 Docker 컨테이너화된 .NET 애플리케이션을 개발할 때 .NET Framework, .NET Core 또는 오픈 소스 Mono 프로젝트를 사용할 수 있습니다. Linux 또는 Windows 컨테이너를 대상으로 할 때 사용 중인 .NET Framework에 따라 C\#, F\# 또는 Visual Basic으로 개발할 수 있습니다. .NET 언어에 대한 자세한 내용은 블로그 게시물, [The .NET Language Strategy](https://devblogs.microsoft.com/dotnet/the-net-language-strategy/)(.NET 언어 전략)를 참조하세요.

>[!div class="step-by-step"]
>[이전](../architect-microservice-container-applications/scalable-available-multi-container-microservice-applications.md)
>[다음](docker-app-development-workflow.md)
