---
title: Docker 용어
description: 컨테이너화된 .NET 애플리케이션을 위한 .NET 마이크로 서비스 아키텍처 | Docker 용어
ms.date: 01/07/2019
ms.openlocfilehash: a5f78ea0e848ef14f6b37e2d97d7546df20096c2
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72179413"
---
# <a name="docker-terminology"></a>Docker 용어

이 섹션에서는 Docker에 대해 더 자세히 알아보기 전에 익숙해져야 하는 용어 및 정의를 나열합니다. 추가 정의는 Docker에서 제공하는 광범위한 [용어](https://docs.docker.com/glossary/)를 참조하세요.

**컨테이너 이미지**: 컨테이너를 만드는 데 필요한 모든 종속성 및 정보를 포함한 패키지입니다. 이미지에는 모든 종속성(예: 프레임워크) 및 컨테이너 런타임에서 사용할 배포 및 실행 구성이 포함됩니다. 일반적으로 이미지는 컨테이너의 파일 시스템을 구성하기 위해 계층으로 서로 포개진 여러 개의 기본 이미지에서 파생됩니다. 이미지를 만들면 변경할 수 없습니다.

**Dockerfile**: Docker 이미지를 빌드하는 방법에 대한 지침을 포함하는 텍스트 파일입니다. 배치 스크립트처럼 첫째 줄에 지정된 기본 이미지에서 시작하여, 필요한 작업 환경이 완성될 때까지 지침에 따라 필요한 프로그램을 설치하고 파일을 복사합니다.

**빌드:** 해당 Dockerfile에서 제공하는 정보 및 컨텍스트에 외에도 이미지를 빌드하는 폴더의 추가 파일에 기반하여 컨테이너 이미지를 빌드하는 작업입니다. Docker **docker build** 명령을 사용하여 이미지를 빌드할 수 있습니다. 

**컨테이너**: Docker 이미지의 인스턴스입니다. 컨테이너는 단일 애플리케이션, 프로세스 또는 서비스의 실행을 나타냅니다. Docker 이미지의 콘텐츠, 실행 환경 및 명령의 표준 집합으로 구성됩니다. 서비스의 크기를 조정하는 경우 동일한 이미지에서 컨테이너의 여러 인스턴스를 만듭니다. 일괄 작업은 동일한 이미지에서 다중 컨테이너를 만들 수 있고 각 인스턴스에 다른 매개 변수를 전달합니다.

**볼륨**: 컨테이너가 사용할 수 있는 쓰기 가능한 파일 시스템을 제공합니다. 이미지는 읽기 전용이지만 대부분의 프로그램이 파일 시스템에 써야 하기 때문에 볼륨은 컨테이너 이미지의 맨 위에 쓰기 가능한 계층을 추가하여 프로그램이 쓰기 가능한 파일 시스템에 액세스할 수 있도록 합니다. 프로그램은 계층화된 파일 시스템에 액세스하는 것을 알지 못하며, 단순히 일반적인 파일 시스템입니다. 볼륨은 호스트 시스템에 있으며 Docker에 의해 관리됩니다.

**태그**: (버전 번호 또는 대상 환경에 따라) 다양한 이미지 또는 동일한 이미지의 버전을 식별할 수 있도록 표시 또는 레이블은 이미지에 적용할 수 있습니다.

**다단계 빌드**: 최종 이미지의 크기를 줄이는 데 도움이 되는 Docker 17.05 이상의 기능입니다. 일부 문장에서는 다단계 빌드를 통해 애플리케이션을 컴파일 및 게시하기 위한 SDK가 포함된 큰 기본 이미지를 사용한 후 작은 런타임 전용 기본 이미지가 포함된 게시 폴더를 사용하여 훨씬 작은 최종 이미지를 생성할 수 있습니다.

**리포지토리**: 이미지 버전을 나타내는 태그를 사용하여 이미지가 지정된 관련 Docker 이미지의 컬렉션입니다. 일부 리포지토리에는 SDK를 포함하는 이미지(무거움), 런타임(가벼움)만을 포함하는 이미지 등 특정 이미지의 여러 변형이 포함됩니다. 이러한 변형은 태그로 표시할 수 있습니다. 단일 리포지토리는 Linux 이미지 및 Windows 이미지 같은 플랫폼 변형을 포함할 수 있습니다.

**레지스트리**: 리포지토리에 대한 액세스를 제공하는 서비스입니다. 대부분의 공용 이미지에 대한 기본 레지스트리는 [Docker 허브](https://hub.docker.com/)(조직인 Docker에서 소유함)입니다. 레지스트리는 일반적으로 여러 팀의 리포지토리를 포함합니다. 회사에는 대체로 만든 이미지를 저장하고 관리하기 위한 개인 레지스트리가 있습니다. Azure Container Registry는 또 다른 예입니다.

**다중 아키텍처 이미지**: 다중 아키텍처의 경우, Docker가 실행되는 플랫폼에 따라 적절한 이미지의 선택을 간소화하는 기능입니다. 예를 들어 Dockerfile이 레지스트리에서 기본 이미지 **FROM mcr.microsoft.com/dotnet/core/sdk:2.2**를 요청하는 경우 실제로는 Docker가 실행되는 운영 체제 및 버전에 따라 **2.2-sdk-nanoserver-1709**, **2.2-sdk-nanoserver-1803**, **2.2-sdk-nanoserver-1809** 또는 **2.2-sdk-stretch**를 얻게 됩니다.

**Docker 허브**: 이미지를 업로드하고 여기에서 작업하는 공개 레지스트리입니다. Docker 허브는 Docker 이미지 호스팅, 공개 또는 개인 레지스트리, 빌드 트리거 및 웹후크, GitHub 및 Bitbucket과 통합을 제공합니다.

**Azure Container Registry**: Docker 이미지로 작업하는 공용 리소스 및 Azure의 해당 구성 요소입니다. 여기서는 Azure에서 배포에 가깝고, 액세스에 대한 제어를 제공하는 레지스트리를 제공하여 Azure Active Directory 그룹 및 권한을 사용할 수 있도록 합니다.

**DTR(Docker Trusted Registry)** : 조직의 데이터 센터 및 네트워크 내에서 유지되도록 온-프레미스에 설치될 수 있는 Docker의 Docker 레지스트리 서비스입니다. 엔터프라이즈 내에서 관리되어야 하는 개인 이미지에 유용합니다. Docker Trusted Registry는 Docker 데이터 센터 제품의 일부로 포함됩니다. 자세한 내용은 [DTR(Docker Trusted Registry)](https://docs.docker.com/docker-trusted-registry/overview/)를 참조하세요.

**Docker CE(Community Edition)** : 로컬로 컨테이너를 빌드하고, 실행하고, 테스트하는 Windows 및 macOS용 개발 도구입니다. Windows용 Docker CE는 Linux 및 Windows 컨테이너에 개발 환경을 제공합니다. Windows의 Linux Docker 호스트는 [Hyper-V](https://www.microsoft.com/cloud-platform/server-virtualization) 가상 머신을 기반으로 합니다. Windows 컨테이너에 대한 호스트는 Windows를 직접 기반으로 합니다. Mac용 Docker CE는 Apple 하이퍼바이저 및 [xhyve 하이퍼바이저](https://github.com/mist64/xhyve) 프레임워크를 기반으로 합니다. 여기서는 Mac OS X에서 Linux Docker 가상 머신을 제공합니다. Windows 및 Mac용 Docker CE는 Oracle VirtualBox를 기반으로 하는 Docker 도구 상자를 대체합니다.

**Docker EE(Enterprise Edition)** : Linux 및 Windows 개발을 위한 엔터프라이즈급 버전의 Docker 도구입니다.

**작성**: 다중 컨테이너 애플리케이션을 정의하고 실행하는 데 메타데이터를 사용하는 명령줄 도구 및 YAML 파일 형식입니다. 환경에 따라 값을 재정의할 수 있는 하나 이상의 .yml 파일을 사용하여 여러 이미지를 기반으로 하는 단일 애플리케이션을 정의합니다. 정의를 만든 후에 Docker 호스트에 이미지당 컨테이너를 만드는 단일 명령(docker-compose up)을 사용하여 전체 다중 컨테이너 애플리케이션을 배포할 수 있습니다.

**클러스터**: 애플리케이션이 클러스터 내의 여러 호스트에 걸쳐 분산된 서비스의 여러 인스턴스 크기를 조정할 수 있도록 단일 가상 Docker 호스트인 것처럼 노출된 Docker 호스트 컬렉션입니다. Docker 클러스터는 Kubernetes, Azure Service Fabric, Docker Swarm 및 Mesosphere DC/OS를 사용하여 만들 수 있습니다.

**오케스트레이터**: 클러스터 및 Docker 호스트의 관리를 간소화하는 도구입니다. 오케스트레이터를 사용하면 CLI(명령줄 인터페이스)또는 그래픽 UI를 통해 해당 이미지, 컨테이너 및 호스트를 관리할 수 있습니다. 컨테이너 네트워킹, 구성, 부하 분산, 서비스 검색, 고가용성, Docker 호스트 구성 등을 관리할 수 있습니다. 오케스트레이터는 노드 컬렉션 간에 워크로드를 실행하고, 배포하고, 크기를 조정하고. 복구하는 작업을 담당합니다. 일반적으로 오케스트레이터 제품은 출시된 다른 제품 중에서 Kubernetes 및 Azure Service Fabric과 같은 클러스터 인프라를 제공하는 동일한 제품입니다. 

>[!div class="step-by-step"]
>[이전](docker-defined.md)
>[다음](docker-containers-images-registries.md)
