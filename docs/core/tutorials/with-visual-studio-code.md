---
title: C# 및 Visual Studio Code 시작
description: Visual Studio Code를 사용하여 C#에서 첫 번째 .NET Core 애플리케이션을 만들고 디버그하는 방법을 알아봅니다.
author: kendrahavens
ms.date: 12/05/2018
ms.custom: seodec18
ms.openlocfilehash: 4e283f631f463953185a37bf196a1a9b706eee2b
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002329"
---
# <a name="get-started-with-c-and-visual-studio-code"></a>C# 및 Visual Studio Code 시작

.NET Core는 Windows, Linux 및 macOS에서 실행되는 애플리케이션을 만들기 위한 빠른 모듈식 플랫폼을 제공합니다. C# 확장이 있는 Visual Studio Code를 사용하면 C# IntelliSense(스마트 코드 완성) 및 디버깅을 완벽하게 지원하는 강력한 편집 환경이 구현됩니다.

## <a name="prerequisites"></a>전제 조건

1. [Visual Studio Code](https://code.visualstudio.com/)를 설치합니다.
2. [.NET Core SDK](https://dotnet.microsoft.com/download)를 설치합니다.
3. Visual Studio Code의 [C# 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)을 설치합니다. Visual Studio Code의 확장을 설치하는 방법에 대한 자세한 내용은 [VS Code Extension Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery)(VS Code 확장 마켓플레이스)를 참조하세요.

## <a name="hello-world"></a>Hello World

.NET Core에서 간단한 "Hello World" 프로그램으로 시작해 보겠습니다.

1. 프로젝트 열기

    - Visual Studio Code를 엽니다.
    - 왼쪽 메뉴에 있는 탐색기 아이콘을 클릭한 다음 **폴더 열기**를 클릭합니다.
    - 주 메뉴에서 **파일** > **폴더 열기**를 선택하여 C# 프로젝트를 저장하려는 폴더를 열고 **폴더 선택**을 클릭합니다. 이 예제에서는 *HelloWorld*라는 프로젝트에 대한 폴더를 만들어 봅니다.

      ![Visual Studio Code 폴더 열기](media/with-visual-studio-code/vs-code-open-folder.png)

2. C# 프로젝트 초기화

    - 주 메뉴에서 **보기** > **통합 터미널**을 선택하여 Visual Studio Code에서 통합 터미널을 엽니다.
    - 터미널 창에서 `dotnet new console`을 입력합니다.
    - 이 명령은 폴더에 이미 작성된 간단한 “헬로 월드” 프로그램이 있는 *Program.cs* 파일을 만들고 *HelloWorld.csproj*라는 C# 프로젝트 파일을 만듭니다.

      ![dotnet new 명령](media/with-visual-studio-code/dotnet-new-command.png)

3. 빌드 자산 확인

    - **.NET Core 1.x**의 경우 `dotnet restore`를 입력합니다. `dotnet restore`를 실행하면 프로젝트를 빌드하는 데 필요한 필수 .NET Core 패키지에 액세스할 수 있습니다.

      ![dotnet restore 명령](media/with-visual-studio-code/dotnet-restore-command.png)

      [!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

4. "Hello World" 프로그램 실행

    - `dotnet run`을 입력합니다.

      ![dotnet run 명령](media/with-visual-studio-code/dotnet-run-command.png)

[Windows](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core), [macOS](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core-on-MacOS) 또는 [Linux](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu)에 대한 추가 설치 도움말이 제공되는 짧은 비디오 자습서를 볼 수도 있습니다.

## <a name="debug"></a>디버그

1. *Program.cs*를 클릭하여 엽니다. Visual Studio Code에서 C# 파일을 처음 열면 [OmniSharp](https://www.omnisharp.net/)에서 편집기가 로드됩니다.

    ![Program.cs 파일 열기](media/with-visual-studio-code/open-program-cs.png)

2. Visual Studio Code에 앱을 빌드하고 디버그하기 위해 누락된 자산을 추가하라는 메시지가 표시됩니다. **예**를 선택합니다.

    ![누락된 자산에 대한 프롬프트](media/with-visual-studio-code/missing-assets.png)

3. 디버그 보기를 열려면 왼쪽 메뉴에서 디버깅 아이콘을 클릭합니다.

    ![Visual Studio Code에서 [디버그] 탭 열기](media/with-visual-studio-code/open-debug-tab.png)

4. 창 위쪽에서 녹색 화살표를 찾습니다. 옆에 있는 드롭다운 목록에서 **.NET Core Launch(콘솔)** 가 선택되어 있는지 확인합니다.

    ![Visual Studio Code에서.NET Core 선택](media/with-visual-studio-code/select-net-core.png)

5. 9번째 줄 옆에 있는 **편집기 여백**(편집기에서 줄 번호 왼쪽에 있는 공간)을 클릭하거나 편집기에서 9번째 줄로 이동하여 <kbd>F9</kbd>를 눌러서 프로젝트에 중단점을 추가합니다.

    ![중단점 설정](media/with-visual-studio-code/set-breakpoint-vs-code.png)

6. 디버깅을 시작하려면 <kbd>F5</kbd>를 누르거나 또는 녹색 화살표를 선택합니다. 이전 단계에서 설정한 중단점에 도달하면 디버거에서 프로그램 실행을 중지합니다.
    - 디버깅 동안 왼쪽 위에 있는 창에서 지역 변수를 보거나 디버그 콘솔을 사용할 수 있습니다.

7. 디버깅을 계속하려면 맨 위에 있는 파란색 화살표를 선택하고, 중지하려면 맨 위에 있는 빨간색 사각형을 선택합니다.

    ![Visual Studio Code에서 실행 및 디버그](media/with-visual-studio-code/run-debug-vs-code.png)

> [!TIP]
> Visual Studio Code에서 OmniSharp를 사용한 .NET Core 디버깅에 대한 자세한 내용과 문제 해결 정보는 [Instructions for setting up the .NET Core debugger](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md)(.NET Core 디버거 설정 지침)를 참조하세요.

## <a name="add-a-class"></a>클래스 추가

1. 새 클래스를 추가하려면 VSCode 탐색기에서 마우스 오른쪽 단추를 클릭하고 **새 파일**을 선택합니다. VSCode에서 열어 놓은 폴더에 새 파일이 추가됩니다.
2. 파일 이름을 *MyClass.cs*로 지정합니다. csharp 파일로 인식되도록 끝에 `.cs` 확장명을 추가해서 저장해야 합니다.
3. 아래 코드를 추가하여 첫 번째 클래스를 만듭니다. *Program.cs* 파일에서 참조할 수 있도록 올바른 네임스페이스를 포함해야 합니다.

    ``` csharp
    using System;

    namespace HelloWorld
    {
        public class MyClass
        {
            public string ReturnMessage()
            {
                return "Happy coding!";
            }
        }
    }
    ```

4. 아래 코드를 추가하여 *Program.cs*의 main 메서드에서 새 클래스를 호출합니다.

    ```csharp
    using System;
    
    namespace HelloWorld
    {
        class Program
        {
            static void Main(string[] args)
            {
                var c1 = new MyClass();
                Console.WriteLine($"Hello World! {c1.ReturnMessage()}");
            }
        }
    }
    ```

5. 변경 내용을 저장하고 프로그램을 다시 실행합니다. 추가된 문자열을 포함하는 새 메시지가 표시됩니다.

    ```console
    > dotnet run
    Hello World! Happy coding!
    ```

## <a name="faq"></a>FAQ

### <a name="im-missing-required-assets-to-build-and-debug-c-in-visual-studio-code-my-debugger-says-no-configuration"></a>Visual Studio Code에서 C#을 빌드하고 디버그하는 데 필요한 자산이 누락되었습니다. 내 디버거에서 "구성 없음"이라고 표시됩니다.

Visual Studio Code C# 확장에서 빌드 및 디버그할 자산을 생성할 수 있습니다. C# 프로젝트를 처음 열면 Visual Studio Code에 이러한 자산을 생성하라는 메시지가 표시됩니다. 자산을 생성하지 않은 경우 명령 팔레트(**보기 > 명령 팔레트**)를 열고 ">.NET: Generate Assets Build and Debug"를 입력하여 이 명령을 실행할 수 있습니다. 이를 선택하면 필요한 . *.vscode*, *launch.json* 및 *tasks.json* 구성 파일이 생성됩니다.

## <a name="see-also"></a>참고 항목

- [Visual Studio Code 설치](https://code.visualstudio.com/docs/setup/setup-overview)
- [Visual Studio Code의 디버깅](https://code.visualstudio.com/Docs/editor/debugging)
