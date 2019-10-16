---
title: 기존 .NET 앱을 Windows 컨테이너로 배포
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | 기존 .NET 앱을 Windows 컨테이너로 배포
ms.date: 04/29/2018
ms.openlocfilehash: 997b32e51272be2126bd824de1f8f026d77ca203
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72318623"
---
# <a name="deploy-existing-net-apps-as-windows-containers"></a>기존 .NET 앱을 Windows 컨테이너로 배포

Windows 컨테이너를 기반으로 하는 배포는 클라우드에 최적화된 응용 프로그램과 클라우드 네이티브 응용 프로그램에 적용할 수 있습니다.

그러나 이 가이드와 특히 다음 절에서는 응용 프로그램을 재설계하지 않아도 되는 *클라우드에 최적화*된 응용 프로그램에 대한 Windows 컨테이너 사용을 중점적으로 설명합니다.

## <a name="what-are-containers-linux-or-windows"></a>컨테이너 란? (Linux 또는 Windows)

컨테이너는 응용 프로그램을 격리된 자체 패키지로 마무리하는 방법입니다. 해당 컨테이너에서 응용 프로그램은 컨테이너 외부에 있는 응용 프로그램 또는 프로세스의 영향을 받지 않습니다. 응용 프로그램이 하나의 프로세스로 성공적으로 실행되는 데 의존하는 모든 것이 컨테이너 내부에 있습니다. 컨테이너가 이동할 수 있는 곳이라면, 직접 종속성 측면에서 응용 프로그램의 요구사항이 충족됩니다.실행에 필요한 모든 항목(라이브러리 종속성, 런타임 등)이 함께 번들되기 때문입니다.

컨테이너의 주요 특징은 컨테이너가 필요한 모든 종속성과 함께 제공 되므로 다른 배포에서 환경을 동일 하 게 만드는 것입니다. 컴퓨터에서 응용 프로그램을 디버깅 한 다음 동일한 환경을 보장 하 여 다른 컴퓨터에 배포할 수 있습니다.

컨테이너는 컨테이너 이미지의 인스턴스입니다. 컨테이너 이미지는 앱 또는 서비스 (예: 스냅숏)를 패키지 한 다음 신뢰할 수 있고 재현 가능한 방식으로 배포 하는 방법입니다. Docker는 기술 뿐만 아니라 철학 및 프로세스 이기도 하다는 것을 나타낼 수 있습니다.

컨테이너는 매일 더 보편화 되 고 있으므로 업계 전체의 "배포 단위"가 됩니다.

## <a name="benefits-of-containers-docker-engine-on-linux-or-windows"></a>컨테이너의 이점 (Linux 또는 Windows의 Docker 엔진)

컨테이너를 사용 하 여 응용 프로그램 빌드-간단한 빌딩 블록으로 정의 될 수도 있음-모든 인프라에서 응용 프로그램을 빌드, 배송 및 실행 하는 민첩성을 크게 향상 시킵니다.

컨테이너를 사용 하면 Microsoft 개발자 도구, 운영 체제 및 클라우드 전반에서 Docker 통합 덕분에 코드를 거의 또는 전혀 변경 하지 않고 개발 환경에서 프로덕션 환경으로 앱을 만들 수 있습니다.

일반 Vm에 배포 하는 경우 ASP.NET apps를 Vm에 배포 하는 방법이 이미 준비 되어 있을 것입니다. 그러나 사용자의 메서드는 퍼핏와 같은 배포 도구나 유사한 도구를 사용 하 여 여러 수동 단계 또는 복잡 한 자동화 된 프로세스를 포함 하는 것일 수 있습니다. 구성 항목 수정, 서버 간에 응용 프로그램 콘텐츠 복사, .msi 설정에 따라 대화형 설치 프로그램 실행, 테스트 후와 같은 작업을 수행 해야 할 수 있습니다. 배포의 이러한 모든 단계는 배포에 시간 및 위험을 추가 합니다. 종속성이 대상 환경에 없는 경우에는 오류가 발생 합니다.

Windows 컨테이너에서 응용 프로그램 패키징 프로세스는 완전히 자동화 되어 있습니다. Windows 컨테이너는 컨테이너 배포에 대 한 자동 업데이트 및 롤백을 제공 하는 Docker 플랫폼을 기반으로 합니다. Docker 엔진을 사용 하 여 얻을 수 있는 주요 개선 사항은 응용 프로그램의 스냅숏과 비슷하며 모든 종속 항목을 포함 하는 이미지를 만드는 것입니다. 이미지는 Docker 이미지 (이 경우 Windows 컨테이너 이미지)입니다. 이미지는 소스 코드로 다시 이동 하지 않고 컨테이너에서 ASP.NET apps를 실행 합니다. 컨테이너 스냅숏은 배포 단위가 됩니다.

많은 조직에서 다음과 같은 이유로 기존 모놀리식 응용 프로그램을 컨테이너 화 하 고 있습니다.

- **향상 된 배포를 통해 민첩성을 해제**합니다. 컨테이너는 개발과 작업 간에 일관 된 배포 계약을 제공 합니다. 컨테이너를 사용 하는 경우 개발자는 "내 컴퓨터에서 작동 하 고, 프로덕션 환경에서 작동 하지 않는 이유는 무엇 인가요?" 라고 표시 됩니다. "이는 컨테이너로 실행 되므로 프로덕션 환경에서 실행 됩니다." 라고 표시 될 수 있습니다. 모든 종속성을 포함 하는 패키지 된 응용 프로그램은 지원 되는 모든 컨테이너 기반 환경에서 실행할 수 있습니다. 모든 배포 대상 (개발, QA, 스테이징, 프로덕션)에서 실행 되는 것과 같은 방식으로 실행 됩니다. 컨테이너는 한 단계에서 다음 단계로 이동할 때 대부분의 마찰을 제거 하 여 배포를 크게 개선 하 고 더 빠르게 제공할 수 있습니다.

- **비용 절감**. 컨테이너는 기존 하드웨어를 통합 및 제거 하거나 하드웨어 단위당 더 높은 밀도에서 응용 프로그램을 실행 하 여 비용을 절감할 수 있습니다.

- **이식성**. 컨테이너는 모듈형 이며 이식 가능 합니다. Docker 컨테이너는 모든 서버 운영 체제 (Linux 및 Windows), 모든 주요 공용 클라우드 (Microsoft Azure, Amazon AWS, Google, IBM) 및 온-프레미스 및 사설 또는 하이브리드 클라우드 환경에서 지원 됩니다.

- **제어**. 컨테이너는 컨테이너 수준에서 제어 되는 유연 하 고 안전한 환경을 제공 합니다. 컨테이너에서 실행 제약 조건 정책을 설정 하 여 컨테이너의 보안을 유지 하 고 격리 하 고 제한할 수 있습니다. Windows 컨테이너에 대 한 섹션에 설명 된 대로 Windows Server 2016 및 Hyper-v 컨테이너는 추가 엔터프라이즈 지원 옵션을 제공 합니다.

응용 프로그램을 개발 하 고 유지 관리 하기 위해 컨테이너를 사용 하는 경우 민첩성, 이식성 및 제어 기능이 크게 향상 되었습니다.

## <a name="what-is-docker"></a>Docker란?

[Docker](https://www.docker.com/) 는 응용 프로그램의 배포를 클라우드 또는 온-프레미스에서 실행할 수 있는, 자신에 게 적합 한 휴대용 컨테이너로 자동화 하는 [오픈 소스 프로젝트](https://github.com/docker/docker) 입니다. Docker는 이 기술을 장려하고 발전시키는 [회사](https://www.docker.com/)이기도 합니다. 이 회사는 Microsoft를 비롯 한 클라우드, Linux 및 Windows 공급 업체와 협력 하 여 작업 합니다.

![Docker가 하이브리드 클라우드에서 컨테이너를 배포 하는 방법을 보여 주는 다이어그램입니다.](./media/deploy-existing-net-apps-as-windows-containers/docker-deploys-containers-all-layers.png)

**그림 4-6.** Docker는 하이브리드 클라우드의 모든 계층에서 컨테이너를 배포

가상 컴퓨터에 익숙한 사용자에 게 컨테이너가 매우 유사한 것으로 보일 수 있습니다. 컨테이너는 운영 체제를 실행 하 고, 파일 시스템을 포함 하며, 실제 또는 가상 컴퓨터 시스템과 마찬가지로 네트워크를 통해 액세스할 수 있습니다. 그러나 컨테이너 뒤의 기술 및 개념은 가상 머신과 크게 다릅니다. 개발자 관점에서 볼 때 컨테이너는 단일 프로세스와 유사 하 게 처리 되어야 합니다. 실제로 컨테이너에는 한 프로세스에 대 한 단일 진입점이 있습니다.

Docker 컨테이너 (간단한 *컨테이너*)는 Linux 및 Windows에서 기본적으로 실행할 수 있습니다. 일반 컨테이너를 실행 하는 경우 Windows 컨테이너는 Windows 호스트 (호스트 서버 또는 VM) 에서만 실행할 수 있고 Linux 컨테이너는 Linux 호스트 에서만 실행할 수 있습니다. 그러나 최신 버전의 Windows Server 및 Hyper-v 컨테이너에서 Linux 컨테이너는 현재 Windows server 컨테이너 에서만 제공 되는 Hyper-v 격리 기술을 사용 하 여 Windows Server에서 기본적으로 실행할 수 있습니다.

가까운 장래에 Linux 및 Windows 컨테이너를 모두 포함 하는 혼합 된 환경도 가능 하 고 널리 사용할 수 있습니다.

## <a name="benefits-of-windows-containers-for-your-existing-net-applications"></a>기존 .NET 응용 프로그램에 대 한 Windows 컨테이너의 이점

Windows 컨테이너를 사용 하는 경우의 이점은 일반적으로 컨테이너에서 얻을 수 있는 것과 같은 이점이 있습니다. Windows 컨테이너를 사용 하는 것은 민첩성, 이식성 및 제어를 크게 개선 하는 것입니다.

기존 .NET 응용 프로그램은 .NET Framework를 사용 하 여 만든 응용 프로그램을 참조 합니다. 예를 들어 기존 ASP.NET 웹 응용 프로그램 일 수 있습니다. .NET Core를 사용 하지 않습니다. .NET Core는 최신 버전 이며 Linux, Windows 및 MacOS에서 플랫폼 간으로 실행 됩니다.

.NET Framework의 주요 종속성은 Windows입니다. 또한 IIS와 같은 보조 종속성과 기존 ASP.NET의 System.web이 있습니다.

.NET Framework 응용 프로그램은 Windows, 기간에 실행 해야 합니다. 기존 .NET Framework 응용 프로그램을 컨테이너 화 하 고 .NET Core로의 마이그레이션에 투자 하지 않으려는 경우 ("제대로 작동 하는 경우 마이그레이션하지 마세요"), 컨테이너에 대 한 유일한 선택은 Windows 컨테이너를 사용 하는 것입니다.

따라서 windows 컨테이너의 주요 이점 중 하나는 Windows에서 컨테이너 화를 실행 하는 기존 .NET Framework 응용 프로그램을 현대화 하는 방법을 제공 한다는 것입니다. 궁극적으로 Windows 컨테이너는 컨테이너를 사용 하 여 민첩성, 이식성 및 향상 된 제어를 사용 하 여 원하는 혜택을 얻을 수 있습니다.

## <a name="choose-an-os-to-target-with-net-based-containers"></a>대상으로 할 OS를 선택 합니다. 네트워크 기반 컨테이너

Docker에서 지원 되는 운영 체제의 다양성 뿐만 아니라 .NET Framework와 .NET Core 간의 차이점을 감안 하 여 사용 하는 프레임 워크에 따라 특정 OS 및 특정 버전을 대상으로 지정 해야 합니다.

Windows의 경우 Windows Server Core 또는 Windows Nano Server를 사용할 수 있습니다. 이러한 Windows 버전은 .NET Framework 또는 .NET Core 응용 프로그램에 필요할 수 있는 다양 한 특성 (예: Kestrel과 같은 자체 호스팅 웹 서버)을 제공 합니다.

Linux의 경우 공식 .NET Docker 이미지(예: Debian)에서 여러 배포판을 제공합니다.

그림 4-7은 앱의 .NET Framework 버전에 따라 대상으로 지정할 수 있는 OS 버전을 보여 줍니다.

![.NET Framework 버전에 따라 대상으로 할 OS를 보여 주는 다이어그램입니다.](./media/deploy-existing-net-apps-as-windows-containers/dotnet-framework-operating-systems.png)

**그림 4-7.** .NET Framework 버전에 따라 대상으로 하는 운영 체제

.NET Framework 응용 프로그램을 기반으로 하는 기존 또는 레거시 응용 프로그램에 대 한 마이그레이션 시나리오에서 주요 종속성은 Windows 및 IIS에 있습니다. 유일한 옵션은 Windows Server Core 및 .NET Framework 기반으로 Docker 이미지를 사용 하는 것입니다.

Dockerfile 파일에 이미지 이름을 추가할 때 .NET Framework 기반 Windows 컨테이너 이미지에 대 한 다음 예제와 같이 태그를 사용 하 여 운영 체제 및 버전을 선택할 수 있습니다.

> | **태그가** | **시스템 및 버전** |
> |---|---|
> | **microsoft/dotnet-framework:4.x-windowsservercore** | Windows Server Core의 .NET Framework 4.x |
> | **microsoft/aspnet:4.x-windowsservercore** | Windows Server Core에서 추가 ASP.NET 사용자 지정을 포함 한 .NET Framework 4.x |

.NET Core (Linux 및 Windows 용 플랫폼 간)의 경우 태그는 다음과 같습니다.

> | **태그가** | **시스템 및 버전**
> |---|---|
> | **microsoft/dotnet:2.0.0-runtime** | Linux의 .NET Core 2.0 런타임 전용 |
> | **microsoft/dotnet:2.0.0-runtime-nanoserver** | Windows Nano Server의 .NET Core 2.0 런타임 전용 |

### <a name="multi-arch-images"></a>다중 아키텍처 이미지

중부-2017부터 [다중 아키텍처](https://github.com/moby/moby/issues/15866) 이미지 라는 Docker의 새 기능을 사용할 수도 있습니다. .NET Core Docker 이미지는 다중 아키텍처 태그를 사용할 수 있습니다. Dockerfile 파일은 대상으로 하는 운영 체제를 더 이상 정의할 필요가 없습니다. 다중 아키텍처 기능을 사용 하면 여러 컴퓨터 구성에서 단일 태그를 사용할 수 있습니다. 예를 들어 다중 아치를 사용 하는 경우 하나의 공통 태그 ( **microsoft/dotnet: 2.0.0 런타임)** 를 사용할 수 있습니다. Linux 컨테이너 환경에서 해당 태그를 가져오는 경우 Debian 기반 이미지가 표시 됩니다. Windows 컨테이너 환경에서 해당 태그를 가져오는 경우 Nano 서버 기반 이미지가 표시 됩니다.

.NET Framework 이미지의 경우 기존 .NET Framework는 Windows만 지원 하기 때문에 다중 아키텍처 기능을 사용할 수 없습니다.

## <a name="windows-container-types"></a>Windows 컨테이너 형식

Linux 컨테이너와 마찬가지로, Windows Server 컨테이너는 Docker 엔진을 사용 하 여 관리 됩니다. Linux 컨테이너와 달리 Windows 컨테이너에는 Windows Server 컨테이너 및 Hyper-v 격리의 두 가지 컨테이너 유형 또는 실행 시간이 포함 됩니다.

**Windows Server 컨테이너**: 프로세스 및 네임 스페이스 격리 기술을 통해 응용 프로그램 격리를 제공 합니다. Windows Server 컨테이너는 컨테이너 호스트와 호스트에서 실행 되는 모든 컨테이너와 커널을 공유 합니다. 이러한 컨테이너는 악의적인 보안 경계를 제공 하지 않으므로 신뢰할 수 없는 코드를 분리 하는 데 사용 하면 안 됩니다. 공유 커널 공간 때문에 이러한 컨테이너에는 동일한 커널 버전 및 구성이 필요 합니다.

**Hyper-v 격리**: 는 최적화 된 VM에서 각 컨테이너를 실행 하 여 Windows Server 컨테이너에서 제공 하는 격리를 확장 합니다. 이 구성에서 컨테이너 호스트의 커널은 동일한 호스트의 다른 컨테이너와 공유 되지 않습니다. 이러한 컨테이너는 악의적인 다중 테 넌 트 호스팅을 위해 설계 되었으며, VM의 보안 보증은 동일 합니다. 이러한 컨테이너는 호스트 또는 호스트의 다른 컨테이너와 커널을 공유 하지 않기 때문에 서로 다른 버전 및 구성을 사용 하 여 커널을 실행할 수 있습니다 (지원 되는 버전 포함). 예를 들어 windows 10의 모든 Windows 컨테이너는 Hyper-v 격리를 사용 하 여 Windows Server 커널 버전 및 구성을 활용 합니다.

Hyper-v 격리를 사용 하거나 사용 하지 않고 Windows에서 컨테이너를 실행 하는 것은 런타임 결정입니다. 처음에 Hyper-v 격리를 사용 하 여 컨테이너를 만들도록 선택 하 고 런타임에 Windows Server 컨테이너로 실행 하도록 선택할 수 있습니다.

### <a name="additional-resources"></a>추가 자료

- **Windows 컨테이너 설명서**

    <https://docs.microsoft.com/virtualization/windowscontainers/>

- **Windows 컨테이너 기본 사항**

    <https://docs.microsoft.com/virtualization/windowscontainers/about/>

- **Infographic: Microsoft 및 컨테이너 @ no__t-0

    <https://info.microsoft.com/rs/157-GQE-382/images/Container%20infographic%201.4.17.pdf>

## <a name="the-container-ecosystem-in-azure"></a>Azure의 컨테이너 에코 시스템

이전 섹션에서는 Docker 컨테이너의 이점 및 .NET 응용 프로그램의 특정 컨테이너 이미지에 대 한 세부 정보를 설명 했습니다. 응용 프로그램을 개발 하거나 컨테이너 화 하기 위해 모든 일반 정보는 기본입니다.
그러나 프로덕션 배포 환경이 나 QA 및 개발/테스트 Microsoft Azure 환경에 대해 생각 하는 경우에는 클라우드에서 전체 컨테이너 에코 시스템 (아래 다이어그램에 표시)을 다양 하 게 제공 하는 다양 한 옵션을 제공 합니다. 특정 응용 프로그램의 요구 사항에 따라 하나 또는 다른 Azure 제품을 선택 해야 합니다.

![Azure의 컨테이너 에코 시스템 다이어그램](./media/deploy-existing-net-apps-as-windows-containers/azure-container-ecosystem.png)

**그림 4-7.5** Azure의 컨테이너 에코 시스템

Azure의 컨테이너 에코 시스템에서 인프라를 고려 하는 컨테이너를 지 원하는 다음 제품입니다.

- **Azure Container Instances (ACI)**
- **Azure Virtual Machines** (컨테이너의 지원)
- **Azure Virtual Machine Scale Sets** (컨테이너의 지원)

이 세 가지 방법으로 ACI는 기본 OS를 유지 관리 하지 않아도 되 고, 업그레이드/패치를 수행할 필요가 없으며,이 책의 이후 섹션에서 설명 하는 것 처럼 ACI는 인프라 수준으로 배치 되는 이점을 제공 합니다.

PaaS (Platform as a Service) 수준에서 동시에 배치 되는 컨테이너를 지 원하는 Azure의 제품은 다음과 같습니다.

- **Azure App Service**
- **Azure Kubernetes 서비스 (AKS 및 ACS)**
- **Azure Batch** 

그런 다음 사용자 지정 컨테이너 이미지를 등록 하 고 배포 하는 경우 모든 이전 제품에서 사용할 수 있는 Azure에서 호스트 되는 확장성이 높은 컨테이너 레지스트리를 Azure Container Registry 합니다.

또한 컨테이너에서 Azure의 다른 관리 서비스 (예: Azure SQL Database, Azure Redis cache, Azure Cosmos DB 등)를 사용할 수 있습니다. 또한 Azure 내에서 컨테이너를 사용할 수 있는 Cloud Foundry 및 OpenShift와 같은 Azure Marketplace에서 사용할 수 있는 타사 솔루션/플랫폼이 있습니다. 

다음 섹션에서는 Windows 컨테이너를 대상으로 지정 하는 경우 이러한 각 Azure 제품 및 솔루션을 사용 하는 시기에 대 한 Microsoft의 권장 사항을 살펴볼 수 있습니다.

>[!div class="step-by-step"]
>[이전](what-about-cloud-native-applications.md)
>[다음](when-not-to-deploy-to-windows-containers.md)
