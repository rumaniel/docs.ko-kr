---
title: 특성에 저장된 정보 검색
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- retrieving attributes
- multiple attribute instances
- attributes [.NET Framework], retrieving
ms.assetid: 37dfe4e3-7da0-48b6-a3d9-398981524e1c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8873b4938f654213bd659631175ba4526a35dcc3
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957335"
---
# <a name="retrieving-information-stored-in-attributes"></a>특성에 저장된 정보 검색
사용자 지정 특성 검색은 간단한 프로세스입니다. 먼저, 검색하려는 특성의 인스턴스를 선언합니다. 그런 다음, <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=nameWithType> 메서드를 사용하여 검색하려는 특성 값으로 새 특성을 초기화합니다. 새 특성이 초기화되면 해당 속성을 사용하여 값을 가져오기만 하면 됩니다.  
  
> [!IMPORTANT]
> 이 항목에서는 실행 컨텍스트에 로드된 코드에 대한 특성을 검색하는 방법을 설명합니다. 리플렉션 전용 컨텍스트에 로드 된 코드의 특성을 검색 하려면 다음과 같이 <xref:System.Reflection.CustomAttributeData> 클래스 [를 사용 해야 합니다. 어셈블리를 리플렉션 전용 컨텍스트에](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)로드 합니다.  
  
 이 섹션에서는 특성을 검색하는 다음 방법에 대해 설명합니다.  
  
- [특성의 단일 인스턴스 검색](#cpconretrievingsingleinstanceofattribute)  
  
- [동일한 범위에 적용된 특성의 다중 인스턴스 검색](#cpconretrievingmultipleinstancesofattributeappliedtosamescope)  
  
- [다양한 범위에 적용된 특성의 다중 인스턴스 검색](#cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes)  
  
<a name="cpconretrievingsingleinstanceofattribute"></a>   
## <a name="retrieving-a-single-instance-of-an-attribute"></a>특성의 단일 인스턴스 검색  
 다음 예제에서 `DeveloperAttribute`(이전 섹션에 설명되어 있음)는 클래스 수준의 `MainApp` 클래스에 적용됩니다. `GetAttribute` 메서드는 클래스 수준의 `DeveloperAttribute`에 저장된 값을 콘솔에 표시하기 전에 먼저 **GetCustomAttribute**를 사용하여 검색합니다.  
  
 [!code-cpp[Conceptual.Attributes.Usage#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#18)]
 [!code-csharp[Conceptual.Attributes.Usage#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#18)]
 [!code-vb[Conceptual.Attributes.Usage#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#18)]  
  
 이 프로그램은 실행 시 다음 텍스트를 표시합니다.  
  
```console  
The Name Attribute is: Joan Smith.  
The Level Attribute is: 42.  
The Reviewed Attribute is: True.  
```  
  
 특성을 찾을 수 없는 경우 **GetCustomAttribute** 메서드는 `MyAttribute`를 null 값으로 초기화합니다. 이 예제는 해당 인스턴스의 `MyAttribute`를 확인하고 특성을 찾을 수 없는 경우 사용자에게 알립니다. 클래스 범위에서 `DeveloperAttribute`를 찾을 수 없는 경우 다음 메시지가 콘솔에 표시됩니다.  
  
```console  
The attribute was not found.   
```  
  
 이 예제에서는 특성 정의가 현재 네임스페이스에 있다고 가정합니다. 현재 네임스페이스에 없는 경우 특성 정의가 있는 네임스페이스를 가져와야 합니다.  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtosamescope"></a>   
## <a name="retrieving-multiple-instances-of-an-attribute-applied-to-the-same-scope"></a>동일한 범위에 적용된 특성의 다중 인스턴스 검색  
 이전 예제에서는 검사할 클래스 및 찾을 특정 특성이 <xref:System.Attribute.GetCustomAttribute%2A>에 전달됩니다. 특성의 인스턴스 하나만 클래스 수준에서 적용되는 경우 해당 코드가 제대로 작동됩니다. 그러나 특성의 여러 인스턴스가 동일한 클래스 수준에서 적용되는 경우 **GetCustomAttribute** 메서드가 모든 정보를 검색하지 못합니다. 동일한 특성의 여러 인스턴스가 동일한 범위에 적용되는 경우 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>를 사용하여 특성의 모든 인스턴스를 배열에 배치할 수 있습니다. 예를 들어 `DeveloperAttribute`의 두 인스턴스가 동일한 클래스의 클래스 수준에서 적용되는 경우 `GetAttribute` 메서드를 수정하여 두 특성 모두에서 찾은 정보를 표시할 수 있습니다. 동일한 수준의 여러 특성을 적용하려면 <xref:System.AttributeUsageAttribute>에서 **AllowMultiple** 속성을 **true**로 설정하여 특성을 정의해야 합니다.  
  
 다음 코드 예제에서는 **GetCustomAttributes** 메서드를 사용하여 지정된 특정 클래스에서 `DeveloperAttribute`의 모든 인스턴스를 참조하는 배열을 만드는 방법을 보여줍니다. 이렇게 하면 모든 특성 값이 콘솔에 표시됩니다.  
  
 [!code-cpp[Conceptual.Attributes.Usage#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#19)]
 [!code-csharp[Conceptual.Attributes.Usage#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#19)]
 [!code-vb[Conceptual.Attributes.Usage#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#19)]  
  
 특성을 찾을 수 없는 경우 이 코드는 사용자에게 경고를 표시합니다. 특성을 찾은 경우 `DeveloperAttribute`의 두 인스턴스 모두에 포함된 정보가 표시됩니다.  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes"></a>   
## <a name="retrieving-multiple-instances-of-an-attribute-applied-to-different-scopes"></a>다양한 범위에 적용된 특성의 다중 인스턴스 검색  
 <xref:System.Attribute.GetCustomAttributes%2A> 및 <xref:System.Attribute.GetCustomAttribute%2A> 메서드는 클래스 전체를 검색하지 않고 해당 클래스 특성의 모든 인스턴스를 반환합니다. 대신, 한 번에 하나의 지정된 메서드 또는 멤버만 검색합니다. 모든 멤버에 동일한 특성이 적용된 클래스가 있는데 해당 멤버에 적용된 모든 특성의 값을 검색하려는 경우 모든 메서드 또는 멤버를 **GetCustomAttributes** 및 **GetCustomAttribute**에 개별적으로 제공해야 합니다.  
  
 다음 코드 예제에서는 클래스를 매개 변수로 사용하여 클래스 수준에서 그리고 해당 클래스의 모든 개별 메서드에서 `DeveloperAttribute`(이전에 정의됨)를 검색합니다.  
  
 [!code-cpp[Conceptual.Attributes.Usage#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#20)]
 [!code-csharp[Conceptual.Attributes.Usage#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#20)]
 [!code-vb[Conceptual.Attributes.Usage#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#20)]  
  
 메서드 수준 또는 클래스 수준에서 `DeveloperAttribute`의 인스턴스를 찾을 수 없는 경우 `GetAttribute` 메서드는 특성을 찾을 수 없음을 사용자에게 알리고 특성이 포함되지 않은 메서드 또는 클래스의 이름을 표시합니다. 특성을 찾은 경우 `Name`, `Level` 및 `Reviewed` 필드가 콘솔에 표시됩니다.  
  
 <xref:System.Type> 클래스의 멤버를 사용하여 전달된 클래스의 개별 메서드 및 멤버를 가져올 수 있습니다. 이 예제에서는 먼저 **Type** 개체를 쿼리하여 클래스 수준에 대한 특성 정보를 가져옵니다. 그런 다음, 메서드 수준의 특성 정보를 검색하기 위해 <xref:System.Type.GetMethods%2A?displayProperty=nameWithType>를 사용하여 모든 메서드의 인스턴스를 <xref:System.Reflection.MemberInfo?displayProperty=nameWithType> 개체의 배열에 배치합니다. 또한 <xref:System.Type.GetProperties%2A?displayProperty=nameWithType> 메서드를 사용하여 속성 수준의 특성을 확인하거나 <xref:System.Type.GetConstructors%2A?displayProperty=nameWithType>를 사용하여 생성자 수준의 특성을 확인할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Type?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>
- [특성](../../../docs/standard/attributes/index.md)
