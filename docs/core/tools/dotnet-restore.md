---
title: dotnet restore 명령
description: dotnet restore 명령을 사용하여 종속성 및 프로젝트 관련 도구를 복원하는 방법을 알아봅니다.
ms.date: 05/29/2018
ms.openlocfilehash: 055a4250755af02ad392877663985f86a647f892
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275756"
---
# <a name="dotnet-restore"></a>dotnet restore

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet restore` - 프로젝트의 종속성 및 도구를 복원합니다.

## <a name="synopsis"></a>개요

<!-- markdownlint-disable MD025 -->

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```dotnetcli
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--force] [--ignore-failed-sources] [--no-cache]
    [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity] [--interactive]
dotnet restore [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```dotnetcli
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--ignore-failed-sources] [--no-cache]
    [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity]
dotnet restore [-h|--help]
```

---

## <a name="description"></a>설명

`dotnet restore` 명령은 NuGet을 사용하여 프로젝트 파일에 지정된 종속성 및 프로젝트 관련 도구를 복원합니다. 기본적으로 종속성 및 도구의 복원은 병렬로 실행됩니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

종속성을 복원하려면 NuGet에 패키지가 있는 피드가 필요합니다. 피드는 일반적으로 *nuget.config* 구성 파일을 통해 제공됩니다. CLI 도구가 설치될 때 기본 구성 파일이 제공됩니다. 프로젝트 디렉터리에 고유한 *nuget.config* 파일을 만들어 추가 피드를 지정합니다. 또한 명령 프롬프트에서 호출당 추가 피드를 지정합니다.

종속성의 경우 복원 작업 중 `--packages` 인수를 사용하여 복원된 패키지가 배치될 위치를 지정합니다. 지정하지 않으면 모든 운영 체제에서 사용자의 홈 디렉터리의 `.nuget/packages` 디렉터리에 있는 기본 NuGet 패키지 캐시가 사용됩니다. 예를 들어 Linux의 경우 */home/user1* 또는 Windows의 경우 *C:\Users\user1*입니다.

프로젝트 관련 도구의 경우 `dotnet restore`는 먼저 도구가 압축된 패키지를 복원한 다음 프로젝트 파일에 지정된 대로 도구의 종속성을 계속 복원합니다.

### <a name="nugetconfig-differences"></a>nuget 구성 차이점

`dotnet restore` 명령의 동작은 있는 경우 *nuget.config* 파일에 있는 일부 설정의 영향을 받습니다. 예를 들어 *nuget.config*의 `globalPackagesFolder`를 설정하면 복원된 NuGet 패키지가 지정한 폴더에 저장됩니다. `dotnet restore` 명령의 `--packages` 옵션을 지정하는 대신 이 방법을 사용할 수 있습니다. 자세한 내용은 [nuget.config 참조](/nuget/schema/nuget-config-file)를 참조하세요.

`dotnet restore`에서 무시하는 3가지 특정 설정은 다음과 같습니다.

- [bindingRedirects](/nuget/schema/nuget-config-file#bindingredirects-section)

  바인딩 리디렉션은 `<PackageReference>` 요소에서 작동하지 않으며 .NET Core에서는 NuGet 패키지의 `<PackageReference>` 요소만 지원합니다.

- [솔루션](/nuget/schema/nuget-config-file#solution-section)

  이 설정은 Visual Studio에만 적용되며 .NET Core에는 적용되지 않습니다. .NET Core에서는 `packages.config` 파일을 사용하지 않고, 대신 NuGet 패키지의 `<PackageReference>` 요소를 사용합니다.

- [trustedSigners](/nuget/schema/nuget-config-file#trustedsigners-section)

  신뢰할 수 있는 패키지의 [플랫폼 간 확인은 NuGet에서 지원하지 않기](https://github.com/NuGet/Home/issues/7939) 때문에 이 설정은 적용되지 않습니다.

## <a name="implicit-dotnet-restore"></a>암시적 `dotnet restore`

.NET Core 2.0부터는 다음 명령을 실행할 때 필요한 경우 `dotnet restore`가 암시적으로 실행됩니다.

- [`dotnet new`](dotnet-new.md)
- [`dotnet build`](dotnet-build.md)
- [`dotnet build-server`](dotnet-build-server.md)
- [`dotnet run`](dotnet-run.md)
- [`dotnet test`](dotnet-test.md)
- [`dotnet publish`](dotnet-publish.md)
- [`dotnet pack`](dotnet-pack.md)

대부분의 경우 더 이상 `dotnet restore` 명령을 명시적으로 사용할 필요가 없습니다.

때때로 `dotnet restore`를 암시적으로 실행하는 것이 불편할 수 있습니다. 예를 들어 빌드 시스템과 같은 자동화된 일부 시스템은 네트워크 사용량을 제어할 수 있도록 복원이 발생하는 경우를 제어하기 위해 명시적으로 `dotnet restore`를 호출해야 합니다. `dotnet restore`가 암시적으로 실행되지 않게 하려면 이러한 명령 중 하나와 함께 `--no-restore` 플래그를 사용하여 암시적 복원을 사용하지 않도록 설정하면 됩니다.

## <a name="arguments"></a>인수

`ROOT`

프로젝트 파일을 복원하는 선택적 경로입니다.

## <a name="options"></a>옵션

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--configfile <FILE>`

복원 작업에 사용할 NuGet 구성 파일(*NuGet.config*)입니다.

`--disable-parallel`

여러 프로젝트를 병렬로 복원을 사용하지 않도록 설정합니다.

`--force`

마지막 복원이 성공한 경우에도 모든 종속성을 강제 확인합니다. 이 플래그를 지정하는 것은 *project.assets.json* 파일을 삭제하는 것과 같습니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--ignore-failed-sources`

버전 요구 사항을 충족하는 패키지가 있는 경우 실패한 소스에 대해서만 경고합니다.

`--no-cache`

패키지 및 HTTP 요청을 캐시하지 하도록 지정합니다.

`--no-dependencies`

프로젝트 간(P2P) 참조를 사용하여 프로젝트를 복원할 경우 참조가 아닌 루트 프로젝트를 복원하세요.

`--packages <PACKAGES_DIRECTORY>`

복원된 패키지에 대한 디렉터리를 지정합니다.

`-r|--runtime <RUNTIME_IDENTIFIER>`

패키지 복원의 런타임을 지정합니다. *.csproj* 파일의 `<RuntimeIdentifiers>` 태그에 명시적으로 나열되지 않은 런타임의 패키지를 복원하는 데 사용됩니다. RID(런타임 식별자) 목록은 [RID 카탈로그](../rid-catalog.md)를 참조하세요. 이 옵션을 여러 번 지정하여 여러 RID를 제공합니다.

`-s|--source <SOURCE>`

복원 작업 중 사용할 NuGet 패키지 소스를 지정합니다. 이 설정은 *nuget.config* 파일에 지정된 모든 소스를 재정의합니다. 이 옵션을 여러 번 지정하여 여러 소스를 제공할 수 있습니다.

`--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다. 기본값은 `minimal`여야 합니다.

`--interactive`

명령이 중지되고 사용자 입력 또는 작업을 대기할 수 있도록 허용합니다(예: 인증 완료). .NET Core 2.1.400 이후입니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--configfile <FILE>`

복원 작업에 사용할 NuGet 구성 파일(*NuGet.config*)입니다.

`--disable-parallel`

여러 프로젝트를 병렬로 복원을 사용하지 않도록 설정합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--ignore-failed-sources`

버전 요구 사항을 충족하는 패키지가 있는 경우 실패한 소스에 대해서만 경고합니다.

`--no-cache`

패키지 및 HTTP 요청을 캐시하지 하도록 지정합니다.

`--no-dependencies`

프로젝트 간(P2P) 참조를 사용하여 프로젝트를 복원할 경우 참조가 아닌 루트 프로젝트를 복원하세요.

`--packages <PACKAGES_DIRECTORY>`

복원된 패키지에 대한 디렉터리를 지정합니다.

`-r|--runtime <RUNTIME_IDENTIFIER>`

패키지 복원의 런타임을 지정합니다. *.csproj* 파일의 `<RuntimeIdentifiers>` 태그에 명시적으로 나열되지 않은 런타임의 패키지를 복원하는 데 사용됩니다. RID(런타임 식별자) 목록은 [RID 카탈로그](../rid-catalog.md)를 참조하세요. 이 옵션을 여러 번 지정하여 여러 RID를 제공합니다.

`-s|--source <SOURCE>`

복원 작업 중 사용할 NuGet 패키지 소스를 지정합니다. 그러면 *nuget.config* 파일에서 지정된 모든 소스가 재정의되고, 사실상 `<packageSource>` 요소가 없는 것처럼 *nuget.config* 파일을 읽습니다. 이 옵션을 여러 번 지정하여 여러 소스를 제공할 수 있습니다.

`--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다. 기본값은 `minimal`입니다.

---

## <a name="examples"></a>예

현재 디렉터리에 있는 프로젝트에 대한 종속성 및 도구를 복원합니다.

`dotnet restore`

지정된 경로에 있는 `app1` 프로젝트에 대한 종속성 및 도구를 복원합니다.

`dotnet restore ~/projects/app1/app1.csproj`

소스로 제공된 파일 경로를 사용하여 현재 디렉터리에 있는 프로젝트에 대한 종속성 및 도구를 복원합니다.

`dotnet restore -s c:\packages\mypackages`

소스로 제공된 2개의 파일 경로를 사용하여 현재 디렉터리에 있는 프로젝트에 대한 종속성 및 도구를 복원합니다.

`dotnet restore -s c:\packages\mypackages -s c:\packages\myotherpackages`

자세한 출력을 표시하는 현재 디렉터리에 있는 프로젝트에 대한 종속성 및 도구를 복원합니다.

`dotnet restore --verbosity detailed`
