---
ms.openlocfilehash: 19e0524f4d40517f3e305b2397e628e0478da8f9
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803540"
---
### <a name="workflow-xoml-file-checksums-changed-from-md5-to-sha256"></a>워크플로 XOML 파일 체크섬이 MD5에서 SHA256으로 변경됨

|   |   |
|---|---|
|세부 정보|Visual Studio를 사용하여 XOML 기반 워크플로 디버깅을 지원하기 위해 XOML 파일이 포함된 워크플로 프로젝트를 빌드할 때 XOML 파일의 콘텐츠에 대한 체크섬이 <xref:System.Workflow.ComponentModel.Compiler.WorkflowMarkupSourceAttribute.MD5Digest?displayProperty=nameWithType> 값으로 생성된 코드에 포함됩니다. .NET Framework 4.7.2 이전 버전에서 이 체크섬 해시는 MD5 알고리즘을 사용하여 FIPS 지원 시스템에 문제가 발생했습니다. .NET Framework 4.8부터 사용된 알고리즘은 SHA256입니다. WorkflowMarkupSourceAttribute.MD5Digest와 호환되도록 생성된 체크섬의 처음 16바이트만 사용됩니다. 이는 디버깅 중에 문제가 발생할 수 있습니다. 프로젝트를 다시 빌드해야 할 수도 있습니다.|
|제안|프로젝트를 다시 빌드해도 문제가 해결되지 않으면 다음 코드에서 <code>AppContext</code> 스위치 &quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum&quot;을 true로 설정합니다.<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum&quot;, true);&#13;&#10;</code></pre>또는 구성 파일(사용 중인 MSBuild.exe에의 경우 MSBuild.exe.config이 있어야 함)에서 다음을 수행합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.8|
|Type|대상 변경|

