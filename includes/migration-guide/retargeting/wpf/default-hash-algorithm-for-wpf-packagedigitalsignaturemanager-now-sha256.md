---
ms.openlocfilehash: 745e880db08c5fa7e5514a71758f7fbb042e7ef4
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858939"
---
### <a name="the-default-hash-algorithm-for-wpf-packagedigitalsignaturemanager-is-now-sha256"></a>WPF PackageDigitalSignatureManager의 기본 해시 알고리즘은 이제 SHA256입니다.

|   |   |
|---|---|
|세부 정보|<code>System.IO.Packaging.PackageDigitalSignatureManager</code>는 WPF 패키지와 관련하여 디지털 서명을 위한 기능을 제공합니다.  .NET Framework 4.7 및 이전 버전에서 패키지 서명 부분에 사용되는 기본 알고리즘(<xref:System.IO.Packaging.PackageDigitalSignatureManager.DefaultHashAlgorithm?displayProperty=nameWithType>)은 SHA1입니다.  SHA1의 최근 보안 문제로 인해 이 기본값은 .NET Framework 4.7.1부터 SHA256으로 변경되었습니다.  이 변경 내용은 XPS 문서를 포함한 모든 패키지 서명에 영향을 줍니다.|
|제안|.NET Framework 4.7.1 미만의 프레임워크 버전을 대상으로 하며 이 변경 내용을 활용하려는 개발자 또는 .NET Framework 4.7.1 이상을 대상으로 하며 이전 기능을 필요로 하는 개발자는 다음 AppContext 플래그를 적절하게 설정할 수 있습니다.  true 값을 지정하면 SHA1이 기본 알고리즘으로 사용됩니다. false를 지정하면 SHA256이 사용됩니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.MS.Internal.UseSha1AsDefaultHashAlgorithmForDigitalSignatures=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7.1|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.IO.Packaging.PackageDigitalSignatureManager.DefaultHashAlgorithm?displayProperty=nameWithType></li></ul>|

