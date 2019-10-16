---
title: 형식 약어
description: 코드를 F# 보다 쉽게 읽을 수 있도록 형식에 더 의미 있는 이름을 지정 하는 형식 약어에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 339b22a675e3f1ad8a3da207053e611942b55a22
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630205"
---
# <a name="type-abbreviations"></a>형식 약어

*형식 약어* 는 형식에 대 한 별칭 또는 대체 이름입니다.

## <a name="syntax"></a>구문

```fsharp
type [accessibility-modifier] type-abbreviation = type-name
```

## <a name="remarks"></a>설명

코드를 보다 쉽게 읽을 수 있도록 형식 약어를 사용 하 여 형식에 더 의미 있는 이름을 지정할 수 있습니다. 이를 사용 하 여 작성 하기 어려운 형식에 대해 사용 하기 쉬운 이름을 만들 수도 있습니다. 또한 형식을 사용 하는 모든 코드를 변경 하지 않고 형식 약어를 사용 하 여 기본 형식을 쉽게 변경할 수 있습니다. 다음은 단순 형식 약어입니다.

약어 형식의 액세스 가능성은 기본적 `public`으로로 설정 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2301.fs)]

형식 약어에는 다음 코드와 같이 제네릭 매개 변수가 포함 될 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2302.fs)]

이전 코드 `Transform` 에서는 모든 형식의 단일 인수를 사용 하 고 동일한 형식의 단일 값을 반환 하는 함수를 나타내는 형식 약어입니다.

형식 약어는 .NET Framework MSIL 코드에서 유지 되지 않습니다. 따라서 다른 .NET Framework 언어의 F# 어셈블리를 사용 하는 경우 형식 약어에 대해 기본 형식 이름을 사용 해야 합니다.

형식 약어를 측정 단위에 사용할 수도 있습니다. 자세한 내용은 [측정 단위](units-of-measure.md)를 참조 하세요.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
