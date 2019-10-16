---
ms.openlocfilehash: c9efbefc2bce9e21f328680795e72b62bfcd5cbd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379594"
---
### <a name="enumerableemptytresult-always-returns-cached-instance"></a>Enumerable.Empty\<TResult>가 항상 캐시된 인스턴스를 반환

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터 <xref:System.Linq.Enumerable.Empty%60%601>는 항상 캐시된 내부 인스턴스 <xref:System.Collections.Generic.IEnumerable%601>를 반환합니다. 이전에는 <xref:System.Linq.Enumerable.Empty%60%601>이 API를 호출할 때 빈 <xref:System.Collections.Generic.IEnumerable%601>을 캐시했으며, 이 말은 즉 <xref:System.Linq.Enumerable.Empty%60%601>가 신속하게 동시에 호출된 일부 조건에서 다른 형식의 인스턴스가 다른 호출에 대해 API로 반환되었다는 것입니다.|
|제안 해결 방법|이전 동작이 명확하지 않았으므로 코드가 종속될 가능성이 작습니다. 그러나 빈 열거형은 비교되고 때로는 같지 않은 것으로 예상되는 드문 경우에는, <xref:System.Linq.Enumerable.Empty%60%601>를 사용하는 대신 명시적인 빈 배열을 만들어야 합니다(<code>new T[0]</code>).|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Linq.Enumerable.Empty%60%601?displayProperty=nameWithType></li></ul>|
