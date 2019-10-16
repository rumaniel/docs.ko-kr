---
ms.openlocfilehash: 12ba683655319e42368f9f2a6cf7bf70e1dbd77d
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858968"
---
### <a name="default-signedxml-and-signedxms-algorithms-changed-to-sha256"></a>기본 SignedXML 및 SignedXMS 알고리즘이 SHA256으로 변경됨

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7 이전 버전에서는 SignedXML 및 SignedCMS의 기본값이 일부 작업에서 SHA1로 설정되었습니다. .NET Framework 4.7.1부터 SHA256은 기본적으로 이러한 작업에 사용됩니다. SHA1은 더 이상 안전하지 않으므로 이 변경이 필요합니다.|
|제안 해결 방법|다음과 같이 SHA1(안전하지 않음) 또는 SHA256이 기본적으로 사용되는지 여부를 제어하는 두 가지 새로운 컨텍스트 스위치 값이 있습니다.<ul><li>Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms</li><li>Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms</li></ul>.NET Framework 4.7.1 이상 버전을 대상으로 하는 애플리케이션의 경우 SHA256 사용이 바람직하지 않으면 앱 구성 파일의 [런타임](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 섹션에 다음 구성 스위치를 추가하여 기본값을 SHA1을 기본값으로 복원할 수 있습니다.<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=true;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=true&quot; /&gt;&#13;&#10;</code></pre>.NET Framework 4.7 이전 버전을 대상으로 하는 애플리케이션의 경우 앱 구성 파일의 [런타임](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 섹션에 다음 구성 스위치를 추가하여 이 변경을 옵트인할 수 있습니다.<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=false;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=false&quot; /&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7.1|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Security.Cryptography.Pkcs.CmsSigner?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.Reference?displayProperty=nameWithType></li></ul>|

