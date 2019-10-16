---
title: dotnet new에 대한 사용자 지정 템플릿
description: 모든 형식의 .NET 프로젝트 또는 파일에 대한 사용자 지정 템플릿을 알아봅니다.
author: thraka
ms.date: 06/14/2019
ms.openlocfilehash: 7a599973a1914f0df187557e48718263f16546f3
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117810"
---
# <a name="custom-templates-for-dotnet-new"></a>dotnet new에 대한 사용자 지정 템플릿

[.NET Core SDK](https://dotnet.microsoft.com/download)에는 이미 설치되어 바로 사용할 수 있는 많은 템플릿이 포함되어 있습니다. [`dotnet new` 명령](dotnet-new.md)은 템플릿을 사용하는 방법일 뿐만 아니라 템플릿을 설치 및 제거하는 방법입니다. .NET Core 2.0부터 앱, 서비스, 도구 또는 클래스 라이브러리와 같은 모든 형식의 프로젝트에 대한 사용자 지정 템플릿을 만들 수 있습니다. 구성 파일과 같이 하나 이상의 종속 파일을 출력하는 템플릿도 만들 수 있습니다.

NuGet *.nupkg* 파일을 직접 참조하거나 템플릿이 포함된 파일 시스템 디렉터리를 지정하여 NuGet 피드의 NuGet 패키지에서 사용자 지정 템플릿을 설치할 수 있습니다. 템플릿 엔진은 값을 바꾸고, 파일을 포함 및 제외하고, 템플릿 사용 시 사용자 지정 처리 작업을 실행할 수 있는 기능을 제공합니다.

템플릿 엔진은 오픈 소스이며 온라인 코드 리포지토리는 GitHub의 [dotnet/templating](https://github.com/dotnet/templating/)에 있습니다. 템플릿 샘플을 보려면 [dotnet/dotnet-template-samples](https://github.com/dotnet/dotnet-template-samples) 리포지토리를 참조하세요. 타사 템플릿을 포함한 추가 템플릿은 GitHub의 [Available templates for dotnet new](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)(dotnet new에 대한 사용 가능한 템플릿)에서 찾을 수 있습니다. 사용자 지정 템플릿을 만들고 사용하는 방법에 대한 자세한 내용은 [How to create your own templates for dotnet new](https://devblogs.microsoft.com/dotnet/how-to-create-your-own-templates-for-dotnet-new/)(dotnet new에 대한 사용자 지정 템플릿을 만드는 방법) 및 [dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki)(dotnet/templating GitHub 리포지토리 Wiki)를 참조하세요.

연습을 수행하고 템플릿을 만들려면 [dotnet new에 대한 사용자 지정 템플릿 만들기](../tutorials/create-custom-template.md) 자습서를 참조하세요.

### <a name="net-default-templates"></a>.NET 기본 템플릿

[.NET Core SDK](https://dotnet.microsoft.com/download)를 설치할 때 콘솔 앱, 클래스 라이브러리, 단위 테스트 프로젝트, ASP.NET Core 앱([Angular](https://angular.io/) 및 [React](https://facebook.github.io/react/) 프로젝트 포함) 및 구성 파일을 비롯한 프로젝트 및 파일을 만들 수 있는 12개 이상의 기본 제공 템플릿이 제공됩니다. 기본 제공 템플릿을 나열하려면 `-l|--list` 옵션과 함께 `dotnet new` 명령을 실행합니다.

```dotnetcli
dotnet new --list
```

## <a name="configuration"></a>구성

템플릿은 다음 파트로 구성되어 있습니다.

- 소스 파일 및 폴더
- 구성 파일(*template.json*)

### <a name="source-files-and-folders"></a>소스 파일 및 폴더

소스 파일 및 폴더에는 `dotnet new <TEMPLATE>` 명령을 실행할 때 템플릿 엔진에서 사용하려는 파일과 폴더가 모두 포함됩니다. 템플릿 엔진은 프로젝트를 생성하는 데 *실행 가능한 프로젝트*를 소스 코드로 사용하도록 디자인되어 있습니다. 여기에는 여러 가지 이점이 있습니다.

- 템플릿 엔진에서는 특수 토큰을 프로젝트의 소스 코드에 삽입할 필요가 없습니다.
- 코드 파일은 특수 파일이 아니고 템플릿 엔진 작업을 수행하는 방식으로 수정되지도 않습니다. 따라서 일반적으로 프로젝트 작업을 할 때 사용하는 도구로 템플릿 콘텐츠를 처리할 수 있습니다.
- 다른 프로젝트를 처리하는 것처럼 템플릿 프로젝트를 빌드, 실행 및 디버그합니다.
- *./.template.config/template.json* 구성 파일을 프로젝트에 추가하면 기존 프로젝트에서 템플릿을 빠르게 만들 수 있습니다.

템플릿에 저장되는 파일과 폴더가 공식적인 .NET 프로젝트 형식으로 제한되지는 않습니다. 템플릿 엔진에서 하나의 파일만 출력으로 생성하는 경우에도, 소스 파일 및 폴더는 템플릿을 사용할 때 만들려는 모든 콘텐츠로 구성될 수 있습니다.

*template.json* 구성 파일에 제공한 논리 및 설정을 기준으로 템플릿에서 생성된 파일을 수정할 수 있습니다. 사용자는 `dotnet new <TEMPLATE>` 명령에 옵션을 전달하여 이러한 설정을 재정의할 수 있습니다. 사용자 지정 논리의 일반적인 예는 템플릿을 통해 배포되는 코드 파일에 클래스 또는 변수의 이름을 제공하는 것입니다.

### <a name="templatejson"></a>template.json

*template.json* 파일은 템플릿 루트 디렉터리의 *.template.config* 폴더에 배치됩니다. 이 파일은 템플릿 엔진에 구성 정보를 제공합니다. 기능 템플릿을 충분히 만들 수 있는 최소 구성으로 다음 표에 나와 있는 멤버가 필요합니다.

| 멤버            | 형식          | 설명 |
| ----------------- | ------------- | ----------- |
| `$schema`         | URI           | *template.json* 파일에 대한 JSON 스키마. 스키마 지정 시 JSON 스키마가 JSON 편집 기능을 구현하도록 지원하는 편집기. 예를 들어 [Visual Studio Code](https://code.visualstudio.com/)에서는 이 멤버가 IntelliSense를 구현해야 합니다. `http://json.schemastore.org/template` 값을 사용하세요. |
| `author`          | string        | 템플릿 작성자. |
| `classifications` | array(string) | 사용자가 템플릿 검색 시 템플릿을 찾는 데 사용할 수 있는 0개 이상의 템플릿 특성. `dotnet new -l|--list` 명령을 사용하여 생성된 템플릿 목록에 템플릿이 나타날 때 *태그* 열에 분류도 표시됩니다. |
| `identity`        | string        | 이 템플릿의 공유한 이름. |
| `name`            | string        | 사용자에게 표시되어야 하는 템플릿의 이름. |
| `shortName`       | string        | GUI를 통해 선택하는 것이 아니라 사용자가 템플릿 이름을 지정하는 환경에 적용되는, 템플릿 선택에 사용되는 기본 약식 이름. 예를 들어 명령 프롬프트에서 템플릿과 CLI 명령을 함께 사용할 경우 짧은 이름이 유용합니다. |

*template.json* 파일에 대한 전체 스키마는 [JSON Schema Store](http://json.schemastore.org/template)(JSON 스키마 저장소)에서 찾을 수 있습니다. *template.json* 파일에 대한 자세한 내용은 [dotnet 템플릿 wiki](https://github.com/dotnet/templating/wiki)를 참조하세요.

#### <a name="example"></a>예

예를 들어 아래에는 *console.cs* 및 *readme.txt*라는 두 개의 콘텐츠 파일이 포함된 템플릿 폴더가 있습니다. 또한 *template.json* 파일이 포함된 *.template.config*라는 필수 폴더가 있습니다.

```text
└───mytemplate
    │   console.cs
    │   readme.txt
    │
    └───.template.config
            template.json
```

*template.json* 파일은 다음과 같습니다.

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Travis Chau",
  "classifications": [ "Common", "Console" ],
  "identity": "AdatumCorporation.ConsoleTemplate.CSharp",
  "name": "Adatum Corporation Console Application",
  "shortName": "adatumconsole"
}
```

*mytemplate* 폴더는 설치 가능한 템플릿 팩입니다. 팩이 설치되고 나면, `dotnet new` 명령에 `shortName`을 사용할 수 있습니다. 예를 들어 `dotnet new adatumconsole`은 `console.cs` 및 `readme.txt` 파일을 현재 폴더에 출력합니다.

## <a name="packing-a-template-into-a-nuget-package-nupkg-file"></a>템플릿을 NuGet 패키지(nupkg 파일)로 압축

사용자 지정 템플릿은 [dotnet pack](dotnet-pack.md) 명령과 *.csproj* 파일을 사용하여 압축됩니다. 또는 [nuget pack](https://docs.microsoft.com/nuget/tools/cli-ref-pack) 명령 및 *.nuspec* 파일과 함께 [NuGet](https://docs.microsoft.com/nuget/tools/nuget-exe-cli-reference)을 사용할 수 있습니다. 그러나 NuGet을 사용하려면 Windows에서는 .NET Framework가 필요하고, Linux 및 MacOS에서는 [Mono](https://www.mono-project.com/)가 필요합니다.

*.csproj* 파일은 기존의 코드 프로젝트 *.csproj* 파일과 약간 다릅니다. 다음 설정을 참고하세요.

01. `<PackageType>` 설정이 추가되고 `Template`으로 설정됩니다.
01. `<PackageVersion>` 설정이 추가되고 유효한 [NuGet 버전 번호](/nuget/reference/package-versioning)로 설정됩니다.
01. `<PackageId>` 설정이 추가되고 고유 식별자로 설정됩니다. 이 식별자는 템플릿 팩을 제거하는 데 사용되며, NuGet 피드에서 템플릿 팩을 등록하는 데 사용됩니다.
01. `<Title>`, `<Authors>`, `<Description>`, `<PackageTags>` 등의 일반 메타데이터 설정을 지정해야 합니다.
01. 템플릿 프로세스에서 생성된 이진 파일을 사용하지 않더라도 `<TargetFramework>` 설정을 지정해야 합니다. 아래 예제에서는 `netstandard2.0`으로 설정되었습니다.

*.nupkg* NuGet 패키지 양식의 템플릿 팩은 모든 템플릿이 패키지 내의 *content* 폴더에 저장되어 있어야 합니다. 생성된 *.nupkg*을 템플릿 팩으로 설치할 수 있도록 *.csproj* 파일에 추가해야 하는 몇 가지 설정이 더 있습니다.

01. 프로젝트에서 NuGet 패키지의 **content**로 설정하는 모든 파일이 포함되도록 `<IncludeContentInPack>` 설정을 `true`로 지정합니다.
01. 컴파일러가 NuGet 패키지에서 생성하는 모든 이진 파일이 제외되도록 `<IncludeBuildOutput>` 설정을 `false`로 지정합니다.
01. `<ContentTargetFolders>` 설정을 `content`로 지정합니다. 이렇게 하면 **content**로 설정된 파일이 NuGet 패키지의 *content* 폴더에 저장됩니다. NuGet 패키지의 이 폴더는 dotnet 템플릿 시스템에서 구문 분석됩니다.

템플릿 프로젝트에서 코드 파일이 컴파일되지 않도록 모두 제외하는 간편한 방법은 프로젝트 파일의 `<ItemGroup>` 요소에 `<Compile Remove="**\*" />` 항목을 사용하는 것입니다.

템플릿 팩을 구성하는 간편한 방법은 모든 템플릿을 개별 폴더에 넣은 다음, *.csproj* 파일과 동일한 디렉터리에 있는 *templates* 폴더에 각 템플릿 폴더를 넣는 것입니다. 이렇게 하면 단일 프로젝트 항목을 사용하여 *templates*에 있는 모든 파일과 폴더를 **content**로 포함할 수 있습니다. `<ItemGroup>` 요소 내부에 `<Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />` 항목을 만듭니다.

다음은 위의 모든 지침을 따르는 예제 *.csproj* 파일입니다. *templates* 자식 폴더를 *content* 패키지 폴더에 압축하고, 코드 파일이 컴파일되지 않도록 모두 제외합니다.

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

아래 예제에서는 *.csproj*를 사용하여 템플릿 팩을 만드는 파일 및 폴더 구조를 보여 줍니다. *MyDotnetTemplates.csproj* 파일과 *templates* 폴더는 모두 *project_folder* 디렉터리의 루트에 있습니다. *templates* 폴더에는 *mytemplate1*과 *mytemplate2*라는 두 개의 템플릿이 들어 있습니다. 각 템플릿에 *template.json* 구성 파일이 포함된 *. template.config* 폴더와 콘텐츠 파일이 있습니다.

```text
project_folder
│   MyDotnetTemplates.csproj
│
└───templates
    ├───mytemplate1
    │   │   console.cs
    │   │   readme.txt
    │   │
    │   └───.template.config
    │           template.json
    │
    └───mytemplate2
        │   otherfile.cs
        │
        └───.template.config
                template.json
```

## <a name="installing-a-template"></a>템플릿 설치

[dotnet new -i|--install](dotnet-new.md) 명령을 사용하여 패키지를 설치합니다.

### <a name="to-install-a-template-from-a-nuget-package-stored-at-nugetorg"></a>nuget.org에 저장된 NuGet 패키지에서 템플릿을 설치하려면

NuGet 패키지 식별자를 사용하여 템플릿 패키지를 설치합니다.

```dotnetcli
dotnet new -i <NUGET_PACKAGE_ID>
```

### <a name="to-install-a-template-from-a-local-nupkg-file"></a>로컬 nupkg 파일에서 템플릿을 설치하려면

*.nupkg* NuGet 패키지 파일의 경로를 제공합니다.

```dotnetcli
dotnet new -i <PATH_TO_NUPKG_FILE>
```

### <a name="to-install-a-template-from-a-file-system-directory"></a>파일 시스템 디렉터리에서 템플릿을 설치하려면

위 예제의 *mytemplate1*과 같은 템플릿 폴더에서 템플릿을 설치할 수 있습니다. *.template.config* 폴더의 폴더 경로를 지정합니다. 템플릿 디렉터리의 경로가 절대 경로여야 하는 것은 아닙니다. 그러나 설치된 템플릿을 폴더에서 제거하려면 절대 경로가 필요합니다.

```dotnetcli
dotnet new -i <FILE_SYSTEM_DIRECTORY>
```

## <a name="get-a-list-of-installed-templates"></a>설치된 템플릿 목록 가져오기

다른 매개 변수가 없는 제거 명령은 설치된 템플릿을 모두 나열합니다.

```dotnetcli
dotnet new -u
```

해당 명령은 다음과 비슷한 출력을 반환합니다.

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)
  Microsoft.DotNet.Common.ProjectTemplates.3.0
    Templates:
      Class library (classlib) C#
      Class library (classlib) F#
      Class library (classlib) VB
      Console Application (console) C#
      Console Application (console) F#
      Console Application (console) VB
...
```

`Currently installed items:` 뒤에 있는 첫 번째 수준의 항목은 템플릿 제거에 사용되는 식별자입니다. 위 예제에서는 `Microsoft.DotNet.Common.ItemTemplates` 및 `Microsoft.DotNet.Common.ProjectTemplates.3.0`이 나열됩니다. 파일 시스템 경로를 사용하여 템플릿을 설치한 경우, 이 식별자는 *.template.config* 폴더의 폴더 경로입니다.

## <a name="uninstalling-a-template"></a>템플릿 제거

[dotnet new -u|--uninstall](dotnet-new.md) 명령을 사용하여 패키지를 제거합니다.

NuGet 피드 또는 *.nupkg* 파일을 통해 직접 패키지를 설치한 경우, 식별자를 제공합니다.

```dotnetcli
dotnet new -u <NUGET_PACKAGE_ID>
```

*.template.config* 폴더의 경로를 지정하여 패키지를 설치한 경우, **절대** 경로를 사용하여 패키지를 제거합니다. `dotnet new -u` 명령을 통해 제공된 출력에서 템플릿의 절대 경로를 확인할 수 있습니다. 자세한 내용은 위의 [설치된 템플릿 목록 가져오기](#get-a-list-of-installed-templates) 섹션을 참조하세요.

```dotnetcli
dotnet new -u <ABSOLUTE_FILE_SYSTEM_DIRECTORY>
```

## <a name="create-a-project-using-a-custom-template"></a>사용자 지정 템플릿을 사용하여 프로젝트 만들기

템플릿이 설치된 후 다른 미리 설치된 템플릿을 사용하는 것처럼 `dotnet new <TEMPLATE>` 명령을 실행하여 템플릿을 사용합니다. 템플릿 설정에서 구성한 템플릿 관련 옵션을 포함하여 `dotnet new` 명령에 대한 [옵션](dotnet-new.md#options)을 지정할 수도 있습니다. 템플릿의 짧은 이름을 직접 명령에 제공합니다.

```dotnetcli
dotnet new <TEMPLATE>
```

## <a name="see-also"></a>참고 항목

- [dotnet new에 대한 사용자 지정 템플릿(자습서)](../tutorials/create-custom-template.md)
- [dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki)(dotnet/templating GitHub 리포지토리 Wiki)
- [dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples)(dotnet/dotnet-template-samples GitHub 리포지토리)
- [How to create your own templates for dotnet new](https://devblogs.microsoft.com/dotnet/how-to-create-your-own-templates-for-dotnet-new/)(dotnet new에 대한 사용자 지정 템플릿을 만드는 방법)
- [*template.json* JSON 스키마 저장소에 대 한 스키마](http://json.schemastore.org/template)
