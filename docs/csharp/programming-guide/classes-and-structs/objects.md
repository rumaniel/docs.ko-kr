---
title: 개체 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- objects [C#], about objects
- variables [C#]
ms.assetid: af4a5230-fbf3-4eea-95e1-8b883c2f845c
ms.openlocfilehash: 3319cfa6b98e3f4b9b8afa070c4784c03d2750ef
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596380"
---
# <a name="objects-c-programming-guide"></a>개체(C# 프로그래밍 가이드)
클래스 또는 구조체 정의는 형식이 수행할 수 있는 작업을 지정하는 청사진과 비슷합니다. 개체는 기본적으로 청사진에 따라 구성 및 할당된 메모리 블록입니다. 프로그램에서 동일한 클래스의 많은 개체를 만들 수 있습니다. 개체를 인스턴스라고도 하며, 명명된 변수나 배열 또는 컬렉션에 저장할 수 있습니다. 클라이언트 코드는 이러한 변수를 사용하여 메서드를 호출하고 개체의 공용 속성에 액세스하는 코드입니다. C#과 같은 개체 지향 언어에서 일반적인 프로그램은 동적으로 상호 작용하는 여러 개체로 구성됩니다.  
  
> [!NOTE]
> 정적 형식은 여기에 설명된 것과 다르게 동작합니다. 자세한 내용은 [static 클래스 및 static 클래스 멤버](./static-classes-and-static-class-members.md)를 참조하세요.
  
## <a name="struct-instances-vs-class-instances"></a>구조체 인스턴스 및 클래스 인스턴스  
 클래스는 참조 형식이므로 클래스 개체의 변수는 관리되는 힙의 개체 주소에 대한 참조를 포함합니다. 동일한 형식의 두 번째 개체가 첫 번째 개체에 할당되면 두 변수가 모두 해당 주소의 개체를 참조합니다. 이 내용에 대해서는 이 항목의 뒷부분에서 자세히 설명합니다.  
  
 클래스 인스턴스는 [new 연산자](../../language-reference/operators/new-operator.md)를 사용하여 생성됩니다. 다음 예제에서 `Person`은 형식이고 `person1` 및 `person 2`는 해당 형식의 인스턴스 또는 개체입니다.  
  
 [!code-csharp[csProgGuideStatements#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#30)]  
  
 구조체는 값 형식이므로 구조체 개체의 변수는 전체 개체의 복사본을 포함합니다. 다음 예제와 같이 `new` 연산자를 사용하여 구조체 인스턴스를 만들 수도 있지만 필수는 아닙니다.  
  
 [!code-csharp[csProgGuideStatements#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#31)]  
  
 `p1` 및 `p2` 둘 다에 대한 메모리가 스레드 스택에서 할당됩니다. 해당 메모리가 선언된 형식 또는 메서드와 함께 회수됩니다. 이는 할당 시 구조체가 복사되는 이유 중 하나입니다. 반면, 클래스 인스턴스에 할당된 메모리는 개체에 대한 모든 참조가 범위를 벗어날 때 공용 언어 런타임에 의해 자동으로 회수(가비지 수집)됩니다. C++에서와 같이 클래스 개체를 자동으로 제거할 수 없습니다. .NET Framework의 가비지 수집에 대한 자세한 내용은 [가비지 수집](../../../standard/garbage-collection/index.md)을 참조하세요.  
  
> [!NOTE]
> 관리되는 힙의 메모리 할당 및 할당 취소는 공용 언어 런타임에서 고도로 최적화되어 있습니다. 대부분의 경우 힙에서 클래스 인스턴스를 할당하는 경우와 스택에서 구조체 인스턴스를 할당하는 경우의 성능 차이는 크지 않습니다.
  
## <a name="object-identity-vs-value-equality"></a>개체 ID와 값 같음 비교  
 두 개체가 같은지를 비교하는 경우 먼저 두 변수가 메모리에서 동일한 개체를 나타내는지 또는 해당 필드 값이 하나 이상 같은지를 알고 싶은 것인지 구분해야 합니다. 값을 비교하려는 경우 개체가 값 형식(구조체) 또는 참조 형식(클래스, 대리자, 배열)의 인스턴스인지 고려해야 합니다.  
  
- 두 클래스 인스턴스가 메모리의 동일한 위치를 참조하는지 확인하려면(즉, *ID*가 같음) 정적 <xref:System.Object.Equals%2A> 메서드를 사용합니다. <xref:System.Object?displayProperty=nameWithType>은 사용자 정의 구조체 및 클래스를 포함하여 모든 값 형식 및 참조 형식에 대한 암시적 기본 클래스입니다.  
  
- 두 구조체 인스턴스의 인스턴스 필드 값이 같은지 확인하려면 <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> 메서드를 사용합니다. 모든 구조체가 <xref:System.ValueType?displayProperty=nameWithType>에서 암시적으로 상속하기 때문에 다음 예제와 같이 개체에서 직접 메서드를 호출합니다.  
  
 [!code-csharp[csProgGuideStatements#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#32)]  
  
 `Equals`의 <xref:System.ValueType?displayProperty=nameWithType> 구현에서는 구조체의 필드를 확인할 수 있어야 하므로 리플렉션을 사용합니다. 고유한 구조체를 만드는 경우 `Equals` 메서드를 재정의하여 해당 형식과 관련된 효율적인 같음 알고리즘을 제공합니다.  
  
- 두 클래스 인스턴스의 필드 값이 같은지 확인하기 위해 <xref:System.Object.Equals%2A> 메서드 또는 [== 연산자](../../language-reference/operators/equality-operators.md#equality-operator-)를 사용할 수 있습니다. 그러나 클래스가 해당 형식의 개체에 대해 "같음"이 무엇을 의미하는지의 사용자 지정 정의를 제공하도록 재정의 또는 오버로드한 경우에만 사용합니다. 클래스는 <xref:System.IEquatable%601> 인터페이스 또는 <xref:System.Collections.Generic.IEqualityComparer%601> 인터페이스도 구현할 수 있습니다. 두 인터페이스 모두 값이 같은지를 테스트하는 데 사용할 수 있는 메서드를 제공합니다. `Equals`을 재정의하는 고유한 클래스를 디자인하는 경우 [방법: 형식의 값 일치 정의](../statements-expressions-operators/how-to-define-value-equality-for-a-type.md) 및 <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType>에 명시된 지침을 따라야 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 추가 정보  
  
- [클래스](./classes.md)  
  
- [구조체](./structs.md)  
  
- [생성자](./constructors.md)  
  
- [종료자](./destructors.md)  
  
- [이벤트](../events/index.md)  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [object](../../language-reference/keywords/object.md)
- [상속](./inheritance.md)
- [class](../../language-reference/keywords/class.md)
- [struct](../../language-reference/keywords/struct.md)
- [new 연산자](../../language-reference/operators/new-operator.md)
- [공용 형식 시스템](../../../standard/base-types/common-type-system.md)
