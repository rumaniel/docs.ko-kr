---
ms.openlocfilehash: 72f907c117748fb19ca0663f24445a8c978afd32
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68235489"
---
### <a name="cspparametersparentwindowhandle-now-expects-hwnd-value"></a>이제 CspParameters.ParentWindowHandle에 HWND 값 필요

|   |   |
|---|---|
|세부 정보|.NET Framework 2.0에 도입된 <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle> 값을 사용하면 애플리케이션에서 키에 액세스하는 데 필요한 UI(PIN 프롬프트 또는 동의 대화 상자)가 지정된 창에 대한 모달 자식 항목으로 열리도록 부모 창 핸들 값을 등록할 수 있습니다. .NET Framework 4.7을 대상으로 하는 앱부터 Windows Forms 애플리케이션은 다음과 같은 코드로 <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle> 속성을 설정할 수 있습니다.<pre><code class="lang-csharp">cspParameters.ParentWindowHandle = form.Handle;&#13;&#10;</code></pre>이전 버전의 .NET Framework에서 값은 [HWND](https://docs.microsoft.com/windows/desktop/WinProg/windows-data-types#HWND) 값이 있던 메모리의 위치를 나타내는 <xref:System.IntPtr?displayProperty=name>가 있어야 합니다. Windows 7 이전 버전에서 이 속성을 form.Handle로 설정해도 아무 영향이 없지만, Windows 8 이상 버전에서는 &quot;<xref:System.Security.Cryptography.CryptographicException?displayProperty=name>: 매개 변수가 잘못되었습니다.&quot;라는 메시지가 표시됩니다.|
|제안 해결 방법|부모 창 관계를 등록하려는 .NET Framework 4.7 이상을 대상으로 하는 애플리케이션에서는 다음과 같은 간단한 형식을 사용하는 것이 좋습니다.<pre><code class="lang-csharp">cspParameters.ParentWindowHandle = form.Handle;&#13;&#10;</code></pre>통과시킬 올바른 값이 <code>form.Handle</code> 값을 가졌던 메모리 위치의 주소임을 확인한 사용자는 AppContext 스위치 <code>Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle</code>를 <code>true</code>로 설정하여 동작 변경을 옵트아웃할 수 있습니다.<ol><li>[여기](https://devblogs.microsoft.com/dotnet/net-announcements-at-build-2015/#dotnet46)에 설명된 대로 AppContext에서 compat 스위치를 프로그래밍 방식으로 설정합니다.</li><li>다음 줄을 app.config 파일의 <code>&lt;runtime&gt;</code> 섹션에 추가</li></ol><pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>반대로 이전 버전의 .NET Framework에서 애플리케이션이 로드될 때 .NET Framework 4.7 런타임에서 새로운 동작을 옵트인하려는 사용자는 AppContext 스위치를 <code>false</code>로 설정할 수 있습니다.|
|범위|부|
|버전|4.7|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Security.Cryptography.CspParameters.ParentWindowHandle?displayProperty=nameWithType></li></ul>|
