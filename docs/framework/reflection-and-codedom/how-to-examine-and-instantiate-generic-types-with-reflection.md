---
title: '방법: 리플렉션을 사용하여 제네릭 형식 검사 및 인스턴스화'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reflection, generic types
- generics [.NET Framework], reflection
ms.assetid: f93b03b0-1778-43fc-bc6d-35983d210e74
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6e15ef69c4777cdafe2e5861050a1ccc1f6a1a70
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046013"
---
# <a name="how-to-examine-and-instantiate-generic-types-with-reflection"></a>방법: 리플렉션을 사용하여 제네릭 형식 검사 및 인스턴스화
다른 형식에 대한 정보와 동일한 방식으로 제네릭 형식에 대한 정보를 가져올 수 있습니다. 제네릭 형식을 나타내는 <xref:System.Type> 개체를 검사하면 됩니다. 원칙의 차이점은 제네릭 형식에는 제네릭 형식 매개 변수를 나타내는 <xref:System.Type> 개체 목록이 있다는 것입니다. 이 섹션의 첫 번째 절차에서는 제네릭 형식을 검사합니다.  
  
 형식 인수를 제네릭 형식 정의의 형식 매개 변수에 바인딩하여 생성된 형식을 나타내는 <xref:System.Type> 개체를 만들 수 있습니다. 두 번째 절차에서 이 방법을 보여 줍니다.  
  
### <a name="to-examine-a-generic-type-and-its-type-parameters"></a>제네릭 형식 및 해당 형식 매개 변수를 검사하려면  
  
1. 제네릭 형식을 나타내는 <xref:System.Type> 인스턴스를 가져옵니다. 다음 코드에서는 C# `typeof` 연산자(Visual Basic에서는 `GetType`, Visual C++에서는 `typeid`)를 사용하여 형식을 가져옵니다. <xref:System.Type> 개체를 가져오는 다른 방법은 <xref:System.Type> 클래스 항목을 참조하세요. 이 절차의 나머지 부분에서는 `t`라는 메서드 매개 변수에 형식이 포함되어 있습니다.  
  
     [!code-cpp[HowToGeneric#2](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#2)]
     [!code-csharp[HowToGeneric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#2)]
     [!code-vb[HowToGeneric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#2)]  
  
2. <xref:System.Type.IsGenericType%2A> 속성을 사용하여 형식이 제네릭인지 여부를 확인하고, <xref:System.Type.IsGenericTypeDefinition%2A> 속성을 사용하여 형식이 제네릭 형식 정의인지 여부를 확인합니다.  
  
     [!code-cpp[HowToGeneric#3](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#3)]
     [!code-csharp[HowToGeneric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#3)]
     [!code-vb[HowToGeneric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#3)]  
  
3. <xref:System.Type.GetGenericArguments%2A> 메서드를 사용하여 제네릭 형식 인수를 포함하는 배열을 가져옵니다.  
  
     [!code-cpp[HowToGeneric#4](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#4)]
     [!code-csharp[HowToGeneric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#4)]
     [!code-vb[HowToGeneric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#4)]  
  
4. <xref:System.Type.IsGenericParameter%2A> 속성을 사용하여 각 형식 인수가 형식 매개 변수인지(예: 제네릭 형식 정의에 있음), 아니면 형식 매개 변수에 대해 지정된 형식인지(예: 생성된 형식에 있음) 확인합니다.  
  
     [!code-cpp[HowToGeneric#5](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#5)]
     [!code-csharp[HowToGeneric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#5)]
     [!code-vb[HowToGeneric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#5)]  
  
5. 형식 시스템에서 제네릭 형식 매개 변수는 일반 형식과 마찬가지로 <xref:System.Type> 인스턴스로 나타냅니다. 다음 코드는 제네릭 형식 매개 변수를 나타내는 <xref:System.Type> 개체의 이름 및 매개 변수 위치를 표시합니다. 매개 변수 위치는 여기서는 중요한 정보가 아니며 다른 제네릭 형식의 형식 인수로 사용된 형식 매개 변수를 검사하는 경우에 더 중요합니다.  
  
     [!code-cpp[HowToGeneric#6](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#6)]
     [!code-csharp[HowToGeneric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#6)]
     [!code-vb[HowToGeneric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#6)]  
  
6. <xref:System.Type.GetGenericParameterConstraints%2A> 메서드를 통해 단일 배열의 모든 제약 조건을 가져와 제네릭 형식 매개 변수의 기본 형식 제약 조건 및 인터페이스 제약 조건을 확인합니다. 제약 조건의 순서는 보장되지 않습니다.  
  
     [!code-cpp[HowToGeneric#7](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#7)]
     [!code-csharp[HowToGeneric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#7)]
     [!code-vb[HowToGeneric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#7)]  
  
7. <xref:System.Type.GenericParameterAttributes%2A> 속성을 사용하여 참조 형식이어야 함 등의 형식 매개 변수에 대한 특수 제약 조건을 검색합니다. 속성에는 다음 코드와 같이 마스킹할 수 있는 차이를 나타내는 값도 포함되어 있습니다.  
  
     [!code-cpp[HowToGeneric#8](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#8)]
     [!code-csharp[HowToGeneric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#8)]
     [!code-vb[HowToGeneric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#8)]  
  
8. 특수 제약 조건 특성은 플래그이고, 특수 제약 조건 없음을 나타내는 동일한 플래그(<xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType>)는 또한 공변성(Covariance) 또는 반공변성(Contravariance) 없음을 나타냅니다. 따라서 이러한 조건 중 하나를 테스트하려면 적절한 마스크를 사용해야 합니다. 이 경우 <xref:System.Reflection.GenericParameterAttributes.SpecialConstraintMask?displayProperty=nameWithType>을 사용하여 특수 제약 조건 플래그를 격리합니다.  
  
     [!code-cpp[HowToGeneric#9](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#9)]
     [!code-csharp[HowToGeneric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#9)]
     [!code-vb[HowToGeneric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#9)]  
  
## <a name="constructing-an-instance-of-a-generic-type"></a>제네릭 형식 인스턴스 생성  
 제네릭 형식은 템플릿과 같습니다. 제네릭 형식 매개 변수에 대해 실제 형식을 지정하지 않으면 해당 인스턴스를 만들 수 없습니다. 런타임에 리플렉션을 사용하여 이 작업을 수행하려면 <xref:System.Type.MakeGenericType%2A> 메서드가 필요합니다.  
  
#### <a name="to-construct-an-instance-of-a-generic-type"></a>제네릭 형식의 인스턴스를 생성하려면  
  
1. 제네릭 형식을 나타내는 <xref:System.Type> 개체를 가져옵니다. 다음 코드는 두 가지 방법으로 제네릭 형식 <xref:System.Collections.Generic.Dictionary%602>를 가져옵니다. 하나는 형식을 설명하는 문자열과 함께 <xref:System.Type.GetType%28System.String%29?displayProperty=nameWithType> 메서드 오버로드를 사용하는 것이고, 다른 하나는 생성된 형식 `Dictionary\<String, Example>`(Visual Basic에서는 `Dictionary(Of String, Example)`)에서 <xref:System.Type.GetGenericTypeDefinition%2A> 메서드를 호출하는 것입니다. <xref:System.Type.MakeGenericType%2A> 메서드에는 제네릭 형식 정의가 필요합니다.  
  
     [!code-cpp[HowToGeneric#10](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#10)]
     [!code-csharp[HowToGeneric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#10)]
     [!code-vb[HowToGeneric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#10)]  
  
2. 형식 매개 변수를 대체할 형식 인수 배열을 생성합니다. 배열에는 올바른 개수의 <xref:System.Type> 개체가 형식 매개 변수 목록에 표시되는 순서대로 포함되어야 합니다. 이 경우 키(첫 번째 형식 매개 변수)는 <xref:System.String> 형식이고, 사전에 있는 값은 `Example`이라는 클래스 인스턴스입니다.  
  
     [!code-cpp[HowToGeneric#11](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#11)]
     [!code-csharp[HowToGeneric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#11)]
     [!code-vb[HowToGeneric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#11)]  
  
3. <xref:System.Type.MakeGenericType%2A> 메서드를 호출하여 형식 인수를 형식 매개 변수에 바인딩하고 형식을 생성합니다.  
  
     [!code-cpp[HowToGeneric#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#12)]
     [!code-csharp[HowToGeneric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#12)]
     [!code-vb[HowToGeneric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#12)]  
  
4. <xref:System.Activator.CreateInstance%28System.Type%29> 메서드 오버로드를 사용하여 생성된 형식의 개체를 만듭니다. 다음 코드는 `Example` 클래스 인스턴스 두 개를 `Dictionary<String, Example>` 개체에 저장합니다.  
  
     [!code-cpp[HowToGeneric#13](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#13)]
     [!code-csharp[HowToGeneric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#13)]
     [!code-vb[HowToGeneric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#13)]  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 코드에서 사용된 제네릭 형식 정의 및 생성된 형식을 검사하고 해당 정보를 표시하는 `DisplayGenericType` 메서드를 정의합니다. `DisplayGenericType` 메서드는 <xref:System.Type.IsGenericType%2A>, <xref:System.Type.IsGenericParameter%2A> 및 <xref:System.Type.GenericParameterPosition%2A> 속성과 <xref:System.Type.GetGenericArguments%2A> 메서드를 사용하는 방법을 보여 줍니다.  
  
 또한 이 예제에서는 제네릭 형식 매개 변수를 검사하고 해당 제약 조건을 표시하는 `DisplayGenericParameter` 메서드를 정의합니다.  
  
 코드 예제에서는 형식 매개 변수 제약 조건을 설명하는 제네릭 형식을 포함하여 테스트 형식 집합을 정의하고 이러한 형식에 대한 정보를 표시하는 방법을 보여 줍니다.  
  
 예제에서는 형식 인수 배열을 만들고 <xref:System.Type.MakeGenericType%2A> 메서드를 호출하여 <xref:System.Collections.Generic.Dictionary%602> 클래스에서 형식을 생성합니다. 프로그램은 <xref:System.Type.MakeGenericType%2A>을 사용하여 생성된 <xref:System.Type> 개체와 `typeof`(Visual Basic에서는 `GetType`)를 사용하여 가져온 <xref:System.Type> 개체를 비교하여 같음을 보여 줍니다. 마찬가지로, 프로그램은 <xref:System.Type.GetGenericTypeDefinition%2A> 메서드를 사용하여 생성된 형식의 제네릭 형식 정의를 가져오고 <xref:System.Collections.Generic.Dictionary%602> 클래스를 나타내는 <xref:System.Type> 개체와 비교합니다.  
  
 [!code-cpp[HowToGeneric#1](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#1)]
 [!code-csharp[HowToGeneric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#1)]
 [!code-vb[HowToGeneric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Type>
- <xref:System.Reflection.MethodInfo>
- [리플렉션 및 제네릭 형식](reflection-and-generic-types.md)
- [형식 정보 보기](viewing-type-information.md)
- [제네릭](../../standard/generics/index.md)
