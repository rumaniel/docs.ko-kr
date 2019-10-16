---
ms.openlocfilehash: b5f12e648a82ebaba7d09b546e8aa2fc7cd82a37
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803274"
---
### <a name="calling-datagridcommitedit-from-a-celleditending-handler-drops-focus"></a>CellEditEnding 처리기에서 DataGrid.CommitEdit를 호출하면 포커스가 사라집니다.

|   |   |
|---|---|
|세부 정보|<xref:System.Windows.Controls.DataGrid?displayProperty=name>의 <xref:System.Windows.Controls.DataGrid.CellEditEnding?displayProperty=name> 이벤트 처리기 중 하나에서 <xref:System.Windows.Controls.DataGrid.CommitEdit>을 호출하면 <xref:System.Windows.Controls.DataGrid?displayProperty=name>가 포커스를 잃게 됩니다.|
|제안|이 버그는 .NET Framework 4.5.2에서 수정되었으므로 .NET Framework를 업그레이드하여 방지할 수 있습니다. 또는 <xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=name>을 호출한 후에 <xref:System.Windows.Controls.DataGrid?displayProperty=name>을 명시적으로 다시 선택하여 방지할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.DataGrid.CommitEdit(System.Windows.Controls.DataGridEditingUnit,System.Boolean)?displayProperty=nameWithType></li></ul>|

