---
title: '방법: TabControl을 사용하여 세로로 정렬된 탭 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tab pages [Windows Forms], displaying side-aligned tabs
- tabs [Windows Forms], displaying side-aligned tabs
- TabControl control [Windows Forms], displaying side-aligned tabs
ms.assetid: 110d5abd-3ae3-4ded-95bf-778aaac798a0
ms.openlocfilehash: d98c5906d99dff9371f8290e7dbc9c9011cd0c29
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61650494"
---
# <a name="how-to-display-side-aligned-tabs-with-tabcontrol"></a>방법: TabControl을 사용하여 세로로 정렬된 탭 표시
<xref:System.Windows.Forms.TabControl>의 <xref:System.Windows.Forms.TabControl.Alignment%2A> 속성은 가로(컨트롤 위쪽 또는 아래쪽에 가로로)가 아니라 세로로(컨트롤 왼쪽 또는 오른쪽 가장자리에 세로로) 탭 표시를 지원합니다. 시각적 스타일을 사용하는 경우 <xref:System.Windows.Forms.TabPage> 개체의 <xref:System.Windows.Forms.TabPage.Text%2A> 속성이 탭에 표시되지 않으므로 기본적으로 이 세로 표시를 사용하면 사용자 환경이 저하됩니다. 탭 내의 텍스트 방향을 제어하는 직접적인 방법도 없습니다. <xref:System.Windows.Forms.TabControl>에서 소유자 그리기를 사용하여 이 환경을 개선할 수 있습니다.  
  
 다음 절차에서는 "소유자 그리기" 기능을 사용하여 탭 텍스트가 왼쪽에서 오른쪽으로 흐르는 오른쪽 맞춤 탭을 렌더링하는 방법을 보여 줍니다.  
  
### <a name="to-display-right-aligned-tabs"></a>오른쪽 맞춤 탭을 표시하려면  
  
1. 폼에 <xref:System.Windows.Forms.TabControl>를 추가합니다.  
  
2. <xref:System.Windows.Forms.TabControl.Alignment%2A> 속성을 <xref:System.Windows.Forms.TabAlignment.Right>으로 설정합니다.  
  
3. 모든 탭의 너비가 같도록 <xref:System.Windows.Forms.TabControl.SizeMode%2A> 속성을 <xref:System.Windows.Forms.TabSizeMode.Fixed>로 설정합니다.  
  
4. <xref:System.Windows.Forms.TabControl.ItemSize%2A> 속성을 원하는 탭의 고정 크기로 설정합니다. <xref:System.Windows.Forms.TabControl.ItemSize%2A> 속성은 탭이 오른쪽 맞춤인 경우에도 위쪽에 있는 것처럼 동작합니다. 따라서 탭의 가로 크기를 늘리려면 <xref:System.Drawing.Size.Height%2A> 속성을 변경해야 하고, 탭의 높이를 늘리려면 <xref:System.Drawing.Size.Width%2A> 속성을 변경해야 합니다.  
  
     아래 코드 예제에서 최상의 결과를 얻으려면 탭의 <xref:System.Drawing.Size.Width%2A>를 25로 설정하고 <xref:System.Drawing.Size.Height%2A>를 100으로 설정합니다.  
  
5. <xref:System.Windows.Forms.TabControl.DrawMode%2A> 속성을 <xref:System.Windows.Forms.TabDrawMode.OwnerDrawFixed>으로 설정합니다.  
  
6. 텍스트를 왼쪽에서 오른쪽으로 렌더링하는 <xref:System.Windows.Forms.TabControl>의 <xref:System.Windows.Forms.TabControl.DrawItem> 이벤트에 대한 처리기를 정의합니다.  
  
     [!code-csharp[TabControl.RightAlignedTabs#1](~/samples/snippets/csharp/VS_Snippets_Winforms/TabControl.RightAlignedTabs/CS/Form1.cs#1)]
     [!code-vb[TabControl.RightAlignedTabs#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/TabControl.RightAlignedTabs/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [TabControl 컨트롤](tabcontrol-control-windows-forms.md)
