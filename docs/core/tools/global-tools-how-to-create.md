---
title: .NET Core 전역 도구를 만드는 방법
description: 전역 도구를 만드는 방법을 설명합니다. 전역 도구는 .NET Core CLI를 통해 설치되는 콘솔 애플리케이션입니다.
author: Thraka
ms.author: adegeo
ms.date: 08/22/2018
ms.openlocfilehash: 5c2b1e459f0308f5f96eb041c10f4d7a7ae0ca20
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117449"
---
# <a name="create-a-net-core-global-tool-using-the-net-core-cli"></a>.NET Core CLI를 사용하여 .NET Core 전역 도구 만들기

이 문서에서는 .NET Core 전역 도구를 만들고 패키지하는 방법을 설명합니다. .NET Core CLI를 사용하면 콘솔 애플리케이션을 다른 사용자가 쉽게 설치하고 실행할 수 있는 전역 도구로 만들 수 있습니다. .NET Core 전역 도구는 .NET Core CLI에서 설치되는 NuGet 패키지입니다. Global Tools에 대한 자세한 내용은 [.NET Core Global Tools 개요](global-tools.md)를 참조하세요.

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="create-a-project"></a>프로젝트 만들기

이 문서에서는 .NET Core CLI를 사용하여 프로젝트를 만들고 관리합니다.

예제 도구는 ASCII 봇을 생성하고 메시지를 인쇄하는 콘솔 애플리케이션입니다. 먼저 새 .NET Core 콘솔 애플리케이션을 만듭니다.

```dotnetcli
dotnet new console -o botsay
```

이전 명령에서 생성된 `botsay` 디렉터리로 이동합니다.

## <a name="add-the-code"></a>코드 추가

`vim` 또는 [Visual Studio Code](https://code.visualstudio.com/)와 같은 원하는 텍스트 편집기를 사용하여 `Program.cs` 파일을 엽니다.

다음 `using` 지시문을 파일 맨 위에 추가하면 애플리케이션의 버전 정보를 표시하는 코드를 줄일 수 있습니다.

```csharp
using System.Reflection;
```

그런 다음, `Main` 메서드까지 아래로 이동합니다. 메서드를 다음 코드로 바꿔 애플리케이션의 명령줄 인수를 처리합니다. 인수가 전달되지 않으면 짧은 도움말 메시지가 표시됩니다. 인수가 전달되면 모든 해당 인수가 문자열로 변환되고 봇을 통해 인쇄됩니다.

```csharp
static void Main(string[] args)
{
    if (args.Length == 0)
    {
        var versionString = Assembly.GetEntryAssembly()
                                .GetCustomAttribute<AssemblyInformationalVersionAttribute>()
                                .InformationalVersion
                                .ToString();

        Console.WriteLine($"botsay v{versionString}");
        Console.WriteLine("-------------");
        Console.WriteLine("\nUsage:");
        Console.WriteLine("  botsay <message>");
        return;
    }

    ShowBot(string.Join(' ', args));
}
```

### <a name="create-the-bot"></a>봇 만들기

그런 다음, 문자열 매개 변수를 사용하는 `ShowBot`이라는 새 메서드를 추가합니다. 이 메서드는 메시지 및 ASCII 봇을 인쇄합니다. ASCII 봇 코드는 [dotnetbot](https://github.com/dotnet/core/blob/master/samples/dotnetsay/Program.cs) 샘플에서 가져왔습니다.

```csharp
static void ShowBot(string message)
{
    string bot = $"\n        {message}";
    bot += @"
    __________________
                      \
                       \
                          ....
                          ....'
                           ....
                        ..........
                    .............'..'..
                 ................'..'.....
               .......'..........'..'..'....
              ........'..........'..'..'.....
             .'....'..'..........'..'.......'.
             .'..................'...   ......
             .  ......'.........         .....
             .    _            __        ......
            ..    #            ##        ......
           ....       .                 .......
           ......  .......          ............
            ................  ......................
            ........................'................
           ......................'..'......    .......
        .........................'..'.....       .......
     ........    ..'.............'..'....      ..........
   ..'..'...      ...............'.......      ..........
  ...'......     ...... ..........  ......         .......
 ...........   .......              ........        ......
.......        '...'.'.              '.'.'.'         ....
.......       .....'..               ..'.....
   ..       ..........               ..'........
          ............               ..............
         .............               '..............
        ...........'..              .'.'............
       ...............              .'.'.............
      .............'..               ..'..'...........
      ...............                 .'..............
       .........                        ..............
        .....
";
    Console.WriteLine(bot);
}
```

### <a name="test-the-tool"></a>도구 테스트

프로젝트를 실행하고 출력을 확인합니다. 다른 결과를 보려면 명령줄에서 다음 변형을 시도해 보세요.

```dotnetcli
dotnet run
dotnet run -- "Hello from the bot"
dotnet run -- hello from the bot
```

`--` 구분 기호 뒤의 모든 인수가 애플리케이션에 전달됩니다.

## <a name="setup-the-global-tool"></a>전역 도구 설정

애플리케이션을 패키지하고 전역 도구로 배포하려면 먼저 프로젝트 파일을 수정해야 합니다. `botsay.csproj` 파일을 열고 다음 세 개의 새 XML 노드를 `<Project><PropertyGroup>` 노드에 추가합니다.

- `<PackAsTool>`\
[필수] 애플리케이션이 전역 도구로 설치하도록 패키지됨을 나타냅니다.

- `<ToolCommandName>`\
[선택 사항] 도구의 대체 이름입니다. 그렇지 않으면 도구의 명령 이름이 프로젝트 파일 이름 뒤에 추가됩니다. 패키지에 여러 도구를 포함할 수 있고, 고유하고 친숙한 이름을 선택하면 동일 패키지의 다른 도구와 구별하는 데 도움이 됩니다.

- `<PackageOutputPath>`\
[선택 사항] NuGet 패키지가 생성될 위치입니다. NuGet 패키지는 .NET Core CLI 전역 도구가 도구를 설치하는 데 사용됩니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>

    <PackAsTool>true</PackAsTool>
    <ToolCommandName>botsay</ToolCommandName>
    <PackageOutputPath>./nupkg</PackageOutputPath>

  </PropertyGroup>

</Project>
```

`<PackageOutputPath>`는 선택 사항이지만 이 예제에서는 이 항목을 사용합니다. `<PackageOutputPath>./nupkg</PackageOutputPath>`를 설정했는지 확인합니다.

그런 다음, 애플리케이션용 NuGet 패키지를 만듭니다.

```dotnetcli
dotnet pack
```

`botsay.1.0.0.nupkg` 파일은 `botsay.csproj` 파일의 `<PackageOutputPath>` XML 값으로 식별되는 폴더에 생성됩니다(이 예제에서는 `./nupkg` 폴더). 이를 사용하여 쉽게 설치 및 테스트할 수 있습니다. 공개적으로 도구를 릴리스하려면 <https://www.nuget.org>에 업로드합니다. NuGet에서 도구를 사용할 수 있게 되면 개발자는 [dotnet tool install](dotnet-tool-install.md) 명령의 `--global` 옵션을 사용하여 사용자 수준의 도구 설치를 수행할 수 있습니다.

이제 패키지가 있으므로 해당 패키지에서 도구를 설치합니다.

```dotnetcli
dotnet tool install --global --add-source ./nupkg botsay
```

`--add-source` 매개 변수는 NuGet 패키지의 추가 소스 피드로 `./nupkg` 폴더(여기서는 `<PackageOutputPath>` 폴더)를 임시로 사용하도록 .NET Core CLI에 지시합니다. Global Tools를 설치하는 방법에 대한 자세한 내용은 [.NET Core Global Tools 개요](global-tools.md)를 참조하세요.

설치에 성공하면 다음 예와 같이 도구와 설치된 버전을 호출하는 데 사용되는 명령을 보여 주는 메시지가 표시됩니다.

```output
You can invoke the tool using the following command: botsay
Tool 'botsay' (version '1.0.0') was successfully installed.
```

이제 `botsay`를 입력하고 도구에서 응답을 가져올 수 있습니다.

> [!NOTE]
> 설치에 성공했지만 `botsay` 명령을 사용할 수 없는 경우에는 새 터미널을 열고 PATH를 새로 고쳐야 할 수 있습니다.

## <a name="remove-the-tool"></a>도구 제거

도구를 사용한 실험을 완료하면 다음 명령을 사용하여 도구를 제거할 수 있습니다.

```dotnetcli
dotnet tool uninstall -g botsay
```
