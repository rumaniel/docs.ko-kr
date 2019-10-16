---
title: 리플렉션 및 제네릭 형식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generics [.NET Framework], reflection emit
- reflection emit, generic types
- reflection, generic types
- type arguments
- generics [.NET Framework], reflection
- viewing type information
- type information, viewing
- types, generic
- type parameters
ms.assetid: f7180fc5-dd41-42d4-8a8e-1b34288e06de
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ce40a54e82e95f41247db525110c510e3d83031e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045925"
---
# <a name="reflection-and-generic-types"></a>리플렉션 및 제네릭 형식
<a name="top"></a> 리플렉션의 관점에서 제네릭 형식과 일반 형식 간 차이점은 제네릭 형식이 형식 매개 변수(제네릭 형식 정의인 경우) 또는 형식 인수(생성된 형식인 경우)의 집합과 연결되어 있다는 점입니다. 제네릭 메서드는 동일한 방식으로 일반 메서드와 다릅니다.  
  
 다음과 같이 리플렉션이 제네릭 형식 및 메서드를 처리하는 방법을 이해하기 위한 두 가지 키가 있습니다.  
  
- 제네릭 형식 정의 및 제네릭 메서드 정의의 형식 매개 변수는 <xref:System.Type> 클래스의 인스턴스로 표현됩니다.  
  
    > [!NOTE]
    > <xref:System.Type> 의 여러 속성 및 메서드는 <xref:System.Type> 개체가 제네릭 형식 매개 변수를 나타낼 때 다른 동작을 내포합니다. 이러한 차이는 속성 및 메서드 항목에 설명되어있습니다. 예제는 <xref:System.Type.IsAutoClass%2A> 및 <xref:System.Type.DeclaringType%2A>을 참조하세요. 또한 일부 멤버는 <xref:System.Type> 개체가 제네릭 형식 매개 변수를 나타낼 경우에만 유효합니다. 예제는 <xref:System.Type.GetGenericTypeDefinition%2A>을 참조하세요.  
  
- <xref:System.Type> 의 인스턴스가 제네릭 형식을 나타내면 형식 매개 변수(제네릭 형식 정의의 경우) 또는 형식 인수(생성된 형식의 경우)를 나타내는 형식의 배열이 포함됩니다. 제네릭 메서드를 나타내는 <xref:System.Reflection.MethodInfo> 클래스의 인스턴스에서도 똑같습니다.  
  
 리플렉션은 <xref:System.Type> 및 <xref:System.Reflection.MethodInfo>의 메서드를 제공합니다. 이 메서드를 통해 형식 매개 변수의 배열에 액세스할 수 있으며, <xref:System.Type>의 인스턴스가 형식 매개 변수를 나타내는지 또는 실제 형식을 나타내는지 확인할 수 있습니다.  
  
 여기에서 설명한 메서드를 보여 주는 코드 예제는 [방법: 리플렉션을 사용하여 제네릭 형식 검사 및 인스턴스화](how-to-examine-and-instantiate-generic-types-with-reflection.md)를 참조하세요.  
  
 다음 논의에서는 형식 매개 변수 및 인수와 개방형 또는 폐쇄형의 생성된 형식 간 차이점과 같은 제네릭 용어에 익숙하다고 가정합니다. 자세한 내용은 [제네릭](../../standard/generics/index.md)을 참조하세요.  
  
 이 개요는 다음과 같은 섹션으로 구성되어 있습니다.  
  
- [제네릭 형식인가요 아니면 제네릭 메서드인가요?](#is_this_a_generic_type_or_method)  
  
- [폐쇄형 제네릭 형식 생성](#generating_closed_generic_types)  
  
- [형식 인수 및 형식 매개 변수 검사](#examining_type_arguments)  
  
- [고정](#invariants)  
  
- [관련 항목](#related_topics)  
  
<a name="is_this_a_generic_type_or_method"></a>   
## <a name="is-this-a-generic-type-or-method"></a>제네릭 형식인가요 아니면 제네릭 메서드인가요?  
 리플렉션을 사용하여 <xref:System.Type>의 인스턴스에서 나타내는 알 수 없는 형식을 검사할 때 알 수 없는 형식이 제네릭인지 여부를 확인하는 데 <xref:System.Type.IsGenericType%2A> 속성을 사용합니다. 형식이 제네릭 경우 `true` 를 반환합니다. 마찬가지로 리플렉션을 사용하여 <xref:System.Reflection.MethodInfo> 클래스의 인스턴스에서 나타내는 알 수 없는 메서드를 검사할 때 메서드가 제네릭인지 여부를 확인하는 데 <xref:System.Reflection.MethodBase.IsGenericMethod%2A> 속성을 사용합니다.  
  
### <a name="is-this-a-generic-type-or-method-definition"></a>제네릭 형식인가요 아니면 메서드 정의인가요?  
 <xref:System.Type.IsGenericTypeDefinition%2A> 속성을 사용하여 <xref:System.Type> 개체가 제네릭 형식 정의를 나타내는지를 확인하고, <xref:System.Reflection.MethodBase.IsGenericMethodDefinition%2A> 메서드를 사용하여 <xref:System.Reflection.MethodInfo> 개체가 제네릭 메서드 정의를 나타내는지를 확인합니다.  
  
 제네릭 형식 및 메서드 정의는 인스턴스화할 수 있는 형식을 생성하는 템플릿입니다. <xref:System.Collections.Generic.Dictionary%602>와 같은 .NET Framework 클래스 라이브러리의 제네릭 형식은 제네릭 형식 정의입니다.  
  
### <a name="is-the-type-or-method-open-or-closed"></a>형식 또는 메서드가 개방형인가요 아니면 폐쇄형인가요?  
 인스턴스화할 수 있는 형식이 모든 바깥쪽 형식의 모든 형식 매개 변수를 비롯하여 모든 해당 형식 매개 변수를 대체한 경우 제네릭 형식 또는 메서드는 폐쇄형입니다. 폐쇄형인 경우 제네릭 형식의 인스턴스만 만들 수 있습니다. 형식이 개방형인 경우 <xref:System.Type.ContainsGenericParameters%2A?displayProperty=nameWithType> 속성에서 `true` 를 반환합니다. 메서드의 경우 <xref:System.Reflection.MethodBase.ContainsGenericParameters%2A?displayProperty=nameWithType> 메서드가 같은 기능을 수행합니다.  
  
 [맨 위로 이동](#top)  
  
<a name="generating_closed_generic_types"></a>   
## <a name="generating-closed-generic-types"></a>폐쇄형 제네릭 형식 생성  
 제네릭 형식 또는 메서드 정의가 있으면 <xref:System.Type.MakeGenericType%2A> 메서드를 사용하여 폐쇄형 제네릭 형식을 만들거나 <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A> 메서드를 사용하여 폐쇄형 제네릭 형식의 <xref:System.Reflection.MethodInfo> 를 만듭니다.  
  
### <a name="getting-the-generic-type-or-method-definition"></a>제네릭 형식 또는 메서드 정의 가져오기  
 제네릭 형식 또는 메서드 정의가 아닌 개방형 제네릭 형식 또는 메서드가 있는 경우 해당 인스턴스를 만들 수 없으며 누락된 형식 매개 변수를 제공할 수 없습니다. 제네릭 형식 또는 메서드 정의가 있어야 합니다. <xref:System.Type.GetGenericTypeDefinition%2A> 메서드를 사용하여 제네릭 형식 정의를 가져오거나 <xref:System.Reflection.MethodInfo.GetGenericMethodDefinition%2A> 메서드를 사용하여 제네릭 메서드 정의를 가져옵니다.  
  
 예를 들어 <xref:System.Type> (Visual Basic의 `Dictionary<int, string>` )을 나타내는`Dictionary(Of Integer, String)` 개체가 있으며 `Dictionary<string, MyClass>`형식을 만들려는 경우 <xref:System.Type.GetGenericTypeDefinition%2A> 메서드를 사용하여 <xref:System.Type> 를 나타내는 `Dictionary<TKey, TValue>` 을 가져온 후 <xref:System.Type.MakeGenericType%2A> 메서드를 사용하여 <xref:System.Type> 를 나타내는 `Dictionary<int, MyClass>`을 생성할 수 있습니다.  
  
 제네릭 형식이 아닌 개방형 제네릭 형식의 예제는 이 항목의 뒷부분에 나오는 "형식 매개 변수 또는 형식 인수"를 참조하세요.  
  
 [맨 위로 이동](#top)  
  
<a name="examining_type_arguments"></a>   
## <a name="examining-type-arguments-and-type-parameters"></a>형식 인수 및 형식 매개 변수 검사  
 <xref:System.Type.GetGenericArguments%2A?displayProperty=nameWithType> 메서드를 사용하여 제네릭 형식의 형식 매개 변수 또는 형식 인수를 나타내는 <xref:System.Type> 개체의 배열을 가져오고, <xref:System.Reflection.MethodInfo.GetGenericArguments%2A?displayProperty=nameWithType> 메서드를 사용하여 제네릭 메서드에 대해 동일한 작업을 수행합니다.  
  
 <xref:System.Type> 개체가 형식 매개 변수를 나타내는 것을 알고 있다면 리플렉션이 대답할 수 있는 추가 질문이 많습니다. 형식 매개 변수의 소스, 해당 위치 및 해당 제약 조건을 확인할 수 있습니다.  
  
### <a name="type-parameter-or-type-argument"></a>형식 매개 변수 또는 형식 인수  
 배열의 특정 요소가 형식 매개 변수인지 또는 형식 인수인지 확인하려면 <xref:System.Type.IsGenericParameter%2A> 속성을 사용합니다. 요소가 형식 매개 변수인 경우 <xref:System.Type.IsGenericParameter%2A> 속성은 `true` 입니다.  
  
 제네릭 형식은 제네릭 형식 정의 없이 열릴 수 있으며, 이 경우에 형식 인수 및 형식 매개 변수가 혼합됩니다. 예를 들어 다음 코드에서 `D` 클래스는 `D` 의 첫 번째 형식 매개 변수로 `B`의 두 번째 형식 매개 변수를 대체하여 생성한 형식에서 파생됩니다.  
  
```csharp  
class B<T, U> {}  
class D<V, W> : B<int, V> {}  
```  
  
```vb  
Class B(Of T, U)  
End Class  
Class D(Of V, W)  
    Inherits B(Of Integer, V)  
End Class  
```  
  
```cpp  
generic<typename T, typename U> ref class B {};  
generic<typename V, typename W> ref class D : B<int, V> {};  
```  
  
 <xref:System.Type> 를 나타내는 `D<V, W>` 개체를 가져오고 <xref:System.Type.BaseType%2A> 속성을 사용하여 해당 기본 형식을 가져오는 경우 결과적으로 `type B<int, V>` 가 열리지만 제네릭 형식 정의는 아닙니다.  
  
### <a name="source-of-a-generic-parameter"></a>제네릭 매개 변수의 소스  
 제네릭 형식 매개 변수는 검사 중인 형식, 바깥쪽 형식 또는 제네릭 메서드에서 가져올 수 있습니다. 다음과 같이 제네릭 형식 매개 변수의 소스를 확인할 수 있습니다.  
  
- 먼저, <xref:System.Type.DeclaringMethod%2A> 속성을 사용하여 형식 매개 변수가 제네릭 메서드에서 가져온 것인지 확인합니다. 속성 값이 null 참조(Visual Basic의`Nothing` )가 아니면 소스가 제네릭 메서드입니다.  
  
- 소스가 제네릭 메서드가 아닌 경우 <xref:System.Type.DeclaringType%2A> 속성을 사용하여 제네릭 형식 매개 변수가 속한 제네릭 형식을 확인합니다.  
  
 형식 매개 변수가 제네릭 메서드에 속한 경우 <xref:System.Type.DeclaringType%2A> 속성은 관련이 없는 제네릭 메서드를 선언한 형식을 반환합니다.  
  
### <a name="position-of-a-generic-parameter"></a>제네릭 매개 변수의 위치  
 선언하는 해당 클래스의 형식 매개 변수 목록에서 형식 매개 변수의 위치를 확인할 필요가 가끔 있습니다. 예를 들어 앞의 예제에서 <xref:System.Type> 형식을 나타내는 `B<int, V>` 개체가 있다고 가정합니다. <xref:System.Type.GetGenericArguments%2A> 메서드는 형식 인수의 목록을 제공하므로 `V` 를 검사할 경우 <xref:System.Type.DeclaringMethod%2A> 및 <xref:System.Type.DeclaringType%2A> 속성을 사용하여 어디에서 가져왔는지 검색할 수 있습니다. 그런 다음 <xref:System.Type.GenericParameterPosition%2A> 속성을 사용하여 원래 정의된 형식 매개 변수 목록에서 해당 위치를 확인할 수 있습니다. 이 예제에서 `V` 는 원래 정의된 형식 매개 변수 목록에서 0(영) 위치에 있습니다.  
  
### <a name="base-type-and-interface-constraints"></a>기본 형식 및 인터페이스 제약 조건  
 <xref:System.Type.GetGenericParameterConstraints%2A> 메서드를 사용하여 형식 매개 변수의 기본 형식 제약 조건 및 인터페이스 제약 조건을 가져옵니다. 배열 요소의 순서는 중요하지 않습니다. 요소는 인터페이스 형식인 경우 인터페이스 제약 조건을 나타냅니다.  
  
### <a name="generic-parameter-attributes"></a>제네릭 매개 변수 특성  
 <xref:System.Type.GenericParameterAttributes%2A> 속성은 형식 매개 변수의 분산(공 분산 및 반공 분산) 및 특별 제약 조건을 나타내는 <xref:System.Reflection.GenericParameterAttributes> 값을 가져옵니다.  
  
#### <a name="covariance-and-contravariance"></a>공 분산 및 반공 분산  
 형식 매개 변수가 공 분산인지 또는 반공 분산인지 확인하려면 <xref:System.Reflection.GenericParameterAttributes.VarianceMask?displayProperty=nameWithType> 마스크를 <xref:System.Reflection.GenericParameterAttributes> 속성에서 반환한 <xref:System.Type.GenericParameterAttributes%2A> 값에 적용합니다. 결과가 <xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType>인 경우 형식 매개 변수는 고정입니다. [공변성(Covariance) 및 반공변성(Contravariance)](../../standard/generics/covariance-and-contravariance.md)을 참조하세요.  
  
#### <a name="special-constraints"></a>특별 제약 조건  
 형식 매개 변수의 특별 제약 조건을 확인하려면 <xref:System.Reflection.GenericParameterAttributes.SpecialConstraintMask?displayProperty=nameWithType> 마스크를 <xref:System.Reflection.GenericParameterAttributes> 속성에서 반환한 <xref:System.Type.GenericParameterAttributes%2A> 값에 적용합니다. 결과가 <xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType>인 경우 특별 제약 조건이 없습니다. 형식 매개 변수는 참조 형식이어야 하고 Nullable이 아닌 값 형식이어야 하며 그리고 매개 변수가 없는 생성자를 보유해야 하는 제약을 받습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="invariants"></a>   
## <a name="invariants"></a>고정  
 제네릭 형식에 대한 리플렉션의 일반적인 용어에 대한 고정 조건 표는 <xref:System.Type.IsGenericType%2A?displayProperty=nameWithType>을 참조하세요. 제네릭 메서드와 관련된 추가 용어는 <xref:System.Reflection.MethodBase.IsGenericMethod%2A?displayProperty=nameWithType>를 참조하세요.  
  
 [맨 위로 이동](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[방법: 리플렉션을 사용하여 제네릭 형식 검사 및 인스턴스화](how-to-examine-and-instantiate-generic-types-with-reflection.md)|<xref:System.Type> 및 <xref:System.Reflection.MethodInfo>의 속성 및 메서드를 사용하여 제네릭 형식을 검사하는 방법을 보여 줍니다.|  
|[제네릭](../../standard/generics/index.md)|제네릭 기능 및 .NET Framework에서 제네릭 기능을 지원하는 방법을 설명합니다.|  
|[방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의](how-to-define-a-generic-type-with-reflection-emit.md)|리플렉션 내보내기를 사용하여 동적 어셈블리에서 제네릭 형식을 생성하는 방법을 보여 줍니다.|  
|[형식 정보 보기](viewing-type-information.md)|<xref:System.Type> 클래스를 설명하고 <xref:System.Type>과 다양한 리플렉션 클래스를 함께 사용하여 생성자, 메서드, 필드, 속성, 이벤트에 대한 정보를 가져오는 방법을 보여 주는 코드 예제를 제공합니다.|
