---
ms.openlocfilehash: a29f0ca6d235250ac1f41e686178b2d6affcd8a0
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804521"
---
### <a name="calling-createdefaultauthorizationcontext-with-a-null-argument-has-changed"></a>Null 인수를 사용한 CreateDefaultAuthorizationContext 호출이 변경되었습니다.

|   |   |
|---|---|
|설명|Null authorizationPolicies를 사용하는 <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext(System.Collections.Generic.IList{System.IdentityModel.Policy.IAuthorizationPolicy})?displayProperty=name>에 대한 호출로 반환된 <xref:System.IdentityModel.Policy.AuthorizationContext?displayProperty=name>의 구현이 .NET Framework 4.6에서 변경되었습니다.|
|제안 해결 방법|드문 경우이지만 사용자 지정 인증을 사용하는 WCF 앱은 다르게 동작할 수 있습니다. 이러한 경우 두 가지 방법 중 하나로 이전 동작을 복원할 수 있습니다.<ol><li>4\.6 이전 버전의 .NET Framework를 대상으로 사용하도록 앱을 다시 컴파일합니다. IIS 호스트 서비스의 경우 .NET Framework의 이전 버전을 대상으로 하려면 &lt;httpRuntime targetFramework =&quot;x.x&quot; /&gt; 요소를 사용합니다.</li><li>다음 줄을 app.config 파일의 <code>&lt;appSettings&gt;</code> 섹션에 추가합니다. <code>&lt;add key=&quot;appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext&quot; value=&quot;true&quot; /&gt;</code></li></ol>|
|범위|부|
|버전|4.6|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext(System.Collections.Generic.IList{System.IdentityModel.Policy.IAuthorizationPolicy})?displayProperty=nameWithType></li></ul>|

