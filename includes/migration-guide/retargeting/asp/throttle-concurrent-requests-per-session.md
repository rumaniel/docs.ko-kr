---
ms.openlocfilehash: db8eb017bdf166b0f1a241f5a8f7db9b9430898a
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859081"
---
### <a name="throttle-concurrent-requests-per-session"></a>세션당 동시 요청 수 조절

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2 이전 버전에서 ASP.NET은 같은 Sessionid를 사용하여 요청을 순차적으로 실행하고, ASP.NET은 항상 기본적으로 쿠키를 통해 Sessionid를 발급합니다. 페이지가 응답하는 데 시간이 오래 걸릴 때 브라우저에서 F5 키를 누르면 서버 성능이 크게 저하됩니다. 수정 사항에서는 카운터를 추가하여 큐에 대기 중인 요청을 추적하고 지정된 한도를 초과할 때 요청을 종료합니다. 기본값은 50입니다. 이 한도에 도달하면 이벤트 로그에 경고가 기록되고 HTTP 500 응답이 IIS 로그에 기록될 수 있습니다.|
|제안|이전 동작을 복원하려면 web.config 파일에 다음 설정을 추가하여 새 동작을 옵트아웃(opt out)할 수 있습니다.<pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;aspnet:RequestQueueLimitPerSession&quot; value=&quot;2147483647&quot;/&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7|
|형식|대상 변경|

