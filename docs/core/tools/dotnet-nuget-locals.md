---
title: dotnet nuget locals 명령
description: dotnet nuget locals 명령은 http-request 캐시, 임시 캐시 또는 컴퓨터 전체의 글로벌 패키지 폴더와 같은 로컬 NuGet 리소스를 지우거나 목록에 포함합니다.
author: karann-msft
ms.date: 06/26/2019
ms.openlocfilehash: 482e841d3b402084eb8c7f2456779f1600a5dd19
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117619"
---
# <a name="dotnet-nuget-locals"></a>dotnet nuget locals

**이 항목 적용 대상: ✓** .NET Core 1.x SDK 이상 버전

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>name

`dotnet nuget locals` - 로컬 NuGet 리소스를 지우거나 나열합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet nuget locals <CACHE_LOCATION> [(-c|--clear)|(-l|--list)] [--force-english-output]
dotnet nuget locals [-h|--help]
```

## <a name="description"></a>설명

`dotnet nuget locals` 명령은 캐시, 임시 캐시 또는 시스템 전체의 글로벌 패키지 폴더에서 로컬 NuGet 리소스를 지우거나 목록에 포함합니다.

## <a name="arguments"></a>인수

* **`CACHE_LOCATION`**

  나열하거나 지울 캐시 위치입니다. 다음 값 중 하나를 허용합니다.

  * `all` - 지정된 작업이 모든 캐시 형식 즉, http-request 캐시, 전역 패키지 캐시 및 임시 캐시에 적용됨을 나타냅니다.
  * `http-cache` - 지정된 작업이 http-request 캐시에만 적용됨을 나타냅니다. 다른 캐시 위치는 영향을 받지 않습니다.
  * `global-packages` - 지정된 작업이 전역 패키지 캐시에만 적용됨을 나타냅니다. 다른 캐시 위치는 영향을 받지 않습니다.
  * `temp` - 지정된 작업이 임시 캐시에만 적용됨을 나타냅니다. 다른 캐시 위치는 영향을 받지 않습니다.

## <a name="options"></a>옵션

* **`--force-english-output`**

  고정 영어 기반 문화권을 사용하여 애플리케이션을 강제로 실행합니다.

* **`-h|--help`**

  명령에 대한 간단한 도움말을 출력합니다.

* **`-c|--clear`**

  지우기 옵션은 지정된 캐시 유형에 지우기 작업을 실행합니다. 캐시 디렉터리의 콘텐츠는 재귀적으로 삭제됩니다. 실행 중인 사용자/그룹에게 캐시 디렉터리의 파일에 대한 사용 권한이 있어야 합니다. 그렇지 않은 경우에는 지우지 않은 파일/폴더가 있음을 나타내는 오류가 표시됩니다.

* **`-l|--list`**

  목록 옵션은 지정된 캐시 형식의 위치를 표시하는 데 사용됩니다.

## <a name="examples"></a>예제

* 모든 로컬 캐시 디렉터리(http-cache 디렉터리, 전역 패키지 캐시 디렉터리 및 임시 캐시 디렉터리)의 경로를 표시합니다.

  ```dotnetcli
  dotnet nuget locals –l all
  ```

* 로컬 http-cache 디렉터리의 경로를 표시합니다.

  ```dotnetcli
  dotnet nuget locals --list http-cache
  ```

* 모든 로컬 캐시 디렉터리(http-cache 디렉터리, 전역 패키지 캐시 디렉터리 및 임시 캐시 디렉터리)에서 모든 파일을 지웁니다.

  ```dotnetcli
  dotnet nuget locals --clear all
  ```

* 로컬 글로벌 패키지 캐시 디렉터리에 있는 모든 파일을 지웁니다.

  ```dotnetcli
  dotnet nuget locals -c global-packages
  ```

* 로컬 임시 캐시 디렉터리에 있는 모든 파일을 지웁니다.

  ```dotnetcli
  dotnet nuget locals -c temp
  ```

## <a name="troubleshooting"></a>문제 해결

`dotnet nuget locals` 명령을 사용하는 동안 가장 일반적으로 나타나는 문제와 오류에 대한 자세한 내용은 [NuGet 캐시 관리](/nuget/consume-packages/managing-the-nuget-cache)를 참조하세요.
