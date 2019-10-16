---
title: CLI를 사용하여 .NET Core 시작
description: .NET Core CLI(명령줄 인터페이스)를 사용하여 Windows, Linux 또는 macOS에서 .NET Core를 시작하는 방법을 보여 주는 단계별 자습서입니다.
author: thraka
ms.author: adegeo
ms.date: 08/07/2019
ms.technology: dotnet-cli
ms.custom: seodec18
ms.openlocfilehash: b5ef70967c8404dc5ce5b816bb9a1c3b1d7e4230
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117357"
---
# <a name="get-started-with-net-core-on-windowslinuxmacos-using-the-command-line"></a>명령줄을 사용하여 Windows/Linux/macOS에서 .NET Core 시작

이 항목에서는 .NET Core CLI 도구를 사용하여 컴퓨터에서 플랫폼 간 앱 개발을 시작하는 방법을 보여 줍니다.

.NET Core CLI 도구 집합에 익숙하지 않은 경우 [.NET Core SDK 개요](../tools/index.md)를 읽어 보세요.

## <a name="prerequisites"></a>전제 조건

- [.NET Core SDK 2.1](https://dotnet.microsoft.com/download) 이상 버전.
- 선택하는 텍스트 편집기 또는 코드 편집기입니다.

## <a name="hello-console-app"></a>Hello, 콘솔 앱!

GitHub의 dotnet/samples 리포지토리에서 [샘플 코드를 보거나 다운로드](https://github.com/dotnet/samples/tree/master/core/console-apps/HelloMsBuild)할 수 있습니다. 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

명령 프롬프트를 열고 *Hello*라는 폴더를 만듭니다. 만든 폴더로 이동하고 다음을 입력합니다.

```dotnetcli
dotnet new console
dotnet run
```

이제 간단한 연습을 해보겠습니다.

1. `dotnet new console`

   [`dotnet new`](../tools/dotnet-new.md)는 콘솔 앱을 빌드하는 데 필요한 종속성이 있는 최신 `Hello.csproj` 프로젝트 파일입니다.  애플리케이션에 대한 진입점을 포함하는 기본 파일인 `Program.cs`도 만듭니다.

   `Hello.csproj`:

   [!code[Hello.csproj](../../../samples/core/console-apps/HelloMsBuild/Hello.csproj)]

   프로젝트 파일은 종속성을 복원하고 프로그램을 빌드하는 데 필요한 모든 항목을 지정합니다.

   - `OutputType` 태그에서는 실행 파일, 즉 콘솔 애플리케이션을 빌드하고 있음을 지정합니다.
   - `TargetFramework` 태그에서는 대상으로 하는 .NET 구현을 지정합니다. 고급 시나리오에서는 여러 대상 프레임워크를 지정하고 이 모든 프레임워크를 단일 작업으로 빌드할 수 있습니다. 이 자습서에서는 .NET Core 2.1에 대해서만 빌드합니다.

   `Program.cs`:

   [!code-csharp[Program.cs](../../../samples/core/console-apps/HelloMsBuild/Program.cs)]

   프로그램은 `using System`으로 시작됩니다. 즉, "`System` 네임스페이스의 모든 항목을 이 파일 범위로 가져옵니다". `System` 네임스페이스에는 `string` 또는 숫자 형식과 같은 기본 구문이 포함되어 있습니다.

   그런 다음 `Hello`라는 네임스페이스를 정의합니다. 이 이름은 원하는 값으로 변경할 수 있습니다. `Program`이라는 클래스는 해당 네임스페이스 내에서 인수로 문자열 배열을 사용하는 `Main` 메서드로 정의됩니다. 이 배열에는 컴파일된 프로그램을 호출할 때 전달된 인수 목록이 포함되어 있습니다. 이 배열은 그대로 사용되지 않습니다. 프로그램은 모두 "Hello World!"를 작성합니다. 표시합니다. 나중에 이 인수를 사용하는 코드를 변경할 예정입니다.

   [!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

   `dotnet new`는 [`dotnet restore`](../tools/dotnet-restore.md)를 암시적으로 호출합니다. `dotnet restore`는 [NuGet](https://www.nuget.org/)(.NET 패키지 관리자)을 호출하여 종속성 트리를 복원합니다. NuGet은 *Hello.csproj* 파일을 분석하고, 파일에 정의된 종속성을 다운로드하고(또는 머신의 캐시에서 종속성을 가져오고), 샘플을 컴파일 및 실행하는 데 필요한 *obj/project.assets.json* 파일을 작성합니다.

   > [!IMPORTANT]
   > SDK의 .NET Core 1.x 버전을 사용하는 경우 `dotnet new`를 호출한 후 `dotnet restore`를 직접 호출해야 합니다.

2. `dotnet run`

   [`dotnet run`](../tools/dotnet-run.md)은 [`dotnet build`](../tools/dotnet-build.md)를 호출하여 빌드 대상이 빌드되었는지를 확인하고 `dotnet <assembly.dll>`을 호출하여 대상 애플리케이션을 실행합니다.

    ```console
    $ dotnet run
    Hello World!
    ```

    또한 [`dotnet build`](../tools/dotnet-build.md)를 실행하여 빌드 콘솔 애플리케이션을 실행하지 않고 코드를 컴파일할 수도 있습니다. 이로 인해 Windows에서는 `dotnet bin\Debug\netcoreapp2.1\Hello.dll`로, 다른 시스템에서는 `/`로 실행할 수 있는 컴파일된 애플리케이션이 DLL 파일로 만들어집니다. 이 항목의 뒷부분에서 살펴보겠지만, 애플리케이션에 인수를 지정할 수도 있습니다.

    ```console
    $ dotnet bin\Debug\netcoreapp2.1\Hello.dll
    Hello World!
    ```

    고급 시나리오에서는 .NET Core를 설치하지 않아도 되는 컴퓨터에 배포하고 실행할 수 있는 자체 포함된 플랫폼별 파일로 애플리케이션을 빌드할 수 있습니다. 자세한 내용은 [.NET Core 애플리케이션 배포](../deploying/index.md)를 참조하세요.

### <a name="augmenting-the-program"></a>프로그램 보강

프로그램을 조금 변경해 봅시다. 피보나치 숫자가 흥미로우므로, 인수 사용과 함께 피보나치 숫자를 추가하여 앱을 실행하는 사람을 맞이해 봅시다.

1. *Program.cs* 파일의 내용을 다음 코드로 바꿉니다.

   [!code-csharp[Fibonacci](../../../samples/core/console-apps/fibonacci-msbuild/Program.cs)]

2. [ `dotnet build` ](../tools/dotnet-build.md)를 실행하여 변경 내용을 컴파일합니다.

3. 앱에 매개 변수를 전달하는 프로그램을 실행합니다.

   ```console
   $ dotnet run -- John
   Hello John!
   Fibonacci Numbers 1-15:
   1: 0
   2: 1
   3: 1
   4: 2
   5: 3
   6: 5
   7: 8
   8: 13
   9: 21
   10: 34
   11: 55
   12: 89
   13: 144
   14: 233
   15: 377
   ```

됐습니다!  원하는 대로 `Program.cs`를 보강할 수 있습니다.

## <a name="working-with-multiple-files"></a>여러 파일 작업

단일 파일은 간단한 일회용 프로그램에 적합하지만 더 복잡한 앱을 빌드하는 경우 프로젝트에 여러 소스 파일이 있을 수 있습니다.
일부 피보나치 값을 캐시하여 이전 피보나치 예제에서 빌드하고 몇몇 재귀 기능을 추가해보겠습니다.

1. 다음 코드를 사용하여 *Hello* 디렉터리 내에 *FibonacciGenerator.cs*라는 새 파일을 추가합니다.

   [!code-csharp[Fibonacci Generator](../../../samples/core/console-apps/FibonacciBetterMsBuild/FibonacciGenerator.cs)]

2. 다음 예제에서처럼 *Program.cs* 파일의 `Main` 메서드를 변경하여 새 클래스를 인스턴스화하고 메서드를 호출합니다.

   [!code-csharp[New Program.cs](../../../samples/core/console-apps/FibonacciBetterMsBuild/Program.cs)]

3. [ `dotnet build` ](../tools/dotnet-build.md)를 실행하여 변경 내용을 컴파일합니다.

4. [`dotnet run`](../tools/dotnet-run.md)을 실행하여 앱을 실행합니다. 다음은 프로그램 출력을 보여 줍니다.

   ```console
   $ dotnet run
   0
   1
   1
   2
   3
   5
   8
   13
   21
   34
   55
   89
   144
   233
   377
   ```

## <a name="publish-your-app"></a>앱 게시

앱을 배포할 준비가 되면 [`dotnet publish`](../tools/dotnet-publish.md) 명령을 사용하여 _bin\\debug\\netcoreapp2.1\\publish\\_ 에 _publish_ 폴더를 생성합니다(비 Windows 시스템의 경우 `/` 사용). 이미 dotnet 런타임을 설치한 경우에 _publish_ 폴더의 콘텐츠를 다른 플랫폼에 배포할 수 있습니다.

[dotnet](../tools/dotnet.md) 명령으로 게시된 앱을 실행할 수 있습니다.

```console
$ dotnet bin\Debug\netcoreapp2.1\publish\Hello.dll
Hello World!
```

## <a name="conclusion"></a>결론

됐습니다! 이제 여기에서 배운 기본 개념을 활용하여 고유의 프로그램을 만들 수 있습니다.

## <a name="see-also"></a>참고 항목

- [.NET Core CLI 도구를 사용하여 프로젝트 구성 및 테스트](testing-with-cli.md)
- [CLI를 사용하여 .NET Core 앱 게시](../deploying/deploy-with-cli.md)
- [앱 배포에 대한 자세한 정보](../deploying/index.md)
