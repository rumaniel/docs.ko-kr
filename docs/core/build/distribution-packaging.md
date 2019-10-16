---
title: .NET Core 배포 패키징
description: 배포를 위해 .NET Core를 패키지하고 이름과 버전을 지정하는 방법에 관해 알아봅니다.
author: tmds
ms.date: 10/09/2019
ms.custom: seodec18
ms.openlocfilehash: 3c41ce8a4a9ac1a914de2535a9b2423a7ddfa2cf
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250135"
---
# <a name="net-core-distribution-packaging"></a>.NET Core 배포 패키징

.NET Core를 점점 더 많은 플랫폼에서 사용할 수 있게 되므로 이를 패키지하고 이름과 버전을 지정하는 방법을 알아보는 것이 도움이 됩니다. 이를 통해 패키지 유지 관리자는 사용자가 .NET을 어디서 실행하든 상관없이 일관된 환경을 보장할 수 있습니다. 이 문서는 다음에 해당하는 사용자에게 유용합니다.

- 원본에서 .NET Core를 빌드하려는 사용자
- 결과 레이아웃 또는 생성된 패키지에 영향을 미칠 수 있는 .NET Core CLI 변경을 수행하려는 사용자

## <a name="disk-layout"></a>디스크 레이아웃

설치하면 .NET Core는 파일 시스템에서 다음과 같이 배치된 여러 구성 요소로 구성됩니다.

```
{dotnet_root}                                     (*)
├── dotnet                       (1)
├── LICENSE.txt                  (8)
├── ThirdPartyNotices.txt        (8)
├── host                                          (*)
│   └── fxr                                       (*)
│       └── <fxr version>        (2)
├── sdk                                           (*)
│   ├── <sdk version>            (3)
│   └── NuGetFallbackFolder      (4)              (*)
├── packs                                         (*)
│   ├── Microsoft.AspNetCore.App.Ref              (*)
│   │   └── <aspnetcore ref version>     (11)
│   ├── Microsoft.NETCore.App.Ref                 (*)
│   │   └── <netcore ref version>        (12)
│   ├── Microsoft.NETCore.App.Host.<rid>          (*)
│   │   └── <apphost version>            (13)
│   ├── Microsoft.WindowsDesktop.App.Ref          (*)
│   │   └── <desktop ref version>        (14)
│   └── NETStandard.Library.Ref                   (*)
│       └── <netstandard version>        (15)
├── shared                                        (*)
│   ├── Microsoft.NETCore.App                     (*)
│   │   └── <runtime version>     (5)
│   ├── Microsoft.AspNetCore.App                  (*)
│   │   └── <aspnetcore version>  (6)
│   ├── Microsoft.AspNetCore.All                  (*)
│   │   └── <aspnetcore version>  (6)
│   └── Microsoft.WindowsDesktop.App              (*)
│       └── <desktop app version> (7)
└── templates                                     (*)
│   └── <templates version>      (17)
/
├── etc/dotnet
│       └── install_location     (16)
├── usr/share/man/man1
│       └── dotnet.1.gz          (9)
└── usr/bin
        └── dotnet               (10)
```

- (1) **dotnet** 호스트("muxer"라고도 함)는 런타임을 활성화하여 애플리케이션을 시작하고 SDK를 활성화하여 명령을 보내는 두 가지의 고유한 역할을 가지고 있습니다. 호스트는 네이티브 실행 파일(`dotnet.exe`)입니다.

단일 호스트가 있지만 다른 구성 요소는 대부분 버전이 지정된 디렉터리(2,3,5,6)에 있습니다. 여러 버전이 나란히 설치되므로 시스템에 여러 버전이 표시될 수 있습니다.

- (2) **host/fxr/\<fxr 버전>** 에는 호스트에서 사용하는 프레임워크 확인 논리가 포함됩니다. 호스트는 설치된 최신 hostfxr을 사용합니다. hostfxr는 .NET Core 애플리케이션을 실행할 때 적합한 런타임을 선택하는 일을 담당합니다. 예를 들어 .NET Core 2.0.0에 대해 빌드된 애플리케이션을 사용할 수 있는 경우 2.0.5 런타임을 사용합니다. 마찬가지로 hostfxr은 개발 중에 적절한 SDK를 선택합니다.

- (3) **sdk/\<sdk version>** SDK("도구"라고도 함)는 .NET Core 라이브러리 및 애플리케이션을 작성하고 빌드하는 데 사용할 수 있는 관리형 도구 집합입니다. SDK는 .NET Core CLI(명령줄 인터페이스), 관리형 언어 컴파일러, MSBuild 및 연결된 빌드 작업과 대상, NuGet, 새 프로젝트 템플릿 등을 포함합니다.

- (4) **sdk/NuGetFallbackFolder**에는 `dotnet restore` 또는 `dotnet build /t:Restore` 실행처럼 복원 작업 중에 SDK에서 사용하는 NuGet 패키지의 캐시가 포함됩니다. 이 폴더는 .NET Core 3.0 이전에만 사용됩니다. `nuget.org`에서 미리 빌드된 이진 자산을 포함하므로 소스에서 빌드할 수 없습니다.

**공유** 폴더에는 프레임워크가 포함됩니다. 공유 프레임워크는 다른 애플리케이션에서 사용할 수 있도록 중앙 위치에 라이브러리의 집합을 제공합니다.

- (5) **shared/Microsoft.NETCore.App/\<runtime 버전>** 이 프레임워크에는 지원되는 .NET Core 런타임 및 관리 라이브러리가 포함됩니다.

- (6) **shared/Microsoft.AspNetCore.{App,All}/\<aspnetcore 버전>** 에는 ASP.NET Core 라이브러리가 포함됩니다. `Microsoft.AspNetCore.App`에서 라이브러리를 개발하고 .NET Core 프로젝트의 일부로 지원합니다. `Microsoft.AspNetCore.All`의 라이브러리는 타사 라이브러리도 포함하는 상위 집합입니다.

- (7) **shared/Microsoft.Desktop.App/\<데스크톱 앱 버전>** 은 Windows 데스크톱 라이브러리를 포함합니다. Windows 이외의 플랫폼에는 포함되지 않습니다.

- (8) **LICENSE.txt,ThirdPartyNotices.txt**는 각각 .NET Core에서 사용되는 .NET Core 라이선스 및 타사 라이브러리의 라이선스입니다.

- (9, 10) **dotnet.1.gz, dotnet**`dotnet.1.gz`은 dotnet 설명서 페이지입니다. `dotnet`은 dotnet 호스트(1)의 symlink입니다. 이러한 파일은 시스템 통합을 위해 잘 알려진 위치에 설치됩니다.

- (11,12) **Microsoft.NETCore.App.Ref,Microsoft.AspNetCore.App.Ref**는 .NET Core 및 ASP.NET Core의 `x.y` 버전의 API를 각각 설명합니다. 이러한 팩은 이러한 대상 버전에 대해 컴파일할 때 사용됩니다.

- (13) **Microsoft.NETCore.App.Host.\<rid>** 는 플랫폼 `rid`용 네이티브 이진을 포함합니다. 이 이진은 .NET Core 애플리케이션을 해당 플랫폼의 네이티브 이진으로 컴파일할 때의 템플릿입니다.

- (14) **Microsoft.WindowsDesktop.App.Ref**는 Windows 데스크톱 애플리케이션의 `x.y` 버전의 API를 설명합니다. 이러한 파일은 해당 대상에 대해 컴파일할 때 사용됩니다. 이는 Windows 이외의 플랫폼에는 제공되지 않습니다.

- (15) **NETStandard.Library.Ref**는 netstandard `x.y` API를 설명합니다. 이러한 파일은 해당 대상에 대해 컴파일할 때 사용됩니다.

- (16) **/etc/dotnet/install_location**은 `{dotnet_root}`의 전체 경로를 포함하는 파일입니다. 경로는 줄 바꿈으로 끝날 수 있습니다. 루트가 `/usr/share/dotnet`인 경우에는 이 파일을 추가할 필요가 없습니다.

- (17) **템플릿**은 SDK에서 사용하는 템플릿을 포함합니다. 예를 들어 `dotnet new`는 여기에서 프로젝트 템플릿을 찾습니다.

`(*)`로 표시된 폴더는 여러 패키지에서 사용됩니다. 일부 패키지 형식(예: `rpm`)에는 이러한 폴더에 대한 특별한 처리가 필요합니다. 패키지 유지 관리자는 이를 처리해야 합니다.

## <a name="recommended-packages"></a>권장된 패키지

.NET Core 버전 관리는 런타임 구성 요소 `[major].[minor]` 버전 번호에 기반합니다.
SDK 버전은 동일한 `[major].[minor]`를 사용하고, SDK의 기능 및 패치 의미 체계를 결합한 독립 `[patch]`를 포함합니다.
예: SDK 버전 2.2.302는 2.2 런타임을 지원하는 SDK의 세 번째 기능 릴리스의 두 번째 패치 릴리스입니다. 버전 관리의 작동 방식에 대 한 자세한 내용은 [.NET Core 버전 관리 개요](../versions/index.md)를 참조하세요.

일부 패키지에는 해당 이름의 버전 번호 일부가 포함됩니다. 그러면 특정 버전을 설치할 수 있습니다.
버전의 나머지 부분은 버전 이름에 포함되지 않습니다. 이 때문에 OS 패키지 관리자가 패키지를 업데이트할 수 있습니다(예: 보안 해결을 자동으로 설치). 지원되는 패키지 관리자는 Linux 특정입니다.

다음은 권장되는 패키지 목록입니다.

- `dotnet-sdk-[major].[minor]` - 특정 런타임의 최신 sdk를 설치합니다.
  - **버전:** \<런타임 버전>
  - **예:** dotnet-sdk-2.1
  - **포함:** (3),(4)
  - **종속성:** `dotnet-runtime-[major].[minor]`, `aspnetcore-runtime-[major].[minor]`, `dotnet-targeting-pack-[major].[minor]`, `aspnetcore-targeting-pack-[major].[minor]`, `netstandard-targeting-pack-[netstandard_major].[netstandard_minor]`, `dotnet-apphost-pack-[major].[minor]`, `dotnet-templates-[major].[minor]`

- `aspnetcore-runtime-[major].[minor]` - 특정 ASP.NET Core 런타임을 설치합니다.
  - **버전:** \<aspnetcore 런타임 버전>
  - **예:** aspnetcore-runtime-2.1
  - **포함:** (6)
  - **종속성:** `dotnet-runtime-[major].[minor]`

- `dotnet-runtime-deps-[major].[minor]` _(선택 사항)_ - 자체 포함 애플리케이션을 실행하기 위한 종속성을 설치합니다.
  - **버전:** \<런타임 버전>
  - **예:** dotnet-runtime-deps-2.1
  - **종속성:** _배포판 특정 종속성_

- `dotnet-runtime-[major].[minor]` - 특정 런타임을 설치합니다.
  - **버전:** \<런타임 버전>
  - **예:** dotnet-runtime-2.1
  - **포함:** (5)
  - **종속성:** `dotnet-hostfxr-[major].[minor]`, `dotnet-runtime-deps-[major].[minor]`

- `dotnet-hostfxr-[major].[minor]` - 종속성
  - **버전:** \<런타임 버전>
  - **예:** dotnet-hostfxr-3.0
  - **포함:** (2)
  - **종속성:** `dotnet-host`

- `dotnet-host` - 종속성
  - **버전:** \<런타임 버전>
  - **예:** dotnet-host
  - **포함:** (1),(8),(9),(10),(16)

- `dotnet-apphost-pack-[major].[minor]` - 종속성
  - **버전:** \<런타임 버전>
  - **포함:** (13)

- `dotnet-targeting-pack-[major].[minor]` - 최신이 아닌 런타임 대상 지정 허용
  - **버전:** \<런타임 버전>
  - **포함:** (12)

- `aspnetcore-targeting-pack-[major].[minor]` - 최신이 아닌 런타임 대상 지정 허용
  - **버전:** \<aspnetcore 런타임 버전>
  - **포함:** (11)

- `netstandard-targeting-pack-[netstandard_major].[netstandard_minor]` - netstandard 버전 대상 지정 허용
  - **버전:** \<sdk 버전>
  - **포함:** (15)

- `dotnet-templates-[major].[minor]`
  - **버전:** \<sdk 버전>
  - **포함:** (15)

`dotnet-runtime-deps-[major].[minor]`에서는 _배포판 특정 종속성_에 대해 이해해야 합니다. 배포판 빌드 시스템은 이를 자동으로 파생시킬 수도 있으므로 패키지는 선택 사항입니다. 이 경우 이러한 종속성은 `dotnet-runtime-[major].[minor]` 패키지에 직접 추가됩니다.

패키지 콘텐츠가 버전이 있는 폴더에 있는 경우 패키지 이름 `[major].[minor]`는 버전이 있는 폴더 이름과 일치합니다. `netstandard-targeting-pack-[netstandard_major].[netstandard_minor]`를 제외한 모든 패키지에서 이는 .NET Core 버전과도 일치합니다.

패키지 간 종속성은 _동일하거나 더 큰_ 버전 요구 사항을 사용해야 합니다. 예를 들어 `dotnet-sdk-2.2:2.2.401`에는 `aspnetcore-runtime-2.2 >= 2.2.6`이 필요합니다. 그러면 사용자는 루트 패키지(예: `dnf update dotnet-sdk-2.2`)를 통해 설치를 업그레이드할 수 있습니다.

대부분의 배포는 모든 아티팩트를 원본에서 빌드해야 합니다. 그러면 패키지에 영향을 줍니다.

- `shared/Microsoft.AspNetCore.All`의 타사 라이브러리는 원본에서 쉽게 빌드할 수 없습니다. 따라서 `aspnetcore-runtime` 패키지에서 해당 폴더를 생략합니다.

- `nuget.org`에서 이진 아티팩트를 사용하여 `NuGetFallbackFolder`를 채웁니다. 비워 두어야 합니다.

여러 `dotnet-sdk` 패키지는 `NuGetFallbackFolder`에 동일한 파일을 제공할 수 있습니다. 패키지 관리자를 사용하여 문제를 방지하려면 이러한 파일이 동일해야 합니다(체크섬, 수정 날짜 등).

## <a name="building-packages"></a>패키지 빌드

[dotnet/source-build](https://github.com/dotnet/source-build) 리포지토리는 .NET Core SDK 및 모든 해당 구성 요소의 소스 Tarball을 빌드하는 방법에 대한 지침을 제공합니다. 원본 빌드 리포지토리의 출력은 이 아티클의 첫 번째 섹션에 설명된 레이아웃과 일치합니다.
