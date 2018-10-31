---
title: Docker란?
description: Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 응용 프로그램 수명 주기
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/21/2017
ms.openlocfilehash: 056fb613c078cc407380060dc11890406ac8cffd
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197680"
---
# <a name="what-is-docker"></a>Docker란?

[Docker](https://www.docker.com/) 되는 [오픈 소스 프로젝트](https://github.com/docker/docker) 클라우드 또는 온-프레미스에서 실행할 수 있는 자체 충족 적 이동식 컨테이너를 응용 프로그램 배포를 자동화 하는 것에 대 한 (참조 그림 1-2). Docker 이기도 한 [회사](https://www.docker.com/) 장려 하 고이 기술은 클라우드, Linux 및 Windows 공급 업체를 비롯 하 여 Microsoft와 공동 작업에서 작업을 개발 합니다.

![](./media/image2.png)

그림 1-2: Docker 하이브리드 클라우드의 모든 계층에서 컨테이너를 배포 합니다.

Docker 이미지 컨테이너는 Linux 및 Windows에서 기본적으로 실행할 수 있습니다. 그러나 Windows 이미지 Windows 호스트 에서만 실행할 수 있으며 Linux 이미지는 Linux 호스트, 즉 호스트 서버 또는 VM에만 실행할 수 있습니다.

개발자는 Windows, Linux 또는 macOS에서 개발 환경을 사용할 수 있습니다. 개발 컴퓨터의 개발자는 docker 이미지가 배포 된 앱 및 해당 종속성을 포함 하 여 Docker 호스트를 실행 합니다. Linux 또는 Mac에서 작업하는 개발자는 Linux 기반의 Docker 호스트를 사용하고 Linux 컨테이너용 이미지만 만들 수 있습니다. (Mac에서 작업 하는 개발자 코드를 편집 하거나 Docker 명령줄 인터페이스를 실행할 수 있습니다 \[CLI\] 컨테이너 macOS에서 하지만이 문서의 작성 시점 현재, macOS에서 직접 실행 되지 않습니다.) Windows에서 작업하는 개발자는 Linux 또는 Windows 컨테이너용 이미지를 만들 수 있습니다.

개발 환경에서 컨테이너를 호스트하고 추가 개발자 도구를 제공하기 위해 Docker는 Windows 또는 macOS용 [Docker CE(Community Edition)](https://www.docker.com/community-edition)를 제공합니다. 이러한 제품은 컨테이너를 호스트하는 데 필요한 VM(Docker 호스트)을 설치합니다. Docker는 기업 개발용으로 설계되고 프로덕션 환경에서 대규모의 업무상 중요한 응용 프로그램을 빌드, 제공 및 실행하는 IT 팀에서 사용되는 [Docker EE(Enterprise Edition)](https://www.docker.com/enterprise-edition)도 제공합니다.

[Windows 컨테이너](/virtualization/windowscontainers/about/)를 실행하기 위해 다음 두 가지 유형의 런타임이 있습니다.

-   **Windows Server 컨테이너** 이 런타임 프로세스 및 네임 스페이스 격리 기술을 통해 응용 프로그램 격리를 제공 합니다. Windows Server 컨테이너는 컨테이너 호스트와 호스트에서 실행 중인 모든 컨테이너와 커널을 공유합니다.

-   **Hyper-v 컨테이너** 이 각 컨테이너를 고도로 최적화 된 VM에서 실행 하 여 Windows Server 컨테이너에서 제공 하는 격리를 확장 합니다. 이 구성에서 컨테이너 호스트의 커널은 Hyper-V 컨테이너와 공유되지 않으므로 격리 기능이 향상됩니다.

이러한 컨테이너 이미지를 동일한 방식으로 생성 되 고 동일 하 게 작동 합니다. 차이점은 컨테이너 이미지에서 만들어지는 방법을-Hyper-v 컨테이너를 실행에 추가 매개 변수가 필요 합니다. 자세한 내용은 [Hyper-V 컨테이너](/virtualization/windowscontainers/about/)를 참조하세요.

## <a name="comparing-docker-containers-with-vms"></a>Vm 사용 하 여 Docker 컨테이너 비교

그림 1-3 Vm과 Docker 비교를 보여 줍니다. 컨테이너입니다.

컨테이너는 훨씬 더 적은 리소스가 필요 하기 때문에 (예를 들어 필요가 없습니다 전체 OS)를 쉽게 배포할 수 있으며 빠른 시작 합니다. 이렇게 하면 더 높은 밀도 줄여 비용 동일한 하드웨어 단위에서 더 많은 서비스를 실행할 수 있습니다 의미 있을 수 있습니다.

동일한 커널에서 실행의 부작용을으로 Vm 보다는 격리가 덜 얻을 수 있습니다.

이미지의 주요 목표는 서로 다른 배포에서 환경(종속성)을 동일하게 만드는 것입니다. 즉, 컴퓨터에서 이를 디버그한 다음, 동일한 환경의 다른 컴퓨터에 배포할 수 있습니다.

컨테이너 이미지는 앱 또는 서비스를 패키지 하 고 안정적이 고 재현 가능한 방식으로 배포 하는 방법을 합니다. 이러한 점에서 Docker는 기술만 아닙니다, 그리고 그리고 개념 및 프로세스입니다.

Docker를 사용 하는 경우 예를 들어 개발자를 들에서는 "작동 내 컴퓨터에서 없습니까 프로덕션 환경에서?" 단순히 말할 수, "Docker에서 실행" 모든 지원 되는 Docker 환경에서 패키지에 포함 된 Docker 응용 프로그램을 실행할 수 있습니다 하 고 모든 배포 대상 (개발, QA, 스테이징, 프로덕션 등.)에서 원래 방식으로 실행 됩니다.

![](./media/image3.png)

그림 1-3: 기존 Vm Docker 컨테이너 비교


>[!div class="step-by-step"]
[이전](index.md)
[다음](docker-terminology.md)
