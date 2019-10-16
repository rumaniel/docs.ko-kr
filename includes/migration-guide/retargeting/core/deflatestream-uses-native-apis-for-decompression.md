---
ms.openlocfilehash: 897bb0b0650c633b87a792516c62566f491ec3fd
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59234062"
---
### <a name="deflatestream-uses-native-apis-for-decompression"></a>DeflateStream은 압축 풀기에 네이티브 API를 사용합니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.2부터 <code>T:System.IO.Compression.DeflateStream</code> 클래스에서 압축 풀기의 구현은 기본적으로 네이티브 Windows API를 사용하는 것으로 변경되었습니다. 일반적으로 이로 인해 성능이 크게 향상됩니다. .NET Framework 버전 4.7.2 이상을 대상으로 하는 모든 .NET 애플리케이션은 네이티브 구현을 사용합니다. 이 변경 내용으로 인해 다음을 포함하여 동작에 일부 차이점이 발생할 수 있습니다.<ul><li>예외 메시지는 달라질 수 있습니다. 그러나 throw된 예외의 형식은 유지됩니다.</li><li>작업을 완료하는 데 메모리가 충분하지 않은 것과 같은 일부 특수한 상황은 다르게 처리될 수 있습니다.</li><li>gzip 헤더를 구문 분석하는 데 알려진 차이점이 있습니다(참고: 압축 풀기에 대한 <code>GZipStream</code> 설정만 영향을 받음).</li><li>잘못된 헤더를 구분 분석하는 경우 예외는 서로 다른 시간에 throw될 수 있습니다.</li><li>네이티브 구현은 gzip 헤더 내부의 일부 예약된 플래그에 대한 값(즉, [FLG](http://www.zlib.org/rfc-gzip.html#header-trailer))이 사양에 따라 설정되도록 적용합니다. 이로 인해 이전에 잘못된 값이 무시되었던 예외를 throw할 수 있습니다.</li></ul>|
|제안 해결 방법|네이티브 API를 사용하는 압축 풀기가 앱의 동작에 부정적으로 영향을 준 경우 app.config 파일의 <code>runtime</code> 섹션에 <code>Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression</code> 스위치를 추가하고 <code>true</code>로 설정하여 이 기능을 옵트아웃할 수 있습니다.<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot; ?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|부|
|버전|4.7.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.IO.Compression.DeflateStream?displayProperty=nameWithType></li><li><xref:System.IO.Compression.GZipStream?displayProperty=nameWithType></li></ul>|
