---
title: Visual Studio 2017을 사용하여 .NET Core Hello World 애플리케이션 게시
description: 게시하면 .NET Core 애플리케이션을 실행하는 데 필요한 파일 집합이 만들어집니다.
author: BillWagner
ms.author: wiwagn
ms.date: 10/05/2017
ms.custom: vs-dotnet, seodec18
ms.openlocfilehash: f8c37f47cc8dfb999f2371773a50c2dd91e074a5
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69660484"
---
# <a name="publish-your-net-core-hello-world-application-with-visual-studio-2017"></a>Visual Studio 2017을 사용하여 .NET Core Hello World 애플리케이션 게시

[Visual Studio 2017에서 .NET Core를 사용하여 C# Hello World 애플리케이션 빌드](with-visual-studio.md) 또는 [Visual Studio 2017에서 .NET Core를 사용하여 Visual Basic Hello World 애플리케이션 빌드](vb-with-visual-studio.md)에서 Hello World 콘솔 애플리케이션을 빌드했습니다. [Visual Studio 2017을 사용하여 C# Hello World 애플리케이션 디버그](debugging-with-visual-studio.md)에서 Visual Studio 디버거를 사용하여 테스트했습니다. 예상대로 작동하는지 확인했으므로 다른 사용자가 실행할 수 있도록 게시할 수 있습니다. 게시하면 애플리케이션을 실행하는 데 필요한 파일 집합이 만들어지며, 이 파일을 대상 컴퓨터에 복사하여 배포할 수 있습니다.

애플리케이션을 게시하고 실행하려면 

1. Visual Studio에서 애플리케이션의 릴리스 버전을 빌드하고 있는지 확인합니다. 필요한 경우 도구 모음의 빌드 구성 설정을 **디버그**에서 **릴리스**로 변경합니다.

   ![릴리스 빌드가 선택된 Visual Studio 도구 모음](media/publishing-with-visual-studio/visual-studio-toolbar-release.png)

1. **HelloWorld** 프로젝트(HelloWorld 솔루션 아님)를 마우스 오른쪽 단추로 클릭하고 메뉴에서 **게시**를 선택합니다. 주 Visual Studio에서 **빌드** 메뉴에서 **HelloWorld 게시**를 선택할 수도 있습니다.

   ![Visual Studio 게시 상황에 맞는 메뉴](media/publishing-with-visual-studio/publish-context-menu.png)

   ![Visual Studio 게시 창](media/publishing-with-visual-studio/publish-settings-window.png)

1. 콘솔 창이 열립니다. 예를 들어 Windows 작업 표시줄의 **검색하려면 여기에 입력하세요.** 텍스트 상자에 `Command Prompt`(약식으로 `cmd`)를 입력한 다음 **명령 프롬프트** 데스크톱 앱을 선택하거나 검색 결과에서 선택된 경우 Enter 키를 눌러 콘솔 창을 엽니다.

1. 애플리케이션 프로젝트 디렉터리의 `bin\release\PublishOutput` 하위 디렉터리에 게시된 애플리케이션으로 이동합니다. 다음 그림과 같이, 게시된 출력에는 다음 4개의 파일이 포함되어 있습니다.

      * *HelloWorld.deps.json*

         애플리케이션의 런타임 종속성 파일입니다. 애플리케이션을 실행하는 데 필요한 .NET Core 구성 요소 및 라이브러리(애플리케이션을 포함하는 동적 연결 라이브러리 포함)를 정의합니다. 자세한 내용은 [ 런타임 구성 파일](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md)을 참조하세요.
 
      * *HelloWorld.dll*

         애플리케이션을 포함하는 파일입니다. 콘솔 창에 `dotnet HelloWorld.dll` 명령을 입력하여 실행될 수 있는 동적 연결 라이브러리입니다. 

      * *HelloWorld.pdb*(배포에 대한 선택 사항)

         디버그 기호를 포함하는 파일입니다. 게시된 애플리케이션 버전을 디버그해야 하는 경우에는 이 파일을 저장해야 하지만 그렇지 않으면 애플리케이션과 함께 배포할 필요가 없습니다.

      * *HelloWorld.runtimeconfig.json*

         애플리케이션의 런타임 구성 파일입니다. 애플리케이션이 실행되도록 빌드된 .NET Core의 버전을 식별합니다. 자세한 내용은 [ 런타임 구성 파일](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md)을 참조하세요.  

   ![게시된 파일을 보여 주는 콘솔 창](media/publishing-with-visual-studio/published-files-output.png)

게시 프로세스는 프레임워크 종속 배포를 만듭니다. 이 배포는 시스템에 .NET Core가 설치되어 있으면 게시된 애플리케이션이 .NET Core에서 지원하는 모든 플랫폼에서 실행되는 배포 유형입니다. 사용자는 콘솔 창에서 `dotnet HelloWorld.dll` 명령을 실행하여 애플리케이션을 실행할 수 있습니다.

.NET Core 애플리케이션 게시 및 배포에 대한 자세한 내용은 [.NET Core 애플리케이션 배포](../deploying/index.md)를 참조하세요.
