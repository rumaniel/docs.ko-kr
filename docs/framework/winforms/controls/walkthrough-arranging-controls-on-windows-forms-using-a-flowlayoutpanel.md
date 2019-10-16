---
title: '연습: FlowLayoutPanel을 사용하여 Windows Forms에서 컨트롤 정렬'
ms.date: 03/30/2017
helpviewer_keywords:
- FlowLayoutPanel control [Windows Forms], walkthroughs
- Windows Forms controls, arranging
- controls [Windows Forms], arranging with FlowLayoutPanel
- layout [Windows Forms], walkthroughs
ms.assetid: a1744323-0316-49c2-992e-ebfc0a976b85
ms.openlocfilehash: c9ee615a610c383c97b5d4f0de195cfc7422d3ec
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67771656"
---
# <a name="walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel"></a>연습: FlowLayoutPanel을 사용하여 Windows Forms에서 컨트롤 정렬

일부 애플리케이션에는 폼 크기가 조정되거나 내용의 크기가 변경될 때 적절하게 정렬되는 레이아웃을 가진 폼이 필요합니다. 동적 레이아웃이 필요하며 코드에서 명시적으로 <xref:System.Windows.Forms.Control.Layout> 이벤트를 처리하지 않으려는 경우 레이아웃 패널을 사용하는 것이 좋습니다.

<xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤 및 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤은 폼에서 컨트롤을 정렬하는 직관적인 방법을 제공합니다. 둘 다 포함된 자식 컨트롤의 상대 위치를 제어하는 구성 가능한 자동 기능을 제공하며, 둘 다 런타임에 동적 레이아웃 기능을 제공하므로 부모 폼의 크기가 변경될 때 자식 컨트롤의 크기를 조정하고 위치를 변경할 수 있습니다. 레이아웃 패널을 레이아웃 패널 내에 중첩하여 정교한 사용자 인터페이스를 구현할 수 있습니다.

합니다 <xref:System.Windows.Forms.TableLayoutPanel> HTML과 비슷한 기능을 제공 하는 눈금으로 내용을 정렬 \<테이블 > 요소입니다. 해당 셀은 행과 열로 정렬되며 크기가 서로 다를 수 있습니다. 자세한 내용은 [연습: TableLayoutPanel을 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)합니다.

<xref:System.Windows.Forms.FlowLayoutPanel> 은 특정 흐름 방향(수평 또는 수직)으로 내용을 정렬합니다. 컨트롤 내용을 한 행에서 다음 행으로 또는 한 열에서 다음 열로 줄 바꿈할 수 있습니다. 또는 컨트롤 내용이 줄 바꿈되는 대신 잘릴 수 있습니다. 이 연습에서 설명하는 작업은 다음과 같습니다.

- Windows Forms 프로젝트 만들기

- 가로 및 세로로 컨트롤 정렬

- 흐름 방향 변경

- 흐름 나누기 삽입

- 안쪽 여백 및 여백을 사용하여 컨트롤 정렬

- 도구 상자에서 두 번 클릭하여 컨트롤 삽입

- 윤곽선을 그려 컨트롤 삽입

- 캐럿을 사용하여 컨트롤 삽입

- 다른 부모에 기존 컨트롤 다시 할당

작업을 완료 하는 경우에 이러한 중요 한 레이아웃 기능을 통해 수행 하는 역할을 이해를 해야 합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

1. Visual Studio에서 "FlowLayoutPanelExample" 이라는 Windows 기반 응용 프로그램 프로젝트를 만듭니다 (**파일** > **새로 만들기** > **프로젝트**  >  **시각적 C#**  하거나 **Visual Basic** > **클래식 바탕 화면** > **Windows Forms응용프로그램**).

2. **폼 디자이너**에서 폼을 선택합니다.

## <a name="arranging-controls-horizontally-and-vertically"></a>가로 및 세로로 컨트롤 정렬
 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤을 사용하면 각 개별 컨트롤의 위치를 정확하게 지정하지 않고 행 또는 열에 컨트롤을 배치할 수 있습니다.

 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤은 부모 폼의 크기가 변경될 때 자식 컨트롤의 크기를 조정하거나 흐름을 변경할 수 있습니다.

### <a name="to-arrange-controls-horizontally-and-vertically-using-a-flowlayoutpanel"></a>FlowLayoutPanel을 사용하여 가로 및 세로로 컨트롤을 정렬하려면

1. <xref:System.Windows.Forms.FlowLayoutPanel> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 <xref:System.Windows.Forms.FlowLayoutPanel>로 끌어다 놓습니다. 컨트롤이 자동으로 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 왼쪽 위로 이동됩니다.

3. <xref:System.Windows.Forms.Button> 도구 상자 **에서 다른** 컨트롤을 <xref:System.Windows.Forms.FlowLayoutPanel>로 끌어다 놓습니다. <xref:System.Windows.Forms.Button> 컨트롤이 자동으로 첫 번째 <xref:System.Windows.Forms.Button> 컨트롤 옆의 위치로 이동됩니다. <xref:System.Windows.Forms.FlowLayoutPanel> 이 너무 좁아서 두 컨트롤을 동일한 행에 배치할 수 없는 경우 새 <xref:System.Windows.Forms.Button> 컨트롤이 자동으로 다음 행으로 이동됩니다.

4. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 몇 개 더 <xref:System.Windows.Forms.FlowLayoutPanel>로 끌어다 놓습니다. 한 컨트롤이 다음 행으로 줄 바꿈될 때까지 <xref:System.Windows.Forms.Button> 컨트롤을 계속 배치합니다.

5. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 <xref:System.Windows.Forms.FlowLayoutPanel.WrapContents%2A> 속성 값을 `false`로 변경합니다. 자식 컨트롤이 더 이상 다음 행으로 흐르지 않습니다. 대신, 첫 번째 행으로 이동되어 잘립니다.

6. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 <xref:System.Windows.Forms.FlowLayoutPanel.WrapContents%2A> 속성 값을 `true`로 변경합니다. 자식 컨트롤이 다시 다음 행으로 줄 바꿈됩니다.

7. 모든 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤이 첫 번째 열로 이동될 때까지 <xref:System.Windows.Forms.Button> 컨트롤의 너비를 줄입니다.

8. 모든 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤이 첫 번째 행으로 이동될 때까지 <xref:System.Windows.Forms.Button> 컨트롤의 너비를 늘립니다. 큰 너비를 수용하기 위해 폼 크기를 조정해야 할 수도 있습니다.

## <a name="changing-flow-direction"></a>흐름 방향 변경
 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 속성을 사용하면 컨트롤이 정렬되는 방향을 변경할 수 있습니다. 왼쪽에서 오른쪽, 오른쪽에서 왼쪽, 위쪽에서 아래쪽 또는 아래쪽에서 위쪽으로 자식 컨트롤을 정렬할 수 있습니다.

### <a name="to-change-the-flow-direction-in-a-flowlayoutpanel"></a>FlowLayoutPanel에서 흐름 방향을 변경하려면

1. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 속성 값을 <xref:System.Windows.Forms.FlowDirection.TopDown>로 변경합니다. 컨트롤의 높이에 따라 자식 컨트롤이 하나 이상의 열에 다시 정렬됩니다.

2. 높이가 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 열보다 더 짧도록 <xref:System.Windows.Forms.Button> 의 크기를 조정합니다. <xref:System.Windows.Forms.FlowLayoutPanel> 이 자식 컨트롤을 다시 정렬하여 다음 열로 흐르도록 합니다. 높이를 계속 줄이면서 자식 컨트롤이 연속하는 열로 흐르는 것을 확인합니다. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 속성 값을 <xref:System.Windows.Forms.FlowDirection.RightToLeft>로 변경합니다. 자식 컨트롤의 위치는 반대가 됩니다. <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 속성의 값을 <xref:System.Windows.Forms.FlowDirection.BottomUp>으로 변경하면서 레이아웃을 살펴봅니다.

## <a name="inserting-flow-breaks"></a>흐름 나누기 삽입
 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤은 자식 컨트롤에 FlowBreak 속성을 제공합니다. FlowBreak 속성의 값을 `true` 로 설정하면 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤이 현재 흐름 방향에서 컨트롤 레이아웃을 중지하고 다음 행이나 열로 줄 바꿈합니다.

### <a name="to-insert-flow-breaks"></a>흐름 나누기를 삽입하려면

1. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 속성 값을 <xref:System.Windows.Forms.FlowDirection.TopDown>로 변경합니다.

2. 맨 왼쪽 열의 중간에서 <xref:System.Windows.Forms.Button> 컨트롤 중 하나를 선택합니다.

3. <xref:System.Windows.Forms.Button> 컨트롤의 FlowBreak 속성 값을 `true`로 설정합니다. 열이 나누어지고 선택한 <xref:System.Windows.Forms.Button> 컨트롤 뒤에 있는 컨트롤이 다음 열로 흐릅니다. <xref:System.Windows.Forms.Button> 컨트롤의 FlowBreak 속성 값을 `false` 로 설정하여 원래 동작으로 되돌립니다.

## <a name="positioning-controls-using-docking-and-anchoring"></a>도킹 및 고정 기능을 사용하여 컨트롤 위치 지정
 자식 컨트롤의 도킹 및 고정 동작은 다른 컨테이너 컨트롤의 동작과 다릅니다. 도킹 및 고정은 둘 다 흐름 방향에서 가장 큰 컨트롤을 기준으로 합니다.

### <a name="to-position-controls-using-docking-and-anchoring"></a>도킹 및 고정 기능을 사용하여 컨트롤 위치를 지정하려면

1. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤이 모두 열에 정렬될 때까지 <xref:System.Windows.Forms.Button> 의 크기를 늘립니다.

2. 위쪽 <xref:System.Windows.Forms.Button> 컨트롤을 선택합니다. 다른 <xref:System.Windows.Forms.Button> 컨트롤 너비의 두 배가 되도록 너비를 늘립니다.

3. 두 번째 <xref:System.Windows.Forms.Button> 컨트롤을 선택합니다. <xref:System.Windows.Forms.Control.Anchor%2A> 속성의 값을 <xref:System.Windows.Forms.AnchorStyles.Right>로 변경합니다. 오른쪽 테두리가 첫 번째 <xref:System.Windows.Forms.Button> 컨트롤의 오른쪽 테두리에 정렬되도록 이동됩니다.

4. <xref:System.Windows.Forms.Control.Anchor%2A> 속성의 값을 <xref:System.Windows.Forms.AnchorStyles.Right> 및 <xref:System.Windows.Forms.AnchorStyles.Left>로 변경합니다. 첫 번째 <xref:System.Windows.Forms.Button> 컨트롤과 동일한 너비로 크기가 조정됩니다.

5. 세 번째 <xref:System.Windows.Forms.Button> 컨트롤을 선택합니다. <xref:System.Windows.Forms.Control.Dock%2A> 속성의 값을 <xref:System.Windows.Forms.DockStyle.Fill>로 변경합니다. 첫 번째 <xref:System.Windows.Forms.Button> 컨트롤과 동일한 너비로 크기가 조정됩니다.

## <a name="arranging-controls-using-padding-and-margins"></a>안쪽 여백 및 여백을 사용하여 컨트롤 정렬
 <xref:System.Windows.Forms.FlowLayoutPanel> 및 <xref:System.Windows.Forms.Control.Padding%2A> 속성을 변경하여 <xref:System.Windows.Forms.Control.Margin%2A> 컨트롤에 컨트롤을 정렬할 수도 있습니다.

 <xref:System.Windows.Forms.Control.Padding%2A> 속성을 사용하면 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 셀 내에서 컨트롤 배치를 제어할 수 있습니다. 자식 컨트롤과 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤 테두리 사이의 간격을 지정합니다.

 <xref:System.Windows.Forms.Control.Margin%2A> 속성을 사용하면 컨트롤 사이의 간격을 제어할 수 있습니다.

### <a name="to-arrange-controls-using-the-padding-and-margin-properties"></a>안쪽 여백 및 여백 속성을 사용하여 컨트롤을 정렬하려면

1. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 <xref:System.Windows.Forms.Control.Dock%2A> 속성 값을 <xref:System.Windows.Forms.DockStyle.Fill>로 변경합니다. 폼이 충분히 큰 경우 <xref:System.Windows.Forms.Button> 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 첫 번째 열로 이동됩니다.

2. <xref:System.Windows.Forms.FlowLayoutPanel> 속성 <xref:System.Windows.Forms.Control.Padding%2A> 창에서 <xref:System.Windows.Forms.Control.Padding%2A> 항목을 확장하고 **속성을** 20 <xref:System.Windows.Forms.Padding.All%2A> 으로 설정하여 **컨트롤의**속성 값을 변경합니다. 자세한 내용은 [연습: 레이아웃 Windows Forms 컨트롤 Padding, Margins 및 AutoSize 속성을 사용 하 여](windows-forms-controls-padding-autosize.md)입니다. 자식 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 중심 쪽으로 이동됩니다. <xref:System.Windows.Forms.Control.Padding%2A> 속성의 값이 증가한 만큼 자식 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 테두리에서 멀어집니다.

3. <xref:System.Windows.Forms.Button> 에서 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤을 모두 선택하고 <xref:System.Windows.Forms.Control.Margin%2A> 속성의 값을 **20**으로 설정합니다. <xref:System.Windows.Forms.Button> 컨트롤 사이의 간격이 증가하므로 더 멀리 떨어져 이동됩니다. 자식 컨트롤을 모두 표시하기 위해 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 크기를 더 크게 조정해야 할 수도 있습니다.

## <a name="inserting-controls-by-double-clicking-them-in-the-toolbox"></a>도구 상자에서 두 번 클릭하여 컨트롤 삽입
 <xref:System.Windows.Forms.FlowLayoutPanel> 도구 상자 **에서 컨트롤을 두 번 클릭하여**컨트롤을 채울 수 있습니다.

### <a name="to-insert-controls-by-double-clicking-in-the-toolbox"></a>도구 상자에서 두 번 클릭하여 컨트롤을 삽입하려면

1. <xref:System.Windows.Forms.Button> 도구 상자 **에서**컨트롤 아이콘을 두 번 클릭합니다. 새 <xref:System.Windows.Forms.Button> 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤에 표시됩니다.

2. **도구 상자**에서 컨트롤을 몇 개 더 두 번 클릭합니다. 새 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤에 연속해서 표시됩니다.

## <a name="inserting-a-control-by-drawing-its-outline"></a>윤곽선을 그려 컨트롤 삽입
 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤에 컨트롤을 삽입하고 셀에서 해당 윤곽선을 그려 크기를 지정합니다.

### <a name="to-insert-a-control-by-drawing-its-outline"></a>윤곽선을 그려 컨트롤을 삽입하려면

1. **도구 상자**에서 <xref:System.Windows.Forms.Button> 컨트롤 아이콘을 클릭합니다. 폼으로 끌어다 놓지 마세요.

2. 마우스 포인터를 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤 위로 이동합니다. 포인터가 <xref:System.Windows.Forms.Button> 컨트롤 아이콘이 연결된 십자형으로 바뀝니다.

3. 마우스 단추를 길게 클릭합니다.

4. 마우스 포인터를 끌어 <xref:System.Windows.Forms.Button> 컨트롤의 윤곽선을 그립니다. 원하는 크기가 되면 마우스 단추를 놓습니다. <xref:System.Windows.Forms.Button> 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 다음 열린 위치에 만들어집니다.

## <a name="inserting-controls-using-the-insertion-bar"></a>삽입 막대를 사용하여 컨트롤 삽입
 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 특정 위치에 컨트롤을 삽입할 수 있습니다. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 클라이언트 영역으로 컨트롤을 끌어다 놓으면 삽입 막대가 나타나 컨트롤이 삽입될 위치를 표시합니다.

### <a name="to-insert-a-control-using-the-caret"></a>캐럿을 사용하여 컨트롤을 삽입하려면

1. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤로 끌어다 놓고 두 <xref:System.Windows.Forms.Button> 컨트롤 사이의 공간을 가리킵니다. 삽입 막대가 그려집니다, 위치를 나타내는 합니다 <xref:System.Windows.Forms.Button> 놓을 때 배치 될는 <xref:System.Windows.Forms.FlowLayoutPanel> 제어 합니다. 새 <xref:System.Windows.Forms.Button> 컨트롤을 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤로 끌어다 놓기 전에 마우스 포인터를 움직여 삽입 막대가 어떻게 이동하는지 관찰합니다.

2. 새 <xref:System.Windows.Forms.Button> 컨트롤을 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤로 끌어다 놓습니다. 새 <xref:System.Windows.Forms.Button> 컨트롤은 <xref:System.Windows.Forms.Control.Margin%2A> 속성 값이 다르기 때문에 다른 컨트롤과 정렬되지 않습니다.

## <a name="reassigning-existing-controls-to-a-different-parent"></a>다른 부모에 기존 컨트롤 다시 할당
 폼에 있는 컨트롤을 새 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤에 할당할 수 있습니다.

### <a name="to-reparent-existing-controls"></a>기존 컨트롤의 부모를 재지정하려면

1. <xref:System.Windows.Forms.Button> 도구 상자 **의 세** 컨트롤을 폼으로 끌어옵니다. 서로 정렬되지 않은 상태로 근처에 배치합니다.

2. **도구 상자**에서 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤 아이콘을 클릭합니다. 폼으로 끌어다 놓지 마세요.

3. 마우스 포인터를 세 <xref:System.Windows.Forms.Button> 컨트롤 쪽으로 이동합니다. 포인터가 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤 아이콘이 연결된 십자형으로 바뀝니다.

4. 마우스 단추를 길게 클릭합니다.

5. 마우스 포인터를 끌어 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 윤곽선을 그립니다. 세 <xref:System.Windows.Forms.Button> 컨트롤 주위에 윤곽선을 그립니다.

6. 마우스 단추를 놓습니다. 세 <xref:System.Windows.Forms.Button> 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤에 삽입됩니다.

## <a name="next-steps"></a>다음 단계
 레이아웃 패널 및 컨트롤의 조합을 사용하여 복잡한 레이아웃을 얻을 수 있습니다. 다음과 같은 사항을 더 살펴보는 것이 좋습니다.

- <xref:System.Windows.Forms.Button> 컨트롤 중 하나의 크기를 더 크게 조정하고 레이아웃에 미치는 영향을 확인합니다.

- 레이아웃 패널에 다른 레이아웃 패널을 포함할 수 있습니다. <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤을 기존 컨트롤에 끌어다 놓습니다.

- <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤을 부모 폼에 도킹합니다. 폼의 크기를 조정하고 레이아웃에 미치는 영향을 확인합니다.

- 컨트롤 중 하나의 <xref:System.Windows.Forms.Control.Visible%2A> 속성을 `false` 로 설정하고 그에 대한 응답으로 <xref:System.Windows.Forms.FlowLayoutPanel> 이 어떻게 재배치되는지 확인합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.FlowLayoutPanel>
- <xref:System.Windows.Forms.TableLayoutPanel>
- [연습: TableLayoutPanel을 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [연습: 맞춤선을 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
- [Microsoft Windows 사용자 환경, 사용자 인터페이스 개발자 및 디자이너를 위한 공식 지침. Redmond, WA: Microsoft Press, 1999. (USBN: 0-7356-0566-1)](https://www.microsoft.com/mspress/southpacific/books/book11588.htm)
- [AutoSize 속성 개요](autosize-property-overview.md)
- [방법: Windows Forms에 컨트롤 도킹](how-to-dock-controls-on-windows-forms.md)
- [방법: Windows Forms에서 컨트롤 고정](how-to-anchor-controls-on-windows-forms.md)
- [연습: Windows Forms 컨트롤 Padding, Margins 및 AutoSize 속성을 사용 하 여 레이아웃](windows-forms-controls-padding-autosize.md)
