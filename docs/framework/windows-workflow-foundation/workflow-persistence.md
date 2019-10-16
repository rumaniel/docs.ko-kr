---
title: 워크플로 유지
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], persistence
ms.assetid: 39e69d1f-b771-4c16-9e18-696fa43b65b2
ms.openlocfilehash: afe47975a393db3074222ebf0461f5b73fb6442d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64655804"
---
# <a name="workflow-persistence"></a>워크플로 유지
워크플로 지속성은 프로세스 또는 컴퓨터 정보에 독립적인 영구 워크플로 인스턴스 상태 캡처입니다. 이 작업은 시스템 오류가 발생한 경우에 워크플로 인스턴스에 대한 잘 알려진 복구 지점을 제공하거나, 현재 작업 중이 아닌 워크플로 인스턴스를 언로드하여 메모리를 보존하거나, 워크플로 인스턴스의 상태를 서버 팜의 한 노드에서 다른 노드로 이동하기 위해 수행합니다.  
  
 지속성은 프로세스의 신속성, 확장성, 오류 복구, 효율적인 메모리 관리를 가능하게 해줍니다. 지속성 프로세스는 유지 지점을 식별하고, 저장할 데이터를 수집하며, 마지막으로 지속성 공급자에게 실제 데이터 스토리지를 위임하는 과정으로 구성됩니다.  
  
 워크플로 지 속성을 사용 하도록 설정 하려면 인스턴스 저장소를 연결 해야 합니다 **WorkflowApplication** 또는 **WorkflowServiceHost** 에 설명 된 대로 [방법: 워크플로 및 워크플로 서비스에 대 한 지](how-to-enable-persistence-for-workflows-and-workflow-services.md)합니다. 합니다 **WorkflowApplication** 하 고 **WorkflowServiceHost** 연결 된 인스턴스 저장소를 사용 하 여 워크플로 인스턴스를 로드 및 지 속성 저장소에 워크플로 인스턴스를 유지를 사용 하도록 설정 하려면 지 속성 저장소에 저장 된 워크플로 인스턴스 데이터를 기반으로 하는 메모리입니다.  
  
 합니다 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 와 함께 제공 되는 **SqlWorkflowInstanceStore** 데이터 및 SQL Server 2005 또는 SQL Server 2008 데이터베이스에 워크플로 인스턴스에 대 한 메타 데이터 지 속성을 허용 하는 클래스입니다. 참조 [SQL 워크플로 인스턴스 저장소](sql-workflow-instance-store.md) 대 한 자세한 내용은 합니다.  
  
 워크플로 인스턴스 관련 정보와 함께 애플리케이션별 데이터를 저장하고 로드하려면 <xref:System.Activities.Persistence.PersistenceParticipant> 클래스를 확장하는 지속성 참석자를 만들 수 있습니다. 지속성 참석자는 지속성 프로세스에 참여하여 serialize 가능한 사용자 지정 데이터를 지속성 저장소에 저장하고, 인스턴스 저장소의 데이터를 메모리로 로드하며, 지속성 트랜잭션에서 추가 논리를 수행합니다. 자세한 내용은 [지 속성 참석자](persistence-participants.md)합니다.  
  
 Windows Server AppFabric은 지속성의 구성 프로세스를 단순화합니다. 자세한 내용은 참조 하세요. [Windows Server App Fabric 지 속성 개념](https://go.microsoft.com/fwlink/?LinkId=201200)  
  
## <a name="implicit-persistence-points"></a>암시적 유지 지점  
 다음 목록에는 인스턴스 저장소가 워크플로에 연결되어 있을 때 워크플로가 유지되는 조건에 대한 예제가 포함되어 있습니다.  
  
- 경우는 **TransactionScope** 활동이 완료 된 또는 **TransactedReceiveScope** 활동이 완료 합니다.  
  
- 워크플로 인스턴스가 유휴 상태가 되는 경우와 **WorkflowIdleBehavior** 워크플로 호스트에 설정 됩니다. 이런 예를 들어 메시징 활동을 사용 하는 경우 또는 **지연** 활동입니다.  
  
- WorkflowApplication 유휴 상태가 되는 경우와 **PersistableIdle** 응용 프로그램의 속성이로 설정 되어 **PersistableIdleAction.Persist**합니다.  
  
- 워크플로 인스턴스를 유지하거나 언로드하도록 호스트 애플리케이션에 지시할 경우  
  
- 워크플로 인스턴스가 종료되거나 완료되는 경우  
  
- 경우는 **Persist** 활동을 실행 합니다.  
  
- 이전 버전의 Windows Workflow Foundation을 사용하여 개발된 워크플로 인스턴스에서 상호 운용 가능한 방식으로 실행되는 동안 유지 지점을 발견한 경우  
  
## <a name="in-this-section"></a>섹션 내용  
  
- [SQL 워크플로 인스턴스 저장소](sql-workflow-instance-store.md)  
  
- [인스턴스 저장소](instance-stores.md)  
  
- [지속성 참석자](persistence-participants.md)  
  
- [지속성 모범 사례](persistence-best-practices.md)  
  
- [비지속형 워크플로 인스턴스](non-persisted-workflow-instances.md)  
  
- [워크플로 일시 중지 및 다시 시작](pausing-and-resuming-a-workflow.md)
