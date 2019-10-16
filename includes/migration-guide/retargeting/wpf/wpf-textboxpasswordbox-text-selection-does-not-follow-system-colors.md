---
ms.openlocfilehash: 3f88c8b80518aa65c082dc3da2d75b5221dd00f0
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774099"
---
### <a name="wpf-textboxpasswordbox-text-selection-does-not-follow-system-colors"></a>WPF TextBox/PasswordBox 텍스트 선택은 시스템 색을 따르지 않음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.1 이전 버전에서 WPF <code>System.Windows.Controls.TextBox</code> 및 <code>System.Windows.Controls.PasswordBox</code>는 표시기(Adorner) 계층에서 텍스트 선택만 렌터링할 수 있었습니다. 일부 시스템 테마에서 텍스트를 가려서 읽기 어려울 수 있습니다.  .NET Framework 4.7.2 이상 버전에서 개발자는 이 문제를 완화하는 비 표시기(Adorner) 기반 선택 렌더링 체계를 활성화하는 옵션이 있습니다.|
|제안 해결 방법|이 변경 내용을 활용하려는 개발자는 다음 AppContext 플래그를 적절하게 설정해야 합니다.  이 기능을 사용하려면 설치된 .NET Framework 버전이 4.7.2 이상이어야 합니다. 비 표시기 기반 선택을 활성화하려면 다음 AppContext 플래그를 사용합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7.2|
|형식|대상 변경|
