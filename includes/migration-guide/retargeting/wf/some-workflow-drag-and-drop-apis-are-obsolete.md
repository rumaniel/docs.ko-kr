---
ms.openlocfilehash: 297af393e86c65e84ea7271d98eab36dbc6dbb0e
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774482"
---
### <a name="some-workflow-drag-and-drop-apis-are-obsolete"></a>일부 워크플로 끌어서 놓기 API가 사용되지 않음

|   |   |
|---|---|
|세부 정보|이 워크플로 끌어서 놓기 API는 사용되지 않으며 응용 프로그램이 4.5에 대해 다시 빌드하는 경우 컴파일러 경고가 발생합니다.|
|제안 해결 방법|여러 개체에 대한 작업을 지원하는 새 <xref:System.Activities.Presentation.DragDropHelper?displayProperty=name> API를 대신 사용해야 합니다. 또는 빌드 경고를 표시하지 않거나 이전 컴파일러를 사용하여 방지할 수 있습니다. API는 계속 지원됩니다.|
|범위|부|
|버전|4.5|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Activities.Presentation.DragDropHelper.DoDragMove(System.Activities.Presentation.WorkflowViewElement,System.Windows.Point)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetCompositeView(System.Windows.DragEventArgs)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetDraggedModelItem(System.Windows.DragEventArgs)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetDroppedObject(System.Windows.DependencyObject,System.Windows.DragEventArgs,System.Activities.Presentation.EditingContext)?displayProperty=nameWithType></li></ul>|
