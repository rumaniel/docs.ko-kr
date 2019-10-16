---
title: WorkflowInstanceId 가져오기
ms.date: 03/30/2017
ms.assetid: bd7eea3b-1c28-4b84-9a67-003bc553aa81
ms.openlocfilehash: f8bd3205f5b7a4b3bae5203dc90a3c393cedcbdd
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989379"
---
# <a name="get-workflowinstanceid"></a>WorkflowInstanceId 가져오기
이 샘플에서는 사용자 지정 활동인 `GetWorkflowInstanceId`를 사용하여 워크플로 인스턴스 ID를 반환하는 방법을 보여 줍니다.  
  
## <a name="demonstrates"></a>세부 항목  
 사용자 지정 활동 개발, 워크플로 인스턴스에 액세스하는 방법  
  
## <a name="discussion"></a>토론  
 실행 중인 워크플로의 인스턴스 ID를 가져오려면 코드를 작성해야 합니다. 완전히 선언적인 워크플로를 작성하려면 워크플로 인스턴스 ID를 반환할 수 있는 활동이 필요합니다. 그래야만 워크플로에서 해당 활동을 참조하여 완전히 선언적인 워크플로 작성 환경을 제공할 수 있습니다. 인스턴스 ID에 액세스해야 하는 시나리오에는 여러 가지가 있습니다. 예를 들어 로깅 또는 감사를 위한 시나리오도 여기에 해당하며, (가령 SendReply 활동 내에 이 활동을 사용하는 등) 나중에 연결하기 위해 인스턴스 ID를 클라이언트에 다시 제공하여 애플리케이션 수준의 상관 관계를 만드는 시나리오도 여기에 해당합니다.  
  
 `GetWorkflowInstanceId`는 <xref:System.Activities.CodeActivity%601>로 구현됩니다. 이는 <xref:System.Guid> 형식의 값을 반환해야 하고 워크플로의 인스턴스 ID를 가져오기 위해 <xref:System.Activities.CodeActivityContext>에 액세스해야 하기 때문입니다. 그 구현은 비교적 기본적입니다.  
  
```csharp  
public sealed class GetWorkflowInstanceId : CodeActivity<Guid>  
{  
    protected override Guid Execute(CodeActivityContext context)  
    {  
        return context.WorkflowInstanceId;  
    }  
}
```  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\GetWorkflowInstanceId`
