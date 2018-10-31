---
title: Docker 컨테이너에 대해 .NET Core를 선택할 경우
description: 컨테이너화된 .NET 응용 프로그램용 .NET 마이크로 서비스 아키텍처 | Docker 컨테이너에 대해 .NET Core를 선택할 경우
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/11/2018
ms.openlocfilehash: fa5efd3c2478965ef01efc39b57918ec2d35962a
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48873377"
---
# <a name="when-to-choose-net-core-for-docker-containers"></a>Docker 컨테이너에 대해 .NET Core를 선택할 경우

.NET Core는 모듈성 있고 가벼워 컨테이너에 완벽한 선택이 됩니다. 컨테이너를 배포 및 시작할 때 이미지 크기는 .NET Framework보다 .NET Core에서 훨씬 작습니다. 반면 .NET Framework를 컨테이너에 사용하려면 이미지가 Windows Server Core 이미지에 기반해야 하는데, .NET Core에 사용하는 Windows Nano Server 또는 Linux 이미지보다 훨씬 무겁습니다.

또한 .NET Core는 여러 플랫폼에 적용되므로 Linux나 Windows 컨테이너 이미지를 통해 서버 앱을 배포할 수 있습니다. 그러나 기존 .NET Framework를 사용하는 경우 Windows Server Core 기반의 이미지만 배포할 수 있습니다.

.NET Core를 선택하는 이유에 대한 자세한 설명은 다음과 같습니다.

## <a name="developing-and-deploying-cross-platform"></a>플랫폼 간 개발 및 배포

분명히, Docker에서 지원하는 여러 플랫폼(Linux 및 Windows)에서 실행할 수 있는 응용 프로그램(웹앱 또는 서비스)이 목표라면 .NET Core가 올바른 선택입니다. .NET Framework는 Windows만 지원하기 때문입니다.

.NET Core는 개발 플랫폼으로 macOS도 지원합니다. 그러나 Docker 호스트에 컨테이너를 배포할 때는 (현재) 호스트가 Linux 또는 Windows를 기반으로 해야 합니다. 예를 들어 개발 환경에서는 Mac에서 실행되는 Linux VM을 사용할 수 있습니다.

[Visual Studio](https://www.visualstudio.com/vs/)는 Windows를 위한 IDE(통합 개발 환경)를 제공하며 Docker 개발을 지원합니다.

[Mac용 Visual Studio](https://www.visualstudio.com/vs/visual-studio-mac/)는 Xamarin Studio에서 진화한 IDE로, macOS에서 실행되고 Docker 기반 응용 프로그램 개발을 지원합니다. 이는 Mac 컴퓨터에서 작업 중인 개발자로, 강력한 IDE도 사용하고자 하는 경우에 권장되는 옵션입니다.

또한 macOS, Linux 및 Windows에서 [Visual Studio Code](https://code.visualstudio.com/)를 사용할 수 있습니다. VS Code는 IntelliSense 및 디버깅을 포함하여 .NET Core를 지원합니다. VS Code는 가벼운 편집기이므로 Mac에서 컨테이너화된 앱을 개발할 때 Docker CLI 및 [.NET Core CLI(명령줄 인터페이스)](https://docs.microsoft.com/dotnet/core/tools/?tabs=netcore2x)와 함께 사용할 수 있습니다. Sublime, Emacs, vi 같은 대부분의 타사 편집기와 IntelliSense 지원을 제공하는 오픈 소스 OmniSharp 프로젝트에서도 .NET Core를 대상으로 지정할 수 있습니다.

IDE 및 편집기 외에도 지원되는 모든 플랫폼에 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/?tabs=netcore2x) 도구를 사용할 수 있습니다.

## <a name="using-containers-for-new-green-field-projects"></a>새("그린-필드") 프로젝트에 컨테이너 사용

컨테이너는 아키텍처 패턴을 따르는 웹앱 또는 서비스를 컨테이너화하는 데 사용할 수 있지만 일반적으로 마이크로 서비스 아키텍처와 연계하여 사용됩니다. Windows 컨테이너에 .NET Framework를 사용할 수 있지만 .NET Core는 모듈 방식이며 가볍기 때문에 컨테이너와 마이크로 서비스 아키텍처에 적합합니다. 컨테이너를만들어 배포할 때 이미지 크기는 .NET Framework보다 .NET Core에서 훨씬 작습니다.

## <a name="creating-and-deploying-microservices-on-containers"></a>컨테이너에서 마이크로 서비스 만들기 및 배포

기존 .NET Framework를 통해 일반 프로세스를 사용하여 컨테이너 없는 마이크로 서비스 기반 응용 프로그램을 구축할 수 있습니다. 이렇게 하면 .NET Framework가 이미 설치되어 프로세스 간에 공유되기 때문에 프로세스가 가볍고 신속하게 시작됩니다. 그러나 컨테이너를 사용할 경우 기존 .NET Framework의 이미지가 Windows Server Core를 기반으로 할 수 있어 컨테이너 위의 마이크로 서비스 방식에 대해서는 너무 무거워집니다.

반면 컨테이너 기반의 마이크로 서비스 중심 시스템을 포괄하려면 .NET Core가 가장 적합합니다. .NET Core는 가볍기 때문입니다. 또한 Linux 이미지나 Windows Nano 이미지 등, 관련된 컨테이너 이미지가 더 나은 선택으로, 작아서 컨테이너를 더 가볍고 신속하게 시작할 수 있습니다.

마이크로 서비스는 가능한 작아야 합니다. 즉 신속하게 가공되고 작은 공간을 사용해야 하며 경계가 지정된 컨텍스트가 적어야 하고(DDD([도메인 기반 디자인](https://en.wikipedia.org/wiki/Domain-driven_design)) 확인) 우려되는 부분이 적어야 하며 신속하게 시작 및 중지할 수 있어야 합니다. 이러한 요구 사항을 위해 .NET Core 컨테이너 이미지 같이 신속하게 인스턴스화할 수 있는 작은 이미지를 사용하고자 할 수 있습니다. 

마이크로 서비스 아키텍처를 사용하면 서비스 경계를 벗어나 여러 기술을 융합할 수 있습니다. 이렇게 하면 ode.js, Python, Java, GoLang 또는 그 밖의 기술로 개발된 다른 마이크로 서비스나 서비스와 연계 작동하는 새 마이크로 서비스를 위해 .NET Core로의 점진적 마이그레이션이 가능합니다.

## <a name="deploying-high-density-in-scalable-systems"></a>확장 가능한 시스템에서 높은 밀도의 배포

컨테이너 기반 시스템에 가장 적합한 밀도, 세분성 및 성능이 필요한 경우 .NET Core와 ASP.NET Core가 가장 좋은 옵션입니다. ASP.NET Core는 기존 .NET Framework의 ASP.NET보다 10배 빠르며 Java 서블릿, Go 및 node.js와 같이 업계에서 널리 사용되는 마이크로 서비스 기술을 이끌고 있습니다.

수백 개의 마이크로 서비스(컨테이너)를 실행하는 마이크로 서비스 아키텍처의 경우 특히 그렇습니다. Linux 또는 Windows Nano의 ASP.NET Core 이미지(.NET Core 런타임 기반)를 통해 더 적은 수의 서버나 VM으로 시스템을 실행하여 인프라 및 호스트 비용을 절감할 수 있습니다.


>[!div class="step-by-step"]
[이전](general-guidance.md)
[다음](net-framework-container-scenarios.md)
