---
title: 워크플로 제어 엔드포인트
ms.date: 03/30/2017
ms.assetid: 1b883334-1590-4fbb-b0d6-65197efe0700
ms.openlocfilehash: 3c826147d9d3ad452957230adb8f32659b4d1352
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988550"
---
# <a name="workflow-control-endpoint"></a>워크플로 제어 엔드포인트
개발자는 워크플로 제어 엔드포인트를 사용하여 <xref:System.ServiceModel.Activities.WorkflowServiceHost>를 사용하여 호스팅되는 워크플로 인스턴스를 원격으로 제어할 수 있는 제어 작업을 호출할 수 있습니다. 이 기능은 일시 중단, 다시 시작 및 종료 같은 제어 작업을 프로그래밍 방식으로 수행하는 데 사용될 수 있습니다.  
  
> [!WARNING]
> 트랜잭션 내에서 워크플로 제어 끝점을 사용 하 고 제어 되는 워크플로에 <xref:System.Activities.Statements.Persist> 활동이 포함 된 경우 트랜잭션 제한 시간이 초과 될 때까지 워크플로 인스턴스가 차단 됩니다.  
  
## <a name="workflow-instance-management"></a>워크플로 인스턴스 관리  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]에서는 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement>라는 새 계약을 정의합니다. 이 계약은 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에서 호스팅하는 워크플로 인스턴스를 원격으로 제어할 수 있도록 하는 일련의 제어 작업을 정의합니다. <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>는 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 계약의 구현을 제공하는 표준 엔드포인트입니다. <xref:System.ServiceModel.Activities.WorkflowControlClient>는 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>에 제어 작업을 보내는 데 사용하는 클래스입니다.  
  
 워크플로 인스턴스의 상태는 다음 중 하나일 수 있습니다.  
  
 활성  
 워크플로 인스턴스가 완료됨 상태에 도달하기 전이고 일시 중단됨 상태에 있지 않는 상태입니다. 이 상태 동안에는 워크플로 인스턴스가 실행되어 애플리케이션 메시지를 처리합니다.  
  
 일시 중단됨  
 이 상태 동안에는 실행이 시작되지 않았거나 부분적으로 실행된 동작이 있는 경우에도 워크플로 인스턴스가 실행되지 않습니다.  
  
 완료  
 워크플로 인스턴스의 최종 상태입니다. 완료됨 상태에 도달한 후에는 워크플로 인스턴스를 실행할 수 없습니다.  
  
## <a name="iworkflowinstancemanagement"></a>IWorkflowInstanceManagement  
 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 인터페이스는 동기 및 비동기 버전이 있는 일련의 제어 작업을 정의합니다. 트랜잭트 버전에서는 트랜잭션 인식 바인딩을 사용해야 합니다. 다음 표에서는 지원되는 제어 작업을 보여 줍니다.  
  
|제어 작업|Description|  
|-----------------------|-----------------|  
|중단|워크플로 인스턴스의 실행을 강제로 중지합니다.|  
|Cancel|워크플로 인스턴스를 활성 또는 일시 중단됨 상태에서 완료됨 상태로 전환합니다.|  
|실행|워크플로 인스턴스를 실행할 수 있는 기회를 제공합니다.|  
|일시 중단|워크플로 인스턴스를 활성 상태에서 일시 중단됨 상태로 전환합니다.|  
|종료|워크플로 인스턴스를 활성 또는 일시 중단됨 상태에서 완료됨 상태로 전환합니다.|  
|일시 중단 해제|워크플로 인스턴스를 일시 중단됨 상태에서 활성 상태로 전환합니다.|  
|TransactedCancel|클라이언트로부터 이동해 왔거나 로컬로 만들어진 트랜잭션에서 취소 작업을 수행합니다. 시스템에서 워크플로 인스턴스의 지속적 상태를 유지하는 경우 이 작업이 실행되는 동안 워크플로 인스턴스를 유지해야 합니다.|  
|TransactedRun|클라이언트로부터 이동해 왔거나 로컬로 만들어진 트랜잭션에서 실행 작업을 수행합니다. 시스템에서 워크플로 인스턴스의 지속적 상태를 유지하는 경우 이 작업이 실행되는 동안 워크플로 인스턴스를 유지해야 합니다.|  
|TransactedSuspend|클라이언트로부터 이동해 왔거나 로컬로 만들어진 트랜잭션에서 일시 중단 작업을 수행합니다. 시스템에서 워크플로 인스턴스의 지속적 상태를 유지하는 경우 이 작업이 실행되는 동안 워크플로 인스턴스를 유지해야 합니다.|  
|TransactedTerminate|클라이언트로부터 이동해 왔거나 로컬로 만들어진 트랜잭션에서 종료 작업을 수행합니다. 시스템에서 워크플로 인스턴스의 지속적 상태를 유지하는 경우 이 작업이 실행되는 동안 워크플로 인스턴스를 유지해야 합니다.|  
|TransactedUnsuspend|클라이언트로부터 이동해 왔거나 로컬로 만들어진 트랜잭션에서 일시 중단 해제 작업을 수행합니다. 시스템에서 워크플로 인스턴스의 지속적 상태를 유지하는 경우 이 작업이 실행되는 동안 워크플로 인스턴스를 유지해야 합니다.|  
  
 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 계약은 새 워크플로 인스턴스를 만들 수 없고 기존 워크플로 인스턴스를 관리할 수만 있습니다. 새 워크플로 인스턴스를 원격으로 만드는 방법에 대 한 자세한 내용은 [워크플로 서비스 호스트 확장성](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)을 참조 하세요.  
  
## <a name="workflowcontrolendpoint"></a>WorkflowControlEndpoint  
 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>는 고정된 계약인 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement>가 있는 표준 엔드포인트입니다. 이 엔드포인트를 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 인스턴스에 추가할 경우 이 엔드포인트를 사용하여 호스트 인스턴스가 호스팅하는 모든 워크플로 인스턴스에 명령 작업을 보낼 수 있습니다. 표준 끝점에 대 한 자세한 내용은 [표준 끝점](../../../../docs/framework/wcf/feature-details/standard-endpoints.md)을 참조 하세요.  
  
## <a name="workflowcontrolclient"></a>WorkflowControlClient  
 <xref:System.ServiceModel.Activities.WorkflowControlClient>는 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>의 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에 제어 메시지를 보낼 수 있는 클래스입니다. 트랜잭션 작업을 제외하고 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 계약에서 지원하는 각 작업에 대한 메서드가 포함되어 있습니다. <xref:System.ServiceModel.Activities.WorkflowControlClient>는 앰비언트 트랜잭션을 사용하여 트랜잭션 작업을 사용해야 하는지 여부를 결정합니다.
