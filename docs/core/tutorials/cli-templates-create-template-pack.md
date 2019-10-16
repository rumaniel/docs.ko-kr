---
title: dotnet new에 대한 템플릿 팩 만들기
description: dotnet new 명령에 대한 템플릿 팩을 빌드하는 csproj 파일을 만드는 방법을 알아봅니다.
author: thraka
ms.date: 06/25/2019
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 520af5022e061236c0cfe80379679d9c7b5896b2
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117403"
---
# <a name="tutorial-create-a-template-pack"></a>자습서: 템플릿 팩 만들기

.NET Core를 사용하여 프로젝트, 파일, 리소스를 생성하는 템플릿을 만들고 배포할 수 있습니다. 이 자습서는 `dotnet new` 명령에 사용할 템플릿을 만들고, 설치하고, 제거하는 방법을 알려주는 시리즈의 3부입니다.

시리즈의 3부에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
>
> * \*.csproj 프로젝트를 만들어 템플릿 팩 빌드
> * 압축을 위해 프로젝트 파일 구성
> * NuGet 패키지 파일에서 템플릿 설치
> * 패키지 ID로 템플릿 제거

## <a name="prerequisites"></a>전제 조건

* 이 자습서 시리즈의 [1부](cli-templates-create-item-template.md) 및 [2부](cli-templates-create-project-template.md)를 완료합니다.

  이 자습서에서는 이 자습서의 처음 두 부분에서 만든 두 템플릿을 사용합니다. _working\templates\\_ 폴더에 템플릿을 폴더로 복사하여 다른 템플릿을 사용할 수 있습니다.

* 터미널을 열고 _working\templates\\_ 폴더로 이동합니다.

## <a name="create-a-template-pack-project"></a>템플릿 팩 프로젝트 만들기

템플릿 팩은 파일로 패키지된 하나 이상의 템플릿입니다. 팩을 설치하거나 제거하면 각각 팩에 포함된 모든 템플릿이 추가되거나 제거됩니다. 이 자습서 시리즈의 이전 부분에서는 개별 템플릿 작업만 수행했습니다. 압축되지 않은 템플릿을 공유하려면 템플릿 폴더를 복사하고 해당 폴더를 통해 설치해야 합니다. 템플릿 팩은 둘 이상의 템플릿을 포함할 수 있고 단일 파일이므로 쉽게 공유할 수 있습니다.

템플릿 팩은 NuGet 패키지( _.nupkg_) 파일로 표시됩니다. NuGet 패키지와 마찬가지로 템플릿 팩을 NuGet 피드에 업로드할 수 있습니다. `dotnet new -i` 명령은 NuGet 패키지 피드에서 템플릿 팩 설치를 지원합니다. _.nupkg_ 파일에서 직접 템플릿 팩을 설치할 수도 있습니다.

일반적으로 C# 프로젝트 파일을 사용하여 코드를 컴파일하고 이진을 생성합니다. 프로젝트를 사용하여 템플릿 팩을 생성할 수도 있습니다. _.csproj_의 설정을 변경하여 코드를 컴파일하지 않도록 차단하고 템플릿의 모든 자산을 리소스로 포함할 수 있습니다. 이 프로젝트를 빌드하면 템플릿 팩 NuGet 패키지가 생성됩니다.

만든 팩에는 이전에 만든 [항목 템플릿](cli-templates-create-item-template.md) 및 [패키지 템플릿](cli-templates-create-project-template.md)이 포함됩니다. 두 템플릿을 _working\templates\\_ 폴더로 그룹화했으므로 _.csproj_ 파일에 대해 _working_ 폴더를 사용할 수 있습니다.

터미널에서 _working_ 폴더로 이동합니다. 새 프로젝트를 만들고 이름을 `templatepack`으로 설정하고 출력 폴더를 현재 폴더로 설정합니다.

```dotnetcli
dotnet new console -n templatepack -o .
```

`-n` 매개 변수는 _.csproj_ 파일 이름을 _templatepack.csproj_로 설정하고 `-o` 매개 변수는 현재 디렉터리에서 파일을 만듭니다. 다음 출력과 유사한 결과가 표시되어야 합니다.

```console
C:\working> dotnet new console -n templatepack -o .
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on .\templatepack.csproj...
  Restore completed in 52.38 ms for C:\working\templatepack.csproj.

Restore succeeded.
```

이제 원하는 편집기에서 _templatepack.csproj_ 파일을 열고 콘텐츠를 다음 XML로 바꿉니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>

    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

위 XML의 `<PropertyGroup>` 설정은 세 개의 그룹으로 나뉩니다. 첫 번째 그룹은 NuGet 패키지에 필요한 속성을 처리합니다. 세 `<Package` 설정은 NuGet 피드에서 패키지를 식별하는 NuGet 패키지 속성과 관련이 있습니다. 특히, `<PacakgeId>` 값은 디렉터리 경로 대신 단일 이름으로 템플릿 팩을 제거하는 데 사용됩니다. 이 값을 사용하여 NuGet 피드에서 템플릿 팩을 설치할 수도 있습니다. `<Title>` 및 `<Tags>`와 같은 나머지 설정은 NuGet 피드에 표시되는 메타데이터와 관련이 있습니다. NuGet 설정에 대한 자세한 내용은 [NuGet 및 MSBuild 속성](/nuget/reference/msbuild-targets)을 참조하세요.

pack 명령을 실행하여 프로젝트를 컴파일하고 압축할 때 MSBuild가 제대로 실행되도록 `<TargetFramework>` 설정을 지정해야 합니다.

마지막 세 설정은 템플릿을 만들 때 NuGet 팩의 적절한 폴더에 포함되도록 프로젝트를 올바르게 구성하는 것과 관련이 있습니다.

`<ItemGroup>`은 두 설정을 포함합니다. 첫째, `<Content>` 설정은 _templates_ 폴더의 모든 항목을 콘텐츠로 포함합니다. 또한 _bin_ 폴더 또는 _obj_ 폴더를 제외하여 컴파일된 코드(템플릿을 테스트하여 컴파일한 경우)를 포함하지 않도록 설정됩니다. 둘째, `<Compile>` 설정은 위치에 상관없이 모든 코드 파일을 컴파일에서 제외합니다. 이 설정은 템플릿 팩을 만드는 데 사용 중인 프로젝트가 _templates_ 폴더 계층에서 코드를 컴파일하려고 시도하지 못하도록 차단합니다.

## <a name="build-and-install"></a>빌드 및 설치

이 파일을 저장한 다음 pack 명령을 실행합니다.

```dotnetcli
dotnet pack
```

이 명령은 프로젝트를 빌드하고 _working\bin\Debug_ 폴더에 NuGet 패키지를 만듭니다.

```console
C:\working> dotnet pack
Microsoft (R) Build Engine version 16.2.0-preview-19278-01+d635043bd for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 123.86 ms for C:\working\templatepack.csproj.

  templatepack -> C:\working\bin\Debug\netstandard2.0\templatepack.dll
  Successfully created package 'C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg'.
```

그런 다음 `dotnet new -i PATH_TO_NUPKG_FILE` 명령을 사용하여 템플릿 팩 파일을 설치합니다.

```console
C:\working> dotnet new -i C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name            Language          Tags
-------------------------------------------------------------------------------------------------------------------------------
Example templates: string extensions              stringext             [C#]              Common/Code
Console Application                               console               [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync          [C#]              Common/Console/C#8
Class library                                     classlib              [C#], F#, VB      Common/Library
```

NuGet 패키지를 NuGet 피드에 업로드한 경우 `dotnet new -i PACKAGEID` 명령을 사용할 수 있습니다. 여기서 `PACKAGEID`는 _.csproj_ 파일의 `<PackageId>` 설정과 동일합니다. 이 패키지 ID는 NuGet 패키지 식별자와 동일합니다.

## <a name="uninstall-the-template-pack"></a>템플릿 팩 제거

_.nupkg_ 파일을 직접 사용하거나 NuGet 피드를 사용하는 등 템플릿 팩을 설치한 방법에 상관없이 템플릿 팩을 제거하는 방법은 동일합니다. 제거하려는 템플릿의 `<PackageId>`를 사용합니다. `dotnet new -u` 명령을 실행하여 설치된 템플릿 목록을 가져올 수 있습니다.

```console
C:\working> dotnet new -u
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      dotnet gitignore file (gitignore)
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)

... cut to save space ...

  NUnit3.DotNetNew.Template
    Templates:
      NUnit 3 Test Project (nunit) C#
      NUnit 3 Test Item (nunit-test) C#
      NUnit 3 Test Project (nunit) F#
      NUnit 3 Test Item (nunit-test) F#
      NUnit 3 Test Project (nunit) VB
      NUnit 3 Test Item (nunit-test) VB
  AdatumCorporation.Utility.Templates
    Templates:
      Example templates: async project (consoleasync) C#
      Example templates: string extensions (stringext) C#
```

`dotnet new -u AdatumCorporation.Utility.Templates`을 실행하여 템플릿을 제거합니다. `dotnet new` 명령은 이전에 설치한 템플릿을 생략해야 한다는 도움말 정보를 출력합니다.

지금까지 템플릿 팩을 설치했다가 제거했습니다. 

## <a name="next-steps"></a>다음 단계

대부분의 내용은 이미 살펴보았지만 템플릿에 대한 자세한 내용은 [dotnet new에 대한 사용자 지정 템플릿](../tools/custom-templates.md) 문서를 참조하세요.

* [dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki)(dotnet/templating GitHub 리포지토리 Wiki)
* [dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples)(dotnet/dotnet-template-samples GitHub 리포지토리)
* [*template.json* JSON 스키마 저장소에 대 한 스키마](http://json.schemastore.org/template)
