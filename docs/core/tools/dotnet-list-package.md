---
title: dotnet list package 명령
description: ‘dotnet list package’ 명령은 프로젝트 또는 솔루션에 대한 패키지 참조를 나열하는 편리한 옵션을 제공합니다.
ms.date: 06/26/2019
ms.openlocfilehash: fe95f3898c5bd85956f4312eb4d20259227e9ff0
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117735"
---
# <a name="dotnet-list-package"></a>dotnet list package

[!INCLUDE [topic-appliesto-net-core-22plus](../../../includes/topic-appliesto-net-core-22plus.md)]

## <a name="name"></a>name

`dotnet list package` - 프로젝트 또는 솔루션에 대한 패키지 참조를 나열합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet list [<PROJECT>|<SOLUTION>] package [--config] [--framework] [--highest-minor] [--highest-patch] 
   [--include-prerelease] [--include-transitive] [--interactive] [--outdated] [--source]
dotnet list package [-h|--help]
```

## <a name="description"></a>설명

`dotnet list package` 명령은 특정 프로젝트 또는 솔루션에 대한 모든 NuGet 패키지 참조를 나열하는 편리한 옵션을 제공합니다. 이 명령을 처리하는 데 필요한 자산을 포함하려면 먼저 프로젝트를 빌드해야 합니다. 다음 예제에서는 [SentimentAnalysis](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/SentimentAnalysis) 프로젝트에 대한 `dotnet list package` 명령의 출력을 보여 줍니다.

```output
Project 'SentimentAnalysis' has the following package references
   [netcoreapp2.1]:
   Top-level Package               Requested   Resolved
   > Microsoft.ML                  0.11.0      0.11.0
   > Microsoft.NETCore.App   (A)   [2.1.0, )   2.1.0

(A) : Auto-referenced package.
```

**요청됨** 열은 프로젝트 파일에 지정된 패키지 버전을 나타내고 이 버전은 범위일 수 있습니다. **해결됨** 열에는 프로젝트가 현재 사용 중이고 항상 단일 값인 버전이 나열됩니다. 이름 오른쪽에 `(A)`를 표시하는 패키지는 프로젝트 설정(`Sdk` 형식, `<TargetFramework>` 또는 `<TargetFrameworks>` 속성 등)에서 유추된 [암시적 패키지 참조](csproj.md#implicit-package-references)를 나타냅니다.

`--outdated` 옵션을 사용하여 프로젝트에서 사용 중인 패키지에 사용 가능한 최신 버전이 있는지 확인합니다. 기본적으로 해결된 버전이 사전 릴리스 버전이 아닌 경우 `--outdated`는 안정적인 최신 패키지를 나열합니다. 최신 버전을 나열할 때 사전 릴리스 버전을 포함하려면 `--include-prerelease` 옵션도 지정합니다. 다음 예제에서는 이전 예제와 동일한 프로젝트에 대한 `dotnet list package --outdated --include-prerelease` 명령의 출력을 보여 줍니다.

```output
The following sources were used:
   https://api.nuget.org/v3/index.json

Project `SentimentAnalysis` has the following updates to its packages
   [netcoreapp2.1]:
   Top-level Package      Requested   Resolved   Latest
   > Microsoft.ML         0.11.0      0.11.0     1.0.0-preview
```

프로젝트에 전이적 종속성이 있는지 확인해야 하는 경우에는 `--include-transitive` 옵션을 사용합니다. 다른 패키지에 의존하는 패키지를 프로젝트에 추가하면 전이적 종속성이 발생합니다. 다음 예제에서는 최상위 패키지 및 자신이 종속된 패키지를 표시하는, [HelloPlugin](https://github.com/dotnet/samples/tree/master/core/extensions/AppWithPlugin/HelloPlugin) 프로젝트에 대한 `dotnet list package --include-transitive` 명령 실행의 출력을 보여 줍니다.

```output
Project 'HelloPlugin' has the following package references
   [netcoreapp3.0]:
   Top-level Package                      Requested                    Resolved
   > Microsoft.NETCore.Platforms    (A)   [3.0.0-preview3.19128.7, )   3.0.0-preview3.19128.7
   > Microsoft.WindowsDesktop.App   (A)   [3.0.0-preview3-27504-2, )   3.0.0-preview3-27504-2

   Transitive Package               Resolved
   > Microsoft.NETCore.Targets      2.0.0
   > PluginBase                     1.0.0

(A) : Auto-referenced package.
```

## <a name="arguments"></a>인수

`PROJECT | SOLUTION`

작업할 프로젝트 또는 솔루션 파일입니다. 지정하지 않으면 이 명령은 현재 디렉터리에서 검색합니다. 둘 이상의 솔루션 또는 프로젝트가 있으면 오류가 throw됩니다.

## <a name="options"></a>옵션

* **`--config <SOURCE>`**

  최신 패키지를 검색할 때 사용할 NuGet 소스입니다. `--outdated` 옵션이 필요합니다.

* **`--framework <FRAMEWORK>`**

  지정된 [대상 프레임워크](../../standard/frameworks.md)에 적용 가능한 패키지만 표시합니다. 여러 프레임워크를 지정하려면 옵션을 여러 번 반복합니다. 예: `--framework netcoreapp2.2 --framework netstandard2.0`

* **`-h|--help`**

  명령에 대한 간단한 도움말을 출력합니다.

* **`--highest-minor`**

  최신 패키지를 검색할 때 주 버전 번호가 일치하는 패키지만 고려합니다. `--outdated` 옵션이 필요합니다.

* **`--highest-patch`**

  최신 패키지를 검색할 때 주 및 부 버전 번호가 일치하는 패키지만 고려합니다. `--outdated` 옵션이 필요합니다.

* **`--include-prerelease`**

  최신 패키지를 검색할 때 사전 릴리스 버전을 가진 패키지를 고려합니다. `--outdated` 옵션이 필요합니다.

* **`--include-transitive`**

  최상위 패키지 이외에 전이적 패키지를 나열합니다. 이 옵션을 지정하면 최상위 패키지가 종속된 패키지 목록을 가져옵니다.

* **`--interactive`**

  명령이 중지되고 사용자 입력 또는 작업을 대기할 수 있도록 허용합니다. 예를 들어 인증을 완료합니다. .NET Core 3.0 SDK 이후 사용할 수 있습니다.

* **`--outdated`**

  최신 버전을 사용할 수 있는 패키지를 나열합니다.

* **`-s|--source <SOURCE>`**

  최신 패키지를 검색할 때 사용할 NuGet 소스입니다. `--outdated` 옵션이 필요합니다.

## <a name="examples"></a>예제

* 특정 프로젝트의 패키지 참조를 나열합니다.

  ```dotnetcli
  dotnet list SentimentAnalysis.csproj package
  ```

* 사전 릴리스 버전을 포함하여 최신 버전을 사용할 수 있는 패키지 참조를 나열합니다.

  ```dotnetcli
  dotnet list package --outdated --include-prerelease
  ```

* 특정 대상 프레임워크에 대한 패키지 참조를 나열합니다.

  ```dotnetcli
  dotnet list package --framework netcoreapp3.0
  ```
