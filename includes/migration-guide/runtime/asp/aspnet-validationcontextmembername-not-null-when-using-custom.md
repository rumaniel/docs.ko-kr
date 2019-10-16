---
ms.openlocfilehash: 3b94c88809513e31a5f226bcfce39abbfa4de378
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70017374"
---
### <a name="aspnet-validationcontextmembername-is-not-null-when-using-custom-dataannotationsvalidationattribute"></a>사용자 지정 DataAnnotations.ValidationAttribute를 사용할 때 ASP.NET ValidationContext.MemberName은 NULL이 아닙니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.2 이하 버전에서 사용자 지정 <xref:System.ComponentModel.DataAnnotations.ValidationAttribute?displayProperty=nameWithType>을 사용할 때 <xref:System.ComponentModel.DataAnnotations.ValidationContext.MemberName?displayProperty=nameWithType> 속성이 <code>null</code>를 반환합니다.  .NET Framework 4.8에서는 멤버 이름을 반환합니다.|
|제안 해결 방법|이전 동작을 복원하려면 다음 설정을 앱 구성 파일에 추가합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appSettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;aspnet:GetValidationMemberName&quot;  value=&quot;true&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appSettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>이 동작은 새 동작을 명시적으로 선택해야 하는 경우 향후 서비스 릴리스에서 변경됩니다. 이 속성은 `aspnet:GetValidationMemberName` 스위치가 `true`로 설정된 경우 사용자 지정 `ValidationAttribute`에 대해 null이 아닌 값을 반환합니다.|
|범위|알 수 없음|
|버전|4.8|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.ComponentModel.DataAnnotations.ValidationContext.MemberName?displayProperty=nameWithType></li></ul>|
