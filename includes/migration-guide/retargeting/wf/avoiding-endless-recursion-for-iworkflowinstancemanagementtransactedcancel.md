---
ms.openlocfilehash: f78f31f4328a45b5ef3f25cdf6eddac1b17fb6e6
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59234067"
---
### <a name="avoiding-endless-recursion-for-iworkflowinstancemanagementtransactedcancel-and-iworkflowinstancemanagementtransactedterminate"></a>IWorkflowInstanceManagement.TransactedCancel 및 IWorkflowInstanceManagement.TransactedTerminate의 무한 재귀를 방지

|   |   |
|---|---|
|세부 정보|<xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedCancel%2A?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedTerminate%2A?displayProperty=nameWithType> API를 사용하여 워크플로 인스턴스를 취소하거나 종료하는 경우에 워크플로 인스턴스는 <code>Workflow</code> 런타임이 요청 처리의 일부로 서비스 인스턴스를 유지하려 할 때 무한 재귀로 인해 스택 오버플로가 발생할 수 있습니다. 워크플로 인스턴스가 일부 기타 처리 중인 WCF가 다른 서비스가 완료되기를 대기 중인 상태에 있는 경우 문제가 발생합니다. <code>TransactedCancel</code> 및 <code>TransactedTerminate</code> 작업은 워크플로 서비스 인스턴스에 대해 큐 대기 중인 작업 항목을 만듭니다. 이러한 작업 항목은 <code>TransactedCancel/TransactedTerminate</code> 요청 처리의 일부로 실행되지 않습니다. 워크플로 서비스 인스턴스는 기타 처리 중인 WCF 요청이 완료되기를 기다리느라 사용 중이므로 만든 작업 항목은 큐 대기 상태를 유지합니다. <code>TransactedCancel/TransactedTerminate</code> 작업이 완료되고 컨트롤이 다시 클라이언트로 반환됩니다. <code>TransactedCancel/TransactedTerminate</code> 작업과 연관된 트랜잭션이 커밋하려 하는 경우 워크플로 서비스 인스턴스 상태를 유지해야 합니다. 그러나 인스턴스에 대해 처리 중인 <code>WCF</code> 요청이 있기 때문에 워크플로 런타임은 워크플로 서비스 인스턴스를 지속할 수 없고 무한 재귀 루프는 스택 오버플로로 이어집니다. <code>TransactedCancel</code> 및 <code>TransactedTerminate</code>만 메모리에 작업 항목을 만드므로 트랜잭션이 존재한다는 팩트는 아무 영향도 줄 수 없습니다. 트랜잭션 롤백은 작업 항목을 삭제하지 않습니다. 이 문제를 해결하기 위해 .NET Framework 4.7.2부터 <code>TransactedCancel</code> 및 <code>TransactedTerminate</code>에 대한 트랜잭션을 무시하도록 지시하는 워크플로 서비스의 <code>web.config/app.config</code>에 추가될 수 있는 <code>AppSetting</code>을 도입했습니다. 이렇게 하면 트랜잭션이 워크플로 인스턴스가 유지되기를 기다리지 않고 커밋할 수 있습니다. 이 기능에 대한 AppSetting은 <code>microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate</code>이라고 합니다. <code>true</code> 값은 트랜잭션을 무시하고 따라서 스택 오버플로를 방지해야 한다는 것을 나타냅니다. 이 AppSetting의 기본값은 <code>false</code>이므로 기존 워크플로 서비스 인스턴스는 영향을 받지 않습니다.|
|제안 해결 방법|AppFabric 또는 다른 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 클라이언트를 사용하고, 워크플로 인스턴스를 취소하거나 종료하려고 할 때 워크플로 서비스 인스턴스에서 스택 오버플로가 발생하는 경우 워크플로 서비스에 대한 web.config/app.config 파일의 <code>&lt;appSettings&gt;</code> 섹션에 다음을 추가할 수 있습니다.<pre><code class="lang-xml">&lt;add key=&quot;microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate&quot; value=&quot;true&quot;/&gt;&#13;&#10;</code></pre>문제가 발생하지 않는 경우 이 작업을 수행할 필요가 없습니다.|
|범위|Microsoft Edge|
|버전|4.7.2|
|형식|대상 변경|
