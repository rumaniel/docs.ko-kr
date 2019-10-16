---
title: dotnet test 명령
description: dotnet test 명령은 지정된 프로젝트에서 단위 테스트를 실행하는 데 사용됩니다.
ms.date: 05/29/2018
ms.openlocfilehash: c3115d546efb1f076ae9f9731f83a12183aa4154
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182506"
---
# <a name="dotnet-test"></a>dotnet test

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet test` - 단위 테스트를 실행하는 데 사용하는 .NET 테스트 드라이버입니다.

## <a name="synopsis"></a>개요

<!-- markdownlint-disable MD025 -->

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```dotnetcli
dotnet test [<PROJECT>] [-a|--test-adapter-path] [--blame] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter]
    [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] 
    [-v|--verbosity] [-- <RunSettings arguments>]

dotnet test [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```dotnetcli
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter]
    [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] [-v|--verbosity]

dotnet test [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```dotnetcli
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [-d|--diag] [-f|--framework] [--filter] [-l|--logger] [--no-build] [-o|--output] [-s|--settings] [-t|--list-tests]  [-v|--verbosity]

dotnet test [-h|--help]
```

---

## <a name="description"></a>설명

`dotnet test` 명령은 지정된 프로젝트에서 단위 테스트를 실행하는 데 사용됩니다. `dotnet test` 명령은 프로젝트에 대해 지정된 테스트 러너 콘솔 애플리케이션을 시작합니다. 테스트 러너는 단위 테스트 프레임워크(예: MSTest, NUnit 또는 xUnit)에 대해 정의된 테스트를 실행하고 각 테스트의 성공 여부를 보고합니다. 모든 테스트에 성공하면 Test Runner가 종료 코드로 0을 반환합니다. 테스트가 하나라도 실패하면 1을 반환합니다. 테스트 러너와 단위 테스트 라이브러리는 NuGet 패키지로 패키지되고 프로젝트에 대한 일반적인 종속성으로 복원됩니다.

테스트 프로젝트는 다음 샘플 프로젝트 파일에서 볼 수 있듯이 일반적인 `<PackageReference>` 요소를 사용하여 테스트 러너를 지정합니다.

[!code-xml[XUnit Basic Template](../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

## <a name="arguments"></a>인수

`PROJECT`

테스트 프로젝트의 경로입니다. 지정하지 않으면 현재 디렉터리로 기본 설정됩니다.

## <a name="options"></a>옵션

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

테스트 실행에 지정된 경로에서 사용자 지정 테스트 어댑터를 사용합니다.

`--blame`

테스트를 원인 모드로 실행합니다. 이 옵션은 테스트 호스트를 충돌시키는 문제가 있는 테스트를 격리하는 데 유용합니다. 현재 디렉터리에 크래시 전에 테스트 실행 순서를 캡처하는 *Sequence.xml*이라는 출력 파일을 만듭니다.

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`이지만 프로젝트의 구성으로 이 기본 SDK 설정이 재정의될 수 있습니다.

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

테스트 실행에 대한 데이터 수집기를 사용하도록 설정합니다. 자세한 내용은 [테스트 실행 모니터링 및 분석](https://aka.ms/vstest-collect)을 참조하세요.

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

테스트 플랫폼에 대한 진단 모드를 사용하도록 설정하고 지정된 파일에 진단 메시지를 기록합니다.

`-f|--framework <FRAMEWORK>`

특정 [프레임워크](../../standard/frameworks.md)에 대한 테스트 이진 파일을 찾습니다.

`--filter <EXPRESSION>`

지정된 식을 사용하여 현재 프로젝트의 테스트를 필터링합니다. 자세한 내용은 [필터 옵션 세부 정보](#filter-option-details) 섹션을 참조하세요. 선택적 단위 테스트 필터링을 사용하는 방법에 대한 자세한 내용 및 예제는 [선택적 단위 테스트 실행](../testing/selective-unit-tests.md)을 참조하세요.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-l|--logger <LoggerUri/FriendlyName>`

테스트 결과에 대해 로거를 지정합니다.

`--no-build`

테스트 프로젝트를 실행하기 전에 빌드하지 않습니다. 또한 `--no-restore` 플래그를 암시적으로 설정합니다.

`--no-restore`

명령을 실행할 때 암시적 복원을 실행하지 않습니다.

`-o|--output <OUTPUT_DIRECTORY>`

실행할 이진 파일을 찾을 디렉터리입니다.

`-r|--results-directory <PATH>`

테스트 결과가 배치될 디렉터리입니다. 지정한 디렉터리가 없으면 생성됩니다.

`-s|--settings <SETTINGS_FILE>`

테스트 실행에 사용할 `.runsettings` 파일입니다. [`.runsettings` 파일을 사용하여 단위 테스트를 구성합니다.](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)

`-t|--list-tests`

현재 프로젝트에서 검색된 테스트를 모두 나열합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

`RunSettings arguments`

테스트를 위해 RunSettings 구성으로 전달되는 인수입니다. 인수는 “-- ” 뒤에 `[name]=[value]` 쌍으로 지정됩니다(-- 뒤 공백 주의). 공백은 여러 `[name]=[value]` 쌍을 구분하는 데 사용됩니다.

예: `dotnet test -- MSTest.DeploymentEnabled=false MSTest.MapInconclusiveToFailed=True`

RunSettings에 대한 자세한 내용은 [vstest.console.exe: Passing RunSettings args(vstest.console.exe: RunSettings 인수 전달)](https://github.com/Microsoft/vstest-docs/blob/master/docs/RunSettingsArguments.md)를 참조하세요.

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

테스트 실행에 지정된 경로에서 사용자 지정 테스트 어댑터를 사용합니다.

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`이지만 프로젝트의 구성으로 이 기본 SDK 설정이 재정의될 수 있습니다.

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

테스트 실행에 대한 데이터 수집기를 사용하도록 설정합니다. 자세한 내용은 [테스트 실행 모니터링 및 분석](https://aka.ms/vstest-collect)을 참조하세요.

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

테스트 플랫폼에 대한 진단 모드를 사용하도록 설정하고 지정된 파일에 진단 메시지를 기록합니다.

`-f|--framework <FRAMEWORK>`

특정 [프레임워크](../../standard/frameworks.md)에 대한 테스트 이진 파일을 찾습니다.

`--filter <EXPRESSION>`

지정된 식을 사용하여 현재 프로젝트의 테스트를 필터링합니다. 자세한 내용은 [필터 옵션 세부 정보](#filter-option-details) 섹션을 참조하세요. 선택적 단위 테스트 필터링을 사용하는 방법에 대한 자세한 내용 및 예제는 [선택적 단위 테스트 실행](../testing/selective-unit-tests.md)을 참조하세요.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-l|--logger <LoggerUri/FriendlyName>`

테스트 결과에 대해 로거를 지정합니다.

`--no-build`

테스트 프로젝트를 실행하기 전에 빌드하지 않습니다. 또한 `--no-restore` 플래그를 암시적으로 설정합니다.

`--no-restore`

명령을 실행할 때 암시적 복원을 실행하지 않습니다.

`-o|--output <OUTPUT_DIRECTORY>`

실행할 이진 파일을 찾을 디렉터리입니다.

`-r|--results-directory <PATH>`

테스트 결과가 배치될 디렉터리입니다. 지정한 디렉터리가 없으면 생성됩니다.

`-s|--settings <SETTINGS_FILE>`

테스트 실행에 사용할 `.runsettings` 파일입니다. [`.runsettings` 파일을 사용하여 단위 테스트를 구성합니다.](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)

`-t|--list-tests`

현재 프로젝트에서 검색된 테스트를 모두 나열합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

테스트 실행에 지정된 경로에서 사용자 지정 테스트 어댑터를 사용합니다.

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`이지만 프로젝트의 구성으로 이 기본 SDK 설정이 재정의될 수 있습니다.

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

테스트 플랫폼에 대한 진단 모드를 사용하도록 설정하고 지정된 파일에 진단 메시지를 기록합니다.

`-f|--framework <FRAMEWORK>`

특정 [프레임워크](../../standard/frameworks.md)에 대한 테스트 이진 파일을 찾습니다.

`--filter <EXPRESSION>`

지정된 식을 사용하여 현재 프로젝트의 테스트를 필터링합니다. 자세한 내용은 [필터 옵션 세부 정보](#filter-option-details) 섹션을 참조하세요. 선택적 단위 테스트 필터링을 사용하는 방법에 대한 자세한 내용 및 예제는 [선택적 단위 테스트 실행](../testing/selective-unit-tests.md)을 참조하세요.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`-l|--logger <LoggerUri/FriendlyName>`

테스트 결과에 대해 로거를 지정합니다.

`--no-build`

테스트 프로젝트를 실행하기 전에 빌드하지 않습니다.

`-o|--output <OUTPUT_DIRECTORY>`

실행할 이진 파일을 찾을 디렉터리입니다.

`-s|--settings <SETTINGS_FILE>`

테스트 실행에 사용할 `.runsettings` 파일입니다. [`.runsettings` 파일을 사용하여 단위 테스트를 구성합니다.](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)

`-t|--list-tests`

현재 프로젝트에서 검색된 테스트를 모두 나열합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

---

## <a name="examples"></a>예

현재 디렉터리에 있는 프로젝트에서 테스트를 실행합니다.

`dotnet test`

`test1` 프로젝트에서 테스트를 실행합니다.

`dotnet test ~/projects/test1/test1.csproj`

현재 디렉터리의 프로젝트에서 테스트를 실행하고 trx 형식으로 테스트 결과 파일을 생성합니다.

`dotnet test --logger trx`

## <a name="filter-option-details"></a>필터 옵션 세부 정보

`--filter <EXPRESSION>`

`<Expression>`에 `<property><operator><value>[|&<Expression>]` 형식이 있습니다.

`<property>`은(는) `Test Case`의 특성입니다. 다음은 인기 있는 단위 테스트 프레임 워크에서 지원되는 속성입니다.

| 테스트 프레임워크 | 지원되는 속성                                                                                      |
| -------------- | --------------------------------------------------------------------------------------------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>name</li><li>ClassName</li><li>우선 순위</li><li>TestCategory</li></ul> |
| xUnit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>특성</li></ul>                                   |

`<operator>`은(는) 속성과 값 사이의 관계를 설명합니다.

| 연산자 | 함수        |
| :------: | --------------- |
| `=`      | 정확하게 일치     |
| `!=`     | 정확하게 일치하지 않음 |
| `~`      | 포함        |

`<value>`는 문자열입니다. 모든 조회는 대/소문자를 구분합니다.

`<operator>`이(가) 없는 식은 `FullyQualifiedName` 속성의 `contains`(으)로 자동으로 간주됩니다(예를 들어 `dotnet test --filter xyz`과(와) `dotnet test --filter FullyQualifiedName~xyz`이(가) 동일).

식은 조건부 연산자와 조인할 수 있습니다.

| 연산자            | 함수 |
| ------------------- | -------- |
| <code>&#124;</code> | 또는       |
| `&`                 | AND      |

조건부 연산자를 사용 하는 경우 식을 괄호로 묶을 수 있습니다(예: `(Name~TestMethod1) | (Name~TestMethod2)`).

선택적 단위 테스트 필터링을 사용하는 방법에 대한 자세한 내용 및 예제는 [선택적 단위 테스트 실행](../testing/selective-unit-tests.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [프레임워크 및 대상](../../standard/frameworks.md)
- [.NET Core RID(런타임 식별자) 카탈로그](../rid-catalog.md)
