---
ms.openlocfilehash: d4859629fe3922b71cc90664e1e3304cdb312bae
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59235597"
---
### <a name="listsort-algorithm-changed"></a>List.Sort 알고리즘 변경

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터 <xref:System.Collections.Generic.List%601?displayProperty=name>의 정렬 알고리즘이 변경되었습니다(빠른 정렬 대신 내면적인 정렬). <xref:System.Collections.Generic.List%601?displayProperty=name>의 정렬은 안정적이지 않았지만 이 변경으로 인해 다양한 시나리오가 불안정하게 정렬될 수 있습니다. 즉, API의 후속 호출에서 동일한 항목이 다른 순서로 정렬될 수 있습니다.|
|제안 해결 방법|이전 정렬 알고리즘은 불안정했기 때문에(약간 다른 방식이지만) 항상 특정 순서로 정렬하는 해당 항목에 종속된 코드가 없어야 합니다. 이에 종속된 코드의 인스턴스가 있고 이전 동작에 운이 따른다면 원하는 순서로 항목을 명확하게 정렬하는 비교자를 사용하도록 해당 코드를 업데이트해야 합니다.|
|범위|투명|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Collections.Generic.List%601.Sort?displayProperty=nameWithType></li><li><xref:System.Collections.Generic.List%601.Sort(System.Collections.Generic.IComparer{%600})?displayProperty=nameWithType></li><li><xref:System.Collections.Generic.List%601.Sort(System.Comparison{%600})?displayProperty=nameWithType></li><li><xref:System.Collections.Generic.List%601.Sort(System.Int32,System.Int32,System.Collections.Generic.IComparer{%600})?displayProperty=nameWithType></li></ul>|
