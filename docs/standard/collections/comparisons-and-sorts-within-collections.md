---
title: 컬렉션 내에서 비교 및 정렬
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sorting data, collections
- IComparable.CompareTo method
- Collections classes
- Equals method
- collections [.NET Framework], comparisons
ms.assetid: 5e4d3b45-97f0-423c-a65f-c492ed40e73b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2d9124c90d09e2fa94a0eaa2ff8cd4e4ab15206f
ms.sourcegitcommit: ced0cccf15adfd492f8196cb739f01dde52c9252
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67135665"
---
# <a name="comparisons-and-sorts-within-collections"></a>컬렉션 내에서 비교 및 정렬
<xref:System.Collections> 클래스는 제거할 요소 검색, 키-값 쌍의 값 반환 등 컬렉션 관리와 관련된 거의 모든 프로세스에서 비교를 수행합니다.  
  
 컬렉션은 일반적으로 같음 비교자 및/또는 순서 비교자를 사용합니다. 비교에는 두 가지 구문이 사용됩니다.  
  
<a name="BKMK_Checkingforequality"></a>   
## <a name="checking-for-equality"></a>같음 확인  
 `Contains`, <xref:System.Collections.IList.IndexOf%2A>, <xref:System.Collections.Generic.List%601.LastIndexOf%2A>, `Remove` 등의 메서드는 컬렉션 요소에 대해 같음 비교자를 사용합니다. 제네릭 컬렉션의 경우 다음 지침에 따라 항목이 같은지를 비교합니다.  
  
- T 형식이 <xref:System.IEquatable%601> 제네릭 인터페이스를 구현하는 경우 같음 비교자는 해당 인터페이스의 <xref:System.IEquatable%601.Equals%2A> 메서드입니다.  
  
- T 형식이 <xref:System.IEquatable%601>을 구현하지 않는 경우에는 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 가 사용됩니다.  
  
 또한 사전 컬렉션의 일부 생성자 오버로드는 키가 같은지를 비교하는 데 사용되는 <xref:System.Collections.Generic.IEqualityComparer%601> 구현을 허용합니다. 예제를 보려면 <xref:System.Collections.Generic.Dictionary%602.%23ctor%2A?displayProperty=nameWithType> 생성자를 참조하세요.  
  
<a name="BKMK_Determiningsortorder"></a>   
## <a name="determining-sort-order"></a>정렬 순서 결정  
 `BinarySearch` 및 `Sort` 와 같은 메서드는 컬렉션 요소에 대해 순서 비교자를 사용합니다. 컬렉션의 요소를 비교할 수도 있고 특정 요소와 지정된 값을 비교할 수도 있습니다. 개체를 비교하는 경우에는 `default comparer` 및 `explicit comparer`의 개념이 적용됩니다.  
  
 기본 비교자는 비교 대상 개체 중 하나 이상을 사용하여 **IComparable** 인터페이스를 구현합니다. 사용되는 모든 클래스에 대해 **IComparable** 을 목록 컬렉션의 값 또는 사전 컬렉션의 키로 구현하는 것이 좋습니다. 제네릭 컬렉션의 경우 다음 기준에 따라 같음 비교를 결정합니다.  
  
- T 형식이 <xref:System.IComparable%601?displayProperty=nameWithType> 제네릭 인터페이스를 구현하는 경우 기본 비교자는 해당 인터페이스의 <xref:System.IComparable%601.CompareTo%28%600%29?displayProperty=nameWithType> 메서드입니다.  
  
- T 형식이 제네릭이 아닌 <xref:System.IComparable?displayProperty=nameWithType> 인터페이스를 구현하는 경우 기본 비교자는 해당 인터페이스의 <xref:System.IComparable.CompareTo%28System.Object%29?displayProperty=nameWithType> 메서드입니다.  
  
- T 형식이 두 인터페이스를 모두 구현하지 않는 경우에는 기본 비교자가 없으며 비교자 또는 비교 대리자를 명시적으로 제공해야 합니다.  
  
 명시적 비교를 제공할 수 있도록 일부 메서드는 매개 변수로 **IComparer** 구현을 허용합니다. 예를 들어 <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> 메서드는 <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> 구현을 허용합니다.  
  
 시스템의 현재 문화권 설정은 컬렉션 내의 비교와 정렬에 영향을 줄 수 있습니다. 기본적으로 **Collections** 클래스의 비교 및 정렬은 문화권을 구분합니다. 문화권 설정을 무시하고 동일한 비교 및 정렬 결과가 반환되도록 하려면 <xref:System.Globalization.CultureInfo.InvariantCulture%2A> 를 허용하는 멤버 오버로드를 포함하여 <xref:System.Globalization.CultureInfo>를 사용합니다. 자세한 내용은 [Performing Culture-Insensitive String Operations in Collections](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md) 및 [Performing Culture-Insensitive String Operations in Arrays](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-arrays.md)를 참조하세요.  
  
<a name="BKMK_Equalityandsortexample"></a>   
## <a name="equality-and-sort-example"></a>같음 및 정렬 예제  
 다음 코드에서는 간단한 비즈니스 개체에 대한 <xref:System.IEquatable%601> 및 <xref:System.IComparable%601> 의 구현을 보여 줍니다. 또한 개체를 목록에 저장하고 정렬할 때 <xref:System.Collections.Generic.List%601.Sort> 메서드를 호출하면 `Part` 형식에 대해 기본 비교자가 사용되며, 무명 메서드를 사용하여 <xref:System.Collections.Generic.List%601.Sort%28System.Comparison%7B%600%7D%29> 메서드가 구현됩니다.  
  
 [!code-csharp[System.Collections.Generic.List.Sort#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.collections.generic.list.sort/cs/program.cs#1)]
 [!code-vb[System.Collections.Generic.List.Sort#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.collections.generic.list.sort/vb/module1.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.IComparer>
- <xref:System.IEquatable%601>
- <xref:System.Collections.Generic.IComparer%601>
- <xref:System.IComparable>
- <xref:System.IComparable%601>
