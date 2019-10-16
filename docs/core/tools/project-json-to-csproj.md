---
title: project.json 및 csproj 비교
description: project.json 및 csproj e요소 간 매핑을 참조하세요.
author: natemcmaster
ms.date: 03/13/2017
ms.custom: seodec18
ms.openlocfilehash: 6ac63f18bd42193e964aaeae3c54c887c9c63163
ms.sourcegitcommit: 8f95d3a37e591963ebbb9af6e90686fd5f3b8707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56747413"
---
# <a name="a-mapping-between-projectjson-and-csproj-properties"></a>project.json 및 csproj 속성 간 매핑

[Nate McMaster](https://github.com/natemcmaster)

.NET Core 도구 개발 중 중요한 디자인 변경으로 인해 *project.json* 파일이 더 이상 지원되지 않으며 대신 .NET Core 프로젝트를 MSBuild/csproj 형식으로 전환합니다.

이 문서에서는 프로젝트를 최신 버전의 도구로 업그레이드할 때, 새 형식을 사용하는 방법을 배우고 마이그레이션 도구에서 수행한 변경 내용을 이해할 수 있도록 *project.json*의 설정이 MSBuild/csproj 형식으로 표시되는 방법을 보여 줍니다.

## <a name="the-csproj-format"></a>csproj 형식

새 형식인 \*.csproj는 XML 기반 형식입니다. 다음 예제에서는 `Microsoft.NET.Sdk`를 사용하는 .NET Core 프로젝트의 루트 노드를 보여 줍니다. 웹 프로젝트의 경우 사용되는 SDK는 `Microsoft.NET.Sdk.Web`입니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
...
</Project>
```

## <a name="common-top-level-properties"></a>일반적인 최상위 속성

### <a name="name"></a>name

```json
{
  "name": "MyProjectName"
}
```

더 이상 지원되지 않습니다. csproj에서는 보통 디렉터리 이름과 일치하는 프로젝트 파일 이름으로 결정됩니다. 예를 들어 `MyProjectName.csproj`과 같은 형식입니다.

기본적으로 프로젝트 파일 이름은 `<AssemblyName>` 및 `<PackageId>` 속성의 값도 지정합니다.

```xml
<PropertyGroup>
  <AssemblyName>MyProjectName</AssemblyName>
  <PackageId>MyProjectName</PackageId>
</PropertyGroup>
```

`buildOptions\outputName` 속성이 project.json에서 정의된 경우 `<AssemblyName>`에는 `<PackageId>`와 다른 값이 있습니다.
자세한 내용은 [기타 일반적인 빌드 옵션](#other-common-build-options)을 참조하세요.

### <a name="version"></a>버전

```json
{
  "version": "1.0.0-alpha-*"
}
```

`VersionPrefix` 및 `VersionSuffix` 속성을 사용합니다.

```xml
<PropertyGroup>
  <VersionPrefix>1.0.0</VersionPrefix>
  <VersionSuffix>alpha</VersionSuffix>
</PropertyGroup>
```

`Version` 속성을 사용할 수도 있지만, 패키징 중 버전 설정이 재정의될 수 있습니다.

```xml
<PropertyGroup>
  <Version>1.0.0-alpha</Version>
</PropertyGroup>
```

### <a name="other-common-root-level-options"></a>기타 일반적인 루트 수준 옵션

```json
{
  "authors": [ "Anne", "Bob" ],
  "company": "Contoso",
  "language": "en-US",
  "title": "My library",
  "description": "This is my library.\r\nAnd it's really great!",
  "copyright": "Nugetizer 3000",
  "userSecretsId": "xyz123"
}
```

```xml
<PropertyGroup>
  <Authors>Anne;Bob</Authors>
  <Company>Contoso</Company>
  <NeutralLanguage>en-US</NeutralLanguage>
  <AssemblyTitle>My library</AssemblyTitle>
  <Description>This is my library.
And it's really great!</Description>
  <Copyright>Nugetizer 3000</Copyright>
  <UserSecretsId>xyz123</UserSecretsId>
</PropertyGroup>
```

## <a name="frameworks"></a>frameworks

### <a name="one-target-framework"></a>단일 대상 프레임워크

```json
{
  "frameworks": {
    "netcoreapp1.0": {}
  }
}
```

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp1.0</TargetFramework>
</PropertyGroup>
```

### <a name="multiple-target-frameworks"></a>여러 대상 프레임워크

```json
{
  "frameworks": {
    "netcoreapp1.0": {},
    "net451": {}
  }
}
```

`TargetFrameworks` 속성을 사용하여 대상 프레임워크의 목록을 정의합니다. 세미콜론을 사용하여 여러 프레임워크 값을 구분합니다.

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp1.0;net451</TargetFrameworks>
</PropertyGroup>
```

## <a name="dependencies"></a>종속성

> [!IMPORTANT]
> 종속성이 **프로젝트**이고 패키지가 아닌 경우 형식이 다릅니다.
> 자세한 내용은 [종속성 유형](#dependency-type) 섹션을 참조하세요.

### <a name="netstandardlibrary-metapackage"></a>NETStandard.Library metapackage

```json
{
  "dependencies": {
    "NETStandard.Library": "1.6.0"
  }
}
```

```xml
<PropertyGroup>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

### <a name="microsoftnetcoreapp-metapackage"></a>Microsoft.NETCore.App metapackage

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.0"
  }
}
```

```xml
<PropertyGroup>
  <RuntimeFrameworkVersion>1.0.3</RuntimeFrameworkVersion>
</PropertyGroup>
```

마이그레이션된 프로젝트에서 `<RuntimeFrameworkVersion>` 값은 설치한 SDK의 버전에 따라 결정됩니다.

### <a name="top-level-dependencies"></a>최상위 종속성

```json
{
  "dependencies": {
    "Microsoft.AspNetCore": "1.1.0"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore" Version="1.1.0" />
</ItemGroup>
```

### <a name="per-framework-dependencies"></a>프레임워크별 종속성

```json
{
  "framework": {
    "net451": {
      "dependencies": {
        "System.Collections.Immutable": "1.3.1"
      }
    },
    "netstandard1.5": {
      "dependencies": {
        "Newtonsoft.Json": "9.0.1"
      }
    }
  }
}
```

```xml
<ItemGroup Condition="'$(TargetFramework)'=='net451'">
  <PackageReference Include="System.Collections.Immutable" Version="1.3.1" />
</ItemGroup>

<ItemGroup Condition="'$(TargetFramework)'=='netstandard1.5'">
  <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
</ItemGroup>
```

### <a name="imports"></a>가져오기

```json
{
  "dependencies": {
    "YamlDotNet": "4.0.1-pre309"
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dnxcore50",
        "dotnet"
      ]
    }
  }
}
```

```xml
<PropertyGroup>
  <PackageTargetFallback>dnxcore50;dotnet</PackageTargetFallback>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="YamlDotNet" Version="4.0.1-pre309" />
</ItemGroup>
```

### <a name="dependency-type"></a>종속성 유형

#### <a name="type-project"></a>type: project

```json
{
  "dependencies": {
    "MyOtherProject": "1.0.0-*",
    "AnotherProject": {
      "type": "project"
    }
  }
}
```

```xml
<ItemGroup>
  <ProjectReference Include="..\MyOtherProject\MyOtherProject.csproj" />
  <ProjectReference Include="..\AnotherProject\AnotherProject.csproj" />
</ItemGroup>
```

> [!NOTE]
> `dotnet pack --version-suffix $suffix`가 프로젝트 참조의 종속성 버전을 결정하는 방법이 중단됩니다.

#### <a name="type-build"></a>type: build

```json
{
  "dependencies": {
    "Microsoft.EntityFrameworkCore.Design": {
      "version": "1.1.0",
      "type": "build"
    }
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="1.1.0" PrivateAssets="All" />
</ItemGroup>
```

#### <a name="type-platform"></a>type: platform

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": {
      "version": "1.1.0",
      "type": "platform"
    }
  }
}
```

csproj에는 동일한 항목이 없습니다.

## <a name="runtimes"></a>runtimes

```json
{
  "runtimes": {
    "win7-x64": {},
    "osx.10.11-x64": {},
    "ubuntu.16.04-x64": {}
  }
}
```

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win7-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="standalone-apps-self-contained-deployment"></a>독립 실행형 앱(자체 포함 배포)

project.json에서 `runtimes` 섹션 정의는 앱이 빌드 및 게시 중 독립 실행형이었음을 의미합니다.
MSBuild에서 모든 프로젝트는 빌드 중 *이식 가능*하지만 독립 실행형으로 게시할 수 있습니다.

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

자세한 내용은 [SCD(자체 포함 배포)](../deploying/index.md#self-contained-deployments-scd)를 참조하세요.

## <a name="tools"></a>도구

```json
{
  "tools": {
    "Microsoft.EntityFrameworkCore.Tools.DotNet": "1.0.0-*"
  }
}
```

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="1.0.0" />
</ItemGroup>
```

> [!NOTE]
> 도구의 `imports`는 csproj에서 지원되지 않습니다. imports가 필요한 도구는 새 `Microsoft.NET.Sdk`와 작동하지 않습니다.

## <a name="buildoptions"></a>buildOptions

[파일](#files)을 참조하세요.

### <a name="emitentrypoint"></a>emitEntryPoint

```json
{
  "buildOptions": {
    "emitEntryPoint": true
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

`emitEntryPoint`가 `false`인 경우 `OutputType` 값은 기본값인 `Library`로 변환됩니다.

```json
{
  "buildOptions": {
    "emitEntryPoint": false
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Library</OutputType>
  <!-- or, omit altogether. It defaults to 'Library' -->
</PropertyGroup>
```

### <a name="keyfile"></a>keyFile

```json
{
  "buildOptions": {
    "keyFile": "MyKey.snk"
  }
}
```

`keyFile` 요소는 MSBuild의 세 가지 속성으로 확장됩니다.

```xml
<PropertyGroup>
  <AssemblyOriginatorKeyFile>MyKey.snk</AssemblyOriginatorKeyFile>
  <SignAssembly>true</SignAssembly>
  <PublicSign Condition="'$(OS)' != 'Windows_NT'">true</PublicSign>
</PropertyGroup>
```

### <a name="other-common-build-options"></a>기타 일반적인 빌드 옵션

```json
{
  "buildOptions": {
    "warningsAsErrors": true,
    "nowarn": ["CS0168", "CS0219"],
    "xmlDoc": true,
    "preserveCompilationContext": true,
    "outputName": "Different.AssemblyName",
    "debugType": "portable",
    "allowUnsafe": true,
    "define": ["TEST", "OTHERCONDITION"]
  }
}
```

```xml
<PropertyGroup>
  <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
  <NoWarn>$(NoWarn);CS0168;CS0219</NoWarn>
  <GenerateDocumentationFile>true</GenerateDocumentationFile>
  <PreserveCompilationContext>true</PreserveCompilationContext>
  <AssemblyName>Different.AssemblyName</AssemblyName>
  <DebugType>portable</DebugType>
  <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  <DefineConstants>$(DefineConstants);TEST;OTHERCONDITION</DefineConstants>
</PropertyGroup>
```

## <a name="packoptions"></a>packOptions

[파일](#files)을 참조하세요.

### <a name="common-pack-options"></a>일반적인 팩 옵션

```json
{
  "packOptions": {
    "summary": "numl is a machine learning library intended to ease the use of using standard modeling techniques for both prediction and clustering.",
    "tags": ["machine learning", "framework"],
    "releaseNotes": "Version 0.9.12-beta",
    "iconUrl": "http://numl.net/images/ico.png",
    "projectUrl": "http://numl.net",
    "licenseUrl": "https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md",
    "requireLicenseAcceptance": false,
    "repository": {
      "type": "git",
      "url": "https://raw.githubusercontent.com/sethjuarez/numl"
    },
    "owners": ["Seth Juarez"]
  }
}
```

```xml
<PropertyGroup>
  <!-- summary is not migrated from project.json, but you can use the <Description> property for that if needed. -->
  <PackageTags>machine learning;framework</PackageTags>
  <PackageReleaseNotes>Version 0.9.12-beta</PackageReleaseNotes>
  <PackageIconUrl>http://numl.net/images/ico.png</PackageIconUrl>
  <PackageProjectUrl>http://numl.net</PackageProjectUrl>
  <PackageLicenseUrl>https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md</PackageLicenseUrl>
  <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
  <RepositoryType>git</RepositoryType>
  <RepositoryUrl>https://raw.githubusercontent.com/sethjuarez/numl</RepositoryUrl>
  <!-- owners is not supported in MSBuild -->
</PropertyGroup>
```

MSBuild에는 `owners` 요소에 대해 동일한 요소가 없습니다.
`summary`의 경우, `summary` 값이 자동으로 해당 속성에 마이그레이션되지 않은 경우에도 속성이 [ `description` ](#other-common-root-level-options) 요소로 매핑되므로 MSBuild `<Description>` 속성을 사용할 수 있습니다.

## <a name="scripts"></a>스크립트

```json
{
  "scripts": {
    "precompile": "generateCode.cmd",
    "postpublish": [ "obfuscate.cmd", "removeTempFiles.cmd" ]
  }
}
```

MSBuild에서 해당하는 요소는 [targets](/visualstudio/msbuild/msbuild-targets)입니다.

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="generateCode.cmd" />
</Target>

<Target Name="MyPostCompileTarget" AfterTargets="Publish">
  <Exec Command="obfuscate.cmd" />
  <Exec Command="removeTempFiles.cmd" />
</Target>
```

## <a name="runtimeoptions"></a>runtimeOptions

```json
{
  "runtimeOptions": {
    "configProperties": {
      "System.GC.Server": true,
      "System.GC.Concurrent": true,
      "System.GC.RetainVM": true,
      "System.Threading.ThreadPool.MinThreads": 4,
      "System.Threading.ThreadPool.MaxThreads": 25
    }
  }
}
```

"System.GC.Server" 속성을 제외하고, 이 그룹의 모든 설정은 마이그레이션 프로세스 중 루트 개체에 적용된 옵션과 함께 프로젝트 폴더에서 *runtimeconfig.template.json*이라는 파일에 적용됩니다.

```json
{
  "configProperties": {
    "System.GC.Concurrent": true,
    "System.GC.RetainVM": true,
    "System.Threading.ThreadPool.MinThreads": 4,
    "System.Threading.ThreadPool.MaxThreads": 25
  }
}
```

"System.GC.Server" 속성은 csproj 파일로 마이그레이션됩니다.

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

그러나 MSBuild 속성뿐만 아니라 csproj에서 모든 해당 값을 설정할 수 있습니다.

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
  <ConcurrentGarbageCollection>true</ConcurrentGarbageCollection>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
  <ThreadPoolMaxThreads>25</ThreadPoolMaxThreads>
</PropertyGroup>
```

## <a name="shared"></a>공유

```json
{
  "shared": "shared/**/*.cs"
}
```

csproj에서 지원되지 않습니다. 대신 *.nuspec* 파일에 콘텐츠 파일을 포함해야 합니다.
자세한 내용은 [콘텐츠 파일 포함](/nuget/schema/nuspec#including-content-files)을 참조하세요.

## <a name="files"></a>파일

*project.json*에서 빌드 및 팩을 확장하여 컴파일하고 다른 폴더에서 포함할 수 있습니다.
MSBuild에서는 [항목](/visualstudio/msbuild/common-msbuild-project-items)을 사용하여 수행합니다. 다음 예제는 일반적인 변환입니다.

```json
{
  "buildOptions": {
    "compile": {
      "copyToOutput": "notes.txt",
      "include": "../Shared/*.cs",
      "exclude": "../Shared/Not/*.cs"
    },
    "embed": {
      "include": "../Shared/*.resx"
    }
  },
  "packOptions": {
    "include": "Views/",
    "mappings": {
      "some/path/in/project.txt": "in/package.txt"
    }
  },
  "publishOptions": {
    "include": [
      "files/",
      "publishnotes.txt"
    ]
  }
}
```

```xml
<ItemGroup>
  <Compile Include="..\Shared\*.cs" Exclude="..\Shared\Not\*.cs" />
  <EmbeddedResource Include="..\Shared\*.resx" />
  <Content Include="Views\**\*" PackagePath="%(Identity)" />
  <None Include="some/path/in/project.txt" Pack="true" PackagePath="in/package.txt" />
  
  <None Include="notes.txt" CopyToOutputDirectory="Always" />
  <!-- CopyToOutputDirectory = { Always, PreserveNewest, Never } -->

  <Content Include="files\**\*" CopyToPublishDirectory="PreserveNewest" />
  <None Include="publishnotes.txt" CopyToPublishDirectory="Always" />
  <!-- CopyToPublishDirectory = { Always, PreserveNewest, Never } -->
</ItemGroup>
```

> [!NOTE]
> 많은 기본 [와일드카드 사용 패턴](https://en.wikipedia.org/wiki/Glob_(programming))이 .NET Core SDK에 의해 자동으로 추가됩니다.
> 자세한 내용은 [기본 컴파일 항목 값](https://aka.ms/sdkimplicititems)을 참조하세요.

모든 MSBuild `ItemGroup` 요소는 `Include`, `Exclude` 및 `Remove`를 지원합니다.

.nupkg 내의 패키지 레이아웃은 `PackagePath="path"`를 사용하여 수정할 수 있습니다.

`Content`를 제외하고, 대부분의 항목 그룹은 패키지에 포함되도록 `Pack="true"`를 명시적으로 추가해야 합니다. MSBuild `<IncludeContentInPack>` 속성이 기본적으로 `true`로 설정되어 있기 때문에 `Content`는 패키지의 *content* 폴더에 놓입니다.
자세한 내용은 [패키지에 콘텐츠 포함](/nuget/schema/msbuild-targets#including-content-in-a-package)을 참조하세요.

`PackagePath="%(Identity)"`는 패키지 경로를 프로젝트 상대 파일 경로에 설정하는 간단한 방법입니다.

## <a name="testrunner"></a>testRunner

### <a name="xunit"></a>xUnit

```json
{
  "testRunner": "xunit",
  "dependencies": {
    "dotnet-test-xunit": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="xunit" Version="2.2.0-*" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0-*" />
</ItemGroup>
```

### <a name="mstest"></a>MSTest

```json
{
  "testRunner": "mstest",
  "dependencies": {
    "dotnet-test-mstest": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.12-*" />
  <PackageReference Include="MSTest.TestFramework" Version="1.1.11-*" />
</ItemGroup>
```

## <a name="see-also"></a>참고 항목

- [CLI의 변경 내용에 대한 대략적인 개요](../tools/cli-msbuild-architecture.md)
