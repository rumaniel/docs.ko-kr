---
title: '방법: Windows Forms의 ToolStrip 오버플로 관리'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStrip control [Windows Forms], managing overflow
- toolbars [Windows Forms], managing overflow
- examples [Windows Forms], toolbars
- CanOverflow property
ms.assetid: fa10e0ad-4cbf-4c0d-9082-359c2f855d4e
ms.openlocfilehash: 53f610a728925d454a8833a49e705818f027aec5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61913759"
---
# <a name="how-to-manage-toolstrip-overflow-in-windows-forms"></a>방법: Windows Forms의 ToolStrip 오버플로 관리

경우에 있는 모든 항목이 <xref:System.Windows.Forms.ToolStrip> 제어 할당된 된 공간에 맞지 않는에서 오버플로 기능을 사용할 수 있습니다 합니다 <xref:System.Windows.Forms.ToolStrip> 특정의 오버플로 동작을 결정 하 고 <xref:System.Windows.Forms.ToolStripItem>s.

추가 하는 경우 <xref:System.Windows.Forms.ToolStripItem>에 할당 된 것 보다 더 많은 공간이 필요는 <xref:System.Windows.Forms.ToolStrip> 폼의 현재 크기를 지정를 <xref:System.Windows.Forms.ToolStripOverflowButton> 에 자동으로 표시 되는 <xref:System.Windows.Forms.ToolStrip>합니다. <xref:System.Windows.Forms.ToolStripOverflowButton> 나타납니다 오버플로 드롭다운 메뉴에 오버플로가 활성화 된 항목 이동 됩니다. 이렇게 하면 사용자 지정 하 고 우선 순위를 지정할 수 있습니다 하는 방법에 <xref:System.Windows.Forms.ToolStrip> 항목 다양 한 폼 크기에 맞게 조정 합니다. 사용 하 여 오버플로 나뉩니다 때에 해당 항목의 모양을 변경할 수 있습니다 합니다 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 하 고 <xref:System.Windows.Forms.ToolStripOverflow.DisplayedItems%2A?displayProperty=nameWithType> 속성 및 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 이벤트입니다. 더 디자인 타임 또는 런타임에 폼을 확대 하는 경우 <xref:System.Windows.Forms.ToolStripItem>주에 s를 표시할 수 있습니다 <xref:System.Windows.Forms.ToolStrip> 고 <xref:System.Windows.Forms.ToolStripOverflowButton> 폼의 크기를 줄일 때까지 않을 수도 있습니다.

## <a name="to-enable-overflow-on-a-toolstrip-control"></a>ToolStrip 컨트롤에는 오버플로 사용 하도록 설정 하려면

- 있는지 확인 합니다 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> 속성으로 설정 되지 않은 `false` 에 대 한는 <xref:System.Windows.Forms.ToolStrip>합니다. 기본값은 `True`입니다.

     때 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> 는 `True` (기본값)를 <xref:System.Windows.Forms.ToolStripItem> 드롭 다운 오버플로 메뉴로 보낼 때 내용의 <xref:System.Windows.Forms.ToolStripItem> 가로 너비를 초과 <xref:System.Windows.Forms.ToolStrip> 높이의 세로 <xref:System.Windows.Forms.ToolStrip>.

## <a name="to-specify-overflow-behavior-of-a-specific-toolstripitem"></a>특정 toolstripitem을 가리키는의 오버플로 동작을 지정 하려면

- 설정 합니다 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 의 속성은 <xref:System.Windows.Forms.ToolStripItem> 를 원하는 값입니다. 가능성은 `Always`하십시오 `Never`, 및 `AsNeeded`합니다. 기본값은 `AsNeeded`입니다.

    ```vb
    toolStripTextBox1.Overflow = _
    System.Windows.Forms.ToolStripItemOverflow.Never
    ```

    ```csharp
    toolStripTextBox1.Overflow = _
    System.Windows.Forms.ToolStripItemOverflow.Never;
    ```

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStripOverflowButton>
- <xref:System.Windows.Forms.ToolStripItem.Overflow%2A>
- <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
- [ToolStrip 컨트롤 아키텍처](toolstrip-control-architecture.md)
- [ToolStrip 기술 요약](toolstrip-technology-summary.md)
