---
ms.openlocfilehash: 14b8930044381d1d86ec7984d36a5c3588eebd81
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774034"
---
### <a name="the-default-hash-algorithm-for-wpfs-markup-compiler-is-now-sha256"></a>WPF의 마크업 컴파일러에 대한 기본 해시 알고리즘은 이제 SHA256

|   |   |
|---|---|
|세부 정보|WPF MarkupCompiler는 XAML 마크업 파일에 대한 컴파일 서비스를 제공합니다.  .NET Framework 4.7.1 및 이전 버전에서 체크섬에 사용되는 기본 해시 알고리즘은 SHA1입니다. SHA1의 최근 보안 문제로 인해 이 기본값은 .NET Framework 4.7.2부터 SHA256으로 변경되었습니다.  이 변경은 컴파일 동안 마크업 파일에 대한 모든 체크섬 생성에 영향을 미칩니다.|
|제안 해결 방법|.NET Framework 4.7.2 이상을 대상으로 하고 SHA1 해시 동작으로 되돌리려는 개발자는 다음 AppContext 플래그를 설정해야 합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Markup.DoNotUseSha256ForMarkupCompilerChecksumAlgorithm=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>.NET 4.7.2 미만 프레임워크 버전을 대상으로 하면서 SHA256 해시를 활용하려는 개발자는 아래의 AppContext 플래그를 설정해야 합니다.  .NET Framework의 설치된 버전은 4.7.2 이상이어야 합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Markup.DoNotUseSha256ForMarkupCompilerChecksumAlgorithm=false&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|투명|
|버전|4.7.2|
|형식|대상 변경|
