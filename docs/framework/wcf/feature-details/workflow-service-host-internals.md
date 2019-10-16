---
title: 워크플로 서비스 호스트 내부 기능
ms.date: 03/30/2017
ms.assetid: af44596f-bf6a-4149-9f04-08d8e8f45250
ms.openlocfilehash: 0596e15e27460a08f859ec3398afbeae752c86fc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61984222"
---
# <a name="workflow-service-host-internals"></a>워크플로 서비스 호스트 내부 기능
<xref:System.ServiceModel.WorkflowServiceHost>에서는 워크플로 서비스에 대한 호스트를 제공합니다. 들어오는 메시지를 수신 대기하여 적절한 워크플로 서비스 인스턴스로 라우팅하고 유휴 워크플로의 언로드 및 유지를 제어하는 등의 작업을 담당합니다. 이 항목에서는 WorkflowServiceHost가 들어오는 메시지를 처리하는 방법을 설명합니다.  
  
## <a name="workflowservicehost-overview"></a>WorkflowServiceHost 개요  

<xref:System.ServiceModel.WorkflowServiceHost> 클래스는 워크플로 서비스를 호스트하는 데 사용됩니다. 들어오는 메시지를 수신 대기하여 적절한 서비스 인스턴스로 라우팅하고 필요에 따라 새 인스턴스를 만들거나 영구 스토리지에서 기존 인스턴스를 로드합니다. 다음 다이어그램은 높은 수준의 방법은 <xref:System.ServiceModel.WorkflowServiceHost> 작동 합니다. 
  
 ![워크플로 서비스 호스트의 개요를 보여 주는 다이어그램입니다.](./media/workflow-service-host-internals/workflow-service-host-high-level-overview.gif)  
  
 이 다이어그램에서는 <xref:System.ServiceModel.WorkflowServiceHost>가 .xamlx 파일에서 워크플로 서비스 정의를 로드하고 구성 파일에서 구성 정보를 로드하는 것을 보여 줍니다. 또한 추적 프로필에서 추적 구성을 로드합니다. <xref:System.ServiceModel.WorkflowServiceHost>는 제어 작업을 워크플로 인스턴스로 보내는 데 사용할 수 있는 워크플로 제어 엔드포인트를 노출합니다.  자세한 내용은 참조 [워크플로 제어 끝점 샘플](../../../../docs/framework/wcf/feature-details/workflow-control-endpoint.md)합니다.  
  
 <xref:System.ServiceModel.WorkflowServiceHost>는 들어오는 애플리케이션 메시지를 수신 대기하는 애플리케이션 엔드포인트도 노출합니다. 들어오는 메시지가 도착하면 적절한 워크플로 서비스 인스턴스로 전송됩니다(현재 로드되어 있는 경우). 필요한 경우 새 워크플로 인스턴스가 만들어지고, 기존 인스턴스가 유지된 경우에는 지속성 저장소에서 로드됩니다.  
  
## <a name="workflowservicehost-details"></a>WorkflowServiceHost 세부 정보  
 다음 다이어그램에서는 어떻게 <xref:System.ServiceModel.WorkflowServiceHost> 좀 더 자세히에서 메시지를 처리 합니다.  
  
 ![워크플로 서비스 호스트 메시지 흐름을 보여 주는 다이어그램입니다.](./media/workflow-service-host-internals/workflow-service-host-message-flow.gif)  
  
 이 다이어그램에서는 세 가지 엔드포인트인 애플리케이션 엔드포인트, 워크플로 제어 엔드포인트 및 워크플로 호스팅 엔드포인트를 보여 줍니다. 애플리케이션 엔드포인트는 특정 워크플로 인스턴스에 바인딩된 메시지를 받습니다. 워크플로 제어 엔드포인트는 제어 작업을 수신 대기합니다. 워크플로 호스팅 엔드포인트는 <xref:System.ServiceModel.WorkflowServiceHost>가 서비스가 아닌 워크플로를 로드하고 실행하도록 하는 메시지를 수신 대기합니다. 다이어그램에 나와 있듯이 모든 메시지는 WCF 런타임을 통해 처리됩니다.  워크플로 서비스 인스턴스 제한은 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> 속성을 사용하여 구현됩니다. 이 속성은 동시 워크플로 서비스 인스턴스 수를 제한합니다. 이 제한을 초과하면 새 워크플로 서비스 인스턴스에 대한 추가 요청이나 지속형 워크플로 인스턴스 활성화 요청이 큐에 저장됩니다. 큐에 대기 중인 요청은 새 인스턴스에 대한 요청인지, 실행 중인 지속형 인스턴스에 대한 요청인지에 관계없이 FIFO 순서대로 처리됩니다. 처리되지 않은 예외가 처리되는 방법과 유휴 워크플로 서비스가 언로드되고 지속되는 방법을 결정하는 호스트 정책 정보가 로드됩니다. 이러한 항목에 대 한 자세한 내용은 참조 하세요. [방법: 워크플로 구성 합니다. 처리 되지 않은 예외 동작 WorkflowServiceHost 사용 하 여](../../../../docs/framework/wcf/feature-details/config-workflow-unhandled-exception-workflowservicehost.md) 고 [방법: WorkflowServiceHost를 사용 하 여 유휴 동작 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-idle-behavior-with-workflowservicehost.md)합니다. 워크플로 인스턴스는 호스트 정책에 따라 유지되고 필요한 경우 다시 로드됩니다. 워크플로 지 속성 참조에 대 한 자세한 내용은: [방법: WorkflowServiceHost를 사용 하 여 지 속성을 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-persistence-with-workflowservicehost.md), [장기 실행 워크플로 서비스를 만드는](../../../../docs/framework/wcf/feature-details/creating-a-long-running-workflow-service.md), 및 [워크플로 지 속성](../../../../docs/framework/windows-workflow-foundation/workflow-persistence.md)합니다.  
  
 다음 그림에서는 WorkflowServiceHost.Open이 호출 하는 경우 흐름을 보여 줍니다.  
  
 ![WorkflowServiceHost.Open이 호출 하는 경우 흐름을 보여 주는 다이어그램입니다.](./media/workflow-service-host-internals/workflow-service-host-open.gif)  
  
 워크플로가 XAML에서 로드되고 작업 트리가 만들어집니다. <xref:System.ServiceModel.WorkflowServiceHost>가 작업 트리를 단계별로 진행하면서 서비스 설명을 만듭니다. 구성이 호스트에 적용됩니다. 마지막으로 호스트가 들어오는 메시지를 수신 대기하기 시작합니다.  
  
 다음 그림에서는 무엇을 <xref:System.ServiceModel.WorkflowServiceHost> CanCreateInstance로 설정 된 Receive 활동에 바인딩된 메시지를 받을 때 수행 `true`:  
  
 ![CanCreateInstance가 true 고 메시지를 받을 때 워크플로 호스트에서 사용 하는 트리를 결정 합니다.](./media/workflow-service-host-internals/workflow-service-host-receive-message-cancreateinstance.gif)  
  
 메시지가 도착하고 WCF 채널 스택에서 처리됩니다. 스로틀이 확인되고 상관 관계 쿼리가 실행됩니다. 메시지가 기존 인스턴스에 바인딩된 경우 메시지가 배달됩니다. 새 인스턴스를 만들어야 하는 경우에는 Receive 활동의 CanCreateInstance 속성이 확인됩니다. 이 속성이 true로 설정되었으면 새 인스턴스가 만들어지고 메시지가 배달됩니다.  
  
 다음 그림에서는 <xref:System.ServiceModel.WorkflowServiceHost>에서 CanCreateInstance가 false로 설정된 Receive 작업에 바인딩된 메시지를 받을 때 수행하는 작업을 보여 줍니다.  
  
 ![CanCreateInstance가 false 메시지를 받을 때 워크플로 호스트에서 사용 하는 트리를 결정 합니다.](./media/workflow-service-host-internals/workflow-service-host-receive-message.gif)  
  
 메시지가 도착하고 WCF 채널 스택에서 처리됩니다. 스로틀이 확인되고 상관 관계 쿼리가 실행됩니다. 메시지가 기존 인스턴스에 바인딩되어 있으므로(CanCreateInstance가 false이기 때문) 인스턴스가 지속성 저장소에서 로드되고 책갈피가 다시 시작되며 워크플로가 실행됩니다.  
  
> [!WARNING]
> SQL Server가 NamedPipe 프로토콜에서만 수신하도록 구성되어 있으면 워크플로 서비스 호스트가 열리지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [워크플로 서비스](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [워크플로 서비스 호스팅](../../../../docs/framework/wcf/feature-details/hosting-workflow-services.md)
- [워크플로 제어 엔드포인트](../../../../docs/framework/wcf/feature-details/workflow-control-endpoint.md)
- [방법: 워크플로 구성 합니다. 처리 되지 않은 예외 동작 WorkflowServiceHost 사용 하 여](../../../../docs/framework/wcf/feature-details/config-workflow-unhandled-exception-workflowservicehost.md)
- [장기 실행 워크플로 서비스 만들기](../../../../docs/framework/wcf/feature-details/creating-a-long-running-workflow-service.md)
- [워크플로 유지](../../../../docs/framework/windows-workflow-foundation/workflow-persistence.md)
