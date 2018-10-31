---
title: .NET Core SDK 원격 분석
description: 어떤 데이터가 수집되고 수집 기능을 사용하지 않도록 설정하는 방법에 대한 분석을 위해 사용 정보를 수집하는 .NET Core SDK 원격 분석 기능을 살펴봅니다.
author: richlander
ms.author: mairaw
ms.date: 06/20/2018
ms.openlocfilehash: a20d79e132726cb342064b681218ee568fab2c13
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48841627"
---
# <a name="net-core-sdk-telemetry"></a>.NET Core SDK 원격 분석

[.NET Core SDK](index.md)에는 사용 정보를 수집하는 [원격 분석 기능](https://github.com/dotnet/cli/tree/master/src/dotnet/Telemetry)이 포함되어 있습니다. .NET 팀이 이 도구를 개선하려면 이 도구가 어떻게 사용되는지 이해해야 합니다. 자세한 내용은 [What we've learned from .NET Core SDK Telemetry](https://blogs.msdn.microsoft.com/dotnet/2017/07/21/what-weve-learned-from-net-core-sdk-telemetry/)(.NET Core SDK 원격 분석에서 배운 내용)를 참조하세요.

수집된 데이터는 익명이며 Microsoft 및 커뮤니티에서 사용할 집계 형식으로 [Creative Commons Attribution 라이선스](https://creativecommons.org/licenses/by/4.0/)에 따라 게시됩니다.

## <a name="scope"></a>범위

`dotnet` 명령은 앱 및 .NET Core CLI를 시작하는 데 사용됩니다. `dotnet` 명령 자체는 원격 분석을 수집하지 않습니다. `dotnet` 명령에 따라 실행되는 .NET Core CLI 명령은 원격 분석을 수집합니다.

연결된 명령 없이 `dotnet` 명령만 사용할 경우 원격 분석을 *사용할 수 없습니다*.

- `dotnet`
- `dotnet [path-to-app]`

다음과 같은 [.NET Core CLI 명령](index.md)을 사용할 경우 원격 분석을 *사용할 수 있습니다*.

- `dotnet build`
- `dotnet pack`
- `dotnet restore`
- `dotnet run`

## <a name="how-to-opt-out"></a>옵트아웃(opt out)하는 방법

.NET Core SDK 원격 분석 기능은 기본적으로 사용됩니다. `DOTNET_CLI_TELEMETRY_OPTOUT` 환경 변수를 `1` 또는 `true`로 설정하여 원격 분석 기능을 옵트아웃(opt out)합니다.

## <a name="data-points"></a>데이터 요소

이 기능은 다음 데이터를 수집합니다.

- 호출의 타임스탬프&#8224;
- 호출된 명령(예: “build”)&#8224;
- 지리적 위치를 확인하는 데 사용되는 8진수 IP 주소 3개&#8224;
- 명령의 `ExitCode`
- Test Runner(테스트 프로젝트의 경우)
- 운영 체제 및 버전&#8224;
- 런타임 ID가 런타임 노드에 있는지 여부
- .NET Core SDK 버전&#8224;

&#8224;이 메트릭은 게시됩니다.

.NET Core SDK 2.0부터 새 데이터 요소가 수집됩니다.

- `dotnet` 명령 인수 및 옵션: 알려진 인수 및 옵션만 수집됩니다(임의 문자열이 아님).
- SDK가 컨테이너에서 실행 중인지 여부.
- 대상 프레임워크.
- 해시된 MAC 주소: 컴퓨터에 대한 암호화된(SHA256) 익명 및 고유 ID입니다. 이 메트릭은 게시되지 않습니다.
- 해시된 현재 작업 디렉터리.

이 기능은 사용자 이름이나 전자 메일 주소 등의 개인 데이터를 수집하지 않습니다. 코드를 검사하지 않고 이름, 리포지토리 또는 작성자와 같은 중요한 프로젝트 수준 데이터를 추출하지 않습니다. 데이터는 [Microsoft Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 기술을 사용하여 Microsoft 서버로 안전하게 전송되고, 제한된 액세스를 기준으로 보관되고, 안전한 [Azure Storage](https://azure.microsoft.com/services/storage/) 시스템에서 엄격한 보안 제어에 따라 게시됩니다.

.NET 팀은 도구를 사용하여 무엇을 빌드하는지가 아니라, 도구 사용 방법과 도구가 제대로 작동하는지 알고자 합니다. 원격 분석이 중요한 데이터를 수집하고 있는지 또는 데이터가 안전하지 않거나 부적절한 방식으로 처리되고 있는지 의심스러운 경우 조사를 위해 [dotnet/cli](https://github.com/dotnet/cli/issues) 리포지토리에서 문제를 보고하세요.

## <a name="published-data"></a>게시된 데이터

게시된 데이터는 분기별로 제공되고 [.NET Core SDK Usage Data](https://github.com/dotnet/core/blob/master/release-notes/cli-usage-data.md)(.NET Core SDK 사용 데이터)에 나열됩니다. 데이터 파일 열은 다음과 같습니다.

- 타임스탬프
- 발생&#8224;
- 명령
- 지리&#8225;
- OSFamily
- RuntimeID
- OSVersion
- SDKVersion

&#8224;*발생* 열에는 해당 날짜에 해당 행 메트릭에 대한 해당 명령 사용의 집계 개수가 표시됩니다.

&#8225;일반적으로 *지리* 열에는 국가 이름이 표시됩니다. 경우에 따라 연구원이 남극에서 .NET Core를 사용하거나 위치 데이터가 정확하지 않아 남극 대륙이 이 열에 표시됩니다.

### <a name="example"></a>예

| 타임스탬프      | 발생 | 명령 | 지리 | OSFamily | RuntimeID     | OSVersion | SDKVersion |
| -------------- | ----------- | ------- | --------- | -------- | ------------- | --------- | ---------- |
| 4/16/2017 0:00 | 8           | 실행     | 우간다    | Darwin   | osx.10.12-x64 | 10.12     | 1.0.1      |

### <a name="datasets"></a>데이터 집합

[2016 - Q3](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2016-q3.tsv)  
[2016 - Q4](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2016-q4.tsv)  
[2017 - Q1](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q1.tsv)  
[2017 - Q2](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q2.tsv)  
[2017 - Q3](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q3.tsv)  
[2017 - Q4](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q4.tsv)  

표준 URL 형식을 사용하여 추가 데이터 집합이 게시됩니다. `<YEAR>`를 연도로 바꾸고 `<QUARTER>`를 해당 연도의 분기로 바꿉니다(`1`, `2`, `3` 또는 `4` 사용). 파일은 *TSV*(탭으로 구분된 값) 형식입니다.

`https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-<YEAR>-q<QUARTER>.tsv`

## <a name="license"></a>라이선스

.NET Core의 Microsoft 배포는 [MICROSOFT.NET 라이브러리 EULA](https://aka.ms/dotnet-core-eula)로 허가됩니다. 이 라이선스에는 원격 분석을 구현하기 위한 “DATA” 섹션이 포함됩니다(아래 참조).

[.NET NuGet 패키지](https://www.nuget.org/profiles/dotnetframework)에는 동일한 라이선스가 사용되지만 원격 분석을 구현하지 않습니다([범위](#scope) 참조).

> 2. 데이터. 소프트웨어에서 사용자 및 사용자의 소프트웨어 사용에 대한 정보를 수집하고 이 정보를 Microsoft에 보낼 수 있습니다. Microsoft에서는 제품 및 서비스 향상을 위해 이 정보를 사용할 수 있습니다. 데이터 수집 및 사용에 대한 자세한 내용은 도움말 문서 및 개인정보처리방침(<http://go.microsoft.com/fwlink/?LinkId=528096>)을 참조하세요. 소프트웨어를 사용하려면 이러한 사례에 동의해야 합니다.

## <a name="disclosure"></a>공개

.NET Core SDK는 [.NET Core CLI 명령](index.md) 중 하나(예: `dotnet restore`)를 처음 실행할 때 다음 텍스트를 표시합니다. 실행 중인 SDK 버전에 따라 텍스트가 약간 달라질 수 있습니다. 이 "첫 실행" 경험이 Microsoft가 사용자에게 데이터 수집에 대해 알리는 방법입니다.

```console
Welcome to .NET Core!
---------------------
Learn more about .NET Core: https://aka.ms/dotnet-docs
Use 'dotnet --help' to see available commands or visit: https://aka.ms/dotnet-cli-docs

Telemetry
---------
The .NET Core tools collect usage data in order to help us improve your experience.
The data is anonymous and doesn't include command-line arguments.
The data is collected by Microsoft and shared with the community.
You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.

Read more about .NET Core CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry
```

## <a name="see-also"></a>참고 항목

- [What we've learned from .NET Core SDK Telemetry](https://blogs.msdn.microsoft.com/dotnet/2017/07/21/what-weve-learned-from-net-core-sdk-telemetry/)(.NET Core SDK 원격 분석에서 배운 내용)
- [원격 분석 참조 소스(dotnet/cli 리포지토리)](https://github.com/dotnet/cli/tree/master/src/dotnet/Telemetry)
- [.NET Core SDK Usage Data](https://github.com/dotnet/core/blob/master/release-notes/cli-usage-data.md)(.NET Core SDK 사용 데이터)
