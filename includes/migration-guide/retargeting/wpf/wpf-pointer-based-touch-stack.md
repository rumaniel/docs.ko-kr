---
ms.openlocfilehash: a620028a4e286799a6762c57145264ac0e2dbaf9
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859122"
---
### <a name="wpf-pointer-based-touch-stack"></a>WPF 포인터 기반 터치 스택

|   |   |
|---|---|
|세부 정보|이러한 변경은 WM_POINTER 기반의 WPF 터치/스타일러스 스택 옵션을 사용할 수 있는 기능을 추가합니다.  이 기능을 명시적으로 활성화하지 않은 개발자는 WPF 터치/스타일러스 동작을 변경하지 않아야 합니다. WM_POINTER 기반 터치/스타일러스 스택 옵션과 관련하여 현재 알려진 문제점:<ul><li>실시간 잉크 기능을 지원하지 않습니다.</li><li>수동 입력 및 StylusPlugins는 계속 작동하지만 UI 스레드에서 처리되므로 성능이 저하될 수 있습니다.</li><li>터치/스타일러스 이벤트에서 마우스 이벤트로 전환하는 방식의 변경으로 인해 동작 변경</li><li>조작이 다르게 동작할 수 있습니다.</li><li>끌어서 놓기 작업이 터치 입력에 대해 적절한 피드백을 표시하지 않습니다.</li><li>이러한 문제가 스타일러스 입력에는 영향을 주지 않습니다.</li><li>끌어서 놓기가 더 이상 터치/스타일러스 이벤트에서 시작될 수 없습니다.</li><li>이로 인해 마우스 입력이 감지될 때까지 애플리케이션이 중단될 수 있습니다.</li><li>대신, 개발자는 마우스 이벤트에서 끌어서 놓기를 시작하는 것이 좋습니다.</li></ul>|
|제안|이 스택을 사용하도록 설정하려는 개발자는 애플리케이션의 App.config 파일에 다음을 추가/병합할 수 있습니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Input.Stylus.EnablePointerSupport=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>이것을 제거하거나 값을 false로 설정하면 이 스택 옵션이 꺼집니다. 이 스택은 Windows 10 크리에이터스 이상에서만 사용할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.7|
|형식|대상 변경|

