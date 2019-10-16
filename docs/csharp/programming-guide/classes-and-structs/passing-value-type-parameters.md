---
title: 값 형식 매개 변수 전달 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- method parameters [C#], value types
- parameters [C#], value
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
ms.openlocfilehash: dfd2c39eff44b431ec10d85f855fb015a2391f29
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596247"
---
# <a name="passing-value-type-parameters-c-programming-guide"></a>값 형식 매개 변수 전달(C# 프로그래밍 가이드)
데이터에 대한 참조가 포함되어 있는 [참조 형식](../../language-reference/keywords/reference-types.md) 변수와는 달리, [값 형식](../../language-reference/keywords/value-types.md) 변수에는 해당 데이터가 직접 포함됩니다. 값 형식 변수를 메서드에 값으로 전달하는 것은 변수의 복사본을 메서드에 전달하는 것과 같습니다. 메서드 내에서 수행되는 매개 변수 변경 작업은 인수 변수에 저장된 원래 데이터에는 영향을 주지 않습니다. 호출된 메서드가 인수 값을 변경하도록 하려면 [ref](../../language-reference/keywords/ref.md) 또는 [out](../../language-reference/keywords/out-parameter-modifier.md) 키워드를 사용하여 해당 메서드를 참조로 전달해야 합니다. [in](../../language-reference/keywords/in-parameter-modifier.md) 키워드를 사용하여 값이 변경되지 않도록 보장하는 동안 복사를 방지하도록 참조로 값 매개 변수를 전달할 수도 있습니다. 간단한 설명을 위해 다음 예제에서는 `ref`를 사용합니다.  
  
## <a name="passing-value-types-by-value"></a>값으로 값 형식 전달  
 다음 예제에서는 값 형식 매개 변수를 값으로 전달하는 방법을 보여 줍니다. `n` 변수가 `SquareIt` 메서드에 값으로 전달됩니다. 메서드 내에서 수행되는 변경 작업은 변수의 원래 값에는 영향을 주지 않습니다.  
  
 [!code-csharp[csProgGuideParameters#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#3)]  
  
 `n` 변수는 값 형식이며 값 `5` 5를 데이터로 포함합니다. `SquareIt`을 호출하면 `n`의 내용이 `x` 매개 변수로 복사됩니다. 그러면 메서드 내에서 이 매개 변수의 값을 제곱합니다. 그러나 `Main`에서는 `n`의 값이 `SquareIt` 메서드를 호출한 후에도 호출 전과 동일합니다. 즉, 메서드 내에서 수행되는 변경은 지역 변수 `x`에만 적용됩니다.  
  
## <a name="passing-value-types-by-reference"></a>참조로 값 형식 전달  
 다음 예제는 인수가 `ref` 매개 변수로 전달된다는 점을 제외하면 이전 예제와 동일합니다. 메서드에서 `x`가 변경되면 기본 인수 `n`의 값도 변경됩니다.  
  
 [!code-csharp[csProgGuideParameters#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#4)]  
  
 이 예제에서는 `n`의 값이 아니라 `n`에 대한 참조가 전달됩니다. `x` 매개 변수는 [int](../../language-reference/builtin-types/integral-numeric-types.md)가 아니며 `int`에 대한 참조(이 예제에서는 `n`에 대한 참조)입니다. 그러므로 메서드 내에서 `x`를 제곱할 때 실제로는 `x`가 참조하는 `n`을 제곱하게 됩니다.  
  
## <a name="swapping-value-types"></a>값 형식 교환  
 인수의 값을 변경하는 일반적인 예로는 두 변수를 메서드에 전달하면 메서드가 변수의 내용을 교환하는 swap 메서드가 있습니다. 이때 인수는 swap 메서드에 참조로 전달해야 합니다. 이렇게 하지 않으면 메서드 내에서 매개 변수의 로컬 복사본이 교환되므로 호출하는 메서드에서는 변경이 수행되지 않습니다. 다음 예제에서는 정수 값을 바꿉니다.  
  
 [!code-csharp[csProgGuideParameters#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#5)]  
  
 `SwapByRef` 메서드를 호출할 때는 다음 예제와 같이 호출에 `ref` 키워드를 사용합니다.  
  
 [!code-csharp[csProgGuideParameters#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#6)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [매개 변수 전달](./passing-parameters.md)
- [참조 형식 매개 변수 전달](./passing-reference-type-parameters.md)
