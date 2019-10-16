---
title: 사용할 .NET Core 버전 선택
description: .NET Core에서 프로그램에 대한 런타임 버전을 자동으로 찾아 선택하는 방법을 알아봅니다. 또한 이 문서에서는 특정 버전을 강제로 적용하는 방법을 설명합니다.
author: thraka
ms.author: adegeo
ms.date: 06/26/2019
ms.custom: seodec18
ms.openlocfilehash: db42ba4916aad739bd2c9d8b547f16022fce44bd
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70104941"
---
# <a name="select-the-net-core-version-to-use"></a>사용할 .NET Core 버전 선택

이 문서에서는 버전을 선택하기 위해 .NET Core 도구, SDK 및 런타임에서 사용되는 정책에 대해 설명합니다. 이러한 정책은 지정된 버전을 사용하여 애플리케이션을 실행하고 개발자와 최종 사용자 모두의 머신을 쉽게 업그레이드할 수 있도록 하는 균형을 제공합니다. 이러한 정책은 다음 작업을 수행합니다.

- 보안 및 안정성 업데이트를 포함하여 .NET Core를 쉽고 효율적으로 배포합니다.
- 대상 런타임과 독립적으로 최신 도구 및 명령을 사용합니다.

버전을 선택하는 경우 발생하는 상황은 다음과 같습니다.

- SDK 명령을 실행할 때 [SDK에서 설치된 최신 버전을 사용](#the-sdk-uses-the-latest-installed-version)합니다.
- 어셈블리를 빌드할 때 [대상 프레임워크 모니커에서 빌드 시간 API를 정의](#target-framework-monikers-define-build-time-apis)합니다.
- .NET Core 애플리케이션을 실행할 때 [대상 프레임워크 종속 애플리케이션이 롤포워드](#framework-dependent-apps-roll-forward)됩니다.
- 자체 포함 애플리케이션을 게시할 때 [자체 포함 배포에는 선택한 런타임](#self-contained-deployments-include-the-selected-runtime)이 포함됩니다.

이 문서의 나머지 부분에서는 이 네 가지 시나리오를 검토합니다.

## <a name="the-sdk-uses-the-latest-installed-version"></a>SDK에서 설치된 최신 버전 사용

SDK 명령에는 `dotnet new` 및 `dotnet run`이 포함됩니다. .NET Core CLI는 모든 `dotnet` 명령의 SDK 버전을 선택해야 합니다. 다음의 경우에도 기본적으로 머신에 설치된 최신 SDK를 사용합니다.

- 프로젝트가 이전 버전의 .NET Core 런타임을 대상으로 하는 경우
- 최신 버전의 .NET Core SDK가 미리 보기 버전인 경우

이전의 .NET Core 런타임 버전을 대상으로 하면서 최신 SDK 기능과 향상된 기능을 활용할 수 있습니다. 모든 프로젝트에 대해 동일한 SDK 도구를 사용하여 여러 프로젝트에서 .NET Core의 여러 런타임 버전을 대상으로 지정할 수 있습니다.

드물지만 경우에 따라 이전 버전의 SDK를 사용해야 할 수도 있습니다. 해당 버전은 [*global.json* 파일](../tools/global-json.md)에 지정합니다. "최신 버전 사용" 정책은 *global.json*을 사용하여 설치된 최신 버전보다 이전의 .NET Core SDK 버전을 지정한다는 것을 의미합니다.

*global.json*은 파일 계층 구조에서 원하는 위치에 배치할 수 있습니다. CLI는 검색된 첫 번째 *global.json*의 프로젝트 디렉터리에서 위쪽 방향으로 검색합니다. 파일 시스템의 해당 위치에 따라 지정된 *global.json*이 적용되는 프로젝트를 제어합니다. .NET CLI는 현재 작업 디렉터리에서 위쪽 경로로 반복적으로 탐색하면서 *global.json* 파일을 검색합니다. 검색된 첫 번째 *global.json* 파일에서 사용된 버전을 지정합니다. 해당 버전이 설치되어 있으면 이 버전이 사용됩니다. *global.json*에 지정된 SDK가 없으면 .NET CLI에서 설치된 최신 SDK로 롤포워드합니다. 롤포워드는 *global.json* 파일이 없는 경우 기본 동작과 동일합니다.

다음 예제에서는 *global.json* 구문을 보여 줍니다.

``` json
{
  "sdk": {
    "version": "2.0.0"
  }
}
```

SDK 버전을 선택하는 프로세스는 다음과 같습니다.

1. `dotnet`은 현재 작업 디렉터리에서 위쪽 경로로의 역방향으로 반복하여 탐색하면서 *global.json* 파일을 검색합니다.
1. `dotnet`은 검색된 첫 번째 *global.json*에 지정된 SDK를 사용합니다.
1. *global.json*이 없으면 `dotnet`에서 설치된 최신 SDK를 사용합니다.

*global.json*에 있는 문서의 [일치 규칙](../tools/global-json.md#matching-rules) 섹션에서 SDK 버전 선택에 대해 자세히 알아볼 수 있습니다.

## <a name="target-framework-monikers-define-build-time-apis"></a>대상 프레임워크 모니커에서 빌드 시간 API 정의

**TFM**(대상 프레임워크 모니커)에 정의된 API에 대해 프로젝트를 빌드합니다. 프로젝트 파일에서 [대상 프레임워크](../../standard/frameworks.md)를 지정합니다. 다음 예제와 같이 프로젝트 파일에서 `TargetFramework` 요소를 설정합니다.

``` xml
<TargetFramework>netcoreapp2.0</TargetFramework>
```

여러 개의 TFM에 대해 프로젝트를 구축할 수 있습니다. 여러 대상 프레임워크를 설정하는 것은 라이브러리에서 더 일반적이지만, 애플리케이션에서도 수행할 수 있습니다. `TargetFrameworks` 속성(`TargetFramework`의 복수형)을 지정합니다. 대상 프레임워크는 다음 예제와 같이 세미콜론으로 구분됩니다.

``` xml
<TargetFrameworks>netcoreapp2.0;net47</TargetFrameworks>
```

지정된 SDK는 함께 제공되는 런타임의 대상 프레임워크로 제한된 프레임워크의 고정된 집합을 지원합니다. 예를 들어 .NET Core 2.0 SDK에는 `netcoreapp2.0` 대상 프레임워크의 구현인 .NET Core 2.0 런타임이 포함되어 있습니다. .NET Core 2.0 SDK는 `netcoreapp1.0`, `netcoreapp1.1` 및 `netcoreapp2.0`을 지원하지만, `netcoreapp2.1`(또는 그 이상)은 지원하지 않습니다. .NET Core 2.1 SDK를 설치하여 `netcoreapp2.1`을 빌드합니다.

또한 .NET Standard 대상 프레임워크도 SDK에서 제공하는 런타임의 대상 프레임워크로 제한됩니다. .NET Core 2.0 SDK는 `netstandard2.0`으로 제한됩니다.

## <a name="framework-dependent-apps-roll-forward"></a>프레임워크 종속 응용 프로그램 롤포워드

[`dotnet run`](../tools/dotnet-run.md)를 사용하여 소스에서, [`dotnet myapp.dll`](../tools/dotnet.md#description)을 사용하여 [**프레임워크 종속 배포**](../deploying/index.md#framework-dependent-deployments-fdd)에서 또는 `myapp.exe`를 사용하여 [**프레임워크 종속 실행 파일**](../deploying/index.md#framework-dependent-executables-fde)에서 애플리케이션을 실행하는 경우 `dotnet` 실행 파일이 애플리케이션의 **호스트**입니다.

호스트는 머신에 설치된 최신 패치 버전을 선택합니다. 예를 들어 프로젝트 파일에서 `netcoreapp2.0`을 지정하고 `2.0.4`가 설치된 최신 .NET 런타임인 경우 `2.0.4` 런타임이 사용됩니다.

허용되는 `2.0.*` 버전이 없으면 새 `2.*` 버전이 사용됩니다. 예를 들어 `netcoreapp2.0`을 지정하고 `2.1.0`만 설치된 경우 `2.1.0` 런타임을 사용하여 애플리케이션이 실행됩니다. 이 동작을 "부 버전 롤포워드"라고 합니다. 또한 더 낮은 버전은 고려되지 않습니다. 허용 가능한 런타임이 설치되어 있지 않으면 애플리케이션이 실행되지 않습니다.

2\.0을 대상으로 하는 경우 몇 가지 사용 예에서 동작을 시연합니다.

- 2.0이 지정됩니다. 2.0.5는 설치된 가장 높은 패치 버전입니다. 2.0.5가 사용됩니다.
- 2.0이 지정됩니다. 2\.0.* 버전이 설치되어 있지 않습니다. 1.1.1은 설치된 가장 높은 런타임 버전입니다. 오류 메시지가 표시됩니다.
- 2.0이 지정됩니다. 2\.0.* 버전이 설치되어 있지 않습니다. 2.2.2는 설치된 가장 높은 2.x 런타임 버전입니다. 2.2.2가 사용됩니다.
- 2.0이 지정됩니다. 2\.x 버전이 설치되어 있지 않습니다. 3.0.0이 설치됩니다. 오류 메시지가 표시됩니다.

부 버전 롤포워드에는 최종 사용자에게 영향을 줄 수 있는 하나의 부작용이 있습니다. 다음 시나리오를 고려하세요.

1. 애플리케이션은 2.0이 필수가 되도록 지정합니다.
2. 실행 시 버전 2.0.*은 설치되지 않지만 2.2.2는 설치됩니다. 버전 2.2.2가 사용됩니다.
3. 나중에 사용자가 2.0.5를 설치하고 애플리케이션을 다시 실행하면 이제 2.0.5가 사용됩니다.

2\.0.5와 2.2.2는 다르게 동작할 수도 있습니다. 특히 이진 데이터를 직렬화하는 것과 같은 시나리오에서는 다르게 동작합니다.

## <a name="self-contained-deployments-include-the-selected-runtime"></a>자체 포함 배포에 선택한 런타임 포함

애플리케이션을 [**자체 포함 배포**](../deploying/index.md#self-contained-deployments-scd)로 게시할 수 있습니다. 이 방법은 .NET Core 런타임 및 라이브러리를 애플리케이션과 함께 번들로 제공합니다. 자체 포함 배포에는 런타임 환경에 대한 종속성이 없습니다. 런타임 버전 선택은 런타임이 아니라 게시 시간에 수행됩니다.

게시 프로세스는 지정된 런타임 제품군의 최신 패치 버전을 선택합니다. 예를 들어 .NET Core 2.0.4가 .NET Core 2.0 런타임 제품군의 최신 패치 버전인 경우 `dotnet publish`는 .NET Core 2.0.4를 선택합니다. 대상 프레임워크(설치된 최신 보안 패치 포함)는 애플리케이션과 함께 패키지됩니다.

애플리케이션에 대해 지정된 최소 버전이 충족되지 않으면 오류가 발생합니다. `dotnet publish`는 최신 런타임 패치 버전(지정된 major.minor 버전 제품군 내에서)에 바인딩합니다. `dotnet publish`는 `dotnet run`의 롤포워드 의미 체계를 지원하지 않습니다. 패치 및 자체 포함 배포에 대한 자세한 내용은 .NET Core 애플리케이션 배포의 [런타임 패치 선택](../deploying/runtime-patch-selection.md)에 대한 문서를 참조하세요.

자체 포함 배포에는 특정 패치 버전이 필요할 수 있습니다. 다음 예제와 같이 프로젝트 파일에서 최소 런타임 패치 버전(더 높거나 낮은 버전)을 재정의할 수 있습니다.

``` xml
<RuntimeFrameworkVersion>2.0.4</RuntimeFrameworkVersion>
```

`RuntimeFrameworkVersion` 요소는 기본 버전 정책보다 우선합니다. 자체 포함 배포의 경우 `RuntimeFrameworkVersion`은 *정확한* 런타임 프레임워크 버전을 지정합니다. 프레임워크 종속 애플리케이션의 경우 `RuntimeFrameworkVersion`은 필요한 *최소* 런타임 프레임워크 버전을 지정합니다.
