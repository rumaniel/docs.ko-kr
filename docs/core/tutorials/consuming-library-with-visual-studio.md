---
title: Visual Studio 2017에서 .NET Standard 라이브러리 사용
description: Visual Studio 2017을 사용하여 다른 클래스 라이브러리의 멤버를 호출하는 .NET Core 애플리케이션을 빌드합니다.
author: BillWagner
ms.author: wiwagn
ms.date: 06/05/2018
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet, seodec18
ms.openlocfilehash: 31a9183f541afa5365862b1e89704354cf7bd527
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969305"
---
# <a name="consume-a-net-standard-library-in-visual-studio-2017"></a>Visual Studio 2017에서 .NET Standard 라이브러리 사용

[Visual Studio 2017에서 .NET Core를 사용하여 C# 클래스 라이브러리 빌드](./library-with-visual-studio.md) 또는 [Visual Studio 2017에서 .NET Core를 사용하여 Visual Basic 클래스 라이브러리 빌드](vb-library-with-visual-studio.md)의 단계를 따라 .NET Standard 클래스 라이브러리를 만들고, [Visual Studio 2017에서 .NET Core를 사용하여 클래스 라이브러리 테스트](testing-library-with-visual-studio.md)에서 테스트하고, 라이브러리의 릴리스 버전을 빌드한 후 다음 단계는 호출자가 사용할 수 있게 만드는 것입니다. 이 작업은

* 라이브러리가 단일 솔루션에 사용되는 경우(예: 단일 대형 애플리케이션의 구성 요소인 경우) 솔루션에 프로젝트로 포함할 수 있습니다.

* 라이브러리에 일반적으로 액세스할 수 있으면 NuGet 패키지로 배포할 수 있습니다.

## <a name="including-a-library-as-a-project-in-a-solution"></a>라이브러리를 솔루션에 프로젝트로 포함

클래스 라이브러리와 동일한 솔루션에 단위 테스트를 포함한 것처럼 애플리케이션을 해당 솔루션의 일부로 포함할 수 있습니다. 예를 들어 사용자가 문자열을 입력하도록 요구하고 첫 번째 문자가 대문자인지 여부를 보고하는 콘솔 애플리케이션에서 이 클래스 라이브러리를 사용할 수 있습니다.

<!-- markdownlint-disable MD025 -->

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

1. [Visual Studio 2017에서 .NET Core를 사용하여 C# 클래스 라이브러리 빌드](./library-with-visual-studio.md) 항목에서 만든 `ClassLibraryProjects` 솔루션을 엽니다. **솔루션 탐색기**에서 **ClassLibraryProjects** 솔루션을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가** > **새 프로젝트**를 선택합니다.

1. **새 프로젝트 추가** 대화 상자에서 **Visual C#** 노드를 확장하고 **.NET Core** 노드, **콘솔 앱(.NET Core)** 프로젝트 템플릿을 차례로 선택합니다. **이름** 텍스트 상자에 "ShowCase"를 입력하고 **확인** 단추를 선택합니다.

   ![Visual Studio 새 프로젝트 추가 대화 상자 - C#](./media/consuming-library-with-visual-studio/add-new-project-dialog.png)

1. **솔루션 탐색기**에서 **ShowCase** 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **시작 프로젝트로 설정**을 선택합니다.

   ![Visual Studio 프로젝트 상황에 맞는 메뉴로 시작 프로젝트 설정 - C#](./media/consuming-library-with-visual-studio/set-startup-project-context-menu.png)

1. 처음에는 프로젝트에서 클래스 라이브러리에 액세스할 수 없습니다. 클래스 라이브러리의 메서드를 호출할 수 있도록 허용하려면 클래스 라이브러리에 대한 참조를 만듭니다. **솔루션 탐색기**에서 `ShowCase` 프로젝트의 **종속성** 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 선택합니다.

   ![Visual Studio 프로젝트 참조 추가 상황에 맞는 메뉴 - C#](./media/consuming-library-with-visual-studio/add-reference-context-menu.png)

1. **참조 관리자** 대화 상자에서 **StringLibrary**, 해당 클래스 라이브러리 프로젝트를 차례로 선택한 다음 **확인** 단추를 선택합니다.

   ![Visual Studio 참조 관리 대화 상자 - C#](./media/consuming-library-with-visual-studio/manage-project-references.png)

1. *Program.cs* 파일의 코드 창에서 모든 코드를 다음 코드로 바꿉니다.

   [!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs)]

   코드는 `row` 변수를 사용하여 콘솔 창에 기록된 데이터 행 수를 유지합니다. 25보다 크거나 같으면 코드는 콘솔 창을 지우고 사용자에게 메시지를 표시합니다.

   프로그램에서 문자열을 입력하라는 메시지를 사용자에게 표시합니다. 문자열이 대문자로 시작하는지 여부를 나타냅니다. 사용자가 문자열을 입력하지 않고 Enter 키를 누르면 애플리케이션이 종료되고 콘솔 창이 닫힙니다.

1. 필요한 경우 도구 모음을 변경하여 컴파일하는 `ShowCase` 프로젝트의 **디버그** 릴리스를 컴파일합니다. **ShowCase** 단추에서 녹색 화살표를 선택하여 프로그램을 컴파일하고 실행합니다.

   ![Visual Studio 프로젝트 도구 모음 디버그 단추 표시 - C#](./media/consuming-library-with-visual-studio/visual-studio-project-toolbar.png)

# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

1. [Visual Studio 2017에서 Visual Basic 및 .NET Core를 사용하여 클래스 라이브러리 빌드](vb-library-with-visual-studio.md) 항목에서 만든 `ClassLibraryProjects` 솔루션을 엽니다. **솔루션 탐색기**에서 **ClassLibraryProjects** 솔루션을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가** > **새 프로젝트**를 선택합니다.

1. **새 프로젝트 추가** 대화 상자에서 **Visual Basic** 노드를 확장하고 **.NET Core** 노드, **콘솔 앱(.NET Core)** 프로젝트 템플릿을 차례로 선택합니다. **이름** 텍스트 상자에 "ShowCase"를 입력하고 **확인** 단추를 선택합니다.

   ![Visual Studio 새 프로젝트 추가 대화 상자 - Visual Basic](./media/consuming-library-with-visual-studio/add-new-vb-project-dialog.png)

1. **솔루션 탐색기**에서 **ShowCase** 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **시작 프로젝트로 설정**을 선택합니다. 

   ![Visual Studio 프로젝트 상황에 맞는 메뉴로 시작 프로젝트 설정 - Visual Basic](./media/consuming-library-with-visual-studio/set-startup-project-context-menu.png)

1. 처음에는 프로젝트에서 클래스 라이브러리에 액세스할 수 없습니다. 클래스 라이브러리의 메서드를 호출할 수 있도록 허용하려면 클래스 라이브러리에 대한 참조를 만듭니다. **솔루션 탐색기**에서 `ShowCase` 프로젝트의 **종속성** 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 선택합니다.

   ![Visual Studio 프로젝트 참조 추가 상황에 맞는 메뉴 - Visual Basic](./media/consuming-library-with-visual-studio/add-reference-context-menu.png)

1. **참조 관리자** 대화 상자에서 **StringLibrary**, 해당 클래스 라이브러리 프로젝트를 차례로 선택한 다음 **확인** 단추를 선택합니다.

   ![Visual Studio 참조 관리 대화 상자 - Visual Basic](./media/consuming-library-with-visual-studio/manage-project-references.png)

1. *Program.vb* 파일의 코드 창에서 모든 코드를 다음 코드로 바꿉니다.

    [!CODE-vb[UsingClassLib#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/showcase.vb)]

   코드는 `row` 변수를 사용하여 콘솔 창에 기록된 데이터 행 수를 유지합니다. 25보다 크거나 같으면 코드는 콘솔 창을 지우고 사용자에게 메시지를 표시합니다.

   프로그램에서 문자열을 입력하라는 메시지를 사용자에게 표시합니다. 문자열이 대문자로 시작하는지 여부를 나타냅니다. 사용자가 문자열을 입력하지 않고 Enter 키를 누르면 애플리케이션이 종료되고 콘솔 창이 닫힙니다.

1. 필요한 경우 도구 모음을 변경하여 컴파일하는 `ShowCase` 프로젝트의 **디버그** 릴리스를 컴파일합니다. **ShowCase** 단추에서 녹색 화살표를 선택하여 프로그램을 컴파일하고 실행합니다.

   ![도구 모음에서 디버그 - Visual Basic](./media/consuming-library-with-visual-studio/visual-studio-project-toolbar.png)

---

[Visual Studio 2017을 사용하여 Hello World 애플리케이션 디버그](debugging-with-visual-studio.md) 및 [Visual Studio 2017을 사용하여 Hello World 애플리케이션 게시](publishing-with-visual-studio.md)의 단계에 따라 이 라이브러리를 사용하는 애플리케이션을 디버그하고 게시할 수 있습니다.

## <a name="distributing-the-library-in-a-nuget-package"></a>NuGet 패키지에 포함된 라이브러리 배포

클래스 라이브러리를 NuGet 패키지로 게시하여 광범위하게 사용하도록 할 수 있습니다. Visual Studio에서는 NuGet 패키지의 생성을 지원하지 않습니다. 이 패키지를 만들려면 [`dotnet` 명령줄 유틸리티](../tools/dotnet.md)를 사용합니다.

1. 콘솔 창이 열립니다. 예를 들어 Windows 작업 표시줄의 **무엇이든 물어보세요.** 텍스트 상자에 `Command Prompt`(약식으로 `cmd`)를 입력한 다음 **명령 프롬프트** 데스크톱 앱을 선택하거나 검색 결과에서 선택된 경우 Enter 키를 눌러 콘솔 창을 엽니다.

1. 라이브러리의 프로젝트 디렉터리로 이동합니다. 일반적인 파일 위치를 다시 구성하지 않은 경우 *Documents\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary* 디렉터리에 있습니다. 이 디렉터리에는 소스 코드 및 프로젝트 파일 *StringLibrary.csproj*가 들어 있습니다.

1. 명령 `dotnet pack --no-build`를 실행합니다. `dotnet` 유틸리티는 *.nupkg* 확장명을 가진 패키지를 생성합니다.

   > [!TIP]
   > *dotnet.exe*를 포함하는 디렉터리가 해당 PATH에 없는 경우 콘솔 창에 `where dotnet.exe`를 입력하여 해당 위치를 찾을 수 있습니다.

NuGet 패키지를 만드는 방법에 대한 자세한 내용은 [플랫폼 간 도구로 NuGet 패키지를 만드는 방법](../deploying/creating-nuget-packages.md)을 참조하세요.
