---
ms.openlocfilehash: edd194fef27d97976f1ff45daec1cd56382bbb55
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804568"
---
### <a name="new-enum-values-in-wpfs-pagerangeselection"></a>WPF의 PageRangeSelection에 새 열거형 값

|   |   |
|---|---|
|세부 정보|두 개의 새 멤버(<xref:System.Windows.Controls.PageRangeSelection.CurrentPage?displayProperty=name> 및 <xref:System.Windows.Controls.PageRangeSelection.SelectedPages?displayProperty=name>)가 <xref:System.Windows.Controls.PageRangeSelection?displayProperty=name> 열거형에 추가되었습니다.|
|제안 해결 방법|대부분의 경우 이러한 변경은 사용자 코드에 영향을 주지 않습니다. 다만 <xref:System.Windows.Controls.PageRangeSelection?displayProperty=name> 형식의 <xref:System.Enum.GetNames(System.Type)> 또는 <xref:System.Enum.GetValues(System.Type)> 호출에 존재하는 요소의 특정 수에 종속된 코드는 수정되어야 합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Windows.Controls.PageRangeSelection?displayProperty=nameWithType></li></ul>|
