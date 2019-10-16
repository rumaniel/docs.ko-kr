---
ms.openlocfilehash: 824d75585efd40937c1a48376ec7862cba1a8fa3
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68235565"
---
### <a name="nullreferenceexception-in-exception-handling-code-from-imagesourceconverterconvertfrom"></a>ImageSourceConverter.ConvertFrom의 예외 처리 코드에서 NullReferenceException이 발생

|   |   |
|---|---|
|세부 정보|<xref:System.Windows.Media.ImageSourceConverter.ConvertFrom(System.ComponentModel.ITypeDescriptorContext,System.Globalization.CultureInfo,System.Object)>에 대한 예외 처리 코드의 오류로 인해 의도한 예외(<xref:System.IO.DirectoryNotFoundException?displayProperty=name> 또는 <xref:System.IO.FileNotFoundException?displayProperty=name>) 대신 잘못된 <xref:System.NullReferenceException?displayProperty=name>이 throw됩니다. 이제 해당 오류를 수정하여 메서드에서 올바른 예외를 throw하도록 변경되었습니다. <p/>기본적으로 .NET Framework 4.6.2 및 이전 버전을 대상으로 하는 모든 애플리케이션은 호환성을 위해 계속 <xref:System.NullReferenceException?displayProperty=name>을 throw합니다. .NET Framework 4.7 이상을 대상으로 하는 개발자는 올바른 예외를 확인해야 합니다.|
|제안 해결 방법|.NET Framework 4.7 이상을 대상으로 할 때 <xref:System.NullReferenceException?displayProperty=name>을 가져오기 위해 되돌리려는 개발자는 애플리케이션의 App.config 파일에 다음을 추가/병합할 수 있습니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Media.ImageSourceConverter.OverrideExceptionWithNullReferenceException=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Windows.Media.ImageSourceConverter.ConvertFrom(System.ComponentModel.ITypeDescriptorContext,System.Globalization.CultureInfo,System.Object)?displayProperty=nameWithType></li></ul>|
