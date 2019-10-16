---
title: 동적으로 형식 로드 및 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- late binding, about late binding
- early binding
- dynamically loading and using types
- implicit late binding
- reflection, dynamically using types
ms.assetid: db985bec-5942-40ec-b13a-771ae98623dc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 21d0425de072c91cf7111162e405f826e00e849d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046100"
---
# <a name="dynamically-loading-and-using-types"></a>동적으로 형식 로드 및 사용
리플렉션은 언어 컴파일러에서 암시적 런타임에 바인딩을 구현하는 데 사용되는 인프라를 제공합니다. 바인딩은 고유하게 지정된 형식에 해당하는 선언(즉, 구현)을 찾는 프로세스입니다. 이 프로세스가 컴파일 시간이 아닌 런타임에 수행되는 경우 이를 런타임에 바인딩이라고 합니다. Visual Basic을 통해 코드에서 암시적 런타임에 바인딩을 사용할 수 있고, Visual Basic 컴파일러는 리플렉션을 사용하여 개체 형식을 가져오는 도우미 메서드를 호출합니다. 인수가 도우미 메서드에 전달되면 런타임에 적절한 메서드가 호출됩니다. 이러한 인수는 메서드를 호출하는 인스턴스(개체), 호출된 메서드의 이름(문자열) 및 호출된 메서드에 전달된 인수(개체 배열)입니다.  
  
 다음 예제에서는 Visual Basic 컴파일러가 리플렉션을 암시적으로 사용하여 컴파일 시간에 형식이 알려지지 않은 개체에 대해 메서드를 호출합니다. **HelloWorld** 클래스에는 **PrintHello** 메서드에 전달되는 일부 텍스트와 연결된 "Hello World"를 출력하는 **PrintHello** 메서드가 포함됩니다. 이 예제에서 호출된 **PrintHello** 메서드는 실제로 <xref:System.Type.InvokeMember%2A?displayProperty=nameWithType>이고, Visual Basic 코드에서는 개체 형식(helloObj)이 런타임(런타임에 바인딩)이 아닌 컴파일 시간(초기 바인딩)에 알려진 것처럼 **PrintHello** 메서드를 호출할 수 있습니다.  
  
```vb
Module Hello  
    Sub Main()  
        ' Sets up the variable.  
        Dim helloObj As Object  
        ' Creates the object.  
        helloObj = new HelloWorld()  
        ' Invokes the print method as if it was early bound  
        ' even though it is really late bound.  
        helloObj.PrintHello("Visual Basic Late Bound")  
    End Sub  
End Module  
```  
  
## <a name="custom-binding"></a>사용자 지정 바인딩  
 리플렉션은 런타임에 바인딩을 위해 컴파일러에서 암시적으로 사용될 뿐만 아니라 코드에서 런타임에 바인딩을 수행하기 위해 명시적으로 사용될 수 있습니다.  
  
 [공용 언어 런타임](../../standard/clr.md)은 여러 가지 프로그래밍 언어를 지원하고 이러한 언어의 바인딩 규칙은 서로 다릅니다. 초기 바인딩된 경우 코드 생성기는 이 바인딩을 완전히 제어할 수 있습니다. 그러나 리플렉션을 통한 런타임에 바인딩에서는 사용자 지정된 바인딩을 통해 바인딩을 제어해야 합니다. <xref:System.Reflection.Binder> 클래스는 멤버 선택 및 호출의 사용자 지정 컨트롤을 제공합니다.  
  
 사용자 지정 바인딩을 사용하면 런타임에 어셈블리를 로드하고, 해당 어셈블리에서 형식 정보를 가져오고, 원하는 형식을 지정하고 나서, 해당 형식에 대한 메서드를 호출하거나 필드 또는 속성에 액세스할 수 있습니다. 개체 형식에 사용자 입력이 사용되는 경우와 같이 컴파일 시간에 개체 형식을 알 수 없는 경우 이 기술이 유용합니다.  
  
 다음 예제에서는 인수 형식 변환을 제공하지 않는 간단한 사용자 지정 바인더를 보여 줍니다. `Simple_Type.dll`에 대한 코드가 기본 예제 앞에 나와 있습니다. `Simple_Type.dll`을 빌드하고 나서 빌드 시간에 프로젝트에서 이에 대한 참조를 포함해야 합니다.  
  
 [!code-cpp[Conceptual.Types.Dynamic#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.dynamic/cpp/source1.cpp#1)]
 [!code-csharp[Conceptual.Types.Dynamic#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.dynamic/cs/source1.cs#1)]
 [!code-vb[Conceptual.Types.Dynamic#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.dynamic/vb/source1.vb#1)]  
  
### <a name="invokemember-and-createinstance"></a>InvokeMember 및 CreateInstance  
 <xref:System.Type.InvokeMember%2A?displayProperty=nameWithType>를 사용하여 형식의 멤버를 호출합니다. <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> 및 <xref:System.Reflection.Assembly.CreateInstance%2A?displayProperty=nameWithType>와 같은 다양한 클래스의 **CreateInstance** 메서드는 지정된 형식의 새 인스턴스를 만드는 **InvokeMember**의 형식으로 특수화됩니다. **Binder** 클래스는 이러한 메서드의 오버로드 확인 및 인수 강제 변환에 사용됩니다.  
  
 다음 예제에서는 인수 강제 변환(형식 변환) 및 멤버 선택의 세 가지 가능한 조합을 보여 줍니다. 사례 1에서는 인수 강제 변환 또는 멤버 선택이 필요하지 않습니다. 사례 2에서는 멤버 선택만 필요합니다. 사례 3에서는 인수 강제 변환만 필요합니다.  
  
 [!code-cpp[Conceptual.Types.Dynamic#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.dynamic/cpp/source2.cpp#2)]
 [!code-csharp[Conceptual.Types.Dynamic#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.dynamic/cs/source2.cs#2)]
 [!code-vb[Conceptual.Types.Dynamic#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.dynamic/vb/source2.vb#2)]  
  
 같은 이름을 가진 두 개 이상의 멤버를 사용할 수 있는 경우 오버로드 확인이 필요합니다. <xref:System.Reflection.Binder.BindToMethod%2A?displayProperty=nameWithType> 및 <xref:System.Reflection.Binder.BindToField%2A?displayProperty=nameWithType> 메서드는 바인딩을 단일 멤버로 확인하는 데 사용됩니다. 또한 **Binder.BindToMethod**는 **get** 및 **set** 속성 접근자를 통해 속성 확인을 제공합니다.  
  
 **BindToMethod**는 호출할 <xref:System.Reflection.MethodBase>를 반환하거나 해당 호출이 가능하지 않은 경우 null 참조(Visual Basic의 경우 **Nothing**)를 반환합니다. **MethodBase** 반환 값은 일반적인 사례인 경우에도 *match* 매개 변수에 포함된 값 중 하나일 필요가 없습니다.  
  
 ByRef 인수가 있으면 호출자가 해당 인수를 되찾으려고 할 수 있습니다. 따라서 **BindToMethod**가 인수 배열을 조작한 경우 **Binder**를 사용하여 클라이언트가 인수 배열을 다시 원래 폼에 매핑할 수 있습니다. 이 작업을 위해 호출자는 인수 순서가 변경되지 않도록 보장해야 합니다. 인수가 이름으로 저장되면 **Binder**는 인수 배열을 다시 정렬하고 호출자는 이 순서를 인식합니다. 자세한 내용은 <xref:System.Reflection.Binder.ReorderArgumentArray%2A?displayProperty=nameWithType>을 참조하세요.  
  
 사용 가능한 멤버 집합은 형식 또는 기본 형식에 정의된 멤버입니다. <xref:System.Reflection.BindingFlags>가 지정되면 접근성이 있는 멤버가 집합에 반환됩니다. **BindingFlags.NonPublic**이 지정되지 않으면 바인더가 접근성 규칙을 적용해야 합니다. **Public** 또는 **NonPublic** 바인딩 플래그를 지정할 경우에는 **Instance** 또는 **Static** 바인딩 플래그도 지정해야 합니다. 그렇지 않으면 멤버가 반환되지 않습니다.  
  
 지정된 이름의 멤버가 하나만 있는 경우에는 콜백이 필요하지 않고 바인딩이 해당 메서드에서 수행됩니다. 코드 예제의 사례 1은 이러한 점을 보여줍니다. 하나의 **PrintBob** 메서드만 사용할 수 있으므로 콜백이 필요하지 않습니다.  
  
 사용 가능한 집합에 두 개 이상의 멤버가 있으면 이러한 메서드가 모두 적절한 메서드를 선택하고 반환하는 **BindToMethod**에 전달됩니다. 코드 예제의 사례 2에는 **PrintValue**라는 두 개의 메서드가 있습니다. **BindToMethod**를 호출하여 적절한 메서드를 선택합니다.  
  
 <xref:System.Reflection.Binder.ChangeType%2A>은 실제 인수를 선택된 메서드의 형식 인수 형식으로 변환하는 인수 강제 변환(형식 변환)을 수행합니다. 형식이 정확히 일치하는 경우에도 모든 인수에 대해 **ChangeType**이 호출됩니다.  
  
 코드 예제의 사례 3에서 값이 5.5인 **String** 형식의 실제 인수가 **Double** 형식의 형식 인수와 함께 메서드에 전달됩니다. 호출이 성공하려면 문자열 값 "5.5"가 double 값으로 변환되어야 합니다. **ChangeType**이 이 변환을 수행합니다.  
  
 **ChangeType**은 다음 표에 나와 있는 대로 무손실 또는 [확대 강제 변환](../../standard/base-types/type-conversion.md)을 수행합니다.  
  
|소스 형식|대상 형식|  
|-----------------|-----------------|  
|모든 형식|기본 형식|  
|모든 형식|구현되는 인터페이스|  
|Char|UInt16, UInt32, Int32, UInt64, Int64, Single, Double|  
|Byte|Char, UInt16, Int16, UInt32, Int32, UInt64, Int64, Single, Double|  
|SByte|Int16, Int32, Int64, Single, Double|  
|UInt16|UInt32, Int32, UInt64, Int64, Single, Double|  
|Int16|Int32, Int64, Single, Double|  
|UInt32|UInt64, Int64, Single, Double|  
|Int32|Int64, Single, Double|  
|UInt64|Single, Double|  
|Int64|Single, Double|  
|Single|Double|  
|비참조 형식|참조 형식|  
  
 <xref:System.Type> 클래스에는 **Binder** 형식의 매개 변수를 사용하여 특정 멤버에 대한 참조를 확인하는 **Get** 메서드가 포함됩니다. <xref:System.Type.GetConstructor%2A?displayProperty=nameWithType>, <xref:System.Type.GetMethod%2A?displayProperty=nameWithType> 및 <xref:System.Type.GetProperty%2A?displayProperty=nameWithType>는 해당 멤버에 대한 시그니처 정보를 제공하여 현재 형식의 특정 멤버를 검색합니다. <xref:System.Reflection.Binder.SelectMethod%2A?displayProperty=nameWithType> 및 <xref:System.Reflection.Binder.SelectProperty%2A?displayProperty=nameWithType>는 해당하는 메서드의 지정된 시그니처 정보를 선택하기 위해 콜백됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Type.InvokeMember%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>
- [형식 정보 보기](viewing-type-information.md)
- [.NET Framework의 형식 변환](../../standard/base-types/type-conversion.md)
