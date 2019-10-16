---
title: Windows Forms의 마우스 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- MouseLeave event [Windows Forms]
- events [Windows Forms], mouse
- Click event [Windows Forms], raising order
- Windows Forms controls, click events
- MouseDoubleClick event [Windows Forms]
- MouseEnter event [Windows Forms]
- MouseHover event [Windows Forms]
- MouseDown event [Windows Forms]
- MouseClick event [Windows Forms]
- MouseMove event [Windows Forms]
- mouse [Windows Forms], events
- MouseUp event
ms.assetid: 8cf0070d-793b-4876-b09e-d20d28280fab
ms.openlocfilehash: a61f4eedde611cfb7598d55465103924516e06c6
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834605"
---
# <a name="mouse-events-in-windows-forms"></a>Windows Forms의 마우스 이벤트

마우스 입력을 처리하는 경우 일반적으로 마우스 포인터의 위치와 마우스 단추의 상태를 알아야 합니다. 이 항목에서는 마우스 이벤트에서 이 정보를 가져오는 방법을 자세히 설명하고 Windows Forms 컨트롤에서 마우스 클릭 이벤트가 발생하는 순서를 설명합니다. 모든 마우스 이벤트에 대 한 목록 및 설명은 [Windows Forms에서 마우스 입력이 작동 하는 방식](how-mouse-input-works-in-windows-forms.md)을 참조 하세요.  [이벤트 처리기 개요 (Windows Forms)](event-handlers-overview-windows-forms.md) 및 [이벤트 개요 (Windows Forms)](events-overview-windows-forms.md)도 참조 하세요.

## <a name="mouse-information"></a>마우스 정보

<xref:System.Windows.Forms.MouseEventArgs>는 마우스 단추 클릭 및 마우스 움직임 추적과 관련된 마우스 이벤트 처리기로 전송됩니다. <xref:System.Windows.Forms.MouseEventArgs>는 클라이언트 좌표에서 마우스 포인터의 위치, 누른 마우스 단추, 마우스 휠의 스크롤 여부를 포함하여 마우스의 현재 상태에 대한 정보를 제공합니다. 마우스 포인터가 컨트롤의 범위로 들어오거나 나갈 때 단순히 알리는 이벤트와 같은 여러 마우스 이벤트가 추가 정보 없이 <xref:System.EventArgs>를 이벤트 처리기로 전송합니다.

마우스 이벤트를 처리하지 않고 마우스 단추의 현재 상태나 마우스 포인터의 위치를 확인하려는 경우 <xref:System.Windows.Forms.Control> 클래스의 <xref:System.Windows.Forms.Control.MouseButtons%2A> 및 <xref:System.Windows.Forms.Control.MousePosition%2A> 속성을 사용할 수도 있습니다. <xref:System.Windows.Forms.Control.MouseButtons%2A>는 현재 누른 마우스 단추에 대한 정보를 반환합니다. <xref:System.Windows.Forms.Control.MousePosition%2A>은 마우스 포인터의 화면 좌표를 반환하며 <xref:System.Windows.Forms.Cursor.Position%2A>에서 반환되는 값과 같습니다.

## <a name="converting-between-screen-and-client-coordinates"></a>화면 좌표와 클라이언트 좌표 간의 변환

일부 마우스 위치 정보는 클라이언트 좌표로 표시되고 일부 정보는 화면 좌표로 표시되므로 좌표계 간에 지점을 변환해야 할 수도 있습니다. <xref:System.Windows.Forms.Control> 클래스에서 사용할 수 있는 <xref:System.Windows.Forms.Control.PointToClient%2A> 및 <xref:System.Windows.Forms.Control.PointToScreen%2A> 메서드를 사용하면 이 작업을 쉽게 수행할 수 있습니다.

## <a name="standard-click-event-behavior"></a>표준 클릭 이벤트 동작

마우스 클릭 이벤트를 적절한 순서로 처리하려는 경우 Windows Forms 컨트롤에서 클릭 이벤트가 발생하는 순서를 알아야 합니다. 개별 컨트롤에 대한 다음 목록에 명시된 경우를 제외하고 모든 Windows Forms 컨트롤은 어떤 마우스 단추인지에 관계없이 마우스 단추를 눌렀다 놓는 순서대로 클릭 이벤트를 발생시킵니다. 다음 목록에서는 마우스 단추 한 번 클릭에 대해 발생하는 이벤트 순서를 보여 줍니다.

1. <xref:System.Windows.Forms.Control.MouseDown> 이벤트

2. <xref:System.Windows.Forms.Control.Click> 이벤트

3. <xref:System.Windows.Forms.Control.MouseClick> 이벤트

4. <xref:System.Windows.Forms.Control.MouseUp> 이벤트

다음은 마우스 단추를 두 번 클릭할 때 발생 하는 이벤트의 순서입니다.

1. <xref:System.Windows.Forms.Control.MouseDown> 이벤트

2. <xref:System.Windows.Forms.Control.Click> 이벤트

3. <xref:System.Windows.Forms.Control.MouseClick> 이벤트

4. <xref:System.Windows.Forms.Control.MouseUp> 이벤트

5. <xref:System.Windows.Forms.Control.MouseDown> 이벤트

6. <xref:System.Windows.Forms.Control.DoubleClick> 이벤트 해당 컨트롤에 대한 <xref:System.Windows.Forms.ControlStyles.StandardDoubleClick> 스타일 비트가 `true`로 설정되었는지 여부에 따라 달라질 수 있습니다. <xref:System.Windows.Forms.ControlStyles>를 설정하는 방법에 대한 자세한 내용은 <xref:System.Windows.Forms.Control.SetStyle%2A> 메서드를 참조하세요.

7. <xref:System.Windows.Forms.Control.MouseDoubleClick> 이벤트

8. <xref:System.Windows.Forms.Control.MouseUp> 이벤트

마우스 클릭 이벤트의 순서를 보여 주는 코드 예제를 보려면 [How to: Windows Forms 컨트롤 @ no__t에서 사용자 입력 이벤트를 처리 합니다.

### <a name="individual-controls"></a>개별 컨트롤

다음 컨트롤은 표준 마우스 클릭 이벤트 동작을 준수하지 않습니다.

- <xref:System.Windows.Forms.Button>
- <xref:System.Windows.Forms.CheckBox>
- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.RadioButton>

  > [!NOTE]
  > <xref:System.Windows.Forms.ComboBox> 컨트롤의 경우 사용자가 편집 필드, 단추 또는 목록 내의 항목을 클릭하면 나중에 자세히 설명하는 이벤트 동작이 발생합니다.

  - 마우스 왼쪽 단추 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>

  - 마우스 오른쪽 단추를 클릭 합니다. Click 이벤트가 발생 하지 않음

  - 마우스 왼쪽 단추 두 번 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>, <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>

  - 마우스 오른쪽 단추를 두 번 클릭 합니다. Click 이벤트가 발생 하지 않음

- <xref:System.Windows.Forms.TextBox>, <xref:System.Windows.Forms.RichTextBox>, <xref:System.Windows.Forms.ListBox>, <xref:System.Windows.Forms.MaskedTextBox>및 <xref:System.Windows.Forms.CheckedListBox> 컨트롤

  > [!NOTE]
  > 사용자가 이러한 컨트롤 내의 아무 곳이나 클릭하면 나중에 자세히 설명하는 이벤트 동작이 발생합니다.

  - 마우스 왼쪽 단추 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>

  - 마우스 오른쪽 단추를 클릭 합니다. Click 이벤트가 발생 하지 않음

  - 마우스 왼쪽 단추 두 번 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>, <xref:System.Windows.Forms.Control.DoubleClick>, <xref:System.Windows.Forms.Control.MouseDoubleClick>

  - 마우스 오른쪽 단추를 두 번 클릭 합니다. Click 이벤트가 발생 하지 않음

- <xref:System.Windows.Forms.ListView> 컨트롤

  > [!NOTE]
  > 사용자가 <xref:System.Windows.Forms.ListView> 컨트롤의 항목을 클릭하는 경우에만 나중에 자세히 설명하는 이벤트 동작이 발생합니다. 컨트롤의 다른 곳을 클릭하면 이벤트가 발생하지 않습니다. 나중에 설명하는 이벤트 외에도 <xref:System.Windows.Forms.ListView> 컨트롤에 유효성 검사를 사용하려는 경우 중요할 수 있는 <xref:System.Windows.Forms.ListView.BeforeLabelEdit> 및 <xref:System.Windows.Forms.ListView.AfterLabelEdit> 이벤트가 있습니다.

  - 마우스 왼쪽 단추 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>

  - 마우스 오른쪽 단추 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>

  - 마우스 왼쪽 단추 두 번 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>, <xref:System.Windows.Forms.Control.DoubleClick>, <xref:System.Windows.Forms.Control.MouseDoubleClick>

  - 마우스 오른쪽 단추 두 번 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>, <xref:System.Windows.Forms.Control.DoubleClick>, <xref:System.Windows.Forms.Control.MouseDoubleClick>

- <xref:System.Windows.Forms.TreeView> 컨트롤

  > [!NOTE]
  > 사용자가 <xref:System.Windows.Forms.TreeView> 컨트롤에서 항목 자체나 항목 오른쪽을 클릭하는 경우에만 나중에 자세히 설명하는 이벤트 동작이 발생합니다. 컨트롤의 다른 곳을 클릭하면 이벤트가 발생하지 않습니다. 나중에 설명하는 이벤트 외에도 <xref:System.Windows.Forms.TreeView> 컨트롤에 유효성 검사를 사용하려는 경우 중요할 수 있는 <xref:System.Windows.Forms.TreeView.BeforeCheck>, <xref:System.Windows.Forms.TreeView.BeforeSelect>, <xref:System.Windows.Forms.TreeView.BeforeLabelEdit>, <xref:System.Windows.Forms.TreeView.AfterSelect>, <xref:System.Windows.Forms.TreeView.AfterCheck> 및 <xref:System.Windows.Forms.TreeView.AfterLabelEdit> 이벤트가 있습니다.

  - 마우스 왼쪽 단추 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>

  - 마우스 오른쪽 단추 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>

  - 마우스 왼쪽 단추 두 번 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>, <xref:System.Windows.Forms.Control.DoubleClick>, <xref:System.Windows.Forms.Control.MouseDoubleClick>

  - 마우스 오른쪽 단추 두 번 클릭: <xref:System.Windows.Forms.Control.Click>, <xref:System.Windows.Forms.Control.MouseClick>, <xref:System.Windows.Forms.Control.DoubleClick>, <xref:System.Windows.Forms.Control.MouseDoubleClick>

### <a name="painting-behavior-of-toggle-controls"></a>토글 컨트롤의 그리기 동작

<xref:System.Windows.Forms.ButtonBase> 클래스에서 파생되는 컨트롤과 같은 토글 컨트롤은 마우스 클릭 이벤트와 결합되어 다음과 같은 고유한 그리기 동작을 제공합니다.

1. 사용자가 마우스 단추를 누릅니다.

2. 컨트롤이 눌린 상태로 그려집니다.

3. <xref:System.Windows.Forms.Control.MouseDown> 이벤트가 발생합니다.

4. 사용자가 마우스 단추를 놓습니다.

5. 컨트롤이 올려진 상태로 그려집니다.

6. <xref:System.Windows.Forms.Control.Click> 이벤트가 발생합니다.

7. <xref:System.Windows.Forms.Control.MouseClick> 이벤트가 발생합니다.

8. <xref:System.Windows.Forms.Control.MouseUp> 이벤트가 발생합니다.

    > [!NOTE]
    > 사용자가 마우스 단추를 누른 동안 토글 컨트롤에서 포인터를 이동하는 경우(예: 누른 동안 <xref:System.Windows.Forms.Button> 컨트롤에서 마우스 이동) 토글 컨트롤이 올려진 상태로 그려지고 <xref:System.Windows.Forms.Control.MouseUp> 이벤트만 발생합니다. 이런 상황에서는 <xref:System.Windows.Forms.Control.Click> 또는 <xref:System.Windows.Forms.Control.MouseClick> 이벤트가 발생하지 않습니다.

## <a name="see-also"></a>참조

- [Windows Forms 애플리케이션의 마우스 입력](mouse-input-in-a-windows-forms-application.md)
