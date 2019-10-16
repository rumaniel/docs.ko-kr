---
title: .NET Framework 및 애플리케이션 배포
ms.date: 03/30/2017
helpviewer_keywords:
- deploying applications [.NET Framework], packaging
- deploying applications [.NET Framework]
- deploying applications [.NET Framework], features
- deploying applications [.NET Framework], distribution
- .NET Framework, deploying
- .NET Framework application deployment
ms.assetid: 238d8284-6042-4a38-a7f6-1ee8efd719da
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f1d13c4c3e27b5af5b3c3e84995cae3df94a307d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052073"
---
# <a name="deploying-the-net-framework-and-applications"></a>.NET Framework 및 애플리케이션 배포

이 문서는 애플리케이션과 함께 .NET Framework 배포를 시작하는 데 도움이 됩니다. 대부분의 정보는 개발자, OEM 및 엔터프라이즈 관리자를 위한 것입니다. 컴퓨터에 .NET Framework를 설치하려는 사용자는 [.NET Framework 설치](../install/index.md)를 읽어야 합니다.

## <a name="key-deployment-resources"></a>주요 배포 리소스

.NET Framework 배포 및 서비스와 관련된 특정 정보는 다른 MSDN 항목의 다음 링크를 참조하세요.

**설치 및 배포**

- 일반적인 설치 관리자 및 배포 정보:

  - 설치 관리자 옵션:

    - [웹 설치 관리자](../install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)

    - [오프라인 설치 관리자](../install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)

  - 설치 모드:

    - [자동 설치](deployment-guide-for-developers.md#chaining_custom)

    - [UI 표시](deployment-guide-for-developers.md#chaining_default)

  - [.NET Framework 4.5를 설치하는 동안 시스템 다시 시작 줄이기](reducing-system-restarts.md)

  - [차단된 .NET Framework 설치 및 제거 문제 해결](../install/troubleshoot-blocked-installations-and-uninstallations.md)

- 클라이언트 애플리케이션과 함께 .NET Framework 배포(개발자용):

  - 설치 및 배포 프로젝트에 [InstallShield 사용](deployment-guide-for-developers.md#installshield-deployment)

  - [Visual Studio ClickOnce 애플리케이션 사용](deployment-guide-for-developers.md#clickonce-deployment)

  - [WiX 설치 패키지 만들기](deployment-guide-for-developers.md#wix)

  - [사용자 지정 설치 관리자 사용](deployment-guide-for-developers.md#chaining)

  - 개발자용 [추가 정보](deployment-guide-for-developers.md)

- .NET Framework 배포(OEM 및 관리자용):

  - [Windows ADK(평가 및 배포 키트)](https://go.microsoft.com/fwlink/p/?LinkId=254976)

  - [관리자 가이드](guide-for-administrators.md)

**서비스**

- 일반적인 내용은 [.NET Framework 블로그](https://go.microsoft.com/fwlink/p/?LinkId=254977)를 참조하세요.

- [버전 검색](../migration-guide/how-to-determine-which-versions-are-installed.md)

- [서비스 팩과 업데이트 검색](../migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)

## <a name="features-that-simplify-deployment"></a>배포를 간소화하는 기능

.NET Framework에서는 애플리케이션을 보다 쉽게 배포할 수 있게 해주는 다음과 같은 많은 기본 기능을 제공합니다.

- 영향을 주지 않은 애플리케이션.

     이 기능은 애플리케이션 격리를 제공하고 DLL 충돌을 제거합니다. 기본적으로 구성 요소는 다른 애플리케이션에 영향을 주지 않습니다.

- 기본적으로 전용 구성 요소.

     기본적으로 구성 요소는 애플리케이션 디렉터리에 배포되며 포함하는 애플리케이션에만 표시됩니다.

- 제어된 코드 공유.

     코드를 공유하려면 기본 동작 대신 코드를 공유할 수 있도록 명시적으로 설정해야 합니다.

- Side-by-side 버전 관리.

     구성 요소 또는 애플리케이션의 여러 버전이 동시에 존재할 수 있으며, 사용할 버전을 선택하면 공용 언어 런타임에서 버전 관리 정책을 적용합니다.

- XCOPY 배포 및 복제.

     레지스트리 항목이나 종속성 없이 자체 설명적 및 자체 포함된 구성 요소와 애플리케이션을 배포할 수 있습니다.

- 즉시 업데이트.

     관리자는 ASP.NET과 같은 호스트를 사용하여 원격 컴퓨터에서도 프로그램 Dll을 업데이트할 수 있습니다.

- Windows Installer와 통합.

     애플리케이션을 배포할 때 광고, 게시, 복구 및 요청 시 설치를 모두 사용할 수 있습니다.

- 엔터프라이즈 배포

     이 기능은 Active Directory 사용을 포함하여 소프트웨어를 쉽게 배포할 수 있게 해줍니다.

- 다운로드 및 캐시.

     증분 다운로드를 통해 다운로드가 더 작게 유지되며, 배포 영향을 최소화하기 위해 애플리케이션에서만 사용하도록 구성 요소를 격리시킬 수 있습니다.

- 부분적으로 신뢰할 수 있는 코드.

     ID가 사용자 대신 코드를 기반으로 하며 인증서 대화 상자가 나타나지 않습니다.

## <a name="packaging-and-distributing-net-framework-applications"></a>.NET Framework 애플리케이션 패키징 및 배포

.NET Framework에 대한 패키징 및 배포 정보 중 일부는 설명서의 다른 섹션에서 설명합니다. 이러한 섹션에서는 레지스트리 항목이 필요 없는 [어셈블리](../../standard/assembly/index.md)라는 자체 설명적 단위, 이름 고유성을 유지하고 이름 스푸핑을 방지하는 [강력한 이름의 어셈블리](../../standard/assembly/strong-named.md) 및 DLL 충돌과 관련된 많은 문제를 해결하는 [어셈블리 버전 관리](../../standard/assembly/versioning.md)에 대한 정보를 제공합니다. 다음 섹션에서는 .NET Framework 애플리케이션 패키징 및 배포에 대한 정보를 제공합니다.

### <a name="packaging"></a>패키지

.NET Framework는 다음과 같은 애플리케이션 패키징 옵션을 제공합니다.

- 단일 어셈블리 또는 어셈블리 컬렉션으로.

     이 옵션을 사용하는 경우 빌드된 .dll 또는 .exe 파일을 사용하면 됩니다.

- 캐비닛(CAB) 파일로.

     이 옵션을 사용하는 경우 파일을 .cab 파일로 압축하여 배포 또는 다운로드 시간을 줄입니다.

- Windows Installer 패키지 또는 다른 설치 관리자 형식으로.

     이 옵션을 사용하는 경우 Windows Installer에서 사용할 .msi 파일을 만들거나 다른 설치 관리자에서 사용하기 위해 애플리케이션을 패키징합니다.

### <a name="distribution"></a>분포

.NET Framework는 다음과 같은 애플리케이션 배포 옵션을 제공합니다.

- XCOPY 또는 FTP 사용.

     공용 언어 런타임 애플리케이션은 자체 설명적이며 레지스트리 항목이 필요하지 않으므로 XCOPY 또는 FTP를 사용하여 애플리케이션을 해당 디렉터리에 복사할 수 있습니다. 그런 다음 해당 디렉터리에서 애플리케이션을 실행할 수 있습니다.

- 코드 다운로드 사용.

     인터넷이나 회사 인트라넷을 통해 애플리케이션을 배포하는 경우 코드를 컴퓨터로 다운로드하고 여기서 애플리케이션을 실행하면 됩니다.

- Windows Installer 2.0과 같은 설치 관리자 프로그램 사용.

     Windows Installer 2.0은 전역 어셈블리 캐시와 전용 디렉터리에서 .NET Framework 어셈블리를 설치, 복구 또는 제거할 수 있습니다.

### <a name="installation-location"></a>설치 위치

런타임에서 찾을 수 있도록 애플리케이션의 어셈블리를 배포할 위치를 확인하려면 [런타임에서 어셈블리를 찾는 방법](how-the-runtime-locates-assemblies.md)을 참조하세요.

보안 고려 사항도 애플리케이션 배포 방법에 영향을 줄 수 있습니다. 코드의 위치에 따라 관리 코드에 보안 권한이 부여됩니다. 인터넷과 같은 거의 신뢰되지 않는 위치에 애플리케이션이나 구성 요소를 배포하면 애플리케이션이나 구성 요소가 수행할 수 있는 기능이 제한됩니다. 배포 및 보안 고려 사항에 대한 자세한 내용은 [코드 액세스 보안 기본 사항](../misc/code-access-security-basics.md)을 참조하세요.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[런타임에서 어셈블리를 찾는 방법](how-the-runtime-locates-assemblies.md)|공용 언어 런타임에서 바인딩 요청을 충족하는 데 사용할 어셈블리를 확인하는 방법을 설명합니다.|
|[최선의 어셈블리 로드 방법](best-practices-for-assembly-loading.md)|<xref:System.InvalidCastException>, <xref:System.MissingMethodException> 및 다른 오류를 발생시킬 수 있는 형식 ID 문제를 방지하는 방법을 설명합니다.|
|[.NET Framework 4.5를 설치하는 동안 시스템 다시 시작 줄이기](reducing-system-restarts.md)|최대한 다시 시작을 방지하는 다시 시작 관리자 및 .NET Framework를 설치하는 애플리케이션이 다시 시작 관리자를 활용할 수 있는 방법을 설명합니다.|
|[관리자를 위한 배포 가이드](guide-for-administrators.md)|시스템 관리자가 SCCM(System Center Configuration Manager)을 사용하여 .NET Framework 및 해당 시스템 종속성을 네트워크 전체에 배포할 수 있는 방법을 설명합니다.|
|[개발자를 위한 배포 가이드](deployment-guide-for-developers.md)|개발자가 애플리케이션과 함께 .NET Framework를 사용자 컴퓨터에 설치할 수 있는 방법을 설명합니다.|
|[애플리케이션, 서비스 및 구성 요소 배포](/visualstudio/deployment/deploying-applications-services-and-components)|ClickOnce 및 Windows Installer 기술을 사용하여 애플리케이션을 게시하기 위한 지침을 포함하여 Visual Studio의 배포 옵션을 설명합니다.|
|[ClickOnce 애플리케이션 게시](/visualstudio/deployment/publishing-clickonce-applications)|Windows Forms 애플리케이션을 패키징하고 ClickOnce로 네트워크의 클라이언트 컴퓨터에 배포하는 방법을 설명합니다.|
|[리소스 패키징 및 배포](../resources/packaging-and-deploying-resources-in-desktop-apps.md)|.NET Framework에서 리소스를 패키징 및 배포하는 데 사용하는 허브 및 스포크 모델을 설명합니다. 리소스 명명 규칙, 대체(fallback) 프로세스 및 패키징 대안을 설명합니다.|
|[Interop 애플리케이션 배포](../interop/deploying-an-interop-application.md)|일반적으로 .NET Framework 클라이언트 어셈블리, 고유한 COM 형식 라이브러리를 나타내는 하나 이상의 interop 어셈블리 및 하나 이상의 등록된 COM 구성 요소를 포함하는 interop 애플리케이션을 제공하고 설치하는 방법을 설명합니다.|
|[방법: .NET Framework 4.5 설치 관리자에서 진행률 가져오기](how-to-get-progress-from-the-dotnet-installer.md)|설치 진행 상황을 자체적으로 표시하면서 .NET Framework 설치 프로세스를 자동으로 시작하고 추적하는 방법을 설명합니다.|

## <a name="see-also"></a>참고 항목

- [개발 가이드](../development-guide.md)
