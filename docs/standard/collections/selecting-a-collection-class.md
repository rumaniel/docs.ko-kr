---
title: Collection 클래스 선택
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- last-in-first-out collections
- first-in-first-out collections
- collections [.NET Framework], selecting collection class
- indexed collections
- Collections classes
- grouping data in collections, selecting collection class
ms.assetid: ba049f9a-ce87-4cc4-b319-3f75c8ddac8a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d84bc5ac2256139626311ff7c848170c28ffbd5b
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836513"
---
# <a name="selecting-a-collection-class"></a>Collection 클래스 선택
컬렉션 클래스를 신중하게 선택해야 합니다. 잘못된 형식을 사용하면 컬렉션 사용이 제한될 수 있습니다. 일반적으로, .NET Framework 버전 1.1을 대상으로 하지 않는 한 <xref:System.Collections> 네임스페이스의 형식을 사용하지 마세요. 형식 안전성이 더 크고 기타 향상된 기능이 있는 제네릭 버전과 동시 버전의 컬렉션을 사용하는 것이 좋습니다.  
  
 다음 질문을 살펴보세요.  
  
-   값을 검색한 후 요소가 일반적으로 삭제되는 순차적 목록이 필요한가요?  
  
    -   예인 경우 FIFO(선입선출) 동작이 필요하면 <xref:System.Collections.Queue> 클래스 또는 <xref:System.Collections.Generic.Queue%601> 제네릭 클래스를 사용합니다. LIFO(후입선출) 동작이 필요하면 <xref:System.Collections.Stack> 클래스 또는 <xref:System.Collections.Generic.Stack%601> 제네릭 클래스를 사용합니다. 여러 스레드에서 안전하게 액세스하려면 동시 버전 <xref:System.Collections.Concurrent.ConcurrentQueue%601> 및 <xref:System.Collections.Concurrent.ConcurrentStack%601>을 사용합니다.  
  
    -   그러지 않은 경우 다른 컬렉션을 사용합니다.  
  
-   FIFO, LIFO, 무작위와 같은 특정 순서대로 요소에 액세스해야 하나요?  
  
    -   <xref:System.Collections.Queue> 클래스와 <xref:System.Collections.Generic.Queue%601> 또는 <xref:System.Collections.Concurrent.ConcurrentQueue%601> 제네릭 클래스는 FIFO 액세스를 제공합니다. 자세한 내용은 [스레드로부터 안전한 컬렉션 사용 시기](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md)를 참조하세요.  
  
    -   <xref:System.Collections.Stack> 클래스와 <xref:System.Collections.Generic.Stack%601> 또는 <xref:System.Collections.Concurrent.ConcurrentStack%601> 제네릭 클래스는 LIFO 액세스를 제공합니다. 자세한 내용은 [스레드로부터 안전한 컬렉션 사용 시기](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md)를 참조하세요.  
  
    -   <xref:System.Collections.Generic.LinkedList%601> 제네릭 클래스는 헤드에서 테일로 또는 테일에서 헤드로 순차적 액세스를 허용합니다.  
  
-   인덱스를 기준으로 각 요소에 액세스해야 하나요?  
  
    -   <xref:System.Collections.ArrayList> 및 <xref:System.Collections.Specialized.StringCollection> 클래스와 <xref:System.Collections.Generic.List%601> 제네릭 클래스는 0부터 시작하는 요소 인덱스를 기준으로 해당 요소에 대한 액세스를 제공합니다.  
  
    -   <xref:System.Collections.Hashtable>, <xref:System.Collections.SortedList>, <xref:System.Collections.Specialized.ListDictionary> 및 <xref:System.Collections.Specialized.StringDictionary> 클래스와 <xref:System.Collections.Generic.Dictionary%602> 및 <xref:System.Collections.Generic.SortedDictionary%602> 제네릭 클래스는 요소 키를 기준으로 해당 요소에 대한 액세스를 제공합니다.  
  
    -   <xref:System.Collections.Specialized.NameObjectCollectionBase> 및 <xref:System.Collections.Specialized.NameValueCollection> 클래스와 <xref:System.Collections.ObjectModel.KeyedCollection%602> 및 <xref:System.Collections.Generic.SortedList%602> 제네릭 클래스는 0부터 시작하는 요소 인덱스 또는 키를 기준으로 해당 요소에 대한 액세스를 제공합니다.  
  
-   각 요소에 값 한 개, 키 한 개와 값 한 개의 조합 또는 키 한 개와 여러 값의 조합이 포함되나요?  
  
    -   값 한 개: <xref:System.Collections.IList> 인터페이스 또는 <xref:System.Collections.Generic.IList%601> 제네릭 인터페이스를 기준으로 컬렉션을 사용합니다.  
  
    -   키 한 개와 값 한 개: <xref:System.Collections.IDictionary> 인터페이스 또는 <xref:System.Collections.Generic.IDictionary%602> 제네릭 인터페이스를 기준으로 컬렉션을 사용합니다.  
  
    -   포함된 키가 있는 값 한 개: <xref:System.Collections.ObjectModel.KeyedCollection%602> 제네릭 클래스를 사용합니다.  
  
    -   키 한 개와 여러 값: <xref:System.Collections.Specialized.NameValueCollection> 클래스를 사용합니다.  
  
-   입력된 순서와 다르게 요소를 정렬해야 하나요?  
  
    -   <xref:System.Collections.Hashtable> 클래스는 해시 코드를 기준으로 요소를 정렬합니다.  
  
    -   <xref:System.Collections.SortedList> 클래스와 <xref:System.Collections.Generic.SortedDictionary%602> 및 <xref:System.Collections.Generic.SortedList%602> 제네릭 클래스는 <xref:System.Collections.IComparer> 인터페이스 및 <xref:System.Collections.Generic.IComparer%601> 제네릭 인터페이스의 구현에 따라 키를 기준으로 요소를 정렬합니다.  
  
    -   <xref:System.Collections.ArrayList>에서는 <xref:System.Collections.IComparer> 구현을 매개 변수로 사용하는 <xref:System.Collections.ArrayList.Sort%2A> 메서드를 제공합니다. 해당하는 제네릭 항목인 <xref:System.Collections.Generic.List%601> 제네릭 클래스는 <xref:System.Collections.Generic.IComparer%601> 제네릭 인터페이스의 구현을 매개 변수로 사용하는 <xref:System.Collections.Generic.List%601.Sort%2A> 메서드를 제공합니다.  
  
-   빠른 검색 및 정보 검색이 필요한가요?  
  
    -   작은 컬렉션(10개 항목 이하)의 경우 <xref:System.Collections.Specialized.ListDictionary>가 <xref:System.Collections.Hashtable>보다 빠릅니다. <xref:System.Collections.Generic.Dictionary%602> 제네릭 클래스는 <xref:System.Collections.Generic.SortedDictionary%602> 제네릭 클래스보다 빠른 조회 기능을 제공합니다. 다중 스레드 구현은 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>입니다. <xref:System.Collections.Concurrent.ConcurrentBag%601>은 순서가 지정되지 않은 데이터에 대한 신속한 다중 스레드 삽입 기능을 제공합니다. 두 가지 다중 스레드 형식에 대한 자세한 내용은 [스레드로부터 안전한 컬렉션 사용 시기](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md)를 참조하세요.  
  
-   문자열만 수락하는 컬렉션이 필요한가요?  
  
    -   <xref:System.Collections.Specialized.StringCollection>(<xref:System.Collections.IList> 기반) 및 <xref:System.Collections.Specialized.StringDictionary>(<xref:System.Collections.IDictionary> 기반)는 <xref:System.Collections.Specialized> 네임스페이스에 있습니다.  
  
    -   또한 제네릭 형식 인수에 대해 <xref:System.String> 클래스를 지정하여 <xref:System.Collections.Generic> 네임스페이스의 제네릭 컬렉션 클래스 중 하나를 강력한 형식의 문자열 컬렉션으로 사용할 수 있습니다.  
  
## <a name="linq-to-objects-and-plinq"></a>LINQ to Objects 및 PLINQ  
 LINQ to Objects를 사용하면 개체 형식이 <xref:System.Collections.IEnumerable> 또는 <xref:System.Collections.Generic.IEnumerable%601>를 구현하는 경우 개발자가 LINQ 쿼리를 통해 메모리 내 개체에 액세스할 수 있습니다. LINQ 쿼리는 데이터 액세스를 위한 일반 패턴을 제공하고, 표준 `foreach` 루프에 비해 간결하고 쉽게 읽을 수 있으며, 필터링, 순서 지정 및 그룹화 기능을 제공합니다. 자세한 내용은 [LINQ to Objects](https://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9)를 참조하세요.  
  
 PLINQ는 다중 코어 컴퓨터의 보다 효율적인 사용을 통해 많은 시나리오에서 더 빠른 쿼리 실행을 제공할 수 있는 LINQ to Objects의 병렬 구현을 제공합니다. 자세한 내용은 [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections>  
- <xref:System.Collections.Specialized>  
- <xref:System.Collections.Generic>  
- [스레드로부터 안전한 컬렉션](../../../docs/standard/collections/thread-safe/index.md)
