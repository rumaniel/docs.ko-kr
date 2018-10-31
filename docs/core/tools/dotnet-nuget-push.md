---
title: dotnet nuget push 명령 - .NET Core CLI
description: dotnet nuget push 명령은 서버에 패키지를 푸시하고 게시합니다.
author: karann-msft
ms.author: mairaw
ms.date: 09/04/2018
ms.openlocfilehash: b9c0fad886cd1234325c58bf61b1a010bce421d9
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50200028"
---
# <a name="dotnet-nuget-push"></a>dotnet nuget push

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet nuget push` - 서버에 패키지를 푸시하고 게시합니다.

## <a name="synopsis"></a>개요

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)
```
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output] [-k|--api-key] [-n|--no-symbols]
    [--no-service-endpoint] [-s|--source] [-sk|--symbol-api-key] [-ss|--symbol-source] [-t|--timeout]
dotnet nuget push [-h|--help]
```
# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)
```
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output] [-k|--api-key] [-n|--no-symbols]
    [-s|--source] [-sk|--symbol-api-key] [-ss|--symbol-source] [-t|--timeout]
dotnet nuget push [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output] [-k|--api-key] [-n|--no-symbols]
    [-s|--source] [-sk|--symbol-api-key] [-ss|--symbol-source] [-t|--timeout]
dotnet nuget push [-h|--help]
```
---

## <a name="description"></a>설명

`dotnet nuget push` 명령은 서버에 패키지를 푸시하고 게시합니다. push 명령은 시스템의 NuGet 구성 파일에 있는 서버 및 자격 증명 정보 또는 구성 파일 체인을 사용합니다. 구성 파일에 대한 자세한 내용은 [NuGet 동작 구성](/nuget/consume-packages/configuring-nuget-behavior)을 참조하세요. NuGet의 기본 구성은 *%AppData%\NuGet\NuGet.config*(Windows) 또는 *$HOME/.local/share*(Linux/macOS)를 로드한 다음 드라이브의 루트에서 시작되고 현재 디렉터리에서 끝나는 *nuget.config* 또는 *.nuget\nuget.config*를 로드하여 가져올 수 있습니다.

## <a name="arguments"></a>인수

`ROOT`

푸시되는 패키지에 대한 파일 경로를 지정합니다.

## <a name="options"></a>옵션

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`-d|--disable-buffering`

메모리 사용량을 줄이려면 HTTP(S) 서버로 푸시할 때 버퍼링을 사용하지 않도록 설정합니다.

`--force-english-output`

고정 영어 기반 문화권을 사용하여 응용 프로그램을 강제로 실행합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-k|--api-key <API_KEY>`

서버에 대한 API 키입니다.

`-n|--no-symbols`

기호를 푸시하지 않습니다(있는 경우).

`--no-service-endpoint`

소스 URL에 “api/v2/package”를 추가하지 마세요.

`-s|--source <SOURCE>`

서버 URL을 지정합니다. 이 옵션은 NuGet 구성 파일에 `DefaultPushSource` 구성 값이 설정되어 있지 않을 때 필요합니다.

`-sk|--symbol-api-key <API_KEY>`

기호 서버에 대한 API 키입니다.

`-ss|--symbol-source <SOURCE>`

기호 서버 URL을 지정합니다.

`-t|--timeout <TIMEOUT>`

서버에 푸시하기 위한 제한 시간(초)을 지정합니다. 기본값은 300 초(5 분)입니다. 0(0초)을 지정하면 기본값이 적용됩니다.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`-d|--disable-buffering`

메모리 사용량을 줄이려면 HTTP(S) 서버로 푸시할 때 버퍼링을 사용하지 않도록 설정합니다.

`--force-english-output`

고정 영어 기반 문화권을 사용하여 응용 프로그램을 강제로 실행합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-k|--api-key <API_KEY>`

서버에 대한 API 키입니다.

`-n|--no-symbols`

기호를 푸시하지 않습니다(있는 경우).

`-s|--source <SOURCE>`

서버 URL을 지정합니다. 이 옵션은 NuGet 구성 파일에 `DefaultPushSource` 구성 값이 설정되어 있지 않을 때 필요합니다.

`-sk|--symbol-api-key <API_KEY>`

기호 서버에 대한 API 키입니다.

`-ss|--symbol-source <SOURCE>`

기호 서버 URL을 지정합니다.

`-t|--timeout <TIMEOUT>`

서버에 푸시하기 위한 제한 시간(초)을 지정합니다. 기본값은 300 초(5 분)입니다. 0(0초)을 지정하면 기본값이 적용됩니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-d|--disable-buffering`

메모리 사용량을 줄이려면 HTTP(S) 서버로 푸시할 때 버퍼링을 사용하지 않도록 설정합니다.

`--force-english-output`

고정 영어 기반 문화권을 사용하여 응용 프로그램을 강제로 실행합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-k|--api-key <API_KEY>`

서버에 대한 API 키입니다.

`-n|--no-symbols`

기호를 푸시하지 않습니다(있는 경우).

`-s|--source <SOURCE>`

서버 URL을 지정합니다. 이 옵션은 NuGet 구성 파일에 `DefaultPushSource` 구성 값이 설정되어 있지 않을 때 필요합니다.

`-sk|--symbol-api-key <API_KEY>`

기호 서버에 대한 API 키입니다.

`-ss|--symbol-source <SOURCE>`

기호 서버 URL을 지정합니다.

`-t|--timeout <TIMEOUT>`

서버에 푸시하기 위한 제한 시간(초)을 지정합니다. 기본값은 300 초(5 분)입니다. 0(0초)을 지정하면 기본값이 적용됩니다.

---

## <a name="examples"></a>예제

기본 푸시 소스에 *foo.nupkg*를 푸시하여 API 키를 지정합니다.

`dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a`

사용자 지정 푸시 소스 `https://customsource`에 *foo.nupkg*를 푸시하여 API 키를 지정합니다.

`dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/`

기본 푸시 소스 *foo.nupkg*를 푸시합니다.

`dotnet nuget push foo.nupkg`

기본 기호 소스에 *foo.symbols.nupkg*를 푸시합니다.

`dotnet nuget push foo.symbols.nupkg`

360초 시간 제한을 지정하여 기본 푸시 소스에 *foo.nupkg*를 푸시합니다.

`dotnet nuget push foo.nupkg --timeout 360`

기본 푸시 소스에 현재 디렉터리에 있는 모든 *.nupkg* 파일을 푸시합니다.

`dotnet nuget push *.nupkg`
