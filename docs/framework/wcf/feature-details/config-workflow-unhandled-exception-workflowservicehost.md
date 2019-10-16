---
title: '방법: WorkflowServiceHost를 사용하여 워크플로의 처리되지 않은 예외 동작 구성'
ms.date: 03/30/2017
ms.assetid: 51b25c86-292c-43e4-8d13-273d2badc8ad
ms.openlocfilehash: aec2fd80e10ae1959b29c0883d51c4045517d792
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957251"
---
# <a name="how-to-configure-workflow-unhandled-exception-behavior-with-workflowservicehost"></a>방법: WorkflowServiceHost를 사용하여 워크플로의 처리되지 않은 예외 동작 구성
<xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>는 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에서 호스팅되는 워크플로 내에서 처리되지 않은 예외가 발생할 경우 수행할 작업을 지정할 수 있도록 하는 동작입니다. 이 항목에서는 구성 파일에서 이 동작을 구성하는 방법을 보여 줍니다.  
  
### <a name="to-configure-workflowunhandledexceptionbehavior"></a>WorkflowUnhandledExceptionBehavior를 구성하려면  
  
1. 다음 예제와`workflowUnhandledException`같이 처리 되지 않은 예외가`behavior`발생할 때 수행할 작업을`serviceBehaviors`지정 하는 `action` 특성을 사용 하 여 < > 요소 내의 < > 요소에 < > 요소를 추가 합니다.  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowUnhandledException action="abandonAndSuspend"/>   
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
    > [!NOTE]
    > 위의 샘플에서 사용하는 구성은 단순화된 구성입니다. 자세한 내용은 [간소화 된 구성](../../../../docs/framework/wcf/simplified-configuration.md)을 참조 하세요.  
  
     이 동작은 다음 예제와 같이 코드에서 구성할 수 있습니다.  
  
    ```csharp  
    host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.AbandonAndSuspend });  
    ```  
  
     `action` <`workflowUnhandledException`> 요소의 특성은 다음 값 중 하나로 설정할 수 있습니다.  
  
     **abandon**  
     유지되는 인스턴스 상태를 변경하지 않고 메모리에서 인스턴스를 중단합니다. 즉, 마지막 유지 지점으로 롤백합니다.  
  
     **abandonAndSuspend**  
     메모리에서 인스턴스를 중단하고 유지되는 인스턴스가 일시 중단되도록 업데이트합니다.  
  
     **cancel**  
     인스턴스에 대한 취소 처리기를 호출하고 메모리에서 인스턴스를 완료합니다. 이 경우 인스턴스가 인스턴스 저장소에서 제거될 수도 있습니다.  
  
     **terminate**  
     메모리에서 인스턴스를 완료하고 인스턴스 저장소에서 제거합니다.  
  
     에 대 한 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>자세한 내용은 [워크플로 서비스 호스트 확장성](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [워크플로 서비스 호스트 확장성](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)
- [워크플로 서비스](../../../../docs/framework/wcf/feature-details/workflow-services.md)
