---
ms.openlocfilehash: f1f37e61917e8331b06d91e6abebfe4ce3288e7c
ms.sourcegitcommit: 43761fcee10aeefcf851ea81cea3f3c691420856
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69564395"
---
### <a name="managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode"></a>관리형 암호화 클래스가 FIPS 모드에서 CryptographyException을 throw하지 않음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.2 이전 버전에서 <xref:System.Security.Cryptography.SHA256Managed>와 같은 관리형 암호화 공급자 클래스는 시스템 암호화 라이브러리가 FIPS 모드로 구성될 때 <xref:System.Security.Cryptography.CryptographicException>을 throw합니다. 이러한 예외는 관리형 버전이 FIPS(Federal Information Processing) 140-2 인증을 받지 않았고 FIPS 규칙에 따라 승인된 것으로 간주되지 않는 암호화 알고리즘을 차단하기 때문에 throw됩니다.  FIPS 모드에서 개발 머신을 사용하는 개발자는 거의 없기 때문에 이러한 예외는 프로덕션 시스템에서만 자주 throw됩니다. 이러한 경우 .NET Framework 4.8 이상 버전을 대상으로 하는 애플리케이션은 <xref:System.Security.Cryptography.CryptographicException>이 더 이상 기본적으로 제공되지 않도록 자동으로 최신의 완화된 정책으로 전환됩니다. 대신, 관리형 암호화 클래스는 암호화 작업을 시스템 암호화 라이브러리로 리디렉션합니다. 이 정책 변경에 따라 개발자 환경과 프로덕션 환경 간에 혼동될 수 있는 차이가 효과적으로 제거되고 네이티브 구성 요소와 관리형 구성 요소가 동일한 암호화 정책에서 작동합니다.|
|제안 해결 방법|이 동작이 바람직하지 않은 경우 애플리케이션의 구성 파일의 [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 섹션에 다음 [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 구성 설정을 추가하여 <xref:System.Security.Cryptography.CryptographicException>이(가) FIPS 모드에서 throw되도록 이전 동작을 옵트아웃하고 복원할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.UseLegacyFipsThrow=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>애플리케이션이 .NET Framework 4.7.2 이하를 대상으로 하는 경우 애플리케이션 구성 파일의 [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 섹션에 다음 [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 구성 설정을 추가하여 이 변경 내용을 옵트인할 수도 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.UseLegacyFipsThrow=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.8|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Security.Cryptography.AesManaged?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.MD5Cng?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.MD5CryptoServiceProvider?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RC2CryptoServiceProvider?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RijndaelManaged?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RIPEMD160Managed?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.SHA1Managed?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.SHA256Managed?displayProperty=nameWithType></li></ul>|
