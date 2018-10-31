---
title: .NET Core SDK 및 CI(연속 통합)의 도구 사용
description: .NET Core SDK 및 빌드 서버의 도구를 사용하는 방법에 대한 정보입니다.
author: guardrex
ms.author: mairaw
ms.date: 05/18/2017
ms.openlocfilehash: 207a6740f2a483d532c194b2bf8112898e9c3463
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48033469"
---
# <a name="using-net-core-sdk-and-tools-in-continuous-integration-ci"></a>.NET Core SDK 및 CI(연속 통합)의 도구 사용

## <a name="overview"></a>개요

이 문서는 .NET Core SDK 및 빌드 서버의 도구를 사용하는 방법의 개요를 제공합니다. .NET Core 도구 집합은 개발자가 명령 프롬프트에 명령을 입력할 경우 대화형으로 작동하고 CI(연속 통합) 서버에서 빌드 스크립트가 실행될 경우 자동으로 작동합니다. 명령, 옵션, 입력 및 출력은 동일하고 도구를 취득하는 방법과 앱을 빌드하기 위한 시스템만 제공하면 됩니다. 이 문서에서는 빌드 스크립트를 디자인 및 구성하는 방법에 대한 권장 사항과 함께 CI용 도구 취득에 대한 시나리오에 초점을 맞춥니다.

## <a name="installation-options-for-ci-build-servers"></a>CI 빌드 서버에 대한 설치 옵션

### <a name="using-the-native-installers"></a>기본 설치 관리자 사용

기본 설치 관리자는 macOS, Linux 및 Windows에 사용할 수 있습니다. 설치 관리자는 빌드 서버에 대한 관리자(sudo) 액세스 권한이 있어야 합니다. 기본 설치 관리자를 사용하는 장점은 기본 설치 관리자는 도구를 실행하는 데 필요한 모든 기본 종속성을 설치한다는 것입니다. 기본 설치 관리자는 SDK의 시스템 차원 설치를 제공합니다.

macOS 사용자는 PKG 설치 관리자를 사용해야 합니다. Linux에서는 피드 기반 패키지 관리자를 사용하거나(Ubuntu의 경우 apt-get, CentOS의 경우 yum), 패키지 자체를 사용할 수 있습니다(DEB 또는 RPM). Windows에서는 MSI 설치 관리자를 사용합니다.

최신 안정적인 이진 파일은 [Get Started with .NET Core](https://aka.ms/dotnetcoregs)(.NET Core 시작)에서 찾을 수 있습니다. 최신(및 안정적이지 않을 수 있는) 시험판 도구를 사용하려면 [dotnet/cli GitHub 리포지토리](https://github.com/dotnet/cli#installers-and-binaries)에 제공된 링크를 사용하세요. Linux 배포의 경우 `tar.gz` 보관(`tarballs`라고도 함)을 사용할 수 있습니다. 보관 내의 설치 스크립트를 사용하여 .NET Core를 설치합니다.

### <a name="using-the-installer-script"></a>설치 관리자 스크립트 사용

설치 관리자 스크립트를 사용하면 관리자가 아닌 사용자도 빌드 서버에 설치하고 도구 취득을 쉽게 자동화할 수 있습니다. 이 스크립트는 도구를 다운로드하고 사용을 위해 기본 또는 지정된 위치로 추출하는 과정을 처리합니다. 또한 설치할 도구 버전을 지정하고 전체 SDK를 설치할지, 아니면 공유 런타임만 설치할지 지정할 수 있습니다.

원하는 SDK 버전을 가져와서 설치할 수 있도록 빌드 시작 시 설치 관리자 스크립트를 실행하도록 자동화됩니다. *원하는 버전*이란 프로젝트에서 빌드에 필요한 SDK 버전입니다. 스크립트를 사용하여 서버의 로컬 디렉터리에 SDK를 설치하고, 설치된 위치에서 도구를 실행하고 나서, 빌드한 후 정리하거나 CI 서비스에서 정리하도록 할 수 있습니다. 이렇게 하면 전체 빌드 프로세스에 캡슐화 및 격리가 제공됩니다. 설치 스크립트 참조는 [dotnet-install](dotnet-install-script.md) 항목에서 찾을 수 있습니다.

> [!NOTE]
> **Azure DevOps Services**
>
> 설치 관리자 스크립트를 사용할 경우 기본 종속성은 자동으로 설치되지 않습니다. 운영 체제에 기본 종속성이 없는 경우 기본 종속성을 설치해야 합니다. [.NET Core native prerequisites](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)(.NET Core 기본 필수 구성 요소) 항목에서 필수 구성 요소 목록을 참조하세요.

## <a name="ci-setup-examples"></a>CI 설치 예제

이 섹션에서는 PowerShell 또는 bash 스크립트를 사용한 수동 설치에 대해 설명하고 여러 가지 SaaS(Software as a Service) CI 솔루션을 설명합니다. 설명되는 SaaS CI 솔루션은 [Travis CI](https://travis-ci.org/), [AppVeyor](https://www.appveyor.com/) 및 [Build](https://docs.microsoft.com/azure/devops/build-release/index)입니다.

### <a name="manual-setup"></a>수동 설치

각 SaaS 서비스에는 빌드 프로세스를 만들고 구성하기 위한 자체적인 방법이 있습니다. 나열된 것과 다른 SaaS 솔루션을 사용하거나 미리 패키지된 지원 이외의 사용자 지정이 필요한 경우 적어도 일부 수동 구성을 수행해야 합니다.

일반적으로 수동으로 설치하려면 특정 버전의 도구(또는 최신 야간 빌드의 도구)를 취득하고 빌드 스크립트를 실행해야 합니다. PowerShell 또는 bash 스크립트를 사용하여 .NET Core 명령을 오케스트레이션하거나 빌드 프로세스의 개요를 설명하는 프로젝트 파일을 사용할 수 있습니다. [오케스트레이션 섹션](#orchestrating-the-build)에서 이러한 옵션을 자세히 설명합니다.

수동 CI 빌드 서버 설치를 수행하는 스크립트를 만든 후 이를 개발 컴퓨터에서 사용하여 테스트 목적으로 코드를 로컬에 빌드합니다. 스트립트가 로컬에서 제대로 실행되는지 확인한 후 스크립트를 CI 빌드 서버에 배포합니다. 비교적 간단한 PowerShell 스크립트는 .NET Core SDK를 취득하고 Windows 빌드 서버에 설치하는 방법을 보여 줍니다.

```powershell
$ErrorActionPreference="Stop"
$ProgressPreference="SilentlyContinue"

# $LocalDotnet is the path to the locally-installed SDK to ensure the
#   correct version of the tools are executed.
$LocalDotnet=""
# $InstallDir and $CliVersion variables can come from options to the
#   script.
$InstallDir = "./cli-tools"
$CliVersion = "1.0.1"

# Test the path provided by $InstallDir to confirm it exists. If it
#   does, it's removed. This is not strictly required, but it's a
#   good way to reset the environment.
if (Test-Path $InstallDir)
{
    rm -Recurse $InstallDir
}
New-Item -Type "directory" -Path $InstallDir

Write-Host "Downloading the CLI installer..."

# Use the Invoke-WebRequest PowerShell cmdlet to obtain the
#   installation script and save it into the installation directory.
Invoke-WebRequest `
    -Uri "https://dot.net/v1/dotnet-install.ps1" `
    -OutFile "$InstallDir/dotnet-install.ps1"

Write-Host "Installing the CLI requested version ($CliVersion) ..."

# Install the SDK of the version specified in $CliVersion into the
#   specified location ($InstallDir).
& $InstallDir/dotnet-install.ps1 -Version $CliVersion `
    -InstallDir $InstallDir

Write-Host "Downloading and installation of the SDK is complete."

# $LocalDotnet holds the path to dotnet.exe for future use by the
#   script.
$LocalDotnet = "$InstallDir/dotnet"

# Run the build process now. Implement your build script here.
```

스크립트 종료 시 빌드 프로세스에 대한 구현을 제공합니다. 스크립트가 도구를 취득하고 나서 빌드 프로세스를 실행합니다. UNIX 컴퓨터에서는 다음 bash 스크립트가 PowerShell 스크립트에 설명된 작업을 비슷한 방식으로 수행합니다.

```bash
#!/bin/bash
INSTALLDIR="cli-tools"
CLI_VERSION=1.0.1
DOWNLOADER=$(which curl)
if [ -d "$INSTALLDIR" ]
then
    rm -rf "$INSTALLDIR"
fi
mkdir -p "$INSTALLDIR"
echo Downloading the CLI installer.
$DOWNLOADER https://dot.net/v1/dotnet-install.sh > "$INSTALLDIR/dotnet-install.sh"
chmod +x "$INSTALLDIR/dotnet-install.sh"
echo Installing the CLI requested version $CLI_VERSION. Please wait, installation may take a few minutes.
"$INSTALLDIR/dotnet-install.sh" --install-dir "$INSTALLDIR" --version $CLI_VERSION
if [ $? -ne 0 ]
then
    echo Download of $CLI_VERSION version of the CLI failed. Exiting now.
    exit 0
fi
echo The CLI has been installed.
LOCALDOTNET="$INSTALLDIR/dotnet"
# Run the build process now. Implement your build script here.
```

### <a name="travis-ci"></a>Travis CI

`csharp` 언어와 `dotnet` 키를 사용하여 .NET Core SDK를 설치하도록 [Travis CI](https://travis-ci.org/)를 구성할 수 있습니다. 자세한 내용은 [Building a C#, F#, or Visual Basic Project](https://docs.travis-ci.com/user/languages/csharp/)(C#, F# 또는 Visual Basic 프로젝트 빌드)에서 공식 Travis CI 문서를 참조하세요. Travis CI 정보에 액세스할 때 커뮤니티에서 유지 관리되는 `language: csharp` 언어 식별자가 F# 및 Mono를 포함한 모든 .NET 언어에 적용된다는 것에 유의하세요.

Travis CI는 앱에 대한 빌드 조합을 설명하기 위해 런타임, 환경 및 제외/포함의 조합을 지정하는 *빌드 행렬*에서 macOS(OS X 10.11, OS X 10.12) 및 Linux(Ubuntu 14.04) 작업을 실행합니다. 자세한 내용은 [.travis.yml example](https://github.com/dotnet/docs/blob/master/.travis.yml) 파일 및 Travis CI 문서의 [Customizing the Build](https://docs.travis-ci.com/user/customizing-the-build)(빌드 사용자 지정)를 참조하세요. MSBuild 기반 도구의 경우 LTS(1.0.x) 및 Current(1.1.x) 런타임이 패키지에 포함되므로 SDK를 설치하면 빌드에 필요한 모든 것이 제공됩니다.

### <a name="appveyor"></a>AppVeyor

[AppVeyor](https://www.appveyor.com/)는 `Visual Studio 2017` 빌드 작업자 이미지를 사용하여 .NET Core 1.0.1 SDK를 설치합니다. .NET Core SDK의 여러 가지 버전이 포함된 다른 빌드 이미지를 사용할 수 있습니다. 자세한 내용은 [appveyor.yml example](https://github.com/dotnet/docs/blob/master/appveyor.yml)(appveyor.yml 예제) 및 AppVeyor 문서의 [Build worker images](https://www.appveyor.com/docs/build-environment/#build-worker-images)(빌드 작업자 이미지) 항목을 참조하세요.

.NET Core SDK 이진 파일은 설치 스크립트를 통해 하위 디렉터리로 다운로드되어 압축이 풀리고 `PATH` 환경 변수에 추가됩니다. 빌드 행렬을 추가하여 .NET Core SDK의 여러 버전으로 통합 테스트를 실행합니다.

```yaml
environment:
  matrix:
    - CLI_VERSION: 1.0.1
    - CLI_VERSION: Latest

install:
  # See appveyor.yml example for install script
```

### <a name="azure-devops-services"></a>Azure DevOps Services

다음 방법 중 하나를 사용하여 .NET Core 프로젝트를 빌드하도록 Azure DevOps Services를 구성합니다.

1. 명령을 사용하여 [수동 설치 단계](#manual-setup)에서 스크립트를 실행합니다.
1. .NET Core 도구를 사용하도록 구성된 여러 가지 Azure DevOps Services 기본 제공 빌드 작업으로 구성된 빌드를 만듭니다.

두 가지 솔루션 모두 유효합니다. 수동 설치 스크립트를 사용하면 도구를 빌드의 일부로 다운로드한 후 취득하는 도구 버전을 제어할 수 있습니다. 빌드는 만들어야 하는 스크립트에서 실행됩니다. 이 항목에서는 수동 옵션만 설명합니다. Azure DevOps Services 빌드 작업으로 빌드를 구성하는 방법에 대한 자세한 내용은 Azure DevOps Services [Continuous integration and deployment](https://docs.microsoft.com/azure/devops/build-release/index)(연속 통합 및 배포) 항목을 참조하세요.

Azure DevOps Services에서 수동 설치 스크립트를 사용하려면 새 빌드 정의를 만들고 빌드 단계에서 실행할 스크립트를 지정합니다. 이 작업에는 Azure DevOps Services 사용자 인터페이스를 사용합니다.

1. 먼저 새 빌드 정의를 만듭니다. 만들려는 빌드 종류를 정의하는 옵션을 제공하는 화면이 표시되면 **비어 있음** 옵션을 선택합니다.

   ![빈 빌드 정의 선택](./media/using-ci-with-cli/screen1.png)

1. 빌드할 리포지토리를 구성한 후 빌드 정의로 이동합니다. **빌드 단계 추가**를 선택합니다.

   ![빌드 단계 추가](./media/using-ci-with-cli/screen2.png)

1. **작업 카탈로그**가 표시됩니다. 카탈로그에는 빌드에서 사용할 작업이 포함됩니다. 스크립트가 준비되면 **PowerShell: PowerShell 스크립트 실행**에 대해 **추가** 단추를 선택합니다.

   ![PowerShell 스크립트 단계 추가](./media/using-ci-with-cli/screen3.png)

1. 빌드 단계를 구성합니다. 빌드 중인 리포지토리에서 스크립트를 추가합니다.

   ![실행할 PowerShell 스크립트 지정](./media/using-ci-with-cli/screen4.png)

## <a name="orchestrating-the-build"></a>빌드 오케스트레이션

이 문서의 대부분은 .NET Core를 사용하여 코드를 오케스트레이션하거나 *실제로 빌드*하는 방법에 대한 설명 없이 .NET Core 도구를 취득하고 다양한 CI 서비스를 구성하는 방법을 설명합니다. 빌드 프로세스를 구성하는 방법은 여기에서 일반적으로 설명할 수 없는 다양한 요소에 따라 선택할 수 있습니다. 각 기술을 사용하여 빌드를 오케스트레이션하는 방법에 대한 자세한 내용은 [Travis CI](https://travis-ci.org/), [AppVeyor](https://www.appveyor.com/) 및 [Azure DevOps Services](https://docs.microsoft.com/azure/devops/build-release/index)의 설명서 집합에 제공된 리소스 및 샘플을 참조하세요.

.NET Core 도구를 사용하여 .NET Core 코드에 대한 빌드 프로세스를 구성할 때 적용할 두 가지 일반적인 방법에서는 MSBuild를 직접 사용하거나 .NET Core 명령줄 명령을 사용합니다. 어떤 방법을 적용해야 하는지는 방법에 대한 숙련도 및 복잡성의 절충 조건에 따라 결정됩니다. MSBuild는 빌드 프로세스를 작업 및 대상으로 표시하는 기능을 제공하지만 MSBuild 프로젝트 파일 구문 학습의 복잡성이 추가됩니다. .NET Core 명령줄 도구를 사용하는 것이 더 간편하지만 `bash` 또는 PowerShell 같은 스크립팅 언어로 오케스트레이션 논리를 작성해야 합니다.

## <a name="see-also"></a>참고 항목

* [Ubuntu acquisition steps](https://www.microsoft.com/net/core#linuxubuntu)(Ubuntu 취득 단계)
