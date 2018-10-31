---
title: global.json 개요
description: .NET Core CLI 명령을 실행할 때 global.json 파일을 사용하여 .NET Core SDK 버전을 설정하는 방법에 대해 알아보세요.
author: mairaw
ms.author: mairaw
ms.date: 07/30/2018
ms.custom: updateeachrelease
ms.openlocfilehash: 05ec296c4c8210c63c7c1b5ce63ef598ca6ac719
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48838080"
---
# <a name="globaljson-overview"></a>global.json 개요

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

*global.json* 파일을 사용하면 .NET Core CLI 명령을 실행할 때 어떤 .NET Core SDK 버전을 사용할지 정의할 수 있습니다. .NET Core SDK를 선택하는 것은 프로젝트가 대상으로 하는 런타임을 지정하는 것과는 별개입니다. .NET Core SDK 버전은 사용된 .NET Core CLI 도구의 버전을 나타냅니다. 일반적으로 최신 버전의 도구를 사용하려고 하기 때문에 *global.json* 파일이 필요하지 않습니다.

대신 런타임 지정에 대한 자세한 내용은 [대상 프레임워크](../../standard/frameworks.md)를 참조하세요.

.NET Core SDK는 현재 작업 디렉터리(반드시 프로젝트 디렉터리와 동일하지는 않음) 또는 상위 디렉터리 중 하나에서 *global.json* 파일을 찾습니다.

## <a name="globaljson-schema"></a>global.json 스키마

### <a name="sdk"></a>sdk

형식: Object

선택할 .NET Core SDK에 대한 정보를 지정합니다.

#### <a name="version"></a>버전

형식: String

사용할 .NET Core SDK의 버전입니다.

이 필드의 특징은 다음과 같습니다.

- globbing을 지원하지 않습니다. 즉, 전체 버전 번호가 지정되어야 합니다.
- 버전 범위를 지원하지 않습니다.

다음 예제에서는 *global.json* 파일의 내용을 보여줍니다.

```json
{
  "sdk": {
    "version": "2.1.300"
  }
}
```

## <a name="globaljson-and-the-net-core-cli"></a>global.json 및 .NET Core CLI

*global.json* 파일에서 어떤 버전을 설정할 수 있는지 알고 있으면 도움이 됩니다. [.NET 다운로드](https://www.microsoft.com/net/download/all) 사이트에서 지원되는 사용 가능한 SDK의 전체 목록을 찾을 수 있습니다. .NET Core SDK 2.1부터는 다음 명령을 실행하여 머신에 이미 설치된 SDK 버전을 확인할 수 있습니다.

```console
dotnet --list-sdks
```

머신에 추가 .NET Core SDK 버전을 설치하려면 [.NET 다운로드](https://www.microsoft.com/net/download/all) 사이트를 방문하세요.

다음 예제와 비슷한 [dotnet new](dotnet-new.md) 명령을 실행하여 현재 디렉터리에서 *global.json* 파일을 새로 만들 수 있습니다.

```console
dotnet new globaljson --sdk-version 2.1.300
```

## <a name="matching-rules"></a>일치 규칙

> [!NOTE]
> 일치 규칙은 .NET Core 런타임의 일부인 apphost에 의해 관리됩니다.
> 호스트의 최신 버전은 여러 런타임이 나란히 설치되어 있는 경우에 사용됩니다.

.NET Core 2.0부터는 어떤 SDK 버전을 사용할지 결정할 때 다음 규칙이 적용됩니다.

- *global.json* 파일이 없거나 *global.json*이 SDK 버전을 지정하지 않으면 최신 설치된 SDK 버전이 사용됩니다. 최신 SDK 버전은 릴리스나 시험판일 수 있으며, 이 중에 높은 버전 번호가 우선합니다.
- *global.json*이 SDK 버전을 지정하는 경우
  - 지정된 SDK 버전이 머신에서 발견되면 정확한 버전이 사용됩니다.
  - 지정된 SDK 버전이 시스템에서 발견되지 않으면 해당 버전의 최신 **패치 버전**이 사용됩니다. 설치된 최신 SDK **패치 버전**은 릴리스나 시험판일 수 있으며, 이 중에 높은 버전 번호가 우선합니다. .NET Core 2.1 이상에서는 지정된 **패치 버전**보다 낮은 **패치 버전**은 SDK 선택에서 무시됩니다.
  - 지정된 SDK 버전과 적절한 SDK **패치 버전**을 찾을 수 없으면 오류가 발생합니다.

SDK 버전은 현재 다음과 같은 부분으로 구성됩니다.

`[.NET Core major version].[.NET Core minor version].[xyz][-optional preview name]`

.NET Core SDK의 **기능 릴리스**는 SDK 버전 2.1.100 이상의 경우 번호의 마지막 부분(`xyz`)의 첫 번째 자리(`x`)로 표시됩니다. 일반적으로 .NET Core SDK는 .NET Core보다 릴리스 주기가 빠릅니다.

**패치 버전**은 SDK 버전 2.1.100 이상의 경우 번호의 마지막 부분(`xyz`)의 마지막 두 자리(`yz`)로 정의됩니다. 예를 들어, SDK 버전으로 `2.1.300`을 지정하면 SDK 선택은 최대 `2.1.399`까지 찾지만 `2.1.400`은 `2.1.300`의 패치 버전으로 간주되지 않습니다.

`2.1.100`부터 `2.1.201`까지의 .NET Core SDK 버전은 버전 번호 체계가 전환되는 중에 릴리스되었으며 `xyz` 표기법을 올바르게 처리하지 못합니다. *global.json* 파일에서 이 버전을 지정하면 지정된 버전이 대상 머신에 있는지 확인할 수 있도록 하는 것이 좋습니다.

.NET Core SDK 1.x에서는 버전을 지정하고 정확히 일치하는 버전이 발견되지 않은 경우 최신 설치된 SDK 버전이 사용되었습니다. 최신 SDK 버전은 릴리스나 시험판일 수 있으며, 이 중에 높은 버전 번호가 우선합니다.

## <a name="troubleshooting-build-warnings"></a>빌드 경고 문제 해결

> [!WARNING]
> .NET Core SDK의 미리보기 버전으로 작업하고 있습니다. SDK 버전은 현재 프로젝트의 global.json 파일을 통해 정의할 수 있습니다. 자세한 내용은 <https://go.microsoft.com/fwlink/?linkid=869452> 참조

이 경고는 [일치 규칙](#matching-rules) 섹션에서 설명한대로 .NET Core SDK의 미리보기 버전을 사용하여 프로젝트가 컴파일되고 있음을 나타냅니다. .NET Core SDK 버전은 높은 품질의 기록과 약정을 가지고 있습니다. 그러나 미리보기 버전을 사용하지 않으려면 프로젝트 계층 구조에 *global.json* 파일을 추가하여 사용할 SDK 버전을 지정하고 `dotnet --list-sdks`를 사용하여 머신에 설치된 버전을 확인합니다. 새 버전이 릴리스되었을 때 새 버전을 사용하려면 *global.json* 파일을 제거하거나 최신 버전을 사용하도록 업데이트합니다.

> [!WARNING]
> 스타트업 프로젝트 '{startupProject}'는 '.NETCoreApp' 버전 '{targetFrameworkVersion}' 프레임워크를 대상으로 합니다. 이 버전의 Entity Framework Core .NET 명령줄 도구는 버전 2.0 이상만 지원합니다. 이전 버전의 도구 사용에 대한 자세한 내용은 <https://go.microsoft.com/fwlink/?linkid=871254>를 참조하세요.

.NET Core SDK 2.1(v. 2.1.300)부터는 `dotnet ef` 명령이 SDK에 포함됩니다. 이 경고는 프로젝트가 EF Core 1.0 또는 1.1을 대상으로 하고 .NET Core SDK 2.1 이상 버전과 호환되지 않음을 나타냅니다. 프로젝트를 컴파일하려면 .NET Core SDK 2.0(v. 2.1.201) 이전 버전을 머신에 설치하고 *global.json* 파일을 사용하여 원하는 SDK 버전을 정의합니다. `dotnet ef` 명령에 대한 자세한 내용은 [EF Core .NET 명령줄 도구](/ef/core/miscellaneous/cli/dotnet)를 참조하세요.

## <a name="see-also"></a>참고 항목

* [프로젝트 SDK를 확인하는 방법](/visualstudio/msbuild/how-to-use-project-sdk#how-project-sdks-are-resolved)
