---
ms.openlocfilehash: de40d16dbb5e7a7a49ae0988342b3eb75bc078c5
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804528"
---
### <a name="currentculture-and-currentuiculture-flow-across-tasks"></a>CurrentCulture 및 CurrentUICulture가 작업에 걸쳐 전달됨

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6부터 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 및 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>은 스레드의 <xref:System.Threading.ExecutionContext?displayProperty=name>에 저장되며 비동기 작업을 통해 전달됩니다. 즉, <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 또는 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>의 변경은 이후 비동기적으로 실행되는 작업에서 반영됩니다. 이는 모든 비동기 작업에서 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 및 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>을 다시 설정하는 이전 .NET Framework 버전의 동작과 다릅니다.|
|제안|이 변경의 영향을 받는 앱은 비동기 작업에서 원하는 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 또는 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>을 첫 번째 작업으로 명확하게 설정하여 문제를 해결할 수 있습니다. 또는 다음 호환성 스위치를 설정하여 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name>/<xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>을 전달하지 않는 이전 동작을 옵트인할 수 있습니다.<pre><code class="lang-csharp">AppContext.SetSwitch(&quot;Switch.System.Globalization.NoAsyncCurrentCulture&quot;, true);&#13;&#10;</code></pre>이 문제는 .NET Framework 4.6.2의 WPF에서 해결되었습니다. 또한 [KB 3139549](https://support.microsoft.com/kb/3139549)를 통해 .NET Frameworks 4.6, 4.6.1에서 해결되었습니다. .NET Framework 4.6 이상을 대상으로 하는 애플리케이션은 디스패처 작업 전반에 걸쳐 WPF 애플리케이션(<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name>/<xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>)에서 올바른 동작을 자동으로 유지합니다.|
|범위|부|
|버전|4.6|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=nameWithType></li><li><xref:System.Threading.Thread.CurrentCulture?displayProperty=nameWithType></li><li><xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=nameWithType></li><li><xref:System.Threading.Thread.CurrentUICulture?displayProperty=nameWithType></li></ul>|

