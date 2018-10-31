---
title: .NET Core 시작
description: Windows, Linux 및 macOS에서 .NET Core 응용 프로그램을 빌드하는 방법을 알아볼 수 있는 리소스를 찾아보세요.
author: thraka
ms.author: adegeo
ms.date: 06/27/2018
ms.openlocfilehash: 3fff7884082c46477d37b08560a2c71e7ee345e5
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121256"
---
# <a name="get-started-with-net-core"></a>.NET Core 시작

이 문서에서는 .NET Core로 시작하는 데 필요한 정보를 제공합니다. Windows, Linux 및 macOS에서 .NET Core를 설치할 수 있습니다. 원하는 텍스트 편집기에서 코딩하고 플랫폼 간 라이브러리 및 응용 프로그램을 생성할 수 있습니다. 

.NET Core가 무엇인지 또는 다른 .NET 기술과 어떻게 관련있는지에 대해 잘 모를 경우 [.NET이란](https://www.microsoft.com/net/learn/dotnet/what-is-dotnet) 개요로 시작하세요. 간단히 말해 .NET Core는 오픈 소스의 플랫폼 간 .NET의 구현입니다.

## <a name="create-an-application"></a>응용 프로그램 만들기

먼저 사용자의 컴퓨터에 [.NET Core SDK](https://www.microsoft.com/net/download/)를 다운로드하여 설치합니다.

다음으로 **PowerShell**, **명령 프롬프트** 또는 **Bash**와 같은 터미널을 엽니다. 다음 `dotnet` 명령을 입력하여 C# 응용 프로그램을 만들고 실행합니다.

```console
dotnet new console --output sample1
dotnet run --project sample1
```

다음과 같은 내용이 출력됩니다.

```console
Hello World!
```

지금까지 간단한 .NET Core 응용 프로그램을 만들었습니다. 또한 [Visual Studio Code](tutorials/with-visual-studio-code.md), [Visual Studio 2017](tutorials/with-visual-studio.md)(Windows만 해당) 또는 [Mac용 Visual Studio](tutorials/using-on-mac-vs.md)(macOS만 해당)를 사용하여 .NET Core 응용 프로그램을 만들 수도 있습니다.

## <a name="tutorials"></a>자습서

다음 단계별 자습서에 따라 .NET Core 응용 프로그램 개발을 시작할 수 있습니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

* [Visual Studio 2017에서 .NET Core를 사용하여 C# “Hello World” 응용 프로그램 빌드.](./tutorials/with-visual-studio.md)

* [Visual Studio 2017에서 .NET Core를 사용하여 C# 클래스 라이브러리 빌드.](./tutorials/library-with-visual-studio.md)

* [Visual Studio 2017에서 .NET Core를 사용하여 Visual Basic “Hello World” 응용 프로그램 빌드.](./tutorials/vb-with-visual-studio.md)

* [Visual Studio 2017에서 Visual Basic 및 .NET Core로 클래스 라이브러리 빌드.](./tutorials/vb-library-with-visual-studio.md)  

* [Visual Studio Code 및 .NET Core를 설치 및 사용하는 방법](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core/)에 관한 비디오 시청.

* [Visual Studio 2017 및 .NET Core를 설치 및 사용하는 방법](https://channel9.msdn.com/Blogs/dotnet/Get-Started-NET-Core-Visual-Studio-2017/)에 관한 비디오 시청.

* [명령줄을 사용하여 .NET Core 시작.](tutorials/using-with-xplat-cli.md)

지원되는 Windows 버전 목록은 [Windows 개발을 위한 필수 조건](windows-prerequisites.md) 문서를 참조하세요.

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

다음 단계별 자습서에 따라 .NET Core 응용 프로그램 개발을 시작할 수 있습니다.

* [명령줄을 사용하여 .NET Core 시작.](tutorials/using-with-xplat-cli.md)

* [Ubuntu에서 C# 및 .NET Core를 사용하여 Visual Studio Code 시작](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu)에 관한 비디오 시청.

지원되는 Linux 배포판 및 버전 목록은 [Linux 개발을 위한 필수 조건](linux-prerequisites.md) 문서를 참조하세요.

# <a name="macostabmacos"></a>[macOS](#tab/macos)

다음 단계별 자습서에 따라 .NET Core 응용 프로그램 개발을 시작할 수 있습니다.

* [macOS에서 C# 및 .NET Core를 사용하여 Visual Studio Code 시작](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-NET-Core-Mac)에 관한 비디오 시청.

* [Visual Studio Code를 사용하여 macOS에서 .NET Core 시작.](tutorials/using-on-macos.md)

* [명령줄을 사용하여 .NET Core 시작.](tutorials/using-with-xplat-cli.md)

* [Mac용 Visual Studio를 사용하여 macOS에서 .NET Core 시작.](tutorials/using-on-mac-vs.md)

* [Mac용 Visual Studio를 사용하여 macOS에서 완전한 .NET Core 솔루션 빌드.](tutorials/using-on-mac-vs-full-solution.md)

지원되는 OS X/macOS 버전 목록은 [macOS 개발을 위한 필수 구성 요소](macos-prerequisites.md) 항목을 참조하세요.

***
