---
ms.openlocfilehash: 448a6160bd64143000c00d21a9ddecdc61b53475
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858991"
---
### <a name="serialport-background-thread-exceptions"></a>SerialPort 백그라운드 스레드 예외

|   |   |
|---|---|
|세부 정보|<xref:System.IO.Ports.SerialPort> 스트림을 사용하여 만든 백그라운드 스레드는 OS 예외가 throw될 때 더 이상 프로세스를 종료하지 않습니다. <br/>.NET Framework 4.7 및 이전 버전을 대상으로 하는 애플리케이션에서 운영 체제 예외가 <xref:System.IO.Ports.SerialPort> 스트림을 사용하여 만든 백그라운드에서 throw되면 프로세스가 종료됩니다. <br/>.NET Framework 4.7.1 또는 이상 버전을 대상으로 하는 애플리케이션에서 백그라운드 스레드는 활성 직렬 포트와 관련된 OS 이벤트에 대해 기다리며 직렬 포트의 급격한 제거와 같은 일부 경우에 충돌할 수 있습니다.|
|제안|.NET Framework 4.7.1을 대상으로 하는 앱의 경우, 필요하지 않으면 <code>app.config</code> 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음을 추가하여 예외 처리를 옵트아웃할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.Ports.DoNotCatchSerialStreamThreadExceptions=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.7.1 이상에서 실행되는 앱의 경우 <code>app.config</code> 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음 줄을 추가하여 예외 처리를 옵트인할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.Ports.DoNotCatchSerialStreamThreadExceptions=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7.1|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.IO.Ports.SerialPort?displayProperty=nameWithType></li></ul>|

