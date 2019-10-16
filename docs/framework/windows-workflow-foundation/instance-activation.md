---
title: 인스턴스 활성화
ms.date: 03/30/2017
ms.assetid: 134c3f70-5d4e-46d0-9d49-469a6643edd8
ms.openlocfilehash: 5e0d5a91a0f0ccc02d13ef96c3470da1942cc520
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348253"
---
# <a name="instance-activation"></a>인스턴스 활성화
SQL 워크플로 인스턴스 저장소는 정기적으로 다시 시작되어 지속성 데이터베이스에서 실행 가능하거나 활성화 가능한 워크플로 인스턴스를 검색하는 내부 작업를 실행합니다. 실행 가능한 워크플로 인스턴스를 발견하면 해당 인스턴스를 활성화할 수 있는 워크플로 호스트에 알려 줍니다. 인스턴스 저장소에서 활성화 가능한 워크플로 인스턴스를 발견하면 워크플로 호스트를 활성화하여 워크플로 인스턴스를 실행하는 일반 호스트에 알려 줍니다. 이 항목의 다음 단원에서는 인스턴스 활성화 프로세스에 대해 자세히 설명합니다.  
  
## <a name="RunnableSection"></a> 실행 가능한 워크플로 인스턴스 검색 및 활성화  
 SQL 워크플로 인스턴스 저장소는 워크플로 인스턴스를 고려 *runnable* 인스턴스 일시 중단 된 상태나 완료 된 상태가 아니며 다음 조건을 충족 하는 경우:  
  
- 인스턴스가 잠금 해제되었으며 만료된 보류 중인 타이머가 있습니다.  
  
- 인스턴스에 만료된 잠금이 있습니다.  
  
- 인스턴스를 잠금 해제 하 고 해당 상태가 **Executing**합니다.  
  
 SQL 워크플로 인스턴스 저장소에서는 실행 가능한 인스턴스가 발견되면 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent>를 발생시킵니다. 그러면 SqlWorkflowInstanceStore는 저장소에서 <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>가 한 번 호출될 때까지 모니터링을 중지합니다.  
  
 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent>에 대해 구독되고 인스턴스를 로드할 수 있는 워크플로 호스트는 인스턴스 저장소에 대해 <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>를 실행하여 인스턴스를 메모리로 로드합니다. 워크플로 호스트는 호스트 및 인스턴스 메타 데이터 속성이 있어야 하는 경우 워크플로 인스턴스를 로드할 수 있는 것으로 간주 됩니다 **WorkflowServiceType** 동일한 값으로 설정 합니다.  
  
## <a name="detecting-and-activating-activatable-workflow-instances"></a>활성화 가능한 워크플로 인스턴스 검색 및 활성화  
 워크플로 인스턴스를 사용 하는 것으로 간주 *활성화할 수 있는* 인스턴스를 로드할 수 있는 워크플로 호스트가 없는 컴퓨터에서 실행 중인 경우 인스턴스를 실행할 수 있습니다. 실행 가능한 워크플로 인스턴스의 정의는 위의 "실행 가능한 워크플로 인스턴스 검색 및 활성화"를 참조하세요.  
  
 SQL 워크플로 인스턴스 저장소에서는 데이터베이스에서 활성화 가능한 워크플로 인스턴스가 발견되면 <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent>를 발생시킵니다. 그러면 SqlWorkflowInstanceStore는 저장소에서 <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand>가 한 번 호출될 때까지 모니터링을 중지합니다.  
  
 <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent>에 대해 구독되는 일반 호스트는 이벤트를 수신할 경우 인스턴스 저장소에 대해 <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand>를 실행하여 워크플로 호스트를 만드는 데 필요한 활성화 매개 변수를 가져옵니다. 일반 호스트는 이러한 활성화 매개 변수를 사용하여 워크플로 호스트를 만들고, 워크플로 호스트가 실행 가능한 서비스 인스턴스를 로드 및 실행합니다.  
  
## <a name="generic-hosts"></a>일반 호스트  
 일반 호스트는 메타 데이터 속성의 값을 사용 하 여 호스트 **WorkflowServiceType** 로 설정 되어 있는 일반 호스트에 대 한 있습니다 **WorkflowServiceType.Any** 모든 워크플로 유형을 처리할 수 있음을 나타냅니다. 일반 호스트 이라는 XName 매개 변수가 **ActivationType**합니다.  
  
 SQL 워크플로 인스턴스 저장소로 ActivationType 매개 변수의 값을 사용 하 여 일반 호스트를 지원 하는 현재 **WAS**합니다. ActivationType이 WAS로 설정되어 있지 않으면 SQL 워크플로 인스턴스 저장소는 <xref:System.Runtime.DurableInstancing.InstancePersistenceException>을 throw합니다. Windows Server appfabric 호스팅 기능을 사용 하 여 제공 되는 워크플로 관리 서비스는로 정품 인증 유형을 포함 하는 일반 호스트 **WAS**합니다.  
  
 WAS 활성화를 위해 일반 호스트에는 새 호스트를 활성화할 수 있는 엔드포인트 주소를 파생하는 활성화 매개 변수 집합이 필요합니다. WAS 활성화를 위한 활성화 매개 변수는 사이트 이름, 사이트에 상대적인 애플리케이션 경로 및 애플리케이션에 상대적인 서비스 경로입니다. SQL 워크플로 인스턴스 저장소는 <xref:System.Activities.DurableInstancing.SaveWorkflowCommand>를 실행하는 동안 이러한 활성화 매개 변수를 저장합니다.  
  
## <a name="runnable-instances-detection-period"></a>실행 가능한 인스턴스 검색 기간  
 합니다 **실행 가능한 인스턴스 검색 기간** SQL 워크플로 인스턴스 저장소를 실행 가능 하거나 활성화 가능한 워크플로 검색 하는 검색 작업을 실행 하는 기간을 지정 하는 SQL 워크플로 인스턴스 저장소의 속성 이전 검색 주기 후 지 속성 데이터베이스의 인스턴스. 참조 [실행 가능한 인스턴스 검색 기간](runnable-instances-detection-period.md) 이 속성에 대 한 자세한 내용은 합니다.
