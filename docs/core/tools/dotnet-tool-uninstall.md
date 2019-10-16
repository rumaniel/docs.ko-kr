---
title: dotnet tool uninstall 명령
description: dotnet tool uninstall 명령은 컴퓨터에서 지정한 .NET Core Global Tool을 제거합니다.
ms.date: 05/29/2018
ms.openlocfilehash: 033753f44464e78b826e908e0b6cdf276da8a179
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117547"
---
# <a name="dotnet-tool-uninstall"></a>dotnet tool uninstall

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool uninstall` - 컴퓨터에서 지정된 [.NET Core Global Tool](global-tools.md)을 제거합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet tool uninstall <PACKAGE_NAME> <-g|--global>
dotnet tool uninstall <PACKAGE_NAME> <--tool-path>
dotnet tool uninstall <-h|--help>
```

## <a name="description"></a>설명

`dotnet tool uninstall` 명령은 컴퓨터에서 .NET Core Global Tool을 제거하는 방법을 제공합니다. 이 명령을 사용하려면 `--global` 옵션을 사용하여 사용자 수준 도구를 제거하거나 `--tool-path` 옵션을 사용하여 도구를 설치할 경로를 지정해야 합니다.

## <a name="arguments"></a>인수

`PACKAGE_NAME`

제거할 .NET Core Global Tool을 포함하는 NuGet 패키지의 이름/ID입니다. [dotnet tool list](dotnet-tool-list.md) 명령을 사용하여 패키지 이름을 찾을 수 있습니다.

## <a name="options"></a>옵션

`-g|--global`

사용자 수준 설치에서 제거할 도구임을 지정합니다. `--tool-path` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--tool-path` 옵션을 지정해야 합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--tool-path <PATH>`

Global Tool을 제거할 위치를 지정합니다. PATH는 절대적이거나 상대적일 수 있습니다. `--global` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--global` 옵션을 지정해야 합니다.

## <a name="examples"></a>예제

[dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool을 제거합니다.

`dotnet tool uninstall -g dotnetsay`

특정 Windows 폴더에서 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool을 제거합니다.

`dotnet tool uninstall dotnetsay --tool-path c:\global-tools`

특정 Linux/macOS 폴더에서 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool을 제거합니다.

`dotnet tool uninstall dotnetsay --tool-path ~/bin`

## <a name="see-also"></a>참고 항목

- [.NET Core Global Tool](global-tools.md)
