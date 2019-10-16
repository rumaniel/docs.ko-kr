---
title: .NET 라이브러리에 대한 플랫폼 간 대상 지정
description: 플랫폼 간 .NET 라이브러리를 만드는 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: 6bd310f2e4b7a9bd7bb550ed9c7da9ebabdf64ba
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53129716"
---
# <a name="cross-platform-targeting"></a>플랫폼 간 대상 지정

최신 .NET은 여러 운영 체제와 디바이스를 지원합니다. .NET 오픈 소스 라이브러리는 Azure에 호스트되는 ASP.NET 웹 사이트를 빌드하든, Unity에서 .NET 게임을 빌드하든 간에, 가능한 한 많은 개발자를 지원하는 것이 중요합니다.

## <a name="net-standard"></a>.NET Standard

.NET Standard는 .NET 라이브러리에 플랫폼 간 지원을 추가하는 가장 좋은 방법입니다. [.NET Standard](../net-standard.md)는 모든 .NET 구현에서 사용할 수 있는 .NET API 사양입니다. .NET Standard를 대상으로 지정하면, 지정된 .NET Standard 버전에 있는 API를 사용하도록 제한된 라이브러리를 생성할 수 있습니다. 이 경우, 해당 버전의 .NET Standard를 구현하는 모든 플랫폼에서 라이브러리를 사용할 수 있습니다.

![.NET Standard](./media/cross-platform-targeting/platforms-netstandard.png ".NET Standard")

.NET Standard를 대상으로 지정하고 프로젝트를 성공적으로 컴파일한다고 해서 라이브러리가 모든 플랫폼에서 실행되는 것은 아닙니다.

1. 플랫폼 특정 API는 다른 플랫폼에서 실패합니다. 예를 들어 <xref:Microsoft.Win32.Registry?displayProperty=nameWithType>은 Windows에서 성공하지만, 다른 OS에서 사용할 때는 <xref:System.PlatformNotSupportedException>을 throw합니다.
2. API가 다르게 동작할 수 있습니다. 예를 들어 응용 프로그램이 iOS 또는 UWP에서 Ahead-Of-Time 컴파일을 사용할 때 리플렉션 API는 서로 다른 성능 특성을 갖습니다.

> [!TIP]
> .NET 팀은 가능한 문제 검색에 도움이 되는 [Roslyn 분석기를 제공](../analyzers/api-analyzer.md)합니다.

**✔️** `netstandard2.0` 대상을 포함하여 시작합니다.

> 대부분의 범용 라이브러리는 .NET Standard 2.0 외부의 API가 필요하지 않습니다. .NET Standard 2.0은 모든 최신 플랫폼에서 지원되며, 하나의 대상으로 여러 플랫폼을 지원하는 권장 방법입니다.

**❌** `netstandard1.x` 대상을 포함하지 않습니다.

> .NET Standard 1.x는 세분화된 NuGet 패키지 집합으로 배포되어 큰 패키지 종속성 그래프를 만들기 때문에 개발자가 빌드 시 많은 패키지를 다운로드해야 합니다. .NET Framework 4.6.1, UWP 및 Xamarin을 포함한 최신 .NET 플랫폼은 모두 .NET Standard 2.0을 지원합니다. 특별히 이전 플랫폼을 대상으로 지정해야 하는 경우에만 .NET Standard 1.x를 대상으로 지정해야 합니다.

**✔️** `netstandard1.x` 대상이 필요한 경우 `netstandard2.0` 대상을 포함합니다.

> 이전 플랫폼도 계속 작동하고 `netstandard1.x` 대상을 사용하도록 대체되는 동시에, .NET Standard 2.0을 지원하는 모든 플랫폼은 `netstandard2.0` 대상을 사용하고 더 작은 패키지 그래프의 혜택을 얻게 됩니다.

**❌** 라이브러리가 플랫폼 특정 앱 모델을 사용하는 경우 .NET Standard 대상을 포함하지 않습니다.

> 예를 들어 UWP 제어 도구 키트 라이브러리는 UWP에서만 사용할 수 있는 앱 모델에 종속됩니다. 앱 모델 특정 API는 .NET Standard에서 사용할 수 없습니다.

## <a name="multi-targeting"></a>멀티 타기팅

라이브러리에서 프레임워크 특정 API에 액세스해야 하는 경우도 있습니다. 프레임워크 특정 API를 호출하는 가장 좋은 방법은 단일 프레임워크가 아니라 많은 [.NET 대상 프레임워크](../frameworks.md)용으로 사용자 프로젝트를 빌드하는 멀티 타기팅을 사용하는 것입니다.

소비자가 개별 프레임워크용으로 빌드할 필요가 없도록 보호하려면 .NET Standard 출력과 하나 이상의 프레임워크 특정 출력을 사용해야 합니다. 멀티 타기팅을 사용하면 모든 어셈블리가 단일 NuGet 패키지 안에 패키지됩니다. 그러면 소비자가 동일한 패키지를 참조할 수 있으며, NuGet이 적절한 구현을 선택합니다. NuGet 패키지가 프레임워크 특정 구현을 제공하는 경우를 제외하고, 사용자 .NET Standard 라이브러리는 모든 곳에서 사용되는 대체 라이브러리 역할을 합니다. 멀티 타기팅을 통해 코드에서 조건부 컴파일을 사용하고 프레임워크 특정 API를 호출할 수 있습니다.

![여러 어셈블리가 포함된 NuGet 패키지](./media/cross-platform-targeting/nuget-package-multiple-assemblies.png "여러 어셈블리가 포함된 NuGet 패키지")

**✔️** .NET Standard 외에도 .NET 구현을 대상으로 지정합니다.

> .NET 구현을 대상으로 지정하면 .NET Standard 외부에 있는 플랫폼 특정 API를 호출할 수 있습니다.
>
> 이때 .NET Standard에 대한 지원을 삭제하지 마세요. 대신, 구현에서 throw하고 기능 API를 제공합니다. 이렇게 하면 사용자 라이브러리를 어느 곳에서나 사용할 수 있으며 런타임 기능 강화가 지원됩니다.

**❌** 모든 대상에 대해 소스 코드가 동일한 경우 .NET Standard 대상 지정뿐만 아니라 멀티 대상 지정도 피하세요.

> NuGet에서 자동으로 .NET Standard 어셈블리를 사용합니다. 개별 .NET 구현을 대상으로 지정하면 아무 혜택 없이 `*.nupkg` 크기만 증가합니다.

**✔️** `netstandard2.0` 대상을 제공할 때 `net461`의 대상을 추가합니다. 

> .NET Framework의 .NET Standard 2.0을 사용하는 경우 .NET Framework 4.7.2에서 해결된 몇 가지 문제가 발생합니다. .NET Framework 4.6.1용으로 빌드된 이진을 제공하면 여전히 .NET Framework 4.6.1 - 4.7.1을 사용 중인 개발자의 경험을 개선할 수 있습니다.

**✔️ 수행** NuGet 패키지를 사용하여 라이브러리를 배포합니다.

> NuGet은 개발자에게 가장 적합한 대상을 선택하여 적절한 구현을 선택할 필요가 없도록 보호합니다.

**✔️** 멀티 타기팅 시 프로젝트 파일의 `TargetFrameworks` 속성을 사용합니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <!-- This project will output netstandard2.0 and net461 assemblies -->
    <TargetFrameworks>netstandard2.0;net461</TargetFrameworks>
  </PropertyGroup>
</Project>
```

**✔️** UWP 및 Xamarin에 대한 멀티 타기팅 시 [MSBuild.Sdk.Extras](https://github.com/onovotny/MSBuildSdkExtras)를 사용합니다. 그러면 프로젝트 파일이 훨씬 간소화됩니다.

## <a name="older-targets"></a>이전 대상

.NET은 더 이상 일반적으로 사용되지 않는 플랫폼뿐만 아니라 오래전에 지원이 중단된 .NET Framework 버전을 대상으로 지정할 수 있도록 지원합니다. 가능한 한 많은 대상에서 라이브러리가 작동하도록 하는 것은 중요하지만, 누락된 API를 해결하기 위해 상당한 오버헤드가 추가될 수 있습니다. 특정 프레임워크는 도달률 및 제한 사항을 고려할 때 더 이상 대상으로 지정할 가치가 없습니다.

**❌** PCL(이식 가능한 클래스 라이브러리) 대상을 포함하지 않습니다. 예를 들어 `portable-net45+win8+wpa81+wp8`과 같은 형식입니다.

> .NET Standard는 플랫폼 간 .NET 라이브러리를 지원하는 최신 방법으로, PCL을 대체합니다.

**❌** 더 이상 지원되지 않는 .NET 플랫폼의 대상을 포함하지 않습니다. 예: `SL4`, `WP`

>[!div class="step-by-step"]
>[이전](get-started.md)
>[다음](strong-naming.md)
