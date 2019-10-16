---
title: '방법: 비지속성 인스턴스 쿼리'
ms.date: 03/30/2017
ms.assetid: 294019b1-c1a7-4b81-a14f-b47c106cd723
ms.openlocfilehash: 87b29ce6a5858872929cea4408d0d7bcc1b378d1
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425315"
---
# <a name="how-to-query-for-non-persisted-instances"></a>방법: 비지속성 인스턴스 쿼리

서비스의 새 인스턴스가 만들어지고 이 서비스에 SQL 워크플로 인스턴스 저장소 동작이 정의되는 경우, 서비스 호스트에서는 인스턴스 저장소에 해당 서비스 인스턴스에 대한 초기 항목을 만듭니다. 이후에 서비스 인스턴스가 처음으로 저장되면 SQL 워크플로 인스턴스 저장소 동작은 활성화, 복구 및 제어에 필요한 추가 데이터와 함께 현재 인스턴스 상태를 저장합니다.

인스턴스의 초기 항목이 만들어진 후 인스턴스가 저장되지 않은 경우 해당 서비스 인스턴스는 비지속성 상태에 있다고 합니다. 저장된 모든 서비스 인스턴스를 쿼리하고 제어할 수 있지만 비지속성 서비스 인스턴스는 쿼리할 수 없으며 제어할 수도 없습니다. 처리되지 않는 예외로 인해 일시 중단된 비지속성 인스턴스는 쿼리할 수만 있고 제어할 수는 없습니다.

아직 저장되지 않는 영속 서비스 인스턴스는 다음과 같은 경우에 비지속성 상태로 유지됩니다.

- 인스턴스가 처음으로 저장되기 전에 서비스 호스트에서 충돌이 발생한 경우. 인스턴스의 초기 항목은 인스턴스 저장소에 유지됩니다. 인스턴스는 복구할 수 없습니다. 상관 관계 메시지가 도착하면 인스턴스는 다시 활성화됩니다.

- 인스턴스가 처음으로 저장되기 전에 인스턴스에서 예기치 않은 예외가 발생한 경우. 다음 시나리오가 발생합니다.

  - 경우 값을 **UnhandledExceptionAction** 속성이로 설정 된 **중단**서비스 배포 정보가 인스턴스 저장소에 기록 되 고 인스턴스가 메모리에서 언로드됩니다. 인스턴스는 지속성 데이터베이스에서 비지속성 상태로 유지됩니다.

  - 하는 경우의 값을 **UnhandledExceptionAction** 속성이 **AbandonAndSuspend**, 서비스 배포 정보가 지 속성 데이터베이스에 기록 되 고 인스턴스 상태가 로설정된 **일시 중단**합니다. 이 인스턴스는 다시 시작하거나 취소하거나 종료할 수 없습니다. 인스턴스가 아직 저장되지 않아 인스턴스의 데이터베이스 항목이 완료되지 않았으므로 서비스 호스트에서는 해당 인스턴스를 로드할 수 없습니다.

  - 경우의 값을 **UnhandledExceptionAction** 속성이 **취소** 또는 **Terminate**, 서비스 배포 정보가 인스턴스 저장소에 기록 됩니다 및 인스턴스 상태가로 설정 되어 **Completed**합니다.

다음 단원에서는 SQL 지속성 데이터베이스에서 비지속성 인스턴스를 찾고 이러한 인스턴스를 데이터베이스에서 삭제하는 샘플 쿼리를 제공합니다.

## <a name="to-find-all-instances-not-persisted-yet"></a>아직 저장되지 않은 모든 인스턴스를 찾으려면

다음 SQL 쿼리에서는 지속성 데이터베이스에 아직 저장되지 않은 모든 인스턴스의 ID와 만든 시간을 반환합니다.

```sql
select InstanceId, CreationTime from [System.Activities.DurableInstancing].[Instances] where IsInitialized = 0;
```

## <a name="to-find-all-instances-not-persisted-yet-and-also-not-loaded"></a>아직 저장되지 않고 로드되지도 않은 모든 인스턴스를 찾으려면
 다음 SQL 쿼리에서는 아직 저장되지 않고 로드되지도 않은 모든 인스턴스의 ID와 만든 시간을 반환합니다.

```sql
select InstanceId, CreationTime from [System.Activities.DurableInstancing].[Instances] where IsInitialized = 0 and CurrentMachine is NULL;
```

## <a name="to-find-all-suspended-instances-not-persisted-yet"></a>아직 저장되지 않은 일시 중단된 모든 인스턴스를 찾으려면

다음 SQL 쿼리에서는 저장되지 않고 일시 중단된 상태에 있는 모든 인스턴스의 ID, 만든 시간, 일시 중단 이유 및 일시 중단 예외 이름을 반환합니다.

```sql
select InstanceId, CreationTime, SuspensionReason, SuspensionExceptionName from [System.Activities.DurableInstancing].[Instances] where IsInitialized = 0 and IsSuspended = 1;
```

## <a name="to-delete-non-persisted-instances-from-the-persistence-database"></a>지속성 데이터베이스에서 비지속성 인스턴스를 삭제하려면

인스턴스 저장소에서 비지속성 인스턴스를 주기적으로 검사하고, 상관 관계 메시지를 받지 않는 것이 확실한 인스턴스는 인스턴스 저장소에서 제거해야 합니다. 예를 들어 인스턴스가 데이터베이스에 몇 달 동안 있었고 일반적으로 워크플로의 수명이 며칠 정도임을 알고 있는 경우 해당 인스턴스는 손상되어 초기화되지 않는 인스턴스라고 간주해도 무방합니다.

일반적으로 일시 중단되지 않거나 로드되지 않은 비지속성 인스턴스는 삭제해도 안전합니다. 삭제 하면 안 **모든** 비지속형 인스턴스가 인스턴스 집합에는 방금 만든는 하지만 되지 않은 인스턴스가 포함 되므로 아직 저장 합니다. 인스턴스가 로드된 워크플로 서비스 호스트에서 예외를 발생시켰거나 인스턴스 자체에서 예외를 발생시켰기 때문에 방치된 비지속성 인스턴스만 삭제해야 합니다.

> [!WARNING]
> 인스턴스 저장소에서 비지속성 인스턴스를 삭제하면 저장소의 크기가 줄어들고 저장소 작업의 성능이 향상될 수 있습니다.
