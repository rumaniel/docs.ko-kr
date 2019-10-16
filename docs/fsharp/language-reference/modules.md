---
title: 모듈
description: 모듈이 프로그램의 값, 형식 및 함수 F# 값과 같은 코드를 그룹화 하는 방법에 대해 알아봅니다. F# F#
ms.date: 04/24/2017
ms.openlocfilehash: 685ab638e7e1b6c8d47d1a316483abcc18e40199
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627430"
---
# <a name="modules"></a>모듈

언어의 컨텍스트에서 *모듈* 은 F# 프로그램의 값, 형식 및 함수 값 F# 과 같은 코드의 그룹입니다. F# 모듈로 코드를 그룹화하면 관련 코드를 함께 유지하고, 프로그램의 이름 충돌을 방지하는 데 도움이 됩니다.

## <a name="syntax"></a>구문

```fsharp
// Top-level module declaration.
module [accessibility-modifier] [qualified-namespace.]module-name
declarations
// Local module declaration.
module [accessibility-modifier] module-name =
    declarations
```

## <a name="remarks"></a>설명

F# 모듈은 형식, 값, F# 함수 값 `do` 및 바인딩의 코드와 같은 코드 구문의 그룹화입니다. 정적 멤버만 있는 CLR (공용 언어 런타임) 클래스로 구현 됩니다. 모듈 선언에는 전체 파일이 모듈에 포함 되는지 여부에 따라 최상위 모듈 선언과 로컬 모듈 선언이 있습니다. 최상위 모듈 선언에는 모듈의 전체 파일이 포함 됩니다. 최상위 모듈 선언은 파일의 첫 번째 선언 으로만 표시 될 수 있습니다.

최상위 모듈 선언에 대 한 구문에서 정규화 된 선택적 *네임 스페이스* 는 모듈이 포함 된 중첩 된 네임 스페이스 이름의 시퀀스입니다. 정규화 된 네임 스페이스는 이전에 선언 하지 않아도 됩니다.

최상위 모듈에서 선언을 들여쓸 필요가 없습니다. 로컬 모듈의 모든 선언을 들여씁니다. 로컬 모듈 선언에서 해당 모듈 선언 아래에 들여쓰기 된 선언만 모듈의 일부입니다.

코드 파일이 최상위 모듈 선언이 나 네임 스페이스 선언으로 시작 하지 않는 경우 로컬 모듈을 포함 하 여 파일의 전체 내용은 확장명이 없는 파일의 이름과 같은 암시적으로 생성 된 최상위 모듈의 일부가 됩니다. 첫 문자가 대문자로 변환 된입니다. 예를 들어 다음 파일을 살펴보십시오.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6601.fs)]

이 파일은 다음과 같은 방식으로 작성 된 것 처럼 컴파일됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6602.fs)]

파일에 모듈이 여러 개 있는 경우 각 모듈에 대해 로컬 모듈 선언을 사용 해야 합니다. 바깥쪽 네임 스페이스를 선언 하는 경우 이러한 모듈은 바깥쪽 네임 스페이스의 일부입니다. 바깥쪽 네임 스페이스가 선언 되지 않은 경우 모듈은 암시적으로 생성 된 최상위 모듈의 일부가 됩니다. 다음 코드 예제에서는 여러 개의 모듈이 포함 된 코드 파일을 보여 줍니다. 컴파일러는 이라는 `Multiplemodules`최상위 모듈을 암시적으로 만들며 `MyModule1` , 및 `MyModule2` 는 해당 최상위 모듈에 중첩 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6603.fs)]

프로젝트에 여러 파일이 있거나 단일 컴파일에서 있거나 라이브러리를 빌드하는 경우에는 파일 맨 위에 네임 스페이스 선언 또는 모듈 선언을 포함 해야 합니다. 프로젝트 F# 또는 컴파일 명령줄에 파일이 하나만 있고 응용 프로그램을 만드는 경우에만 컴파일러에서 모듈 이름을 암시적으로 결정 합니다.

*액세스 가능성 한정자* 는, `public` `private`, `internal`중 하나일 수 있습니다. 자세한 내용은 [액세스 제어](access-control.md)를 참조하세요. 기본값은 public입니다.

## <a name="referencing-code-in-modules"></a>모듈의 코드 참조

다른 모듈에서 함수, 형식 및 값을 참조 하는 경우 정규화 된 이름을 사용 하거나 모듈을 열어야 합니다. 정규화 된 이름을 사용 하는 경우 네임 스페이스, 모듈 및 원하는 프로그램 요소에 대 한 식별자를 지정 해야 합니다. 다음과 같이 정규화 된 경로의 각 부분을 점 (.)으로 구분 합니다.

`Namespace1.Namespace2.ModuleName.Identifier`

모듈 또는 하나 이상의 네임 스페이스를 열어 코드를 단순화할 수 있습니다. 네임 스페이스 및 모듈을 여는 방법에 대 [한 자세한 내용은 가져오기 선언을 참조 하세요. `open` 키워드](import-declarations-the-open-keyword.md)입니다.

다음 코드 예제에서는 파일의 끝까지 모든 코드를 포함 하는 최상위 모듈을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6604.fs)]

동일한 프로젝트의 다른 파일에서이 코드를 사용 하려면 다음 예제와 같이 함수를 사용 하기 전에 정규화 된 이름을 사용 하거나 모듈을 열어야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6605.fs)]

## <a name="nested-modules"></a>중첩 모듈

모듈은 중첩할 수 있습니다. 내부 모듈은 새 모듈이 아니라 내부 모듈 임을 나타내기 위해 바깥쪽 모듈 선언 만큼 바깥쪽으로 들여쓰기 되어야 합니다. 예를 들어 다음 두 예제를 비교해 보십시오. 모듈 `Z` 은 다음 코드의 내부 모듈입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6607.fs)]

그러나 모듈 `Z` 은 다음 코드의 형제의 `Y` to module입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6608.fs)]
모듈은 모듈 `Y`의 다른 선언과 같이 들여쓰기 되지 않으므로 다음 코드의 형제 모듈 이기도 합니다. `Z`

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6609.fs)]
마지막으로 외부 모듈에 선언이 없고 다른 모듈 선언 바로 뒤에 오는 경우 새 모듈 선언이 내부 모듈로 간주 되지만 두 번째 모듈 정의가 두 번째 모듈 정의가 보다 더 들여쓰기 되지 않으면 컴파일러에서 경고를 표시 합니다. 기본.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6610.fs)]
이 경고를 제거 하려면 내부 모듈을 들여씁니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6611.fs)]
파일의 모든 코드를 하나의 외부 모듈에 포함 하 고 내부 모듈을 원하는 경우 외부 모듈은 등호를 요구 하지 않고 외부 모듈에 포함 되는 모든 내부 모듈 선언을 포함 한 선언을 들여쓸 필요가 없습니다. 내부 모듈 선언 내의 선언을 들여씁니다. 다음 코드에서는이 경우를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/modules/snippet6612.fs)]

## <a name="recursive-modules"></a>재귀 모듈

F#4.1에는 포함 된 모든 코드를 상호 재귀 하는 데 사용할 수 있는 모듈의 개념이 도입 되었습니다.  이 작업은를 `module rec`통해 수행 됩니다.  를 사용 `module rec` 하면 형식 및 모듈 간에 상호 참조 코드를 작성할 수 없는 일부 pains을 완화할 수 있습니다.  이에 대 한 예는 다음과 같습니다.

```fsharp
module rec RecursiveModule =
    type Orientation = Up | Down
    type PeelState = Peeled | Unpeeled

    // This exception depends on the type below.
    exception DontSqueezeTheBananaException of Banana

    type BananaPeel() = class end

    type Banana(orientation : Orientation) =
        member val IsPeeled = false with get, set
        member val Orientation = orientation with get, set
        member val Sides: PeelState list = [ Unpeeled; Unpeeled; Unpeeled; Unpeeled] with get, set

        member self.Peel() = BananaHelpers.peel self // Note the dependency on the BananaHelpers module.
        member self.SqueezeJuiceOut() = raise (DontSqueezeTheBananaException self) // This member depends on the exception above.

    module BananaHelpers =
        let peel (b: Banana) =
            let flip (banana: Banana) =
                match banana.Orientation with
                | Up -> 
                    banana.Orientation <- Down
                    banana
                | Down -> banana

            let peelSides (banana: Banana) =
                banana.Sides
                |> List.map (function
                             | Unpeeled -> Peeled
                             | Peeled -> Peeled)

            match b.Orientation with
            | Up ->   b |> flip |> peelSides
            | Down -> b |> peelSides
```

예외 `DontSqueezeTheBananaException` 와 클래스 `Banana` 는 둘 다 서로를 참조 합니다.  또한 모듈과 `BananaHelpers` 클래스가 `Banana` 서로를 참조 합니다.  모듈에서 `rec` 키워드를 제거 하는 경우 F# 에는이를 표현할 수 없습니다. `RecursiveModule`

4\.1를 사용 하 F# 는 [네임 스페이스](namespaces.md) 에서도이 기능을 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [네임스페이스](namespaces.md)
- [F#RFC FS-1009-파일 내에서 더 큰 범위에 대해 상호 참조 형식 및 모듈 허용](https://github.com/fsharp/fslang-design/blob/master/FSharp-4.1/FS-1009-mutually-referential-types-and-modules-single-scope.md)
