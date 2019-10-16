---
title: .NET Core Global Tool
description: .NET Core Global Tool의 개요와 사용 가능한 .NET Core CLI 명령입니다.
author: KathleenDollard
ms.date: 05/29/2018
ms.custom: seodec18
ms.openlocfilehash: 40a0aabcf523e8dac9a3ad226064bbb3c1b3ce5b
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332015"
---
# <a name="net-core-global-tools-overview"></a>.NET Core Global Tool 개요

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

.NET Core Global Tool은 콘솔 애플리케이션을 포함하는 특별한 NuGet 패키지입니다. Global Tool은 컴퓨터에서 PATH 환경 변수 또는 사용자 지정 위치에 포함된 기본 위치에 설치할 수 있습니다.

.NET Core Global Tool을 사용하려는 경우:

* 도구에 대한 정보를 찾습니다(일반적으로 웹 사이트 또는 GitHub 페이지).
* 홈에서 피드의 작성자 및 통계를 확인합니다(일반적으로 NuGet.org).
* 도구를 설치합니다.
* 도구를 호출합니다.
* 도구를 업데이트합니다.
* 도구를 제거합니다.

> [!IMPORTANT]
> .NET Core Global Tool이 경로에 나타나고 완전 신뢰 상태로 실행됩니다. 작성자를 신뢰하지 않는 경우 .NET Core Global Tool을 설치하지 않습니다.

## <a name="find-a-net-core-global-tool"></a>.NET Core Global Tool 찾기

현재 .NET Core CLI(명령줄 인터페이스)에는 Global Tool 검색 기능이 없습니다.

[NuGet](https://www.nuget.org)에서 .NET Core Global Tool을 찾을 수 있습니다. 그러나 NuGet에서는 아직 .NET Core Global Tool을 검색할 수 없습니다.

블로그 게시물 또는 [natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) GitHub 리포지토리에서 도구 권장 사항을 찾을 수도 있습니다.

[aspnet/DotNetTools](https://github.com/aspnet/DotNetTools/) GitHub 리포지토리에서 ASP.NET 팀이 만든 Global Tool의 소스 코드를 볼 수도 있습니다.

## <a name="check-the-author-and-statistics"></a>작성자 및 통계 확인

.NET Core Global Tool은 완전 신뢰 상태로 실행되며 일반적으로 사용자 경로에 설치되므로 매우 강력할 수 있습니다. 신뢰할 수 없는 사용자의 도구를 다운로드하지 마세요.

도구가 NuGet에서 호스팅되는 경우 도구를 검색하여 작성자 및 통계를 확인할 수 있습니다.

## <a name="install-a-global-tool"></a>Global Tool 설치

Global Tool을 설치하려면 [dotnet tool install](dotnet-tool-install.md) .NET Core CLI 명령을 사용합니다. 다음 예제에서는 기본 위치에 Global Tool을 설치하는 방법을 보여 줍니다.

```dotnetcli
dotnet tool install -g dotnetsay
```

도구를 설치할 수 없는 경우 오류 메시지가 표시됩니다. 예상한 피드가 확인되고 있는지 검사합니다.

이전 릴리스 버전 또는 특정 버전의 도구를 설치하려는 경우 다음 형식을 사용하여 버전 번호를 지정할 수 있습니다.

```dotnetcli
dotnet tool install -g <package-name> --version <version-number>
```

설치에 성공하면 다음 예와 같이 도구와 설치된 버전을 호출하는 데 사용되는 명령을 보여 주는 메시지가 표시됩니다.

```output
You can invoke the tool using the following command: dotnetsay
Tool 'dotnetsay' (version '2.0.0') was successfully installed.
```

Global Tool은 기본 디렉터리 또는 특정 위치에 설치할 수 있습니다. 기본 디렉터리는 다음과 같습니다.

| OS          | 경로                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

이러한 위치는 SDK를 처음 실행할 때 사용자 경로에 추가되므로 설치된 Global Tool을 직접 호출할 수 있습니다.

Global Tool은 컴퓨터 전체가 아니라 사용자별 도구입니다. 사용자별 도구라는 것은 컴퓨터의 모든 사용자가 사용할 수 있는 Global Tool을 설치할 수 없음을 의미합니다. 이 도구는 도구가 설치된 각 사용자 프로필에서만 사용할 수 있습니다.

Global Tool을 특정 디렉터리에 설치할 수도 있습니다. 특정 디렉터리에 설치된 경우 사용자는 경로에 해당 디렉터리를 포함하거나, 지정된 디렉터리로 명령을 호출하거나, 지정된 디렉터리 내에서 도구를 호출하여 명령을 사용할 수 있는지 확인해야 합니다.
이 경우 .NET Core CLI는 이 위치를 PATH 환경 변수에 자동으로 추가하지 않습니다.

## <a name="use-the-tool"></a>도구 사용

도구가 설치되면 명령을 사용하여 도구를 호출할 수 있습니다. 명령이 패키지 이름과 같지 않을 수 있습니다.

명령이 `dotnetsay`인 경우 다음을 사용하여 호출합니다.

```console
dotnetsay
```

도구 작성자가 도구를 `dotnet` 프롬프트 컨텍스트에 표시하려면 도구를 다음과 같이 `dotnet <command>`로 호출하는 방식으로 작성했을 수 있습니다.

```dotnetcli
dotnet doc
```

[dotnet tool list](dotnet-tool-list.md) 명령을 사용하여 설치된 패키지를 나열하면 설치된 Global Tool 패키지에 포함된 도구를 찾을 수 있습니다.

도구의 웹 사이트에서 사용 지침을 찾거나 다음 명령 중 하나를 입력할 수도 있습니다.

```console
<command> --help
dotnet <command> --help
```

## <a name="other-cli-commands"></a>기타 CLI 명령

.NET Core SDK에는 .NET Core Global Tool을 지원하는 다른 명령이 포함되어 있습니다. 다음 옵션 중 하나와 함께 `dotnet tool` 명령을 사용합니다.

* `--global` 또는 `-g`는 명령을 사용자 수준의 Global Tool에 적용 가능함을 지정합니다.
* `--tool-path`는 Global Tool의 사용자 지정 위치를 지정합니다.

Global Tool에 사용할 수 있는 명령을 확인하려면:

```dotnetcli
dotnet tool --help
```

Global Tool을 업데이트하려면 원래 버전을 제거하고 안정적인 최신 버전으로 다시 설치해야 합니다. Global Tool을 업데이트하려면 [dotnet tool update](dotnet-tool-update.md) 명령을 사용합니다.

```dotnetcli
dotnet tool update -g <packagename>
```

[dotnet tool uninstall](dotnet-tool-uninstall.md)을 사용하여 Global Tool을 제거합니다.

```dotnetcli
dotnet tool uninstall -g <packagename>
```

현재 컴퓨터에 설치된 모든 Global Tool과 해당 버전 및 명령을 표시하려면 [dotnet tool list](dotnet-tool-list.md) 명령을 사용합니다.

```dotnetcli
dotnet tool list -g
```

## <a name="see-also"></a>참고 항목

* [.NET Core 도구 사용 문제 해결](troubleshoot-usage-issues.md)
