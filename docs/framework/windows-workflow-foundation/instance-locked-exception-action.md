---
title: 인스턴스 잠금 예외 동작
ms.date: 03/30/2017
ms.assetid: 164a5419-315c-4987-ad72-54cbdb88d402
ms.openlocfilehash: d8fd2d1299a8563ae41b098c1cfb7a0ba30bb8f8
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662990"
---
# <a name="instance-locked-exception-action"></a>인스턴스 잠금 예외 동작
SQL 워크플로 인스턴스 저장소의 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A> 속성을 사용하면 SQL 지속성 공급자가 <xref:System.Runtime.DurableInstancing.InstanceLockedException>을 수신할 때 수행해야 하는 동작을 지정할 수 있습니다. 지속성 공급자가 현재 다른 서비스 호스트에 의해 잠긴 워크플로 서비스 인스턴스를 잠그려고 하면 이 예외가 발생합니다. 이 속성의 값은 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>, <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry> 및 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry>입니다. 기본값은 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>입니다. 다음 목록에서는 세 가지 옵션에 대해 설명합니다.  
  
- <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>. 서비스 호스트는 워크플로 서비스 인스턴스가 전달 잠금을 시도 하지 않습니다는 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 호출자에 게 합니다.  60 초를 초과 하는 동안 메모리에 유지 되 워크플로 사용 하 여 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry> 은 재시도 합니다. 기본값은 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>입니다.  
  
- <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry>. 서비스 호스트가 다시 시도 사이에 선형 간격을 사용하여 워크플로 서비스 인스턴스의 잠금을 다시 시도하고 시퀀스 끝에 호출자에게 <xref:System.Runtime.DurableInstancing.InstanceLockedException>을 전달합니다. 워크플로가 메모리에 약 5-60초 사이에 유지되어 있고 워크플로를 업로드하기 전에 모든 메시지를 처리하기 위해 같은 호스트에서 같은 인스턴스로 전송 중인 메시지가 모든 메시지를 더 많이 처리할 수 있는 지점에 일괄적으로 도착하면 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry>를 사용하여 리소스를 낭비하지 않고 지연 시간을 가장 많이 줄일 수 있습니다.  
  
- <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry>. 서비스 호스트가 다시 시도 사이에 지수 형식의 백오프 간격을 사용하여 워크플로 서비스 인스턴스의 잠금을 다시 시도하고 시퀀스 끝에 호출자에게 예외를 전달합니다. 워크플로가 매우 짧은 시간(5초 이내) 동안 메모리에 유지되거나 웹 팜이 크고 다른 메시지가 같은 호스트에 전달될 수 있는 기회가 그리 크지 않을 경우 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry>를 사용하여 지연 시간을 가장 많이 줄일 수 있습니다.  
  
 인스턴스 잠금 예외 동작 기능은 다음 시나리오를 지원합니다. 모든 시나리오에서 SqlWorkflowInstanceStore의 instanceLockedExceptionAction 속성이 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry> 또는 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry>로 설정되어 있는 경우 호스트는 인스턴스에 대한 잠금을 주기적으로 투명하게 다시 시도합니다.  
  
1. **정상 종료 및 중첩 재활용 응용 프로그램 도메인을 사용 하도록 설정 합니다.** 가정 된 **AppDomain** 서비스 호스트를 사용 하 여 실행 중인 워크플로 서비스 인스턴스를 재활용 하 고 새 **AppDomain** 으로 이전 하는 동안 동시에 새 요청을 처리  **AppDomain** 정상적으로 중단 합니다. 워크플로 서비스 인스턴스가 유휴 상태가 될 때까지 종료를 중지했다가 인스턴스를 유지하고 언로드합니다. 새 호스트에서 모든 시도가 **AppDomain** 인스턴스를 잠그려고 하면는 <xref:System.Runtime.DurableInstancing.InstanceLockedException>합니다.  
  
2. **유형이 같은 서버 팜에서 지속형 워크플로 수평 확장.** 워크플로 인스턴스가 실행 중인 서버 팜 노드가 충돌하고 워크플로 호스트가 실행 중인 인스턴스에 대한 잠금을 제거할 수 없다고 가정합니다. 다른 팜 노드에서 실행 중인 서비스 호스트가 워크플로 인스턴스에 대한 메시지를 수신한 후 해당 인스턴스를 잠그려고 시도하면 <xref:System.Runtime.DurableInstancing.InstanceLockedException>이 발생합니다. 잠금을 갱신하려는 호스트가 더 이상 존재하기 않기 때문에 잠금이 잠시 후 만료됩니다.  
  
     **유형이 같은 서버 팜에서 지속형 워크플로 수평 확장.**  NLB (네트워크 부하 분산 장치) 뒤의 여러 호스트를 사용 하 여 지속형 워크플로 수평으로 확장 하려는, 팜의 한 노드에서 실행 중인 워크플로 호스트는 워크플로 인스턴스를 로드 하 고 메시지를 처리 하며, 고 다음 메시지 인스턴스에 라우팅됩니다 가정해 보겠습니다. NLB에 인스턴스를 이미 실행 중인 호스트에 메시지를 배달 하는 라우팅 알고리즘이 없기 때문에 다른 노드에서 실행 중인 호스트입니다. 메시지가 수신되면 두 번째 호스트에서 워크플로 인스턴스를 로드하려고 시도합니다. 그러면 첫 번째 호스트에서 인스턴스를 잠갔기 때문에 <xref:System.Runtime.DurableInstancing.InstanceLockedException>이 발생합니다. 첫 번째 호스트에서 첫 번째 메시지를 처리한 후 인스턴스를 잠금 해제하면 두 번째 호스트에서 다음에 재시도할 때 인스턴스를 잠가 인스턴스를 로드한 후 두 번째 메시지를 처리할 수 있습니다.
