---
title: .NET의 제네릭
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generic methods, type inference
- generics [.NET Framework], collections
- generic interfaces [.NET Framework]
- constructed generic types
- nested generic types
- generic type definitions
- generic classes [.NET Framework]
- generics [.NET Framework], interfaces
- generics [.NET Framework], about
- generics [.NET Framework]
- generic collections [.NET Framework]
- generic delegates [.NET Framework]
- generic type arguments
- generics [.NET Framework], delegates
- generics [.NET Framework], features
- constraints [.NET Framework]
- generic types
- generic type parameters
ms.assetid: 2994d786-c5c7-4666-ab23-4c83129fe39c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 104a0018896eb95255cf4054f9402ce5160b95f7
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48584145"
---
# <a name="generics-in-net"></a>.NET의 제네릭

<a name="top"></a> 제네릭을 사용하면 메서드, 클래스, 구조체 또는 인터페이스를 사용 대상인 정확한 데이터 형식에 맞게 조정할 수 있습니다. 예를 들어 모든 형식의 키와 값을 허용하는 <xref:System.Collections.Hashtable> 클래스를 사용하는 대신 <xref:System.Collections.Generic.Dictionary%602> 제네릭 클래스를 사용하고 키에 허용되는 형식과 값에 허용되는 형식을 지정할 수 있습니다. 제네릭의 이점으로는 향상된 코드 다시 사용 가능성과 형식 안전성 등이 있습니다.  
  
 이 항목에서는 .NET 제네릭에 대해 간략하게 설명하고 제네릭 형식이나 메서드의 요약을 제공합니다. 여기에는 다음 단원이 포함되어 있습니다.  
  
-   [제네릭 정의 및 사용](#defining_and_using_generics)  
  
-   [제네릭 관련 용어](#generics_terminology)  
  
-   [클래스 라이브러리 및 언어 지원](#class_library_and_language_support)  
  
-   [중첩 형식 및 제네릭](#nested_types_and_generics)  
  
-   [관련 항목](#related_topics)  
  
-   [참조](#reference)  
  
<a name="defining_and_using_generics"></a>   
## <a name="defining-and-using-generics"></a>제네릭 정의 및 사용  
 제네릭은 저장하거나 사용하는 하나 이상의 형식에 대한 자리 표시자(형식 매개 변수)를 포함하는 클래스, 구조체, 인터페이스 및 메서드입니다. 제네릭 컬렉션 클래스는 저장하는 개체 형식에 대해 형식 매개 변수를 자리 표시자로 사용할 수 있습니다. 형식 매개 변수는 필드의 형식과 메서드의 매개 변수 형식으로 표시됩니다. 제네릭 메서드는 형식 매개 변수를 반환 값의 형식 또는 정식 매개 변수 중 하나의 형식으로 사용할 수 있습니다. 다음 코드에서는 간단한 제네릭 클래스 정의를 보여 줍니다.  
  
 [!code-cpp[Conceptual.Generics.Overview#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#2)]
 [!code-csharp[Conceptual.Generics.Overview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#2)]
 [!code-vb[Conceptual.Generics.Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#2)]  
  
 제네릭 클래스의 인스턴스를 만들 때는 형식 매개 변수를 대체할 실제 형식을 지정합니다. 이렇게 하면 형식 매개 변수가 표시되는 모든 위치에서 선택한 형식으로 대체된 새 제네릭 클래스인 생성된 제네릭 형식이 설정됩니다. 그 결과 다음 코드에 나와 있는 것처럼 선택한 형식에 맞게 조정된 형식이 안전한 클래스가 생성됩니다.  
  
 [!code-cpp[Conceptual.Generics.Overview#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#3)]
 [!code-csharp[Conceptual.Generics.Overview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#3)]
 [!code-vb[Conceptual.Generics.Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#3)]  
  
<a name="generics_terminology"></a>   
### <a name="generics-terminology"></a>제네릭 관련 용어  
 .NET에서 제네릭을 설명하는 데 사용되는 용어는 다음과 같습니다.  
  
-   *제네릭 형식 정의* 는 포함하거나 사용할 수 있는 형식에 대한 자리 표시자를 포함하며 템플릿으로 작동하는 클래스, 구조체 또는 인터페이스 선언입니다. 예를 들어 <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> 클래스는 키와 값의 두 형식을 포함할 수 있습니다. 제네릭 형식 정의는 템플릿일 뿐이므로 제네릭 형식 정의인 클래스, 구조체 또는 인터페이스의 인스턴스를 만들 수는 없습니다.  
  
-   *제네릭 형식 매개 변수*( *형식 매개 변수*)는 제네릭 형식 또는 메서드 정의의 자리 표시자입니다. <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> 제네릭 형식에는 키와 값의 형식을 나타내는 두 형식 매개 변수 `TKey` 및 `TValue`가 포함되어 있습니다.  
  
-   *생성된 제네릭 형식*( *생성된 형식*)은 제네릭 형식 정의의 제네릭 형식 매개 변수에 대한 형식을 지정한 결과로 생성된 형식입니다.  
  
-   *제네릭 형식 인수* 는 제네릭 형식 매개 변수에 대해 대체되는 모든 형식입니다.  
  
-   일반 용어인 *제네릭 형식* 에는 생성된 형식과 제네릭 형식 정의가 모두 포함됩니다.  
  
-   *공변성(covariance)* 및 *반공변성(contravariance)* 제네릭 형식 매개 변수를 사용하면 형식 인수가 생성된 대상 형식보다 더 많이 파생(공변성)되거나 더 적게 파생(반공변성)된 생성된 제네릭 형식을 사용할 수 있습니다. 공 분산과 반공 분산을 통칭하여 *가변성(variance)* 이라고 합니다. 자세한 내용은 [공변성(Covariance) 및 반공변성(Contravariance)](../../../docs/standard/generics/covariance-and-contravariance.md)을 참조하세요.  
  
-   *제약 조건*은 제네릭 형식 매개 변수에 대해 적용되는 제한 사항입니다. 예를 들어 형식 인스턴스의 순서를 지정할 수 있도록 <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> 제네릭 인터페이스를 구현하는 형식으로 형식 매개 변수를 제한할 수 있습니다. 또한 참조 형식 또는 값 형식이거나 특정 기본 클래스 또는 기본 생성자를 포함하는 형식으로 형식 매개 변수를 제한할 수도 있습니다. 제네릭 형식의 사용자는 제약 조건을 충족하지 않는 형식 인수를 대체할 수 없습니다.  
  
-   *제네릭 메서드 정의* 는 두 개의 매개 변수 목록(제네릭 형식 매개 변수 목록 및 정식 매개 변수 목록)을 포함하는 메서드입니다. 형식 매개 변수는 다음 코드에 나와 있는 것처럼 정식 매개 변수의 형식 또는 반환 형식으로 표시될 수 있습니다.  
  
 [!code-cpp[Conceptual.Generics.Overview#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#4)]
 [!code-csharp[Conceptual.Generics.Overview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#4)]
 [!code-vb[Conceptual.Generics.Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#4)]  
  
 제네릭 메서드는 제네릭 형식 또는 제네릭이 아닌 형식으로 표시될 수 있습니다. 메서드는 단순히 제네릭 형식에 속한다고 해서 제네릭인 것은 아니며, 형식이 바깥쪽 형식의 제네릭 매개 변수인 정식 매개 변수를 포함하더라도 제네릭은 아닙니다. 메서드는 자체 형식 매개 변수 목록을 포함하는 경우에만 제네릭입니다. 다음 코드에서는 `G` 메서드만 제네릭입니다.  
  
 [!code-cpp[Conceptual.Generics.Overview#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#5)]
 [!code-csharp[Conceptual.Generics.Overview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#5)]
 [!code-vb[Conceptual.Generics.Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#5)]  
  
 [맨 위로 이동](#top)  
  
<a name="advantages_limitations"></a>   
## <a name="advantages-and-disadvantages-of-generics"></a>제네릭의 장점 및 단점  
 제네릭 컬렉션과 대리자를 사용하는 경우의 장점은 다음과 같습니다.  
  
-   형식 안전성. 제네릭을 사용하면 컴파일러에서 형식 안전성을 보장해야 하는 부담이 없어집니다. 컴파일 타임에 올바른 데이터 형식이 적용되므로 코드를 작성하여 데이터 형식을 테스트할 필요가 없습니다. 형식 캐스팅의 필요성과 런타임 오류 발생 가능성도 감소합니다.  
  
-   코드의 양이 감소하며 코드를 보다 쉽게 다시 사용할 수 있습니다. 기본 형식에서 상속하고 멤버를 재정의할 필요가 없습니다. 예를 들어 <xref:System.Collections.Generic.LinkedList%601> 은 즉시 사용할 수 있습니다. 다음 변수 선언을 사용하면 문자열의 연결된 목록을 만들 수 있습니다.  
  
     [!code-cpp[HowToGeneric#24](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/source2.cpp#24)]
     [!code-csharp[HowToGeneric#24](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/source2.cs#24)]
     [!code-vb[HowToGeneric#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/source2.vb#24)]  
  
-   성능 향상. 제네릭 컬렉션 형식은 값 형식을 boxing할 필요가 없기 때문에 일반적으로 값 형식 저장 및 조작 시 성능이 보다 우수합니다.  
  
-   제네릭 대리자를 사용하면 여러 대리자 클래스를 만들지 않고도 형식이 안전한 콜백을 사용할 수 있습니다. 예를 들어 <xref:System.Predicate%601> 제네릭 대리자를 사용하면 특정 형식에 대해 고유한 검색 기준을 구현하는 메서드를 만든 다음 <xref:System.Array> , <xref:System.Array.Find%2A>, <xref:System.Array.FindLast%2A>등의 <xref:System.Array.FindAll%2A>형식 메서드와 함께 사용할 수 있습니다.  
  
-   제네릭을 통해 동적으로 생성된 코드를 원활하게 실행. 동적으로 생성된 코드에서 제네릭을 사용하는 경우 형식을 생성할 필요가 없습니다. 이로 인해 전체 어셈블리를 생성하는 대신 간단한 동적 메서드를 사용할 수 있는 시나리오의 수가 증가합니다. 자세한 내용은 [방법: 동적 메서드 정의 및 실행](../../../docs/framework/reflection-and-codedom/how-to-define-and-execute-dynamic-methods.md) 및 <xref:System.Reflection.Emit.DynamicMethod>을 참조하세요.  
  
 아래에는 제네릭의 몇 가지 제한이 나와 있습니다.  
  
-   제네릭 형식은 <xref:System.MarshalByRefObject> 와 같은 대부분의 기본 클래스에서 파생될 수 있으며, 제약 조건을 사용하면 제네릭 형식 매개 변수가 <xref:System.MarshalByRefObject>와 같은 기본 클래스에서 파생되어야 하도록 지정할 수 있습니다. 그러나 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 에서는 컨텍스트에 바인딩된 제네릭 형식을 지원하지 않습니다. 제네릭 형식이 <xref:System.ContextBoundObject>에서 파생될 수는 있지만 해당 형식의 인스턴스를 만들려고 하면 <xref:System.TypeLoadException>이 발생합니다.  
  
-   열거형은 제네릭 형식 매개 변수를 포함할 수 없습니다. 열거형은 Visual Basic, C# 또는 C++를 사용하여 정의되는 제네릭 형식에 중첩되는 경우 부수적으로만 제네릭이 될 수 있습니다. 자세한 내용은 [Common Type System](../../../docs/standard/base-types/common-type-system.md)에서 “열거”를 참조하세요.  
  
-   경량의 동적 메서드는 제네릭이 될 수 없습니다.  
  
-   Visual Basic, C# 및 C++에서는 모든 바깥쪽 형식의 형식 매개 변수에 형식이 할당된 경우가 아니면 제네릭 형식으로 묶인 중첩 형식을 인스턴스화할 수 없습니다. 다시 말해서, 리플렉션에서 이러한 언어를 사용하여 정의되는 중첩 형식은 모든 바깥쪽 형식의 형식 매개 변수를 포함합니다. 따라서 바깥쪽 형식의 형식 매개 변수를 중첩 형식의 멤버 정의에서 사용할 수 있습니다. 자세한 내용은 <xref:System.Type.MakeGenericType%2A>의 "중첩 형식"을 참조하세요.  
  
    > [!NOTE]
    >  동적 어셈블리에서 코드를 내보내거나 [Ilasm.exe(IL 어셈블러)](../../../docs/framework/tools/ilasm-exe-il-assembler.md)를 사용하여 정의되는 중첩 형식은 바깥쪽 형식의 형식 매개 변수를 포함하지 않아도 됩니다. 그러나 형식 매개 변수를 포함하지 않는 경우에는 중첩 클래스의 범위 내에 형식 매개 변수가 포함되지 않습니다.  
  
     자세한 내용은 <xref:System.Type.MakeGenericType%2A>의 "중첩 형식"을 참조하세요.  
  
 [맨 위로 이동](#top)  
  
<a name="class_library_and_language_support"></a>   
## <a name="class-library-and-language-support"></a>클래스 라이브러리 및 언어 지원  
 .NET에서는 다음 네임스페이스에서 다양한 제네릭 컬렉션 클래스를 제공합니다.  
  
-   <xref:System.Collections.Generic> 네임스페이스에는 <xref:System.Collections.Generic.List%601> 및 <xref:System.Collections.Generic.Dictionary%602> 제네릭 클래스와 같이 .NET에서 제공하는 대부분의 제네릭 컬렉션 형식이 포함되어 있습니다.  
  
-   <xref:System.Collections.ObjectModel> 네임스페이스에는 클래스 사용자에게 개체 모델을 노출하는 데 유용한 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 제네릭 클래스와 같은 추가 제네릭 컬렉션 형식이 포함되어 있습니다.  
  
 정렬 및 같음 비교를 구현하는 제네릭 인터페이스는 이벤트 처리기, 변환 및 검색 조건자용 제네릭 대리자 형식과 함께 <xref:System> 네임스페이스에서 제공됩니다.  
  
 제네릭 형식 및 제네릭 메서드 검사를 위한 <xref:System.Reflection> 네임스페이스, 제네릭 형식과 메서드를 포함하는 동적 어셈블리 내보내기를 위한 <xref:System.Reflection.Emit> 네임스페이스 그리고 제네릭을 포함하는 소스 그래프 생성을 위한 <xref:System.CodeDom> 네임스페이스에 제네릭 지원이 추가되었습니다.  
  
 공용 언어 런타임에서는 <xref:System.Reflection.Emit.OpCodes.Stelem>, <xref:System.Reflection.Emit.OpCodes.Ldelem>, <xref:System.Reflection.Emit.OpCodes.Unbox_Any>, <xref:System.Reflection.Emit.OpCodes.Constrained>, <xref:System.Reflection.Emit.OpCodes.Readonly>등의 MSIL(Microsoft Intermediate Language)에서 제네릭 형식을 지원하기 위한 새로운 opcode 및 접두사를 제공합니다.  
  
 Visual C++, C# 및 Visual Basic은 모두 제네릭 정의 및 사용을 위한 모든 지원을 제공합니다. 언어 지원에 대한 자세한 내용은 [Visual Basic의 제네릭 형식](~/docs/visual-basic/programming-guide/language-features/data-types/generic-types.md), [제네릭 소개](~/docs/csharp/programming-guide/generics/introduction-to-generics.md) 및 [Visual C++의 제네릭 개요](/cpp/windows/overview-of-generics-in-visual-cpp)를 참조하세요.  
  
 [맨 위로 이동](#top)  
  
<a name="nested_types_and_generics"></a>   
## <a name="nested-types-and-generics"></a>중첩 형식 및 제네릭  
 제네릭 형식에 중첩된 형식은 바깥쪽 제네릭 형식의 형식 매개 변수에 따라 달라질 수 있습니다. 공용 언어 런타임은 고유한 제네릭 형식 매개 변수를 포함하지 않는 중첩 형식도 제네릭으로 간주합니다. 중첩 형식의 인스턴스를 만들 때는 모든 바깥쪽 제네릭 형식에 대해 형식 인수를 지정해야 합니다.  
  
 [맨 위로 이동](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[.NET의 제네릭 컬렉션](../../../docs/standard/generics/collections.md)|.NET의 제네릭 컬렉션 클래스 및 기타 제네릭 형식에 대해 설명합니다.|  
|[배열과 목록을 조작하기 위한 제네릭 대리자](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)|배열 또는 컬렉션의 요소에 대해 수행할 작업, 검색 조건자 및 변환을 위한 제네릭 대리자에 대해 설명합니다.|  
|[제네릭 인터페이스](../../../docs/standard/generics/interfaces.md)|여러 제네릭 형식 패밀리에 대해 공통 기능을 제공하는 제네릭 인터페이스에 대해 설명합니다.|  
|[공 분산 및 반공 분산](../../../docs/standard/generics/covariance-and-contravariance.md)|제네릭 형식 매개 변수의 공 분산(covariance) 및 반공변성(contravariance)에 대해 설명합니다.|  
|[일반적으로 사용되는 컬렉션 형식](../../../docs/standard/collections/commonly-used-collection-types.md)|제네릭 형식을 비롯하여 .NET의 컬렉션 형식 특성과 사용 시나리오에 대한 요약 정보를 제공합니다.|  
|[제네릭 컬렉션 사용 기준](../../../docs/standard/collections/when-to-use-generic-collections.md)|제네릭 컬렉션 형식의 사용 시기를 결정하기 위한 일반 규칙을 설명합니다.|  
|[방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)|제네릭 형식과 메서드가 포함된 동적 어셈블리를 생성하는 방법을 설명합니다.|  
|[Generic Types in Visual Basic](~/docs/visual-basic/programming-guide/language-features/data-types/generic-types.md)|제네릭 형식 사용 및 정의에 대한 방법 항목을 포함하여 Visual Basic 사용자를 위한 제네릭 기능에 대해 설명합니다.|  
|[제네릭 소개](~/docs/csharp/programming-guide/generics/introduction-to-generics.md)|C# 사용자를 위한 제네릭 형식 사용 및 정의 방법을 간략하게 설명합니다.|  
|[Visual C++의 제네릭 개요](/cpp/windows/overview-of-generics-in-visual-cpp)|제네릭과 템플릿 간의 차이점을 비롯하여 C++ 사용자를 위한 제네릭 기능에 대해 설명합니다.|  
  
<a name="reference"></a>   
## <a name="reference"></a>참조  
 <xref:System.Collections.Generic>  
  
 <xref:System.Collections.ObjectModel>  
  
 <xref:System.Reflection.Emit.OpCodes?displayProperty=nameWithType>  
  
 [맨 위로 이동](#top)
