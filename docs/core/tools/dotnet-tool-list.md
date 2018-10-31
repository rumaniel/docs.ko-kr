---
title: dotnet tool list 명령 - .NET Core CLI
description: dotnet tool list 명령은 컴퓨터에서 지정한 .NET Core Global Tool을 나열합니다.
author: mairaw
ms.author: mairaw
ms.date: 05/29/2018
ms.openlocfilehash: e2bea974207d3098ed67b69ed16a72a03c44cd8b
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48841244"
---
# <a name="dotnet-tool-list"></a>dotnet tool list

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool list` - 컴퓨터의 기본 디렉터리 또는 지정된 경로에 현재 설치된 모든 [.NET Core Global Tool](global-tools.md)을 나열합니다.

## <a name="synopsis"></a>개요

```console
dotnet tool list <-g|--global>
dotnet tool list <--tool-path>
dotnet tool list <-h|--help>
```

## <a name="description"></a>설명

`dotnet tool list` 명령은 컴퓨터(현재 사용자 프로필) 또는 지정된 경로에 사용자 수준에서 설치된 모든.NET Core Global Tool을 나열하는 방법을 제공합니다. 이 명령은 패키지 이름, 설치된 버전 및 Global Tool 명령을 나열합니다. 목록 명령을 사용하려면 `--global` 옵션을 사용하여 모든 사용자 수준 도구를 표시하도록 지정하거나 `--tool-path` 옵션을 사용하여 사용자 지정 경로를 지정해야 합니다.

## <a name="options"></a>옵션

`-g|--global`

사용자 수준 Global Tool을 나열합니다. `--tool-path` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--tool-path` 옵션을 지정해야 합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--tool-path <PATH>`

Global Tool을 찾을 사용자 지정 위치를 지정합니다. PATH는 절대적이거나 상대적일 수 있습니다. `--global` 옵션과 함께 사용할 수 없습니다. 이 옵션을 지정하지 않으면 `--global` 옵션을 지정해야 합니다.

## <a name="examples"></a>예제

사용자 수준 컴퓨터에 설치된 모든 Global Tool을 나열합니다(현재 사용자 프로필).

`dotnet tool list -g`

특정 Windows 폴더의 Global Tool을 나열합니다.

`dotnet tool list --tool-path c:\global-tools`

특정 Linux/macOS 폴더의 Global Tool을 나열합니다.

`dotnet tool list --tool-path ~/bin`

## <a name="see-also"></a>참고 항목

* [.NET Core Global Tool](global-tools.md)