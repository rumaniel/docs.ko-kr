---
title: CLI 도구를 사용한 .NET Core 앱 배포
description: CLI(명령줄 인터페이스) 도구를 사용한 .NET Core 앱 배포에 대해 알아봅니다.
author: rpetrusha
ms.author: ronpet
ms.date: 09/05/2018
dev_langs:
- csharp
- vb
ms.openlocfilehash: 6c0eb82b6be5d65c70287dd601bb97868af1c943
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49454451"
---
# <a name="deploying-net-core-apps-with-command-line-interface-cli-tools"></a>CLI(명령줄 인터페이스) 도구를 사용하여 .NET Core 앱 배포

.NET Core 응용 프로그램은 응용 프로그램 이진을 포함하지만 대상 시스템에 .NET Core가 있는지 여부에 따라 달라지는 *프레임워크 종속 배포* 또는 응용 프로그램과 .NET Core 이진을 모두 포함하는 *자체 포함 배포*로 배포할 수 있습니다. 개요는 [.NET Core 응용 프로그램 배포](index.md)를 참조하세요.

다음 섹션에서는 [.NET Core 명령줄 인터페이스 도구](../tools/index.md)를 사용하여 다음과 같은 종류의 배포를 만드는 방법을 보여 줍니다.

- 프레임워크 종속 배포
- 타사 종속성이 있는 프레임워크 종속 배포
- 자체 포함 배포
- 타사 종속성이 있는 자체 포함 배포

명령줄에서 작업하는 경우 선택한 프로그램 편집기를 사용할 수 있습니다. 프로그램 편집기가 [Visual Studio Code](https://code.visualstudio.com)인 경우 **보기** > **통합 터미널**을 선택하여 Visual Studio Code 환경 내에서 명령 콘솔을 열 수 있습니다.

## <a name="framework-dependent-deployment"></a>프레임워크 종속 배포

타사 종속성이 없는 프레임워크 종속 배포에는 앱의 빌드, 테스트 및 게시만 포함됩니다. C#으로 작성된 간단한 예제에서는 이 프로세스를 보여 줍니다.

1. 프로젝트 디렉터리를 만듭니다.

   프로젝트에 대한 디렉터리를 만들고 현재 디렉터리로 설정합니다.

1. 프로젝트를 만듭니다.

   명령줄에서 [dotnet new console](../tools/dotnet-new.md)을 입력하여 새 C# 콘솔 프로젝트를 만들거나 [dotnet new console -lang vb](../tools/dotnet-new.md)를 입력하여 해당 디렉터리에 새 Visual Basic 콘솔 프로젝트를 만듭니다.

1. 응용 프로그램의 소스 코드를 추가합니다.

   편집기에서 *Program.cs* 또는 *Program.vb* 파일을 열고 자동 생성된 코드를 다음 코드로 바꿉니다. 텍스트를 입력하라는 메시지가 표시된 다음 사용자가 입력한 개별 단어가 표시됩니다. 정규식 `\w+`를 사용하여 입력 테스트의 단어를 구분합니다.

   [!code-csharp[deployment#1](~/samples/snippets/core/deploying/cs/deployment-example.cs)]
   [!code-vb[deployment#1](~/samples/snippets/core/deploying/vb/deployment-example.vb)]

1. 프로젝트의 종속성 및 도구를 업데이트합니다.

   [dotnet restore](../tools/dotnet-restore.md)([참고 참조](#dotnet-restore-note)) 명령을 실행하여 프로젝트에 지정된 종속성을 복원합니다.

1. 앱의 디버그 빌드를 만듭니다.

   [dotnet build](../tools/dotnet-build.md) 명령을 사용하여 응용 프로그램을 빌드하거나 [dotnet run](../tools/dotnet-run.md) 명령을 사용하여 응용 프로그램을 빌드하고 실행합니다.

1. 앱을 배포합니다.

   프로그램을 디버그하고 테스트한 후 다음 명령을 사용하여 배포를 만듭니다.

      ```console
      dotnet publish -f netcoreapp2.1 -c Release
      ```
   그러면 앱의 디버그가 아닌 릴리스 버전이 만들어집니다. 결과 파일은 프로젝트 *bin* 디렉터리의 하위 디렉터리에 있는 *publish*라는 디렉터리에 배치됩니다.

   게시 프로세스에서는 응용 프로그램의 파일과 함께 앱에 대한 디버깅 정보를 포함하는 프로그램 데이터베이스(.pdb) 파일을 내보냅니다. 이 파일은 주로 예외 디버그에 유용합니다. 응용 프로그램 파일과 함께 배포하지 않도록 선택할 수 있습니다. 하지만 앱의 릴리스 빌드를 디버그하려는 경우 파일을 저장해야 합니다.

   응용 프로그램 파일의 전체 집합을 원하는 방식으로 배포할 수 있습니다. 예를 들어 Zip 파일로 패키지하거나, 간단한 `copy` 명령을 사용하거나, 선택한 설치 패키지와 함께 배포할 수 있습니다.

1. 앱 실행

   설치되고 나면 사용자가 `dotnet` 명령을 사용하고 `dotnet fdd.dll` 등의 응용 프로그램 파일 이름을 제공하여 응용 프로그램을 실행할 수 있습니다.

   설치 관리자는 응용 프로그램 이진 외에도 공유 프레임워크 설치 관리자를 번들로 제공하거나 응용 프로그램 설치의 일부로 필수 조건을 확인해야 합니다.  공유 프레임워크 설치에는 관리자/루트 액세스 권한이 필요합니다.

## <a name="framework-dependent-deployment-with-third-party-dependencies"></a>타사 종속성이 있는 프레임워크 종속 배포

하나 이상의 타사 종속성이 있는 프레임워크 종속 배포를 배포하려면 프로젝트에서 해당 종속성을 사용할 수 있어야 합니다. 다음 두 가지 추가 단계를 수행해야 `dotnet restore`([참고 참조](#dotnet-restore-note)) 명령을 실행할 수 있습니다.

1. 필요한 타사 라이브러리에 대한 참조를 *csproj* 파일의 `<ItemGroup>` 섹션에 추가합니다. 다음 `<ItemGroup>` 섹션에는 [Json.NET](https://www.newtonsoft.com/json)에 대한 종속성이 타사 라이브러리로 포함되어 있습니다.

      ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
      </ItemGroup>
      ```

1. 타사 종속성을 포함하는 NuGet 패키지를 아직 다운로드하지 않은 경우 다운로드합니다. 패키지를 다운로드하려면 종속성을 추가한 후 `dotnet restore`([참고 참조](#dotnet-restore-note)) 명령을 실행합니다. 종속성은 게시 시간에 로컬 NuGet 캐시에서 확인되므로 시스템에서 사용할 수 있어야 합니다.

타사 종속성이 있는 프레임워크 종속 배포는 타사 종속성만큼만 이식 가능합니다. 예를 들어 타사 라이브러리에서 macOS를 지원하는 경우 Windows 시스템에 앱을 이식할 수 없습니다. 이러한 현상은 타사 종속성 자체가 네이티브 코드에 종속된 경우에 발생합니다. 관련된 좋은 예로 [libuv](https://github.com/libuv/libuv)에 대한 기본 종속성이 필요한 [Kestrel 서버](/aspnet/core/fundamentals/servers/kestrel)가 있습니다. 이런 종류의 타사 종속성이 있는 응용 프로그램에 대해 FDD를 만들면 게시된 출력에는 기본 종속성에서 지원하고 NuGet 패키지에 있는 각 [RID(런타임 식별자)](../rid-catalog.md)에 대한 폴더가 포함됩니다.

## <a name="simpleSelf"></a> 타사 종속성이 없는 자체 포함 배포

타사 종속성이 없는 자체 포함 배포에는 프로젝트 만들기, *csproj* 파일 수정, 앱 빌드, 테스트 및 게시가 포함됩니다. C#으로 작성된 간단한 예제에서는 이 프로세스를 보여 줍니다. 이 예제는 명령줄에서 [dotnet 유틸리티](../tools/dotnet.md)를 사용하여 자체 포함 배포를 만드는 방법을 보여 줍니다.

1. 프로젝트에 대한 디렉터리를 만듭니다.

   프로젝트에 대한 디렉터리를 만들고 현재 디렉터리로 설정합니다.

1. 프로젝트를 만듭니다.

   명령줄에서 [dotnet new console](../tools/dotnet-new.md)을 입력하여 해당 디렉터리에 새 C# 콘솔 프로젝트를 만듭니다.

1. 응용 프로그램의 소스 코드를 추가합니다.

   편집기에서 *Program.cs* 파일을 열고 자동 생성된 코드를 다음 코드로 바꿉니다. 텍스트를 입력하라는 메시지가 표시된 다음 사용자가 입력한 개별 단어가 표시됩니다. 정규식 `\w+`를 사용하여 입력 테스트의 단어를 구분합니다.

   [!code-csharp[deployment#1](~/samples/snippets/core/deploying/cs/deployment-example.cs)]
   [!code-vb[deployment#1](~/samples/snippets/core/deploying/vb/deployment-example.vb)]
1. 앱의 대상 플랫폼을 정의합니다.

   *csproj* 파일의 `<PropertyGroup>` 섹션에서 앱의 대상 플랫폼을 정의하는 `<RuntimeIdentifiers>` 태그를 만들고 각 대상 플랫폼의 RID(런타임 식별자)를 지정합니다. RID를 구분하려면 세미콜론도 추가해야 합니다. 런타임 식별자 목록은 [런타임 식별자 카탈로그](../rid-catalog.md)를 참조하세요.

   예를 들어 다음 `<PropertyGroup>` 섹션은 앱이 64비트 Windows 10 운영 체제 및 64비트 OS X 버전 10.11 운영 체제에서 실행됨을 나타냅니다.

     ```xml
     <PropertyGroup>
         <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
     </PropertyGroup>
     ```

   `<RuntimeIdentifiers>` 요소는 *csproj* 파일에 있는 모든 `<PropertyGroup>`에 표시될 수 있습니다. 전체 샘플 *csproj* 파일은 이 섹션의 뒷부분에 나옵니다.

1. 프로젝트의 종속성 및 도구를 업데이트합니다.

   [dotnet restore](../tools/dotnet-restore.md)([참고 참조](#dotnet-restore-note)) 명령을 실행하여 프로젝트에 지정된 종속성을 복원합니다.

1. 세계화 고정 모드를 사용할 것인지 여부를 결정합니다.

   특히 앱이 Linux를 대상으로 하는 경우 [세계화 고정 모드](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/globalization-invariant-mode.md)를 활용하여 배포의 총 크기를 줄일 수 있습니다. 세계화 고정 모드는 전역적으로 인식되지 않는 서식 지정 규칙, 대/소문자 규칙 및 문자열 비교와 [고정 문화권](xref:System.Globalization.CultureInfo.InvariantCulture)의 정렬 순서를 사용할 수 있는 응용 프로그램에 유용합니다.

   고정 모드를 사용하려면 **솔루션 탐색기**에서 프로젝트(솔루션 아님)를 마우스 오른쪽 단추로 클릭하고 **SCD.csproj 편집** 또는 **SCD.vbproj 편집**을 선택합니다. 그런 다음, 강조 표시된 다음 줄을 파일에 추가합니다.

 [!code-xml[globalization-invariant-mode](~/samples/snippets/core/deploying/xml/invariant.csproj)]

1. 앱의 디버그 빌드를 만듭니다.

   명령줄에서 [dotnet build](../tools/dotnet-build.md) 명령을 사용합니다.

1. 프로그램을 디버그하고 테스트한 후에는 각 대상 플랫폼에 대해 앱과 함께 배포할 파일을 만듭니다.

   다음과 같이 두 대상 플랫폼에 대해 `dotnet publish` 명령을 사용합니다.

      ```console
      dotnet publish -c Release -r win10-x64
      dotnet publish -c Release -r osx.10.11-x64
      ```

   그러면 각 대상 플랫폼에 대해 앱의 디버그가 아닌 릴리스 버전이 만들어집니다. 결과 파일은 프로젝트 *.\bin\Release\netcoreapp2.1\<runtime_identifier>* 하위 디렉터리의 하위 디렉터리에 있는 *publish*라는 하위 디렉터리에 저장됩니다. 각 하위 디렉터리에는 앱을 시작하는 데 필요한 전체 파일 집합(앱 파일 및 모든 .NET Core 파일)이 포함됩니다.

게시 프로세스에서는 응용 프로그램의 파일과 함께 앱에 대한 디버깅 정보를 포함하는 프로그램 데이터베이스(.pdb) 파일을 내보냅니다. 이 파일은 주로 예외 디버그에 유용합니다. 응용 프로그램 파일과 함께 패키지하지 않도록 선택할 수 있습니다. 하지만 앱의 릴리스 빌드를 디버그하려는 경우 파일을 저장해야 합니다.

게시된 파일을 원하는 방식으로 배포합니다. 예를 들어 Zip 파일로 패키지하거나, 간단한 `copy` 명령을 사용하거나, 선택한 설치 패키지와 함께 배포할 수 있습니다.

다음은 이 프로젝트에 대한 전체 *csproj* 파일입니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
</Project>
```

## <a name="self-contained-deployment-with-third-party-dependencies"></a>타사 종속성이 있는 자체 포함 배포

하나 이상의 타사 종속성이 있는 자체 포함 배포에는 종속성 추가가 포함됩니다. 다음 두 가지 추가 단계를 수행해야 `dotnet restore`([참고 참조](#dotnet-restore-note)) 명령을 실행할 수 있습니다.

1. 모든 타사 라이브러리에 대한 참조를 *csproj* 파일의 `<ItemGroup>` 섹션에 추가합니다. 다음 `<ItemGroup>` 섹션에서는 Json.NET을 타사 라이브러리로 사용합니다.

    ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
      </ItemGroup>
    ```

1. 타사 종속성을 포함하는 NuGet 패키지를 시스템에 아직 다운로드하지 않은 경우 다운로드합니다. 앱에서 종속성을 사용할 수 있도록 하려면 종속성을 추가한 후 `dotnet restore`([참고 참조](#dotnet-restore-note)) 명령을 실행합니다. 종속성은 게시 시간에 로컬 NuGet 캐시에서 확인되므로 시스템에서 사용할 수 있어야 합니다.

다음은 이 프로젝트에 대한 전체 *csproj* 파일입니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
  </ItemGroup>
</Project>
```

응용 프로그램을 배포하면 앱에서 사용된 타사 종속성도 응용 프로그램 파일에 포함됩니다. 타사 라이브러리는 앱이 실행되는 시스템에 없어도 됩니다.

타사 라이브러리가 있는 자체 포함 배포는 해당 라이브러리에서 지원하는 플랫폼에만 배포할 수 있습니다. 이 배포는 기본 종속성과 함께 타사 종속성이 있는 프레임워크 종속 배포와 유사하며, 기본 종속성이 앱을 배포할 플랫폼과 호환되어야 합니다.

<a name="dotnet-restore-note"></a>
[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

## <a name="see-also"></a>참고 항목

* [.NET Core 응용 프로그램 배포](index.md)
* [.NET Core RID(런타임 식별자) 카탈로그](../rid-catalog.md)
