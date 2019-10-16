---
ms.openlocfilehash: 62ba525a28960d96c5458aa1481e1f319d5bc875
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859337"
---
### <a name="operationcontextcurrent-may-return-null-when-called-in-a-using-clause"></a>OperationContext.Current는 using 절에서 호출될 때 null을 반환할 수 있습니다.

|   |   |
|---|---|
|세부 정보|다음 조건이 모두 참인 경우 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType>이 <code>null</code>를 반환하고 <xref:System.NullReferenceException>이 발생할 수 있습니다.<ul><li><xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>을 반환하는 메서드에서 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> 속성 값을 검색합니다.</li><li><xref:System.ServiceModel.OperationContextScope> 개체는 <code>using</code> 절에서 인스턴스화됩니다.</li><li><code>using statement</code> 내의 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> 속성 값을 검색합니다. 예:</li></ul><pre><code class="lang-csharp">using (new OperationContextScope(OperationContext.Current))&#13;&#10;{&#13;&#10;OperationContext context = OperationContext.Current;      // OperationContext.Current is null.&#13;&#10;// ...&#13;&#10;}&#13;&#10;</code></pre>|
|제안|이 문제를 해결하려면 다음을 수행합니다.<ul><li>다음과 같이 코드를 수정하여 새로운 비-<code>null</code> <xref:System.ServiceModel.OperationContext.Current%2A> 개체를 인스턴스화합니다.</li></ul><pre><code class="lang-csharp">OperationContext ocx = OperationContext.Current;&#13;&#10;using (new OperationContextScope(OperationContext.Current))&#13;&#10;{&#13;&#10;OperationContext.Current = new OperationContext(ocx.Channel);&#13;&#10;// ...&#13;&#10;}&#13;&#10;</code></pre><ul><li>.NET Framework 4.6.2의 최신 업데이트를 설치하거나 이후 버전의 .NET Framework로 업그레이드합니다. 이렇게 하면 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType>에서 <xref:System.Threading.ExecutionContext>의 흐름이 비활성화되고 .NET Framework 4.6.1 및 이전 버전에서 WCF 애플리케이션의 동작이 복원됩니다. 이 동작은 구성할 수 있습니다. 구성 파일에 다음 앱 설정을 추가하는 것과 같습니다.</li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;Switch.System.ServiceModel.DisableOperationContextAsyncFlow&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>이러한 변경은 바람직하지 않으며 애플리케이션이 작업 컨텍스트 간에 흐르는 실행 컨텍스트에 의존하는 경우 다음과 같이 해당 흐름을 활성화할수 있습니다.<pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;Switch.System.ServiceModel.DisableOperationContextAsyncFlow&quot; value=&quot;false&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.6.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType></li></ul>|

