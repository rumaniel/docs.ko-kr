---
title: 가비지 컬렉션 알림
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- garbage collection, notifications
ms.assetid: e12d8e74-31e3-4035-a87d-f3e66f0a9b89
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: edf519621c2113843b89d96948243e9c095d2a57
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988866"
---
# <a name="garbage-collection-notifications"></a>가비지 컬렉션 알림
공용 언어 런타임에서 전체 가비지 컬렉션(즉, 2세대 컬렉션)을 실행하면 성능이 저하될 수 있는 경우가 있습니다. 이는 대량의 요청을 처리하는 서버에서 특히 문제가 될 수 있습니다. 이 경우 장기적인 가비지 수집으로 인해 요청 시간이 초과될 수 있습니다. 중요 기간에 전체 수집이 발생하지 않도록 하기 위해 전체 가비지 수집에 근접하고 있다는 알림을 받을 수 있습니다. 그러면 워크로드를 다른 서버 인스턴스로 리디렉션하는 조치를 취할 수 있습니다. 또한 현재 서버 인스턴스가 요청을 처리하지 않아도 되는 경우 직접 수집을 유도할 수도 있습니다.  
  
 <xref:System.GC.RegisterForFullGCNotification%2A> 메서드는 런타임에서 전체 가비지 수집에 근접하고 있음을 감지할 때 발생되는 알림에 등록합니다. 이 알림에는 두 부분이 있습니다. 즉, 알림은 전체 가비지 수집에 근접하고 있을 때와 전체 가비지 수집이 완료되었을 때 발생할 수 있습니다.  
  
> [!WARNING]
> 차단 가비지 컬렉션만 알림을 발생시킵니다. [\<gcConcurrent>](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) 구성 요소를 사용하면 백그라운드 가비지 수집은 알림을 발생시키지 않습니다.  
  
 알림이 발생한 시기를 확인하려면 <xref:System.GC.WaitForFullGCApproach%2A> 및 <xref:System.GC.WaitForFullGCComplete%2A> 메서드를 사용합니다. 일반적으로 `while` 루프에 이러한 메서드를 사용하면 알림 상태를 표시하는 <xref:System.GCNotificationStatus> 열거형을 계속해서 가져올 수 있습니다. 해당 값이 <xref:System.GCNotificationStatus.Succeeded>인 경우 다음을 수행할 수 있습니다.  
  
- <xref:System.GC.WaitForFullGCApproach%2A> 메서드를 사용하여 받은 알림에 대한 대응으로, 워크로드를 리디렉션하고 직접 수집을 유도할 수도 있습니다.  
  
- <xref:System.GC.WaitForFullGCComplete%2A> 메서드를 사용하여 받은 알림에 대한 대응으로, 현재 서버 인스턴스에서 요청을 다시 처리할 수 있게 설정할 수 있습니다. 또한 정보도 수집할 수 있습니다. 예를 들어 <xref:System.GC.CollectionCount%2A> 메서드를 사용하여 컬렉션 수를 기록할 수 있습니다.  
  
 <xref:System.GC.WaitForFullGCApproach%2A> 및 <xref:System.GC.WaitForFullGCComplete%2A> 메서드는 함께 작동하도록 설계되었습니다. 두 메서드를 함께 사용하지 않고 하나만 사용하면 불확실한 결과를 얻을 수 있습니다.  
  
## <a name="full-garbage-collection"></a>전체 가비지 수집  
 다음 시나리오 중 하나에 해당하는 경우 런타임은 전체 가비지 수집을 발생시킵니다.  
  
- 그다음 세대 2 컬렉션을 일으키기에 충분한 메모리가 세대 2로 승격된 경우.  
  
- 그다음 세대 2 컬렉션을 일으키기에 충분한 메모리가 대형 개체 힙으로 승격된 경우.  
  
- 세대 1의 컬렉션이 다른 요인으로 인해 세대 2의 컬렉션으로 에스컬레이션된 경우  
  
 <xref:System.GC.RegisterForFullGCNotification%2A> 메서드에서 지정한 임계값은 처음 두 시나리오에 적용됩니다. 그러나 첫 번째 시나리오에서는 다음과 같은 두 가지 이유로 지정된 임계값에 비례한 시간에 알림을 항상 받지는 못합니다.  
  
- 런타임이 성능상의 이유로 각각의 소형 개체 할당을 확인하지 않습니다.  
  
- 세대 1 컬렉션만 메모리 수준이 세대 2로 올라갑니다.  
  
 또한 세 번째 시나리오는 알림을 받을 수 있는 시기를 불확실하게 하는 원인이 됩니다. 따라서 보장할 수는 없지만, 이 시간 동안 요청을 리디렉션하거나 더 잘 수용할 수 있을 때 직접 수집을 유도함으로써 부적절한 시기의 전체 가비지 수집으로 인한 영향을 완화하는 것이 유용한 방법임은 명백합니다.  
  
## <a name="notification-threshold-parameters"></a>알림 임계값 매개 변수  
 <xref:System.GC.RegisterForFullGCNotification%2A> 메서드에는 세대 2 개체 및 대형 개체 힙의 임계값을 지정하는 두 개의 매개 변수가 있습니다. 이러한 값이 충족되면 가비지 수집 알림이 발생되어야 합니다. 다음 표에서는 이러한 매개 변수에 대해 설명합니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|`maxGenerationThreshold`|세대 2에서 수준이 상승된 개체에 따라 알림을 발생시킬 시점을 지정하는 1에서 99 사이의 숫자입니다.|  
|`largeObjectHeapThreshold`|대형 개체 힙에 할당되는 개체에 따라 알림을 발생시킬 시점을 지정하는 1에서 99 사이의 숫자입니다.|  
  
 너무 높은 값을 지정하는 경우 알림을 받을 확률은 높아지지만 런타임에서 수집을 일으킬 때까지 너무 오래 대기할 수 있습니다. 직접 수집을 유도하는 경우 런타임에서 수집을 일으킬 때 회수하는 것보다 더 많은 개체를 회수할 수 있습니다.  
  
 너무 낮은 값을 지정하는 경우 알림을 받기에 충분한 시간이 경과하기도 전에 런타임이 수집을 일으킬 수 있습니다.  
  
## <a name="example"></a>예  
  
### <a name="description"></a>설명  
 다음 예제에서 서버 그룹이 들어오는 웹 요청을 처리합니다. 요청 처리의 워크로드를 시뮬레이트하기 위해 바이트 배열을 <xref:System.Collections.Generic.List%601> 컬렉션에 추가합니다. 각 서버는 가비지 수집 알림에 등록한 후 `WaitForFullGCProc` 사용자 메서드의 스레드를 시작하여 <xref:System.GC.WaitForFullGCApproach%2A> 및 <xref:System.GC.WaitForFullGCComplete%2A> 메서드에서 반환하는 <xref:System.GCNotificationStatus> 열거형을 지속적으로 모니터링합니다.  
  
 <xref:System.GC.WaitForFullGCApproach%2A> 및 <xref:System.GC.WaitForFullGCComplete%2A> 메서드는 알림이 발생할 때 다음과 같은 각각의 이벤트 처리 사용자 메서드를 호출합니다.  
  
- `OnFullGCApproachNotify`  
  
     이 메서드는 `RedirectRequests` 사용자 메서드를 호출하여, 서버로의 요청 전송을 일시 중단하도록 요청 큐 서버에 지시합니다. 이는 더 이상 개체가 할당되지 않도록 클래스 수준 변수 `bAllocate`를 `false`로 설정하여 시뮬레이트됩니다.  
  
     다음으로, 보류 중인 서버 요청에 대한 처리를 완료하기 위해 `FinishExistingRequests` 사용자 메서드를 호출합니다. 이는 <xref:System.Collections.Generic.List%601> 컬렉션을 지움으로써 시뮬레이트됩니다.  
  
     마지막으로 워크로드가 가벼우므로 가비지 수집을 유도합니다.  
  
- `OnFullGCCompleteNotify`  
  
     서버가 전체 가비지 수집에 더 이상 취약하지 않으므로 이 메서드는 사용자 메서드 `AcceptRequests`를 호출하여 요청 수락을 다시 시작합니다. 이 작업은 개체를 <xref:System.Collections.Generic.List%601> 컬렉션에 추가하는 것을 다시 시작할 수 있도록 `bAllocate` 변수를 `true`로 설정하여 시뮬레이트됩니다.  
  
 다음 코드에는 예제의 `Main` 메서드가 포함되어 있습니다.  
  
 [!code-cpp[GCNotification#2](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#2)]
 [!code-csharp[GCNotification#2](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#2)]
 [!code-vb[GCNotification#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#2)]  
  
 다음 코드에는 가비지 수집 알림을 확인하기 위한 연속 while 루프가 들어 있는 `WaitForFullGCProc` 사용자 메서드가 포함되어 있습니다.  
  
 [!code-cpp[GCNotification#8](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#8)]
 [!code-csharp[GCNotification#8](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#8)]
 [!code-vb[GCNotification#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#8)]  
  
 다음 코드에는 다음에서 호출되는 `OnFullGCApproachNotify` 메서드가 포함되어 있습니다.  
  
 `WaitForFullGCProc` 메서드를 호출하여 생성됩니다.  
  
 [!code-cpp[GCNotification#5](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#5)]
 [!code-csharp[GCNotification#5](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#5)]
 [!code-vb[GCNotification#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#5)]  
  
 다음 코드에는 다음에서 호출되는 `OnFullGCApproachComplete` 메서드가 포함되어 있습니다.  
  
 `WaitForFullGCProc` 메서드를 호출하여 생성됩니다.  
  
 [!code-cpp[GCNotification#6](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#6)]
 [!code-csharp[GCNotification#6](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#6)]
 [!code-vb[GCNotification#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#6)]  
  
 다음 코드에는 `OnFullGCApproachNotify` 및 `OnFullGCCompleteNotify` 메서드에서 호출되는 사용자 메서드가 포함되어 있습니다. 사용자 메서드는 요청을 리디렉션하고, 기존 요청을 완료한 다음, 전체 가비지 수집이 발생한 이후에 요청을 다시 시작합니다.  
  
 [!code-cpp[GCNotification#9](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#9)]
 [!code-csharp[GCNotification#9](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#9)]
 [!code-vb[GCNotification#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#9)]  
  
 전체 코드 샘플은 다음과 같습니다.  
  
 [!code-cpp[GCNotification#1](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#1)]
 [!code-csharp[GCNotification#1](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#1)]
 [!code-vb[GCNotification#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- [가비지 수집](../../../docs/standard/garbage-collection/index.md)
