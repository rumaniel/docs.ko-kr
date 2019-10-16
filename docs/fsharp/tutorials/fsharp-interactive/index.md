---
title: F# Interactive(fsi.exe) 참조
description: 대화형 ( F# fsi.exe)을 사용 하 여 콘솔에서 코드를 F# 대화형으로 실행 하거나 스크립트를 실행 F# 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 4e8521677cad5f4e62d2822837818292c55da96d
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002069"
---
# <a name="interactive-programming-with-f"></a>F @ no__t를 사용한 대화형 프로그래밍-0

> [!NOTE]
> 이 문서에서는 현재 Windows만을 위한 환경에 대해 설명합니다.  다시 작성될 예정입니다.

> [!NOTE]
> API 참조 링크를 통해 MSDN으로 이동됩니다.  docs.microsoft.com API 참조가 완전하지 않습니다.

F# Interactive(fsi.exe)는 콘솔에서 F# 코드를 대화형으로 실행하거나 F# 스크립트를 실행하는 데 사용됩니다. 즉, F# Interactive는 F# 언어에 대해 REPL(읽기, 평가, 인쇄 루프)을 실행합니다.

콘솔에서 F# Interactive를 실행하려면 fsi.exe를 실행합니다.  Fsi.exe는 다음 위치에서 찾을 수 있습니다.

```console
C:\Program Files (x86)\Microsoft Visual Studio\2019\<sku>\Common7\IDE\CommonExtensions\Microsoft\FSharp
```

여기서 `sku`은 `Community`, `Professional` 또는 `Enterprise`입니다.

사용 가능한 명령줄 옵션에 대한 정보는 [F# Interactive Options](../../language-reference/fsharp-interactive-options.md)(F# Interactive 옵션)를 참조하세요.

Visual Studio를 통해 F# Interactive를 실행하려면 **F# Interactive**라는 레이블이 있는 적절한 도구 모음 단추를 클릭하거나 **Ctrl+Alt+F** 키를 사용합니다. 이렇게 하면 대화형 창(F# Interactive 세션을 실행하는 도구 창)이 열립니다. 대화형 창에서 실행할 코드를 선택하고 **Alt+Enter** 키 조합을 눌러도 됩니다. 그러면 레이블이 **F# Interactive**인 도구 창에서 F# Interactive가 시작됩니다. 이 키 조합을 사용할 때 편집기 창에 포커스가 있는지 확인합니다.

콘솔을 사용하든 Visual Studio를 사용하든 상관없이 명령 프롬프트가 나타납니다. 해석기를 실행하려면 사용자가 이 명령 프롬프트에 필요한 사항을 입력해야 합니다. 코드 파일에서와 같은 방법으로 코드를 입력할 수 있습니다. 코드를 컴파일하고 실행하려면 세미콜론 두 개( **;;** )를 입력하여 입력 줄 하나 또는 여러 개를 종료합니다.

F# Interactive가 코드 컴파일을 시도하며, 컴파일이 성공하면 코드를 실행하고 컴파일된 형식과 값의 서명을 인쇄합니다. 오류가 발생하면 해석기에 오류 메시지가 출력됩니다.

프로그램을 빌드할 수 있도록 동일한 세션에서 입력한 코드는 이전에 입력된 모든 구문에 액세스할 수 있습니다. 도구 창에서는 확장 버퍼가 제공되므로 필요한 경우 파일에 코드를 복사할 수 있습니다.

F# Interactive는 Visual Studio에서 실행할 때 프로젝트와 독립적으로 실행되므로 예를 들어 함수의 코드를 대화형 창에 복사하지 않으면 프로젝트에 정의한 구문을 F# Interactive에서 사용할 수 없습니다.

일부 라이브러리를 참조하는 프로젝트를 연 경우, F# Interactive에서 **솔루션 탐색기**를 통해 해당 프로젝트를 참조할 수 있습니다. F# Interactive에서 라이브러리를 참조하려면 **참조** 노드를 확장하고, 라이브러리에 대한 바로 가기 메뉴를 열고, **F# Interactive로 보내기**를 선택합니다.

설정을 조정하여 F# Interactive 명령줄 인수(옵션)를 제어할 수 있습니다. 이렇게 하려면 **도구** 메뉴에서 **옵션...** 을 선택하고 **F# 도구**를 확장합니다. 변경 가능한 두 가지 설정은 F# Interactive 옵션과 **64비트 F# Interactive** 설정(F# Interactive를 64비트 컴퓨터에서 실행하는 경우만 해당)입니다. 이 설정은 전용 64비트 버전의 fsi.exe 또는 fsianycpu.exe(컴퓨터 아키텍처를 사용하여 32비트 또는 64비트 프로세스로 실행할지 여부를 결정)를 실행할지 여부를 결정합니다.

## <a name="scripting-with-f"></a>F @ no__t를 사용한 스크립팅-0
스크립트는 파일 확장명 **.fsx** 또는 **.fsscript**를 사용합니다. 소스 코드를 컴파일한 다음 나중에 컴파일된 어셈블리를 실행하는 대신 **fsi.exe**를 실행하고 F# 소스 코드의 스크립트 파일 이름을 지정하면 F# Interactive가 코드를 읽어 실시간으로 실행합니다.

## <a name="differences-between-the-interactive-scripting-and-compiled-environments"></a>대화형, 스크립팅 및 컴파일된 환경의 차이점
F# Interactive에서 코드를 컴파일할 때는 대화형으로 실행하든 스크립트를 실행하든 관계없이 **INTERACTIVE** 기호가 정의됩니다. 컴파일러에서 코드를 컴파일할 때는 **COMPILED** 기호가 정의됩니다. 따라서 컴파일된 모드와 대화형 모드에서 코드가 달라야 하는 경우 조건부 컴파일용 전처리기 지시문을 통해 사용할 코드를 결정할 수 있습니다.

F# Interactive에서 스크립트를 실행할 때는 컴파일러에서 실행하는 경우 제공되지 않는 일부 지시문을 사용할 수 있습니다. 다음 표에는 F# Interactive를 사용할 때 제공되는 지시문이 요약되어 있습니다.

|지시문|설명|
|---------|-----------|
|**#help**|사용 가능한 지시문에 대한 정보를 표시합니다.|
|**#I**|어셈블리 검색 경로를 따옴표로 묶어 지정합니다.|
|**#load**|소스 파일을 읽고 컴파일한 다음 실행합니다.|
|**#quit**|F# Interactive 세션을 종료합니다.|
|**#r**|어셈블리를 참조합니다.|
|**#time ["on"&#124;"off"]**|**#time** 자체는 성능 정보 표시 여부를 전환합니다. 이 지시문을 사용하도록 설정하면 F# Interactive가 해석 및 실행되는 각 코드 섹션에 대해 실제 시간, CPU 시간 및 가비지 컬렉션 정보를 측정합니다.|

F# Interactive에서 파일 또는 경로를 지정할 때는 문자열 리터럴이 필요합니다. 따라서 파일 및 경로를 따옴표로 묶어야 하며, 일반적인 이스케이프 문자가 적용됩니다. 또한 @ 문자를 사용하여 F# Interactive가 경로를 포함하는 문자열을 축자 문자열로 해석하도록 할 수 있습니다. 그러면 F# Interactive에서 이스케이프 문자를 무시합니다.

컴파일된 모드와 대화형 모드 간의 차이점 중 하나는 명령줄 인수에 액세스하는 방식입니다. 컴파일된 모드에서 **System.Environment.GetCommandLineArgs**를 사용합니다. 스크립트에서는 **fsi.CommandLineArgs**를 사용합니다.

다음 코드에서는 스크립트에서 명령줄 인수를 읽는 함수를 만드는 방법과 스크립트에서 다른 어셈블리를 참조하는 방법을 보여 줍니다. 첫 번째 코드 파일인 **MyAssembly.fs**는 참조되는 어셈블리의 코드입니다. **fsc-a MyAssembly.fs** 명령줄을 사용하여 이 파일을 컴파일한 다음 **fsi-exec file1.fsx** 테스트 명령줄을 사용하여 두 번째 파일을 스크립트로 실행합니다.

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

```fsharp
// file1.fsx
#r "MyAssembly.dll"

printfn "Command line arguments: "

for arg in fsi.CommandLineArgs do
    printfn "%s" arg

printfn "%A" (MyAssembly.myFunction 10 40)
```

출력은 다음과 같습니다.

```console
Command line arguments: 
file1.fsx
test
90
```

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----|-----------|
|[F# Interactive 옵션](../../language-reference/fsharp-interactive-options.md)|F# 대화형의 명령줄 구문 및 옵션에 대해 설명 합니다. fsi.exe.|
|[F# Interactive 라이브러리 참조](https://msdn.microsoft.com/visualfsharpdocs/conceptual/fsharp-interactive-library-reference)|F# Interactive에서 코드를 실행할 때 사용할 수 있는 라이브러리 기능에 대해 설명합니다.|
