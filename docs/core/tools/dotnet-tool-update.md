---
title: dotnet tool update 명령
description: dotnet tool update 명령은 컴퓨터에 지정된 .NET Core Global Tool을 업데이트합니다.
ms.date: 05/29/2018
ms.openlocfilehash: b10ce39c8b9d4df23243bcf672454a455e34eec1
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117539"
---
# <a name="dotnet-tool-update"></a>dotnet tool update

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool update` - 컴퓨터에서 지정된 [.NET Core Global Tool](global-tools.md)을 업데이트합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet tool update <PACKAGE_NAME> <-g|--global> [--configfile] [--framework] [-v|--verbosity]
dotnet tool update <PACKAGE_NAME> <--tool-path> [--configfile] [--framework] [-v|--verbosity]
dotnet tool update <-h|--help>
```

## <a name="description"></a>설명

`dotnet tool update` 명령은 컴퓨터의 .NET Core Global Tool을 패키지의 안정적인 최신 버전으로 업데이트하는 방법을 제공합니다. 이 명령은 도구를 제거하고 다시 설치하여 효과적으로 업데이트합니다. 이 명령을 사용하려면 `--global` 옵션을 사용하여 사용자 수준 설치에서 도구를 업데이트하거나 `--tool-path` 옵션을 사용하여 도구를 설치할 경로를 지정해야 합니다.

## <a name="arguments"></a>인수

`PACKAGE_NAME`

업데이트할 .NET Core Global Tool을 포함하는 NuGet 패키지의 이름/ID입니다. [dotnet tool list](dotnet-tool-list.md) 명령을 사용하여 패키지 이름을 찾을 수 있습니다.

## <a name="options"></a>옵션

`--add-source <SOURCE>`

설치 중에 사용할 추가 NuGet 패키지 원본을 추가합니다.

`--configfile <FILE>`

사용할 NuGet 구성(*nuget.config*) 파일입니다.

`--framework <FRAMEWORK>`

도구를 업데이트할 [대상 프레임워크](../../standard/frameworks.md)를 지정합니다.

`-g|--global`

업데이트가 사용자 수준 도구에 대한 것임을 지정합니다. `--tool-path` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--tool-path` 옵션을 지정해야 합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--tool-path <PATH>`

Global Tool이 설치되는 위치를 지정합니다. PATH는 절대적이거나 상대적일 수 있습니다. `--global` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--global` 옵션을 지정해야 합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

## <a name="examples"></a>예제

[dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool을 업데이트합니다.

`dotnet tool update -g dotnetsay`

특정 Windows 폴더에 있는 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool을 업데이트합니다.

`dotnet tool update dotnetsay --tool-path c:\global-tools`

특정 Linux/macOS 폴더에 있는 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool을 업데이트합니다.

`dotnet tool update dotnetsay --tool-path ~/bin`

## <a name="see-also"></a>참고 항목

- [.NET Core Global Tool](global-tools.md)
