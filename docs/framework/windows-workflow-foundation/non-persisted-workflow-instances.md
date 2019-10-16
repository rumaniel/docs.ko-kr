---
title: 비지속형 워크플로 인스턴스
ms.date: 03/30/2017
ms.assetid: 5e01af77-6b14-4964-91a5-7dfd143449c0
ms.openlocfilehash: 315d791585ace6ce4adf281abbba0a4c8c72d75a
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663038"
---
# <a name="non-persisted-workflow-instances"></a>비지속형 워크플로 인스턴스

<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>에 상태를 유지하는 워크플로의 새 인스턴스가 만들어지면 서비스 호스트에서는 인스턴스 저장소에 해당 서비스에 대한 항목을 만듭니다. 이후 워크플로 인스턴스가 처음으로 유지될 때 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>는 현재 인스턴스 상태를 저장합니다. 워크플로가 Windows Process Activation Service에서 호스트되는 경우에는 인스턴스가 처음으로 유지될 때 서비스 배포 데이터도 인스턴스 저장소에 기록됩니다.

워크플로 인스턴스가 유지 되지 않은 것으로에 **비지속형** 상태. 이 상태에 있는 동안에는 애플리케이션 도메인 재활용, 호스트 오류 또는 컴퓨터 오류 후 워크플로 인스턴스를 복구할 수 없습니다.

## <a name="the-non-persisted-state"></a>비지속형 상태

유지되지 않은 영속 워크플로 인스턴스는 다음과 같은 경우에 비지속형 상태로 남아 있습니다.

- 워크플로 인스턴스가 처음으로 유지되기 전에 서비스 호스트에서 충돌이 발생한 경우. 워크플로 인스턴스가 인스턴스 저장소에 남아 있고 복구되지 않습니다. 상관 관계 메시지가 도착하면 워크플로 인스턴스가 다시 활성화됩니다.

- 워크플로 인스턴스가 처음으로 유지되기 전에 워크플로 인스턴스에서 예외가 발생한 경우. 반환되는 <xref:System.Activities.UnhandledExceptionAction>에 따라 다음과 같은 시나리오가 발생합니다.

  - <xref:System.Activities.UnhandledExceptionAction> 로 설정 된 <xref:System.Activities.UnhandledExceptionAction.Abort>: 예외가 발생 하는 경우 서비스 배포 정보가 인스턴스 저장소에 기록 됩니다 하 고 워크플로 인스턴스가 메모리에서 언로드 되었습니다. 워크플로 인스턴스는 비지속형 상태로 남아 있으며 다시 로드될 수 없습니다.

  - <xref:System.Activities.UnhandledExceptionAction> 로 설정 되어 <xref:System.Activities.UnhandledExceptionAction.Cancel> 또는 <xref:System.Activities.UnhandledExceptionAction.Terminate>: 예외가 발생 하는, 서비스 배포 정보가 인스턴스 저장소에 기록 되 고 활동 인스턴스 상태 설정 된 경우 <xref:System.Activities.ActivityInstanceState.Closed>합니다.

언로드된 비지속형 워크플로 인스턴스가 발생하는 위험을 최소화하려면 수명 주기의 초기에 워크플로를 유지하는 것이 좋습니다.

## <a name="detection-and-removal-of-non-persisted-instances"></a>비지속형 인스턴스의 검색 및 제거

<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>는 비지속형 워크플로 인스턴스를 인스턴스 저장소에서 제거하지 않으며 비지속형 워크플로 인스턴스가 연결되어 있는 만료된 잠금 소유자도 제거하지 않습니다.

관리자가 주기적으로 인스턴스 저장소에서 비지속형 인스턴스를 확인하는 것이 좋습니다. 관리자는 이 워크플로가 상관 관계 메시지를 받지 않을 것임을 아는 한 해당 인스턴스를 인스턴스 저장소에서 제거할 수 있습니다. 예를 들어 인스턴스가 데이터베이스에 몇 달 동안 있었고 일반적으로 워크플로의 수명이 며칠 정도임을 알고 있는 경우 해당 인스턴스는 손상되어 초기화된 인스턴스라고 간주해도 무방합니다.

SQL 워크플로 인스턴스 저장소에서 비지속형 인스턴스를 찾으려면 다음 SQL 쿼리를 사용할 수 있습니다.

- 이 쿼리는 유지되지 않은 모든 인스턴스를 찾고 인스턴스의 ID와 만든 시간(UTC 시간으로 저장됨)을 반환합니다.

  ```sql
  select InstanceId, CreationTime
      from [System.Activities.DurableInstancing].[Instances]
      where IsInitialized = 0
  ```

- 이 쿼리는 유지되지 않고 로드되지 않은 모든 인스턴스를 찾고 인스턴스의 ID와 만든 시간(UTC 시간으로 저장됨)을 반환합니다.

  ```sql
  select InstanceId, CreationTime
      from [System.Activities.DurableInstancing].[Instances]
      where IsInitialized = 0
          and CurrentMachine is NULL
  ```

- 이 쿼리는 유지되지 않은 모든 일시 중단된 인스턴스를 찾고 인스턴스의 ID, 만든 시간(UTC 시간으로 저장됨), 일시 중단 이유 및 예외 이름을 반환합니다.

  ```sql
  select InstanceId, CreationTime, SuspensionReason, SuspensionExceptionName
      from [System.Activities.DurableInstancing].[Instances]
      where IsInitialized = 0
          and IsSuspended = 1
  ```

비지속형 인스턴스를 삭제하는 경우 주의해야 합니다. 일반적으로 일시 중단되었거나 로드되지 않은 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에서 만든 비지속형 인스턴스는 제거해도 안전합니다. 이러한 특정 인스턴스는 다음 SQL 명령을 사용하고 올바른 인스턴스 ID로 대체하여 `[System.Activities.DurableInstancing].[Instances]` 뷰에서 삭제함으로써 저장소에서 삭제할 수 있습니다.

```sql
delete [System.Activities.DurableInstancing].[Instances]
    where InstanceId=’078a9bc4-ada5-4f9e-8cce-b0eb0009995f’
```

> [!WARNING]
> 방금 만들어져서 아직 유지되지 않은 인스턴스가 포함되므로 비지속형 인스턴스를 모두 제거하지 않는 것이 좋습니다.
