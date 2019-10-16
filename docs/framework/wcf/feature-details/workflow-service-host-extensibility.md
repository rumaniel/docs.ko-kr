---
title: 워크플로 서비스 호스트 확장
ms.date: 03/30/2017
ms.assetid: c0e8f7bb-cb13-49ec-852f-b85d7c23972f
ms.openlocfilehash: 4f1f67feb728cb2236f84c88ff223058d34990dc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648365"
---
# <a name="workflow-service-host-extensibility"></a>워크플로 서비스 호스트 확장
[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]에서는 워크플로 서비스를 호스트하는 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 클래스를 제공합니다. 이 클래스는 관리되는 애플리케이션의 워크플로 서비스나 Windows 서비스를 자체 호스트할 때 사용되며, IIS(인터넷 정보 서비스) 또는 WAS(Windows Process Activation Service)에서 워크플로 서비스를 호스트할 때도 사용됩니다. <xref:System.ServiceModel.Activities.WorkflowServiceHost> 클래스는 사용자 지정 확장을 추가하고, 유휴 동작을 변경하고, 서비스가 아닌 워크플로(메시징 작업을 사용하지 않는 워크플로)를 호스트할 수 있는 확장명 지점을 제공합니다.  
  
## <a name="workflow-service-host-extensions"></a>워크플로 서비스 호스트 확장  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에는 <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A>에 확장을 추가하는 메서드를 제공하는 <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager> 형식의 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 속성이 포함되어 있습니다. <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A> 메서드를 사용하면 각 워크플로 서비스 인스턴스에 대한 확장을 추가할 수 있습니다. 워크플로 서비스 인스턴스를 만들거나 지속성 저장소에서 로드하면 새 확장을 만들기 위해 지정된 대리자가 호출됩니다. <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A> 메서드를 사용하면 각 워크플로 서비스 호스트에 대한 확장을 추가할 수 있습니다. 모든 워크플로 서비스 인스턴스에서 하나의 확장 인스턴스를 공유합니다.  
  
## <a name="react-to-unhandled-exceptions"></a>처리되지 않은 예외에 응답  
 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>를 사용하면 워크플로 서비스 내에서 처리되지 않은 예외가 발생할 경우 수행할 동작을 지정할 수 있습니다. <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior.Action%2A> 속성은 다음 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction> 값 중 하나를 지정합니다.  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Abandon> – 워크플로 서비스 인스턴스를 중단합니다.  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.AbandonAndSuspend> – 마지막으로 지속된 상태로 롤백하고 워크플로 서비스 인스턴스를 일시 중단합니다. 이는 워크플로가 이미 한 번 이상 지속된 경우에만 발생합니다. 그렇지 않은 경우 워크플로 인스턴스가 중단됩니다.  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Cancel> – 인스턴스를 취소합니다.  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Terminate> – 인스턴스를 종료합니다.  
  
 이 동작은 다음 예제와 같이 코드에서 구성할 수 있습니다.  
  
```csharp  
host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.Abandon });  
```  
  
 또한 다음 예제와 같이 구성 파일에서 이 동작을 구성할 수도 있습니다.  
  
```xml
<behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <workflowUnhandledExceptionBehavior action="Abandon" />        
        </behavior>  
      </serviceBehaviors>  
```  
  
## <a name="hosting-non-service-workflows"></a>서비스가 아닌 워크플로 호스팅  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost>를 사용하여 서비스가 아닌 워크플로, <xref:System.ServiceModel.Activities.Receive> 작업으로 시작하지 않는 워크플로 또는 메시징 작업을 사용하지 않는 워크플로를 호스트할 수 있습니다. 일반적으로 워크플로 서비스는 <xref:System.ServiceModel.Activities.Receive> 작업으로 시작합니다. <xref:System.ServiceModel.Activities.WorkflowServiceHost>가 워크플로 서비스에 대한 메시지를 받을 때 실행 중이거나 지속된 워크플로 서비스가 없으면 새 워크플로 서비스 인스턴스가 만들어집니다. 워크플로가 받기 작업으로 시작하지 않으면 메시지를 받는 작업이 없기 때문에 메시지를 보내도 워크플로가 시작되지 않습니다. 서비스가 아닌 워크플로를 호스트하려면 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>에서 클래스를 파생시키고 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A>, <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A> 및 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A>를 재정의합니다. 원하는 인스턴스 ID를 제공하려면 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A>를 재정의합니다. 사용자 지정 워크플로 생성 컨텍스트를 만들거나 기존 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A>의 인스턴스를 채우려면 <xref:System.ServiceModel.Activities.WorkflowCreationContext>를 재정의합니다. 들어오는 메시지에서 책갈피를 수동으로 추출하려면 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A>를 재정의합니다. 이 메서드를 재정의하는 경우 WorkflowHostingEndpoint에 전송된 메시지에 응답하도록 메시지 본문에서 <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A>를 호출해야 합니다. 이렇게 하지 않으면 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 제한을 결국 초과할 수 있습니다. 양방향 계약에서는 클라이언트가 응답을 받지 못하기 때문에 <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> 호출 실패를 감지할 수 있습니다. 단방향 계약에서는 <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> 스로틀 제한이 초과된 후 너무 늦을 때까지 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 호출 실패 실수를 인식하지 못할 수 있습니다. 자세한 내용은 참조 하십시오 합니다 [WorkflowHostingEndpoint 다시 시작 책갈피](../../../../docs/framework/windows-workflow-foundation/samples/workflowhostingendpoint-resume-bookmark.md)서비스가 아닌 워크플로의 새 인스턴스를 만들려면 새 인스턴스를 만드는 작업을 정의 하는 서비스 계약을 선언 합니다. 만들기 작업은 idictionary\<문자열, 개체 > 필수 워크플로 매개 변수를 전달 합니다. 이 계약은 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 파생 클래스에 의해 암시적으로 구현됩니다. 워크플로를 호스트할 때는 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>를 호출하여 <xref:System.ServiceModel.Activities.WorkflowServiceHost.AddServiceEndpoint%2A> 파생 클래스를 추가하고 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>을 호출합니다. 워크플로의 인스턴스를 만들려면 서비스 계약 형식의 <xref:System.ServiceModel.ChannelFactory%601>를 만들고 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A>를 호출합니다. 그러면 서비스 계약에 정의된 만들기 작업을 호출할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [워크플로 서비스](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [메시징 작업](../../../../docs/framework/wcf/feature-details/messaging-activities.md)
