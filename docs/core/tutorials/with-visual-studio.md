---
title: Visual Studio 2017에서 .NET Core를 사용하여 C# Hello World 애플리케이션 빌드
description: Visual Studio 2017에서 C#을 사용하여 간단한 .NET Core 콘솔 애플리케이션을 빌드하는 방법을 알아봅니다.
author: BillWagner
ms.author: wiwagn
ms.date: 09/13/2017
ms.custom: vs-dotnet, seodec18
ms.openlocfilehash: b42a71993cb120c88b90e867b7af23873b99d280
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039593"
---
# <a name="build-a-c-hello-world-application-with-the-net-core-sdk-in-visual-studio-2017"></a>Visual Studio 2017에서 .NET Core SDK를 사용하여 C# Hello World 애플리케이션 빌드

이 항목에서는 Visual Studio 2017에서 C#을 사용하여 간단한 .NET Core 콘솔 애플리케이션을 빌드, 디버그 및 게시하는 과정을 단계별로 소개합니다. Visual Studio 2017은 .NET Core 애플리케이션 빌드를 위해 필요한 모든 기능을 갖춘 개발 환경을 제공합니다. 플랫폼 특정 종속성이 없는 애플리케이션은 .NET Core에서 대상으로 하는 모든 플랫폼과 .NET Core가 설치된 모든 시스템에서 실행할 수 있습니다.

## <a name="prerequisites"></a>전제 조건

".NET Core 플랫폼 간 개발" 워크로드가 설치된 [Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs). .NET Core 2.1 버전 이상을 사용하여 앱을 개발할 수 있습니다.

자세한 내용은 [Windows의 .NET Core에 대한 필수 조건](../windows-prerequisites.md) 항목을 참조하세요.

## <a name="a-simple-hello-world-application"></a>간단한 Hello World 애플리케이션

먼저 간단한 "Hello World" 콘솔 애플리케이션을 만들어 보겠습니다. 아래 단계를 수행합니다.

1. Visual Studio 2017을 시작합니다. 메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다. *새 프로젝트** 대화 상자에서 **Visual C#** 노드와 **.NET Core** 노드를 차례로 선택합니다. 그런 다음 **콘솔 앱(.NET Core)** 프로젝트 템플릿을 선택합니다. **이름** 텍스트 상자에 "HelloWorld"를 입력합니다. **확인** 단추를 선택합니다.

   ![콘솔 앱이 선택된 새 프로젝트 대화 상자](./media/with-visual-studio/visual-studio-new-project.png)

1. Visual Studio에서는 템플릿을 사용하여 프로젝트를 만듭니다. .NET Core용 C# 콘솔 애플리케이션 템플릿은 <xref:System.String> 배열을 인수로 사용하는 단일 메서드 `Main`로 `Program` 클래스를 자동으로 정의합니다. `Main`은 애플리케이션 진입점으로, 애플리케이션을 시작할 때 런타임에 의해 자동으로 호출되는 메서드입니다. 애플리케이션이 시작될 때 제공되는 모든 명령줄 인수는 *args* 배열에서 사용할 수 있습니다.

   ![Visual Studio 및 새 HelloWorld 프로젝트](./media/with-visual-studio/visual-studio-main-window.png)

   템플릿은 간단한 "Hello World" 애플리케이션을 만듭니다. <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 메서드를 호출하여 리터럴 문자열 "Hello World!"를 콘솔 창에 표시합니다. 도구 모음에서 녹색 화살표가 있는 **HelloWorld** 단추를 선택하여 디버그 모드에서 프로그램을 실행할 수 있습니다. 이렇게 하면 콘솔 창이 잠깐만 표시되었다가 닫힙니다. `Main` 메서드의 단일 문이 실행되는 즉시 `Main` 메서드가 종료되고 애플리케이션도 종료되기 때문입니다.

1. 애플리케이션이 콘솔 창을 닫기 전에 일시 중지되도록 하려면 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 메서드 호출 바로 뒤에 다음 코드를 추가합니다.

   ```csharp
   Console.Write("Press any key to continue...");
   Console.ReadKey(true);
   ```

   이 코드는 프로그램을 중지하려면 아무 키나 누르라는 메시지를 표시하며, 사용자가 아무 키나 누르면 프로그램이 일시 중지됩니다.

1. 메뉴 모음에서 **빌드** > **솔루션 빌드**를 선택합니다. 이렇게 하면 프로그램이 IL(중간 언어)로 컴파일됩니다. 이 컴파일 결과는 JIT(Just-In-Time) 컴파일러에 의해 이진 코드로 변환됩니다.

1. 도구 모음에서 녹색 화살표가 있는 **HelloWorld** 단추를 선택하여 프로그램을 실행합니다.

   ![“Hello World 계속하려면 아무 키나 누르세요.”를 표시하는 콘솔 창](./media/with-visual-studio/hello-world-console.png)

1. 콘솔 창을 닫으려면 아무 키나 누릅니다.

## <a name="enhancing-the-hello-world-application"></a>Hello World 애플리케이션 개선

사용자에게 이름을 입력하라는 메시지를 표시한 다음 사용자 이름을 날짜 및 시간과 함께 표시하도록 애플리케이션을 개선합니다. 프로그램을 수정하고 테스트하려면 다음을 수행합니다.

1. 코드 창에서 `static void Main(string[] args)` 줄 다음에 오는 여는 중괄호 바로 뒤, 첫 번째 닫는 중괄호 앞에 다음 C# 코드를 입력합니다.

   [!code-csharp[GettingStarted#1](../../../samples/snippets/csharp/getting_started/with_visual_studio/helloworld.cs#1)]

   이 코드는 `Main` 메서드의 콘텐츠를 바꿉니다.

   ![업데이트된 Main 메서드가 포함된 Visual Studio 프로그램 C# 파일](./media/with-visual-studio/visual-csharp-code-window.png)

   이 코드는 "What is your name?"을 콘솔 창에 표시하고 사용자가 문자열을 입력한 후 Enter 키를 누를 때까지 기다립니다. 이 문자열을 `name`이라는 변수에 저장합니다. 또한 현재 현지 시간을 포함하는 <xref:System.DateTime.Now?displayProperty=nameWithType> 속성 값을 검색한 후 `date`라는 변수에 할당합니다. 마지막으로, [보간된 문자열](../../csharp/language-reference/tokens/interpolated.md)을 사용하여 콘솔 창에 이러한 값을 표시합니다.

1. **빌드** > **솔루션 빌드**를 선택하여 프로그램을 컴파일합니다.

1. 도구 모음에서 녹색 화살표를 선택하거나, F5 키를 누르거나, **디버그** > **디버깅 시작** 메뉴 항목을 선택하여 Visual Studio의 디버그 모드에서 프로그램을 실행합니다. 이름을 입력하고 Enter 키를 눌러 프롬프트에 응답합니다.

   ![수정된 프로그램 출력이 표시된 콘솔 창](./media/with-visual-studio/hello-world-update.png)

1. 콘솔 창을 닫으려면 아무 키나 누릅니다.

애플리케이션을 만들고 실행했습니다. 전문가 수준의 애플리케이션을 개발하려면 애플리케이션 릴리스 준비를 위해 몇 가지 추가 단계를 수행합니다.

- 애플리케이션 디버그에 대한 자세한 내용은 [Visual Studio 2017을 사용하여 .NET Core Hello World 애플리케이션 디버그](debugging-with-visual-studio.md)를 참조하세요.

- 애플리케이션의 배포 가능한 버전을 개발 및 게시하는 방법에 대한 자세한 내용은 [Visual Studio 2017을 사용하여 .NET Core Hello World 애플리케이션 게시](publishing-with-visual-studio.md)를 참조하세요.

## <a name="related-topics"></a>관련 항목

콘솔 애플리케이션 대신 .NET Core 및 Visual Studio 2017을 사용하여 클래스 라이브러리를 빌드할 수도 있습니다. 단계별 지침을 보려면 [Visual Studio 2017에서 C# 및 .NET Core로 클래스 라이브러리 빌드](library-with-visual-studio.md)를 참조하세요.

다운로드할 수 있는 코드 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용하여 Mac, Linux 및 Windows에서 .NET Core 콘솔 응용 프로그램을 개발할 수도 있습니다. 단계별 자습서에 대해서는 [Visual Studio Code 시작](with-visual-studio-code.md)을 참조하세요.
