---
ms.openlocfilehash: 2f94ec58e6fdb56cfc5147e74b6ffd6bb657228d
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857584"
---
### <a name="itemsclear-does-not-remove-duplicates-from-selecteditems"></a>Items.Clear는 SelectedItems에서 중복 항목을 제거하지 않습니다.

|   |   |
|---|---|
|세부 정보|선택기(다중 항목 선택 가능)의 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=name> 컬렉션에 중복 항목이 있을 경우 동일한 항목이 두 번 이상 나타납니다.  데이터 소스에서 해당 항목을 제거하면(예: Items.Clear를 호출하여) <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=name> 컬렉션에서 제거할 수 없으며, 첫 번째 인스턴스만 제거됩니다. 또한 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=name>에 더 이상 데이터 소소에 없는 항목이 있기 때문에, <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=name>(예: SelectedItems.Clear())을 계속 사용하면 <xref:System.ArgumentException?displayProperty=name>과 같은 문제가 발생할 수 있습니다.|
|제안|가능한 경우 .NET Framework 4.6.2로 업그레이드하세요.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=nameWithType></li></ul>|

