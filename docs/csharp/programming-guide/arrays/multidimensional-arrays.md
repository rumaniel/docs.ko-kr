---
title: 다차원 배열(C# 프로그래밍 가이드)
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [C#], multidimensional
- multidimensional arrays [C#]
ms.assetid: 020ce02e-7dff-4273-8e53-bf0b33747232
ms.openlocfilehash: a1d7a0a014c330682316e869f6727082fa3b31ef
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48841089"
---
# <a name="multidimensional-arrays-c-programming-guide"></a>다차원 배열(C# 프로그래밍 가이드)

배열에 둘 이상의 차원이 있을 수 있습니다. 예를 들어 다음 선언은 행 4개, 열 2개의 2차원 배열을 만듭니다.  
  
 [!code-csharp[csProgGuideArrays#11](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_1.cs)]  
  
 다음 선언은 세 가지 차원 4, 2, 3의 배열을 만듭니다.  
  
 [!code-csharp[csProgGuideArrays#12](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_2.cs)]  
  
## <a name="array-initialization"></a>배열 초기화

 다음 예제와 같이 선언 시 배열을 초기화할 수 있습니다.  
  
 [!code-csharp[csProgGuideArrays#13](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_3.cs)]  
  
 차수를 지정하지 않고 배열을 초기화할 수도 있습니다.  
  
 [!code-csharp[csProgGuideArrays#14](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_4.cs)]  
  
 초기화하지 않고 배열 변수를 선언하도록 선택할 경우 `new` 연산자를 사용하여 변수에 배열을 할당해야 합니다. `new` 사용은 다음 예제에서 확인할 수 있습니다.  
  
 [!code-csharp[csProgGuideArrays#15](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_5.cs)]  
  
 다음 예제에서는 특정 배열 요소에 값을 할당합니다.  
  
 [!code-csharp[csProgGuideArrays#16](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_6.cs)]  
  
 마찬가지로, 다음 예제에서는 특정 배열 요소의 값을 가져와 `elementValue` 변수에 할당합니다.  
  
 [!code-csharp[csProgGuideArrays#42](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_7.cs)]  
  
 다음 코드 예제에서는 가변 배열을 제외하고 배열 요소를 기본 값으로 초기화합니다.  
  
 [!code-csharp[csProgGuideArrays#17](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_8.cs)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [배열](../../../csharp/programming-guide/arrays/index.md)  
- [1차원 배열](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)  
- [가변 배열](../../../csharp/programming-guide/arrays/jagged-arrays.md)
