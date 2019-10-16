---
ms.openlocfilehash: eff7e7cfc8fa0b4bc8ee3a64a7c60ee21d51f466
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70997669"
---
### <a name="resizing-a-grid-can-hang"></a>눈금 크기 조정이 중지될 수 있음

|   |   |
|---|---|
|세부 정보|다음과 같은 경우 <code>T:System.Windows.Controls.Grid</code>의 레이아웃 중에 무한 루프가 발생할 수 있습니다.<ul><li>행 정의는 MinHeight 및 MaxHeight를 선언하는 두 개의 *-row를 포함합니다.</li><li>*-row의 콘텐츠가 해당 MaxHeight를 초과하지 않음</li><li>눈금의 사용 가능한 높이가 첫 번째 MinHeight(및 모든 고정 또는 자동 행)를 초과합니다.</li><li>앱이 .Net Framework 4.7을 대상으로 하거나 <code>Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=false</code>를 설정하여 4.7 할당 알고리즘으로 옵트인합니다.</li></ul>루프는 두 개가 넘는 행 또는 열의 유사한 경우에도 발생합니다. 이 문제는 .NET Framework 4.7.1에서 해결됩니다.|
|제안 해결 방법|.NET Framework 4.7.1로 업그레이드합니다.  또는 4.7 할당 알고리즘이 필요하지 않은 경우, 다음 구성 설정을 사용할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7|
|형식|런타임|
