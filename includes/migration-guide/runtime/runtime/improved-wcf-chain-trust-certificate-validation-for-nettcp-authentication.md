---
ms.openlocfilehash: e69ed64390504af872fa6785aa0b7d6c4db84ef0
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69671036"
---
### <a name="improved-wcf-chain-trust-certificate-validation-for-nettcp-certificate-authentication"></a>Net.Tcp 인증서 인증에 대한 개선된 WCF 체인 신뢰 인증서 유효성 검사

|   |   |
|---|---|
|세부 정보|.NET framework 4.7.2는 WCF 전송 보안으로 인증서 인증을 사용할 때 체인 신뢰 인증서 유효성 검사를 개선합니다. 이 개선 사항으로 서버를 인증하는 데 사용되는 클라이언트 인증서는 클라이언트 인증을 위해 구성되어야 합니다.  마찬가지로 서버를 인증하기 위한 서버 인증서는 서버 인증을 위해 구성되어야 합니다. 이러한 변경으로 인해 루트 인증서가 사용할 수 없게 설정된 경우 인증서 체인 유효성 검사는 실패합니다. 동일한 변경이 Windows 보안 롤업을 통해 .NET Framework 3.5 이상 버전에도 적용됩니다. 자세한 정보는 [여기](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7)에서 찾을 수 있습니다. 이 변경은 기본적으로 활성화되어 있으며 구성 설정을 통해 해제할 수 있습니다.|
|제안 해결 방법|<ul><li>서버 및 클라이언트 인증에 EKU OID가 필수인지 유효성 검사를 합니다. 필수가 아니라면 사용자 인증을 업데이트합니다.</li><li>루트 인증서가 잘못됐는지 유효성 검사를 합니다. 잘못됐다면 루트 인증서를 업데이트합니다.</li><li>변경을 옵트아웃하는 방법: 인증서를 업데이트할 수 없는 경우 다음 구성 설정으로 호환성이 손상되는 변경을 일시적으로 해결할 수 있습니다. 그러나 변경을 옵트아웃하면 해당 시스템이 보안 문제에 취약하게 됩니다.</li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;wcf:useLegacyCertificateUsagePolicy&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7.2|
|형식|런타임|
