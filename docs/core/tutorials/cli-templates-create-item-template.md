---
title: dotnet new에 대한 항목 템플릿 만들기 - .NET Core CLI
description: dotnet new 명령에 대한 항목 템플릿을 만드는 방법을 알아봅니다. 항목 템플릿에 포함할 수 있는 파일 수에는 제한이 없습니다.
author: thraka
ms.date: 06/25/2019
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 5183781d6a131aa395cf7c1fd8a09e05ed0bd71d
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926147"
---
# <a name="tutorial-create-an-item-template"></a>자습서: 항목 템플릿 만들기

.NET Core를 사용하여 프로젝트, 파일, 리소스를 생성하는 템플릿을 만들고 배포할 수 있습니다. 이 자습서는 `dotnet new` 명령에 사용할 템플릿을 만들고, 설치하고, 제거하는 방법을 알려주는 시리즈의 1부입니다.

시리즈의 1부에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
>
> * 항목 템플릿에 대한 클래스 만들기
> * 템플릿 구성 폴더 및 파일 만들기
> * 파일 경로에서 템플릿 설치
> * 항목 템플릿 테스트
> * 항목 템플릿 제거

## <a name="prerequisites"></a>전제 조건

* [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download) 이상 버전
* 참조 문서 [dotnet new에 대한 사용자 지정 템플릿](../tools/custom-templates.md)을 읽어보세요.

  이 참조 문서에서는 템플릿에 대한 기본 사항과 템플릿을 취합하는 방법을 설명합니다. 이 참조 문서의 정보 일부가 여기에도 나옵니다.

* 터미널을 열고 _working\templates\\_ 폴더로 이동합니다.

## <a name="create-the-required-folders"></a>필요한 폴더 만들기

이 시리즈에서는 템플릿 소스가 포함되는 “작업 폴더”와 템플릿을 테스트하는 데 사용되는 “테스트 폴더”를 사용합니다. 작업 폴더와 테스트 폴더는 동일한 부모 폴더 아래에 있어야 합니다.

먼저 부모 폴더를 만듭니다. 이름은 중요하지 않습니다. 그런 다음 _working_이라는 하위 폴더를 만듭니다. _working_ 폴더 내부에 _templates_이라는 하위 폴더를 만듭니다.

그런 다음 부모 폴더 아래에 _test_라는 폴더를 만듭니다. 폴더 구조는 다음과 같이 표시됩니다.

```console
parent_folder
├───test
└───working
    └───templates
```

## <a name="create-an-item-template"></a>항목 템플릿 만들기

항목 템플릿은 하나 이상의 파일을 포함하는 특정 형식의 템플릿입니다. 이러한 형식의 템플릿은 구성, 코드 또는 솔루션 파일과 같은 항목을 생성하려는 경우에 유용합니다. 이 예제에서는 문자열 형식에 확장 메서드를 추가하는 클래스를 만듭니다.

터미널에서 _working\templates\\_폴더로 이동하고_extensions_라는 새 하위 폴더를 만듭니다. 폴더로 들어갑니다.

```console
working
└───templates
    └───extensions
```

_CommonExtensions.cs_라는 새 파일을 만들고 원하는 텍스트 편집기를 사용하여 엽니다. 이 클래스는 문자열의 내용을 반전하는 `Reverse`라는 확장 메서드를 제공합니다. 다음 코드를 붙여넣고 파일을 저장합니다.

```csharp
using System;

namespace System
{
    public static class StringExtensions
    {
        public static string Reverse(this string value)
        {
            var tempArray = value.ToCharArray();
            Array.Reverse(tempArray);
            return new string(tempArray);
        }
    }
}
```

템플릿의 콘텐츠를 만들었으므로 이제 템플릿의 루트 폴더에 템플릿 구성을 만들어야 합니다.

## <a name="create-the-template-config"></a>템플릿 구성 만들기

템플릿은 .NET Core의 템플릿 루트에 있는 특수 폴더 및 구성 파일에서 인식됩니다. 이 자습서에서 템플릿 폴더는 _working\templates\extensions\\_ 에 있습니다.

템플릿을 만들 때 템플릿 폴더의 모든 파일과 폴더는 특수 구성 폴더를 제외하고 템플릿의 일부로 포함됩니다. 이 구성 폴더는 _.template.config_입니다.

먼저 _.template.config_라는 새 하위 폴더를 만들고 폴더로 들어갑니다. 그런 다음 _template.json_이라는 새 파일을 만듭니다. 폴더 구조는 다음과 같이 표시됩니다.

```console
working
└───templates
    └───extensions
        └───.template.config
                template.json
```

원하는 텍스트 편집기에서 _template.json_을 열고 다음 JSON 코드를 붙여넣은 다음 저장합니다.

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Me",
  "classifications": [ "Common", "Code" ],
  "identity": "ExampleTemplate.StringExtensions",
  "name": "Example templates: string extensions",
  "shortName": "stringext",
  "tags": {
    "language": "C#",
    "type": "item"
  }
}
```

이 구성 파일에는 템플릿에 대한 모든 설정이 포함되어 있습니다. 기본 설정(예: `name` 및 `shortName`)도 확인할 수 있지만 `item`으로 설정된 `tags/type` 값도 있습니다. 이 값에 따라, 만든 템플릿이 항목 템플릿으로 분류됩니다. 만드는 템플릿 형식에 대한 제한은 없습니다. `item` 및 `project` 값은 사용자가 검색 중인 템플릿 형식을 쉽게 필터링할 수 있도록 .NET Core에서 권장하는 일반적인 이름입니다.

`classifications` 항목은 `dotnet new`를 실행할 때 표시되고 템플릿 목록을 가져오는 **태그** 열을 나타냅니다. 사용자는 분류 태그를 기준으로 검색할 수도 있습니다. \*.json 파일의 `tags` 속성을 `classifications` 태그 목록과 혼동하지 마세요. 불행히도 두 항목은 이름이 비슷합니다. *template.json* 파일에 대한 전체 스키마는 [JSON Schema Store](http://json.schemastore.org/template)(JSON 스키마 저장소)에서 찾을 수 있습니다. *template.json* 파일에 대한 자세한 내용은 [dotnet 템플릿 wiki](https://github.com/dotnet/templating/wiki)를 참조하세요.

유효한 _.template.config/template.json_ 파일이 있으므로 이제 템플릿을 설치할 준비가 되었습니다. 터미널에서 _extensions_ 폴더로 이동하고 다음 명령을 실행하여 현재 폴더에 있는 템플릿을 설치합니다.

* **Windows**: `dotnet new -i .\`
* **Linux 또는 macOS**: `dotnet new -i ./`

이 명령은 사용자 템플릿을 포함하여 설치된 템플릿 목록을 출력합니다.

```console
C:\working\templates\extensions> dotnet new -i .\
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name            Language          Tags
-------------------------------------------------------------------------------------------------------------------------------
Example templates: string extensions              stringext             [C#]              Common/Code
Console Application                               console               [C#], F#, VB      Common/Console
Class library                                     classlib              [C#], F#, VB      Common/Library
WPF Application                                   wpf                   [C#], VB          Common/WPF
Windows Forms (WinForms) Application              winforms              [C#], VB          Common/WinForms
Worker Service                                    worker                [C#]              Common/Worker/Web
```

## <a name="test-the-item-template"></a>항목 템플릿 테스트

항목 템플릿을 설치했으므로 이제 템플릿을 테스트합니다. _test/_ 폴더로 이동하고 `dotnet new console`을 사용하여 새 콘솔 애플리케이션을 만듭니다. 그러면 `dotnet run` 명령으로 쉽게 테스트할 수 있는 작업 프로젝트가 생성됩니다.

```console
C:\test> dotnet new console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on C:\test\test.csproj...
  Restore completed in 54.82 ms for C:\test\test.csproj.

Restore succeeded.
```

```console
C:\test> dotnet run
Hello World!
```

이제 `dotnet new stringext`를 실행하여 템플릿에서 _CommonExtensions.cs_를 생성합니다.

```console
C:\test> dotnet new stringext
The template "Example templates: string extensions" was created successfully.
```

템플릿에 제공된 확장 메서드를 사용하여 `"Hello World"` 문자열을 반전하도록 _Program.cs_에서 코드를 변경합니다.

```csharp
Console.WriteLine("Hello World!".Reverse());
```

프로그램을 다시 실행하면 결과가 반전된 것을 알 수 있습니다.

```console
C:\test> dotnet run
!dlroW olleH
```

지금까지 .NET Core를 사용하여 항목 템플릿을 만들고 배포했습니다. 이 자습서 시리즈의 다음 부분에 대비하여, 여기서 만든 템플릿을 제거해야 합니다. 또한 _test_ 폴더에서 모든 파일을 삭제해야 합니다. 그러면 이 자습서의 다음 주요 섹션을 위해 정리된 상태로 되돌아갑니다.

## <a name="uninstall-the-template"></a>템플릿 제거

파일 경로를 사용하여 템플릿을 설치했으므로 **절대** 파일 경로를 사용하여 템플릿을 제거해야 합니다. `dotnet new -u` 명령을 실행하여 설치된 템플릿 목록을 확인할 수 있습니다. 사용자 템플릿은 마지막에 나열되어야 합니다. `dotnet new -u <ABSOLUTE PATH TO TEMPLATE DIRECTORY>` 명령을 사용하여 템플릿을 제거하려면 나열된 경로를 사용합니다.

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
  C:\working\templates\extensions
    Templates:
      Example templates: string extensions (stringext) C#
```

```console
C:\working> dotnet new -u C:\working\templates\extensions
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 항목 템플릿을 만들었습니다. 프로젝트 템플릿을 만드는 방법을 알아보려면 이 자습서 시리즈를 계속 진행하세요.

> [!div class="nextstepaction"]
> [프로젝트 템플릿 만들기](cli-templates-create-project-template.md)
