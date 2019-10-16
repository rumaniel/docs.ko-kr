---
title: 익명 형식 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- anonymous types [C#]
- C# Language, anonymous types
ms.assetid: 59c9d7a4-3b0e-475e-b620-0ab86c088e9b
ms.openlocfilehash: 93f02b8a0f828be89c6a1b7bfcdc6ba2a2a93e81
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597184"
---
# <a name="anonymous-types-c-programming-guide"></a>익명 형식(C# 프로그래밍 가이드)

익명 형식을 사용하면 먼저 명시적으로 형식을 정의할 필요 없이 읽기 전용 속성 집합을 단일 개체로 편리하게 캡슐화할 수 있습니다. 형식 이름은 컴파일러에 의해 생성되며 소스 코드 수준에서 사용할 수 없습니다. 각 속성의 형식은 컴파일러에서 유추합니다.  
  
 [new](../../language-reference/operators/new-operator.md) 연산자를 개체 이니셜라이저와 함께 사용하여 무명 형식을 만듭니다. 개체 이니셜라이저에 대한 자세한 내용은 [개체 및 컬렉션 이니셜라이저](./object-and-collection-initializers.md)를 참조하세요.  
  
 다음 예제에서는 `Amount` 및 `Message`라는 두 속성으로 초기화된 익명 형식을 보여 줍니다.  
  
```csharp  
var v = new { Amount = 108, Message = "Hello" };  
  
// Rest the mouse pointer over v.Amount and v.Message in the following  
// statement to verify that their inferred types are int and string.  
Console.WriteLine(v.Amount + v.Message);  
```  
  
 일반적으로 무명 형식은 소스 시퀀스에 있는 각 개체의 속성 하위 집합을 반환하기 위해 쿼리 식의 [select](../../language-reference/keywords/select-clause.md) 절에 사용됩니다. 쿼리에 대한 자세한 내용은 [LINQ 쿼리 식](../linq-query-expressions/index.md)을 참조하세요.  
  
 익명 형식은 하나 이상의 public 읽기 전용 속성을 포함합니다. 메서드 또는 이벤트와 같은 다른 종류의 클래스 멤버는 유효하지 않습니다. 속성을 초기화하는 데 사용되는 식은 `null`, 익명 함수 또는 포인터 형식일 수 없습니다.  
  
 가장 일반적인 시나리오는 다른 형식의 속성으로 익명 형식을 초기화하는 것입니다. 다음 예제에서는 `Product`라는 클래스가 있다고 가정합니다. `Product` 클래스에는 `Color` 및 `Price` 속성뿐만 아니라 관심 없는 다른 속성도 포함되어 있습니다. `products` 변수는 `Product` 개체의 컬렉션입니다. 익명 형식 선언은 `new` 키워드로 시작합니다. 선언에서는 `Product`의 두 속성만 사용하는 새 형식을 초기화합니다. 따라서 쿼리에 작은 양의 데이터가 반환됩니다.  
  
 익명 형식에 멤버 이름을 지정하지 않으면 컴파일러가 익명 형식 멤버에 해당 멤버를 초기화하는 데 사용된 속성과 동일한 이름을 제공합니다. 앞의 예제에 표시된 것처럼, 식으로 초기화되는 속성의 이름을 제공해야 합니다. 다음 예제에서 익명 형식의 속성 이름은 `Color` 및 `Price`입니다.  
  
 [!code-csharp[csRef30Features#81](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csRef30Features/CS/csref30.cs#81)]  
  
 일반적으로 무명 형식을 사용하여 변수를 초기화할 때는 [var](../../language-reference/keywords/var.md)을 사용하여 변수를 암시적 형식 지역 변수로 선언합니다. 컴파일러만 익명 형식의 기본 이름에 액세스할 수 있으므로 변수 선언에는 형식 이름을 지정할 수 없습니다. `var`에 대한 자세한 내용은 [암시적 형식 지역 변수](./implicitly-typed-local-variables.md)를 참조하세요.  
  
 다음 예제에 표시된 것처럼, 암시적으로 형식화된 지역 변수와 암시적으로 형식화된 배열을 결합하여 익명으로 형식화된 요소의 배열을 만들 수 있습니다.  
  
```csharp  
var anonArray = new[] { new { name = "apple", diam = 4 }, new { name = "grape", diam = 1 }};  
```  
  
## <a name="remarks"></a>설명  
 무명 형식은 [object](../../language-reference/keywords/object.md)에서 직접 파생되고 [object](../../language-reference/keywords/object.md)를 제외한 어떠한 형식으로도 캐스팅될 수 없는 [class](../../language-reference/keywords/class.md) 형식입니다. 컴파일러는 애플리케이션에서 해당 익명 형식에 액세스할 수 없더라도 각 익명 형식의 이름을 제공합니다. 공용 언어 런타임의 관점에서 익명 형식은 다른 참조 형식과 다를 바가 없습니다.  
  
 어셈블리에서 둘 이상의 익명 개체 이니셜라이저가 순서와 이름 및 형식이 동일한 속성의 시퀀스를 지정하는 경우 컴파일러는 개체를 동일한 형식의 인스턴스로 처리합니다. 이러한 개체는 컴파일러에서 생성된 동일한 형식 정보를 공유합니다.  
  
 익명 형식을 가지고 있으므로 필드, 속성, 이벤트 또는 메서드의 반환 형식은 선언할 수 없습니다. 마찬가지로, 익명 형식을 가지고 있으므로 메서드, 속성, 생성자 또는 인덱서의 정식 매개 변수는 선언할 수 없습니다. 익명 형식이나 익명 형식을 포함한 컬렉션을 메서드에 대한 인수로 전달하려면 매개 변수를 형식 개체로 선언하면 됩니다. 그러나 이렇게 하면 강력한 형식화를 사용하는 의미가 없습니다. 쿼리 결과를 저장하거나 메서드 경계 외부로 전달해야 하는 경우 익명 형식 대신 일반적인 명명된 구조체 또는 클래스 사용을 고려하세요.  
  
 익명 형식에 대한 <xref:System.Object.Equals%2A> 및 <xref:System.Object.GetHashCode%2A> 메서드는 속성의 `Equals` 및 `GetHashCode` 메서드 측면에서 정의되므로 동일한 익명 형식의 두 인스턴스는 해당 속성이 모두 동일한 경우에만 동일합니다.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [개체 이니셜라이저 및 컬렉션 이니셜라이저](./object-and-collection-initializers.md)
- [C#에서 LINQ 시작](../concepts/linq/getting-started-with-linq.md)
- [LINQ 쿼리 식](../linq-query-expressions/index.md)
