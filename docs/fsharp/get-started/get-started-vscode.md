---
title: Visual Studio Code에서 F# 시작
description: Visual Studio Code와 Ionide 플러그인 도구 모음으로 F#을 사용하는 방법을 알아봅니다.
ms.date: 12/23/2018
ms.openlocfilehash: 2fa0518488d37b2130aaba96028ac92dac77eb97
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71082994"
---
# <a name="get-started-with-f-in-visual-studio-code"></a>Visual Studio Code에서 F# 시작

[Visual Studio Code](https://code.visualstudio.com)에서 [Ionide 플러그인](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp)을 사용하여 F# 코드를 작성하면 IntelliSense와 기본적인 코드 리팩토링이 가능한 경량이면서 다양한 플랫폼에서 사용할 수 있는 IDE(Integrated Development Environment) 환경을 얻을 수 있습니다. 이 플러그인을 더 자세히 알고 싶다면 [Ionide.io](http://ionide.io)를 방문합니다.

시작하려면 [F#과 Ionide 플러그인의 설치](install-fsharp.md#install-f-with-visual-studio-code)가 올바르게 되어있는지 확인합니다.

> [!NOTE]
> Ionide는 플랫폼 간 호환성 문제가 발생할 수 있는 닷넷 코어가 아닌 .NET Framework F# 프로젝트를 생성합니다. **Linux** 또는 **OSX**에서 실행 하는 경우 [명령줄 도구](get-started-command-line.md)를 사용 하 여 시작 하는 것이 더 간단 합니다.

## <a name="creating-your-first-project-with-ionide"></a>Ionide를 사용하여 첫 번째 프로젝트 만들기

새 F# 프로젝트를 생성하기 위해 새 폴더(원하는 이름을 지정할 수 있습니다)에서 Visual Studio Code를 엽니다.

다음으로, 명령 팔레트를 열고(**보기 > 명령 팔레트**) 다음을 입력합니다.

```console
> F# new project
```

[FORGE](https://github.com/fsharp-editing/Forge) 프로젝트에 의해 동작합니다.

> [!NOTE]
> 템플릿 옵션을 보이지 않으면 명령 팔레트에서 다음 명령을 실행하여 템플릿을 새로 고쳐보세요: `>F#: Refresh Project Templates`

Enter를 눌러서 "F#: new project"를 선택합니다. 이렇게 하면 프로젝트 템플릿을 선택하는 다음 단계로 넘어갑니다.

`classlib` 템플릿을 선택하고 **Enter**를 칩니다.

그런 다음에 프로젝트를 생성하기 위한 디렉터리를 선택합니다. 비워 두면 현재 디렉터리를 사용합니다.

끝으로, 마지막 단계에서는 프로젝트의 이름을 지정합니다. F#에서는 [파스칼식 대/소문자](http://c2.com/cgi/wiki?PascalCase)를 프로젝트 이름으로 사용합니다. 이 문서에서는 `ClassLibraryDemo`를 이름으로 합니다. 자신이 원하는 프로젝트 이름을 입력한 후 **Enter**를 칩니다.

지금까지의 단계를 수행했다면 Visual Studio 코드의 좌측 작업 영역에 다음 내용이 표시됩니다.

1. F# 프로젝트 자체는 `ClassLibraryDemo` 폴더 하위에 존재합니다.
2. [`Paket`](https://fsprojects.github.io/Paket/)을 통해 패키지를 추가하기 위한 올바른 디렉터리 구조.
3. [`FAKE`](https://fsharp.github.io/FAKE/)를 통한 크로스 플랫폼 빌드 스크립트.
4. 패키지를 설치하고 종속성을 해결할 수 있는 `paket.exe` 실행 파일.
5. 이 프로젝트를 Git 기반 소스 컨트롤에 추가하려는 경우 `.gitignore` 파일

## <a name="writing-some-code"></a>코드 작성

*ClassLibraryDemo* 폴더를 엽니다.  다음과 같은 파일이 표시됩니다.

1. 클래스가 정의된 F# 구현 파일인`ClassLibraryDemo.fs`
2. 이 프로젝트를 빌드하는 데 사용되는 F# 프로젝트 파일인 `ClassLibraryDemo.fsproj`
3. 소스 파일을 로드하는 F# 스크립트 파일인 `Script.fsx`.
4. 프로젝트 종속성을 지정하는 Paket 파일인 `paket.references`

`Script.fsx`를 열고 마지막에 다음 코드를 추가합니다.

[!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx)]

이 함수는 단어를 [Pig Latin](https://en.wikipedia.org/wiki/Pig_Latin) 형태로 변환합니다. 다음으로 F# Interactive (FSI)를 사용하여 평가합니다.

전체 함수를 강조 표시합니다(11줄 길이여야 함). 강조 표시되면 **Alt** 키를 누른 상태에서 **Enter**를 누릅니다. 팝업창이 표시되며 다음과 같이 표시됩니다.

![Ionide를 사용한 F# Interactive 출력 예시](./media/getting-started-vscode/vscode-fsi.png)

여기서 다음 세 가지 작업이 수행되었습니다.

1. FSI 프로세스를 시작했습니다.
2. FSI 프로세스로 강조 표시된 코드를 전송했습니다.
3. FSI 프로세스에서 전송한 코드를 평가합니다.

[함수](../language-reference/functions/index.md)를 전송했으므로 이제 FSI를 사용하여 해당 함수를 호출할 수 있습니다. 대화형 창에서 다음을 입력합니다.

```fsharp
toPigLatin "banana";;
```

다음과 같은 결과가 나타납니다.

```fsharp
val it : string = "ananabay"
```

이제 모음을 첫 글자로 사용해 보겠습니다. 다음과 같이 입력합니다.

```fsharp
toPigLatin "apple";;
```

다음과 같은 결과가 나타납니다.

```fsharp
val it : string = "appleyay"
```

예상대로 함수가 작동합니다. 축하합니다. 첫 번째 F#함수를 Visual Studio Code에서 작성하고 FSI를 사용하여 평가했습니다!

> [!NOTE]
> FSI에서는 `;;`가 라인의 끝입니다. FSI에서는 여러 줄의 입력을 허용하기 때문입니다. 마지막에 있는 `;;`는 FSI가 코드의 마지막이라는 것을 인지할 수 있게 해줍니다.

## <a name="explaining-the-code"></a>코드 설명

코드가 실제로 수행 하는 작업을 잘 모르는 경우에는 다음 단계를 수행 합니다.

여기서 볼 `toPigLatin` 수 있듯이는 단어를 입력으로 사용 하 고 해당 단어의 Pig 표현으로 변환 하는 함수입니다. 이에 대 한 규칙은 다음과 같습니다.

단어의 첫 문자가 모음으로 시작 하는 경우 단어의 끝에 "yay"를 추가 합니다. 모음으로 시작 하지 않으면 첫 번째 문자를 단어의 끝으로 이동 하 여 "ay"를 추가 합니다.

FSI.EXE에서 다음을 발견할 수 있습니다.

```fsharp
val toPigLatin : word:string -> string
```

이는를 `toPigLatin` 입력 `string` `word`으로 사용 하 고 다른 `string`를 반환 하는 함수입니다. 이를 [함수의 형식 서명](https://fsharpforfunandprofit.com/posts/function-signatures/)이라고 하며, 코드를 이해 F# F# 하는 데 해당 키의 기본 부분입니다. 또한 Visual Studio Code에서 함수를 가리키면이를 확인할 수 있습니다.

함수의 본문에는 다음과 같은 두 가지 요소가 있습니다.

1. 지정 된 문자 () `isVowel`가 [패턴 일치](../language-reference/pattern-matching.md)를 통해 제공 된 패턴`c`중 하 나와 일치 하는지 확인 하 여 해당 문자 ()가 모음 인지 여부를 확인 하는 이라는 내부 함수입니다.

   [!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L2-L6)]

2. 첫 번째 문자가 모음 인지 확인 하 고 첫 번째 문자가 모음 인지 여부를 기준으로 입력 문자에서 반환 값을 생성 하는 [식입니다.`if..then..else`](../language-reference/conditional-expressions-if-then-else.md)

   [!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L8-L11)]

따라서의 `toPigLatin` 흐름은 다음과 같습니다.

입력 단어의 첫 문자가 모음 인지 확인 합니다. 이 경우 "yay"를 단어 끝에 연결 합니다. 그렇지 않으면 첫 번째 문자를 단어의 끝으로 이동 하 여 "ay"를 추가 합니다.

이에 대 한 최종 정보는 다음과 같습니다. 다른 많은 언어와 달리 함수에서 반환할 명시적인 명령이 없습니다. 가 식 기반 F# 이 고 함수 본문의 마지막 식이 반환 값 이기 때문입니다. 는 `if..then..else` 자체로 식 `then` 이므로 블록의 본문이 `else` 나 블록의 본문은 입력 값에 따라 반환 됩니다.

## <a name="moving-your-script-code-into-the-implementation-file"></a>스크립트 코드를 구현 파일로 이동

이 문서의 이전 섹션에서는 초기 함수를 작성 하 고 FSI.EXE를 F# 사용 하 여 대화형으로 실행 하는 코드를 작성 하는 일반적인 첫 번째 단계를 보여 주었습니다. 이를 repl 기반 개발 이라고 하며, 여기서 [repl](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) 은 "읽기-평가-인쇄 루프"를 나타냅니다. 작업을 수행할 때까지 기능을 시험해 볼 수 있는 좋은 방법입니다.

REPL 기반 개발의 다음 단계는 작업 코드를 F# 구현 파일로 이동 하는 것입니다. 그런 다음 F# 컴파일러에서 실행할 수 있는 어셈블리로 컴파일할 수 있습니다.

시작 하려면를 엽니다 `ClassLibraryDemo.fs`.  일부 코드는 이미 여기에 있습니다. 계속 해 서 클래스 정의를 삭제 하 되, [`namespace`](../language-reference/namespaces.md) 선언을 맨 위에 두어야 합니다.

다음으로, 라는 [`module`](../language-reference/modules.md) `PigLatin` 새를 만들고 `toPigLatin` 함수를 다음과 같이 복사 합니다.

[!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/pig-latin.fs#L1-L14)]

그런 다음 `Script.fsx` 파일을 다시 열고 전체 `toPigLatin` 함수를 삭제 하지만 파일에서 다음 두 줄을 유지 해야 합니다.

```fsharp
#load "ClassLibraryDemo.fs"
open ClassLibraryDemo
```

텍스트의 두 줄을 모두 선택 하 고 Alt + Enter를 눌러 FSI.EXE에서 이러한 줄을 실행 합니다. 그러면 Pig 라틴어 라이브러리의 내용이 fsi.exe 프로세스 및 `open` `ClassLibraryDemo` 네임 스페이스에 로드 되어 해당 기능에 액세스할 수 있습니다.

그런 다음 fsi.exe 창에서 앞에서 정의한 `PigLatin` 모듈을 사용 하 여 함수를 호출 합니다.

```console
> PigLatin.toPigLatin "banana";;
val it : string = "ananabay"
> PigLatin.toPigLatin "apple";;
val it : string = "appleyay"
```

성공 이전 처럼 동일한 결과를 얻을 수 있지만 이제는 F# 구현 파일에서 로드 됩니다. 여기서 주요 차이점은 F# 원본 파일이 fsi.exe 뿐만 아니라 어디에서 나 실행할 수 있는 어셈블리로 컴파일되기 때문입니다.

## <a name="summary"></a>요약

이 문서에서는 다음을 배웠습니다.

1. 충돌 Ide를 사용 하 여 Visual Studio Code를 설정 하는 방법
2. 충돌 Ide를 사용 하 F# 여 첫 번째 프로젝트를 만드는 방법입니다.
3. 스크립트를 사용 F# 하 여 fsi.exe에서 첫 F# 번째 함수를 작성 하 고이를에서 실행 하는 방법을 설명 합니다.
4. 스크립트 코드를 F# 소스로 마이그레이션한 다음 fsi.exe에서 해당 코드를 호출 하는 방법을 설명 합니다.

이제 Visual Studio Code 및 이상 Ide를 사용 하 F# 여 훨씬 더 많은 코드를 작성할 준비가 되었습니다.

## <a name="troubleshooting"></a>문제 해결

다음은 발생할 수 있는 특정 문제를 해결할 수 있는 몇 가지 방법입니다.

1. F# 파일을 디스크에 저장 하 고 Visual Studio Code 작업 영역에 열려 있는 폴더 내에 저장 해야 합니다.
2. 시스템이 열려 있는 상태에서 시스템을 변경 하거나 Visual Studio Code를 설치한 경우 Visual Studio Code를 다시 시작 합니다.
3. 정규화 된 경로 없이 명령줄에서 F# 컴파일러와 F# interactive를 사용할 수 있는지 확인 합니다. 이렇게 하려면 F# 컴파일러에 대 한 `fsc` 명령줄을 입력 하 고 `fsi` , 또는 `fsharpi` Windows의 시각적 F# 도구와 Mac/Linux의 Mono를 입력 하면 됩니다.
4. 프로젝트 디렉터리에 잘못 된 문자가 있는 경우에는 작동 하지 않을 수 있습니다.  이 경우 프로젝트 디렉터리의 이름을 바꿉니다.
5. 작동 하는 지 여부 Ide 명령이 없으면 [Visual Studio Code 키 바인딩을](https://code.visualstudio.com/docs/customization/keybindings#_customizing-shortcuts) 확인 하 여 실수로 재정의 하 고 있는지 확인 합니다.
6. 컴퓨터에서 손상 된 ide가 손상 된 경우 어떤 것도 문제가 해결 되지 않으면 컴퓨터에서 디렉터리를 `ionide-fsharp` 제거 하 고 플러그 인 도구 모음을 다시 설치 하세요.

이상 ide는 F# 커뮤니티의 구성원이 빌드하고 유지 관리 하는 오픈 소스 프로젝트입니다. 문제를 보고 하 고 무료 ide-vscode [에 참여 하세요. Fsharp.core GitHub 리포지토리](https://github.com/ionide/ionide-vscode-fsharp).

보고 하는 데 문제가 있는 경우 [문제를 보고할 때 사용할 로그를 가져오는 방법에 대 한 지침](https://github.com/ionide/ionide-vscode-fsharp#how-to-get-logs-for-debugging--issue-reporting)을 따르세요.

이상 ide 개발자와 F# 커뮤니티의 [Gitter channel](https://gitter.im/ionide/ionide-project)에서 추가 도움을 요청할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

F# 및 해당 언어의 기능에 대해 자세히 알아보려면 [둘러보기 F# ](../tour.md)를 참조 하세요.
