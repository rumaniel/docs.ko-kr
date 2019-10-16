---
ms.openlocfilehash: bc33266bb2af639d7d0d1cb532ed73abd7f1ba9a
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803247"
---
### <a name="ef-no-longer-throws-for-queryviews-with-specific-characteristics"></a>EF는 더 이상 특정 특성을 가진 Queryview를 throw하지 않습니다.

|   |   |
|---|---|
|세부 정보|관련 엔터티를 쿼리의 일부로 포함시키려는 0..1 탐색 속성이 포함된 QueryView와 관련된 쿼리를 앱에서 실행하는 경우 Entity Framework가 더 이상 <xref:System.StackOverflowException?displayProperty=name> 예외를 throw하지 않습니다. 예를 들어 <code>.Include(e =&gt; e.RelatedNavProp)</code>를 호출합니다.|
|제안|이러한 변경은 .Include를 호출하는 쿼리를 실행할 때 1-0..1 관계가 있는 QueryView를 사용하는 코드에만 영향을 줍니다. 이 변경으로 인해 안정성이 향상되며 거의 모든 앱에는 영향을 주지 않습니다. 하지만 이 변경으로 예기치 않은 동작이 발생하면 다음 항목을 앱 구성 파일의 <code>&lt;appSettings&gt;</code> 섹션에 추가하여 이 기능을 비활성화할 수 있습니다.<pre><code class="lang-xml">&lt;add key=&quot;EntityFramework_SimplifyUserSpecifiedViews&quot; value=&quot;false&quot; /&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.5.2|
|형식|런타임|

