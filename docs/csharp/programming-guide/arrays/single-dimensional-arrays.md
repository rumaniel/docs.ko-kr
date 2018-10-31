---
title: 1차원 배열(C# 프로그래밍 가이드)
ms.date: 07/20/2015
helpviewer_keywords:
- single-dimensional arrays [C#]
- arrays [C#], single-dimensional
ms.assetid: 2cec1196-1de0-49d2-baf2-c607c33310e8
ms.openlocfilehash: c2f26fd74a596ada21eef578e58c9cd8e0305d6c
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48027130"
---
# <a name="single-dimensional-arrays-c-programming-guide"></a>1차원 배열(C# 프로그래밍 가이드)

다음 예제와 같이 5개 정수의 1차원 배열을 선언할 수 있습니다.  
  
 [!code-csharp[csProgGuideArrays#4](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_1.cs)]  
  
 이 배열에는 `array[0]` ~ `array[4]`의 요소가 포함되어 있습니다. [new](../../../csharp/language-reference/keywords/new.md) 연산자는 배열을 만들고 배열 요소를 기본값으로 초기화하는 데 사용됩니다. 이 예제에서는 모든 배열 요소가 0으로 초기화됩니다.  
  
 동일한 방식으로 문자열 요소를 저장하는 배열을 선언할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideArrays#5](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_2.cs)]  
  
## <a name="array-initialization"></a>배열 초기화

 선언 시 배열을 초기화할 수 있으며, 이 경우 차수 지정자가 초기화 목록에 있는 요소 수에 의해 제공되기 때문에 지정할 필요가 없습니다. 예:  
  
 [!code-csharp[csProgGuideArrays#6](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_3.cs)]  
  
 문자열 배열도 동일한 방식으로 초기화할 수 있습니다. 다음은 각 배열 요소가 하루의 이름으로 초기화되는 문자열 배열의 선언입니다.  
  
 [!code-csharp[csProgGuideArrays#7](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_4.cs)]  
  
 선언 시 배열을 초기화하면 다음 바로 가기를 사용할 수 있습니다.  
  
 [!code-csharp[csProgGuideArrays#8](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_5.cs)]  
  
 초기화하지 않고 배열 변수를 선언할 수 있지만 이 변수에 배열을 할당할 때 `new` 연산자를 사용해야 합니다. 예:  
  
 [!code-csharp[csProgGuideArrays#9](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_6.cs)]  
  
 C# 3.0에서는 암시적으로 형식화된 배열이 도입되었습니다. 자세한 내용은 [암시적으로 형식화된 배열](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)을 참조하세요.  
  
## <a name="value-type-and-reference-type-arrays"></a>값 형식 및 참조 형식 배열

 다음 배열 선언을 살펴보세요.  
  
 [!code-csharp[csProgGuideArrays#10](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_7.cs)]  
  
 이 문의 결과는 `SomeType`이 값 형식인지 또는 참조 형식인지에 따라 달라집니다. 값 형식인 경우 이 문은 각각 `SomeType` 형식인 10개 요소의 배열을 만듭니다. `SomeType`이 참조 형식인 경우 이 문은 각각 null 참조로 초기화된 10개 요소의 배열을 만듭니다.  
  
 값 형식과 참조 형식에 대한 자세한 내용은 [형식](../../../csharp/language-reference/keywords/types.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Array>  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [배열](../../../csharp/programming-guide/arrays/index.md)  
- [다차원 배열](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)  
- [가변 배열](../../../csharp/programming-guide/arrays/jagged-arrays.md)
