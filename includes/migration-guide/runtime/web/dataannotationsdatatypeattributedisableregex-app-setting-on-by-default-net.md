---
ms.openlocfilehash: fe6ff59066c9e6bcf5387e7c266c879b8ae173c6
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68237669"
---
### <a name="dataannotationsdatatypeattributedisableregex-app-setting-is-on-by-default-in-net-framework-472"></a>"dataAnnotations:dataTypeAttribute:disableRegEx" 앱 설정은 .NET Framework 4.7.2에서 기본적으로 설정됩니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.1에서는 사용자가 데이터 형식 특성(예: <xref:System.ComponentModel.DataAnnotations.EmailAddressAttribute?displayProperty=nameWithType>, <xref:System.ComponentModel.DataAnnotations.UrlAttribute?displayProperty=nameWithType> 및 <xref:System.ComponentModel.DataAnnotations.PhoneAttribute?displayProperty=nameWithType>)에서 정규식을 사용하지 않도록 설정할 수 있는 앱 설정(<code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code>)이 도입되었습니다. 이는 특정 정규식을 사용하여 서비스 거부 공격 회피와 같이 보안 취약점을 줄이는 데 도움이 됩니다.<br/>.NET Framework 4.6.1에서는 RegEx를 사용하지 않도록 설정된 이 앱은 기본적으로 <code>false</code>로 설정되었습니다. .NET Framework 4.7.2부터 .NET Framework 4.7.2 이상을 대상으로 하는 웹 애플리케이션의 보안 취약성을 더 줄이기 위해 이 구성 스위치는 기본적으로 <code>true</code>로 설정됩니다.|
|제안 해결 방법|.NET Framework 4.7.2로 업그레이드한 후 웹 애플리케이션의 정규식이 작동하지 않는 것으로 확인된 경우, <code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code> 설정 값을 <code>false</code>로 업데이트하여 이전 동작으로 되돌릴 수 있습니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appSettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot; value=&quot;false&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appSettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7.2|
|형식|런타임|
