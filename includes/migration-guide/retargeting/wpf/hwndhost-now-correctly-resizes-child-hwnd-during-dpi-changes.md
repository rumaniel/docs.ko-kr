---
ms.openlocfilehash: d374ded6a29ce815beeb26505010563a26d978e8
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803536"
---
### <a name="hwndhost-now-correctly-resizes-child-hwnd-during-dpi-changes"></a>HwndHost는 이제 DPI 변경 중에 자식 HWND의 크기를 올바르게 조정합니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.2 이하 버전에서 WPF가 모니터별 인식 모드로 실행될 때 애플리케이션을 모니터 간에 이동할 때와 같이 DPI 변경 후 <xref:System.Windows.Interop.HwndHost> 내에 호스팅되는 컨트롤의 크기가 올바르게 조정되지 않았습니다. 이 수정을 통해 호스팅된 컨트롤의 크기가 적절하게 조정됩니다.|
|제안|애플리케이션이 이러한 변경에서 이점을 활용하려면 .NET Framework 4.7.2 이상에서 실행해야 하며, 다음 예제와 같이 앱 구성 파일의 <code>&lt;runtime&gt;</code> 섹션에 있는 다음 [AppContext 스위치](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)를 <code>false</code>로 설정하여 이 동작을 옵트인해야 합니다.<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.DoNotUsePresentationDpiCapabilityTier2OrGreater=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|주요함|
|버전|4.8|
|Type|대상 변경|

