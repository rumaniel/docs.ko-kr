---
ms.openlocfilehash: f672645fb98f511f7e1326c9c584b287a0fae7dc
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859318"
---
### <a name="long-path-support"></a>긴 경로 지원

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2를 대상으로 하는 앱부터 긴 경로(최대 32K자)가 지원되고 260자(또는 <code>MAX_PATH</code>)의 경로 길이 제한이 제거되었습니다. .NET Framework 4.6.2를 대상으로 다시 컴파일된 앱의 경우, 이전에는 260자를 초과했기 때문에 <xref:System.IO.PathTooLongException?displayProperty=name>을 throw했던 코드 경로는 이제 다음 조건에서만 <xref:System.IO.PathTooLongException?displayProperty=name>을 throw합니다.<ul><li>경로의 길이가 <xref:System.Int16.MaxValue>(32,767)자보다 긴 경우</li><li>운영 체제가 <code>COR_E_PATHTOOLONG</code> 또는 동급을 반환하는 경우</li></ul>.NET Framework 4.6.1 이하 버전을 대상으로 하는 앱의 경우, 경로가 260자를 초과할 때마다 런타임에서 자동으로 <xref:System.IO.PathTooLongException?displayProperty=name>을 throw합니다.|
|제안|.NET Framework 4.6.2를 대상으로 하는 앱의 경우, 필요하지 않으면 <code>app.config</code> 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음을 추가하여 긴 경로 지원을 옵트아웃할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.6.2 이상에서 실행되는 앱의 경우 <code>app.config</code> 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음 줄을 추가하여 긴 경로 지원을 옵트인할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.6.2|
|형식|대상 변경|

