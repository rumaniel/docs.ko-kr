---
title: dotnet remove reference 명령
description: dotnet remove reference 명령은 프로젝트 간 참조를 제거하는 편리한 옵션을 제공합니다.
ms.date: 05/29/2018
ms.openlocfilehash: bfac4721743babcf48fd8e86a50c8df136e1bfce
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53170615"
---
# <a name="dotnet-remove-reference"></a>dotnet remove reference

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet remove reference` - 프로젝트 간 참조를 제거합니다.

## <a name="synopsis"></a>개요

`dotnet remove [<PROJECT>] reference [-f|--framework] <PROJECT_REFERENCES> [-h|--help]`

## <a name="description"></a>설명

`dotnet remove reference` 명령은 프로젝트에서 프로젝트 참조를 제거하는 편리한 옵션을 제공합니다.

## <a name="arguments"></a>인수

`PROJECT`

대상 프로젝트 파일입니다. 지정하지 않으면 이 명령은 현재 디렉터리에서 검색합니다.

`PROJECT_REFERENCES`

제거할 프로젝트 간(P2P) 참조입니다. 하나 또는 여러 프로젝트를 지정할 수 있습니다. Unix/Linux 기반 터미널에서는 [와일드카드 사용 패턴](https://en.wikipedia.org/wiki/Glob_(programming))이 지원됩니다.

## <a name="options"></a>옵션

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-f|--framework <FRAMEWORK>`

특정 [프레임워크](../../standard/frameworks.md)를 대상으로 하는 경우에만 참조를 제거합니다.

## <a name="examples"></a>예제

지정한 프로젝트에서 프로젝트 참조를 제거합니다.

`dotnet remove app/app.csproj reference lib/lib.csproj`

현재 디렉터리의 프로젝트에서 여러 프로젝트 참조를 제거합니다.

`dotnet remove reference lib1/lib1.csproj lib2/lib2.csproj`

Unix/Linux에서 와일드카드 사용 패턴을 사용하여 여러 프로젝트 참조를 제거합니다.

`dotnet remove app/app.csproj reference **/*.csproj`
