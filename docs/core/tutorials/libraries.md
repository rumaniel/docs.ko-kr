---
title: 플랫폼 간 도구로 라이브러리 개발
description: .NET Core CLI 도구를 사용하여 .NET Core 라이브러리를 만드는 방법을 알아봅니다. 여러 프레임워크를 지원하는 라이브러리를 만듭니다.
author: cartermp
ms.date: 05/01/2017
ms.custom: seodec18
ms.openlocfilehash: 536319bc02b45e7948c89ae67988e821a55a842d
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117414"
---
# <a name="developing-libraries-with-cross-platform-tools"></a>플랫폼 간 도구로 라이브러리 개발

이 문서에서는 플랫폼 간 CLI 도구를 사용하여 .NET용 라이브러리를 작성하는 방법을 다룹니다. CLI는 지원되는 운영 체제에서 작동하는 효율적인 하위 수준 환경을 제공합니다. Visual Studio로 라이브러리를 빌드할 수 있습니다. 그러한 환경을 선호하는 경우 [Visual Studio 설명서를 참조하세요](libraries-with-vs.md).

## <a name="prerequisites"></a>전제 조건

컴퓨터에 [.NET Core SDK 및 CLI](https://dotnet.microsoft.com/download)를 설치해야 합니다.

.NET Framework 버전을 다루는 이 문서의 섹션에서는 [.NET Framework](https://dotnet.microsoft.com)가 설치된 Windows 컴퓨터가 필요합니다.

또한 이전 .NET Framework 대상을 지원하려는 경우 [.NET 다운로드 보관 페이지](https://dotnet.microsoft.com/download/archives)에서 이전 프레임워크 버전용 타기팅/개발자 팩을 설치해야 합니다. 다음 표를 참조하세요.

| .NET Framework 버전 | 다운로드할 파일                                       |
| ---------------------- | ------------------------------------------------------ |
| 4.6.1                  | .NET Framework 4.6.1 타기팅 팩                    |
| 4.6                    | .NET framework 4.6 타기팅 팩                      |
| 4.5.2                  | .NET framework 4.5.2 개발자 팩                    |
| 4.5.1                  | .NET framework 4.5.1 개발자 팩                    |
| 4.5                    | Windows 8용 Windows 소프트웨어 개발 키트         |
| 4.0                    | Windows 7 및 .NET Framework 4용 Windows SDK         |
| 2.0, 3.0 및 3.5      | .NET Framework 3.5 SP1 런타임(또는 Windows 8 이상 버전) |

## <a name="how-to-target-the-net-standard"></a>.NET 표준을 대상으로 지정하는 방법

.NET 표준에 익숙하지 않은 경우 자세한 내용은 [.NET 표준](../../standard/net-standard.md)을 참조하세요.

이 문서에는 .NET 표준을 다양한 구현에 매핑하는 표가 있습니다.

[!INCLUDE [net-standard-table](../../../includes/net-standard-table.md)]

라이브러리 만들기 작업에서 이 표의 의미는 다음과 같습니다.

선택한 .NET Standard 버전에 따라 최신 API에 대한 액세스와 .NET 구현 및 .NET Standard 버전을 대상으로 지정할 수 있는 기능 간에 균형을 유지하게 됩니다. `netstandardX.X`(여기서 `X.X`는 버전 번호임) 버전을 선택하고 프로젝트 파일(`.csproj` 또는 `.fsproj`)에 추가하여 대상 지정이 가능한 플랫폼과 버전의 범위를 제어합니다.

.NET 표준을 대상으로 할 때 요구에 따라 세 가지 기본 옵션이 있습니다.

1. 템플릿에서 제공하는 기본 버전의 .NET 표준(`netstandard1.4`)을 사용할 수 있습니다. 이 버전을 통해 UWP, .NET Framework 4.6.1 및 예정된 .NET 표준 2.0과 호환성을 유지하면서 .NET 표준에 있는 대부분의 API에 액세스할 수 있습니다.

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <TargetFramework>netstandard1.4</TargetFramework>
      </PropertyGroup>
    </Project>
    ```

2. 프로젝트 파일의 `TargetFramework` 노드에 있는 값을 수정하여 하위 또는 상위 버전의 .NET 표준을 사용할 수 있습니다.

    .NET 표준 버전은 이전 버전과 호환됩니다. 즉, `netstandard1.0` 라이브러리는 `netstandard1.1` 플랫폼 이상에서 실행됩니다. 그러나 이후 버전과는 호환되지 않습니다. 더 낮은 .NET 표준 플랫폼은 더 높은 버전을 참조할 수 없습니다. 즉, `netstandard1.0` 라이브러리는 `netstandard1.1` 이상을 대상으로 하는 라이브러리를 참조할 수 없습니다. 요구에 맞게 API와 플랫폼 지원이 올바르게 혼합된 표준 버전을 선택하세요. 지금은 `netstandard1.4`를 사용하는 것이 좋습니다.

3. .NET Framework 버전 4.0 이하를 대상으로 하거나 .NET Framework에서는 사용 가능하지만 .NET 표준에서는 사용할 수 없는 API를 사용하려는 경우(예: `System.Drawing`) 다음 섹션을 읽어보고 멀티 타기팅 방법을 알아보세요.

## <a name="how-to-target-the-net-framework"></a>.NET Framework를 대상으로 지정하는 방법

> [!NOTE]
> 다음 지침은 컴퓨터에 .NET Framework가 설치된 것으로 가정합니다. 설치된 종속성을 알아보려면 [필수 조건](#prerequisites)을 참조하세요.

여기서 사용된 .NET Framework 버전 중 일부는 더 이상 지원되지 않습니다. 지원되지 않는 버전은 [.NET Framework Support Lifecycle Policy FAQ(.NET Framework 지원 수명 주기 정책 FAQ)](https://support.microsoft.com/gp/framework_faq/en-us)를 참조하세요.

가장 많은 수의 개발자 및 프로젝트에 도달하려면 기준 대상으로 .NET Framework 4.0을 사용합니다. .NET Framework를 대상으로 하려면 지원할 .NET Framework 버전에 해당하는 올바른 TFM(Target Framework Moniker)을 사용하여 시작해야 합니다.

| .NET Framework 버전 | TFM      |
| ---------------------- | -------- |
| .NET Framework 2.0     | `net20`  |
| .NET Framework 3.0     | `net30`  |
| .NET Framework 3.5     | `net35`  |
| .NET Framework 4.0     | `net40`  |
| .NET Framework 4.5     | `net45`  |
| .NET Framework 4.5.1   | `net451` |
| .NET Framework 4.5.2   | `net452` |
| .NET Framework 4.6     | `net46`  |
| .NET Framework 4.6.1   | `net461` |
| .NET Framework 4.6.2   | `net462` |
| .NET Framework 4.7     | `net47`  |
| .NET Framework 4.8     | `net48`  |

그런 다음 이 TFM을 프로젝트 파일의 `TargetFramework` 섹션에 삽입합니다. 예를 들어 .NET Framework 4.0을 대상으로 하는 라이브러리의 작성 방법을 같습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net40</TargetFramework>
  </PropertyGroup>
</Project>
```

됐습니다! 이는 .NET Framework 4에 대해서만 컴파일되지만 이후 버전의 .NET Framework에서 라이브러리를 사용할 수 있습니다.

## <a name="how-to-multitarget"></a>멀티 타기팅 방법

> [!NOTE]
> 다음 지침에서는 컴퓨터에 .NET Framework가 설치된 것으로 가정합니다. 설치해야 할 종속성 및 다운로드할 위치에 대해 알아보려면 [필수 조건](#prerequisites) 섹션을 참조하세요.

프로젝트가 .NET Framework 및 .NET Core를 모두 지원하는 경우 이전 버전의 .NET Framework를 대상으로 해야 할 수 있습니다. 이 시나리오에서, 최신 대상에 최신 API 및 언어 구조를 사용하려는 경우 코드에 `#if` 지시문을 사용하세요. 각각의 경우에 필요한 API를 포함하기 위해 대상으로 지정하는 각 플랫폼마다 서로 다른 패키지와 종속성을 추가해야 할 수도 있습니다.

예를 들어 HTTP를 통해 네트워킹 작업을 수행하는 라이브러리가 있다고 가정해 보겠습니다. .NET 표준 및 .NET Framework 버전 4.5 이상 경우 `System.Net.Http` 네임스페이스의 `HttpClient` 클래스를 사용할 수 있습니다. 그러나 이전 버전의 .NET Framework에는 `HttpClient` 클래스가 없으므로, 이에 대해 `System.Net` 네임스페이스의 `WebClient` 클래스를 사용할 수 있습니다.

프로젝트 파일이 다음과 같이 표시될 수 있습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.0 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net40'">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.5 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net45'">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>
</Project>
```

여기서 다음 세 가지 주요 변경 내용을 확인할 수 있습니다.

1. `TargetFramework` 노드가 `TargetFrameworks`로 대체되었으며, 세 개의 TFM이 내부에 표시됩니다.
1. `net40` 대상에는 .NET Framework 참조 하나를 끌어오는 `<ItemGroup>` 노드가 있습니다.
1. `net45` 대상에는 .NET Framework 참조 두 개를 끌어오는 `<ItemGroup>` 노드가 있습니다.

빌드 시스템은 `#if` 지시문에 사용된 다음의 전처리기 기호를 인식합니다.

[!INCLUDE [Preprocessor symbols](../../../includes/preprocessor-symbols.md)]

대상당 조건부 컴파일을 사용하는 예는 다음과 같습니다.

```csharp
using System;
using System.Text.RegularExpressions;
#if NET40
// This only compiles for the .NET Framework 4 targets
using System.Net;
#else
 // This compiles for all other targets
using System.Net.Http;
using System.Threading.Tasks;
#endif

namespace MultitargetLib
{
    public class Library
    {
#if NET40
        private readonly WebClient _client = new WebClient();
        private readonly object _locker = new object();
#else
        private readonly HttpClient _client = new HttpClient();
#endif

#if NET40
        // .NET Framework 4.0 does not have async/await
        public string GetDotNetCount()
        {
            string url = "https://www.dotnetfoundation.org/";

            var uri = new Uri(url);

            string result = "";

            // Lock here to provide thread-safety.
            lock(_locker)
            {
                result = _client.DownloadString(uri);
            }

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"Dotnet Foundation mentions .NET {dotNetCount} times!";
        }
#else
        // .NET 4.5+ can use async/await!
        public async Task<string> GetDotNetCountAsync()
        {
            string url = "https://www.dotnetfoundation.org/";

            // HttpClient is thread-safe, so no need to explicitly lock here
            var result = await _client.GetStringAsync(url);

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"dotnetfoundation.org mentions .NET {dotNetCount} times in its HTML!";
        }
#endif
    }
}
```

`dotnet build`를 사용하여 이 프로젝트를 빌드하면 `bin/` 폴더 아래에 다음 3개의 디렉터리가 표시됩니다.

```
net40/
net45/
netstandard1.4/
```

각 디렉터리에는 각 대상에 대한 `.dll` 파일이 들어 있습니다.

## <a name="how-to-test-libraries-on-net-core"></a>.NET Core에서 라이브러리를 테스트하는 방법

플랫폼 간에 테스트할 수 있는 기능이 중요합니다. 기본적으로 [xUnit](https://xunit.github.io/) 또는 MSTest를 사용할 수 있습니다. 둘 다 .NET Core에서 라이브러리를 단위 테스트하는 데 적합합니다. 테스트 프로젝트로 솔루션을 설정하는 방법은 [솔루션 구조](#structuring-a-solution)에 따라 달라집니다. 다음 예제에서는 테스트 및 원본 디렉터리가 동일한 최상위 디렉터리에 있다고 가정합니다.

> [!NOTE]
> 일부 [.NET Core CLI 명령](../tools/index.md)이 사용됩니다. 자세한 내용은 [dotnet new](../tools/dotnet-new.md) 및 [dotnet sln](../tools/dotnet-sln.md)을 참조하세요.

1. 솔루션을 설정합니다. 다음 명령을 사용하여 설정할 수 있습니다.

   ```bash
   mkdir SolutionWithSrcAndTest
   cd SolutionWithSrcAndTest
   dotnet new sln
   dotnet new classlib -o MyProject
   dotnet new xunit -o MyProject.Test
   dotnet sln add MyProject/MyProject.csproj
   dotnet sln add MyProject.Test/MyProject.Test.csproj
   ```

   그러면 프로젝트가 생성되고 솔루션에서 함께 연결됩니다. `SolutionWithSrcAndTest` 디렉터리가 다음과 같이 표시됩니다.

   ```
   /SolutionWithSrcAndTest
   |__SolutionWithSrcAndTest.sln
   |__MyProject/
   |__MyProject.Test/
   ```

1. 테스트 프로젝트의 디렉터리로 이동한 다음 `MyProject`의 `MyProject.Test`에 대한 참조를 추가합니다.

   ```bash
   cd MyProject.Test
   dotnet add reference ../MyProject/MyProject.csproj
   ```

1. 패키지를 복원하고 프로젝트를 빌드합니다.

   ```dotnetcli
   dotnet restore
   dotnet build
   ```

   [!INCLUDE[DotNet Restore Note](../../../includes/dotnet-restore-note.md)]

1. `dotnet test` 명령을 실행하여 xUnit가 실행되는지 확인합니다. MSTest를 사용하도록 선택한 경우 MSTest 콘솔 실행기가 대신 실행되어야 합니다.

됐습니다! 이제 명령줄 도구를 사용하여 모든 플랫폼 라이브러리를 테스트할 수 있습니다. 이제 모든 것이 설정되어 계속해서 테스트하려는 경우 라이브러리 테스트는 매우 간단합니다.

1. 라이브러리를 변경합니다.
1. 명령줄의 테스트 디렉터리에서 `dotnet test` 명령으로 테스트를 실행합니다.

`dotnet test` 명령을 호출하면 자동으로 코드가 다시 빌드됩니다.

## <a name="how-to-use-multiple-projects"></a>여러 프로젝트를 사용하는 방법

더 큰 라이브러리의 경우 일반적으로 서로 다른 프로젝트에 기능을 배치해야 합니다.

자연스러운 C# 및 F#에 사용할 수 있는 라이브러리를 빌드하려 한다고 가정해 보겠습니다. 즉, 라이브러리의 소비자가 C# 및 F#에 자연스러운 방식으로 라이브러리를 사용한다는 의미입니다. 예를 들어 C#에서 다음과 같이 라이브러리를 사용할 수 있습니다.

```csharp
using AwesomeLibrary.CSharp;

public Task DoThings(Data data)
{
    var convertResult = await AwesomeLibrary.ConvertAsync(data);
    var result = AwesomeLibrary.Process(convertResult);
    // do something with result
}
```

F#에서는 다음과 같습니다.

```fsharp
open AwesomeLibrary.FSharp

let doWork data = async {
    let! result = AwesomeLibrary.AsyncConvert data // Uses an F# async function rather than C# async method
    // do something with result
}
```

이와 같은 사용 시나리오는, 액세스하는 API가 C# 및 F#에 대해 다른 구조를 가지고 있어야 한다는 뜻입니다.  이를 수행하는 일반적인 방법은 Core 프로젝트로 호출하는 API 계층을 정의하는 C# 및 F# 프로젝트에서 라이브러리의 모든 논리를 해당 Core 프로젝트로 팩터링하는 것입니다.  섹션의 나머지 부분에서는 다음 이름을 사용합니다.

* **AwesomeLibrary.Core** - 라이브러리에 대한 모든 논리를 포함하는 Core 프로젝트
* **AwesomeLibrary.CSharp** - C#에서 사용하기 위한 공용 API가 포함된 프로젝트
* **AwesomeLibrary.FSharp** - F#에서 사용하기 위한 공용 API가 포함된 프로젝트

터미널에서 다음 명령을 실행하면 이 가이드와 동일한 구조를 생성할 수 있습니다.

```console
mkdir AwesomeLibrary && cd AwesomeLibrary
dotnet new sln
mkdir AwesomeLibrary.Core && cd AwesomeLibrary.Core && dotnet new classlib
cd ..
mkdir AwesomeLibrary.CSharp && cd AwesomeLibrary.CSharp && dotnet new classlib
cd ..
mkdir AwesomeLibrary.FSharp && cd AwesomeLibrary.FSharp && dotnet new classlib -lang F#
cd ..
dotnet sln add AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
dotnet sln add AwesomeLibrary.CSharp/AwesomeLibrary.CSharp.csproj
dotnet sln add AwesomeLibrary.FSharp/AwesomeLibrary.FSharp.fsproj
```

그러면 위의 세 가지 프로젝트와 프로젝트를 함께 연결하는 솔루션 파일 하나가 추가됩니다. 솔루션 파일을 만들고 프로젝트를 연결하면 최상위 수준에서 프로젝트를 복원하고 빌드할 수 있습니다.

### <a name="project-to-project-referencing"></a>프로젝트 간 참조

프로젝트를 참조하는 가장 좋은 방법은 .NET Core CLI를 사용하여 프로젝트 참조를 추가하는 것입니다. **AwesomeLibrary.CSharp** 및 **AwesomeLibrary.FSharp** 프로젝트 디렉터리에서 다음 명령을 실행할 수 있습니다.

```dotnetcli
dotnet add reference ../AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
```

이제 **AwesomeLibrary.CSharp** 및 **AwesomeLibrary.FSharp** 둘 다의 프로젝트 파일에서 **AwesomeLibrary.Core**를 `ProjectReference` 대상으로 참조합니다.  프로젝트 파일을 검사하고 파일에서 다음을 통해 이를 확인할 수 있습니다.

```xml
<ItemGroup>
  <ProjectReference Include="..\AwesomeLibrary.Core\AwesomeLibrary.Core.csproj" />
</ItemGroup>
```

.NET Core CLI를 사용하지 않으려는 경우 이 섹션을 각 프로젝트 파일에 수동으로 추가할 수 있습니다.

### <a name="structuring-a-solution"></a>솔루션 구성

다중 프로젝트 솔루션의 또 다른 중요한 측면은 전체 프로젝트 구조를 올바르게 설정하는 것입니다. 코드를 원하는 대로 구성할 수 있으며, `dotnet sln add`를 사용하여 각 프로젝트를 솔루션 파일에 연결하기만 하면 솔루션 수준에서 `dotnet restore` 및 `dotnet build`를 실행할 수 있습니다.
