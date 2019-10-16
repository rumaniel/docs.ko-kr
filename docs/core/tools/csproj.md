---
title: .NET Core용 csproj 형식에 대한 추가 사항
description: 기존 및 .NET Core csproj 파일 간의 차이점에 대해 알아보기
ms.date: 04/08/2019
ms.openlocfilehash: 2ec1aaff88754848d844a56b1744beb2efa4cd89
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291240"
---
# <a name="additions-to-the-csproj-format-for-net-core"></a>.NET Core용 csproj 형식에 대한 추가 사항

이 문서는 *project.json*에서 *csproj* 및 [MSBuild](https://github.com/Microsoft/MSBuild)로 프로젝트 시스템을 전환함에 따라 프로젝트 파일에 추가된 변경 내용을 간략하게 설명합니다. 일반 프로젝트 파일 구문 및 참조에 대한 자세한 내용은 [MSBuild 프로젝트 파일](/visualstudio/msbuild/msbuild-project-file-schema-reference) 설명서를 참조하세요.

## <a name="implicit-package-references"></a>암시적 패키지 참조

메타패키지는 프로젝트 파일의 `<TargetFramework>` 또는 `<TargetFrameworks>` 속성에 지정된 대상 프레임워크를 기준으로 암시적으로 참조됩니다. `<TargetFramework>`가 지정된 경우 `<TargetFrameworks>`는 순서와 관계없이 무시됩니다. 자세한 내용은 [패키지, 메타패키지 및 프레임워크](../packages.md)를 참조하세요. 

```xml
 <PropertyGroup>
   <TargetFramework>netcoreapp2.1</TargetFramework>
 </PropertyGroup>
 ```

 ```xml
 <PropertyGroup>
   <TargetFrameworks>netcoreapp2.1;net462</TargetFrameworks>
 </PropertyGroup>
 ```

### <a name="recommendations"></a>권장 사항

`Microsoft.NETCore.App` 또는 `NETStandard.Library` 메타패키지가 암시적으로 참조되기 때문에 권장되는 모범 사례는 다음과 같습니다.

* .NET Core 또는 .NET Standard를 대상으로 하는 경우 절대로 프로젝트 파일의 `<PackageReference>` 항목을 통해 `Microsoft.NETCore.App` 또는 `NETStandard.Library` 메타패키지를 명시적으로 참조하지 않습니다.
* .NET Core를 대상으로 할 때 특정 버전의 런타임이 필요한 경우 메타패키지를 참조하는 대신 프로젝트의 `<RuntimeFrameworkVersion>` 속성(예: `1.0.4`)을 사용해야 합니다.
  * 예를 들어 [자체 포함 배포](../deploying/index.md#self-contained-deployments-scd)를 사용하고, 1.0.0 LTS 런타임이라는 특정 패치 버전이 필요한 경우 이런 일이 발생할 수 있습니다.
* .NET Standard를 대상으로 할 때 특정 버전의 `NETStandard.Library` 메타패키지가 필요한 경우 `<NetStandardImplicitPackageVersion>` 속성을 사용하고 필요한 버전을 설정할 수 있습니다.
* .NET Framework 프로젝트의 `Microsoft.NETCore.App` 또는 `NETStandard.Library` 메타패키지에 참조를 명시적으로 추가하거나 업데이트하지 마십시오. .NET Standard 기반 NuGet 패키지를 사용할 때 모든 버전의 `NETStandard.Library`가 필요한 경우 NuGet은 자동으로 해당 버전을 설치합니다.

## <a name="implicit-version-for-some-package-references"></a>일부 패키지 참조의 암시적 버전

대부분 [`<PackageReference>`](#packagereference)를 사용하려면 `Version` 특성을 설정하여 사용할 NuGet 패키지 버전을 지정해야 합니다. 그러나 .NET Core 2.1 또는 2.2를 사용하고 [Microsoft.AspNetCore.App](/aspnet/core/fundamentals/metapackage-app) 또는 [Microsoft.AspNetCore.All](/aspnet/core/fundamentals/metapackage)을 참조하는 경우에는 해당 특성이 필요하지 않습니다. .NET Core SDK는 사용해야 하는 패키지의 버전을 자동으로 선택할 수 있습니다.

### <a name="recommendation"></a>권장

`Microsoft.AspNetCore.App` 또는 `Microsoft.AspNetCore.All` 패키지를 참조하는 경우에는 해당 버전을 지정하지 마세요. 버전을 지정하면 SDK에서 경고 NETSDK1071이 생성될 수 있습니다. 이 경고를 해결하려면 다음 예제와 같이 패키지 버전을 제거합니다.

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore.App" />
</ItemGroup>
```

> 알려진 문제: .NET Core 2.1 SDK는 프로젝트에서 Microsoft.NET.Sdk.Web을 사용하는 경우에만 이 구문을 지원했습니다. 이 문제는 .NET Core 2.2 SDK에서 해결되었습니다.

ASP.NET Core 메타패키지에 대한 이 참조의 동작은 대부분의 일반 NuGet 패키지와 약간 다릅니다. 이 메타패키지를 사용하는 애플리케이션의 [프레임워크 종속 배포](../deploying/index.md#framework-dependent-deployments-fdd)에서는 자동으로 ASP.NET Core 공유 프레임워크를 활용합니다. 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 애플리케이션을 사용하여 배포되지 **않습니다**. 이 자산은 ASP.NET Core 공유 프레임워크에 포함됩니다. 공유 프레임워크의 자산은 애플리케이션 시작 시간을 개선하기 위해 대상 플랫폼에 최적화됩니다. 공유 프레임워크에 대한 자세한 내용은 [.NET Core 배포 패키징](../build/distribution-packaging.md)을 참조하세요.

버전이 지정되면 프레임워크 종속 배포의 경우 ASP.NET Core 공유 프레임워크의 최소 버전으로 처리되고, 자체 포함 배포의 경우 정확한 버전으로 처리됩니다.    다음과 같은 결과가 나타날 수 있습니다.

* 서버에 설치된 ASP.NET Core 버전이 PackageReference에 지정된 버전보다 낮으면 .NET Core 프로세스가 시작되지 않습니다. Azure와 같은 호스팅 환경에서 업데이트를 제공되기 전에 일반적으로 NuGet.org에서 메타패키지 업데이트를 사용할 수 있습니다. ASP.NET Core에 대한 PackageReference에서 버전을 업데이트하면 배포된 애플리케이션이 실패할 수 있습니다.
* 애플리케이션이 [자체 포함 배포](../deploying/index.md#self-contained-deployments-scd)로 배포되면 애플리케이션에는 .NET Core에 대한 최신 보안 업데이트가 포함되지 않을 수 있습니다. 버전이 지정되지 않으면 SDK는 자체 포함 배포에 최신 버전의 ASP.NET Core를 자동으로 포함할 수 있습니다.

## <a name="default-compilation-includes-in-net-core-projects"></a>.NET Core 프로젝트의 기본 컴파일 포함 사항

최신 SDK 버전의 *csproj* 형식으로 전환하면서 컴파일 항목에 대한 기본 포함 사항과 제외 사항 및 포함 리소스를 SDK 속성 파일로 이동했습니다. 따라서 더 이상 프로젝트 파일에서 컴파일 항목을 지정할 필요가 없습니다.

이렇게 하는 주된 이유는 프로젝트 파일에서 혼란을 줄이기 위해서입니다. SDK의 기본값은 가장 일반적인 사용 사례를 다루므로 개발자가 만드는 모든 프로젝트에서 반복할 필요가 없습니다. 결과적으로 프로젝트 파일 수가 줄어 훨씬 쉽게 이해하고 편집(필요한 경우)할 수 있습니다.

다음 표에는 SDK에 모두 포함되거나 제외되는 요소 및 [GLOB](https://en.wikipedia.org/wiki/Glob_(programming))가 나와 있습니다.

| 요소           | GLOB 포함                              | GLOB 제외                                                  | GLOB 제거              |
|-------------------|-------------------------------------------|---------------------------------------------------------------|----------------------------|
| Compile           | \*\*/\*.cs(또는 기타 언어 확장) | \*\*/\*.user;  \*\*/\*.\*proj;  \*\*/\*.sln;  \*\*/\*.vssscc  | 해당 사항 없음                      |
| EmbeddedResource  | \*\*/\*.resx                              | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | 해당 사항 없음                      |
| 없음              | \*\*/\*                                   | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | \*\*/\*.cs; \*\*/\*.resx   |

> [!NOTE]
> **GLOB 제외**는 각각 `$(BaseOutputPath)` 및 `$(BaseIntermediateOutputPath)` MSBuild 속성으로 나타내는 `./bin` 및 `./obj` 폴더를 제외합니다. 전체적으로 모든 제외는 `$(DefaultItemExcludes)`로 나타냅니다.

프로젝트에 GLOB가 있고 최신 SDK를 사용하여 빌드하려는 경우 다음 오류가 발생합니다.

> 중복된 컴파일 항목이 포함되었습니다. .NET SDK에는 기본적으로 프로젝트 디렉터리의 컴파일 항목이 포함됩니다. 프로젝트 파일에서 이러한 항목을 제거하거나, 프로젝트 파일에서 이러한 항목을 명시적으로 포함하려면 'EnableDefaultCompileItems' 속성을 'false'로 설정할 수 있습니다.

이 오류를 해결하려면 이전 표에 나열된 항목과 일치하는 명시적인 `Compile` 항목을 제거하거나 다음과 같이 `<EnableDefaultCompileItems>` 속성을 `false`로 설정할 수 있습니다.

```xml
<PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```

이 속성을 `false`로 설정하면 암시적인 포함이 사용되지 않도록 설정되고, 프로젝트에서 기본 GLOB를 지정해야 했던 이전 SDK로 동작이 되돌아갑니다.

이러한 변경으로 인해 다른 포함 항목의 기본 메커니즘이 수정되지 않습니다. 그러나 예를 들어 일부 파일을 지정하여 앱에 게시하려는 경우 해당 사항에 대해 *csproj*의 알려진 메커니즘을 계속 사용할 수 있습니다(예: `<Content>` 요소).

`<EnableDefaultCompileItems>`는 `Compile` glob를 비활성화하지만 암시적 `None` glob와 같은 다른 glob에 영향을 주지 않습니다. \*.cs 항목에도 적용됩니다. 따라서 **솔루션 탐색기**는 `None` 항목으로 포함된 프로젝트의 일부로 \*.cs 항목을 계속해서 표시합니다. 이와 비슷한 방식으로 `<EnableDefaultNoneItems>`를 false로 설정하여 다음과 같이 암시적 `None` glob를 비활성화할 수 있습니다.

```xml
<PropertyGroup>
    <EnableDefaultNoneItems>false</EnableDefaultNoneItems>
</PropertyGroup>
```

**모든 암시적 glob**를 비활성화하기 위해 다음 예제와 같이 `<EnableDefaultItems>` 속성을 `false`로 설정할 수 있습니다.

```xml
<PropertyGroup>
    <EnableDefaultItems>false</EnableDefaultItems>
</PropertyGroup>
```

## <a name="how-to-see-the-whole-project-as-msbuild-sees-it"></a>MSBuild에서 보는 것처럼 전체 프로젝트를 보는 방법

해당 csproj 변경 내용은 프로젝트 파일을 크게 간소화하지만 SDK 및 해당 대상이 포함된 후 MSBuild에서 보는 것처럼 완전히 확장된 프로젝트를 확인해야 할 수 있습니다. 가져온 파일, 해당 소스 및 실제로 프로젝트를 빌드하지 않는 빌드에 대한 기여를 보여 주는 [`dotnet msbuild`](dotnet-msbuild.md) 명령의 [`/pp` 스위치](/visualstudio/msbuild/msbuild-command-line-reference#preprocess)를 사용하여 프로젝트를 전처리합니다.

`dotnet msbuild -pp:fullproject.xml`

프로젝트에 대상 프레임워크가 여러 개 있는 경우 명령의 결과는 대상을 MSBuild 속성으로 지정하여 대상 프레임워크 중 하나에만 초점을 맞춰야 합니다.

`dotnet msbuild -p:TargetFramework=netcoreapp2.0 -pp:fullproject.xml`

## <a name="additions"></a>추가

### <a name="sdk-attribute"></a>SDK 특성

*.csproj* 파일의 루트 `<Project>` 요소에 `Sdk`라고 하는 새 특성이 있습니다. `Sdk`는 프로젝트에서 사용될 SDK를 지정합니다. [레이어 문서](cli-msbuild-architecture.md)에 설명된 것처럼 SDK는 .NET Core 코드를 빌드할 수 있는 MSBuild [작업](/visualstudio/msbuild/msbuild-tasks) 및 [대상](/visualstudio/msbuild/msbuild-targets)의 집합입니다. .NET Core에 사용할 수 있는 SDK는 다음과 같습니다.

1. `Microsoft.NET.Sdk`의 ID와 함께 .NET Core SDK
2. `Microsoft.NET.Sdk.Web`의 ID와 함께 .NET Core 웹 SDK
3. `Microsoft.NET.Sdk.Razor`의 ID와 함께 .NET Core Razor 클래스 라이브러리 SDK
4. ID가 `Microsoft.NET.Sdk.Worker`인 .NET Core 작업자 서비스(.NET Core 3.0 이후)
5. ID가 `Microsoft.NET.Sdk.WindowsDesktop`인 .NET Core WinForms 및 WPF(.NET Core 3.0 이후)

.NET Core 도구를 사용하고 코드를 빌드하려면 `<Project>` 요소의 해당 ID 중 하나에 대한 `Sdk` 특성 집합이 있어야 합니다.

### <a name="packagereference"></a>PackageReference

`<PackageReference>` 항목 요소는 [프로젝트에서 NuGet 종속성](/nuget/consume-packages/package-references-in-project-files)을 지정합니다. `Include` 특성은 패키지 ID를 지정합니다.

```xml
<PackageReference Include="<package-id>" Version="" PrivateAssets="" IncludeAssets="" ExcludeAssets="" />
```

#### <a name="version"></a>버전

필수 `Version` 특성은 복원할 패키지의 버전을 지정합니다. 이 특성은 [NuGet 버전 지정](/nuget/reference/package-versioning#version-ranges-and-wildcards) 체계의 규칙을 따릅니다. 기본 동작은 정확한 버전 일치입니다. 예를 들어 `Version="1.2.3"`을 지정하는 것은 정확한 1.2.3 버전의 패키지에 대한 NuGet 표기법 `[1.2.3]`과 동일합니다.

#### <a name="includeassets-excludeassets-and-privateassets"></a>IncludeAssets, ExcludeAssets 및 PrivateAssets

`IncludeAssets` 특성은 `<PackageReference>`에서 지정한 패키지에 속하여 사용해야 하는 자산을 지정합니다. 기본적으로 모든 패키지 자산이 포함됩니다.

`ExcludeAssets` 특성은 `<PackageReference>`에서 지정한 패키지에 속하여 사용하면 안 되는 자산을 지정합니다.

`PrivateAssets` 특성은 `<PackageReference>`에서 지정한 패키지에 속하여 사용하지만 다음 프로젝트로 전달하지 말아야 하는 자산을 지정합니다. 이 특성이 없으면 `Analyzers`, `Build` 및 `ContentFiles` 자산이 기본적으로 비공개가 됩니다.

> [!NOTE]
> `PrivateAssets`는 *project.json*/*xproj* `SuppressParent` 요소와 같습니다.

이러한 특성은 다음 항목 중 하나 이상을 포함할 수 있습니다. 둘 이상을 포함하는 경우 세미콜론 `;` 문자로 구분합니다.

* `Compile` - lib 폴더의 콘텐츠를 컴파일에 사용할 수 있습니다.
* `Runtime` - 런타임 폴더의 콘텐츠가 분산됩니다.
* `ContentFiles` - *contentfiles* 폴더의 콘텐츠가 사용됩니다.
* `Build` - 빌드 폴더의 속성/대상이 사용됩니다.
* `Native` - 런타임에 네이티브 자산의 콘텐츠가 출력 폴더에 복사됩니다.
* `Analyzers` – 분석기가 사용됩니다.

또는 다음 특성이 포함될 수 있습니다.

* `None` – 자산이 사용되지 않습니다.
* `All` – 모든 자산이 사용됩니다.

### <a name="dotnetclitoolreference"></a>DotNetCliToolReference
`<DotNetCliToolReference>` 항목 요소는 사용자가 프로젝트의 컨텍스트에서 복원할 CLI 도구를 지정합니다. 이 요소는 *project.json*의 `tools` 노드를 대체합니다.

```xml
<DotNetCliToolReference Include="<package-id>" Version="" />
```

#### <a name="version"></a>버전

`Version`은 복원할 패키지 버전을 지정합니다. 이 특성은 [NuGet 버전 지정](/nuget/create-packages/dependency-versions#version-ranges) 체계의 규칙을 따릅니다. 기본 동작은 정확한 버전 일치입니다. 예를 들어 `Version="1.2.3"`을 지정하는 것은 정확한 1.2.3 버전의 패키지에 대한 NuGet 표기법 `[1.2.3]`과 동일합니다.

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers

`<RuntimeIdentifiers>` 속성 요소를 사용하면 프로젝트에 대해 세미콜론으로 구분된 [RID(런타임 식별자)](../rid-catalog.md) 목록을 지정할 수 있습니다.
RID를 통해 자체 포함 배포를 게시할 수 있습니다.

```xml
<RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
```

### <a name="runtimeidentifier"></a>RuntimeIdentifier

`<RuntimeIdentifier>` 속성 요소를 사용하면 프로젝트의 [RID(런타임 식별자)](../rid-catalog.md)를 하나만 지정할 수 있습니다. RID를 통해 자체 포함 배포를 게시할 수 있습니다.

```xml
<RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
```

여러 런타임에 게시해야 하는 경우 `<RuntimeIdentifiers>`(복수)를 대신 사용하세요. 단일 런타임만 필요한 경우에는 `<RuntimeIdentifier>`를 사용하면 빌드 속도가 더 빨라집니다.

### <a name="packagetargetfallback"></a>PackageTargetFallback

`<PackageTargetFallback>` 속성 요소를 사용하면 패키지를 복원할 때 사용할 호환 가능한 대상 집합을 지정할 수 있습니다. 이는 dotnet [TxM(대상 x 모니커)](/nuget/schema/target-frameworks)을 사용하는 패키지가 dotnet TxM을 선언하지 않은 패키지와 작동하도록 허용합니다. 프로젝트에서 dotnet TxM을 사용하는 경우 프로젝트에 `<PackageTargetFallback>`을 추가하여 dotnet이 아닌 플랫폼이 dotnet과 호환되도록 허용하지 않는 이상, 프로젝트에 사용하는 모든 패키지에도 dotnet TxM이 있어야 합니다.

다음 예제에서는 프로젝트의 모든 대상에 대한 대체를 제공합니다.

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

다음 예제에서는 `netcoreapp2.1` 대상에 대해서만 대체를 지정합니다.

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netcoreapp2.1'">
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

## <a name="nuget-metadata-properties"></a>NuGet 메타데이터 속성

MSBuild로 전환하면서 NuGet 패키지를 압축할 때 사용되는 입력 메타데이터를 *project.json*에서 *.csproj* 파일로 전환했습니다. 이 입력은 MSBuild 속성이므로 `<PropertyGroup>` 그룹 내에서 이동해야 합니다. 다음은 `dotnet pack` 명령 또는 SDK의 일부인 `Pack` MSBuild 대상을 사용할 때 압축 프로세스의 입력으로 사용되는 속성 목록입니다.

### <a name="ispackable"></a>IsPackable

프로젝트를 압축할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.

### <a name="packageversion"></a>PackageVersion

결과 패키지의 버전을 지정합니다. 모든 형식의 NuGet 버전 문자열을 수락합니다. 기본값은 `$(Version)`의 값입니다. 즉 프로젝트에서 `Version` 속성의 값입니다.

### <a name="packageid"></a>PackageId

결과 패키지의 이름을 지정합니다. 지정하지 않으면 `pack` 작업에서 기본값으로 `AssemblyName`을 사용하거나 패키지 이름으로 디렉터리 이름을 사용합니다.

### <a name="title"></a>제목

사람들에게 친숙한 패키지 제목이며 보통 nuget.org 및 Visual Studio의 패키지 관리자에서 UI 표시에 사용됩니다. 지정하지 않으면 패키지 ID가 대신 사용됩니다.

### <a name="authors"></a>만든 이

nuget.org에서 프로필 이름과 일치하는, 세미콜론으로 구분된 패키지 작성자 목록입니다. 이러한 목록은 nuget.org의 NuGet 갤러리에 표시되고 동일한 작성자가 패키지를 상호 참조하는 데 사용됩니다.

### <a name="packagedescription"></a>PackageDescription

UI 표시를 위한 패키지에 대한 자세한 설명입니다.

### <a name="description"></a>설명

어셈블리에 대한 자세한 설명입니다. `PackageDescription`을 지정하지 않으면 이 속성이 패키지 설명으로도 사용됩니다.

### <a name="copyright"></a>Copyright

패키지에 대한 저작권 정보입니다.

### <a name="packagerequirelicenseacceptance"></a>PackageRequireLicenseAcceptance

클라이언트에서, 소비자가 패키지를 설치하기 전에 패키지 라이선스에 동의하도록 물어야 할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.

### <a name="packagelicenseexpression"></a>PackageLicenseExpression

[SPDX 라이선스 식별자](https://spdx.org/licenses/) 또는 식입니다. 예: `Apache-2.0`.

[SPDX 라이선스 식별자](https://spdx.org/licenses/)에서 전체 식별자 목록을 확인할 수 있습니다. 라이선스 형식 식을 사용하는 경우, NuGet.org에서는 OSI 또는 FSF 승인된 라이선스만 허용합니다.

아래의 [ABNF](https://tools.ietf.org/html/rfc5234)에서 라이선스 식의 정확한 구문을 설명하고 있습니다.

```abnf
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

> [!NOTE]
> 한 번에 `PackageLicenseExpression`, `PackageLicenseFile` 및 `PackageLicenseUrl` 중 하나만 지정할 수 있습니다.

### <a name="packagelicensefile"></a>PackageLicenseFile

SPDX 식별자가 할당되지 않은 라이선스나 사용자 지정 라이선스를 사용하는 경우, 패키지에 포함된 라이선스 파일의 경로입니다(그 밖에 경우에는 `PackageLicenseExpression`이 선호됨).

`PackageLicenseUrl`을 대체하며, `PackageLicenseExpression`과 함께 사용할 수 없고, Visual Studio 15.9.4, .NET SDK 2.1.502 또는 2.2.101 이상이 필요합니다.

라이선스 파일이 누락되지 않도록 라이선스 파일을 프로젝트에 명시적으로 추가해야 합니다. 사용 예:

```xml
<PropertyGroup>
  <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>
<ItemGroup>
  <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```

### <a name="packagelicenseurl"></a>PackageLicenseUrl

패키지에 적용되는 라이선스에 대한 URL입니다. (Visual Studio 15.9.4, .NET SDK 2.1.502 및 2.2.101 이후부터 사용되지 않습니다.) 

### <a name="packageiconurl"></a>PackageIconUrl

UI 표시에서 패키지에 대한 아이콘으로 사용하는 투명한 배경의 64x64 이미지에 대한 URL입니다.

### <a name="packagereleasenotes"></a>PackageReleaseNotes

패키지에 대한 릴리스 정보입니다.

### <a name="packagetags"></a>PackageTags

패키지를 지정하는 세미콜론으로 구분된 태그 목록입니다.

### <a name="packageoutputpath"></a>PackageOutputPath

압축된 패키지가 삭제되는 출력 경로를 결정합니다. 기본값은 `$(OutputPath)`입니다.

### <a name="includesymbols"></a>IncludeSymbols
이 부울 값은 프로젝트가 압축될 때 패키지에서 추가 기호 패키지를 만들어야 하는지 여부를 나타냅니다. 기호 패키지의 형식은 `SymbolPackageFormat` 속성으로 제어됩니다.

### <a name="symbolpackageformat"></a>SymbolPackageFormat
기호 패키지의 형식을 지정합니다. “symbols.nupkg”인 경우 레거시 기호 패키지가 PDB, DLL 및 기타 출력 파일이 포함된 *.symbols.nupkg* 확장과 함께 생성됩니다. “snupkg”인 경우 snupkg 기호 패키지가 이식 가능한 PDB가 포함되어 생성됩니다. 기본값은 “symbols.nupkg”입니다.

### <a name="includesource"></a>IncludeSource

이 부울 값은 팩 프로세스에서 소스 패키지를 만들어야 하는지 여부를 나타냅니다. 소스 패키지에는 PDB 파일뿐만 아니라 라이브러리의 소스 코드가 포함되어 있습니다. 소스 파일은 결과 패키지 파일의 `src/ProjectName` 디렉터리 아래에 놓입니다.

### <a name="istool"></a>IsTool

모든 출력 파일이 *lib* 폴더 대신 *tools* 폴더에 복사되는지 여부를 지정합니다. 이것은 *.csproj* 파일에서 `PackageType`을 설정하여 지정하는 `DotNetCliTool`과 다릅니다.

### <a name="repositoryurl"></a>RepositoryUrl

패키지에 대한 소스 코드 및/또는 빌드 중인 소스 코드가 있는 리포지토리의 URL을 지정합니다.

### <a name="repositorytype"></a>RepositoryType

리포지토리의 유형을 지정합니다. 기본값은 "git"입니다.

### <a name="repositorybranch"></a>RepositoryBranch
리포지토리의 소스 분기 이름을 지정합니다. 프로젝트가 NuGet 패키지에 패키지되면 패키지 메타데이터에 추가됩니다.

### <a name="repositorycommit"></a>RepositoryCommit
패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다. `RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다. 프로젝트가 NuGet 패키지에 패키지되면 이 커밋 또는 변경 집합이 패키지 메타데이터에 추가됩니다.

### <a name="nopackageanalysis"></a>NoPackageAnalysis

패키지를 빌드한 후 팩에서 패키지 분석을 실행하지 않아야 함을 지정합니다.

### <a name="minclientversion"></a>MinClientVersion

nuget.exe 및 Visual Studio 패키지 관리자에 의해 적용되는, 이 패키지를 설치할 수 있는 NuGet 클라이언트의 최소 버전을 지정합니다.

### <a name="includebuildoutput"></a>IncludeBuildOutput

이 부울 값은 빌드 출력 어셈블리를 *.nupkg* 파일에 압축해야 할지 여부를 지정합니다.

### <a name="includecontentinpack"></a>IncludeContentInPack

이 부울 값은 `Content` 형식이 있는 항목이 결과 패키지에 자동으로 포함될지 여부를 지정합니다. 기본값은 `true`입니다.

### <a name="buildoutputtargetfolder"></a>BuildOutputTargetFolder

출력 어셈블리를 배치할 폴더를 지정합니다. 출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.

### <a name="contenttargetfolders"></a>ContentTargetFolders

이 속성은 `PackagePath`가 지정되지 않은 경우 모든 콘텐츠 파일의 기본 위치를 지정합니다. 기본값은 "content;contentFiles"입니다.

### <a name="nuspecfile"></a>NuspecFile

압축에 사용되는 *.nuspec* 파일에 대한 상대 또는 절대 경로입니다.

> [!NOTE]
> *.nuspec* 파일이 지정된 경우 패키징 정보에 대해 **단독으로** 사용되며 프로젝트의 모든 정보는 사용되지 않습니다.

### <a name="nuspecbasepath"></a>NuspecBasePath

*.nuspec* 파일에 대한 기본 경로입니다.

### <a name="nuspecproperties"></a>NuspecProperties

key=value 쌍의 세미콜론으로 구분된 목록입니다.

## <a name="assemblyinfo-properties"></a>AssemblyInfo 속성

일반적으로 *AssemblyInfo* 파일에 있는 [어셈블리 특성](../../standard/assembly/set-attributes.md)은 이제 속성에서 자동으로 생성됩니다.

### <a name="properties-per-attribute"></a>특성별 속성

각 특성에는 해당 콘텐츠를 제어하는 속성과 다음 표에 표시된 대로 생성을 사용하지 않도록 설정하는 또 다른 속성이 있습니다.

| 특성                                                      | 속성               | 사용하지 않도록 설정할 속성                             |
|----------------------------------------------------------------|------------------------|-------------------------------------------------|
| <xref:System.Reflection.AssemblyCompanyAttribute>              | `Company`              | `GenerateAssemblyCompanyAttribute`              |
| <xref:System.Reflection.AssemblyConfigurationAttribute>        | `Configuration`        | `GenerateAssemblyConfigurationAttribute`        |
| <xref:System.Reflection.AssemblyCopyrightAttribute>            | `Copyright`            | `GenerateAssemblyCopyrightAttribute`            |
| <xref:System.Reflection.AssemblyDescriptionAttribute>          | `Description`          | `GenerateAssemblyDescriptionAttribute`          |
| <xref:System.Reflection.AssemblyFileVersionAttribute>          | `FileVersion`          | `GenerateAssemblyFileVersionAttribute`          |
| <xref:System.Reflection.AssemblyInformationalVersionAttribute> | `InformationalVersion` | `GenerateAssemblyInformationalVersionAttribute` |
| <xref:System.Reflection.AssemblyProductAttribute>              | `Product`              | `GenerateAssemblyProductAttribute`              |
| <xref:System.Reflection.AssemblyTitleAttribute>                | `AssemblyTitle`        | `GenerateAssemblyTitleAttribute`                |
| <xref:System.Reflection.AssemblyVersionAttribute>              | `AssemblyVersion`      | `GenerateAssemblyVersionAttribute`              |
| <xref:System.Resources.NeutralResourcesLanguageAttribute>      | `NeutralLanguage`      | `GenerateNeutralResourcesLanguageAttribute`     |

메모:

* `AssemblyVersion` 및 `FileVersion` 기본값은 접미사 없이 `$(Version)` 값을 사용하는 것입니다. 예를 들어 `$(Version)`가 `1.2.3-beta.4`인 경우 값은 `1.2.3`입니다.
* `InformationalVersion`은 기본적으로 `$(Version)` 값으로 설정됩니다.
* 속성이 있는 경우 `InformationalVersion`에 `$(SourceRevisionId)`가 추가됩니다. `IncludeSourceRevisionInInformationalVersion`을 사용하여 사용하지 않도록 설정할 수 있습니다.
* `Copyright` 및 `Description` 속성도 NuGet 메타데이터에 사용됩니다.
* `Configuration`은 모든 빌드 프로세스와 공유되고 `dotnet` 명령의 `--configuration` 매개 변수를 통해 설정됩니다.

### <a name="generateassemblyinfo"></a>GenerateAssemblyInfo

모든 AssemblyInfo 생성을 사용하거나 사용하지 않도록 설정하는 부울입니다. 기본값은 `true`입니다.

### <a name="generatedassemblyinfofile"></a>GeneratedAssemblyInfoFile

생성된 어셈블리 정보 파일의 경로입니다. 기본적으로 `$(IntermediateOutputPath)`(obj) 디렉터리의 파일로 설정합니다.
