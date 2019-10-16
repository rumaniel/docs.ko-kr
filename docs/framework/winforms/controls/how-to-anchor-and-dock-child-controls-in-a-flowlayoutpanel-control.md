---
title: '방법: FlowLayoutPanel 컨트롤에서 자식 컨트롤 고정 및 도킹'
ms.date: 03/30/2017
helpviewer_keywords:
- layout [Windows Forms], child controls
- FlowLayoutPanel control [Windows Forms], child controls
- controls [Windows Forms], child
- child controls [Windows Forms], anchoring and docking
ms.assetid: a2bcdfca-9b63-45e6-9c0e-3411015cba98
ms.openlocfilehash: 3e9a5be944e199254ddb9cee0772c4d55be8fb77
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046063"
---
# <a name="how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control"></a>방법: FlowLayoutPanel 컨트롤에서 자식 컨트롤 고정 및 도킹

<xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤은 자식 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 및 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 지원합니다.

### <a name="to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control"></a>FlowLayoutPanel 컨트롤의 자식 컨트롤을 고정 및 도킹하려면

1. 폼에 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤을 만듭니다.

2. <xref:System.Windows.Forms.Control.Width%2A> <xref:System.Windows.Forms.FlowDirection.TopDown> <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 컨트롤의를 300로 설정 하 고를로 설정 합니다. <xref:System.Windows.Forms.FlowLayoutPanel>

3. 두 개의 <xref:System.Windows.Forms.Button> 컨트롤을 만들어 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤에 배치합니다.

4. 첫 번째 <xref:System.Windows.Forms.Control.Width%2A> 단추의를 **200**으로 설정 합니다.

5. 두 번째 단추의 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>로 설정합니다.

    > [!NOTE]
    > 두 번째 단추는 첫 번째 단추와 동일한 너비를 사용합니다. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 너비에 가로로 늘여지지 않습니다.

6. 두 번째 단추의 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 `None`로 설정합니다. 그러면 단추가 원래 너비를 사용합니다.

7. 두 번째 단추의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 `Left, Right`로 설정합니다.

    > [!IMPORTANT]
    > 두 번째 단추는 첫 번째 단추와 동일한 너비를 사용합니다. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 너비에 가로로 늘여지지 않습니다. 이는 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 고정 및 도킹에 대한 일반적인 규칙입니다. 세로 흐름 방향에서는 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤이 폼에서 가장 넓은 자식 컨트롤의 암시된 열 너비를 계산합니다. 이 열에서 <xref:System.Windows.Forms.Control.Anchor%2A> 또는 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 가진 다른 모든 컨트롤은 이 암시된 열에 맞게 맞춰지거나 늘어납니다. 이 동작은 가로 흐름 방향에서도 비슷하게 작동합니다. <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤은 행에서 가장 높은 자식 컨트롤의 암시된 행 높이를 계산하고 이 행에서 도킹 또는 고정된 모든 자식 컨트롤이 암시된 행을 채우도록 맞춰지거나 크기가 조정됩니다.

## <a name="example"></a>예제

다음 그림에서는 <xref:System.Windows.Forms.FlowLayoutPanel>의 파란색 단추를 기준으로 고정 및 도킹된 단추 4개를 보여 줍니다. <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>이 <xref:System.Windows.Forms.FlowDirection.LeftToRight>인 경우

![FlowLayoutPanel 고정](./media/net-flpanchorexp.gif "NET_FLPanchorExp")

다음 그림에서는 <xref:System.Windows.Forms.FlowLayoutPanel>의 파란색 단추를 기준으로 고정 및 도킹된 단추 4개를 보여 줍니다. <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>이 <xref:System.Windows.Forms.FlowDirection.TopDown>인 경우

![FlowLayoutPanel 고정](./media/vs-flpanchor2.gif "VS_FLPanchor2")

다음 코드 예제에서는 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 <xref:System.Windows.Forms.Button> 컨트롤에 대한 다양한 <xref:System.Windows.Forms.Control.Anchor%2A> 속성 값을 보여 줍니다.

[!code-csharp[System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm/CS/FlpAnchorExampleForm.cs#1)]
[!code-vb[System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm/VB/FlpAnchorExampleForm.vb#1)]

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- System, System.Data, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.FlowLayoutPanel>
- [FlowLayoutPanel 컨트롤 개요](flowlayoutpanel-control-overview.md)
