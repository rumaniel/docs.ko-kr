---
ms.openlocfilehash: 4eac93d5cfea19cb83c66cd3fe35c1b0703c0cc0
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59234039"
---
### <a name="wpf-focusvisual-for-radiobutton-and-checkbox-now-displays-correctly-when-the-controls-have-no-content"></a>RadioButton 및 CheckBox용 WPF FocusVisual은 컨트롤이 콘텐츠가 없을 경우 올바르게 표시됨

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.1 및 이전 버전에서 WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWIthType> 및 <xref:System.Windows.Controls.RadioButton?displayProperty=nameWIthType>에는 일치하지 않는, 그리고 기본 및 고대비 테마에서는 잘못된 포커스 시각적 개체가 있습니다.  이러한 문제는 컨트롤에 아무 콘텐츠 집합도 없는 경우 발생합니다.  이렇게 하면 테마 혼동 및 포커스 시각적 개체 간 전환을 보기 어렵게 할 수 있습니다. NET Framework 4.7.2에서 이러한 시각적 개체는 이제 테마에서 더욱 일관적이고 기본 및 고대비 테마에서 더욱 쉽게 볼 수 있습니다.|
|제안 해결 방법|.NET 4.7.1에서 동작을 되돌리려는 .NET Framework 4.7.2를 대상으로 하는 개발자는 다음 AppContext 플래그를 설정해야 합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures.2=true;&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>.NET 4.7.2 미만 프레임워크 버전을 대상으로 하면서 이 변경을 활용하려는 개발자는 다음 AppContext 플래그를 설정해야 합니다. 모든 플래그를 적절하게 설정해야 하며 설치된 .NET Framework 버전은 4.7.2 이상이어야 합니다. WPF 애플리케이션이 최신 기능 향상을 가져오려면 모든 이전 접근성 향상을 옵트인할 것을 요구합니다. 이러려면 AppContext 스위치 'Switch.UseLegacyAccessibilityFeatures' 및 'Switch.UseLegacyAccessibilityFeatures.2' 모두가 False로 설정됐는지 확인합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7.2|
|형식|대상 변경|
