---
title: dotnet nuget delete 명령
description: dotnet-nuget-delete 명령은 서버에서 패키지를 삭제하거나 목록에서 제거합니다.
author: karann-msft
ms.date: 06/26/2019
ms.openlocfilehash: 79634baa9d6d7ff1f388f6a794ffd816687be105
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117644"
---
# <a name="dotnet-nuget-delete"></a>dotnet nuget delete

**이 항목 적용 대상: ✓** .NET Core 1.x SDK 이상 버전

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>name

`dotnet nuget delete` - 서버에서 패키지를 삭제하거나 목록에서 제거합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [--interactive] [-k|--api-key] [--no-service-endpoint]
    [--non-interactive] [-s|--source]
dotnet nuget delete [-h|--help]
```

## <a name="description"></a>설명

`dotnet nuget delete` 명령은 패키지를 삭제하거나 목록에서 제거합니다. [nuget.org](https://www.nuget.org/)의 경우 작업을 통해 패키지가 목록에서 제거됩니다.

## <a name="arguments"></a>인수

* **`PACKAGE_NAME`**

  삭제할 패키지의 이름/ID입니다.

* **`PACKAGE_VERSION`**

  삭제할 패키지의 버전입니다.

## <a name="options"></a>옵션

* **`--force-english-output`**

  고정 영어 기반 문화권을 사용하여 애플리케이션을 강제로 실행합니다.

* **`-h|--help`**

  명령에 대한 간단한 도움말을 출력합니다.

* **`--interactive`**

  명령 차단을 허용하고 인증 등의 작업에 대해 수동 작업을 요구합니다. .NET Core 2.2 SDK 이후 사용할 수 있는 옵션입니다.

* **`-k|--api-key <API_KEY>`**

  서버에 대한 API 키입니다.

* **`--no-service-endpoint`**

  소스 URL에 “api/v2/package”를 추가하지 마세요. .NET Core 2.1 SDK 이후 사용할 수 있는 옵션입니다.

* **`--non-interactive`**

  사용자 입력 또는 확인에 대한 메시지를 표시하지 않습니다.

* **`-s|--source <SOURCE>`**

  서버 URL을 지정합니다. nuget.org에 대해 지원되는 URL에는 `https://www.nuget.org`, `https://www.nuget.org/api/v3` 및 `https://www.nuget.org/api/v2/package`가 포함됩니다. 개인용 피드의 경우 호스트 이름(예: `%hostname%/api/v3`)을 바꿉니다.

## <a name="examples"></a>예제

* `Microsoft.AspNetCore.Mvc` 패키지 버전 1.0을 삭제합니다.

  ```dotnetcli
  dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0
  ```

* 사용자에게 자격 증명 또는 기타 입력을 위한 메시지를 표시하지 않고 `Microsoft.AspNetCore.Mvc` 패키지 버전 1.0을 삭제합니다.

  ```dotnetcli
  dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0 --non-interactive
  ```
