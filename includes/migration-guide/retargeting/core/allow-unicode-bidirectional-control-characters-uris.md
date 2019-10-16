---
ms.openlocfilehash: 3e9a1009167d8a765bc401d64a574bd123736ccd
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774060"
---
### <a name="allow-unicode-bidirectional-control-characters-in-uris"></a>URI에서 유니코드 양방향 컨트롤 문자 허용

|   |   |
|---|---|
|세부 정보|유니코드는 텍스트의 방향을 지정하는 데 사용되는 몇 가지 특수 컨트롤 문자를 지정합니다. 이전 버전의 .NET Framework에서 이러한 문자는 백분율로 인코딩된 형식으로 존재했더라도 모든 URI에서 올바르지 않게 제거되었습니다. [RFC 3987](https://tools.ietf.org/html/rfc3987)을 더 잘 따르기 위해 이제 URI에서 이러한 문자를 허용합니다. URI에서 인코딩되지 않은 것을 발견한 경우 백분율로 인코딩됩니다. 백분율로 인코딩된 것을 발견한 경우 그대로 유지됩니다.|
|제안 해결 방법|4.7.2 이상의 .NET Framework 버전을 대상으로 하는 애플리케이션의 경우 유니코드 양방향 문자에 대한 지원이 기본적으로 활성화됩니다. 이 변경을 원치 않는 경우 다음 [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 스위치를 애플리케이션 구성 파일의 <code>&lt;runtime&gt;</code> 섹션에 추가하여 비활성화할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Uri.DontKeepUnicodeBidiFormattingCharacters=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.7.2 이상 버전에서 실행되는 애플리케이션의 경우 유니코드 양방향 문자에 대한 지원이 기본적으로 비활성화됩니다. 다음 [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 스위치를 애플리케이션 구성 파일의 <code>&lt;runtime&gt;</code> 섹션에 추가하여 활성화할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Uri.DontKeepUnicodeBidiFormattingCharacters=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Uri?displayProperty=nameWithType></li></ul>|
