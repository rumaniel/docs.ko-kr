---
ms.openlocfilehash: 19dcdf006de0bfa7c6b0a8127612a49a66a24802
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804469"
---
### <a name="tls-1x-by-default-passes-the-schsendauxrecord-flag-to-the-underlying-schannel-api"></a>기본적으로 TLS 1.x는 SCH_SEND_AUX_RECORD 플래그를 기본 SCHANNEL API에 전달

|   |   |
|---|---|
|세부 정보|TLS 1.x를 사용할 때 .NET Framework는 기본 Windows SCHANNEL API에 의존합니다. .NET Framework 4.6부터는 [SCH_SEND_AUX_RECORD](https://docs.microsoft.com/windows/desktop/api/schannel/ns-schannel-_schannel_cred) 플래그가 기본적으로 SCHANNEL로 전달됩니다. 이렇게 하면 SCHANNEL이 암호화할 데이터를 두 개의 개별 레코드로 분할합니다. 첫 번째 레코드는 단일 바이트이고 두 번째 레코드는 <em>n</em>-1 바이트입니다. 이로 인해 간혹 데이터가 단일 레코드에 있다고 가정하고 클라이언트와 기존 서버 간의 통신이 중단되기도 합니다.|
|제안|이 변경으로 인해 기존 서버와의 통신이 중단된 경우 [SCH_SEND_AUX_RECORD](https://docs.microsoft.com/windows/desktop/api/schannel/ns-schannel-_schannel_cred) 플래그 전송을 비활성화하고 앱 구성 파일의 [<](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 섹션에 있는 [<](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소에 다음 스위치를 추가하여 데이터를 별도의 레코드로 분리하지 않는 이전 동작으로 복원할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.Net.DontEnableSchSendAuxRecord=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre> <blockquote> [!IMPORTANT] 이 설정은 이전 버전과의 호환성을 위해서만 제공됩니다. 그러나 사용하지 않는 것이 좋습니다.</blockquote> |
|범위|Microsoft Edge|
|버전|4.6|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Net.Security.SslStream?displayProperty=nameWithType></li><li><xref:System.Net.ServicePointManager?displayProperty=nameWithType></li><li><xref:System.Net.Http.HttpClient?displayProperty=nameWithType></li><li><xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType></li><li><xref:System.Net.HttpWebRequest?displayProperty=nameWithType></li><li><xref:System.Net.FtpWebRequest?displayProperty=nameWithType></li></ul>|

