---
title: Mac 용 Visual Studio에서 F# 시작
description: Mac 용 Visual Studio에서 F#을 사용하는 방법을 알아봅니다.
ms.date: 07/03/2018
ms.openlocfilehash: d3604178f93cf17d21f25b09084be7e7977378b5
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71082971"
---
# <a name="get-started-with-f-in-visual-studio-for-mac"></a>Mac 용 Visual Studio에서 F# 시작

F#과 F# Visual 도구가 Mac IDE용 Visual Studio에서 지원됩니다. [Mac용 Visual Studio의 설치](install-fsharp.md#install-f-with-visual-studio-for-mac)를 확인합니다.

## <a name="creating-a-console-application"></a>콘솔 응용 프로그램 만들기

Mac 용 Visual Studio에서 가장 기본적인 프로젝트 중 하나는 콘솔 응용 프로그램입니다.  방법은 다음과 같습니다.  Mac 용 Visual Studio를 열고

1. **파일** 메뉴에서 **새 솔루션**을 선택합니다.

2. 새 프로젝트 대화 상자에 두 개의 다른 콘솔 응용 프로그램 템플릿이 존재합니다.  기타 -> .NET에는 .NET Framework를 대상으로 하는 템플릿이 존재합니다.  나머지 템플릿은 .NET Core -> App에 존재하며 .NET Core를 대상으로 합니다.  이 템플릿은 이 문서의 목적에 맞게 동작합니다.

3. 필요에 따라 콘솔 앱을 C#에서 F#으로 변경합니다.  다음으로 진행하기 위해 **다음**버튼을 선택합니다.  

4. 프로젝트 이름을 지정하고 앱에서 사용할 옵션을 선택합니다.  화면 측면의 미리 보기 창에는 선택한 옵션을 기반으로 생성될 디렉터리 구조가 표시됩니다.  

5. **만들기**를 클릭합니다.  이제는 솔루션 탐색기에서 F# 프로젝트를 볼 수 있습니다.

## <a name="writing-your-code"></a>코드 작성

먼저 코드 작성으로 시작하세요.  `Program.fs` 파일을 열고 다음 내용으로 변경합니다.

[!code-fsharp[HelloSquare](~/samples/snippets/fsharp/getting-started/hello-square.fs)]

이 코드 샘플에서는 입력으로 `x`를 가져와 자신과 곱셈하도록 정의된 `square`함수가 정의되어 있습니다.  F#에서는 [Typeinference](../language-reference/type-inference.md)를 사용하기 때문에 `x`의 형식을 지정할 필요가 없습니다.  F# 컴파일러는 곱셈에서 유효한 형식을 이해하고 `square`가 호출되는 방식에 따라 `x`의 형식을 할당합니다.  `square` 위로 마우스를 가져가면 다음과 같이 표시됩니다.

```console
val square: x:int -> int
```

이것을 함수 형식 시그니처라고 합니다.  다음과 같이 "square는 정수 x를 사용하고 정수를 생성하는 함수"라고 읽을 수 있습니다.  컴파일러가 `square`를 `int`형식으로 지정한 것에 주목하십시오. 곱셈은 *모든* 형식에서 제네릭이 아니라, 폐쇄형 집합 형식에서 제네릭이기 때문입니다.  F# 컴파일러에서 지금은 `int`를 선택하지만, `float` 같은 다른 입력 형식으로 `square`를 호출 하는 경우는 형식 시그니처가 조정됩니다.

그 밖에 `main` 함수가 정의되고 F# 컴파일러에게 프로그램 수행이 시작되는 곳이라는 것을 알려주는 `EntryPoint`속성이 데코레이트되었습니다.  함수에 명령줄 인수를 전달하고 정수 코드(일반적으로 `0`)를 반환하는 [C 스타일 프로그래밍 언어](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B)와 동일한 규칙을 따릅니다.

이 함수에서는 인수로 `12`를 사용하여 `square` 함수를 호출합니다.  F# 컴파일러에는 `square`의 형식을 `int -> int`가 되도록 할당합니다(이것이 `int`를 가지고 `int`를 생성하는 함수입니다).  `printfn` 호출은 서식이 지정된 출력 기능으로, C 스타일 프로그래밍 언어와 유사한 형식 문자열을 사용하고, 형식 문자열의 서식이 지정된 매개 변수와 결과를 새로운 라인에 출력합니다.

## <a name="running-your-code"></a>코드 실행

최상단 메뉴에서 **실행**과 **디버깅하지 않고 시작**을 순서대로 클릭하여 코드를 실행하고 그 결과를 확인할 수 있습니다.  이렇게 하면 디버깅을 하지 않고 프로그램을 실행하여 그 결과 볼 수 있습니다.

이제 Mac 용 Visual Studio의 콘솔 창에서 다음 내용이 표시되는 것을 볼 수 있습니다.

```console
12 squared is 144!
```

축하합니다.  지금까지 Mac 용 Visual Studio에서 첫 번째 F# 프로젝트를 만들고, 함수를 호출하면 그 결과를 출력하는 F# 함수를 작성하고, 결과를 확인하기 위해 실행해 보았습니다.

## <a name="using-f-interactive"></a>F# 대화형 사용

Mac용 Visual Studio에서 가장 유용한 Visual F# 도구는 F# 대화형 창입니다.  여기서 코드를 호출하여 대화형으로 결과를 볼 수 있는 프로세스로 코드를 보낼 수 있습니다.

사용을 시작하려면 코드에 정의된 `square` 함수를 강조 표시합니다.  다음으로 최상위 메뉴에서 **편집**을 클릭합니다.  다음으로 **F# 대화형으로 참조 보내기**를 선택합니다.  이렇게 하면 F# 대화형 창에서 코드가 실행됩니다.  또는 선택 항목에서 마우스 오른쪽 버튼으로 클릭하고 **F# 대화형으로 참조 보내기**를 선택합니다.  F# 대화형 창에 다음과 같이 나타나야 합니다.

```console
>

val square : x:int -> int

>
```

여기서는 이전에 함수 위에 마우스를 가져 갔을 때 보았던 `square` 함수와 동일한 함수 시그니처를 보여줍니다.  이제 `square`는 F# 대화형 프로세스로 정의되었기 때문에 다음과 같이 다른 값으로 호출할 수 있습니다.

```console
> square 12;;
val it : int = 144
>square 13;;
val it : int = 169
```

여기서는 함수를 실행하고 그 결과를 새로운 이름 `it`으로 바인드하며, `it`의 유형과 값을 표시합니다.  각 행은 `;;`로 끝나야 합니다.  이것은 F# 대화형에서 함수 호출이 끝났을 때를 알 수 있는 방법입니다.  다음과 같이 F# 대화형에서 새 함수를 정의할 수도 있습니다.

```console
> let isOdd x = x % 2 <> 0;;

val isOdd : x:int -> bool

> isOdd 12;;
val it : bool = false
```

위의 함수는 새로운 함수 `isOdd`를 정의합니다. `isOdd`는 `int`를 취해 홀수인지 확인합니다.  이 함수를 호출하여 다른 입력 값으로 무엇이 반환되는지 확인할 수 있습니다.  함수 호출 내에서 함수를 호출할 수 있습니다.

```console
> isOdd (square 15);;
val it : bool = true
```

다음과 같이 두 함수에 값을 전달하기 위해 [파이프 전달 연산자](../language-reference/symbol-and-operator-reference/index.md)를 사용할 수도 있습니다.

```console
> 15 |> square |> isOdd;;
val it : bool = true
```

파이프 전달 연산자 등은 나중에 자습서에서 설명합니다.

이는 F# 대화형을 통해 할 수 있는 일을 간략하게 보여준 것입니다.  자세한 내용은 [F#을 사용한 대화형 프로그래밍](../tutorials/fsharp-interactive/index.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

아직 확인하지 않았다면 F# 언어의 핵심 기능 중 일부를 다루는 [F# 둘러보기](../tour.md)를 확인해보세요.  F#의 기능 중 일부에 대한 개요를 제공하고 Mac용 Visual Studio로 복사하여 실행할 수 있는 풍부한 코드 샘플을 제공합니다.  [F# 가이드](../index.md)에서 소개된 훌륭한 외부 리소스도 있습니다.

## <a name="see-also"></a>참고자료

- [Visual F#](../index.md)
- [F# 둘러보기](../tour.md)
- [F# 언어 참조](../language-reference/index.md)
- [형식 유추](../language-reference/type-inference.md)
- [기호 및 연산자 참조](../language-reference/symbol-and-operator-reference/index.md)
