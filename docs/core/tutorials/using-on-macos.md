---
title: '자습서: Visual Studio Code를 사용하여 macOS에서 .NET Core 솔루션 만들기'
description: 이 문서에서는 Visual Studio Code를 사용하여 .NET Core 솔루션을 만드는 단계와 워크플로를 제공합니다.
ms.date: 03/23/2017
ms.custom: seodec18
ms.openlocfilehash: 5df43ae235b9fd901a65f7f8898bec67e24de682
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117363"
---
# <a name="tutorial-create-a-net-core-solution-in-macos-using-visual-studio-code"></a>자습서: Visual Studio Code를 사용하여 macOS에서 .NET Core 솔루션 만들기

이 문서에서는 macOS용 .NET Core 솔루션을 만드는 단계와 워크플로를 제공합니다. 프로젝트 및 단위 테스트를 만들고, 디버깅 도구를 사용하고, [NuGet](https://www.nuget.org/)을 통해 타사 라이브러리를 통합하는 방법을 알아봅니다.

> [!NOTE]
> 이 문서에서는 macOS의 [Visual Studio Code](https://code.visualstudio.com)를 사용합니다.

## <a name="prerequisites"></a>전제 조건

[.NET Core SDK](https://dotnet.microsoft.com/download)를 설치합니다. .NET Core SDK에는 최신 버전의 .NET Core 프레임워크 및 런타임이 포함되어 있습니다.

[Visual Studio Code](https://code.visualstudio.com)를 설치합니다. 이 문서를 진행하면서 .NET Core 개발자 환경을 개선하는 Visual Studio Code 확장도 설치하게 됩니다.

Visual Studio Code 팔레트를 열려면 Visual Studio Code를 열고 <kbd>F1</kbd> 키를 눌러 Visual Studio Code C# 확장을 설치합니다. **ext install**을 입력하여 확장 목록을 표시합니다. C# 확장을 선택합니다. Visual Studio Code를 다시 시작하여 확장을 활성화합니다. 자세한 내용은 [Visual Studio Code C# 확장 문서](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md)를 참조하세요.

## <a name="get-started"></a>시작

이 자습서에서는 라이브러리 프로젝트, 해당 라이브러리 프로젝트에 대한 테스트, 라이브러리를 사용하는 콘솔 애플리케이션 등 프로젝트 3개를 만듭니다. GitHub의 dotnet/samples 리포지토리에서 이 항목에 대한 [소스를 보거나 다운로드](https://github.com/dotnet/samples/tree/master/core/getting-started/golden)할 수 있습니다. 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

Visual Studio Code를 시작합니다. <kbd>Ctrl</kbd>+<kbd>\`</kbd> 키(역따옴표 또는 억음 문자)를 누르거나 메뉴에서 **보기 > 통합 터미널**을 선택하여 Visual Studio Code에서 포함된 터미널을 엽니다. Visual Studio Code 외부에서 작업하려는 경우 탐색기 **명령 프롬프트에서 열기** 명령(Mac 또는 Linux에서는 **터미널에서 열기**)을 사용하여 외부 셸을 열 수 있습니다.

하나 이상의 .NET Core 프로젝트에 대한 컨테이너로 사용되는 솔루션 파일을 먼저 만듭니다. 터미널에서 [`dotnet new`](../tools/dotnet-new.md) 명령을 실행하여 *golden*이라는 새 폴더에 새 솔루션 *golden.sln*을 만듭니다.

```dotnetcli
dotnet new sln -o golden
```

새 *golden* 폴더로 이동하고 다음 명령을 실행하여 *library* 폴더에 두 파일 *library.csproj* 및 *Class1.cs*를 생성하는 라이브러리 프로젝트를 만듭니다.

```dotnetcli
dotnet new classlib -o library
```

[`dotnet sln`](../tools/dotnet-sln.md) 명령을 실행하여 새로 만든 *library.csproj* 프로젝트를 솔루션에 추가합니다.

```dotnetcli
dotnet sln add library/library.csproj
```

*library.csproj* 파일에는 다음 정보가 들어 있습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
  </PropertyGroup>

</Project>
```

라이브러리 메서드는 JSON 형식으로 개체를 직렬화 및 deserialize합니다. JSON serialization 및 deserialization을 지원하려면 `Newtonsoft.Json` NuGet 패키지에 대한 참조를 추가합니다. `dotnet add` 명령은 프로젝트에 새 항목을 추가합니다. NuGet 패키지에 대한 참조를 추가하려면 [`dotnet add package`](../tools/dotnet-add-package.md) 명령을 사용하고 패키지 이름을 지정합니다.

```dotnetcli
dotnet add library package Newtonsoft.Json
```

그러면 `Newtonsoft.Json` 및 해당 종속성이 라이브러리 프로젝트에 추가됩니다. 또는 *library.csproj* 파일을 수동으로 편집하고 다음 노드를 추가합니다.

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="12.0.2" />
</ItemGroup>
```

종속성을 복원하고 *library* 내에 *obj* 폴더를 만드는 [`dotnet restore`](../tools/dotnet-restore.md)([참고 참조](#dotnet-restore-note))를 실행합니다. 이 폴더 안에는 *project.assets.json* 파일을 비롯한 세 개의 파일이 들어 있습니다.

```dotnetcli
dotnet restore
```

*library* 폴더에서 *Class1.cs* 파일의 이름을 *Thing.cs*로 바꿉니다. 코드를 다음으로 바꿉니다.

```csharp
using static Newtonsoft.Json.JsonConvert;

namespace Library
{
    public class Thing
    {
        public int Get(int left, int right) =>
            DeserializeObject<int>($"{left + right}");
    }
}
```

`Thing` 클래스에는 공용 메서드 `Get`이 포함되어 있습니다. 이 메서드는 두 숫자의 합계를 반환하지만, 이 작업을 위해 합계를 문자열로 변환한 다음 정수로 deserialize합니다. 여기에는 [`using static` 지시문](../../csharp/language-reference/keywords/using-static.md), [식 본문 멤버](../../csharp/whats-new/csharp-7.md#more-expression-bodied-members), [문자열 보간](../../csharp/language-reference/tokens/interpolated.md) 등 많은 최신 C# 기능이 사용됩니다.

[`dotnet build`](../tools/dotnet-build.md) 명령을 사용하여 라이브러리를 빌드합니다. 그러면 *golden/library/bin/Debug/netstandard1.4* 아래에 *library.dll* 파일이 생성됩니다.

```dotnetcli
dotnet build
```

## <a name="create-the-test-project"></a>테스트 프로젝트 만들기

라이브러리에 대한 테스트 프로젝트를 빌드합니다. *golden* 폴더에서 새 테스트 프로젝트를 만듭니다.

```dotnetcli
dotnet new xunit -o test-library
```

테스트 프로젝트를 솔루션에 추가합니다.

```dotnetcli
dotnet sln add test-library/test-library.csproj
```

컴파일러가 라이브러리 프로젝트를 찾아서 사용할 수 있도록 이전 섹션에서 만든 라이브러리에 대한 프로젝트 참조를 추가합니다. [`dotnet add reference`](../tools/dotnet-add-reference.md) 명령을 사용합니다.

```dotnetcli
dotnet add test-library/test-library.csproj reference library/library.csproj
```

또는 *test-library.csproj* 파일을 수동으로 편집하고 다음 노드를 추가합니다.

```xml
<ItemGroup>
  <ProjectReference Include="..\library\library.csproj" />
</ItemGroup>
```

이제 종속성이 제대로 구성되었으므로 라이브러리에 대한 테스트를 만들어 보겠습니다. *UnitTest1.cs*를 열고 내용을 다음 코드로 바꿉니다.

```csharp
using Library;
using Xunit;

namespace TestApp
{
    public class LibraryTests
    {
        [Fact]
        public void TestThing() {
            Assert.NotEqual(42, new Thing().Get(19, 23));
        }
    }
}
```

단위 테스트를 처음 만들 때는 값 42가 19+23(또는 42)과 같지 않다고 어설션하며(`Assert.NotEqual`) 이는 실패하게 됩니다. 단위 테스트 빌드 시 중요한 단계는 테스트 논리를 확인하기 위해 처음에 한 번 실패하는 테스트를 만드는 것입니다.

*golden* 폴더에서 다음 명령을 실행합니다.

```dotnetcli
dotnet restore 
dotnet test test-library/test-library.csproj
```

이러한 명령은 모든 프로젝트를 재귀적으로 찾아 종속성을 복원하고 빌드한 다음 xUnit Test Runner를 활성화하여 테스트를 실행합니다. 예상대로 단일 테스트가 실패합니다.

*UnitTest1.cs* 파일을 편집하고 어설션을 `Assert.NotEqual`에서 `Assert.Equal`로 변경합니다. *golden* 폴더에서 다음 명령을 실행하여 테스트를 다시 실행합니다. 이번에는 테스트를 통과합니다.

```dotnetcli
dotnet test test-library/test-library.csproj
```

## <a name="create-the-console-app"></a>콘솔 앱 만들기

다음 단계에 따라 만든 콘솔 앱은 이전에 만든 라이브러리 프로젝트에 대한 종속성을 가지며, 실행 시 해당 라이브러리 메서드를 호출합니다. 이 개발 패턴을 사용하면 여러 프로젝트에 재사용 가능한 라이브러리를 만드는 방법을 확인할 수 있습니다.

*golden* 폴더에서 새 콘솔 애플리케이션을 만듭니다.

```dotnetcli
dotnet new console -o app
```

콘솔 앱 프로젝트를 솔루션에 추가합니다.

```dotnetcli
dotnet sln add app/app.csproj
```

`dotnet add reference` 명령을 실행하여 라이브러리에 대한 종속성을 만듭니다.

```dotnetcli
dotnet add app/app.csproj reference library/library.csproj
```

`dotnet restore`([참고 참조](#dotnet-restore-note))를 실행하여 솔루션에 있는 세 프로젝트의 종속성을 복원합니다. *Program.cs*를 열고 `Main` 메서드의 내용을 다음 줄로 바꿉니다.

```csharp
WriteLine($"The answer is {new Thing().Get(19, 23)}");
```

*Program.cs* 파일의 맨 위에 두 개의 `using` 지시문을 추가합니다.

```csharp
using static System.Console;
using Library;
```

다음 `dotnet run` 명령을 실행하여 실행 파일을 실행합니다. 여기서 `dotnet run`에 대한 `-p` 옵션은 주 애플리케이션에 대한 프로젝트를 지정합니다. 앱이 "The answer is 42" 문자열을 생성합니다.

```dotnetcli
dotnet run -p app/app.csproj
```

## <a name="debug-the-application"></a>애플리케이션 디버그

`Main` 메서드의 `WriteLine` 문에 중단점을 설정합니다. 이렇게 하려면 `WriteLine` 줄에 커서를 놓고 <kbd>F9</kbd> 키를 누르거나 중단점을 설정할 줄의 왼쪽 여백에서 마우스를 클릭합니다. 코드 줄 옆의 여백에 빨간색 원이 나타납니다. 중단점에 도달하면 중단점 줄이 실행되기 *전에* 코드 실행이 중지됩니다.

Visual Studio Code 도구 모음에서 디버그 아이콘을 선택하거나, 메뉴 모음에서 **보기 > 디버그**를 선택하거나, 바로 가기 키 <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>D</kbd>를 사용하여 디버거 탭을 엽니다.

![Visual Studio Code 디버거](./media/using-on-macos/visual-studio-code-debugger.png)

디버거에서 애플리케이션을 시작하려면 재생 단추를 누릅니다. 앱이 실행을 시작하고 중단점까지 실행되며, 여기서 중단됩니다. `Get` 메서드를 단계별로 실행하며 올바른 인수를 전달했는지 확인합니다. 응답이 42인지 확인합니다.

<a name="dotnet-restore-note"></a>
[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]
