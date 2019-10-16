---
title: 참조 형식 매개 변수 전달 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- method parameters [C#], reference types
- parameters [C#], reference
ms.assetid: 9e6eb65c-942e-48ab-920a-b7ba9df4ea20
ms.openlocfilehash: f4329c525995b8246427072d1f537d91d875ef95
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596270"
---
# <a name="passing-reference-type-parameters-c-programming-guide"></a>참조 형식 매개 변수 전달(C# 프로그래밍 가이드)
[참조 형식](../../language-reference/keywords/reference-types.md)의 변수에는 해당 데이터가 직접 포함되지 않고 데이터에 대한 참조가 포함됩니다. 참조 형식 매개 변수를 값으로 전달하는 경우 클래스 멤버 값 등 참조된 개체에 속하는 데이터를 변경할 수 있습니다. 하지만 참조 자체의 값은 변경할 수 없습니다. 예를 들어 동일한 참조를 사용하여 새 개체에 대한 메모리를 할당하고 메서드 외부에 유지되도록 할 수 없습니다. 이렇게 하려면 [ref](../../language-reference/keywords/ref.md) 또는 [out](../../language-reference/keywords/out-parameter-modifier.md) 키워드를 사용하여 매개 변수를 전달합니다. 간단한 설명을 위해 다음 예제에서는 `ref`를 사용합니다.  
  
## <a name="passing-reference-types-by-value"></a>값으로 참조 형식 전달  
 다음 예제에서는 참조 형식 매개 변수 `arr`을 `Change` 메서드에 값으로 전달하는 방법을 보여 줍니다. 매개 변수가 `arr`에 대한 참조이므로 배열 요소의 값을 변경할 수 있습니다. 그러나 다른 메모리 위치에 매개 변수를 다시 할당하려는 시도는 메서드 내부에서만 작동하고 원래 변수 `arr`에는 영향을 주지 않습니다.  
  
 [!code-csharp[csProgGuideParameters#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#7)]  
  
 앞의 예제에서 참조 형식인 `arr` 배열은 `ref` 매개 변수 없이 메서드에 전달됩니다. 이 경우 `arr`을 가리키는 참조의 복사본이 메서드에 전달됩니다. 출력에서는 이 경우 메서드가 배열 요소의 내용을 `1`에서 `888`로 변경할 수 있음을 보여 줍니다. 그러나 `Change` 메서드 내에서 [new](../../language-reference/operators/new-operator.md) 연산자를 사용하여 새 메모리 부분을 할당하면 `pArray` 변수가 새 배열을 참조합니다. 따라서 그 후의 변경 내용은 `Main` 내에서 생성된 원래 배열 `arr`에 영향을 주지 않습니다. 실제로 이 예제에서는 `Main` 내부와 `Change` 메서드 내부에 각각 하나씩, 두 개의 배열이 생성됩니다.  
  
## <a name="passing-reference-types-by-reference"></a>참조로 참조 형식 전달  
 다음 예제는 `ref` 키워드가 메서드 헤더 및 호출에 추가된다는 점을 제외하고 앞의 예제와 동일합니다. 메서드에서 발생하는 모든 변경 내용이 호출하는 프로그램의 원래 변수에 영향을 줍니다.  
  
 [!code-csharp[csProgGuideParameters#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#8)]  
  
 메서드 내에서 발생하는 모든 변경 내용은 `Main`의 원래 배열에 영향을 줍니다. 실제로 원래 배열은 `new` 연산자를 사용하여 다시 할당됩니다. 따라서 `Change` 메서드를 호출한 후 `arr`에 대한 모든 참조는 `Change` 메서드에서 생성된 5개 요소의 배열을 가리킵니다.  
  
## <a name="swapping-two-strings"></a>두 문자열 교환  
 문자열 교환은 참조 형식 매개 변수를 참조로 전달하는 좋은 예입니다. 예제에서는 두 개의 문자열 `str1` 및 `str2`가 `Main`에서 초기화되고 `ref` 키워드로 수정되는 매개 변수로 `SwapStrings` 메서드에 전달됩니다. 두 문자열이 메서드 및 `Main` 내에서 교환됩니다.  
  
 [!code-csharp[csProgGuideParameters#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#9)]  
  
 이 예제에서는 호출하는 프로그램의 변수에 영향을 주기 위해 매개 변수를 참조로 전달해야 합니다. 메서드 헤더와 메서드 호출 모두에서 `ref` 키워드를 제거하는 경우 호출하는 프로그램에서는 아무것도 변경되지 않습니다.  
  
 문자열에 대한 자세한 내용은 [문자열](../../language-reference/keywords/string.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [매개 변수 전달](./passing-parameters.md)
- [ref](../../language-reference/keywords/ref.md)
- [in](../../language-reference/keywords/in-parameter-modifier.md)
- [out](../../language-reference/keywords/out.md)
- [참조 형식](../../language-reference/keywords/reference-types.md)
