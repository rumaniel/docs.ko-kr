---
title: 인덱싱된 컬렉션
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, forced
ms.assetid: 019008fe-4708-4e65-bebf-04fd9941e149
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 149597f0e34448d9c275a2cb8cd4ffc250bec619
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54492127"
---
# <a name="induced-collections"></a>인덱싱된 컬렉션
대부분의 경우 가비지 수집기가 수집을 수행할 적절한 시기를 결정할 수 있으며 가비지 수집기가 독립적으로 실행되는 것이 좋습니다. 강제된 컬렉션이 애플리케이션의 성능을 향상시키는 드문 경우도 있습니다. 이러한 경우에 가비지 수집을 강제하는 <xref:System.GC.Collect%2A?displayProperty=nameWithType> 메서드를 사용하여 가비지 수집을 유도할 수 있습니다.  
  
 애플리케이션 코드의 특정 지점에서 사용되는 메모리양이 상당히 감소하는 경우 <xref:System.GC.Collect%2A?displayProperty=nameWithType> 메서드를 사용합니다. 예를 들어 애플리케이션이 몇 가지 컨트롤이 있는 복잡한 대화 상자를 사용하는 경우 대화 상자를 닫을 때 <xref:System.GC.Collect%2A>를 호출하면 즉시 대화 상자에서 사용하는 메모리를 확보하여 성능을 개선할 수 있습니다. 가비지 수집기가 최적이 아닌 시간에 개체를 회수하려고 하는 경우 성능이 저하될 수 있기 때문에 애플리케이션이 너무 자주 가비지 수집을 발생시키지 않도록 합니다. 다음 섹션에서 설명된 대로 <xref:System.GCCollectionMode.Optimized?displayProperty=nameWithType> 열거형 값을 <xref:System.GC.Collect%2A> 메서드에 제공하여 수집의 생산성이 높은 경우에만 수집할 수 있습니다.  
  
## <a name="gc-collection-mode"></a>GC 컬렉션 모드  
 다음과 같이 <xref:System.GCCollectionMode> 값을 포함하는 <xref:System.GC.Collect%2A?displayProperty=nameWithType> 메서드 오버로드 중 하나를 사용하여 강제된 컬렉션에 대한 동작을 지정할 수 있습니다.  
  
|`GCCollectionMode` 값|설명|  
|------------------------------|-----------------|  
|<xref:System.GCCollectionMode.Default>|실행 중인 버전의 .NET에 대한 기본 가비지 수집 설정을 사용합니다.|  
|<xref:System.GCCollectionMode.Forced>|가비지 수집이 즉시 실행되도록 강제합니다. 이는 <xref:System.GC.Collect?displayProperty=nameWithType> 오버로드를 호출하는 것과 같습니다. 모든 세대의 전체 차단 컬렉션에서 발생합니다.<br /><br /> 또한 즉각적인 전체 차단 가비지 수집을 적용하기 전에 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType> 속성을 <xref:System.Runtime.GCLargeObjectHeapCompactionMode.CompactOnce?displayProperty=nameWithType>로 설정하여 대형 개체 힙을 압축할 수 있습니다.|  
|<xref:System.GCCollectionMode.Optimized>|가비지 수집기는 현재 시간이 개체를 회수하기 위한 최적 시간인지 확인할 수 있습니다.<br /><br /> 가비지 수집기는 컬렉션이 정당화될 만큼 생산적이지 않다는 것을 결정할 수 있습니다. 이 경우에 개체를 회수하지 않고 반환합니다.|  
  
## <a name="background-or-blocking-collections"></a>배경 또는 차단 컬렉션  
 <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29?displayProperty=nameWithType> 메서드 오버로드를 호출하여 유도한 컬렉션이 차단인지 여부를 지정할 수 있습니다. 수행된 컬렉션의 유형은 메서드의 `mode` 및 `blocking` 매개 변수의 조합에 따라 달라집니다. `mode`는 <xref:System.GCCollectionMode> 열거형의 멤버이며, `blocking`은 <xref:System.Boolean> 값입니다. 다음 표에서는 `mode` 및 `blocking` 인수의 상호 작용을 간략히 설명합니다.  
  
|`mode`|`blocking` = `true`|`blocking` = `false`|  
|------------|--------------------------|---------------------------|  
|<xref:System.GCCollectionMode.Forced> 또는 <xref:System.GCCollectionMode.Default>|차단 컬렉션은 가능한 한 빨리 수행됩니다. 백그라운드 컬렉션이 진행 중이고 세대가 0 또는 1인 경우 <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> 메서드는 차단 컬렉션을 즉시 트리거하고 컬렉션이 완료될 때 반환합니다. 백그라운드 컬렉션이 진행 중이고 `generation` 매개 변수가 2인 경우 메서드는 백그라운드 컬렉션이 완료될 때까지 대기하고 세대 2 컬렉션을 트리거한 후 반환합니다.|컬렉션은 가능한 한 빨리 수행됩니다. <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> 메서드는 백그라운드 컬렉션을 요청하지만 이 작업이 항상 수행되지는 않으며 상황에 따라 차단 컬렉션이 계속 수행될 수도 있습니다. 백그라운드 컬렉션이 이미 진행 중인 경우 메서드가 즉시 반환됩니다.|  
|<xref:System.GCCollectionMode.Optimized>|차단 컬렉션은 가비지 수집기의 상태와 `generation` 매개 변수에 따라 수행될 수 있습니다. 가비지 수집기는 최적의 성능을 제공하려고 합니다.|가비지 수집기의 상태에 따라 컬렉션이 수행될 수 있습니다. <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> 메서드는 백그라운드 컬렉션을 요청하지만 이 작업이 항상 수행되지는 않으며 상황에 따라 차단 컬렉션이 계속 수행될 수도 있습니다. 가비지 수집기는 최적의 성능을 제공하려고 합니다. 백그라운드 컬렉션이 이미 진행 중인 경우 메서드가 즉시 반환됩니다.|  
  
## <a name="see-also"></a>참고 항목

- [대기 시간 모드](../../../docs/standard/garbage-collection/latency.md)
- [가비지 수집](../../../docs/standard/garbage-collection/index.md)
