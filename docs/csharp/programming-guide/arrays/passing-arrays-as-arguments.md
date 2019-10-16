---
title: 배열을 인수로 전달 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/05/2018
helpviewer_keywords:
- arrays [C#], passing as arguments
ms.assetid: f3a0971e-c87c-4a1f-8262-bc0a3b712772
ms.openlocfilehash: 1538988c1145a19055074b440f04cbaac4ef7aa7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54741180"
---
# <a name="passing-arrays-as-arguments-c-programming-guide"></a>배열을 인수로 전달(C# 프로그래밍 가이드)

배열을 메서드 매개 변수에 인수로 전달할 수 있습니다. 배열은 참조 형식이므로 메서드를 통해 요소 값을 변경할 수 있습니다.

## <a name="passing-single-dimensional-arrays-as-arguments"></a>1차원 배열을 인수로 전달

초기화된 1차원 배열을 메서드에 전달할 수 있습니다. 예를 들어 다음 문은 인쇄 메서드에 배열을 보냅니다.

[!code-csharp[csProgGuideArrays#34](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#34)]

다음 코드는 인쇄 메서드의 부분 구현을 보여 줍니다.

[!code-csharp[csProgGuideArrays#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#33)]

다음 예제와 같이 한 단계로 새 배열을 초기화하고 전달할 수 있습니다.

[!code-csharp[CsProgGuideArrays#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#35)]

### <a name="example"></a>예제

다음 예제에서는 문자열 배열이 초기화되고 문자열에 대한 `DisplayArray` 메서드에 인수로 전달됩니다. 메서드가 배열 요소를 표시합니다. 다음으로 `ChangeArray` 메서드는 배열 요소를 반대로 전환한 다음, `ChangeArrayElements` 메서드는 배열의 처음 세 요소를 수정합니다. 각 메서드가 반환된 후 `DisplayArray` 메서드는 배열을 값으로 전달해도 배열 요소가 변경되지 않는다는 것을 보여줍니다.

[!code-csharp[csProgGuideArrays#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/ArrayExample.cs)]

## <a name="passing-multidimensional-arrays-as-arguments"></a>다차원 배열을 인수로 전달

초기화된 다차원 배열을 1차원 배열 전달과 동일한 방식으로 메서드에 전달합니다.

[!code-csharp[csProgGuideArrays#41](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#41)]

다음 코드는 2차원 배열을 해당 인수로 허용하는 인쇄 메서드의 부분 선언을 보여 줍니다.

[!code-csharp[csProgGuideArrays#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#36)]

다음 예제와 같이 한 단계로 새 배열을 초기화하고 전달할 수 있습니다.

[!code-csharp[csProgGuideArrays#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#32)]

### <a name="example"></a>예제

다음 예제에서는 정수의 2차원 배열이 초기화되고 `Print2DArray` 메서드에 전달됩니다. 메서드가 배열 요소를 표시합니다.

[!code-csharp[csProgGuideArrays#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#31)]

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [배열](index.md)
- [1차원 배열](single-dimensional-arrays.md)
- [다차원 배열](multidimensional-arrays.md)
- [가변 배열](jagged-arrays.md)
