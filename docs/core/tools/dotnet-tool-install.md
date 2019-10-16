---
title: dotnet tool install 명령
description: dotnet tool install 명령은 컴퓨터에 지정한 .NET Core Global 도구를 설치합니다.
ms.date: 05/29/2018
ms.openlocfilehash: d6f691117e93a39c9837b282dca19e452515c80a
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117470"
---
# <a name="dotnet-tool-install"></a>dotnet tool install

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool install` - 컴퓨터에 지정된 [.NET Core Global 도구](global-tools.md)를 설치합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet tool install <PACKAGE_NAME> <-g|--global> [--add-source] [--configfile] [--framework] [-v|--verbosity] [--version]
dotnet tool install <PACKAGE_NAME> <--tool-path> [--add-source] [--configfile] [--framework] [-v|--verbosity] [--version]
dotnet tool install <-h|--help>
```

## <a name="description"></a>설명

`dotnet tool install` 명령은 컴퓨터에서 .NET Core Global 도구를 설치하는 방법을 제공합니다. 이 명령을 사용하려면 `--global` 옵션을 사용하여 사용자 전체 설치를 원한다고 지 정하거나 `--tool-path` 옵션을 사용하여 도구를 설치할 경로를 지정해야 합니다.

전역 도구는 `-g`(또는 `--global`) 옵션을 지정할 때 기본적으로 다음 디렉터리에 설치됩니다.

| OS          | 경로                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

## <a name="arguments"></a>인수

`PACKAGE_NAME`

설치할 .NET Core Global 도구를 포함하는 NuGet 패키지의 이름/ID입니다.

## <a name="options"></a>옵션

`--add-source <SOURCE>`

설치 중에 사용할 추가 NuGet 패키지 원본을 추가합니다.

`--configfile <FILE>`

사용할 NuGet 구성(*nuget.config*) 파일입니다.

`--framework <FRAMEWORK>`

도구를 설치할 [대상 프레임워크](../../standard/frameworks.md)를 지정합니다. 기본적으로 .NET Core SDK는 가장 적합한 대상 프레임워크를 선택하도록 시도합니다.

`-g|--global`

사용자 전체 설치임을 지정합니다. `--tool-path` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--tool-path` 옵션을 지정해야 합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--tool-path <PATH>`

전역 도구를 설치할 위치를 지정합니다. 경로는 절대 또는 상대 경로일 수 있습니다. 경로가 존재하지 않는 경우 이 명령은 해당 경로를 만들려고 합니다. `--global` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--global` 옵션을 지정해야 합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

`--version <VERSION_NUMBER>`

설치할 도구의 버전입니다. 기본적으로 안정적인 최신 버전이 설치됩니다. 도구의 미리 보기 또는 이전 버전을 설치할 경우 이 옵션을 사용합니다.

## <a name="examples"></a>예제

기본 위치에 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 전역 도구를 설치합니다.

`dotnet tool install -g dotnetsay`

특정 Windows 폴더에서 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 전역 도구를 설치합니다.

`dotnet tool install dotnetsay --tool-path c:\global-tools`

특정 Linux/macOS 폴더에서 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 전역 도구를 설치합니다.

`dotnet tool install dotnetsay --tool-path ~/bin`

[dotnetsay](https://www.nuget.org/packages/dotnetsay/) 전역 도구 버전 2.0.0을 설치합니다.

`dotnet tool install -g dotnetsay --version 2.0.0`

## <a name="see-also"></a>참고 항목

- [.NET Core Global Tool](global-tools.md)
