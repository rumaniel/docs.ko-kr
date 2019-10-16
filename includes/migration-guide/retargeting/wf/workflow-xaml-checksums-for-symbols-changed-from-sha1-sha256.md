---
ms.openlocfilehash: 9c54572b8dcedaa103db8503cfc1155b4698c3ed
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803507"
---
### <a name="workflow-xaml-checksums-for-symbols-changed-from-sha1-to-sha256"></a>SHA1에서 SHA256으로 변경된 기호에 대한 워크플로 XAML 체크섬

|   |   |
|---|---|
|세부 정보|Visual Studio로 디버깅을 지원하기 위해 워크플로 런타임은 해싱 알고리즘을 사용하여 워크플로 XAML 파일에 대한 체크섬을 생성합니다. .NET Framework 4.6.2 이전 버전에서 워크플로 체크섬 해시는 MD5 알고리즘을 사용하여 FIPS 지원 시스템에 문제가 발생했습니다. .NET Framework 4.7부터 기본 알고리즘이 SHA1로 변경되었습니다. .NET Framework 4.8부터 기본 알고리즘이 SHA256으로 변경되었습니다.|
|제안|체크섬 오류로 인해 코드가 워크플로 인스턴스를 로드할 수 없거나 적절한 기호를 찾을 수 없는 경우 <code>AppContext</code> switch &quot;Switch.System.Activities.UseSHA1HashForDebuggerSymbols&quot;를 true.In 코드로 설정합니다.<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Activities.UseSHA1HashForDebuggerSymbols&quot;, true);&#13;&#10;</code></pre>또는 다음 구성을 사용할 수도 있습니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Activities.UseSHA1HashForDebuggerSymbols=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.8|
|Type|대상 변경|

