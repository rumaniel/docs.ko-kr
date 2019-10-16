---
ms.openlocfilehash: f007a2b81820a1d25a2d101b35f3a49e7794fec1
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859112"
---
### <a name="workflow-checksums-changed-from-md5-to-sha1"></a>워크플로 체크섬이 MD5에서 SHA1로 변경됨

|   |   |
|---|---|
|설명|Visual Studio로 디버깅을 지원하기 위해 워크플로 런타임은 해싱 알고리즘을 사용하여 워크플로 인스턴스에 대한 체크섬을 생성합니다. .NET Framework 4.6.2 이전 버전에서 워크플로 체크섬 해시는 MD5 알고리즘을 사용하여 FIPS 지원 시스템에 문제가 발생했습니다. .NET Framework 4.7부터 알고리즘은 SHA1입니다. 코드가 이러한 체크섬을 지속하면 호환되지 않습니다.|
|제안 해결 방법|체크섬 오류로 인해 코드가 워크플로 인스턴스를 로드할 수 없는 경우 <code>AppContext</code> switch &quot; Switch.System.Activities.UseMD5ForWFDebugger &quot;을 true.In code로 설정합니다.<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Activities.UseMD5ForWFDebugger&quot;, true);&#13;&#10;</code></pre>또는 다음 구성을 사용할 수도 있습니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Activities.UseMD5ForWFDebugger=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7|
|형식|대상 변경|

