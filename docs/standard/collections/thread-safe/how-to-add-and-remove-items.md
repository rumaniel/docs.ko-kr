---
title: '방법: ConcurrentDictionary에서 항목 추가 및 제거'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- thread-safe collections, concurrent dictionary
ms.assetid: 81b64b95-13f7-4532-9249-ab532f629598
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9d8b1c63f10d1d79c3fec6cad87c9a82f03716c8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54543424"
---
# <a name="how-to-add-and-remove-items-from-a-concurrentdictionary"></a>방법: ConcurrentDictionary에서 항목 추가 및 제거
이 예제는 <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=nameWithType>에서 항목을 추가, 검색, 업데이트 및 제거하는 방법을 보여 줍니다. 이 컬렉션 클래스는 스레드로부터 안전하게 구현됩니다. 여러 스레드에서 컬렉션에 동시에 액세스할 수 있을 때는 언제든지 이 클래스를 사용하는 것이 좋습니다.  
  
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>에서는 추가하거나 제거하려고 시도하기 전에 키의 존재 여부를 먼저 확인하는 코드가 필요하지 않게 하는 편리한 몇 가지 메서드를 제공합니다. 다음 표에서는 이처럼 편리한 메서드를 나열하고 해당 메서드가 사용되는 경우에 대해 설명합니다.  
  
|메서드|사용 시기...|  
|------------|---------------|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>|지정된 키의 새 값을 추가하려는 경우 및 이미 존재하는 키의 값을 바꾸려는 경우|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>|지정된 키의 기존 값을 검색하려는 경우 및 존재하지 않는 키/값 쌍을 지정하려는 경우|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryAdd%2A>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryGetValue%2A> , <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryUpdate%2A> , <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryRemove%2A>|키/값 쌍 추가, 가져오기, 업데이트 또는 제거를 수행하려는 경우 및 어떤 이유로 인해 이러한 시도가 실패하거나 이미 키가 존재할 때 다른 작업을 대신 수행하려는 경우|  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 <xref:System.Threading.Tasks.Task> 인스턴스를 사용하여 일부 요소를 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>에 동시에 추가한 다음 모든 콘텐츠를 출력하여 해당 요소가 성공적으로 추가되었음을 보여 줍니다. 또한 이 예제에서는 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>, <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> 및 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> 메서드를 사용하여 컬렉션의 항목을 추가, 업데이트 및 검색하는 방법을 보여 줍니다.  
  
 [!code-csharp[CDS#16](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/cds_dictionaryhowto.cs#16)]
 [!code-vb[CDS#16](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/cds_concdict.vb#16)]  
  
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>는 다중 스레드 시나리오를 위해 설계되었습니다. 이 컬렉션에서 항목을 추가하거나 제거하기 위해 코드에 잠금을 사용할 필요는 없습니다. 그러나 동일한 키에 새 값을 지정하여 한 스레드에서 값을 검색하고 다른 스레드에서 컬렉션을 바로 업데이트하는 것은 언제든지 가능합니다.  
  
 또한 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>의 모든 메서드가 스레드로부터 안전하지만 모든 메서드, 특히 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> 및 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>가 원자성 메서드인 것은 아닙니다. 이러한 메서드에 전달되는 사용자 대리자는 사전의 내부 잠금 밖에서 호출됩니다(이는 알 수 없는 코드에서 모든 스레드를 차단하는 것을 방지하기 위해 수행됨). 따라서 다음과 같은 이벤트 시퀀스가 발생할 수 있습니다.  
  
 1\) threadA에서 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>를 호출하고, 항목을 찾지 못하면, valueFactory 대리자를 호출하여 Add에 새 항목을 만듭니다.  
  
 2\) threadB에서 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>를 동시에 호출하고, 해당 valueFactory 대리자가 호출된 다음 threadA보다 먼저 내부 잠금에 도달하여 threadB의 새 키-값 쌍이 사전에 추가됩니다.  
  
 3\) threadA의 사용자 대리자가 완료되고 스레드가 잠금에 도달하지만 이제는 해당 항목이 이미 존재하는 것으로 표시됩니다.  
  
 4\) threadA에서 "Get"을 수행하고 이전에 threadB에서 추가한 데이터를 반환합니다.  
  
 따라서 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>에서 반환한 데이터가 스레드의 valueFactory에서 만든 것과 동일한 데이터라고 보장되지 않습니다. <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>를 호출할 때에도 비슷한 이벤트 시퀀스가 발생할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Concurrent?displayProperty=nameWithType>
- [스레드로부터 안전한 컬렉션](../../../../docs/standard/collections/thread-safe/index.md)
