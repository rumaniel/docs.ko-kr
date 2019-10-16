---
ms.openlocfilehash: 384f8c7fa08b69c13d05edb3404787d428dad837
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774076"
---
### <a name="stack-traces-obtained-when-using-portable-pdbs-now-include-source-file-and-line-information-if-requested"></a>휴대용 PDB를 사용할 때 가져온 스택 추적은 이제 요청된 경우 원본 파일 및 줄 정보를 포함합니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.2부터 휴대용 PDB를 사용할 때 가져온 스택 추적은 요청된 경우 원본 파일 및 줄 정보를 포함합니다. .NET Framework 4.7.2 이전 버전에서 명시적으로 요청된 경우에도 휴대용 PDB를 사용할 때 원본 파일 및 줄 정보를 사용할 수 없습니다.|
|제안 해결 방법|.NET Framework 4.7.2를 대상으로 하는 애플리케이션의 경우, 필요하지 않으면 <code>app.config</code> 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음을 추가하여 휴대용 PDB를 사용할 때 원본 파일 및 줄 정보를 옵트아웃할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Diagnostics.IgnorePortablePDBsInStackTraces=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.7.2 이상에서 실행되는 애플리케이션의 경우 <code>app.config</code> 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음을 추가하여 휴대용 PDB를 사용할 때 원본 파일 및 줄 정보를 옵트인할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Diagnostics.IgnorePortablePDBsInStackTraces=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Diagnostics.StackTrace.%23ctor(System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.StackTrace.%23ctor(System.Exception,System.Boolean)?displayProperty=nameWithType><li><xref:System.Diagnostics.StackTrace.%23ctor(System.Exception,System.Int32,System.Boolean)?displayProperty=nameWithType></li></ul>|
