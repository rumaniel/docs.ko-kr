---
title: 런타임의 제네릭 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], at run time
ms.assetid: 119df7e6-9ceb-49df-af36-24f8f8c0747f
ms.openlocfilehash: a627ac51399b67aeb7da8c3d98a4530248a84703
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659744"
---
# <a name="generics-in-the-run-time-c-programming-guide"></a>런타임의 제네릭(C# 프로그래밍 가이드)
제네릭 형식 또는 메서드가 MSIL(Microsoft Intermediate Language)로 컴파일되면 자체적으로 형식 매개 변수를 갖는 것으로 식별하는 메타데이터가 포함됩니다. 제네릭 형식의 MSIL이 사용되는 방식은 제공된 형식 매개 변수가 값 형식인지 참조 형식인지에 따라 다릅니다.  
  
 값 형식을 매개 변수로 사용하여 제네릭 형식을 처음 생성할 경우 런타임에서는 제공된 매개 변수를 MSIL의 해당 위치에 대체하여 특수화된 제네릭 형식을 만듭니다. 고유한 값 형식이 매개 변수로 사용될 때마다 특수화된 제네릭 형식이 만들어집니다.  
  
 예를 들어 프로그램 코드에서 다음과 같이 정수로 구성된 스택을 선언한다고 가정합니다.  
  
 [!code-csharp[csProgGuideGenerics#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#42)]  
  
 이 시점에서 런타임은 매개 변수를 정수로 적절히 대체하여 특수화된 버전의 <xref:System.Collections.Generic.Stack%601> 클래스를 생성합니다. 이제부터 프로그램 코드에서 정수 스택을 사용하면 런타임은 생성된 특수화 <xref:System.Collections.Generic.Stack%601> 클래스를 다시 사용합니다. 다음 예제에서는 `Stack<int>` 코드의 단일 인스턴스를 공유하는 정수 스택의 두 인스턴스를 만듭니다.  
  
 [!code-csharp[csProgGuideGenerics#43](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#43)]  
  
 그러나 코드의 다른 지점에서 `long`과 같이 값 형식이 다르거나, 사용자 정의된 구조체를 매개 변수로 사용하는 다른 <xref:System.Collections.Generic.Stack%601> 클래스를 만들었다고 가정해 보겠습니다. 이 경우 런타임에서는 제네릭 형식의 다른 버전을 생성하여 MSIL의 적절한 위치에 `long`을 대체합니다. 특수화된 각 제네릭 클래스에는 기본적으로 값 형식이 포함되므로 변환은 더 이상 필요하지 않습니다.  
  
 참조 형식에 대해서는 제네릭의 작동 방식이 조금 다릅니다. 참조 형식을 사용하여 제네릭 형식이 처음 생성될 때 런타임에서는 MSIL의 매개 변수를 개체 참조로 대체하여 특수화된 제네릭 형식을 만듭니다. 이후 참조 형식과 관계없이 참조 형식을 매개 변수로 사용하여 생성된 형식이 인스턴스화될 때마다 런타임에서는 이전에 만든 특수화된 버전의 제네릭 형식을 다시 사용합니다. 이는 모든 참조의 크기가 동일하기 때문에 가능합니다.  
  
 예를 들어 `Customer` 클래스와 `Order` 클래스라는 두 참조 형식이 있고 `Customer` 형식의 스택을 만들었다고 가정합니다.  
  
 [!code-csharp[csProgGuideGenerics#47](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#47)]  
  
 [!code-csharp[csProgGuideGenerics#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#44)]  
  
 이 시점에서 런타임은 데이터를 저장하는 대신 이후에 채워질 개체 참조를 저장하는 특수화된 버전의 <xref:System.Collections.Generic.Stack%601> 클래스를 생성합니다. 다음 코드 줄에서 `Order`라는 다른 참조 형식의 스택을 만든다고 가정해 봅니다.  
  
 [!code-csharp[csProgGuideGenerics#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#45)]  
  
 값 형식과는 달리 `Order` 형식에 대한 또 다른 특수화된 버전의 <xref:System.Collections.Generic.Stack%601> 클래스는 만들어지지 않습니다. 대신 특수화된 버전의 <xref:System.Collections.Generic.Stack%601> 클래스 인스턴스가 만들어지고 `orders` 변수가 이 인스턴스를 참조하도록 설정됩니다. 이후에 `Customer` 형식의 스택을 만드는 코드 줄이 나타난다고 가정해 봅니다.  
  
 [!code-csharp[csProgGuideGenerics#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#46)]  
  
 `Order` 형식을 사용하여 만든 <xref:System.Collections.Generic.Stack%601> 클래스를 사용한 경우와 마찬가지로 특수화된 <xref:System.Collections.Generic.Stack%601> 클래스의 다른 인스턴스가 생성됩니다. 여기에 포함된 포인터는 `Customer` 형식과 크기가 같은 메모리 영역을 참조하도록 설정됩니다. 참조 형식의 수는 프로그램마다 크게 다를 수 있으므로, 제네릭을 C# 방식으로 구현하면 컴파일러가 참조 형식의 제네릭 클래스에 대해 만드는 특수화된 클래스의 수가 1개로 줄어들어 코드가 매우 간결해집니다.  
  
 그뿐만 아니라, 값 형식 또는 참조 형식 매개 변수를 사용하여 제네릭 C# 클래스가 인스턴스화되면 런타임에 리플렉션을 통해 쿼리할 수 있고 실제 형식과 형식 매개 변수를 모두 확인할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic>
- [C# 프로그래밍 가이드](../index.md)
- [제네릭 소개](./index.md)
- [제네릭](../../../standard/generics/index.md)
