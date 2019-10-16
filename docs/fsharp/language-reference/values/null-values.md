---
title: Null 값
description: F# 프로그래밍 언어에서 null 값이 사용 되는 방법에 대해 알아봅니다.
ms.date: 03/22/2019
ms.openlocfilehash: 2038c0a461fec9884c51edd50c3c9f336104e30e
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630809"
---
# <a name="null-values"></a>Null 값

이 항목에서는에서 F#null 값이 사용 되는 방법에 대해 설명 합니다.

## <a name="null-value"></a>Null 값

Null 값은 일반적으로 값 또는 변수에 F# 대해에서 사용 되지 않습니다. 그러나 null은 특정 상황에서 비정상 값으로 나타납니다. 형식이에 정의 되어 있는 F#경우 [allownullliteral](https://msdn.microsoft.com/library/4f315196-f444-4cca-ba07-1176ff71eb0f) 특성이 형식에 적용 되지 않는 한 null은 일반 값으로 허용 되지 않습니다. 형식이 다른 .NET 언어에서 정의 된 경우 null은 가능한 값 이며 이러한 형식과 상호 운용할 때 코드에 F# null 값이 발생할 수 있습니다.

에서 F# 정의 되 고 F#에서 엄격 하 게 사용 되는 형식의 경우, 라이브러리를 F# 직접 사용 하 여 Null 값을 만드는 유일한 방법은 [array.zerocreate](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2) [의 Unchecked](https://msdn.microsoft.com/library/9ff97f2a-1bd4-4f4c-afbe-5886a74ab977) 를 사용 하는 것입니다. 그러나 다른 .NET 언어 F# 에서 사용 되는 형식의 경우 또는 .NET Framework와 같이로 작성 F#되지 않은 API로 해당 형식을 사용 하는 경우 null 값이 발생할 수 있습니다.

다른 .net 언어에서 `option` 가능한 null F# 값을 가진 참조 변수를 사용할 수 있는 경우의 형식을 사용할 수 있습니다. `option` 형식이 있는 F# null이 아닌 경우에는 개체가 없는 경우 옵션 값 `None` 을 사용 합니다. 개체를 사용 하는 `Some(obj)` 경우 옵션 값 `obj` 을 개체와 함께 사용 합니다. 자세한 내용은 [옵션](../options.md)을 참조하세요. 의 경우 `null` `Some x`에 는값을옵션으로압축할수있습니다.`x` `null` 따라서 값이 일 `None` `null`때를 사용 하는 것이 중요 합니다.

키워드는 F# 언어에서 유효한 키워드 이며 .NET Framework api 또는 다른 .net 언어로 작성 된 다른 api를 사용 하 여 작업할 때 사용 해야 합니다. `null` Null 값이 필요할 수 있는 두 가지 경우는 .NET API를 호출 하 고, null 값을 인수로 전달 하 고, 반환 값 또는 .NET 메서드 호출에서 출력 매개 변수를 해석할 때입니다.

Null 값을 .net 메서드에 전달 하려면 호출 코드에서 `null` 키워드를 사용 하면 됩니다. 다음 코드 예제에서는 그 구체적인 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet701.fs)]

.NET 메서드에서 얻은 null 값을 해석 하려면 가능 하면 패턴 일치를 사용 합니다. 다음 코드 예제에서는 패턴 일치를 사용 하 여 입력 스트림의 끝을 지나서 읽으려고 할 때에서 `ReadLine` 반환 되는 null 값을 해석 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet702.fs)]

를 사용 `Array.zeroCreate`하 F# 는 경우를 호출 `Unchecked.defaultof`하는 등의 다른 방법으로도 형식의 Null 값을 생성할 수 있습니다. Null 값을 캡슐화 된 상태로 유지 하려면 이러한 코드를 주의 해 서 사용 해야 합니다. 에 F#만 사용 되는 라이브러리에서는 모든 함수에서 null 값을 확인할 필요가 없습니다. 다른 .net 언어와의 상호 운용을 위한 라이브러리를 작성 하는 경우 Visual Basic에는 코드에서 `ArgumentNullException` C# 수행 하는 것과 마찬가지로 null 입력 매개 변수에 대 한 검사를 추가 하 고를 throw 해야 할 수 있습니다.

다음 코드를 사용 하 여 임의의 값이 null 인지 확인할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet703.fs)]

## <a name="see-also"></a>참고자료

- [값](index.md)
- [일치 식](../match-expressions.md)
