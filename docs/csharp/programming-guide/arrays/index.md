---
title: 배열 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [C#]
- C# language, arrays
ms.assetid: bb79bdde-e570-4c30-adb0-1dd5759ae041
ms.openlocfilehash: 24c6d54c3fe92ada661e732adec582e87ab62417
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597525"
---
# <a name="arrays-c-programming-guide"></a>배열(C# 프로그래밍 가이드)

배열 데이터 구조에 형식이 동일한 변수를 여러 개 저장할 수 있습니다. 요소의 형식을 지정하여 배열을 선언합니다.  
  
 `type[] arrayName;`  
  
 다음 예제에서는 단일 차원, 다차원 및 가변 배열을 만듭니다.  
  
 [!code-csharp[csProgGuideArrays#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#1)]  
  
## <a name="array-overview"></a>배열 개요

 배열에는 다음과 같은 속성이 있습니다.  
  
- 배열은 [단일 차원](./single-dimensional-arrays.md), [다차원](./multidimensional-arrays.md) 또는 [가변](./jagged-arrays.md)일 수 있습니다.  
  
- 차원 수와 각 차원의 길이는 배열 인스턴스를 만들 때 설정됩니다. 이러한 값은 인스턴스의 수명 동안 변경할 수 없습니다.  
  
- 숫자 배열 요소의 기본값은 0으로 설정되고, 참조 요소는 null로 설정됩니다.  
  
- 가변 배열은 여러 배열로 구성되어 있기 때문에 해당 요소가 참조 형식이며, `null`로 초기화됩니다.  
  
- 배열은 0으로 인덱싱됩니다. `n` 요소는 `0`부터 `n-1`로 인덱싱됩니다.  
  
- 배열 요소 형식은 배열 형식을 비롯한 어떤 형식도 될 수 있습니다.  
  
- 배열 형식은 <xref:System.Array> 추상 기본 형식에서 파생된 [참조 형식](../../language-reference/keywords/reference-types.md)입니다. 이 형식은 <xref:System.Collections.IEnumerable> 및 <xref:System.Collections.Generic.IEnumerable%601>을 구현하므로 C#의 모든 배열에서 [foreach](../../language-reference/keywords/foreach-in.md) 반복을 사용할 수 있습니다.  
  
## <a name="related-sections"></a>관련 단원  
  
- [개체로 사용되는 배열](./arrays-as-objects.md)  
  
- [배열에 foreach 사용](./using-foreach-with-arrays.md)  
  
- [인수로 배열 전달](./passing-arrays-as-arguments.md)  
  
## <a name="c-language-specification"></a>C# 언어 사양

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [컬렉션](../concepts/collections.md)
