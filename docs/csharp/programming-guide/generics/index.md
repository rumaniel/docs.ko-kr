---
title: 제네릭 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, generics
- generics [C#]
ms.assetid: 75ea8509-a4ea-4e7a-a2b3-cf72482e9282
ms.openlocfilehash: 7d212aeaa7d7a8c3f152f8610a7ef3fe5de0fe23
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589599"
---
# <a name="generics-c-programming-guide"></a>제네릭(C# 프로그래밍 가이드)
제네릭이 C# 언어 및 CLR(공용 언어 런타임)의 버전 2.0에 추가되었습니다. 제네릭은 .NET Framework에 클라이언트 코드에서 클래스 또는 메서드를 선언하고 인스턴스화할 때까지 하나 이상의 형식 사양을 따르는 클래스 및 메서드를 디자인할 수 있도록 만드는 형식 매개 변수 개념을 도입합니다. 예를 들어 제네릭 형식 매개 변수 T를 사용하여 여기에 표시된 것처럼, 다른 클라이언트 코드에서 런타임 캐스팅 또는 boxing 작업에 대한 비용이나 위험을 발생하지 않고 사용할 수 있는 단일 클래스를 작성할 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#1)]  

제네릭 클래스 및 메서드는 제네릭이 아닌 클래스 및 메서드에서는 결합할 수 없는 방식으로 재사용성, 형식 안전성 및 효율성을 결합합니다. 제네릭은 컬렉션 및 해당 컬렉션에서 작동하는 메서드에서 가장 자주 사용됩니다. .NET Framework 클래스 라이브러리 2.0 버전은 여러 가지 새로운 제네릭 기반 컬렉션 클래스가 포함된 새로운 네임스페이스 <xref:System.Collections.Generic>을 제공합니다. .NET Framework 2.0 이상을 대상으로 하는 모든 애플리케이션은 <xref:System.Collections.ArrayList> 같은 이전의 제네릭이 아닌 컬렉션 클래스 대신 새로운 제네릭 컬렉션 클래스를 사용하는 것이 좋습니다. 자세한 내용은 [.NET의 제네릭](../../../standard/generics/index.md)을 참조하세요.  
  
 물론, 사용자 지정 제네릭 형식 및 메서드를 만들어 형식이 안전하고 효율적인 일반화된 솔루션 및 디자인 패턴을 직접 제공할 수도 있습니다. 다음 코드 예제에서는 데모용으로 간단한 제네릭 연결된 목록 클래스를 보여 줍니다. 대부분의 경우 직접 만드는 대신 .NET Framework 클래스 라이브러리에서 제공하는 <xref:System.Collections.Generic.List%601> 클래스를 사용해야 합니다. 형식 매개 변수 `T`는 일반적으로 구체적인 형식을 사용하여 목록에 저장된 항목의 형식을 나타내는 여러 위치에서 사용되며, 다음과 같은 방법으로 사용됩니다.  
  
- `AddHead` 메서드에서 메서드 매개 변수의 형식.  
  
- 중첩 `Node` 클래스에서 `Data` 속성의 반환 형식.  
  
- 중첩 클래스에서 private 멤버 `data`의 형식.  
  
 T는 중첩 `Node` 클래스에 사용할 수 있습니다. `GenericList<T>`가 `GenericList<int>`와 같이 구체적인 형식으로 인스턴스화되면 `T`가 나타날 때마다 `int`로 바뀝니다.  
  
 [!code-csharp[csProgGuideGenerics#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#2)]  
  
 다음 코드 예제에서는 클라이언트 코드에서 제네릭 `GenericList<T>` 클래스를 사용하여 정수 목록을 만드는 방법을 보여 줍니다. 형식 인수를 변경하기만 하면 다음 코드를 쉽게 수정하여 문자열이나 다른 모든 사용자 지정 형식 목록을 만들 수 있습니다.  
  
 [!code-csharp[csProgGuideGenerics#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#3)]  
  
## <a name="generics-overview"></a>제네릭 개요  
  
- 제네릭 형식을 사용하여 코드 재사용, 형식 안전성 및 성능을 최대화합니다.  
  
- 가장 일반적으로 제네릭은 컬렉션 클래스를 만드는 데 사용됩니다.  
  
- .NET Framework 클래스 라이브러리에는 <xref:System.Collections.Generic> 네임스페이스에 여러 가지 새로운 제네릭 컬렉션 클래스가 포함됩니다. 이러한 제네릭 컬렉션 클래스는 가능할 때마다 <xref:System.Collections> 네임스페이스의 <xref:System.Collections.ArrayList>처럼 클래스 대신 사용되어야 합니다.  
  
- 사용자 고유의 제네릭 인터페이스, 클래스, 메서드, 이벤트 및 대리자를 만들 수 있습니다.  
  
- 제네릭 클래스는 특정 데이터 형식의 메서드에 액세스할 수 있도록 제한될 수 있습니다.  
  
- 제네릭 데이터 형식에 사용되는 형식에 대한 정보는 리플렉션을 사용하여 런타임 시 얻을 수 있습니다.  
  
## <a name="related-sections"></a>관련 단원  
 추가 정보  
  
- [제네릭 형식 매개 변수](./generic-type-parameters.md)  
  
- [형식 매개 변수에 대한 제약 조건](./constraints-on-type-parameters.md)  
  
- [제네릭 클래스](./generic-classes.md)  
  
- [제네릭 인터페이스](./generic-interfaces.md)  
  
- [제네릭 메서드](./generic-methods.md)  
  
- [제네릭 대리자](./generic-delegates.md)  
  
- [C++ 템플릿과 C# 제네릭의 차이점](./differences-between-cpp-templates-and-csharp-generics.md)  
  
- [제네릭 및 리플렉션](./generics-and-reflection.md)  
  
- [런타임의 제네릭](./generics-in-the-run-time.md)  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/types.md#constructed-types)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic>
- [C# 프로그래밍 가이드](../index.md)
- [유형](../types/index.md)
- [\<typeparam>](../xmldoc/typeparam.md)
- [\<typeparamref>](../xmldoc/typeparamref.md)
- [.NET의 제네릭](../../../standard/generics/index.md)
