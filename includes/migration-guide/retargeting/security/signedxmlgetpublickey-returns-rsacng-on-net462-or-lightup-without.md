---
ms.openlocfilehash: 52693beada7b301e62414e38cef523226ee9c044
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859042"
---
### <a name="signedxmlgetpublickey-returns-rsacng-on-net462-or-lightup-without-retargeting-change"></a>SignedXml.GetPublicKey는 대상 변경 없이 net462(또는 lightup)에서 RSACng를 반환

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2부터는 <xref:System.Security.Cryptography.Xml.SignedXml.GetPublicKey%2A?displayProperty=nameWithType> 메서드에서 반환된 개체의 구체적인 형식이 CryptoServiceProvider 구현에서 Cng 구현으로 변경되었습니다(쿼크 사용 안 함). 이는 구현이 <code>certificate.PublicKey.Key</code> 사용에서 <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey%2A?displayProperty=nameWithType>로 전달되는 내부 <code>certificate.GetAnyPublicKey</code> 사용으로 변경 되었기 때문입니다.|
|제안|.NET Framework 4.7.1에서 실행되는 앱부터는 앱 구성 파일의 [런타임](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 섹션에 다음 구성 스위치를 추가하여 .NET Framework 4.6.1 이전 버전에서 기본적으로 사용되는 CryptoServiceProvider 구현을 사용할 수 있습니다.<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.Xml.SignedXmlUseLegacyCertificatePrivateKey=true&quot; /&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.6.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Security.Cryptography.Xml.SignedXml.CheckSignatureReturningKey(System.Security.Cryptography.AsymmetricAlgorithm@)?displayProperty=nameWithType></li></ul>|

