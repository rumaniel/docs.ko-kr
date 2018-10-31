---
title: dotnet pack 명령 - .NET Core CLI
description: dotnet pack 명령은 .NET Core 프로젝트에 대한 NuGet 패키지를 만듭니다.
author: mairaw
ms.author: mairaw
ms.date: 05/29/2018
ms.openlocfilehash: 434f1c97af24d1417cd79edd52b63814fd4c6512
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48840476"
---
# <a name="dotnet-pack"></a>dotnet pack

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet pack` - 코드를 NuGet 패키지로 압축합니다.

## <a name="synopsis"></a>개요

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet pack [<PROJECT>] [-c|--configuration] [--force] [--include-source] [--include-symbols] [--no-build] [--no-dependencies]
    [--no-restore] [-o|--output] [--runtime] [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet pack [<PROJECT>] [-c|--configuration] [--include-source] [--include-symbols] [--no-build] [-o|--output]
    [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```
---

## <a name="description"></a>설명

`dotnet pack` 명령은 프로젝트를 빌드하고 NuGet 패키지를 만듭니다. 이 명령의 결과가 NuGet 패키지입니다. `--include-symbols` 옵션이 있는 경우 디버그 기호를 포함하는 다른 패키지가 생성됩니다.

압축된 프로젝트의 NuGet 종속성은 *.nuspec* 파일에 추가되므로 패키지를 설치할 때 적절히 확인됩니다. 프로젝트 간 참조는 프로젝트 내에서 패키지되지 않습니다. 현재 프로젝트 간 종속성이 있는 경우 프로젝트당 패키지가 있어야 합니다.

`dotnet pack`은 기본적으로 프로젝트를 먼저 빌드합니다. 이렇게 하지 않으려면 `--no-build` 옵션을 전달합니다. 이 옵션은 코드가 이미 빌드된 CI(연속 통합) 빌드 시나리오에서 유용합니다.

압축 프로세스에 대한 `dotnet pack` 명령에 MSBuild 속성을 제공할 수 있습니다. 자세한 내용은 [NuGet 메타데이터 속성](csproj.md#nuget-metadata-properties) 및 [MSBuild 명령줄 참조](/visualstudio/msbuild/msbuild-command-line-reference)를 참조하세요. [예제](#examples) 섹션에서는 몇 가지 시나리오에 MSBuild -p 스위치를 사용하는 방법을 보여 줍니다.

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="arguments"></a>인수

`PROJECT`

압축할 프로젝트입니다. [csproj file](csproj.md) 파일 또는 디렉터리에 대한 경로입니다. 지정하지 않으면 현재 디렉터리로 기본 설정됩니다.

## <a name="options"></a>옵션

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`입니다.

`--force`

마지막 복원이 성공한 경우에도 모든 종속성을 강제 확인합니다. 이 플래그를 지정하는 것은 *project.assets.json* 파일을 삭제하는 것과 같습니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--include-source`

NuGet 패키지에 소스 파일을 포함합니다. 소스 파일은 `nupkg`의 `src` 폴더에 있습니다.

`--include-symbols`

기호 `nupkg`를 생성합니다.

`--no-build`

압축하기 전에 프로젝트를 빌드하지 않습니다. 또한 `--no-restore` 플래그를 암시적으로 설정합니다.

`--no-dependencies`

프로젝트 간 참조를 무시하고 루트 프로젝트만 복원합니다.

`--no-restore`

명령을 실행할 때 암시적 복원을 실행하지 않습니다.

`-o|--output <OUTPUT_DIRECTORY>`

지정된 디렉터리에 빌드된 패키지를 배치합니다.

`--runtime <RUNTIME_IDENTIFIER>`

패키지를 복원할 대상 런타임을 지정합니다. RID(런타임 식별자) 목록은 [RID 카탈로그](../rid-catalog.md)를 참조하세요.

`-s|--serviceable`

패키지에 서비스 가능 플래그를 설정합니다. 자세한 내용은 [.NET 블로그: .NET 4.5.1에서 .NET NuGet 라이브러리에 대한 Microsoft 보안 업데이트를 지원함](https://aka.ms/nupkgservicing)을 참조하세요.

`--version-suffix <VERSION_SUFFIX>`

프로젝트에서 `$(VersionSuffix)` MSBuild 속성에 대한 값을 정의합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

> [!NOTE]
> 웹 프로젝트는 기본적으로 패키지할 수 없습니다. 기본 동작을 재정의하려면 다음 속성을 *.csproj* 파일에 추가합니다.
> ```xml
> <PropertyGroup>
>    <IsPackable>true</IsPackable>
> </PropertyGroup>
> ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`입니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--include-source`

NuGet 패키지에 소스 파일을 포함합니다. 소스 파일은 `nupkg`의 `src` 폴더에 있습니다.

`--include-symbols`

기호 `nupkg`를 생성합니다.

`--no-build`

압축하기 전에 프로젝트를 빌드하지 않습니다.

`-o|--output <OUTPUT_DIRECTORY>`

지정된 디렉터리에 빌드된 패키지를 배치합니다.

`-s|--serviceable`

패키지에 서비스 가능 플래그를 설정합니다. 자세한 내용은 [.NET 블로그: .NET 4.5.1에서 .NET NuGet 라이브러리에 대한 Microsoft 보안 업데이트를 지원함](https://aka.ms/nupkgservicing)을 참조하세요.

`--version-suffix <VERSION_SUFFIX>`

프로젝트에서 `$(VersionSuffix)` MSBuild 속성에 대한 값을 정의합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

---

## <a name="examples"></a>예제

현재 디렉터리에 있는 프로젝트를 압축합니다.

`dotnet pack`

`app1` 프로젝트를 압축합니다.

`dotnet pack ~/projects/app1/project.csproj`

현재 디렉터리에 있는 프로젝트를 압축하고 결과 패키지를 `nupkgs` 폴더에 배치합니다.

`dotnet pack --output nupkgs`

현재 디렉터리에 있는 프로젝트를 `nupkgs` 폴더로 압축하고 빌드 단계를 건너뜁니다.

`dotnet pack --no-build --output nupkgs`

*.csproj* 파일에서 프로젝트의 버전 접미사를 `<VersionSuffix>$(VersionSuffix)</VersionSuffix>`로 구성한 상태로 현재 프로젝트를 압축하고 결과 패키지 버전을 지정된 접미사로 업데이트합니다.

`dotnet pack --version-suffix "ci-1234"`

`PackageVersion` MSBuild 속성을 사용하여 패키지 버전을 `2.1.0`으로 설정합니다.

`dotnet pack -p:PackageVersion=2.1.0`

특정 [대상 프레임워크](../../standard/frameworks.md)에 대한 프로젝트를 압축합니다.

`dotnet pack -p:TargetFrameworks=net45`

프로젝트를 압축하고 복원 작업에 대한 특정 런타임(Windows 10)을 사용합니다(.NET Core SDK 2.0 이상 버전).

`dotnet pack --runtime win10-x64`
