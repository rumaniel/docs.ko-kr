---
title: Hello World -- Windows 또는 Mac에서 Visual Studio를 사용하여 프로그램 처음 만들기 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 09/12/2019
f1_keywords:
- cs.program
- vs.csharp.startpage.firstapplication
helpviewer_keywords:
- examples [C#], Hello World
- Hello World example [C#]
ms.assetid: 6493182a-b0b6-4539-a719-518a168cb730
ms.openlocfilehash: 0807e46d36a4cf031bc44ae0dc4efab79dd51d03
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991336"
---
# <a name="hello-world----your-first-program"></a>Hello World -- 프로그램 처음 만들기

이 문서에서는 Visual Studio를 사용하여 전통적인 "Hello World!" 프로그램을 만듭니다. Visual Studio는 .NET 개발용으로 설계된 다양한 기능을 갖춘 전문적인 IDE(통합 개발 환경)입니다. 이 프로그램은 Visual Studio의 일부 기능만 사용하여 만듭니다. Visual Studio에 대해 자세히 알아보려면 [Visual C# 및 Visual Basic 시작](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)을 참조하세요.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="create-a-new-application"></a>새 애플리케이션 만들기

<!-- markdownlint-disable MD025 -->

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

Visual Studio를 시작합니다. Windows에 다음 이미지와 같이 표시됩니다.

![Windows의 Visual Studio 시작 화면](./media/hello-world-your-first-program/visual-studio-windows-start-screen.png)

이미지 오른쪽 아래 모서리에서 **새 프로젝트 만들기**를 선택합니다. Visual Studio에 **새 프로젝트** 대화 상자가 표시됩니다.

![Windows의 Visual Studio 새 프로젝트 화면](./media/hello-world-your-first-program/visual-studio-windows-new-project.png)

> [!NOTE]
> Visual Studio를 처음 시작하는 경우 **최근 프로젝트 템플릿** 목록이 비어 있습니다.

새 프로젝트 대화 상자에서 "콘솔 앱(.NET Core)"을 선택한 후 **다음**을 누릅니다. 프로젝트에 "HelloWorld"와 같은 이름을 지정한 다음 **만들기**를 누릅니다.

Visual Studio에서 프로젝트가 열립니다. 이미 기본적인 "Hello World!" 예가 포함됩니다. `Ctrl` + `F5`를 눌러 프로젝트를 실행합니다. Visual Studio가 프로젝트를 빌드하고 소스 코드를 실행 파일로 변환합니다. 그런 다음 새 애플리케이션을 실행하는 명령 창이 시작됩니다. 창에 다음 텍스트가 표시되어야 합니다.

```console
Hello World!

C:\Program Files\dotnet\dotnet.exe (process 11964) exited with code 0.
Press any key to close this window . . .
```

아무 키나 눌러 창을 닫습니다.

# <a name="macostabmacos"></a>[macOS](#tab/macos)

Mac용 Visual Studio를 시작합니다. Mac에 다음 이미지와 같이 표시됩니다.

![Mac의 Visual Studio 시작 화면](./media/hello-world-your-first-program/visual-studio-mac-start-screen.png)

> [!NOTE]
> Mac용 Visual Studio를 처음 시작하는 경우 **최근 프로젝트** 목록이 비어 있습니다.

이미지의 오른쪽 위 모서리에서 **새로 만들기**를 선택합니다. Mac용 Visual Studio에 **새 프로젝트** 대화 상자가 표시됩니다.

![Mac의 Visual Studio 새 프로젝트 화면](./media/hello-world-your-first-program/visual-studio-mac-new-project.png)

새 프로젝트 대화 상자에서 ".NET Core"와 “콘솔 앱”을 선택한 후 **다음**을 누릅니다. 대상 프레임워크를 선택해야 합니다. 기본값을 사용해도 되므로 다음을 누릅니다. 프로젝트에 "HelloWorld"와 같은 이름을 지정한 다음 **만들기**를 누릅니다. 기본 프로젝트 위치를 사용할 수 있습니다. 소스 제어에 이 프로젝트를 추가하지 마세요.

Mac용 Visual Studio에서 프로젝트가 열립니다. 이미 기본적인 "Hello World!" 예가 포함됩니다. `Ctrl` + `Fn` + `F5`를 눌러 프로젝트를 실행합니다. Mac용 Visual Studio가 프로젝트를 빌드하고 소스 코드를 실행 파일로 변환합니다. 그런 다음 새 애플리케이션을 실행하는 명령 창이 시작됩니다. 창에 다음 텍스트가 표시되어야 합니다.

```console
Hello World!

Press any key to close this window . . .
```

세션을 종료하려면 아무 키나 누릅니다.

---

## <a name="elements-of-a-c-program"></a>C# 프로그램의 요소

이 프로그램의 중요한 부분을 살펴보겠습니다. 첫 번째 줄에는 설명이 포함됩니다. `//` 문자는 줄의 나머지 부분을 설명으로 변환합니다.

[!code-csharp[csProgGuide#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#32)]

텍스트 블록을 `/*` 및 `*/` 문자 사이에 포함하여 주석으로 처리할 수도 있습니다. 다음 예제에서 이를 확인할 수 있습니다.

[!code-csharp[csProgGuide#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#33)]

C# 콘솔 애플리케이션에는 시작 및 끝을 제어하는 `Main` 메서드가 포함되어야 합니다. `Main` 메서드에서 개체를 만들고 다른 메서드를 실행합니다.

`Main` 메서드는 클래스나 구조체 내부에 있는 [정적](../../language-reference/keywords/static.md) 메서드입니다. 이전 "Hello World!" 예제에서 이 메서드는 `Hello` 클래스에 있습니다. 다음 방법 중 하나로 `Main` 메서드를 선언할 수 있습니다.

- 이 메서드는 `void`를 반환합니다. 즉, 프로그램에서 값을 반환하지 않습니다.

[!code-csharp[csProgGuideMain#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#12)]

- 정수를 반환할 수도 있습니다. 이 정수는 애플리케이션의 **종료 코드**입니다.

[!code-csharp[csProgGuideMain#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#13)]

- 반환 형식은 각각 인수를 사용할 수 있습니다.

[!code-csharp[csProgGuideMain#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#19)]

또는

[!code-csharp[csProgGuideMain#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#18)]

`Main` 메서드의 매개 변수 `args`는 프로그램을 호출하는 데 사용된 명령줄 인수가 포함된 `string` 배열입니다.

명령줄 인수를 사용하는 방법에 대한 자세한 내용은 [Main() 및 명령줄 인수](../main-and-command-args/index.md)의 예를 참조하세요.

## <a name="input-and-output"></a>입력 및 출력

일반적으로 C# 프로그램에서는 .NET Framework의 런타임 라이브러리에서 제공되는 입출력 서비스를 사용합니다. `System.Console.WriteLine("Hello World!");` 문은 <xref:System.Console.WriteLine%2A> 메서드를 사용합니다. 이 메서드는 런타임 라이브러리에 있는 <xref:System.Console> 클래스의 출력 메서드 중 하나입니다. 이 메서드는 표준 출력 스트림에 문자열 매개 변수를 표시하고 이어서 새 줄을 표시합니다. 기타 <xref:System.Console> 메서드는 다양한 입력 및 출력 작업에 사용할 수 있습니다. 프로그램 시작 부분에 `using System;` 지시문을 포함하면 <xref:System> 클래스 및 메서드를 정규화하지 않고 바로 사용할 수 있습니다. 예를 들어 `System.Console.WriteLine` 대신 `Console.WriteLine`을 호출할 수 있습니다.

[!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]

[!code-csharp[csProgGuide#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#23)]

입출력 메서드에 대한 자세한 내용은 <xref:System.IO>를 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [샘플 및 자습서](../../../samples-and-tutorials/index.md)
- [Main()과 명령줄 인수](../main-and-command-args/index.md)
- [Visual C# 및 Visual Basic 시작](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)
