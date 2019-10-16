---
ms.openlocfilehash: c4b293cf7db3762831be7f3a7a355748ff5758c5
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859020"
---
### <a name="servicebase-doesnt-propagate-onstart-exceptions"></a>ServiceBase는 OnStart 예외를 전파하지 않음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7 및 이전 버전에서 서비스 시작 시 throw되는 예외는 <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType>의 호출자에게 전파되지 않습니다.<br/>.NET Framework 4.7.1을 대상으로 하는 애플리케이션을 시작으로 런타임은 시작에 실패하는 서비스에 대해 <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType>에 예외를 전파합니다.|
|제안|서비스 시작 시 예외가 있는 경우 해당 예외가 전파됩니다. 이는 서비스가 시작에 실패하는 사례를 진단하는 데 도움이 됩니다. <br/>이 동작을 원치 않을 경우 애플리케이션 구성 파일의 &lt;runtime&gt; 섹션에 다음 &lt;AppContextSwitchOverrides&gt; 요소를 추가하여 옵트아웃할 수 있습니다.<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.ServiceProcess.DontThrowExceptionsOnStart=true&quot; /&gt;&#13;&#10;</code></pre>애플리케이션이 4.7.1 이전 버전을 대상으로 하지만 이 동작을 원할 경우 애플리케이션 구성 파일의 &lt;runtime&gt; 섹션에 다음 &lt;AppContextSwitchOverrides&gt; 요소를 추가합니다.<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.ServiceProcess.DontThrowExceptionsOnStart=false&quot; /&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7.1|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.ServiceProcess.ServiceBase.Run(System.ServiceProcess.ServiceBase)?displayProperty=nameWithType></li><li><xref:System.ServiceProcess.ServiceBase.Run(System.ServiceProcess.ServiceBase[])?displayProperty=nameWithType></li></ul>|

