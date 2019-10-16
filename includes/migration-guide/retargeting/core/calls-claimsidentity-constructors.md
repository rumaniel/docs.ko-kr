---
ms.openlocfilehash: 7848b9a15c34e40c33495c31bd942e93c522cbdb
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859245"
---
### <a name="calls-to-claimsidentity-constructors"></a>ClaimsIdentity 생성자 호출

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2부터는 <xref:System.Security.Principal.IIdentity?displayProperty=name> 매개 변수로 <xref:System.Security.Claims.ClaimsIdentity> 생성자가 <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=name> 속성을 설정하는 방법이 변경되었습니다. <xref:System.Security.Principal.IIdentity?displayProperty=name> 인수가 <xref:System.Security.Claims.ClaimsIdentity> 개체이고 해당 <xref:System.Security.Claims.ClaimsIdentity> 개체의 <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=name> 속성이 <code>null</code>이 아닌 경우 <xref:System.Security.Claims.ClaimsIdentity.Clone> 메서드를 사용하여 <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=name> 속성이 연결됩니다. Framework 4.6.1 이전 버전에서 <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=name> 속성은 기존 참조로 첨부됩니다. 이 변경으로 인해 .NET Framework 4.6.2부터는 새 <xref:System.Security.Claims.ClaimsIdentity> 개체의 <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=name> 속성이 생성자의 <xref:System.Security.Principal.IIdentity?displayProperty=name> 인수의 <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=name> 속성과 같지 않습니다. .NET Framework 4.6.1 이전 버전에서는 이 속성이 같습니다.|
|제안|이 동작을 원치 않을 경우 애플리케이션 구성 파일에서 <code>Switch.System.Security.ClaimsIdentity.SetActorAsReferenceWhenCopyingClaimsIdentity</code> 스위치를 <code>true</code>로 설정하여 이전 동작을 복원할 수 있습니다. 이렇게 하려면 web.config 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음을 추가해야 합니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.ClaimsIdentity.SetActorAsReferenceWhenCopyingClaimsIdentity=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.6.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Security.Principal.IIdentity)?displayProperty=nameWithType></li><li><xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Security.Principal.IIdentity,System.Collections.Generic.IEnumerable{System.Security.Claims.Claim})?displayProperty=nameWithType></li><li><xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Security.Principal.IIdentity,System.Collections.Generic.IEnumerable{System.Security.Claims.Claim},System.String,System.String,System.String)?displayProperty=nameWithType></li></ul>|

