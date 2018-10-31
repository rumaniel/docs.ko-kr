---
title: dotnet new 명령 - .NET Core CLI
description: dotnet new 명령은 지정된 템플릿을 기반으로 새 .NET Core 프로젝트를 만듭니다.
author: mairaw
ms.author: mairaw
ms.date: 10/24/2018
ms.openlocfilehash: 56d76f1dd54097f9cf20129d74057235290c273c
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188206"
---
# <a name="dotnet-new"></a>dotnet new

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet new` - 지정된 템플릿을 기반으로 새 프로젝트, 구성 파일 또는 솔루션을 만듭니다.

## <a name="synopsis"></a>개요

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```console
dotnet new <TEMPLATE> [--force] [-i|--install] [-lang|--language] [-n|--name] [--nuget-source] [-o|--output]
    [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```console
dotnet new <TEMPLATE> [--force] [-i|--install] [-lang|--language] [-n|--name] [-o|--output] [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```console
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template options]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

---

## <a name="description"></a>설명

`dotnet new` 명령은 유효한 .NET Core 프로젝트를 초기화하는 편리한 방법을 제공합니다.

이 명령은 [템플릿 엔진](https://github.com/dotnet/templating)을 호출하여 지정된 템플릿 및 옵션을 기반으로 디스크에 아티팩트를 만듭니다.

## <a name="arguments"></a>인수

`TEMPLATE`

명령이 호출될 때 인스턴스화할 템플릿입니다. 각 템플릿에는 전달할 수 있는 특정 옵션이 있을 수 있습니다. 자세한 내용은 [템플릿 옵션](#template-options)을 참조하세요.

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

명령에는 템플릿의 기본 목록이 포함되어 있습니다. `dotnet new -l`을 사용하여 사용 가능한 템플릿 목록을 가져옵니다. 다음 표에는 .NET Core SDK 2.1.300과 함께 사전 설치된 템플릿이 나와 있습니다. 템플릿의 기본 언어는 대괄호 안에 표시됩니다.

|템플릿 설명                          | 템플릿 이름    | 언어     |
|----------------------------------------------|------------------|---------------|
| 콘솔 응용 프로그램                          | `console`        | [C#], F#, VB  |
| 클래스 라이브러리                                | `classlib`       | [C#], F#, VB  |
| 단위 테스트 프로젝트                            | `mstest`         | [C#], F#, VB  |
| xUnit 테스트 프로젝트                           | `xunit`          | [C#], F#, VB  |
| Razor 페이지                                   | `page`           | [C#]          |
| MVC ViewImports                              | `viewimports`    | [C#]          |
| MVC ViewStart                                | `viewstart`      | [C#]          |
| ASP.NET Core 비어 있음                           | `web`            | [C#], F#      |
| ASP.NET Core 웹앱(모델-뷰-컨트롤러) | `mvc`            | [C#], F#      |
| ASP.NET Core 웹앱                         | `razor`, `webapp`| [C#]          |
| ASP.NET Core(Angular 사용)                    | `angular`        | [C#]          |
| ASP.NET Core(React.js 사용)                   | `react`          | [C#]          |
| ASP.NET Core(React.js 및 Redux 사용)         | `reactredux`     | [C#]          |
| ASP.NET Core 웹 API                         | `webapi`         | [C#], F#      |
| Razor 클래스 라이브러리                          | `razorclasslib`  | [C#]          |
| global.json 파일                             | `globaljson`     |               |
| NuGet 구성                                 | `nugetconfig`    |               |
| 웹 구성                                   | `webconfig`      |               |
| 솔루션 파일                                | `sln`            |               |

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

명령에는 템플릿의 기본 목록이 포함되어 있습니다. `dotnet new -l`을 사용하여 사용 가능한 템플릿 목록을 가져옵니다. 다음 표에는 .NET Core SDK 2.0과 함께 사전 설치된 템플릿이 나와 있습니다. 템플릿의 기본 언어는 대괄호 안에 표시됩니다.

|템플릿 설명                          | 템플릿 이름 | 언어     |
|----------------------------------------------|---------------|---------------|
| 콘솔 응용 프로그램                          | `console`     | [C#], F#, VB  |
| 클래스 라이브러리                                | `classlib`    | [C#], F#, VB  |
| 단위 테스트 프로젝트                            | `mstest`      | [C#], F#, VB  |
| xUnit 테스트 프로젝트                           | `xunit`       | [C#], F#, VB  |
| ASP.NET Core 비어 있음                           | `web`         | [C#], F#      |
| ASP.NET Core 웹앱(모델-뷰-컨트롤러) | `mvc`         | [C#], F#      |
| ASP.NET Core 웹앱                         | `razor`       | [C#]          |
| ASP.NET Core(Angular 사용)                    | `angular`     | [C#]          |
| ASP.NET Core(React.js 사용)                   | `react`       | [C#]          |
| ASP.NET Core(React.js 및 Redux 사용)         | `reactredux`  | [C#]          |
| ASP.NET Core 웹 API                         | `webapi`      | [C#], F#      |
| global.json 파일                             | `globaljson`  |               |
| NuGet 구성                                 | `nugetconfig` |               |
| 웹 구성                                   | `webconfig`   |               |
| 솔루션 파일                                | `sln`         |               |
| Razor 페이지                                   | `page`        |               |
| MVC ViewImports                              | `viewimports` |               |
| MVC ViewStart                                | `viewstart`   |               |

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

명령에는 템플릿의 기본 목록이 포함되어 있습니다. `dotnet new -all`을 사용하여 사용 가능한 템플릿 목록을 가져옵니다. 다음 표에는 .NET Core SDK 1.x와 함께 사전 설치된 템플릿이 나와 있습니다. 템플릿의 기본 언어는 대괄호 안에 표시됩니다.

|템플릿 설명  | 템플릿 이름 | 언어 |
|----------------------|---------------|-----------|
| 콘솔 응용 프로그램  | `console`     | [C#], F#  |
| 클래스 라이브러리        | `classlib`    | [C#], F#  |
| 단위 테스트 프로젝트    | `mstest`      | [C#], F#  |
| xUnit 테스트 프로젝트   | `xunit`       | [C#], F#  |
| ASP.NET Core 비어 있음   | `web`         | [C#]      |
| ASP.NET Core 웹앱 | `mvc`         | [C#], F#  |
| ASP.NET Core 웹 API | `webapi`      | [C#]      |
| NuGet 구성         | `nugetconfig` |           |
| 웹 구성           | `webconfig`   |           |
| 솔루션 파일        | `sln`         |           |

---

## <a name="options"></a>옵션

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--force`

기존 파일을 변경할 경우에도 콘텐츠를 강제 생성합니다. 출력 디렉터리에 이미 프로젝트가 포함되어 있는 경우 필수입니다.

`-h|--help`

명령에 대한 도움말을 출력합니다. `dotnet new` 명령 자체 또는 `dotnet new mvc --help` 같은 템플릿에 대해 호출될 수 있습니다.

`-i|--install <PATH|NUGET_ID>`

제공된 `PATH` 또는 `NUGET_ID`에서 소스 또는 템플릿 팩을 설치합니다. 시험판 버전의 템플릿 패키지를 설치하려면 버전을 `<package-name>::<package-version>` 형식으로 지정해야 합니다. 기본적으로 `dotnet new`는 마지막 안정 패키지 버전을 나타내는 버전에 대해 \*를 전달합니다. [예제](#examples) 섹션의 예제를 참조하세요.

사용자 지정 템플릿을 만드는 방법에 대한 자세한 내용은 [dotnet new에 대한 사용자 지정 템플릿](custom-templates.md)을 참조하세요.

`-l|--list`

지정된 이름을 포함하는 템플릿을 나열합니다. `dotnet new` 명령에 대해 호출되는 경우 지정된 디렉터리에서 사용 가능한 템플릿을 나열합니다. 예를 들어 디렉터리에 이미 프로젝트가 포함되어 있는 경우 일부 프로젝트 템플릿을 나열하지 않습니다.

`-lang|--language {C#|F#|VB}`

만들 템플릿의 언어입니다. 허용되는 언어는 템플릿에 따라 다릅니다([인수](#arguments) 섹션에서 기본값 참조). 일부 템플릿의 경우 유효하지 않습니다.

> [!NOTE]
> 일부 셸은 `#`을 특수 문자로 해석합니다. 이러한 경우 `dotnet new console -lang "F#"`과 같은 언어 매개 변수 값을 포함해야 합니다.

`-n|--name <OUTPUT_NAME>`

생성된 출력에 대한 이름입니다. 이름을 지정하지 않으면 현재 디렉터리의 이름이 사용됩니다.

`--nuget-source`

설치 중 사용할 NuGet 소스를 지정합니다.

`-o|--output <OUTPUT_DIRECTORY>`

생성된 출력을 배치할 위치입니다. 기본값은 현재 디렉터리입니다.

`--type`

사용 가능한 형식에 따라 템플릿을 필터링합니다. 미리 정의된 값은 “project”, “item” 또는 “other”입니다.

`-u|--uninstall <PATH|NUGET_ID>`

제공된 `PATH` 또는 `NUGET_ID`에서 소스 또는 템플릿 팩을 제거합니다.

> [!NOTE]
> `PATH`를 사용하여 템플릿을 제거하려면 경로를 정규화해야 합니다. 예를 들어 *C:/Users/\<사용자>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp*는 작동하지만 상위 폴더의 *./GarciaSoftware.ConsoleTemplate.CSharp*는 작동하지 않습니다.
> 마지막의 종료하는 디렉터리 슬래시도 템플릿 경로에 포함하지 마세요.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--force`

기존 파일을 변경할 경우에도 콘텐츠를 강제 생성합니다. 출력 디렉터리에 이미 프로젝트가 포함되어 있는 경우 필수입니다.

`-h|--help`

명령에 대한 도움말을 출력합니다. `dotnet new` 명령 자체 또는 `dotnet new mvc --help` 같은 템플릿에 대해 호출될 수 있습니다.

`-i|--install <PATH|NUGET_ID>`

제공된 `PATH` 또는 `NUGET_ID`에서 소스 또는 템플릿 팩을 설치합니다. 시험판 버전의 템플릿 패키지를 설치하려면 버전을 `<package-name>::<package-version>` 형식으로 지정해야 합니다. 기본적으로 `dotnet new`는 마지막 안정 패키지 버전을 나타내는 버전에 대해 \*를 전달합니다. [예제](#examples) 섹션의 예제를 참조하세요.

사용자 지정 템플릿을 만드는 방법에 대한 자세한 내용은 [dotnet new에 대한 사용자 지정 템플릿](custom-templates.md)을 참조하세요.

`-l|--list`

지정된 이름을 포함하는 템플릿을 나열합니다. `dotnet new` 명령에 대해 호출되는 경우 지정된 디렉터리에서 사용 가능한 템플릿을 나열합니다. 예를 들어 디렉터리에 이미 프로젝트가 포함되어 있는 경우 일부 프로젝트 템플릿을 나열하지 않습니다.

`-lang|--language {C#|F#|VB}`

만들 템플릿의 언어입니다. 허용되는 언어는 템플릿에 따라 다릅니다([인수](#arguments) 섹션에서 기본값 참조). 일부 템플릿의 경우 유효하지 않습니다.

> [!NOTE]
> 일부 셸은 `#`을 특수 문자로 해석합니다. 이러한 경우 `dotnet new console -lang "F#"`과 같은 언어 매개 변수 값을 포함해야 합니다.

`-n|--name <OUTPUT_NAME>`

생성된 출력에 대한 이름입니다. 이름을 지정하지 않으면 현재 디렉터리의 이름이 사용됩니다.

`-o|--output <OUTPUT_DIRECTORY>`

생성된 출력을 배치할 위치입니다. 기본값은 현재 디렉터리입니다.

`--type`

사용 가능한 형식에 따라 템플릿을 필터링합니다. 미리 정의된 값은 “project”, “item” 또는 “other”입니다.

`-u|--uninstall <PATH|NUGET_ID>`

제공된 `PATH` 또는 `NUGET_ID`에서 소스 또는 템플릿 팩을 제거합니다.

> [!NOTE]
> 소스 `PATH`를 사용하여 템플릿을 제거하려면 경로를 정규화해야 합니다. 예를 들어 *C:/Users/\<사용자>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp*는 작동하지만 상위 폴더의 *./GarciaSoftware.ConsoleTemplate.CSharp*는 작동하지 않습니다. 마지막의 종료하는 디렉터리 슬래시도 템플릿 경로에 포함하지 마세요.
> 
> 템플릿을 제거하는 데 필요한 `PATH` 또는 `NUGET_ID` 인수를 확인할 수 없는 경우, 인수 없이 `dotnet new --uninstall`을 실행하면 설치된 모든 템플릿 및 템플릿을 제거하는 데 필요한 인수가 나열됩니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-all|--show-all`

`dotnet new` 명령의 컨텍스트에서만 실행되는 경우 특정 유형의 프로젝트에 대한 모든 템플릿을 표시합니다. `dotnet new web -all`처럼 특정 템플릿의 컨텍스트에서 실행되는 경우 `-all`은 강제 생성 플래그로 해석됩니다. 출력 디렉터리에 이미 프로젝트가 포함되어 있는 경우 필수입니다.

`-h|--help`

명령에 대한 도움말을 출력합니다. `dotnet new` 명령 자체 또는 `dotnet new mvc --help` 같은 템플릿에 대해 호출될 수 있습니다.

`-l|--list`

지정된 이름을 포함하는 템플릿을 나열합니다. `dotnet new` 명령에 대해 호출되는 경우 지정된 디렉터리에서 사용 가능한 템플릿을 나열합니다. 예를 들어 디렉터리에 이미 프로젝트가 포함되어 있는 경우 일부 프로젝트 템플릿을 나열하지 않습니다.

`-lang|--language {C#|F#}`

만들 템플릿의 언어입니다. 허용되는 언어는 템플릿에 따라 다릅니다([인수](#arguments) 섹션에서 기본값 참조). 일부 템플릿의 경우 유효하지 않습니다.

> [!NOTE]
> 일부 셸은 `#`을 특수 문자로 해석합니다. 이러한 경우 `dotnet new console -lang "F#"`과 같은 언어 매개 변수 값을 포함해야 합니다.

`-n|--name <OUTPUT_NAME>`

생성된 출력에 대한 이름입니다. 이름을 지정하지 않으면 현재 디렉터리의 이름이 사용됩니다.

`-o|--output <OUTPUT_DIRECTORY>`

생성된 출력을 배치할 위치입니다. 기본값은 현재 디렉터리입니다.

---

## <a name="template-options"></a>템플릿 옵션

각 프로젝트 템플릿에는 사용할 수 있는 추가 옵션이 있을 수 있습니다. 코어 템플릿에는 다음과 같은 추가 옵션이 있습니다.

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

**console, angular, react, reactredux, razorclasslib**

  `--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**classlib**

`-f|--framework <FRAMEWORK>` - 대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 값: `netcoreapp2.0`(.NET Core 클래스 라이브러리를 만드는 경우) 또는 `netstandard2.0`(.NET Standard 클래스 라이브러리를 만드는 경우). 기본값은 `netstandard2.0`입니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**mstest, xunit**

`-p|--enable-pack` - [dotnet pack](dotnet-pack.md)을 사용하여 프로젝트에 대한 패키징을 사용하도록 설정합니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**globaljson**

`--sdk-version <VERSION_NUMBER>` - *global.json* 파일에서 사용할 .NET Core SDK 버전을 지정합니다.

**web**

`--exclude-launch-settings` - 생성된 템플릿에서 *launchSettings.json*을 제외합니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

`--no-https` - 프로젝트에는 HTTPS가 필요하지 않습니다. 이 옵션은 `IndividualAuth` 또는 `OrganizationalAuth`를 사용하지 않는 경우에만 적용됩니다.

**webapi**

`-au|--auth <AUTHENTICATION_TYPE>` - 사용할 인증 형식입니다. 가능한 값은 다음과 같습니다.

- `None` - 인증하지 않습니다(기본값).
- `IndividualB2C` - Azure AD B2C를 사용한 개별 인증입니다.
- `SingleOrg` - 단일 테넌트에 대한 조직적 인증입니다.
- `Windows` - Windows 인증입니다.

`--aad-b2c-instance <INSTANCE>` - 연결할 Azure Active Directory B2C 인스턴스입니다. `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/tfp/`입니다.

`-ssp|--susi-policy-id <ID>` - 이 프로젝트에 대한 로그인 및 등록 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`--aad-instance <INSTANCE>` - 연결할 Azure Active Directory 인스턴스입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/`입니다.

`--client-id <ID>` - 이 프로젝트의 클라이언트 ID입니다. `IndividualB2C` 또는 `SingleOrg` 인증과 함께 사용합니다. 기본값은 `11111111-1111-1111-11111111111111111`입니다.

`--domain <DOMAIN>` - 디렉터리 테넌트에 대한 도메인입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `qualified.domain.name`입니다.

`--tenant-id <ID>` - 연결할 디렉터리의 TenantId ID입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `22222222-2222-2222-2222-222222222222`입니다.

`-r|--org-read-access` - 디렉터리에 대한 이 응용 프로그램 읽기 액세스를 허용합니다. `SingleOrg` 또는 `MultiOrg` 인증에만 적용됩니다.

`--exclude-launch-settings` - 생성된 템플릿에서 *launchSettings.json*을 제외합니다.

`-uld|--use-local-db` - SQLite 대신 LocalDB를 사용하도록 지정합니다. `Individual` 또는 `IndividualB2C` 인증에만 적용됩니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

`--no-https` - 프로젝트에는 HTTPS가 필요하지 않습니다. `app.UseHsts` 및 `app.UseHttpsRedirection`은 `Startup.Configure`에 추가되지 않습니다. 이 옵션은 `Individual`, `IndividualB2C`, `SingleOrg` 또는 `MultiOrg`를 사용하지 않는 경우에만 적용됩니다.

**mvc, razor**

`-au|--auth <AUTHENTICATION_TYPE>` - 사용할 인증 형식입니다. 가능한 값은 다음과 같습니다.

- `None` - 인증하지 않습니다(기본값).
- `Individual` - 개별 인증입니다.
- `IndividualB2C` - Azure AD B2C를 사용한 개별 인증입니다.
- `SingleOrg` - 단일 테넌트에 대한 조직적 인증입니다.
- `MultiOrg` - 여러 테넌트에 대한 조직적 인증입니다.
- `Windows` - Windows 인증입니다.

`--aad-b2c-instance <INSTANCE>` - 연결할 Azure Active Directory B2C 인스턴스입니다. `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/tfp/`입니다.

`-ssp|--susi-policy-id <ID>` - 이 프로젝트에 대한 로그인 및 등록 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`-rp|--reset-password-policy-id <ID>` - 이 프로젝트에 대한 암호 재설정 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`-ep|--edit-profile-policy-id <ID>` - 이 프로젝트에 대한 프로필 편집 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`--aad-instance <INSTANCE>` - 연결할 Azure Active Directory 인스턴스입니다. `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/`입니다.

`--client-id <ID>` - 이 프로젝트의 클라이언트 ID입니다. `IndividualB2C`, `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `11111111-1111-1111-11111111111111111`입니다.

`--domain <DOMAIN>` - 디렉터리 테넌트에 대한 도메인입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `qualified.domain.name`입니다.

`--tenant-id <ID>` - 연결할 디렉터리의 TenantId ID입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `22222222-2222-2222-2222-222222222222`입니다.

`--callback-path <PATH>` - 리디렉션 URI의 응용 프로그램 기본 경로 내 요청 경로입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `/signin-oidc`입니다.

`-r|--org-read-access` - 디렉터리에 대한 이 응용 프로그램 읽기 액세스를 허용합니다. `SingleOrg` 또는 `MultiOrg` 인증에만 적용됩니다.

`--exclude-launch-settings` - 생성된 템플릿에서 *launchSettings.json*을 제외합니다.

`--use-browserlink` - 프로젝트에 BrowserLink를 포함합니다.

`-uld|--use-local-db` - SQLite 대신 LocalDB를 사용하도록 지정합니다. `Individual` 또는 `IndividualB2C` 인증에만 적용됩니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

`--no-https` - 프로젝트에는 HTTPS가 필요하지 않습니다. `app.UseHsts` 및 `app.UseHttpsRedirection`은 `Startup.Configure`에 추가되지 않습니다. 이 옵션은 `Individual`, `IndividualB2C`, `SingleOrg` 또는 `MultiOrg`를 사용하지 않는 경우에만 적용됩니다.

**page**

`-na|--namespace <NAMESPACE_NAME>` - 생성된 코드에 대한 네임스페이스입니다. 기본값은 `MyApp.Namespace`입니다.

`-np|--no-pagemodel` - PageModel 없이 페이지를 만듭니다.

**viewimports**

`-na|--namespace <NAMESPACE_NAME>` - 생성된 코드에 대한 네임스페이스입니다. 기본값은 `MyApp.Namespace`입니다.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

**console, angular, react, reactredux**

  `--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**classlib**

`-f|--framework <FRAMEWORK>` - 대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 값: `netcoreapp2.0`(.NET Core 클래스 라이브러리를 만드는 경우) 또는 `netstandard2.0`(.NET Standard 클래스 라이브러리를 만드는 경우). 기본값은 `netstandard2.0`입니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**mstest, xunit**

`-p|--enable-pack` - [dotnet pack](dotnet-pack.md)을 사용하여 프로젝트에 대한 패키징을 사용하도록 설정합니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**globaljson**

`--sdk-version <VERSION_NUMBER>` - *global.json* 파일에서 사용할 .NET Core SDK 버전을 지정합니다.

**web**

`--use-launch-settings` - 생성된 템플릿 출력에 *launchSettings.json*을 포함합니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**webapi**

`-au|--auth <AUTHENTICATION_TYPE>` - 사용할 인증 형식입니다. 가능한 값은 다음과 같습니다.

- `None` - 인증하지 않습니다(기본값).
- `IndividualB2C` - Azure AD B2C를 사용한 개별 인증입니다.
- `SingleOrg` - 단일 테넌트에 대한 조직적 인증입니다.
- `Windows` - Windows 인증입니다.

`--aad-b2c-instance <INSTANCE>` - 연결할 Azure Active Directory B2C 인스턴스입니다. `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/tfp/`입니다.

`-ssp|--susi-policy-id <ID>` - 이 프로젝트에 대한 로그인 및 등록 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`--aad-instance <INSTANCE>` - 연결할 Azure Active Directory 인스턴스입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/`입니다.

`--client-id <ID>` - 이 프로젝트의 클라이언트 ID입니다. `IndividualB2C` 또는 `SingleOrg` 인증과 함께 사용합니다. 기본값은 `11111111-1111-1111-11111111111111111`입니다.

`--domain <DOMAIN>` - 디렉터리 테넌트에 대한 도메인입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `qualified.domain.name`입니다.

`--tenant-id <ID>` - 연결할 디렉터리의 TenantId ID입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `22222222-2222-2222-2222-222222222222`입니다.

`-r|--org-read-access` - 디렉터리에 대한 이 응용 프로그램 읽기 액세스를 허용합니다. `SingleOrg` 또는 `MultiOrg` 인증에만 적용됩니다.

`--use-launch-settings` - 생성된 템플릿 출력에 *launchSettings.json*을 포함합니다.

`-uld|--use-local-db` - SQLite 대신 LocalDB를 사용하도록 지정합니다. `Individual` 또는 `IndividualB2C` 인증에만 적용됩니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**mvc, razor**

`-au|--auth <AUTHENTICATION_TYPE>` - 사용할 인증 형식입니다. 가능한 값은 다음과 같습니다.

- `None` - 인증하지 않습니다(기본값).
- `Individual` - 개별 인증입니다.
- `IndividualB2C` - Azure AD B2C를 사용한 개별 인증입니다.
- `SingleOrg` - 단일 테넌트에 대한 조직적 인증입니다.
- `MultiOrg` - 여러 테넌트에 대한 조직적 인증입니다.
- `Windows` - Windows 인증입니다.

`--aad-b2c-instance <INSTANCE>` - 연결할 Azure Active Directory B2C 인스턴스입니다. `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/tfp/`입니다.

`-ssp|--susi-policy-id <ID>` - 이 프로젝트에 대한 로그인 및 등록 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`-rp|--reset-password-policy-id <ID>` - 이 프로젝트에 대한 암호 재설정 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`-ep|--edit-profile-policy-id <ID>` - 이 프로젝트에 대한 프로필 편집 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

`--aad-instance <INSTANCE>` - 연결할 Azure Active Directory 인스턴스입니다. `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/`입니다.

`--client-id <ID>` - 이 프로젝트의 클라이언트 ID입니다. `IndividualB2C`, `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `11111111-1111-1111-11111111111111111`입니다.

`--domain <DOMAIN>` - 디렉터리 테넌트에 대한 도메인입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `qualified.domain.name`입니다.

`--tenant-id <ID>` - 연결할 디렉터리의 TenantId ID입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `22222222-2222-2222-2222-222222222222`입니다.

`--callback-path <PATH>` - 리디렉션 URI의 응용 프로그램 기본 경로 내 요청 경로입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `/signin-oidc`입니다.

`-r|--org-read-access` - 디렉터리에 대한 이 응용 프로그램 읽기 액세스를 허용합니다. `SingleOrg` 또는 `MultiOrg` 인증에만 적용됩니다.

`--use-launch-settings` - 생성된 템플릿 출력에 *launchSettings.json*을 포함합니다.

`--use-browserlink` - 프로젝트에 BrowserLink를 포함합니다.

`-uld|--use-local-db` - SQLite 대신 LocalDB를 사용하도록 지정합니다. `Individual` 또는 `IndividualB2C` 인증에만 적용됩니다.

`--no-restore` - 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**page**

`-na|--namespace <NAMESPACE_NAME>` - 생성된 코드에 대한 네임스페이스입니다. 기본값은 `MyApp.Namespace`입니다.

`-np|--no-pagemodel` - PageModel 없이 페이지를 만듭니다.

**viewimports**

`-na|--namespace <NAMESPACE_NAME>` - 생성된 코드에 대한 네임스페이스입니다. 기본값은 `MyApp.Namespace`입니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**console, xunit, mstest, web, webapi**

`-f|--framework` - 대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 값: `netcoreapp1.0` 또는 `netcoreapp1.1`. 기본값은 `netcoreapp1.0`입니다.

**classlib**

`-f|--framework` - 대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 값: `netcoreapp1.0`, `netcoreapp1.1` 또는 `netstandard1.0`~`netstandard1.6`. 기본값은 `netstandard1.4`입니다.

**mvc**

`-f|--framework` - 대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 값: `netcoreapp1.0` 또는 `netcoreapp1.1`. 기본값은 `netcoreapp1.0`입니다.

`-au|--auth` - 사용할 인증 형식입니다. 값: `None` 또는 `Individual`. 기본값은 `None`입니다.

`-uld|--use-local-db` - SQLite 대신 LocalDB를 사용할지 여부를 지정합니다. 값: `true` 또는 `false`. 기본값은 `false`입니다.

---

## <a name="examples"></a>예제

현재 디렉터리에 F# 콘솔 응용 프로그램 프로젝트를 만듭니다.

`dotnet new console -lang F#`

지정된 디렉터리에서 .NET Standard 클래스 라이브러리 프로젝트를 만듭니다(.NET Core SDK 2.0 이상 버전에서만 사용 가능).

`dotnet new classlib -lang VB -o MyLibrary`

인증 없이 현재 디렉터리에 새 ASP.NET Core C# MVC 응용 프로그램 프로젝트를 만듭니다.

`dotnet new mvc -au None`

새 xUnit 응용 프로그램을 만듭니다.

`dotnet new xunit`

MVC에 대해 사용할 수 있는 모든 템플릿을 나열합니다.

`dotnet new mvc -l`

ASP.NET Core용 단일 페이지 응용 프로그램 템플릿 버전 2.0을 설치합니다(.NET Core SDK 1.1 및 이후 버전에서만 사용할 수 있는 명령 옵션).

`dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0`

현재 디렉터리에서 SDK 버전을 2.0.0으로 설정하여 *global.json*을 만듭니다(.NET Core SDK 2.0 이상 버전에서만 사용 가능).

`dotnet new globaljson --sdk-version 2.0.0`

## <a name="see-also"></a>참고 항목

* [dotnet new에 대한 사용자 지정 템플릿](custom-templates.md)  
* [dotnet용 사용자 지정 템플릿 새로 만들기](~/docs/core/tutorials/create-custom-template.md)  
* [dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples)(dotnet/dotnet-template-samples GitHub 리포지토리)  
* [Available templates for dotnet new](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)(dotnet new에 대한 사용 가능한 템플릿)
