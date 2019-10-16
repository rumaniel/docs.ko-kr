---
ms.openlocfilehash: cce19d6c9afa5f5ce9bb17b5b5d92f2060a08414
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804453"
---
### <a name="currentculture-is-not-preserved-across-wpf-dispatcher-operations"></a>CurrentCulture는 WPF 발송자 작업 간에 유지되지 않습니다.

|   |   |
|---|---|
|설명|.NET Framework 4.6부터, <xref:System.Windows.Threading.Dispatcher?displayProperty=name> 내에서 수행된 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 또는 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>에 대한 변경 내용은 해당 디스패처 작업이 끝날 때 손실됩니다. 마찬가지로, 디스패처 작업 외부에서 수행된 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 또는 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>의 변경 내용은 해당 작업이 실행될 때 반영되지 않을 수 있습니다. 실제로 이는 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 및 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name> 변경 내용이 WPF UI 콜백과 WPF 애플리케이션의 다른 코드 간에 흐르지 않을 수 있음을 의미합니다. 이는 .NET Framework 4.6을 대상으로 하는 앱부터 <xref:System.Threading.ExecutionContext?displayProperty=name>이 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 및 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>을 실행 컨텍스트에 저장하도록 변경되었기 때문입니다. WPF 발송자 작업이 작업을 시작할 때 사용된 실행 컨텍스트를 저장하고 작업이 완료되면 이전의 컨텍스트를 복원합니다. 이제는 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 및 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>가 해당 컨텍스트의 일부이므로 발송자 작업 내의 해당 속성 변경 내용이 작업 외부에서 유지되지 않습니다.|
|제안 해결 방법|이 변경의 영향을 받는 앱은 원하는 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 또는 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>를 필드에 저장하고 올바른 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name> 및 <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>가 설정되도록 모든 디스패처 작업 본문(UI 이벤트 콜백 처리기 포함)을 확인하여 문제를 해결할 수 있습니다. 또는 이 WPF 변경 내용에 기반을 둔 ExecutionContext 변경 내용이 .NET Framework 4.6 이상을 대상으로 하는 앱에만 영향을 주기 때문에 대상을 .NET Framework 4.5.2로 변경하면 이 문제를 방지할 수 있습니다. 또한 .NET Framework 4.6 이상을 대상으로 하는 앱은 다음 호환성 스위치를 설정하여 이 문제를 해결할 수도 있습니다.<pre><code class="lang-csharp">AppContext.SetSwitch(&quot;Switch.System.Globalization.NoAsyncCurrentCulture&quot;, true);&#13;&#10;</code></pre>이 문제는 .NET Framework 4.6.2의 WPF에서 해결되었습니다. 또한 [KB 3139549](https://support.microsoft.com/kb/3139549)를 통해 .NET Frameworks 4.6, 4.6.1에서 해결되었습니다. .NET Framework 4.6 이상을 대상으로 하는 애플리케이션은 디스패처 작업 전반에 걸쳐 WPF 애플리케이션(<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=name>/<xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=name>)에서 올바른 동작을 자동으로 유지합니다.|
|범위|부|
|버전|4.6|
|형식|대상 변경|

