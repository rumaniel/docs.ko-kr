---
ms.openlocfilehash: 51691ced3f05201f784ccdeffbc130e34748b7c1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379644"
---
### <a name="wpf-datatemplate-elements-are-now-visible-to-uia"></a>WPF DataTemplate 요소가 UIA에 표시됩니다.

|   |   |
|---|---|
|세부 정보|이전에는 <xref:System.Windows.DataTemplate?displayProperty=name> 요소가 UI 자동화에 표시되지 않았습니다. 4.5부터는 UI 자동화가 이러한 요소를 감지합니다. 이것은 대부분의 사례에 유용하지만 <xref:System.Windows.DataTemplate?displayProperty=name> 요소를 포함하지 않는 UIA 트리에 의존하는 테스트를 중단시킬 수 있습니다.|
|제안 해결 방법|이 응용 프로그램에 대한 UI 자동화 테스트는 이전에 보이지 않던 <xref:System.Windows.DataTemplate?displayProperty=name> 요소를 포함하는 UIA 트리에 대해 업데이트가 필요할 수 있습니다. 예를 들어 일부 요소가 서로 옆에 있도록 예상하는 테스트는 이제 이전에 요소 간에 보이지 않던 UIA 요소를 예상해야 할 수 있습니다. 또는 UIA 요소에 대한 특정 개수 또는 인덱스를 사용하는 테스트는 새 값으로 업데이트해야 할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Windows.DataTemplate.%23ctor?displayProperty=nameWithType></li><li><xref:System.Windows.DataTemplate.%23ctor(System.Object)?displayProperty=nameWithType></li></ul>|
