---
title: 제네릭 메서드(C# 프로그래밍 가이드)
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], methods
ms.assetid: 673eeea2-4b48-4faa-9c4e-2e89449221b9
ms.openlocfilehash: c6846b28813273cf99334b0427e304651e4cf5ee
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50187168"
---
# <a name="generic-methods-c-programming-guide"></a>제네릭 메서드(C# 프로그래밍 가이드)
제네릭 메서드는 다음과 같은 형식 매개 변수를 사용하여 선언된 메서드입니다.  
  
 [!code-csharp[csProgGuideGenerics#22](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_1.cs)]  
  
 다음 코드 예제는 형식 인수에 `int`를 사용하여 메서드를 호출하는 한 가지 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideGenerics#23](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_2.cs)]  
  
 형식 인수를 생략하고 컴파일러에서 이를 자동으로 유추하도록 할 수도 있습니다. `Swap`에 대한 다음 호출은 위 예제의 호출과 동일한 작업을 수행합니다.  
  
 [!code-csharp[csProgGuideGenerics#24](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_3.cs)]  
  
 정적 메서드와 인스턴스 메서드에는 형식 유추와 동일한 규칙이 적용됩니다. 컴파일러는 전달한 메서드 인수에 따라 형식 매개 변수를 유추할 수 있지만, 제약 조건이나 반환 값만으로는 형식 매개 변수를 유추할 수 없습니다. 따라서 매개 변수가 없는 메서드에 대해서는 형식 유추가 실행되지 않습니다. 형식 유추는 컴파일러에서 오버로드된 메서드 시그니처를 확인하려고 하기 전에 컴파일 시간에 진행됩니다. 컴파일러는 동일한 이름을 공유하는 모든 제네릭 메서드에 형식 유추 논리를 적용합니다. 오버로드 확인 단계에서 컴파일러는 형식 유추에 성공한 제네릭 메서드만 포함합니다.  
  
 제네릭 클래스 내에서 제네릭이 아닌 메서드는 다음과 같은 클래스 수준의 형식 매개 변수에 액세스할 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#25](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_4.cs)]  
  
 포함하는 클래스와 동일한 형식 매개 변수를 사용하는 제네릭 메서드를 정의하면 컴파일러에서 CS0693 경고가 발생합니다. 이는 메서드 범위 내에서 내부 `T`에 제공된 인수가 외부 `T`에 제공된 인수를 숨기기 때문입니다. 클래스를 인스턴스화할 때 제공한 형식 인수가 아닌 다른 형식 인수를 사용하여 제네릭 클래스 메서드를 호출할 수 있으려면 다음 예제의 `GenericList2<T>`에서와 같이 메서드의 형식 매개 변수에 다른 식별자를 제공해 보세요.  
  
 [!code-csharp[csProgGuideGenerics#26](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_5.cs)]  
  
 메서드에서 형식 매개 변수에 대한 더 구체적인 작업을 수행하려면 제약 조건을 사용합니다. `SwapIfGreater<T>`라는 이 버전의 `Swap<T>`은 <xref:System.IComparable%601>을 구현하는 형식 인수와만 함께 사용할 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#27](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_6.cs)]  
  
 제네릭 메서드는 몇몇 형식 매개 변수에 오버로드될 수 있습니다. 예를 들어 다음 메서드는 모두 동일한 클래스에 지정할 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#28](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_7.cs)]  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/classes.md#methods)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic>  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [제네릭 소개](../../../csharp/programming-guide/generics/introduction-to-generics.md)  
- [메서드](../../../csharp/programming-guide/classes-and-structs/methods.md)
