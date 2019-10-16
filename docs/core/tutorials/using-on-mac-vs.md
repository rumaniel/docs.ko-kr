---
title: Mac용 Visual Studio를 사용하여 macOS에서 .NET Core 시작
description: 이 항목에서는 Mac 및 .NET Core용 Visual Studio를 사용하여 간단한 콘솔 애플리케이션을 빌드하는 과정을 안내합니다.
author: mairaw
ms.date: 07/11/2019
ms.custom: seodec18
ms.openlocfilehash: 77e676c327b62369e7ddb9444bf8f246d3c5c2e8
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182503"
---
# <a name="get-started-with-net-core-on-macos-using-visual-studio-for-mac"></a>Mac용 Visual Studio를 사용하여 macOS에서 .NET Core 시작

Visual Studio for Mac은 .NET Core 애플리케이션 개발을 위해 필요한 전기능 IDE(통합 개발 환경)를 제공합니다. 이 항목에서는 Mac 및 .NET Core용 Visual Studio를 사용하여 간단한 콘솔 애플리케이션을 빌드하는 과정을 안내합니다.

> [!NOTE]
> 사용자 의견은 매우 중요합니다. Mac용 Visual Studio의 개발 팀에 다음 두 가지 방법으로 의견을 제공할 수 있습니다.
>
> * Mac용 Visual Studio의 메뉴에서 **도움말** > **문제 보고**를 선택하거나 시작 화면에서 **문제 보고**를 선택하면 버그 보고서를 작성하기 위한 창이 열립니다. [Developer Community](https://developercommunity.visualstudio.com/spaces/8/index.html)(개발자 커뮤니티) 포털에서 의견을 추적할 수 있습니다.
> * 제안하려면 메뉴에서 **도움말** > **제안하기**를 선택하거나 시작 화면에서 **제안하기**를 선택합니다. 그러면 [Mac용 Visual Studio Developer Community 웹 페이지](https://developercommunity.visualstudio.com/content/idea/post.html?space=41)로 이동됩니다.

## <a name="prerequisites"></a>전제 조건

[Mac에서 .NET Core의 필수 구성 요소](../macos-prerequisites.md) 항목을 참조하세요.

[.NET Core 지원](/visualstudio/mac/net-core-support) 문서를 참조하여 지원되는 버전의 .NET Core를 사용하고 있는지 확인합니다.

## <a name="get-started"></a>시작

필수 구성 요소와 Visual Studio for Mac을 이미 설치한 경우 이 섹션을 건너뛰고 [프로젝트 만들기](#creating-a-project)를 계속 진행합니다. 다음 단계에 따라 필수 구성 요소 및 Visual Studio for Mac을 설치합니다.

[Visual Studio for Mac 설치 관리자](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)를 다운로드합니다. 설치 관리자를 실행합니다. 사용권 계약을 읽은 다음 동의합니다. 설치하는 동안 .NET Core 설치 옵션을 선택합니다. 플랫폼 간 모바일 앱 개발 기술인 Xamarin을 설치할 기회가 제공됩니다. Xamarin 및 관련된 구성 요소의 설치는 .NET Core 개발에서 선택 사항입니다. Mac용 Visual Studio 설치 프로세스에 대한 연습을 진행하려면 [Mac용 Visual Studio 설명서](/visualstudio/mac/)를 참조하세요. 설치가 완료되면 Visual Studio for Mac IDE를 시작합니다.

## <a name="creating-a-project"></a>프로젝트 만들기

1. [시작] 창에서 **새로 만들기**를 선택합니다.

   ![Mac용 Visual Studio 시작 화면의 새로 만들기 단추](./media/using-on-mac-vs/visual-studio-mac-new-project.png)

1. **새 프로젝트** 대화 상자에서 **.NET Core** 노드 아래에서 **앱**을 선택합니다. **콘솔 애플리케이션** 템플릿을 선택하고 **다음**을 선택합니다.

   ![새 프로젝트 템플릿 목록](./media/using-on-mac-vs/visual-studio-mac-new-dialog.png)

1. 여러 버전의 .NET Core가 설치된 경우 프로젝트의 대상 프레임워크를 선택합니다.

1. **프로젝트 이름**으로 "HelloWorld"를 입력합니다. **만들기**를 선택합니다.

   ![새 콘솔 애플리케이션 대화 상자 구성](./media/using-on-mac-vs/visual-studio-mac-new-options.png)

1. 프로젝트의 종속성이 복원되는 동안 기다립니다. 프로젝트에는 `Main` 메서드가 있는 `Program` 클래스를 포함하는 C# 파일 *Program.cs*가 있습니다. 앱이 실행되면 `Console.WriteLine` 문은 "Hello World!"를 콘솔에 출력합니다.

   ![Program.cs 파일이 열려 있는 주 창](./media/using-on-mac-vs/visual-studio-mac-editor.png)

## <a name="run-the-application"></a>애플리케이션 실행

앱을 디버그 모드에서 실행하려면 ⌘ ↵(Command + Enter)를 사용하고 릴리스 모드에서 실행하려면 ⌥ ⌘ ↵(Option + Command + Enter)를 사용합니다.

![애플리케이션 출력 창에 Hello World!가 표시됩니다.](./media/using-on-mac-vs/visual-studio-mac-output.png)

## <a name="next-step"></a>다음 단계

[Visual Studio for Mac을 사용하여 macOS에서 완전한 .NET Core 솔루션 빌드](using-on-mac-vs-full-solution.md) 항목에서는 재사용 가능한 라이브러리 및 단위 테스트를 포함하는 전체 .NET Core 솔루션을 빌드하는 방법을 보여 줍니다.
