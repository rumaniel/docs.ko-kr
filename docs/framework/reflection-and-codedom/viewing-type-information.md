---
title: 형식 정보 보기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- types, viewing type information
- Type object
- viewing type information
- reflection, viewing type information
ms.assetid: 7e7303a9-4064-4738-b4e7-b75974ed70d2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a5417f330040c2b6ce08a53920f9a92117624a80
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045768"
---
# <a name="viewing-type-information"></a>형식 정보 보기
<xref:System.Type?displayProperty=nameWithType> 클래스는 리플렉션의 핵심입니다. 공용 언어 런타임은 리플렉션이 요청할 때 로드된 형식의 **Type**을 만듭니다. **Type** 개체의 메서드, 필드, 속성 및 중첩 클래스를 사용하여 해당 형식에 대한 모든 것을 찾을 수 있습니다.  
  
 <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> 또는 <xref:System.Reflection.Assembly.GetTypes%2A?displayProperty=nameWithType>를 사용하여 로드되지 않은 어셈블리에서 **Type** 개체를 가져와 원하는 형식 또는 형식 이름을 전달합니다. <xref:System.Type.GetType%2A?displayProperty=nameWithType>을 사용하여 이미 로드된 어셈블리에서 **Type** 개체를 가져옵니다. <xref:System.Reflection.Module.GetType%2A?displayProperty=nameWithType> 및 <xref:System.Reflection.Module.GetTypes%2A?displayProperty=nameWithType>를 사용하여 모듈 **Type** 개체를 가져옵니다.  
  
> [!NOTE]
> 제네릭 형식 및 메서드를 검사하고 조작하려면 [리플렉션 및 제네릭 형식](reflection-and-generic-types.md) 및 [방법: 리플렉션을 사용하여 제네릭 형식 검사 및 인스턴스화](how-to-examine-and-instantiate-generic-types-with-reflection.md)를 참조하세요.  
  
 다음 예제에서는 어셈블리에 대한 <xref:System.Reflection.Assembly> 개체 및 모듈을 가져오는 데 필요한 구문을 보여 줍니다.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source5.cpp#6)]
 [!code-csharp[Conceptual.Types.ViewInfo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source5.cs#6)]
 [!code-vb[Conceptual.Types.ViewInfo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source5.vb#6)]  
  
 다음 예제에서는 로드된 어셈블리에서 **Type** 개체를 가져오는 방법을 보여 줍니다.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source5.cpp#7)]
 [!code-csharp[Conceptual.Types.ViewInfo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source5.cs#7)]
 [!code-vb[Conceptual.Types.ViewInfo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source5.vb#7)]  
  
 **Type**을 가져온 후 해당 형식의 멤버에 대한 정보를 검색할 수 있는 다양한 방법이 있습니다. 예를 들어 현재 형식의 각 멤버를 설명하는 <xref:System.Reflection.MemberInfo> 개체의 배열을 가져오는 <xref:System.Type.GetMembers%2A?displayProperty=nameWithType> 메서드를 호출하여 모든 형식의 멤버에 대한 정보를 찾을 수 있습니다.  
  
 **Type** 클래스에서 메서드를 사용하여 이름으로 지정하는 하나 이상의 생성자, 메서드, 이벤트, 필드 또는 속성에 대한 정보를 검색할 수도 있습니다. 예를 들어 <xref:System.Type.GetConstructor%2A?displayProperty=nameWithType>는 현재 클래스의 특정 생성자를 캡슐화합니다.  
  
 **Type**이 있는 경우 <xref:System.Type.Module%2A?displayProperty=nameWithType> 속성을 사용하여 해당 형식이 포함된 모듈을 캡슐화하는 개체를 가져올 수 있습니다. <xref:System.Reflection.Module.Assembly%2A?displayProperty=nameWithType> 속성을 사용하여 모듈이 포함된 어셈블리를 캡슐화하는 개체를 찾습니다. <xref:System.Type.Assembly%2A?displayProperty=nameWithType> 속성을 사용하여 직접 형식을 캡슐화하는 어셈블리를 가져올 수 있습니다.  
  
## <a name="systemtype-and-constructorinfo"></a>System.Type 및 ConstructorInfo  
 다음 예제에서는 클래스(이 경우 <xref:System.String> 클래스)에 대한 생성자를 나열하는 방법을 보여 줍니다.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source1.cpp#1)]
 [!code-csharp[Conceptual.Types.ViewInfo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source1.cs#1)]
 [!code-vb[Conceptual.Types.ViewInfo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source1.vb#1)]  
  
## <a name="memberinfo-methodinfo-fieldinfo-and-propertyinfo"></a>MemberInfo, MethodInfo, FieldInfo 및 PropertyInfo  
 <xref:System.Reflection.MemberInfo>, <xref:System.Reflection.MethodInfo>, <xref:System.Reflection.FieldInfo> 또는 <xref:System.Reflection.PropertyInfo> 개체를 사용하여 형식의 메서드, 속성, 이벤트 및 필드에 대한 정보를 가져옵니다.  
  
 다음 예제에서는 **MemberInfo**를 사용하여 **System.IO.File** 클래스의 멤버 수를 나열하고, <xref:System.Type.IsPublic%2A> 속성을 사용하여 클래스의 표시 유형을 결정합니다.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source2.cpp#2)]
 [!code-csharp[Conceptual.Types.ViewInfo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source2.cs#2)]
 [!code-vb[Conceptual.Types.ViewInfo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source2.vb#2)]  
  
 다음 예제에서는 지정된 멤버의 형식을 조사합니다. **MemberInfo** 클래스의 멤버에 대한 리플렉션을 수행하고 해당 형식을 나열합니다.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source3.cpp#3)]
 [!code-csharp[Conceptual.Types.ViewInfo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source3.cs#3)]
 [!code-vb[Conceptual.Types.ViewInfo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source3.vb#3)]  
  
 다음 예제에서는 모든 Reflection **\*Info** 클래스를 <xref:System.Reflection.BindingFlags>와 함께 사용하여 지정된 클래스의 모든 멤버(생성자, 필드, 속성, 이벤트 및 메서드)를 나열하고 멤버를 정적 및 인스턴스 범주로 구분합니다.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source4.cpp#4)]
 [!code-csharp[Conceptual.Types.ViewInfo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source4.cs#4)]
 [!code-vb[Conceptual.Types.ViewInfo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source4.vb#4)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.BindingFlags>
- <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.GetTypes%2A?displayProperty=nameWithType>
- <xref:System.Type.GetType%2A?displayProperty=nameWithType>
- <xref:System.Type.GetMembers%2A?displayProperty=nameWithType>
- <xref:System.Type.GetFields%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Module.GetType%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Module.GetTypes%2A?displayProperty=nameWithType>
- <xref:System.Reflection.MemberInfo>
- <xref:System.Reflection.ConstructorInfo>
- <xref:System.Reflection.MethodInfo>
- <xref:System.Reflection.FieldInfo>
- <xref:System.Reflection.EventInfo>
- <xref:System.Reflection.ParameterInfo>
- [리플렉션 및 제네릭 형식](reflection-and-generic-types.md)
