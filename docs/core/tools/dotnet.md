---
title: dotnet 명령
description: dotnet 명령(.NET Core CLI 도구에 대한 일반 드라이버) 및 사용법에 대해 알아봅니다.
ms.date: 06/04/2018
ms.openlocfilehash: a22340c26ca2e483e43857e2ecb31f2ab53b60f4
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117512"
---
# <a name="dotnet-command"></a>dotnet 명령

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet` - .NET 소스 코드 및 이진 파일을 관리하기 위한 도구입니다.

## <a name="synopsis"></a>개요

<!-- markdownlint-disable MD025 -->

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```dotnetcli
dotnet [command] [arguments] [--additional-deps] [--additionalprobingpath] [--depsfile]
    [-d|--diagnostics] [--fx-version] [-h|--help] [--info] [--list-runtimes] [--list-sdks] [--roll-forward-on-no-candidate-fx] [--runtimeconfig] [-v|--verbosity] [--version]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```dotnetcli
dotnet [command] [arguments] [--additional-deps] [--additionalprobingpath] [--depsfile]
    [-d|--diagnostics] [--fx-version] [-h|--help] [--info] [--roll-forward-on-no-candidate-fx]
    [--runtimeconfig] [-v|--verbosity] [--version]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```dotnetcli
dotnet [command] [arguments] [--additionalprobingpath] [--depsfile] [-d|--diagnostics]
    [--fx-version] [-h|--help] [--info] [--runtimeconfig] [-v|--verbosity] [--version]
```

---

## <a name="description"></a>설명

`dotnet`은 .NET 소스 코드 및 이진 파일을 관리하기 위한 도구입니다. [`dotnet build`](dotnet-build.md) 및 [`dotnet run`](dotnet-run.md)와 같은 특정 작업을 수행하는 명령을 표시합니다. 각 명령은 자체 인수를 정의합니다. 각 명령 다음에 `--help`를 입력하면 간단한 도움말 설명서에 액세스할 수 있습니다.

`dotnet`은 `dotnet myapp.dll`과 같은 애플리케이션 DLL을 지정하여 애플리케이션을 실행하는 데 사용할 수 있습니다. 배포 옵션에 대해 자세히 알아보려면 [.NET Core 애플리케이션 배포](../deploying/index.md)를 참조하세요.

## <a name="options"></a>옵션

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--additional-deps <PATH>`

추가적인 *.deps.json* 파일의 경로입니다.

`--additionalprobingpath <PATH>`

검색 정책 및 검색할 어셈블리를 포함하는 경로입니다.

`--depsfile`

*deps.json* 파일의 경로입니다.

*deps.json* 파일에는 어셈블리 충돌을 해결하는 데 사용되는 종속성, 컴파일 종속성 및 버전 정보 목록이 포함됩니다. 이 파일에 대한 자세한 내용은 GitHub에서 [런타임 구성 파일](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)을 참조하세요.

`-d|--diagnostics`

진단 출력을 사용합니다.

`--fx-version <VERSION>`

애플리케이션 실행에 사용할 .NET Core 런타임의 버전입니다.

`-h|--help`

`dotnet build --help`와 같은 지정된 명령에 대한 설명서를 인쇄합니다. `dotnet --help`는 사용 가능한 명령 목록을 인쇄합니다.

`--info`

.NET Core 설치 및 머신 환경(예: 현재 운영 체제)에 대한 자세한 정보를 인쇄하고 .NET Core 버전의 SHA를 커밋합니다.

`--list-runtimes`

설치된 .NET Core 런타임을 표시합니다.

`--list-sdks`

설치된 .NET Core SDK를 표시합니다.

`--roll-forward-on-no-candidate-fx <N>`

필요한 공유 프레임워크를 사용할 수 없을 때 동작을 정의합니다. `N`는 다음이 될 수 있습니다.

- `0` - 부 버전 롤포워드도 사용하지 않도록 설정합니다.
- `1` - 부 버전에서는 롤포워드하지만 주 버전에서는 롤포워드하지 않습니다. 이것은 기본적인 동작입니다.
- `2` - 부 버전과 주 버전에서 롤포워드합니다.

 자세한 내용은 [롤포워드](../whats-new/dotnet-core-2-1.md#roll-forward)를 참조하세요.

`--runtimeconfig`

*runtimeconfig.json* 파일의 경로입니다.

*runtimeconfig.json* 파일은 런타임 구성 설정을 포함하는 구성 파일입니다. 자세한 내용은 GitHub에서 [런타임 구성 파일](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)을 참조하세요.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다. 모든 명령에서 지원되지 않습니다. 이 옵션을 사용할 수 있는지 확인하려면 특정 명령 페이지를 참조하세요.

`--version`

사용 중인 .NET Core SDK 버전을 출력합니다.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--additional-deps <PATH>`

추가적인 *.deps.json* 파일의 경로입니다.

`--additionalprobingpath <PATH>`

검색 정책 및 검색할 어셈블리를 포함하는 경로입니다.

`--depsfile`

*deps.json* 파일의 경로입니다.

*deps.json* 파일에는 어셈블리 충돌을 해결하는 데 사용되는 종속성, 컴파일 종속성 및 버전 정보 목록이 포함됩니다. 이 파일에 대한 자세한 내용은 [GitHub에서 런타임 구성 파일](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)을 참조하세요.

`-d|--diagnostics`

진단 출력을 사용합니다.

`--fx-version <VERSION>`

애플리케이션 실행에 사용할 .NET Core 런타임의 버전입니다.

`-h|--help`

`dotnet build --help`와 같은 지정된 명령에 대한 설명서를 인쇄합니다. `dotnet --help`는 사용 가능한 명령 목록을 인쇄합니다.

`--info`

.NET Core 설치 및 머신 환경(예: 현재 운영 체제)에 대한 자세한 정보를 인쇄하고 .NET Core 버전의 SHA를 커밋합니다.

`--roll-forward-on-no-candidate-fx`

 `0`으로 설정된 경우 부 버전 롤포워드를 사용하지 않도록 설정합니다. 자세한 내용은 [롤포워드](../whats-new/dotnet-core-2-1.md#roll-forward)를 참조하세요.

`--runtimeconfig`

*runtimeconfig.json* 파일의 경로입니다.

*runtimeconfig.json* 파일은 런타임 구성 설정을 포함하는 구성 파일입니다. 자세한 내용은 [GitHub에서 런타임 구성 파일](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)을 참조하세요.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다. 모든 명령에서 지원되지 않습니다. 이 옵션을 사용할 수 있는지 확인하려면 특정 명령 페이지를 참조하세요.

`--version`

사용 중인 .NET Core SDK 버전을 출력합니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--additionalprobingpath <PATH>`

검색 정책 및 검색할 어셈블리를 포함하는 경로입니다.

`--depsfile`

*deps.json* 파일의 경로입니다.

*deps.json* 파일에는 어셈블리 충돌을 해결하는 데 사용되는 종속성, 컴파일 종속성 및 버전 정보 목록이 포함됩니다. 이 파일에 대한 자세한 내용은 [GitHub에서 런타임 구성 파일](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)을 참조하세요.

`-d|--diagnostics`

진단 출력을 사용합니다.

`--fx-version <VERSION>`

애플리케이션 실행에 사용할 .NET Core 런타임의 버전입니다.

`-h|--help`

`dotnet build --help`와 같은 지정된 명령에 대한 설명서를 인쇄합니다. `dotnet --help`는 사용 가능한 명령 목록을 인쇄합니다.

`--info`

.NET Core 설치 및 머신 환경(예: 현재 운영 체제)에 대한 자세한 정보를 인쇄하고 .NET Core 버전의 SHA를 커밋합니다.

`--runtimeconfig`

*runtimeconfig.json* 파일의 경로입니다.

*runtimeconfig.json* 파일은 런타임 구성 설정을 포함하는 구성 파일입니다. 자세한 내용은 [GitHub에서 런타임 구성 파일](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)을 참조하세요.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다. 모든 명령에서 지원되지 않습니다. 이 옵션을 사용할 수 있는지 확인하려면 특정 명령 페이지를 참조하세요.

`--version`

사용 중인 .NET Core SDK 버전을 출력합니다.

---

## <a name="dotnet-commands"></a>dotnet 명령

### <a name="general"></a>일반

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

| 명령                                       | 함수                                                            |
| --------------------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)               | .NET Core 애플리케이션을 빌드합니다.                                     |
| [dotnet build-server](dotnet-build-server.md) | 빌드에서 시작된 서버와 상호 작용합니다.                          |
| [dotnet clean](dotnet-clean.md)               | 빌드 출력을 정리합니다.                                                |
| [dotnet help](dotnet-help.md)                 | 명령에 대한 자세한 온라인 설명서를 표시합니다.           |
| [dotnet migrate](dotnet-migrate.md)           | 유효한 Preview 2 프로젝트를 .NET Core SDK 1.0 프로젝트로 마이그레이션합니다.  |
| [dotnet msbuild](dotnet-msbuild.md)           | MSBuild 명령줄에 대한 액세스 권한을 제공합니다.                        |
| [dotnet new](dotnet-new.md)                   | 지정한 템플릿에 대해 C# 또는 F# 프로젝트를 초기화합니다.                |
| [dotnet pack](dotnet-pack.md)                 | 코드의 NuGet 패키지를 만듭니다.                               |
| [dotnet publish](dotnet-publish.md)           | .NET Framework 종속형 또는 자체 포함 애플리케이션을 게시합니다. |
| [dotnet restore](dotnet-restore.md)           | 지정된 애플리케이션에 대한 종속성을 복원합니다.                  |
| [dotnet run](dotnet-run.md)                   | 소스에서 애플리케이션을 실행합니다.                                   |
| [dotnet sln](dotnet-sln.md)                   | 솔루션 파일에 프로젝트를 추가, 제거 및 나열하는 옵션입니다.       |
| [dotnet store](dotnet-store.md)               | 어셈블리를 런타임 패키지 저장소에 저장합니다.                     |
| [dotnet test](dotnet-test.md)                 | Test Runner를 사용하여 테스트를 실행합니다.                                     |

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

| 명령                             | 함수                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | .NET Core 애플리케이션을 빌드합니다.                                     |
| [dotnet clean](dotnet-clean.md)     | 빌드 출력을 정리합니다.                                              |
| [dotnet help](dotnet-help.md)       | 명령에 대한 자세한 온라인 설명서를 표시합니다.           |
| [dotnet migrate](dotnet-migrate.md) | 유효한 Preview 2 프로젝트를 .NET Core SDK 1.0 프로젝트로 마이그레이션합니다.  |
| [dotnet msbuild](dotnet-msbuild.md) | MSBuild 명령줄에 대한 액세스 권한을 제공합니다.                        |
| [dotnet new](dotnet-new.md)         | 지정한 템플릿에 대해 C# 또는 F# 프로젝트를 초기화합니다.                |
| [dotnet pack](dotnet-pack.md)       | 코드의 NuGet 패키지를 만듭니다.                               |
| [dotnet publish](dotnet-publish.md) | .NET Framework 종속형 또는 자체 포함 애플리케이션을 게시합니다. |
| [dotnet restore](dotnet-restore.md) | 지정된 애플리케이션에 대한 종속성을 복원합니다.                  |
| [dotnet run](dotnet-run.md)         | 소스에서 애플리케이션을 실행합니다.                                   |
| [dotnet sln](dotnet-sln.md)         | 솔루션 파일에 프로젝트를 추가, 제거 및 나열하는 옵션입니다.       |
| [dotnet store](dotnet-store.md)     | 어셈블리를 런타임 패키지 저장소에 저장합니다.                     |
| [dotnet test](dotnet-test.md)       | Test Runner를 사용하여 테스트를 실행합니다.                                     |

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

| 명령                             | 함수                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | .NET Core 애플리케이션을 빌드합니다.                                     |
| [dotnet clean](dotnet-clean.md)     | 빌드 출력을 정리합니다.                                              |
| [dotnet migrate](dotnet-migrate.md) | 유효한 Preview 2 프로젝트를 .NET Core SDK 1.0 프로젝트로 마이그레이션합니다.  |
| [dotnet msbuild](dotnet-msbuild.md) | MSBuild 명령줄에 대한 액세스 권한을 제공합니다.                        |
| [dotnet new](dotnet-new.md)         | 지정한 템플릿에 대해 C# 또는 F# 프로젝트를 초기화합니다.                |
| [dotnet pack](dotnet-pack.md)       | 코드의 NuGet 패키지를 만듭니다.                               |
| [dotnet publish](dotnet-publish.md) | .NET Framework 종속형 또는 자체 포함 애플리케이션을 게시합니다. |
| [dotnet restore](dotnet-restore.md) | 지정된 애플리케이션에 대한 종속성을 복원합니다.                  |
| [dotnet run](dotnet-run.md)         | 소스에서 애플리케이션을 실행합니다.                                   |
| [dotnet sln](dotnet-sln.md)         | 솔루션 파일에 프로젝트를 추가, 제거 및 나열하는 옵션입니다.       |
| [dotnet test](dotnet-test.md)       | Test Runner를 사용하여 테스트를 실행합니다.                                     |

---

### <a name="project-references"></a>프로젝트 참조

명령 | 함수
--- | ---
[dotnet add reference](dotnet-add-reference.md) | 프로젝트 참조를 추가합니다.
[dotnet list reference](dotnet-list-reference.md) | 프로젝트 참조를 나열합니다.
[dotnet remove reference](dotnet-remove-reference.md) | 프로젝트 참조를 제거합니다.

### <a name="nuget-packages"></a>NuGet 패키지

명령 | 함수
--- | ---
[dotnet add package](dotnet-add-package.md) | NuGet 패키지를 추가합니다.
[dotnet remove package](dotnet-remove-package.md) | NuGet 패키지를 제거합니다.

### <a name="nuget-commands"></a>NuGet 명령

명령 | 함수
--- | ---
[dotnet nuget delete](dotnet-nuget-delete.md) | 서버에서 패키지를 삭제하거나 목록에서 제거합니다.
[dotnet nuget locals](dotnet-nuget-locals.md) | http-request 캐시, 임시 캐시 또는 시스템 전체의 글로벌 패키지 폴더와 같은 로컬 NuGet 리소스를 지우거나 목록에 포함합니다.
[dotnet nuget push](dotnet-nuget-push.md) | 서버에 패키지를 푸시하고 게시합니다.

### <a name="global-tools-commands"></a>전역 도구 명령

[.NET Core 전역 도구](global-tools.md)는 .NET Core SDK 2.1.300부터 사용할 수 있습니다.

명령 | 함수
--- | ---
[dotnet tool install](dotnet-tool-install.md) | 컴퓨터에 전역 도구를 설치합니다.
[dotnet tool list](dotnet-tool-list.md) | 컴퓨터의 기본 디렉터리 또는 지정된 경로에 현재 설치된 모든 전역 도구를 나열합니다.
[dotnet tool uninstall](dotnet-tool-uninstall.md) | 컴퓨터에서 전역 도구를 제거합니다.
[dotnet tool update](dotnet-tool-update.md) | 컴퓨터에서 전역 도구를 업데이트합니다.

### <a name="additional-tools"></a>추가 도구

.NET Core SDK 2.1.300부터는 `DotnetCliToolReference`을 사용하여 프로젝트별로만 사용할 수 있었던 여러 도구를 .NET Core SDK의 일부로 사용할 수 있습니다. 이러한 도구는 다음 표에 나열되어 있습니다.

| 도구                                              | 함수                                                     |
| ------------------------------------------------- | ------------------------------------------------------------ |
| dev-certs                                         | 개발 인증서를 만들고 관리합니다.                |
| [ef](/ef/core/miscellaneous/cli/dotnet)           | Entity Framework Core 명령줄 도구입니다.                    |
| sql-cache                                         | SQL Server 캐시 명령줄 도구입니다.                         |
| [user-secrets](/aspnet/core/security/app-secrets) | 개발 사용자 비밀을 관리합니다.                            |
| [watch](/aspnet/core/tutorials/dotnet-watch)      | 파일이 변경될 때 명령을 실행하는 파일 감시자를 시작합니다. |

각 도구에 대한 자세한 내용을 보려면 `dotnet <tool-name> --help`를 입력합니다.

## <a name="examples"></a>예제

새 .NET Core 콘솔 애플리케이션을 만듭니다.

`dotnet new console`

지정된 애플리케이션에 대한 종속성을 복원합니다.

`dotnet restore`

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

지정된 디렉터리에서 프로젝트 및 해당 종속성을 빌드합니다.

`dotnet build`

`myapp.dll`과 같은 애플리케이션 DLL을 실행합니다.

`dotnet myapp.dll`

## <a name="environment-variables"></a>환경 변수

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`DOTNET_PACKAGES`

글로벌 패키지 폴더입니다. 설정하지 않으면 기본적으로 Unix에서는 `~/.nuget/packages`, Windows에서는 `%userprofile%\.nuget\packages`로 지정됩니다.

`DOTNET_SERVICING`

런타임을 로드할 때 공유 호스트에서 사용할 서비스 인덱스의 위치를 지정합니다.

`DOTNET_CLI_TELEMETRY_OPTOUT`

.NET Core 도구 사용에 대한 데이터를 수집하여 Microsoft에 전송할지 여부를 지정합니다. 원격 분석 기능을 옵트아웃하려면 `true`로 설정합니다(값 `true`, `1` 또는 `yes`가 허용됨). 이외의 경우 원격 분석 기능을 옵트인하려면 `false`로 설정합니다(`false`, `0` 또는 `no`가 허용됨). 설정하지 않으면 기본적으로 `false`이고 원격 분석 기능은 활성화됩니다.

`DOTNET_MULTILEVEL_LOOKUP`

전역 위치에서 .NET Core 런타임, 공유 프레임워크 또는 SDK가 확인되는지 여부를 지정합니다. 설정하지 않은 경우 기본값은 `true`입니다. 전역 위치에서 확인하지 않고 격리된 .NET Core 설치를 가지려면 `false`로 설정합니다(값 `0` 또는 `false`는 허용됨). 다중 수준의 조회에 대한 자세한 내용은 [다중 수준 SharedFX 조회](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/multilevel-sharedfx-lookup.md)를 참조하세요.

`DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX`

`0`으로 설정된 경우 부 버전 롤포워드를 사용하지 않도록 설정합니다. 자세한 내용은 [롤포워드](../whats-new/dotnet-core-2-1.md#roll-forward)를 참조하세요.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`DOTNET_PACKAGES`

주 패키지 캐시입니다. 설정하지 않으면 기본적으로 Unix에서는 `$HOME/.nuget/packages`, Windows에서는 `%userprofile%\.nuget\packages`로 지정됩니다.

`DOTNET_SERVICING`

런타임을 로드할 때 공유 호스트에서 사용할 서비스 인덱스의 위치를 지정합니다.

`DOTNET_CLI_TELEMETRY_OPTOUT`

.NET Core 도구 사용에 대한 데이터를 수집하여 Microsoft에 전송할지 여부를 지정합니다. 원격 분석 기능을 옵트아웃하려면 `true`로 설정합니다(값 `true`, `1` 또는 `yes`가 허용됨). 이외의 경우 원격 분석 기능을 옵트인하려면 `false`로 설정합니다(`false`, `0` 또는 `no`가 허용됨). 설정하지 않으면 기본적으로 `false`이고 원격 분석 기능은 활성화됩니다.

`DOTNET_MULTILEVEL_LOOKUP`

전역 위치에서 .NET Core 런타임, 공유 프레임워크 또는 SDK가 확인되는지 여부를 지정합니다. 설정하지 않은 경우 기본값은 `true`입니다. 전역 위치에서 확인하지 않고 격리된 .NET Core 설치를 가지려면 `false`로 설정합니다(값 `0` 또는 `false`는 허용됨). 다중 수준의 조회에 대한 자세한 내용은 [다중 수준 SharedFX 조회](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/multilevel-sharedfx-lookup.md)를 참조하세요.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`DOTNET_PACKAGES`

주 패키지 캐시입니다. 설정하지 않으면 기본적으로 Unix에서는 `$HOME/.nuget/packages`, Windows에서는 `%userprofile%\.nuget\packages`로 지정됩니다.

`DOTNET_SERVICING`

런타임을 로드할 때 공유 호스트에서 사용할 서비스 인덱스의 위치를 지정합니다.

`DOTNET_CLI_TELEMETRY_OPTOUT`

.NET Core 도구 사용에 대한 데이터를 수집하여 Microsoft에 전송할지 여부를 지정합니다. 원격 분석 기능을 옵트아웃하려면 `true`로 설정합니다(값 `true`, `1` 또는 `yes`가 허용됨). 이외의 경우 원격 분석 기능을 옵트인하려면 `false`로 설정합니다(`false`, `0` 또는 `no`가 허용됨). 설정하지 않으면 기본적으로 `false`이고 원격 분석 기능은 활성화됩니다.

---

## <a name="see-also"></a>참고 항목

- [런타임 구성 파일](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)
