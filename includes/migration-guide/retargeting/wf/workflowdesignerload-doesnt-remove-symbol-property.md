---
ms.openlocfilehash: 97a92c6bce80b93e9a8bdd863bf881631eaffb27
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804676"
---
### <a name="workflowdesignerload-doesnt-remove-symbol-property"></a>WorkflowDesigner.Load가 기호 속성을 제거하지 않음

|   |   |
|---|---|
|세부 정보|워크플로 디자이너에서 .NET Framework 4.5를 대상으로 하고 <xref:System.Activities.Presentation.WorkflowDesigner.Load> 메서드를 사용하여 다시 호스트된 3.5 워크플로를 로드하면 워크플로를 저장하는 동안 <xref:System.Xaml.XamlDuplicateMemberException?displayProperty=name>가 throw됩니다.|
|제안|이 버그는 Workflow Designer에서 .NET Framework 4.5를 대상으로 할 때에 매니페스트되므로 <code>WorkflowDesigner.Context.Services.GetService&lt;DesignerConfigurationService&gt;().TargetFrameworkName</code>를 .NET Framework 4.0로 설정하여 해결할 수 있습니다. 또는 <xref:System.Activities.Presentation.WorkflowDesigner.Load> 대신 <xref:System.Activities.Presentation.WorkflowDesigner.Load(System.String)> 메서드를 사용하여 워크플로를 로드하여 문제를 방지할 수 있습니다.|
|범위|주요함|
|버전|4.5|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Activities.Presentation.WorkflowDesigner.Load?displayProperty=nameWithType></li></ul>|

