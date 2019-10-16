---
title: 네임스페이스
description: F# 네임 스페이스를 사용 하 여 프로그램 요소 그룹에 이름을 첨부 하 여 관련 기능 영역으로 코드를 구성 하는 방법을 알아봅니다.
ms.date: 12/08/2018
ms.openlocfilehash: d295f25cae81bc28b4fcb522bdcacde862f9517a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627381"
---
# <a name="namespaces"></a>네임스페이스

네임 스페이스를 사용 하면 F# 프로그램 요소 그룹에 이름을 첨부 하 여 코드를 관련 기능 영역으로 구성할 수 있습니다. 네임 스페이스는 일반적으로 파일의 F# 최상위 요소입니다.

## <a name="syntax"></a>구문

```fsharp
namespace [rec] [parent-namespaces.]identifier
```

## <a name="remarks"></a>설명

네임 스페이스에 코드를 저장 하려면 파일의 첫 번째 선언에서 네임 스페이스를 선언 해야 합니다. 그러면 파일의 다른 네임 스페이스 선언이 추가로 존재 하지 않는 경우 전체 파일의 내용이 네임 스페이스의 일부가 됩니다. 이 경우 다음 네임 스페이스 선언이 첫 번째 네임 스페이스 내에 있는 것으로 간주 될 때까지 모든 코드를 처리 합니다.

네임 스페이스에는 값과 함수를 직접 포함할 수 없습니다. 대신, 값 및 함수는 모듈에 포함 되어야 하며, 모듈은 네임 스페이스에 포함 되어 있습니다. 네임 스페이스는 형식 모듈을 포함할 수 있습니다.

XML 문서 주석은 네임 스페이스 위에 선언 될 수 있지만 무시 됩니다. 컴파일러 지시문은 네임 스페이스 위에 선언 될 수도 있습니다.

네임 스페이스는 네임 스페이스 키워드를 사용 하 여 명시적으로 선언 하거나 모듈을 선언할 때 암시적으로 선언할 수 있습니다. 네임 스페이스를 명시적으로 선언 하려면 namespace 키워드와 네임 스페이스 이름을 차례로 사용 합니다. 다음 예제에서는 형식 및 해당 네임 스페이스에 포함 된 `Widgets` 모듈을 사용 하 여 네임 스페이스를 선언 하는 코드 파일을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6406.fs)]

파일의 전체 내용이 한 모듈에 있는 경우 `module` 키워드를 사용 하 고 정규화 된 모듈 이름에 새 네임 스페이스 이름을 제공 하 여 네임 스페이스를 암시적으로 선언할 수도 있습니다. 다음 예제에서는 함수를 포함 하는 네임 스페이스 `Widgets` 및 모듈 `WidgetsModule`을 선언 하는 코드 파일을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6401.fs)]

다음 코드는 앞의 코드와 동일 하지만 모듈은 로컬 모듈 선언입니다. 이 경우 네임 스페이스는 자체 줄에 표시 되어야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/namespaces/snippet6402.fs)]

하나 이상의 네임 스페이스에서 둘 이상의 모듈이 동일한 파일에 필요한 경우에는 로컬 모듈 선언을 사용 해야 합니다. 로컬 모듈 선언을 사용 하는 경우 모듈 선언에서 정규화 된 네임 스페이스를 사용할 수 없습니다. 다음 코드는 네임 스페이스 선언 및 두 개의 로컬 모듈 선언이 있는 파일을 보여 줍니다. 이 경우 모듈은 네임 스페이스에 직접 포함 됩니다. 파일과 이름이 같은 암시적으로 생성 된 모듈이 없습니다. `do` 바인딩과 같은 파일의 다른 모든 코드는 네임 스페이스에 있지만 내부 모듈에는 없지만 모듈 이름을 사용 하 여 모듈 멤버 `widgetFunction` 를 정규화 해야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6403.fs)]

이 예제의 출력은 다음과 같습니다.

```fsharp
Module1 10 20
Module2 5 6
```

자세한 내용은 [모듈](modules.md)을 참조 하세요.

## <a name="nested-namespaces"></a>중첩 된 네임 스페이스

중첩 된 네임 스페이스를 만드는 경우 정규화 해야 합니다. 그렇지 않으면 새 최상위 네임 스페이스를 만듭니다. 네임 스페이스 선언에서는 들여쓰기가 무시 됩니다.

다음 예제에서는 중첩 된 네임 스페이스를 선언 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6404.fs)]

## <a name="namespaces-in-files-and-assemblies"></a>파일 및 어셈블리의 네임 스페이스

네임 스페이스는 단일 프로젝트 또는 컴파일에서 여러 파일에 걸쳐 있을 수 있습니다. *네임 스페이스 조각* 이라는 용어는 한 파일에 포함 된 네임 스페이스 부분을 설명 합니다. 네임 스페이스는 여러 어셈블리에 걸쳐 있을 수도 있습니다. 예를 들어, `System` 네임 스페이스는 많은 어셈블리에 걸쳐 있고 여러 개의 중첩 된 네임 스페이스를 포함 하는 전체 .NET Framework를 포함 합니다.

## <a name="global-namespace"></a>전역 네임 스페이스

미리 정의 된 네임 스페이스 `global` 를 사용 하 여 .net 최상위 네임 스페이스에 이름을 배치 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6407.fs)]

또한 전역을 사용 하 여 최상위 .NET 네임 스페이스를 참조할 수 있습니다. 예를 들어 다른 네임 스페이스와의 이름 충돌을 해결할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6408.fs)]

## <a name="recursive-namespaces"></a>재귀 네임 스페이스

네임 스페이스를 재귀적으로 선언 하 여 포함 된 모든 코드가 상호 재귀 되도록 할 수도 있습니다.  이 작업은를 `namespace rec`통해 수행 됩니다. 를 사용 `namespace rec` 하면 형식 및 모듈 간에 상호 참조 코드를 작성할 수 없는 일부 pains을 완화할 수 있습니다. 이에 대 한 예는 다음과 같습니다.

```fsharp
namespace rec MutualReferences

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

예외 `DontSqueezeTheBananaException` 와 클래스 `Banana` 는 둘 다 서로를 참조 합니다.  또한 모듈과 `BananaHelpers` 클래스가 `Banana` 서로를 참조 합니다. 네임 스페이스에서 F# `rec` 키워드를 제거 하는 경우에는이를 표현할 수 없습니다. `MutualReferences`

이 기능은 최상위 [모듈](modules.md)에도 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [모듈](modules.md)
- [F#RFC FS-1009-파일 내에서 더 큰 범위에 대해 상호 참조 형식 및 모듈 허용](https://github.com/fsharp/fslang-design/blob/master/FSharp-4.1/FS-1009-mutually-referential-types-and-modules-single-scope.md)
