---
title: dotnet migrate 명령
description: dotnet migrate 명령은 프로젝트와 모든 종속성을 마이그레이션합니다.
ms.date: 08/08/2019
ms.openlocfilehash: afc16161761d151e743e53a8572a6564add43517
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117684"
---
# <a name="dotnet-migrate"></a>dotnet 마이그레이션

**이 문서 적용 대상: ✓** .NET Core 1.x SDK **✓** .NET Core 2.x SDK

## <a name="name"></a>name

`dotnet migrate` - Preview 2 .NET Core 프로젝트를 .NET Core SDK 스타일 프로젝트로 마이그레이션합니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet migrate [<SOLUTION_FILE|PROJECT_DIR>] [--format-report-file-json] [-r|--report-file] [-s|--skip-project-references] [--skip-backup] [-t|--template-file] [-v|--sdk-package-version] [-x|--xproj-file]
dotnet migrate [-h|--help]
```

## <a name="description"></a>설명

`dotnet migrate` 명령은 유효한 Preview 2 *project.json* 기반 프로젝트를 유효한 .NET Core SDK 스타일 *csproj* 프로젝트로 마이그레이션합니다.

기본적으로 이 명령은 루트 프로젝트와, 루트 프로젝트에 포함된 모든 프로젝트 참조를 마이그레이션합니다. 이 동작은 런타임에 `--skip-project-references` 옵션을 사용하여 사용하지 않도록 설정합니다.

다음 자산에 대해 마이그레이션을 수행할 수 있습니다.

* 마이그레이션할 *project.json* 파일을 지정하여 단일 프로젝트
* *global.json* 파일로 경로를 전달하여 *global.json* 파일에 지정된 모든 디렉터리
* *solution.sln* 파일: 솔루션에서 참조된 프로젝트를 마이그레이션합니다.
* 지정된 디렉터리의 모든 하위 디렉터리(재귀적).

`dotnet migrate` 명령은 마이그레이션된 *project.json* 파일을 `backup` 디렉터리에서 유지합니다. 이 디렉터리는 없는 경우 생성됩니다. 이 동작은 `--skip-backup` 옵션을 사용하여 재정의됩니다.

기본적으로 마이그레이션 작업은 표준 출력(STDOUT)에 마이그레이션 프로세스의 상태를 출력합니다. `--report-file <REPORT_FILE>` 옵션을 사용하는 경우 출력이 지정된 파일에 저장됩니다.

`dotnet migrate` 명령은 유효한 Preview 2 *project.json* 기반 프로젝트만 지원합니다. 즉, DNX 또는 Preview 1 *project.json* 기반 프로젝트를 MSBuild/csproj 프로젝트에 직접 마이그레이션하는 데는 사용할 수 없습니다. 먼저 수동으로 프로젝트를 Preview 2 *project.json* 기반 프로젝트로 마이그레이션한 다음 `dotnet migrate` 명령을 사용하여 프로젝트를 마이그레이션해야 합니다.

`dotnet migrate` 명령은 .NET Core 3.0 SDK부터 더 이상 사용할 수 없습니다.

## <a name="arguments"></a>인수

`PROJECT_JSON/GLOBAL_JSON/SOLUTION_FILE/PROJECT_DIR`

다음 중 하나의 경로

* 마이그레이션할 *project.json* 파일
* *global.json* 파일: *global.json*에 지정된 폴더가 마이그레이션됩니다.
* *solution.sln* 파일: 솔루션에서 참조된 프로젝트가 마이그레이션됩니다.
* 마이그레이션할 디렉터리: 지정한 디렉터리 내에서 마이그레이션할 *project.json* 파일을 재귀적으로 검색합니다.

지정하지 않으면 현재 디렉터리로 기본 설정됩니다.

## <a name="options"></a>옵션

`--format-report-file-json <REPORT_FILE>`

사용자 메시지가 아닌 JSON으로 마이그레이션 보고서 파일을 출력합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-r|--report-file <REPORT_FILE>`

마이그레이션 보고서를 콘솔 외에도 파일에 출력합니다.

`-s|--skip-project-references [Debug|Release]`

마이그레이션 프로젝트 참조를 건너뜁니다. 기본적으로 프로젝트 참조는 재귀적으로 마이그레이션됩니다.

`--skip-backup`

마이그레이션을 완료한 후 *project.json*, *global.json* 및 *\*.xproj*를 `backup` 디렉터리로 이동하는 작업을 건너뜁니다.

`-t|--template-file <TEMPLATE_FILE>`

마이그레이션에 사용할 템플릿 csproj 파일입니다. 기본적으로 `dotnet new console`에서 삭제한 것과 동일한 템플릿이 사용됩니다.

`-v|--sdk-package-version <VERSION>`

마이그레이션된 앱에서 참조할 sdk 패키지의 버전입니다. 기본값은 `dotnet new`의 SDK 버전입니다.

`-x|--xproj-file <FILE>`

사용할 xproj 파일에 대한 경로입니다. 프로젝트 디렉터리에 둘 이상의 xproj 있을 때 필요합니다.

## <a name="examples"></a>예제

현재 디렉터리의 프로젝트와 해당하는 모든 프로젝트를 프로젝트 종속성으로 마이그레이션합니다.

`dotnet migrate`

*global.json* 파일에 포함된 프로젝트를 모두 마이그레이션합니다.

`dotnet migrate path/to/global.json`

현재 프로젝트만 마이그레이션하고 프로젝트 간(P2P) 종속성은 마이그레이션하지 않으며, 특정 SDK 버전을 사용합니다.

`dotnet migrate -s -v 1.0.0-preview4`
