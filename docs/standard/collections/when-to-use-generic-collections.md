---
title: 제네릭 컬렉션 사용 기준
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- collections [.NET Framework], generic
- generic collections [.NET Framework]
ms.assetid: e7b868b1-11fe-4ac5-bed3-de68aca47739
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9831212cf65e3913bae2431e4746b5def03430b6
ms.sourcegitcommit: 700b9003ea6bdd83a53458bbc436c9b5778344f1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48261237"
---
# <a name="when-to-use-generic-collections"></a>제네릭 컬렉션 사용 기준
제네릭 컬렉션을 사용하면 기본 컬렉션 형식에서 파생하고 형식별 멤버를 구현하지 않아도 형식 보안 이점이 즉시 제공되므로 일반적으로는 제네릭 컬렉션을 사용하는 것이 좋습니다. 또한 컬렉션 요소가 값 형식일 때는 대개 제네릭 컬렉션 형식이 해당하는 제네릭이 아닌 컬렉션 형식 및 제네릭이 아닌 기본 컬렉션 형식에서 파행되는 형식에 비해 성능도 뛰어납니다. 제네릭을 사용하는 경우에는 요소를 boxing할 필요가 없기 때문입니다.  
  
 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 이상을 대상으로 하는 프로그램의 경우에는 여러 스레드가 컬렉션에서 동시에 항목을 추가하거나 제거하는 경우 <xref:System.Collections.Concurrent> 네임스페이스에서 제네릭 컬렉션 클래스를 사용해야 합니다.  
  
 기존 컬렉션 형식에 해당하는 제네릭 형식은 다음과 같습니다.  
  
-   <xref:System.Collections.Generic.List%601> 는 <xref:System.Collections.ArrayList>에 해당하는 제네릭 클래스입니다.  
  
-   <xref:System.Collections.Generic.Dictionary%602> 및 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> 는 <xref:System.Collections.Hashtable>에 해당하는 제네릭 클래스입니다.  
  
-   <xref:System.Collections.ObjectModel.Collection%601> 는 <xref:System.Collections.CollectionBase>에 해당하는 제네릭 클래스입니다. <xref:System.Collections.ObjectModel.Collection%601> 는 기본 클래스로 사용할 수 있지만 <xref:System.Collections.CollectionBase>와는 달리 추상 클래스가 아니므로 훨씬 쉽게 사용할 수 있습니다.  
  
-   <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 는 <xref:System.Collections.ReadOnlyCollectionBase>에 해당하는 제네릭 클래스입니다. <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 는 추상 클래스가 아니며 기존 <xref:System.Collections.Generic.List%601> 를 읽기 전용 컬렉션으로 쉽게 노출할 수 있는 생성자를 포함합니다.  
  
-   <xref:System.Collections.Generic.Queue%601>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, <xref:System.Collections.Generic.Stack%601>, <xref:System.Collections.Concurrent.ConcurrentStack%601>, <xref:System.Collections.Generic.SortedList%602> 제네릭 클래스는 각각 같은 이름의 제네릭이 아는 클래스에 해당합니다.  
  
## <a name="additional-types"></a>추가 형식  
 다수의 제네릭 컬렉션 형식에는 그에 해당하는 제네릭이 아닌 형식이 없습니다. 이러한 형식은 다음과 같습니다.  
  
-   <xref:System.Collections.Generic.LinkedList%601> 는 O(1) 삽입 및 제거 작업을 제공하는 범용 연결된 목록입니다.  
  
-   <xref:System.Collections.Generic.SortedDictionary%602> 는 O(로그 `n`) 삽입 및 검색 작업을 제공하는 정렬된 사전으로, <xref:System.Collections.Generic.SortedList%602>대신 사용하면 유용합니다.  
  
-   <xref:System.Collections.ObjectModel.KeyedCollection%602> 은 자체 키를 포함하는 개체를 저장할 수 있도록 하는 목록과 사전 간의 하이브리드 형식입니다.  
  
-   <xref:System.Collections.Concurrent.BlockingCollection%601> 는 경계 및 차단 기능을 포함하는 컬렉션 클래스를 구현합니다.  
  
-   <xref:System.Collections.Concurrent.ConcurrentBag%601> 는 순서가 지정되지 않은 요소의 빠른 삽입 및 제거 기능을 제공합니다.  
  
## <a name="linq-to-objects"></a>LINQ to Objects  
 LINQ to Objects 기능을 사용하면 개체 형식이 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 또는 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 인터페이스를 구현하는 경우 LINQ 쿼리를 통해 메모리 내 개체에 액세스할 수 있습니다. LINQ 쿼리는 데이터 액세스를 위한 일반 패턴을 제공하고, 표준 `foreach` 루프에 비해 간결하고 쉽게 읽을 수 있으며, 필터링, 순서 지정 및 그룹화 기능을 제공합니다. 또한 LINQ 쿼리를 통해 성능을 향상시킬 수도 있습니다. 자세한 내용은 [LINQ to Objects](https://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9) 및 [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)를 참조하세요.  
  
## <a name="additional-functionality"></a>추가 기능  
 일부 제네릭 형식은 제네릭이 아닌 컬렉션 형식에는 없는 기능을 포함합니다. 예를 들어 제네릭이 아닌 <xref:System.Collections.Generic.List%601> 클래스에 해당하는 <xref:System.Collections.ArrayList> 클래스에는 제네릭 대리자를 허용하는 여러 메서드가 포함되어 있습니다. 이러한 대리자로는 목록 검색을 위한 메서드를 지정할 수 있도록 하는 <xref:System.Predicate%601> 대리자, 목록의 각 요소에 대해 작동하는 메서드를 나타내는 <xref:System.Action%601> 대리자, 형식 간의 변환을 정의할 수 있도록 하는 <xref:System.Converter%602> 대리자 등이 있습니다.  
  
 <xref:System.Collections.Generic.List%601> 클래스를 사용하면 목록 검색 및 정렬을 위해 <xref:System.Collections.Generic.IComparer%601> 제네릭 인터페이스 구현을 직접 지정할 수 있습니다. <xref:System.Collections.Generic.SortedDictionary%602> 및 <xref:System.Collections.Generic.SortedList%602> 클래스에도 이 기능이 있습니다. 또한 이러한 클래스를 사용하는 경우 컬렉션을 만들 때 비교자를 지정할 수 있습니다. 마찬가지로 <xref:System.Collections.Generic.Dictionary%602> 및 <xref:System.Collections.ObjectModel.KeyedCollection%602> 클래스에서도 고유한 같음 비교자를 지정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [컬렉션 및 데이터 구조](../../../docs/standard/collections/index.md)  
- [일반적으로 사용되는 컬렉션 형식](../../../docs/standard/collections/commonly-used-collection-types.md)  
- [제네릭](../../../docs/standard/generics/index.md)
