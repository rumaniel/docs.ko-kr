---
title: dotnet sln 명령
description: dotnet-sln 명령은 솔루션 파일의 프로젝트를 추가, 제거 및 나열하는 간편한 옵션을 제공합니다.
ms.date: 06/13/2018
ms.openlocfilehash: 84508aaefff61b31e2965576ebc2daaae7331951
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117590"
---
# <a name="dotnet-sln"></a>dotnet sln

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet sln` - .NET Core 솔루션 파일을 수정합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet sln [<SOLUTION_NAME>] add <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] add <GLOBBING_PATTERN>
dotnet sln [<SOLUTION_NAME>] remove <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] remove <GLOBBING_PATTERN>
dotnet sln [<SOLUTION_NAME>] list
dotnet sln [-h|--help]
```

## <a name="description"></a>설명

`dotnet sln` 명령은 솔루션 파일의 프로젝트를 추가, 제거 및 나열하는 간편한 옵션을 제공합니다.

`dotnet sln` 명령을 사용하려면 솔루션 파일이 이미 있어야 합니다. 하나를 생성해야 하는 경우, 다음 예제와 같이 [dotnet new](dotnet-new.md) 명령을 사용합니다.

```dotnetcli
dotnet new sln
```

## <a name="commands"></a>명령

`add <PROJECT> ...`

`add <GLOBBING_PATTERN>`

솔루션 파일에 하나 이상의 프로젝트를 추가합니다. Unix/Linux 기반 터미널에서는 [와일드카드 사용 패턴](https://en.wikipedia.org/wiki/Glob_(programming))이 지원됩니다.

`remove <PROJECT> ...`

`remove <GLOBBING_PATTERN>`

솔루션 파일에서 하나 이상의 프로젝트를 제거합니다. Unix/Linux 기반 터미널에서는 [와일드카드 사용 패턴](https://en.wikipedia.org/wiki/Glob_(programming))이 지원됩니다.

`list`

솔루션 파일의 모든 프로젝트를 나열합니다.

## <a name="arguments"></a>인수

`SOLUTION_NAME`

사용할 솔루션 파일입니다. 지정하지 않으면 이 명령은 현재 디렉터리에서 검색합니다. 디렉터리에 여러 솔루션 파일이 있으면 하나를 지정해야 합니다.

## <a name="options"></a>옵션

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

## <a name="examples"></a>예제

솔루션에 C# 프로젝트를 추가합니다.

`dotnet sln todo.sln add todo-app/todo-app.csproj`

솔루션에서 C# 프로젝트를 제거합니다.

`dotnet sln todo.sln remove todo-app/todo-app.csproj`

솔루션에 여러 C# 프로젝트를 추가합니다.

`dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj`

솔루션에서 여러 C# 프로젝트를 제거합니다.

`dotnet sln todo.sln remove todo-app/todo-app.csproj back-end/back-end.csproj`

와일드카드 사용 패턴을 사용하여 솔루션에 여러 C# 프로젝트를 추가합니다.

`dotnet sln todo.sln add **/*.csproj`

와일드카드 사용 패턴을 사용하여 솔루션에서 여러 C# 프로젝트를 제거합니다.

`dotnet sln todo.sln remove **/*.csproj`

> [!NOTE]
> 와일드카드 사용은 CLI 기능이 아니라 명령 셸의 기능입니다. 파일을 확장하려면 와일드카드 사용을 지원하는 셸을 사용해야 합니다. 와일드카드 사용에 대한 자세한 내용은 [Wikipedia](https://en.wikipedia.org/wiki/Glob_(programming))를 참조하세요.
