---
ms.openlocfilehash: a93fbbd787aa50f080337a6170cf8f56d0d24e31
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804557"
---
### <a name="concurrentqueuettrypeek-can-return-an-erroneous-null-via-its-out-parameter"></a>ConcurrentQueue\<T>.TryPeek는 out 매개 변수를 통해 잘못된 null을 반환할 수 있습니다.

|   |   |
|---|---|
|세부 정보|일부 다중 스레드 시나리오에서 <xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=name> true를 반환할 수 있지만 (올바르고 미리 본 값 대신) null 값으로 out 매개 변수를 채웁니다.|
|제안 해결 방법|이 문제는 .NET Framework 4.5.1에서 수정되었습니다. 해당 프레임워크로 업그레이드하면 문제가 해결됩니다.|
|범위|주요함|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=nameWithType></li></ul>|
