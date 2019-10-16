---
title: '방법: Windows Forms에서 컨트롤 고정'
ms.date: 03/30/2017
helpviewer_keywords:
- Anchor property [Windows Forms], enabling resizable forms
- Windows Forms controls, screen resolutions
- resizing forms [Windows Forms]
- Windows Forms controls, size
- screen resolution and control display
- controls [Windows Forms], anchoring
- forms [Windows Forms], resizing
- Windows Forms, resizing
- controls [Windows Forms], positioning
ms.assetid: 59ea914f-fbd3-427a-80fe-decd02f7ae6d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 94fa6fe90e5583a3bfecf376af59d53f6d8528af
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987498"
---
# <a name="how-to-anchor-controls-on-windows-forms"></a>방법: Windows Forms에서 컨트롤 고정

런타임에 사용자가 크기를 조정할 수 있는 폼을 디자인 하는 경우 폼의 컨트롤 크기를 조정 하 고 적절 하 게 위치를 변경 해야 합니다. 폼을 사용 하 여 동적으로 컨트롤의 크기를 조정 <xref:System.Windows.Forms.Control.Anchor%2A> 하려면 Windows Forms 컨트롤의 속성을 사용할 수 있습니다. 속성 <xref:System.Windows.Forms.Control.Anchor%2A> 은 컨트롤의 앵커 위치를 정의 합니다. 컨트롤이 폼에 고정 되 고 폼의 크기가 조정 되 면 컨트롤은 컨트롤과 앵커 위치 간의 거리를 유지 합니다. 예를 들어 폼의 왼쪽, <xref:System.Windows.Forms.TextBox> 오른쪽 및 아래쪽 가장자리에 고정 된 컨트롤이 있는 경우 폼의 크기가 조정 될 때 컨트롤의 크기를 조정 하 여 <xref:System.Windows.Forms.TextBox> 폼의 오른쪽과 왼쪽에서 같은 거리를 유지 합니다. 또한 컨트롤은 위치가 항상 폼의 아래쪽 가장자리와 동일한 거리를 갖도록 세로로 배치 됩니다. 컨트롤이 고정 되어 있지 않고 폼의 크기가 조정 되 면 폼의 가장자리를 기준으로 하는 컨트롤의 위치가 변경 됩니다.

합니다 <xref:System.Windows.Forms.Control.Anchor%2A> 상호 작용 하는 속성을 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성입니다. 자세한 내용은 [AutoSize 속성 개요](autosize-property-overview.md)를 참조 하세요.

## <a name="anchor-a-control-on-a-form"></a>폼에 컨트롤 고정

1. Visual Studio에서 고정 하려는 컨트롤을 선택 합니다.

    > [!NOTE]
    > CTRL 키를 누른 채 각 컨트롤을 클릭 하 여 선택 하 고이 절차의 나머지 단계를 수행 하 여 여러 컨트롤을 동시에 고정할 수 있습니다.

2. **속성** 창에서 <xref:System.Windows.Forms.Control.Anchor%2A> 속성의 오른쪽에 있는 화살표를 클릭 합니다.

     십자 표시를 보여 주는 편집기가 표시 됩니다.

3. 앵커를 설정 하려면 십자의 위쪽, 왼쪽, 오른쪽 또는 아래쪽 섹션을 클릭 합니다.

     컨트롤은 기본적으로 위쪽과 왼쪽에 고정 됩니다.

4. 앵커 된 컨트롤의 측면을 지우려면 십자의 arm을 클릭 합니다.

5. <xref:System.Windows.Forms.Control.Anchor%2A> 속성 편집기를 닫으려면 <xref:System.Windows.Forms.Control.Anchor%2A> 속성 이름을 다시 클릭 합니다.

런타임에 폼이 표시 되 면 컨트롤의 크기가 폼의 가장자리와 같은 거리에 배치 됩니다. 고정 가장자리 로부터의 거리는 항상 컨트롤이 Windows Forms 디자이너 배치 될 때 정의 된 거리와 동일 하 게 유지 됩니다.

> [!NOTE]
> <xref:System.Windows.Forms.ComboBox> 컨트롤과 같은 특정 컨트롤의 높이는 제한 되어 있습니다. 컨트롤을 폼 이나 컨테이너의 아래쪽에 고정 하면 컨트롤이 높이 제한을 초과할 수 없습니다.

상속 된 컨트롤은 `Protected` 고정 될 수 있어야 합니다. 컨트롤의 액세스 수준을 변경 하려면 `Modifiers` **속성** 창에서 해당 속성을 설정 합니다.

## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤](index.md)
- [AutoSize 속성 개요](autosize-property-overview.md)
- [방법: Windows Forms에 컨트롤 도킹](how-to-dock-controls-on-windows-forms.md)
- [연습: FlowLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [연습: TableLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [연습: 안쪽 여백, 여백 및 AutoSize 속성을 사용 하 여 Windows Forms 컨트롤 레이아웃](windows-forms-controls-padding-autosize.md)
