---
title: .NET Core로 코드를 포팅하기 위해 종속성 분석
description: .NET Framework에서 .NET Core로 프로젝트를 포팅하기 위해 외부 종속성을 분석하는 방법을 알아봅니다.
author: cartermp
ms.date: 12/07/2018
ms.custom: seodec18
ms.openlocfilehash: 6c0f55150a4a1c4d0fb8b3125565c9ab8ade3117
ms.sourcegitcommit: c6f69b0cf149f6b54483a6d5c2ece222913f43ce
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55904329"
---
# <a name="analyze-your-dependencies-to-port-code-to-net-core"></a>.NET Core로 코드를 포팅하기 위해 종속성 분석

코드를 .NET Core 또는 .NET Standard로 포팅하려면 종속성을 파악해야 합니다. 외부 종속성은 프로젝트에서 참조하지만 빌드하지 않는 [NuGet 패키지](#analyze-referenced-nuget-packages-in-your-projects) 또는 [DLL](#analyze-dependencies-that-arent-nuget-packages)입니다. 각 종속성을 평가하고 .NET Core와 호환되지 않는 종속성에 대한 대체 계획을 개발합니다. 종속성이 .NET Core와 호환되는지 확인하는 방법은 다음과 같습니다.

## <a name="analyze-referenced-nuget-packages-in-your-projects"></a>프로젝트에서 참조된 NuGet 패키지 분석

프로젝트에서 NuGet 패키지를 참조하는 경우 .NET Core와 호환되는지 확인해야 합니다.
여기에는 두 가지 방법이 있습니다.

* [NuGet 패키지 탐색기 앱 사용](#analyze-nuget-packages-using-nuget-package-explorer)
* [nuget.org 사이트 사용](#analyze-nuget-packages-using-nugetorg)

패키지를 분석한 후 .NET Core 및 대상 .NET Framework와 호환되지 않는 경우 [.NET Framework 호환 모드](#net-framework-compatibility-mode)가 이식 프로세스에 도움이 될 수 있는지 확인할 수 있습니다.

### <a name="analyze-nuget-packages-using-nuget-package-explorer"></a>NuGet 패키지 탐색기를 사용하여 NuGet 패키지 분석

NuGet 패키지 자체는 플랫폼 관련 어셈블리를 포함하는 폴더 집합입니다. 따라서 패키지 내에 호환되는 어셈블리를 포함하는 폴더인지 확인해야 합니다.

NuGet 패키지 폴더를 검사하는 가장 쉬운 방법은 [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) 도구를 사용하는 것입니다. 설치한 후 다음 단계를 사용하여 폴더 이름을 표시합니다.

1. NuGet 패키지 탐색기를 엽니다.
2. **온라인 피드에서 패키지 열기**를 클릭합니다.
3. 패키지의 이름을 검색합니다.
4. 검색 결과에서 패키지 이름을 선택하고 **열기**를 클릭합니다.
5. 오른쪽에서 *lib* 폴더를 확장하고 폴더 이름을 찾습니다.

다음 이름 중 하나를 사용하여 폴더를 찾습니다.

```
netstandard1.0
netstandard1.1
netstandard1.2
netstandard1.3
netstandard1.4
netstandard1.5
netstandard1.6
netstandard2.0
netcoreapp1.0
netcoreapp1.1
netcoreapp2.0
netcoreapp2.1
netcoreapp2.2
portable-net45-win8
portable-win8-wpa8
portable-net451-win81
portable-net45-win8-wpa8-wpa81
```

이러한 값은 [.NET Standard](../../standard/net-standard.md), .NET Core의 버전에 매핑되는 [TFM(대상 프레임워크 모니커)](../../standard/frameworks.md) 및 .NET Core와 호환되는 기존의 PCL(이식 가능한 클래스 라이브러리) 프로필입니다.

> [!IMPORTANT]
> 패키지에서 지원하는 TFM을 살펴볼 때 호환되는 동안 `netcoreapp*`은 .NET Standard 프로젝트용이 아닌 .NET Core 프로젝트용입니다.
> `netstandard*`가 아닌 `netcoreapp*`만을 대상으로 하는 라이브러리는 다른 .NET Core 앱에서만 사용할 수 있습니다.

### <a name="analyze-nuget-packages-using-nugetorg"></a>nuget.org를 사용하여 NuGet 패키지 분석

또는 패키지 페이지의 **종속성** 섹션 아래의 [nuget.org](https://www.nuget.org/)에서 패키지가 지원하는 TFM을 확인할 수 있습니다.

사이트를 사용하는 것이 호환성을 확인하는 쉬운 방법이지만 **종속성** 정보를 모든 패키지에 대한 사이트에서 사용할 수 없습니다.

### <a name="net-framework-compatibility-mode"></a>.NET Framework 호환 모드

NuGet 패키지를 분석한 후 대부분의 NuGet 패키지와 마찬가지로 .NET Framework만 대상으로 하는 것을 확인할 수 있습니다.

.NET Standard 2.0부터 .NET Framework 호환성 모드가 도입되었습니다. 이 호환 모드에서는 .NET Standard 및 .NET Core 프로젝트에서 .NET Framework 라이브러리를 참조할 수 있습니다. .NET Framework 라이브러리 참조는 라이브러리가 WPF(Windows Presentation Foundation) API를 사용하는 것처럼 모든 프로젝트에 대해 작동하지 않지만 많은 이식 시나리오를 차단 해제합니다.

프로젝트에서 .NET Framework를 대상으로 하는 NuGet 패키지를 참조하는 경우(예:[Huitian.PowerCollections](https://www.nuget.org/packages/Huitian.PowerCollections)) 다음 예제와 유사한 패키지 대체 경고([NU1701](/nuget/reference/errors-and-warnings/nu1701))를 받습니다.

`NU1701: Package ‘Huitian.PowerCollections 1.0.0’ was restored using ‘.NETFramework,Version=v4.6.1’ instead of the project target framework ‘.NETStandard,Version=v2.0’. This package may not be fully compatible with your project.`

해당 경고는 패키지를 추가하고 해당 패키지를 프로젝트와 테스트하도록 빌드할 때마다 표시됩니다. 프로젝트가 예상대로 작동하는 경우 Visual Studio에서 패키지 속성을 편집하거나 즐겨 찾는 코드 편집기에서 프로젝트 파일을 수동으로 편집하여 해당 경고를 제거할 수 있습니다.

프로젝트 파일을 편집하여 경고를 제거하려면 경고를 제거하려는 패키지에 대한 `PackageReference` 항목을 찾고 `NoWarn` 특성을 추가합니다. `NoWarn` 특성은 모든 경고 ID의 쉼표로 구분된 목록을 허용합니다. 다음 예제는 프로젝트 파일을 수동으로 편집하여 `Huitian.PowerCollections` 프로젝트에 대한 `NU1701` 경고를 제거하는 방법을 보여 줍니다.

```xml
<ItemGroup>
  <PackageReference Include="Huitian.PowerCollections" Version="1.0.0" NoWarn="NU1701" />
</ItemGroup>
```

Visual Studio에서 컴파일러 경고를 제거하는 방법에 대한 자세한 내용은 [NuGet 패키지에 대한 경고 표시 안 함](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages)을 참조하세요.

## <a name="port-your-packages-to-packagereference"></a>`PackageReference`로 패키지 포팅

.NET Core는 [PackageReference](/nuget/consume-packages/package-references-in-project-files)를 사용하여 패키지 종속성을 지정합니다. [packages.config](/nuget/reference/packages-config)를 사용하여 패키지를 지정하는 경우 `PackageReference`로 변환해야 합니다.

[packages.config에서 PackageReference로 마이그레이션](/nuget/reference/migrate-packages-config-to-package-reference)에서 자세히 알아볼 수 있습니다.

## <a name="what-to-do-when-your-nuget-package-dependency-doesnt-run-on-net-core"></a>NuGet 패키지 종속성이 .NET Core에서 실행되지 않는 경우 수행할 작업

종속된 NuGet 패키지가 .NET Core에서 실행되지 않을 경우 수행할 수 있는 몇 가지가 있습니다.

1. 프로젝트가 오픈 소스이고 GitHub 같은 곳에 호스트된 경우 개발자가 직접 참여하도록 할 수 있습니다.
2. [nuget.org](https://www.nuget.org/)에서 작성자에게 직접 문의할 수 있습니다. 패키지를 검색하고 패키지 페이지의 왼쪽에서 **연락처 소유자**를 클릭합니다.
3. 사용하던 패키지와 동일한 작업을 수행하는 .NET Core에서 실행되는 다른 패키지를 찾을 수도 있습니다.
4. 패키지가 수행하고 있는 코드를 직접 작성해볼 수 있습니다.
5. 적어도 패키지의 호환 버전을 사용할 수 있을 때까지는 앱의 기능을 변경하여 패키지에 대한 종속성을 없앨 수 있습니다.

오픈 소스 프로젝트 유지 관리자와 NuGet 패키지 게시자는 종종 지원자입니다. 지정된 도메인을 중요하게 여기기 때문에 참여하고, 자유롭게 수행하고, 종종 다른 주간 작업을 갖습니다. 따라서 .NET Core 지원에 대해 문의하는 경우 주의해야 합니다.

위 방법으로 문제를 해결할 수 없는 경우 나중에 .NET Core로 이식해야 할 수 있습니다.

.NET 팀은 .NET Core를 지원하기 위해 어떤 라이브러리가 가장 중요한지 알고자 합니다. 사용하고 싶은 라이브러리에 대해 dotnet@microsoft.com으로 메일을 보낼 수 있습니다.

## <a name="analyze-dependencies-that-arent-nuget-packages"></a>NuGet 패키지가 아닌 종속성 분석

파일 시스템의 DLL처럼, NuGet 패키지가 아닌 종속성이 있을 수 있습니다. 해당 종속성의 이식 가능성을 확인하는 유일한 방법은 [.NET 이식성 분석기](https://github.com/Microsoft/dotnet-apiport)를 실행하는 것입니다. 도구는 .NET Framework를 대상으로 하는 어셈블리를 분석하고 .NET Core와 같은 다른 .NET 플랫폼으로 이식할 수 없는 API를 식별할 수 있습니다. 콘솔 애플리케이션 또는 [Visual Studio 확장](../../standard/analyzers/portability-analyzer.md)으로 도구를 실행할 수 있습니다.

>[!div class="step-by-step"]
>[다음](libraries.md)
