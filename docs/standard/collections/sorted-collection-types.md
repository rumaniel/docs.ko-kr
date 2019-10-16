---
title: Sorted 컬렉션 형식
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- SortedDictionary collection type
- SortedList class, grouping data in collections
- grouping data in collections, SortedList collection type
- SortedList collection type
- collections [.NET Framework], SortedList collection type
ms.assetid: 3db965b2-36a6-4b12-b76e-7f074ff7275a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c49b3fcd5b50cc5b48497dcf97862e80b066ab46
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957877"
---
# <a name="sorted-collection-types"></a>Sorted 컬렉션 형식
<xref:System.Collections.SortedList?displayProperty=nameWithType> 클래스, <xref:System.Collections.Generic.SortedList%602?displayProperty=nameWithType> 제네릭 클래스 및 <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=nameWithType> 제네릭 클래스는 <xref:System.Collections.Hashtable> 클래스 및 <xref:System.Collections.Generic.Dictionary%602> 제네릭 클래스와 유사합니다. 해당 항목은 여기서 <xref:System.Collections.IDictionary> 인터페이스를 구현하지만 키를 기준으로 한 정렬 순서로 해당 요소를 유지 관리하고 O(1) 삽입 및 해시 테이블의 검색 특성을 갖지 않습니다. 세 가지 클래스에는 공통적으로 다음과 같은 몇 가지 기능이 있습니다.  
  
- 세 가지 클래스는 모두 <xref:System.Collections.IDictionary?displayProperty=nameWithType> 인터페이스를 구현합니다. 두 개의 제네릭 인터페이스는 <xref:System.Collections.Generic.IDictionary%602?displayProperty=nameWithType> 제네릭 클래스도 구현합니다.  
  
- 각 요소는 열거형에 사용할 키/값 쌍입니다.  
  
    > [!NOTE]
    > 제네릭 클래스가 아닌 <xref:System.Collections.SortedList> 클래스는 열거될 때 <xref:System.Collections.DictionaryEntry> 개체를 반환하지만 두 개의 제네릭 형식은 <xref:System.Collections.Generic.KeyValuePair%602> 개체를 반환합니다.  
  
- 요소는 <xref:System.Collections.IComparer?displayProperty=nameWithType> 구현(제네릭 클래스가 아닌 <xref:System.Collections.SortedList>의 경우) 또는 <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> 구현(두 개의 제네릭 클래스의 경우)에 따라 정렬됩니다.  
  
- 각 클래스는 키만 포함하거나 값만 포함하는 컬렉션을 반환하는 속성을 제공합니다.  
  
 다음 표에서는 두 개의 정렬된 목록 클래스 및 <xref:System.Collections.Generic.SortedDictionary%602> 클래스 간의 차이점을 나열합니다.  
  
|<xref:System.Collections.SortedList> 제네릭이 아닌 클래스 및 <xref:System.Collections.Generic.SortedList%602> 제네릭 클래스|<xref:System.Collections.Generic.SortedDictionary%602> 제네릭 클래스|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|키와 값을 반환하는 속성은 인덱스되어 인덱싱된 효율적인 검색을 허용합니다.|인덱스된 검색이 없습니다.|  
|검색은 O(로그 `n`)입니다.|검색은 O(로그 `n`)입니다.|  
|삽입 및 제거는 일반적으로 O(`n`)이지만 정렬 순서로 나열된 데이터의 경우 삽입은 O(로그 `n`)이므로 각 요소가 목록 끝에 추가됩니다. (여기서는 크기 조정이 필요하지 않다고 가정합니다.)|삽입과 제거는 O(로그 `n`)입니다.|  
|<xref:System.Collections.Generic.SortedDictionary%602>보다 적은 메모리를 사용합니다.|<xref:System.Collections.SortedList> 제네릭이 아닌 클래스와 <xref:System.Collections.Generic.SortedList%602> 제네릭 클래스보다 더 많은 메모리를 사용합니다.|  
  
 여러 스레드에서 동시에 액세스할 수 있어야 하는 정렬된 목록 또는 사전의 경우 정렬 논리를 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>에서 파생된 클래스에 추가할 수 있습니다.  
  
> [!NOTE]
> 고유한 키를 포함하는 값(예: 직원 ID 번호를 포함하는 직원 레코드)의 경우 <xref:System.Collections.ObjectModel.KeyedCollection%602> 제네릭 클래스에서 파생하여 목록의 일부 특성 및 사전의 일부 특성을 가진 키가 지정된 컬렉션을 만들 수 있습니다.  
  
 .NET Framework 4부터 <xref:System.Collections.Generic.SortedSet%601> 클래스는 삽입, 삭제 및 검색 후에 정렬된 순서에 따라 데이터를 유지 관리하는 자체 균형 조정 트리를 제공합니다. 이 클래스와 <xref:System.Collections.Generic.HashSet%601> 클래스는 <xref:System.Collections.Generic.ISet%601> 인터페이스를 구현합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.IDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Generic.IDictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.Concurrent.ConcurrentDictionary%602>
- [일반적으로 사용되는 컬렉션 형식](../../../docs/standard/collections/commonly-used-collection-types.md)
