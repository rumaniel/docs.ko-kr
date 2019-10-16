---
ms.openlocfilehash: 47aa67096f8dcd250521d9c34dde97cb2eb368d7
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803439"
---
### <a name="workflow-xoml-definition-and-sqltrackingservice-cache-keys-changed-from-md5-to-sha256"></a>워크플로 XOML 정의 및 SqlTrackingService 캐시 키가 MD5에서 SHA256으로 변경됨

|   |   |
|---|---|
|세부 정보|워크플로 런타임은 XOML에 정의된 워크플로 정의의 캐시를 유지합니다. 또한 SqlTrackingService는 문자열에 의해 키가 지정된 캐시를 유지합니다. 이러한 캐시는 체크섬 해시 값을 포함하는 값에 의해 키가 지정됩니다. .NET Framework 4.7.2 이전 버전에서 이 체크섬 해시는 MD5 알고리즘을 사용하여 FIPS 지원 시스템에 문제가 발생했습니다. .NET Framework 4.8부터 사용되는 알고리즘은 SHA256입니다. 워크플로 런타임 및 SqlTrackingService가 시작될 때마다 다시 계산되기 때문에 이 변경 내용과의 호화성 문제가 없어야 합니다. 그러나 고객이 필요한 경우 레거시 해싱 알고리즘의 사용량으로 되돌릴 수 있는 쿼크를 제공했습니다.|
|제안|워크플로를 실행할 때 이 변경으로 인해 문제가 발생하는 경우 <code>AppContext</code> 스위치 중 하나 또는 둘 다를 설정해 보세요.<ul><li>&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey&quot;를 true로 설정합니다.</li><li>&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey&quot;를 true로 설정합니다.</li></ul>코드:<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey&quot;, true);&#13;&#10;System.AppContext.SetSwitch(&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey&quot;, true);&#13;&#10;</code></pre>또는 구성 파일(<xref:System.Workflow.Runtime.WorkflowRuntime> 개체를 만드는 애플리케이션의 구성 파일에 있어야 함):<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey=true&quot; /&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKeytrue&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.8|
|Type|대상 변경|

