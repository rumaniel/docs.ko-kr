---
title: dotnet nuget delete 명령 - .NET Core CLI
description: dotnet-nuget-delete 명령은 서버에서 패키지를 삭제하거나 목록에서 제거합니다.
author: karann-msft
ms.author: mairaw
ms.date: 06/01/2018
ms.openlocfilehash: f4aa027a465c4adea1de13853063d03e8e295411
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50180882"
---
# <a name="dotnet-nuget-delete"></a>dotnet nuget delete

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet nuget delete` - 서버에서 패키지를 삭제하거나 목록에서 제거합니다.

## <a name="synopsis"></a>개요

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [-k|--api-key] [--no-service-endpoint]
    [--non-interactive] [-s|--source]
dotnet nuget delete [-h|--help]
```
# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [-k|--api-key] [--non-interactive]
    [-s|--source]
dotnet nuget delete [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [-k|--api-key] [--non-interactive]
    [-s|--source]
dotnet nuget delete [-h|--help]
```
---

## <a name="description"></a>설명

`dotnet nuget delete` 명령은 패키지를 삭제하거나 목록에서 제거합니다. [nuget.org](https://www.nuget.org/)의 경우 작업을 통해 패키지가 목록에서 제거됩니다.

## <a name="arguments"></a>인수

`PACKAGE_NAME`

삭제할 패키지의 이름/ID입니다.

`PACKAGE_VERSION`

삭제할 패키지의 버전입니다.

## <a name="options"></a>옵션

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--force-english-output`

 고정 영어 기반 문화권을 사용하여 응용 프로그램을 강제로 실행합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-k|--api-key <API_KEY>`

서버에 대한 API 키입니다.

`--no-service-endpoint` 소스 URL에 “api/v2/package”를 추가하지 마세요.

`--non-interactive`

사용자 입력 또는 확인에 대한 메시지를 표시하지 않습니다.

`-s|--source <SOURCE>`

서버 URL을 지정합니다. nuget.org에 대해 지원되는 URL에는 `https://www.nuget.org`, `https://www.nuget.org/api/v3` 및 `https://www.nuget.org/api/v2/package`가 포함됩니다. 개인용 피드의 경우 호스트 이름(예: `%hostname%/api/v3`)을 바꿉니다.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--force-english-output`

 고정 영어 기반 문화권을 사용하여 응용 프로그램을 강제로 실행합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-k|--api-key <API_KEY>`

서버에 대한 API 키입니다.

`--non-interactive`

사용자 입력 또는 확인에 대한 메시지를 표시하지 않습니다.

`-s|--source <SOURCE>`

서버 URL을 지정합니다. nuget.org에 대해 지원되는 URL에는 `https://www.nuget.org`, `https://www.nuget.org/api/v3` 및 `https://www.nuget.org/api/v2/package`가 포함됩니다. 개인용 피드의 경우 호스트 이름(예: `%hostname%/api/v3`)을 바꿉니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--force-english-output`

 고정 영어 기반 문화권을 사용하여 응용 프로그램을 강제로 실행합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-k|--api-key <API_KEY>`

서버에 대한 API 키입니다.

`--non-interactive`

사용자 입력 또는 확인에 대한 메시지를 표시하지 않습니다.

`-s|--source <SOURCE>`

서버 URL을 지정합니다. nuget.org에 대해 지원되는 URL에는 `https://www.nuget.org`, `https://www.nuget.org/api/v3` 및 `https://www.nuget.org/api/v2/package`가 포함됩니다. 개인용 피드의 경우 호스트 이름(예: `%hostname%/api/v3`)을 바꿉니다.

---

## <a name="examples"></a>예제

`Microsoft.AspNetCore.Mvc` 패키지 버전 1.0을 삭제합니다.

`dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0`

사용자에게 자격 증명 또는 기타 입력을 위한 메시지를 표시하지 않고 `Microsoft.AspNetCore.Mvc` 패키지 버전 1.0을 삭제합니다.

`dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0 --non-interactive`
