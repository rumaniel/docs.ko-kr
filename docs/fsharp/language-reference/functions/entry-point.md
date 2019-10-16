---
title: 진입점
description: 실행 파일로 컴파일되는 F# 프로그램에 진입점을 설정 하는 방법에 대해 알아봅니다 .이 경우 실행은 공식적으로 시작 됩니다.
ms.date: 05/16/2016
ms.openlocfilehash: 5e13416131d4dfd22583439fedf51f18f7a461da
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630527"
---
# <a name="entry-point"></a>진입점

이 항목에서는 F# 프로그램에 대 한 진입점을 설정 하는 데 사용 하는 방법에 대해 설명 합니다.

## <a name="syntax"></a>구문

```fsharp
[<EntryPoint>]
let-function-binding
```

## <a name="remarks"></a>설명

이전 구문에서 *함수-바인딩은* `let` 바인딩의 함수 정의입니다.

실행 파일로 컴파일되는 프로그램의 진입점은 실행이 공식적으로 시작 되는 위치입니다. 프로그램의 F# `EntryPoint` 함수에특성을적용하여응용프로그램에대한진입점을지정합니다.`main` `let` 바인딩을 사용 하 여 만든이 함수는 마지막으로 컴파일된 파일의 마지막 함수 여야 합니다. 마지막으로 컴파일된 파일은 명령줄에 전달 된 마지막 파일 또는 프로젝트의 마지막 파일입니다.

진입점 함수의 형식은 `string array -> int`입니다. 명령줄에 제공 된 인수는 문자열 배열의 `main` 함수에 전달 됩니다. 배열의 첫 번째 요소는 첫 번째 인수입니다. 실행 파일의 이름은 다른 언어에 포함 되어 있으므로 배열에 포함 되지 않습니다. 반환 값은 프로세스에 대 한 종료 코드로 사용 됩니다. 0은 일반적으로 success를 나타냅니다. 0이 아닌 값은 오류를 표시 합니다. 0이 아닌 반환 코드의 특정 의미에 대 한 규칙은 없습니다. 반환 코드의 의미는 응용 프로그램 마다 다릅니다.

다음 예에서는 간단한 `main` 함수를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/entry-point/snippet501.fs)]

명령줄을 사용 하 여이 코드를 실행 `EntryPoint.exe 1 2 3`하는 경우 출력은 다음과 같습니다.

```console
Arguments passed to function : [|"1"; "2"; "3"|]
```

## <a name="implicit-entry-point"></a>암시적 진입점

프로그램에 진입점을 명시적으로 나타내는 **EntryPoint** 특성이 없으면 컴파일할 마지막 파일의 최상위 바인딩이 진입점으로 사용 됩니다.

## <a name="see-also"></a>참고자료

- [함수](index.md)
- [let 바인딩](let-bindings.md)
