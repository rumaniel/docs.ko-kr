---
title: .NET Core CLI 확장성 모델
description: CLI(명령줄 인터페이스) 도구를 확장할 수 있는 방법을 알아봅니다.
author: blackdwarf
ms.author: mairaw
ms.date: 04/12/2017
ms.openlocfilehash: 9f54479704f547ada567619a82b24a47a0b104c4
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48842738"
---
# <a name="net-core-cli-tools-extensibility-model"></a>.NET Core CLI 도구 확장성 모델

이 문서에서는 .NET Core CLI(명령줄 인터페이스) 도구를 확장할 수 있는 다양한 방법 및 각 방법을 구동하는 시나리오를 설명합니다.
도구를 사용하는 방법과 여러 유형의 도구를 빌드하는 방법을 알아보겠습니다.

## <a name="how-to-extend-cli-tools"></a>CLI 도구를 확장하는 방법
CLI 도구는 세 가지 주요 방법으로 확장할 수 있습니다.

1. [프로젝트 단위로 NuGet 패키지 사용](#per-project-based-extensibility)

   프로젝트 단위 도구는 프로젝트의 컨텍스트 내에 포함되지만 복원을 통해 간편한 설치를 허용합니다.

2. [사용자 지정 대상을 사용하여 NuGet 패키지 사용](#custom-targets)

   사용자 지정 대상을 사용하면 사용자 지정 작업을 사용하여 빌드 프로세스를 쉽게 확장할 수 있습니다.

3. [시스템의 PATH 사용](#path-based-extensibility)

   PATH 기반 도구는 단일 컴퓨터에서 사용할 수 있는 일반적인 프로젝트 간 도구에 적합합니다.

위에서 간략하게 설명한 세 가지 확장성 메커니즘은 함께 사용할 수 있습니다. 하나 또는 모두 사용하거나 임의로 조합해서 사용할 수 있습니다. 선택하는 방법은 확장을 통해 달성하려는 목표에 따라 크게 달라집니다.

## <a name="per-project-based-extensibility"></a>프로젝트 단위 기반 확장성
프로젝트 단위 도구는 NuGet 패키지로 배포되는 [프레임워크 종속 배포](../deploying/index.md#framework-dependent-deployments-fdd)입니다. 도구는 도구를 참조하는 프로젝트의 컨텍스트에서 복원된 프로젝트에 대해서만 사용할 수 있습니다. 프로젝트의 컨텍스트 외부(예: 프로젝트가 포함된 디렉터리 외부)에서 호출하면 명령을 찾을 수 없기 때문에 실패합니다.

이러한 도구는 빌드 서버에도 완벽한데, 프로젝트 파일 외부의 항목이 필요하지 않기 때문입니다. 빌드 프로세스에서는 빌드하는 프로젝트에 대해 복원을 실행하므로 도구를 사용할 수 있습니다. 각 프로젝트가 하나의 특정 언어로만 작성될 수 있기 때문에 F#과 같은 언어 프로젝트도 이 범주에 속합니다.

마지막으로 이 확장성 모델에서는 프로젝트의 빌드된 출력에 액세스해야 하는 도구를 만들 수 있습니다. 예를 들어 [ASP.NET](https://www.asp.net/) MVC 응용 프로그램의 다양한 Razor 보기 도구는 이 범주에 속합니다.

### <a name="consuming-per-project-tools"></a>프로젝트 단위 도구 사용
이러한 도구를 사용하려면 사용할 각 도구에 대한 `<DotNetCliToolReference>` 요소를 프로젝트 파일에 추가해야 합니다. `<DotNetCliToolReference>` 요소 내에서 도구가 상주하는 패키지를 참조하고 필요한 버전을 지정합니다. [`dotnet restore`](dotnet-restore.md)를 실행하면 도구 및 해당 종속성이 복원됩니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

프로젝트의 빌드 출력을 로드하여 실행해야 하는 도구의 경우 일반적으로 프로젝트 파일의 일반 종속성 아래에 나열되는 다른 종속성이 있습니다. CLI에서는 빌드 엔진으로 MSBuild를 사용하기 때문에 전반적인 빌드 프로세스에 포함될 수 있는 방식으로 이러한 도구 부분을 사용자 지정 MSBuild [대상](/visualstudio/msbuild/msbuild-targets) 및 [작업](/visualstudio/msbuild/msbuild-tasks)으로 작성하는 것이 좋습니다. 또한 출력 파일 위치, 빌드 중인 현재 구성 등 빌드를 통해 생성된 모든 데이터를 쉽게 가져올 수 있습니다. 이 정보는 모두 임의 대상에서 읽을 수 있는 MSBuild 속성 집합이 됩니다. 이 문서의 뒷부분에 있는 NuGet을 사용하여 사용자 지정 대상을 추가하는 방법을 확인할 수 있습니다.

간단한 도구를 추가하는 예제를 검토해 보겠습니다. 간단한 프로젝트에 도구만 추가합니다. 다음은 NuGet 패키지에서 지정된 API를 검색할 수 있는 `dotnet-api-search`라는 예제 명령이 지정된 경우 해당 도구를 사용하는 콘솔 응용 프로그램의 프로젝트 파일입니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <!-- The tools reference -->
  <ItemGroup>
    <DotNetCliToolReference Include="dotnet-api-search" Version="1.0.0" />
  </ItemGroup>
</Project>
```

`<DotNetCliToolReference>` 요소는 `<PackageReference>` 요소와 비슷한 방식으로 구성됩니다. 이 노드에는 도구와 복원할 수 있는 도구 버전을 포함하는 패키지의 패키지 ID가 필요합니다.

### <a name="building-tools"></a>도구 빌드
앞에서 설명한 대로 도구는 단순히 이식 가능한 콘솔 응용 프로그램입니다. 다른 콘솔 응용 프로그램을 빌드함에 따라 도구를 빌드합니다.
도구를 빌드한 후에는 [`dotnet pack`](dotnet-pack.md) 명령을 사용하여 코드, 종속성에 대한 정보 등을 포함하는 NuGet 패키지(.nupkg 파일)를 만듭니다. 패키지 이름을 원하는 대로 지정할 수 있지만 응용 프로그램 내부 실제 도구 이진이 `dotnet-<command>`의 규칙을 준수해야 `dotnet`에서 패키지를 호출할 수 있습니다.

> [!NOTE]
> .NET Core 명령줄 도구의 RC3 이전 버전에서는 `dotnet pack` 명령에 버그가 있어서 `runtime.config.json`이 도구로 압축되지 않았습니다. 해당 파일이 없으면 런타임 시 오류가 발생합니다. 이 문제가 발생하는 경우 최신 도구로 업데이트하고 `dotnet pack`을 다시 시도하세요.

도구는 이식 가능한 응용 프로그램이므로 도구 사용자가 도구를 실행하려면 도구가 빌드된 버전의 .NET Core 라이브러리가 있어야 합니다. 도구에서 사용하고 .NET Core 라이브러리 내에서 포함되지 않은 다른 모든 종속성은 NuGet 캐시에서 복원되고 배치됩니다. 따라서 전체 도구는 .NET Core 라이브러리의 어셈블리뿐만 아니라 NuGet 캐시의 어셈블리를 사용하여 실행됩니다.

이러한 종류의 도구에는 해당 도구를 사용하는 프로젝트의 종속성 그래프와 완전히 구분되는 종속성 그래프가 있습니다. 복원 프로세스에서는 먼저 프로젝트의 종속성을 복원한 다음 각 도구 및 해당 종속성을 복원합니다.

보다 풍부한 예제 및 다양한 조합은 [.NET Core CLI 리포지토리](https://github.com/dotnet/cli/tree/release/2.1/TestAssets/TestProjects)에서 확인할 수 있습니다.
동일한 리포지토리에서 [사용된 도구의 구현](https://github.com/dotnet/cli/tree/release/2.1/TestAssets/TestPackages)도 확인할 수 있습니다.

### <a name="custom-targets"></a>사용자 지정 대상
NuGet에는 [사용자 지정 MSBuild 대상 및 props 파일을 패키지](/nuget/create-packages/creating-a-package#including-msbuild-props-and-targets-in-a-package)하는 기능이 있습니다. .NET Core CLI 도구가 MSBuild를 사용하도록 이동하면서 이제 동일한 확장성 메커니즘이 .NET Core 프로젝트에 적용됩니다. 빌드 프로세스를 확장하거나 빌드 프로세스에서 생성된 파일과 같은 아티팩트에 액세스하거나 빌드 호출 시 구성을 검사하려는 경우 이 유형의 확장성을 사용하게 됩니다.

다음 예제에서는 `csproj` 구문을 사용하여 대상의 프로젝트 파일을 볼 수 있습니다. 이렇게 하면 [`dotnet pack`](dotnet-pack.md) 명령에 대상 파일 및 어셈블리를 패키지 내의 *빌드* 폴더에 배치하여 패키지할 항목이 지정됩니다. `Label` 속성이 `dotnet pack instructions`로 설정된 `<ItemGroup>` 요소 및 그 아래에 정의된 Target을 확인합니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <Description>Sample Packer</Description>
    <VersionPrefix>0.1.0-preview</VersionPrefix>
    <TargetFramework>netstandard1.3</TargetFramework>
    <DebugType>portable</DebugType>
    <AssemblyName>SampleTargets.PackerTarget</AssemblyName>
  </PropertyGroup>
  <ItemGroup>
    <EmbeddedResource Include="Resources\Pkg\dist-template.xml;compiler\resources\**\*" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
    <None Include="build\SampleTargets.PackerTarget.targets" />
  </ItemGroup>
  <ItemGroup Label="dotnet pack instructions">
    <Content Include="build\*.targets">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">
    <!-- Collect these items inside a target that runs after build but before packaging. -->
    <ItemGroup>
      <Content Include="$(OutputPath)\*.dll;$(OutputPath)\*.json">
        <Pack>true</Pack>
        <PackagePath>build\</PackagePath>
      </Content>
    </ItemGroup>
  </Target>
  <ItemGroup>
    <PackageReference Include="Microsoft.Extensions.DependencyModel" Version="1.0.1-beta-000933"/>
    <PackageReference Include="Microsoft.Build.Framework" Version="0.1.0-preview-00028-160627" />
    <PackageReference Include="Microsoft.Build.Utilities.Core" Version="0.1.0-preview-00028-160627" />
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
  </ItemGroup>
  <ItemGroup />
  <PropertyGroup Label="Globals">
    <ProjectGuid>463c66f0-921d-4d34-8bde-7c9d0bffaf7b</ProjectGuid>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(TargetFramework)' == 'netstandard1.3' ">
    <DefineConstants>$(DefineConstants);NETSTANDARD1_3</DefineConstants>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <DefineConstants>$(DefineConstants);RELEASE</DefineConstants>
  </PropertyGroup>
</Project>
```

사용자 지정 대상을 사용하는 작업은 확장되고 있는 프로젝트 내부 버전과 패키지를 가리키는 `<PackageReference>`를 제공함으로써 수행됩니다. 도구와 달리 사용자 지정 대상 패키지는 사용하는 프로젝트의 종속성 종료 항목에 포함됩니다.

사용자 지정 대상을 사용하는 작업은 구성하는 방법에 따라 전적으로 달라집니다. MSBuild 대상이므로 지정된 대상에 따라 달라지고 다른 대상 이후에 실행될 수 있으며, `dotnet msbuild -t:<target-name>` 명령을 사용하여 수동으로 호출할 수도 있습니다.

그러나 사용자에게 더 나은 사용자 환경을 제공하려는 경우 프로젝트별 도구 및 사용자 지정 대상을 결합할 수 있습니다. 이 시나리오에서 프로젝트별 도구는 기본적으로 매개 변수가 필요한 항목은 허용하고, 대상을 실행할 필수 [`dotnet msbuild`](dotnet-msbuild.md) 호출로 변환합니다. 이러한 종류의 시너지 효과는 [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer) 프로젝트의 [MVP Summit 2016 Hackathon 샘플](https://github.com/dotnet/MVPSummitHackathon2016) 리포지토리에서 확인할 수 있습니다.

### <a name="path-based-extensibility"></a>PATH 기반 확장성
일반적으로 PATH 기반 확장성은 개념적으로 둘 이상의 프로젝트를 포함하는 도구가 필요한 개발 컴퓨터에 사용됩니다. 이 확장 메커니즘의 주요 단점은 도구가 있는 컴퓨터에 연결된다는 점입니다. 따라서 다른 컴퓨터에서 필요한 경우에는 배포해야 합니다.

CLI 도구 집합 확장성의 이 패턴은 매우 간단합니다. [.NET Core CLI 개요](index.md)에서 설명한 대로 `dotnet` 드라이버는 `dotnet-<command>` 규칙에 따라 명명된 모든 명령을 실행할 수 있습니다. 기본 해결 논리에서는 여러 위치를 먼저 검색하고 마지막으로 시스템 PATH를 검색합니다. 요청한 명령이 시스템 PATH에 있고 호출할 수 있는 이진인 경우 `dotnet` 드라이버에서 호출합니다.

파일은 실행 파일이어야 합니다. Unix 시스템에서는 `chmod +x`를 통해 실행 비트를 설정하는 모든 항목을 의미하고, Windows에서는 *cmd* 파일을 사용할 수 있습니다.

"Hello World" 도구의 매우 간단한 구현을 살펴보겠습니다. Windows에서는 `bash` 및 `cmd`를 둘 다 사용합니다.
다음 명령은 단순히 "Hello World"를 콘솔에 에코합니다.

```bash
#!/bin/bash

echo "Hello World!"
```

```cmd
echo "Hello World"
```

MacOS에서는 이 스크립트를 `dotnet-hello`으로 저장하고 `chmod +x dotnet-hello`을 사용하여 실행 파일 비트를 설정할 수 있습니다. 그런 다음 `ln -s <full_path>/dotnet-hello /usr/local/bin/` 명령을 사용하여 `/usr/local/bin`에 바로 가기 링크를 만들 수 있습니다. 그러면 `dotnet hello` 구문을 사용하여 명령을 호출할 수 있습니다.

Windows에서는 이 스크립트를 `dotnet-hello.cmd`로 저장하고 시스템 경로에 있는 위치에 보관하거나 경로에 이미 있는 폴더에 추가할 수 있습니다. 그런 다음 `dotnet hello`를 사용하여 이 예제를 실행할 수 있습니다.
