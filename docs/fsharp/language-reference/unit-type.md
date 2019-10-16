---
title: 단위 형식
description: 값이 필요 F# 하거나 원하는 값이 없는 경우 언어 구문에 값이 필요한 위치를 저장 하는 데 ' unit ' 형식이 자주 사용 되는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 4e586702324565b8dcd4f6c7e11a0e1754f89c58
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630168"
---
# <a name="unit-type"></a>단위 형식

형식은 특정 값이 없음을 나타내는 형식입니다 .이 형식에 `unit` 는 다른 값이 없거나 필요 하지 않은 경우 자리 표시자 역할을 하는 단일 값만 있습니다. `unit`

## <a name="syntax"></a>구문

```fsharp
// The value of the unit type.
()
```

## <a name="remarks"></a>설명

모든 F# 식은 값으로 계산 되어야 합니다. 관심이 있는 값을 생성 하지 않는 식의 경우 형식의 `unit` 값이 사용 됩니다. 형식은 및와 같은 `void` 언어의 형식과 유사 합니다. C++ C# `unit`

형식 `unit` 에는 단일 값이 있으며이 값은 토큰 `()`으로 표시 됩니다.

`unit` 형식 값은 언어 구문에 값이 필요한 F# 위치를 포함 하는 프로그래밍에 자주 사용 되며, 값이 필요 하지 않거나 원하는 경우에는 필요 하지 않습니다. 예를 들어 `printf` 함수의 반환 값이 될 수 있습니다. `printf` 작업의 중요 한 작업은 함수에서 발생 하므로 함수는 실제 값을 반환할 필요가 없습니다. 따라서 반환 값은 형식 `unit`입니다.

일부 구문에는 `unit` 값이 있어야 합니다. 예 `do` 를 들어 모듈의 최상위 수준에 있는 바인딩 또는 코드는 `unit` 값으로 계산 되어야 합니다. 다음 예제와 같이 모듈의 최상위 `do` 수준에 있는 바인딩 또는 코드에서 사용 되지 않는 `unit` 값 이외의 결과가 생성 되는 경우 컴파일러는 경고를 보고 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet901.fs)]

이 경고는 함수형 프로그래밍의 특징입니다. 다른 .NET 프로그래밍 언어에는 표시 되지 않습니다. 함수에서 의도 하지 않은 결과가 발생 하지 않는 순수한 함수형 프로그램에서 최종 반환 값은 함수 호출의 유일한 결과입니다. 따라서 결과가 무시 되는 경우 프로그래밍 오류가 발생할 수 있습니다. 는 F# 순수 함수형 프로그래밍 언어가 아니지만 가능 하면 항상 함수형 프로그래밍 스타일을 따르는 것이 좋습니다.

## <a name="see-also"></a>참고자료

- [형식을](primitive-types.md)
- [F# 언어 참조](index.md)
