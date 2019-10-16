---
title: dotnet run 명령
description: dotnet run 명령은 소스 코드에서 애플리케이션을 실행하는 편리한 옵션을 제공합니다.
ms.date: 05/29/2018
ms.openlocfilehash: ec2a24b78f435dd1905ec67b6f3f4a4ec3f7e7fa
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117479"
---
# <a name="dotnet-run"></a>dotnet run

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet run` - 명시적 컴파일이나 시작 명령을 사용하지 않고 소스 코드를 실행합니다.

## <a name="synopsis"></a>개요

<!-- markdownlint-disable MD025 -->

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [-v|--verbosity] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]]
dotnet run [-h|--help]
```

---

## <a name="description"></a>설명

`dotnet run` 명령은 하나의 명령을 사용하여 소스 코드에서 애플리케이션을 실행하는 편리한 옵션을 제공합니다. 명령줄에서 빠른 반복 개발에 유용합니다. 이 명령은 코드 빌드 시 [`dotnet build`](dotnet-build.md) 명령에 의존합니다. 프로젝트를 먼저 복원해야 하는 등, 빌드에 대한 요구 사항은 `dotnet run`에도 적용됩니다.

출력 파일은 기본 위치, 즉 `bin/<configuration>/<target>`에 기록됩니다. 예를 들어 `netcoreapp2.1` 애플리케이션이 있고 `dotnet run`을 실행하는 경우 출력은 `bin/Debug/netcoreapp2.1`에 추가됩니다. 필요에 따라 파일을 덮어씁니다. 임시 파일은 `obj` 디렉터리에 놓입니다.

프로젝트가 여러 프레임워크를 지정하는 경우 프레임워크를 지정하는 데 `-f|--framework <FRAMEWORK>` 옵션을 사용하지 않은 한, `dotnet run`을 실행하면 오류가 발생합니다.

`dotnet run` 명령은 빌드된 어셈블리가 아닌 프로젝트의 컨텍스트에서 사용됩니다. 대신 프레임워크 종속 애플리케이션 DLL을 실행하려고 하는 경우 명령 없이 [dotnet](dotnet.md)을 사용해야 합니다. 예를 들어 `myapp.dll`을 실행하려면 다음을 사용합니다.

```dotnetcli
dotnet myapp.dll
```

`dotnet` 드라이버에 대한 자세한 내용은 [.NET Core 명령줄 도구(CLI)](index.md) 항목을 참조하세요.

애플리케이션을 실행하기 위해 `dotnet run` 명령은 NuGet 캐시에서 공유 런타임의 외부에 있는 애플리케이션의 종속성을 확인합니다. 캐시된 종속성을 사용하기 때문에 프로덕션 환경에서 애플리케이션을 실행하는 데 `dotnet run`을 사용하는 것은 바람직하지 않습니다. 대신, [`dotnet publish`](dotnet-publish.md) 명령을 사용하여 [배포를 만들고](../deploying/index.md) 게시된 출력을 배포합니다.

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="options"></a>옵션

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--`

실행 중인 애플리케이션에 대한 인수에서 `dotnet run`에 대한 인수를 구분합니다. 이 구분 기호 다음의 모든 인수가 실행 중인 애플리케이션에 전달됩니다.

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`입니다.

`-f|--framework <FRAMEWORK>`

지정된 [프레임워크](../../standard/frameworks.md)를 사용하여 앱을 빌드하고 실행합니다. 프레임워크는 프로젝트 파일에 지정되어야 합니다.

`--force`

마지막 복원이 성공한 경우에도 모든 종속성을 강제 확인합니다. 이 플래그를 지정하는 것은 *project.assets.json* 파일을 삭제하는 것과 같습니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--launch-profile <NAME>`

애플리케이션을 시작할 때 사용할 시작 프로필(있는 경우)의 이름입니다. 시작 프로필은 *launchSettings.json* 파일에서 정의되고 일반적으로 `Development`, `Staging` 및 `Production`이라고 합니다. 자세한 내용은 [여러 환경 사용](/aspnet/core/fundamentals/environments)을 참조하세요.

`--no-build`

실행하기 전에 프로젝트를 빌드하지 않습니다. 또한 `--no-restore` 플래그를 암시적으로 설정합니다.

`--no-dependencies`

프로젝트 간(P2P) 참조를 사용하여 프로젝트를 복원할 경우 참조가 아닌 루트 프로젝트를 복원하세요.

`--no-launch-profile`

애플리케이션을 구성하는 데 *launchSettings.json*을 사용하지 않습니다.

`--no-restore`

명령을 실행할 때 암시적 복원을 실행하지 않습니다.

`-p|--project <PATH>`

실행할 프로젝트 파일의 경로를 지정합니다(폴더 이름 또는 전체 경로). 지정하지 않으면 현재 디렉터리로 기본 설정됩니다.

`--runtime <RUNTIME_IDENTIFIER>`

패키지를 복원할 대상 런타임을 지정합니다. RID(런타임 식별자) 목록은 [RID 카탈로그](../rid-catalog.md)를 참조하세요.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--`

실행 중인 애플리케이션에 대한 인수에서 `dotnet run`에 대한 인수를 구분합니다. 이 구분 기호 다음의 모든 인수가 실행 중인 애플리케이션에 전달됩니다.

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`입니다.

`-f|--framework <FRAMEWORK>`

지정된 [프레임워크](../../standard/frameworks.md)를 사용하여 앱을 빌드하고 실행합니다. 프레임워크는 프로젝트 파일에 지정되어야 합니다.

`--force`

마지막 복원이 성공한 경우에도 모든 종속성을 강제 확인합니다. 이 플래그를 지정하는 것은 *project.assets.json* 파일을 삭제하는 것과 같습니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--launch-profile <NAME>`

애플리케이션을 시작할 때 사용할 시작 프로필(있는 경우)의 이름입니다. 시작 프로필은 *launchSettings.json* 파일에서 정의되고 일반적으로 `Development`, `Staging` 및 `Production`이라고 합니다. 자세한 내용은 [여러 환경 사용](/aspnet/core/fundamentals/environments)을 참조하세요.

`--no-build`

실행하기 전에 프로젝트를 빌드하지 않습니다. 또한 `--no-restore` 플래그를 암시적으로 설정합니다.

`--no-dependencies`

프로젝트 간(P2P) 참조를 사용하여 프로젝트를 복원할 경우 참조가 아닌 루트 프로젝트를 복원하세요.

`--no-launch-profile`

애플리케이션을 구성하는 데 *launchSettings.json*을 사용하지 않습니다.

`--no-restore`

명령을 실행할 때 암시적 복원을 실행하지 않습니다.

`-p|--project <PATH>`

실행할 프로젝트 파일의 경로를 지정합니다(폴더 이름 또는 전체 경로). 지정하지 않으면 현재 디렉터리로 기본 설정됩니다.

`--runtime <RUNTIME_IDENTIFIER>`

패키지를 복원할 대상 런타임을 지정합니다. RID(런타임 식별자) 목록은 [RID 카탈로그](../rid-catalog.md)를 참조하세요.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--`

실행 중인 애플리케이션에 대한 인수에서 `dotnet run`에 대한 인수를 구분합니다. 이 구분 기호 다음의 모든 인수가 실행 중인 애플리케이션에 전달됩니다.

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`입니다.

`-f|--framework <FRAMEWORK>`

지정된 [프레임워크](../../standard/frameworks.md)를 사용하여 앱을 빌드하고 실행합니다. 프레임워크는 프로젝트 파일에 지정되어야 합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-p|--project <PATH/PROJECT.csproj>`

프로젝트 파일의 경로 및 이름을 지정합니다. (참고 참조) 지정하지 않으면 현재 디렉터리로 기본 설정됩니다.

> [!NOTE]
> `-p|--project` 옵션과 함께 프로젝트 파일의 경로와 이름을 사용합니다. CLI의 재발로 인해 폴더 경로에 .NET Core SDK 1.x를 제공할 수 없습니다. 이 문제에 대한 자세한 내용은 [dotnet run -p, can not start a project (dotnet/cli #5992)](https://github.com/dotnet/cli/issues/5992)(dotnet run -p로 프로젝트를 시작할 수 없음(dotnet/cli #5992))를 참조하세요.

---

## <a name="examples"></a>예제

현재 디렉터리에 있는 프로젝트를 실행합니다.

`dotnet run`

지정된 프로젝트를 실행합니다.

`dotnet run --project ./projects/proj1/proj1.csproj`

현재 디렉터리에 있는 프로젝트를 실행합니다. 비어 있는 `--` 옵션을 사용하므로 이 예제의 `--help` 인수는 애플리케이션에 전달됩니다.

`dotnet run --configuration Release -- --help`

최소 출력만을 표시하는 현재 디렉터리에 프로젝트에 대한 종속성 및 도구를 저장한 다음, 프로젝트를 실행합니다(.NET Core SDK 2.0 이상 버전).

`dotnet run --verbosity m`
