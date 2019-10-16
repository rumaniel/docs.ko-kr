---
title: .NET Core SDK 원격 분석
description: 어떤 데이터가 수집되고 수집 기능을 사용하지 않도록 설정하는 방법에 대한 분석을 위해 사용량 정보를 수집하는 .NET Core SDK 원격 분석 기능을 살펴봅니다.
author: KathleenDollard
ms.date: 08/27/2019
ms.custom: seodec18
ms.openlocfilehash: 253f69392f034e330a75ed387d9346e8a5ae2a08
ms.sourcegitcommit: 77e33b682db39955e331b8e8eda4ef1925a24e78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70133689"
---
# <a name="net-core-sdk-telemetry"></a>.NET Core SDK 원격 분석

[.NET Core SDK](index.md)에는 .NET Core CLI에서 크래시가 발생할 때 사용량 현황 데이터 및 예외 정보를 수집하는 원격 분석 기능이 포함되어 있습니다. .NET Core CLI는 .NET Core SDK와 함께 제공되며 .NET Core 앱을 빌드, 테스트 및 게시하는 데 사용되는 동사 세트입니다. .NET 팀이 이 도구를 개선하려면 이 도구가 어떻게 사용되는지 이해해야 합니다. 오류에 대한 정보는 팀이 문제를 해결하고 버그를 수정하는 데 도움이 됩니다.

수집된 데이터는 익명이며 [Creative Commons Attribution 라이선스](https://creativecommons.org/licenses/by/4.0/)에 따라 모두 집계하여 게시됩니다. 

## <a name="scope"></a>범위

`dotnet`에는 앱을 실행하고 CLI 명령을 실행하는 두 가지 기능이 있습니다. `dotnet`을 사용하여 다음 형식으로 애플리케이션을 시작하는 경우 원격 분석이 ‘수집되지 않습니다’. 

- `dotnet [path-to-app].dll`

다음과 같은 [.NET Core CLI 명령](index.md)을 사용하는 경우 원격 분석이 ‘수집됩니다’. 

- `dotnet build`
- `dotnet pack`
- `dotnet run`

## <a name="how-to-opt-out"></a>옵트아웃(opt out)하는 방법

.NET Core SDK 원격 분석 기능은 기본적으로 사용됩니다. 원격 분석 기능을 옵트아웃하려면 `DOTNET_CLI_TELEMETRY_OPTOUT` 환경 변수를 `1` 또는 `true`로 설정합니다. 

설치에 성공하면 .NET Core SDK 설치 관리자는 단일 원격 분석 항목을 보냅니다. 옵트아웃하려면 .NET Core SDK를 설치하기 전에 `DOTNET_CLI_TELEMETRY_OPTOUT` 환경 변수를 설정합니다.

## <a name="disclosure"></a>공개

.NET Core SDK는 [.NET Core CLI 명령](index.md) 중 하나(예: `dotnet build`)를 처음 실행할 때 다음과 비슷한 텍스트를 표시합니다. 실행 중인 SDK 버전에 따라 텍스트가 약간 달라질 수 있습니다. 이 "첫 실행" 경험이 Microsoft가 사용자에게 데이터 수집에 대해 알리는 방법입니다.

```console
Telemetry
---------
The .NET Core tools collect usage data in order to help us improve your experience. The data is anonymous. It is collected by Microsoft and shared with the community. You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.

Read more about .NET Core CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry
```

## <a name="data-points"></a>데이터 요소

이 원격 분석 기능은 사용자 이름이나 전자 메일 주소 등의 개인 데이터를 수집하지 않습니다. 코드를 검사하지 않고 이름, 리포지토리 또는 작성자와 같은 프로젝트 수준 데이터를 추출하지 않습니다. 데이터는 [Azure Monitor](https://azure.microsoft.com/services/monitor/) 기술을 사용하여 Microsoft 서버로 안전하게 전송되고, 제한된 액세스를 기준으로 보관되고, 안전한 [Azure Storage](https://azure.microsoft.com/services/storage/) 시스템에서 엄격한 보안 제어에 따라 게시됩니다.

개인 정보 보호는 Microsoft에 중요합니다. 원격 분석이 중요한 데이터를 수집하고 있는지 또는 데이터가 안전하지 않거나 부적절한 방식으로 처리되고 있는지 의심스러운 경우 조사를 위해 [dotnet/cli](https://github.com/dotnet/cli/issues) 리포지토리에서 이슈를 보고하거나 [dotnet@microsoft.com](mailto:dotnet@microsoft.com)에 전자 메일을 보내세요.

원격 분석 기능은 다음 데이터를 수집합니다.

| SDK 버전 | 데이터 |
|--------------|------|
| 모두          | 호출의 타임스탬프 |
| 모두          | 2\.1부터 해시된 호출된 명령(예: “build”) |
| 모두          | 지리적 위치를 확인하는 데 사용되는 8진수 IP 주소 3개 |
| 모두          | 운영 체제 및 버전 |
| 모두          | SDK가 실행되고 있는 RID(런타임 ID) |
| 모두          | .NET Core SDK 버전 |
| 모두          | 원격 분석 프로필: 명시적 사용자 옵트인과 함께 사용되고 Microsoft에서 내부적으로만 사용되는 선택적 값 |
| 2\.0 이상        | 명령 인수 및 옵션: 알려진 인수 및 옵션만 수집됩니다(임의 문자열이 아님). [수집된 옵션](#collected-options)을 참조하세요. 2\.1.300 이후에 해시됩니다. |
| 2\.0 이상         | SDK가 컨테이너에서 실행 중인지 여부 |
| 2\.0 이상         | 2\.1부터 해시된 `TargetFramework` 이벤트의 대상 프레임워크 |
| 2\.0 이상         | 해시된 MAC(미디어 액세스 제어) 주소: 머신의 암호화된(SHA256) 익명 및 고유 ID |
| 2\.0 이상         | 해시된 현재 작업 디렉터리 |
| 2\.0 이상         | 해시된 설치 관리자 exe 파일 이름을 사용하는 설치 성공 보고서 |
| 2\.1.300 이상     | 커널 버전 |
| 2\.1.300 이상     | Libc 릴리스/버전 |
| 3\.0.100 이상     | 출력이 리디렉션되었는지 여부(true 또는 false) |
| 3\.0.100 이상     | CLI/SDK 크래시 발생 시 예외 형식 및 해당 스택 추적(전송된 스택 추적에는 CLI/SDK 코드만 포함됨). 자세한 내용은 [수집된 .NET Core CLI/SDK 크래시 예외 원격 분석](#net-core-clisdk-crash-exception-telemetry-collected)을 참조하세요. |

### <a name="collected-options"></a>수집된 옵션

특정 명령은 추가 데이터를 보냅니다. 명령의 하위 집합은 첫 번째 인수를 보냅니다.

| 명령               | 전송된 첫 번째 인수 데이터                |
|-----------------------|-----------------------------------------|
| `dotnet help <arg>`   | 명령 도움말이 쿼리됩니다.  |
| `dotnet new <arg>`    | 템플릿 이름(해시)             |
| `dotnet add <arg>`    | 단어 `package` 또는 `reference`      |
| `dotnet remove <arg>` | 단어 `package` 또는 `reference`      |
| `dotnet list <arg>`   | 단어 `package` 또는 `reference`      |
| `dotnet sln <arg>`    | 단어 `add`, `list` 또는 `remove`    |
| `dotnet nuget <arg>`  | 단어 `delete`, `locals` 또는 `push` |

명령 하위 집합은 해당 값과 함께 사용되는 경우 선택된 옵션을 보냅니다.

| 옵션                  | 명령                                                                                       |
|-------------------------|------------------------------------------------------------------------------------------------|
| `--verbosity`           | 모든 명령                                                                                   |
| `--language`            | `dotnet new`                                                                                   |
| `--configuration`       | `dotnet build`, `dotnet clean`, `dotnet publish`, `dotnet run`, `dotnet test`                  |
| `--framework`           | `dotnet build`, `dotnet clean`, `dotnet publish`, `dotnet run`, `dotnet test`, `dotnet vstest` |
| `--runtime`             | `dotnet build`, `dotnet publish`                                                              |
| `--platform`            | `dotnet vstest`                                                                                |
| `--logger`              | `dotnet vstest`                                                                                |
| `--sdk-package-version` | `dotnet migrate`                                                                               |

`--verbosity` 및 `--sdk-package-version`을 제외하면 다른 모든 값은 .NET Core 2.1.100 SDK부터 해시됩니다.

## <a name="net-core-clisdk-crash-exception-telemetry-collected"></a>수집된 .NET Core CLI/SDK 크래시 예외 원격 분석

.NET Core CLI/SDK에서 크래시가 발생하면 CLI/SDK 코드의 예외 및 스택 추적 이름을 수집합니다. 이 정보는 문제를 평가하고 .NET Core SDK 및 CLI의 품질을 향상하기 위해 수집됩니다. 이 문서에서는 수집하는 데이터에 대한 정보를 제공합니다. 자체 .NET Core SDK 버전을 빌드하는 사용자가 실수로 개인 정보나 중요한 정보를 공개하지 않도록 하는 방법에 대한 팁도 제공합니다.

### <a name="types-of-collected-data"></a>수집되는 데이터의 유형

.NET Core CLI는 애플리케이션의 예외가 아닌 CLI/SDK 예외에 대한 정보를 수집합니다. 수집된 데이터에는 예외 및 스택 추적의 이름이 포함됩니다. 이 스택 추적은 CLI/SDK 코드와 관련됩니다.

다음 예제는 수집되는 데이터의 종류를 보여 줍니다.

```
System.IO.IOException
at System.ConsolePal.WindowsConsoleStream.Write(Byte[] buffer, Int32 offset, Int32 count)
at System.IO.StreamWriter.Flush(Boolean flushStream, Boolean flushEncoder)
at System.IO.StreamWriter.Write(Char[] buffer)
at System.IO.TextWriter.WriteLine()
at System.IO.TextWriter.SyncTextWriter.WriteLine()
at Microsoft.DotNet.Cli.Utils.Reporter.WriteLine()
at Microsoft.DotNet.Tools.Run.RunCommand.EnsureProjectIsBuilt()
at Microsoft.DotNet.Tools.Run.RunCommand.Execute()
at Microsoft.DotNet.Tools.Run.RunCommand.Run(String[] args)
at Microsoft.DotNet.Cli.Program.ProcessArgs(String[] args, ITelemetry telemetryClient)
at Microsoft.DotNet.Cli.Program.Main(String[] args)
```

### <a name="avoid-inadvertent-disclosure-information"></a>의도하지 않은 정보 공개 방지

.NET Core 기여자 및 자체적으로 빌드한 .NET Core SDK 버전을 실행하는 사용자는 SDK 소스 코드의 경로를 고려해야 합니다. 사용자 지정 디버그 빌드이거나 사용자 지정 빌드 기호 파일로 구성된 .NET Core SDK를 사용하는 동안 크래시가 발생하면 빌드 머신의 SDK 소스 파일 경로는 스택 추적의 일부로 수집되며 해시되지 않습니다.

따라서 .NET Core SDK의 사용자 지정 빌드는 경로 이름이 개인 정보나 중요한 정보를 공개하는 디렉터리에 있으면 안 됩니다. 

## <a name="see-also"></a>참고 항목

- [.NET Core CLI 원격 분석 - 2019 Q2 데이터](https://dotnet.microsoft.com/platform/telemetry/dotnet-core-cli-2019q2)
- [원격 분석 참조 소스(dotnet/cli 리포지토리)](https://github.com/dotnet/cli/tree/master/src/dotnet/Telemetry)
