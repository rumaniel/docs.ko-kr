---
title: 지속성 최선의 구현 방법
ms.date: 03/30/2017
ms.assetid: 6974c5a4-1af8-4732-ab53-7d694608a3a0
ms.openlocfilehash: 399d2f5dbb5f3114a58cc7fdaede249b253089c3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592115"
---
# <a name="persistence-best-practices"></a>지속성 최선의 구현 방법
이 문서에서는 워크플로 지속성과 관련된 워크플로 디자인 및 구성에 대한 최상의 방법을 설명합니다.  
  
## <a name="design-and-implementation-of-durable-workflows"></a>지속형 워크플로의 디자인 및 구현  
 일반적으로 워크플로는 이벤트를 기다리고 있기 때문에 유휴 상태인 시간과 인터리브된 짧은 기간 동안 작업을 수행합니다. 이러한 이벤트는 메시지, 만료 타이머 등일 수 있습니다. 워크플로 인스턴스가 유휴 상태가 될 때 워크플로 인스턴스를 언로드할 수 있으려면 서비스 호스트가 워크플로 인스턴스를 유지해야 합니다. 이는 워크플로 인스턴스가 비지속성 영역에 없는 경우(예를 들어 트랜잭션이 완료되기를 기다리거나 비동기 콜백을 기다리는 경우)에만 가능합니다. 유휴 워크플로 인스턴스가 언로드될 수 있도록 하려면 워크플로 작성자가 수명이 짧은 작업에만 트랜잭션 범위와 비동기 활동을 사용해야 합니다. 특히 작성자는 이러한 비지속성 영역의 지연 활동을 가능한 한 짧게 유지해야 합니다.  
  
 워크플로에서 사용되는 모든 데이터 형식이 serialize 가능한 경우에만 워크플로가 유지될 수 있습니다. 또한 지속형 워크플로에서 사용되는 사용자 지정 형식은 <xref:System.Runtime.Serialization.NetDataContractSerializer>를 사용하여 serialize 가능해야 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>에 의해 유지될 수 있습니다.  
  
 워크플로 인스턴스가 유지되지 않은 경우 호스트나 컴퓨터에서 오류가 발생하면 워크플로 인스턴스를 복구할 수 없습니다. 일반적으로 워크플로의 수명 주기 초반에 워크플로 인스턴스를 유지하는 것이 좋습니다.  
  
 워크플로가 오랫동안 작업을 수행하는 경우 작업 중인 기간 동안 워크플로 인스턴스를 주기적으로 유지하는 것이 좋습니다. 이렇게 하려면 워크플로 인스턴스가 계속 작업을 수행하도록 하는 일련의 활동 전반에서 <xref:System.Activities.Statements.Persist> 활동을 추가하면 됩니다. 이에 따라 애플리케이션 도메인 재활용, 호스트 오류 또는 컴퓨터 오류가 발생해도 시스템이 작업 중인 기간의 시작으로 롤백되지 않습니다. <xref:System.Activities.Statements.Persist> 활동을 워크플로에 추가하면 성능이 저하될 수 있으므로 주의하세요.  
  
 Windows Server AppFabric은 지속성의 구성과 사용을 크게 단순화합니다. 자세한 내용은 참조 하세요. [Windows Server App Fabric 지 속성](https://go.microsoft.com/fwlink/?LinkID=201200&clcid=0x409)  
  
## <a name="configuration-of-scalability-parameters"></a>확장성 매개 변수의 구성  
 확장성 및 성능 요구 사항에 따라 다음 매개 변수의 설정이 결정됩니다.  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A>  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>  
  
- <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior.InstanceLockedExceptionAction%2A>  
  
 이러한 매개 변수는 현재 시나리오에 따라 다음과 같이 설정되어야 합니다.  
  
### <a name="scenario-a-small-number-of-workflow-instances-that-require-optimal-response-time"></a>시나리오: 적은 수의 응답 시간을 최적화 해야 하는 워크플로 인스턴스  
 이 시나리오에서는 모든 워크플로 인스턴스가 유휴 상태가 될 때 로드된 상태로 유지되어야 합니다. <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>를 큰 값으로 설정합니다. 이 설정을 사용하면 워크플로 인스턴스가 컴퓨터 간에 이동하지 않습니다. 다음 중 하나 이상에 해당하는 경우에만 이 설정을 사용합니다.  
  
- 워크플로 인스턴스가 수명 전반에서 단일 메시지를 받습니다.  
  
- 모든 워크플로 인스턴스가 단일 컴퓨터에서 실행됩니다.  
  
- 워크플로 인스턴스가 받는 모든 메시지를 동일한 컴퓨터에서 받습니다.  
  
 <xref:System.Activities.Statements.Persist> 활동을 사용하거나 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A>를 0으로 설정하여 서비스 호스트나 컴퓨터에서 오류가 발생한 후 워크플로 인스턴스를 복구할 수 있도록 합니다.  
  
### <a name="scenario-workflow-instances-are-idle-for-long-periods-of-time"></a>시나리오: 워크플로 인스턴스는 오랜 시간 동안 유휴 상태  
 이 시나리오에서는 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>를 0으로 설정하여 리소스를 가능한 한 빨리 해제합니다.  
  
### <a name="scenario-workflow-instances-receive-multiple-messages-in-a-short-period-of-time"></a>시나리오: 워크플로 인스턴스가 짧은 기간에 여러 메시지를 수신합니다.  
 이 시나리오에서는 해당 메시지를 동일한 컴퓨터에서 받는 경우 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>를 60초로 설정합니다. 이렇게 하면 워크플로 인스턴스가 빠르게 연속적으로 언로드되고 로드되지 않으며 인스턴스가 메모리에 너무 오래 유지되지도 않습니다.  
  
 해당 메시지를 여러 컴퓨터에서 받을 수 있는 경우에는 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>를 0으로 설정하고 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior.InstanceLockedExceptionAction%2A>을 BasicRetry 또는 AggressiveRetry로 설정합니다. 이렇게 하면 워크플로 인스턴스가 다른 컴퓨터에서 로드될 수 있습니다.  
  
### <a name="scenario-workflow-uses-delay-activities-with-short-durations"></a>시나리오: 워크플로에서 짧은 기간을 사용 하 여 지연 작업 사용  
 이 시나리오에서는 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>가 만료된 <xref:System.Activities.Statements.Delay> 활동 때문에 로드되어야 하는 인스턴스를 지속성 데이터베이스에서 주기적으로 폴링합니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>가 다음 폴링 간격에서 만료될 타이머를 찾는 경우 SQL 워크플로 인스턴스 저장소에서는 폴링 간격을 단축합니다. 그러면 다음 폴링이 타이머가 만료된 직후에 발생합니다. 이러한 방식으로 SQL 워크플로 인스턴스 저장소는 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>로 설정된 폴링 간격보다 길게 실행되는 타이머의 높은 정확도를 달성합니다. 지연을 단축하여 적시에 처리할 수 있으려면 워크플로 인스턴스가 최소한 한 번의 폴링 간격 동안 메모리에 유지되어야 합니다.  
  
 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A>를 0으로 설정하여 만료 시간을 지속성 데이터베이스에 기록합니다.  
  
 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>를 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>보다 길거나 같은 값으로 설정하여 최소한 한 번의 폴링 간격 동안 인스턴스를 메모리에 유지합니다.  
  
 지속성 데이터베이스에서 부하가 늘어날 수 있기 때문에 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>를 줄이지 않는 것이 좋습니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>를 사용하는 각 서비스 호스트는 검색 기간마다 한 번씩 데이터베이스를 폴링합니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>를 너무 작은 시간 간격으로 설정하면 서비스 호스트 수가 많은 경우 시스템 성능이 저하될 수 있습니다.  
  
## <a name="configuring-the-sql-workflow-instance-store"></a>SQL 워크플로 인스턴스 저장소 구성  
 SQL 워크플로 인스턴스 저장소에는 다음과 같은 구성 매개 변수가 있습니다.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceEncodingOption%2A>  
 이 매개 변수는 워크플로 인스턴스 상태를 압축하도록 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>에 지시합니다. 압축을 하면 지속성 데이터베이스에 저장된 데이터의 양이 줄어들고 지속성 데이터베이스가 전용 데이터베이스 서버에 있는 경우 네트워크 트래픽이 줄어듭니다. 압축을 사용하는 경우 인스턴스 상태를 압축하고 추출할 계산 리소스가 필요합니다. 대부분의 경우 압축을 통해 성능이 향상됩니다.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceCompletionAction%2A>  
 이 매개 변수는 완료된 인스턴스를 유지하거나 삭제하도록 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>에 지시합니다. 완료된 인스턴스를 유지하면 지속성 데이터베이스 스토리지 요구 사항이 증가하고 테이블이 커지며 테이블 조회 시간도 늘어납니다. 완료된 인스턴스가 디버깅이나 감사에 필요하지 않으면 완료된 인스턴스를 삭제하도록 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>에 지시하는 것이 좋습니다. 삭제된 인스턴스는 사용자가 해당 인스턴스를 결국 제거하는 프로세스를 설정하는 경우에만 유지되어야 합니다. 완료된 워크플로 인스턴스가 인스턴스 저장소에 있는 한 상관 관계 키를 다시 사용할 수 없습니다.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>  
 이 매개 변수는 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>가 <xref:System.Activities.Statements.Delay> 활동이 만료될 때 로드되어야 하는 인스턴스를 지속성 데이터베이스에서 폴링하는 최대 간격을 정의합니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>가 다음 폴링 간격에서 만료될 타이머를 찾는 경우 타이머가 만료된 직후에 다음 폴링이 발생하도록 폴링 간격을 단축합니다. 이러한 방식으로 SQL 워크플로 인스턴스 저장소는 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>보다 길게 실행되는 타이머의 높은 정확도를 달성합니다.  
  
 지속성 데이터베이스에서 부하가 늘어날 수 있기 때문에 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>를 줄이지 않는 것이 좋습니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>를 사용하는 각 서비스 호스트는 검색 기간마다 한 번씩 데이터베이스를 폴링합니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>를 너무 작은 간격으로 설정하면 서비스 호스트 수가 많은 경우 시스템 성능이 저하될 수 있습니다.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.HostLockRenewalPeriod%2A>  
 이 매개 변수는 호스트가 지속성 데이터베이스에서 잠금을 갱신하는 간격을 정의합니다. 이 간격을 단축하면 호스트나 컴퓨터에서 오류가 발생하는 경우 워크플로 인스턴스를 더욱 빠르게 복구할 수 있습니다. 반면에 잠금 갱신 기간이 짧으면 지속성 데이터베이스에서 부하가 늘어납니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>를 사용하는 각 서비스 호스트는 갱신 기간마다 한 번씩 데이터베이스에서 잠금을 업데이트합니다. 컴퓨터에서 많은 서비스 호스트가 실행되는 경우 잠금 갱신으로 인한 부하 때문에 시스템 성능이 저하되지 않도록 해야 합니다. 시스템 성능이 저하되는 경우에는 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.HostLockRenewalPeriod%2A>를 늘리는 것이 좋습니다.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A>  
 사용할 경우 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>가 다음 30초 동안 잠긴 인스턴스를 로드하려고 다시 시도합니다. 워크플로가 짧은 기간 동안 여러 메시지를 받고 여러 컴퓨터에서 이러한 메시지를 받는 경우에는 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A>을 BasicRetry 또는 AggressiveRetry로 설정합니다.  
  
 로드 재시도가 시도되지 않는 한 로드 재시도 메커니즘에서 성능 오버헤드를 유발하지 않기 때문에 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A>을 항상 사용하도록 설정해야 합니다.
