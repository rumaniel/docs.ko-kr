---
title: dotnet 설치 스크립트
description: .NET Core CLI 도구 및 공유 런타임을 설치하는 dotnet-install 스크립트에 대해 알아봅니다.
author: blackdwarf
ms.author: mairaw
ms.date: 09/11/2017
ms.openlocfilehash: ea14424297dcf1dab8711197bee1d3b3e19879c1
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48837078"
---
# <a name="dotnet-install-scripts-reference"></a>dotnet-install 스크립트 참조

## <a name="name"></a>name

`dotnet-install.ps1` | `dotnet-install.sh` - .NET Core CLI 도구 및 공유 런타임을 설치하는 데 사용되는 스크립트입니다.

## <a name="synopsis"></a>개요

Windows:

`dotnet-install.ps1 [-Channel] [-Version] [-InstallDir] [-Architecture] [-SharedRuntime] [-DryRun] [-NoPath] [-AzureFeed] [-ProxyAddress] [--Verbose] [--Help]`

macOS/Linux:

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture] [--shared-runtime] [--dry-run] [--no-path] [--azure-feed] [--verbose] [--help]`

## <a name="description"></a>설명

`dotnet-install` 스크립트는 .NET Core CLI 도구 및 공유 런타임을 포함하는 .NET Core SDK의 비관리자 설치를 수행하는 데 사용됩니다.

[.NET Core 기본 웹 사이트](https://dot.net)에서 호스팅되는 안정적인 버전을 사용하는 것이 좋습니다. 스크립트에 대한 직접 경로는 다음과 같습니다.

* <https://dot.net/v1/dotnet-install.sh>(bash, UNIX)
* <https://dot.net/v1/dotnet-install.ps1>(Powershell, Windows)

이러한 스크립트의 주요 유용성은 자동화 시나리오 및 비관리자 설치입니다. 두 가지 스크립트가 있습니다. 하나는 Windows에서 작동하는 PowerShell 스크립트입니다. 다른 스크립트는 Linux/macOS에서 작동하는 bash 스크립트입니다. 두 스크립트의 동작은 동일합니다. 또한 bash 스크립트는 PowerShell 스위치를 읽으므로 Linux/macOS 시스템에서 스크립트와 함께 PowerShell 스위치를 사용할 수 있습니다.

설치 스크립트는 CLI 빌드 저장 위치에서 ZIP/tarball 파일을 다운로드하여 기본 위치나 `-InstallDir|--install-dir`로 지정한 위치에 설치를 계속 진행합니다. 기본적으로 설치 스크립트는 SDK를 다운로드하고 설치합니다. 공유 런타임만 가져오려는 경우 `--shared-runtime` 인수를 지정합니다.

기본적으로 스크립트는 현재 세션에 대한 $PATH에 설치 위치를 추가합니다. `--no-path` 인수를 지정하여 이 기본 동작을 재정의합니다.

스크립트를 실행하기 전에 필요한 모든 [종속성](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)을 설치하세요.

`--version` 인수를 사용하여 특정 버전을 설치할 수 있습니다. 버전은 세 부분으로 구성된 버전(예: 1.0.0-13232)으로 지정해야 합니다. 생략하면 `latest` 버전을 사용합니다.

## <a name="options"></a>옵션

`-Channel <CHANNEL>`

설치에 대한 소스 채널을 지정합니다. 가능한 값은 다음과 같습니다.

- `Current` - 현재 릴리스
- `LTS` - 장기 지원 채널(현재 지원되는 릴리스)
- 특정 릴리스를 나타내는 X.Y 형식의 두 부분으로 된 버전(예: `2.0` 또는 `1.0`)
- 분기 이름[예: `master` 분기에서 온 최신 값의 경우 `release/2.0.0`, `release/2.0.0-preview2` 또는 `master`("bleeding edge" 야간 릴리스)]

기본값은 `LTS`입니다. .NET 지원 채널에 대한 자세한 내용은 [.NET Core 지원 주기](https://www.microsoft.com/net/core/support) 항목을 참조하세요.

`-Version <VERSION>`

특정 빌드 버전을 나타냅니다. 가능한 값은 다음과 같습니다.

- `latest` - 채널의 최신 빌드(`-Channel` 옵션과 함께 사용됨)
- `coherent` - 채널의 일관된 최신 빌드, 안정적인 최신 패키지 조합 사용(분기 이름 `-Channel` 옵션과 함께 사용됨)
- 특정 빌드 버전을 나타내는 X.Y.Z 형식의 세 부분으로 구성된 버전이며 `-Channel` 옵션을 대체합니다. `2.0.0-preview2-006120`

생략하면 `-Version`은 `latest`로 기본 설정됩니다.

`-InstallDir <DIRECTORY>`

설치 경로를 지정합니다. 디렉터리가 없을 경우 만듭니다. 기본값은 *%LocalAppData%\.dotnet*입니다. 이진 파일은 디렉터리에 직접 배치됩니다.

`-Architecture <ARCHITECTURE>`

설치할 .NET Core 바이너리의 아키텍처입니다. 가능한 값은 `auto`, `x64` 및 `x86`입니다. 기본값은 현재 실행 중인 OS 아키텍처를 나타내는 `auto`입니다.

`-SharedRuntime`

설정되면 이 스위치는 설치를 공유 런타임으로 제한합니다. 전체 SDK가 설치되지는 않습니다.

`-DryRun`

설정된 경우 스크립트에서 설치를 수행하지는 않지만 대신 현재 요청된 버전의 .NET Core CLI를 일관되게 설치하기 위해 사용할 명령줄을 표시합니다. 예를 들어 `latest` 버전을 지정하면 빌드 스크립트에서 이 명령을 결정적으로 사용할 수 있도록 특정 버전에 대한 링크를 표시합니다. 또한 직접 설치하거나 다운로드하는 것을 선호하는 경우 이진 파일 위치를 표시합니다.

`-NoPath`

설정된 경우 현재 세션에 대한 경로로 접두사/installdir을 내보내지 않습니다. 기본적으로 스크립트는 경로를 수정하여, 설치 후 CLI 도구를 즉시 사용할 수 있게 만듭니다.

`-AzureFeed`

설치 관리자에 대한 Azure 피드의 URL을 지정합니다. 이 값은 변경하는 것이 좋습니다. 기본값은 `https://dotnetcli.azureedge.net/dotnet`입니다.

`-ProxyAddress`

설정된 경우 설치 관리자에서 웹 요청을 만들 때 프록시를 사용합니다. (Windows에만 유효함)

`--verbose`

진단 정보를 표시합니다.

`--help`

스크립트에 대한 도움말을 출력합니다.

## <a name="examples"></a>예제

기본 위치에 최신 LTS(장기 지원) 버전을 설치합니다.

Windows:

`./dotnet-install.ps1 -Channel LTS`

macOS/Linux:

`./dotnet-install.sh --channel LTS`

지정된 위치에 2.0 채널의 최신 버전을 설치합니다.

Windows:

`./dotnet-install.ps1 -Channel 2.0 -InstallDir C:\cli`

macOS/Linux:

`./dotnet-install.sh --channel 2.0 --install-dir ~/cli`

1.1.0 버전의 공유 런타임을 설치합니다.

Windows:

`./dotnet-install.ps1 -SharedRuntime -Version 1.1.0`

macOS/Linux:

`./dotnet-install.sh --shared-runtime --version 1.1.0`

스크립트 가져와서 .NET Core CLI one-liner 예제를 설치합니다.

Windows:

`@powershell -NoProfile -ExecutionPolicy unrestricted -Command "[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; &([scriptblock]::Create((Invoke-WebRequest -useb 'https://dot.net/v1/dotnet-install.ps1'))) <additional install-script args>"`

macOS/Linux:

`curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin <additional install-script args>`

## <a name="see-also"></a>참고 항목

* [.NET Core 릴리스](https://github.com/dotnet/core/releases)
* [.NET Core 런타임 및 SDK 다운로드 아카이브](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md)
