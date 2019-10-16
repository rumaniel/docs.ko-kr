---
title: 제네릭 클래스 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, generic classes
- generics [C#], classes
ms.assetid: 27d6f256-cd61-41e3-bc6e-b990a53b0224
ms.openlocfilehash: 6eb4df4489f4b377c68c5d49d1bf0bb01b835e85
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589772"
---
# <a name="generic-classes-c-programming-guide"></a>제네릭 클래스(C# 프로그래밍 가이드)
제네릭 클래스는 특정 데이터 형식과 관련이 없는 작업을 캡슐화합니다. 제네릭 클래스는 연결된 목록, 해시 테이블, 스택, 큐, 트리 등의 컬렉션에 가장 일반적으로 사용됩니다. 컬렉션에서 항목을 추가하고 제거하는 등의 작업은 저장되는 데이터의 형식과 관계없이 기본적으로 동일한 방식으로 수행됩니다.  
  
 컬렉션 클래스를 필요로 하는 대부분의 시나리오에서는 .NET 클래스 라이브러리에서 제공하는 컬렉션 클래스를 사용하는 것이 좋습니다. 이러한 클래스 사용에 대한 자세한 내용은 [.NET의 제네릭 컬렉션](../../../standard/generics/collections.md)을 참조하세요.  
  
 일반적으로 기존의 구체적인 클래스로 시작하여 일반성과 편의성의 균형이 맞을 때까지 형식을 하나씩 형식 매개 변수로 변경하여 제네릭 클래스를 만듭니다. 고유한 제네릭 클래스를 만들 때 중요한 고려 사항은 다음과 같습니다.  
  
- 형식 매개 변수로 일반화할 형식  
  
     일반적으로 매개 변수화할 수 있는 형식이 많을수록 코드의 유용성과 재사용 가능성이 향상됩니다. 그러나 지나친 일반화는 다른 개발자가 읽거나 이해하기 어려운 코드를 만들어낼 소지가 있습니다.  
  
- 형식 매개 변수에 적용할 제약 조건([형식 매개 변수에 대한 제약 조건](./constraints-on-type-parameters.md) 참조)  
  
     필요한 형식을 처리할 수 있는 범위 내에서 최대한 많은 제약 조건을 적용하는 것이 좋습니다. 예를 들어 제네릭 클래스를 참조 형식으로만 사용하려는 경우에는 클래스 제약 조건을 적용합니다. 이렇게 하면 클래스를 값 형식으로 잘못 사용하는 것을 막을 수 있고, `as` 연산자를 `T`에 적용하여 null 값 여부를 확인할 수 있습니다.  
  
- 제네릭 동작을 기본 클래스와 서브클래스로 분할할지 여부  
  
     제네릭 클래스는 기본 클래스가 될 수 있으므로 제네릭이 아닌 클래스에 적용되는 디자인 고려 사항이 동일하게 적용됩니다. 자세한 내용은 이 항목의 뒷부분에서 설명하는 제네릭 기본 클래스에서 상속하는 데 대한 규칙을 참조하세요.  
  
- 제네릭 인터페이스를 하나 이상 구현할지 여부  
  
     예를 들어 제네릭 기반 컬렉션에 항목을 만드는 데 사용될 클래스를 디자인할 경우 클래스 형식이 `T`인 <xref:System.IComparable%601>와 같은 인터페이스를 구현해야 할 수 있습니다.  
  
 간단한 제네릭 클래스의 예제를 보려면 [제네릭 소개](./index.md)를 참조하세요.  
  
 형식 매개 변수와 제약 조건에 대한 규칙은 제네릭 클래스 동작, 특히 상속과 멤버 접근성에 몇 가지 영향을 줍니다. 계속하려면 몇 가지 용어를 이해하고 있어야 합니다. 제네릭 클래스 `Node<T>,`의 경우 클라이언트 코드는 형식 인수를 지정하여 폐쇄형 생성 형식(`Node<int>`)을 만들어 클래스를 참조할 수 있습니다. 또는 제네릭 기본 클래스를 지정하는 경우와 같이 형식 매개 변수를 지정하지 않고 개방형 생성 형식(`Node<T>`)을 만들 수 있습니다. 제네릭 클래스는 구체적인 클래스, 폐쇄형 생성 클래스 또는 개방형 생성 기본 클래스에서 상속할 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#16)]  
  
 제네릭이 아닌 구체적인 클래스는 폐쇄형 생성 기본 클래스에서는 상속할 수 있지만 개방형 생성 클래스 또는 형식 매개 변수에서는 상속할 수 없습니다. 이는 런타임에 클라이언트 코드에서 기본 클래스를 인스턴스화할 때 필요한 형식 인수를 제공할 수 없기 때문입니다.  
  
 [!code-csharp[csProgGuideGenerics#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#17)]  
  
 개방형 생성 형식에서 상속하는 제네릭 클래스에서는 다음 코드와 같이 상속하는 클래스에서 공유하지 않는 모든 기본 클래스 형식 매개 변수에 대해 형식 인수를 제공해야 합니다.  
  
 [!code-csharp[csProgGuideGenerics#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#18)]  
  
 개방형 생성 형식에서 상속하는 제네릭 클래스에서는 기본 형식에 대한 제약 조건을 포함하거나 암시하는 제약 조건을 지정해야 합니다.  
  
 [!code-csharp[csProgGuideGenerics#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#19)]  
  
 제네릭 형식은 다음과 같이 여러 형식 매개 변수와 제약 조건을 사용할 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#20)]  
  
 개방형 생성 형식 및 폐쇄형 생성 형식은 메서드 매개 변수로 사용할 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#21)]  
  
 제네릭 클래스에서 인터페이스를 구현하면 이 클래스의 모든 인스턴스를 해당 인터페이스에 캐스팅할 수 있습니다.  
  
 제네릭 클래스는 고정적입니다. 즉, 입력 매개 변수에서 `List<BaseClass>`를 지정하면 `List<DerivedClass>`를 제공하려고 할 때 컴파일 시간 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic>
- [C# 프로그래밍 가이드](../index.md)
- [제네릭](./index.md)
- [열거자의 상태 저장](https://blogs.msdn.microsoft.com/wesdyer/2006/01/13/saving-the-state-of-enumerators/)
- [상속 퍼즐, 1부](https://blogs.msdn.microsoft.com/ericlippert/2007/07/27/an-inheritance-puzzle-part-one/)
