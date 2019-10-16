---
title: 스레드 스케줄링
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], scheduling
- scheduling threads
ms.assetid: 67e4a0eb-3095-4ea7-b20f-908faa476277
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 502e118a67e157ce7756efdece866564fddc6ab7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54611491"
---
# <a name="scheduling-threads"></a>스레드 스케줄링

모든 스레드에는 할당된 스레드 우선 순위가 있습니다. 공용 언어 런타임 내에서 생성된 스레드에는 초기에 <xref:System.Threading.ThreadPriority.Normal?displayProperty=nameWithType>의 우선 순위가 할당됩니다. 런타임 외부에서 생성된 스레드는 관리되는 환경에 들어가기 전의 우선 순위를 유지합니다. <xref:System.Threading.Thread.Priority?displayProperty=nameWithType> 속성이 있는 스레드의 우선 순위를 가져오거나 설정할 수 있습니다.  
  
 스레드는 우선 순위에 따라 실행되도록 예약됩니다. 스레드가 런타임 내에서 실행 중인 경우에도 모든 스레드에는 운영 체제에 의해 프로세서 시간 조각이 할당됩니다. 스레드가 실행되는 순서를 확인하는 데 사용되는 예약 알고리즘의 세부 정보는 각 운영 체제에 따라 다릅니다. 일부 운영 체제에서는 실행할 수 있는 스레드 중 우선 순위가 가장 높은 스레드가 항상 첫 번째로 실행되도록 예약됩니다. 우선 순위가 동일한 여러 스레드가 모두 사용 가능한 경우 스케줄러는 해당 우선 순위에 있는 스레드를 순환하여 각 스레드에 실행할 고정 시간 조각을 제공합니다. 우선 순위가 더 높은 스레드를 실행할 수 있는 경우에는 우선 순위가 더 낮은 스레드는 실행되지 않습니다. 지정된 우선 순위에 실행 가능한 스레드가 더 이상 없는 경우 스케줄러는 다음으로 낮은 우선 순위로 이동하고 해당 우선 순위의 스레드를 실행하도록 예약합니다. 우선 순위가 더 높은 스레드가 실행 가능해지면 우선 순위가 더 낮은 스레드가 대체되고 우선 순위가 더 높은 스레드가 다시 한번 실행될 수 있습니다. 무엇보다 이 운영 체제에서는 애플리케이션의 사용자 인터페이스가 포그라운드와 백그라운드 사이에서 이동될 때 스레드 우선 순위를 동적으로 조정할 수 있습니다. 다른 운영 체제에서는 다른 예약 알고리즘을 사용하도록 선택할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [스레드 및 스레딩 사용](../../../docs/standard/threading/using-threads-and-threading.md)
- [Windows에서 관리되는 스레딩 및 관리되지 않는 스레딩](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)
