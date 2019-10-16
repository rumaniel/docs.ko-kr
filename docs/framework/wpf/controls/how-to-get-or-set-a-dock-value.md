---
title: '방법: Dock 값 가져오기 또는 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dock values [WPF], setting
- Dock values [WPF], getting
ms.assetid: fcf4ab8a-c7cd-4835-8d04-de1c999ab4a8
ms.openlocfilehash: fb6c8a7d62aa09a6e1d82cb4079d1425a7f39f8c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910288"
---
# <a name="how-to-get-or-set-a-dock-value"></a>방법: Dock 값 가져오기 또는 설정
다음 예제에서는 할당 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Dock> 개체에 대 한 값입니다. 이 예제에서는 사용 합니다 <xref:System.Windows.Controls.DockPanel.GetDock%2A> 및 <xref:System.Windows.Controls.DockPanel.SetDock%2A> 메서드의 <xref:System.Windows.Controls.DockPanel>.  
  
## <a name="example"></a>예제  
 예제의 인스턴스를 만듭니다는 <xref:System.Windows.Controls.TextBlock> 요소인 `txt1`, 할당 및를 <xref:System.Windows.Controls.Dock> 값 `Top` 를 사용 하 여를 <xref:System.Windows.Controls.DockPanel.SetDock%2A> 메서드의 <xref:System.Windows.Controls.DockPanel>. 다음의 값을 추가 합니다 <xref:System.Windows.Controls.Dock> 속성을를 <xref:System.Windows.Controls.TextBlock.Text%2A> 의 <xref:System.Windows.Controls.TextBlock> 요소를 사용 하 여를 <xref:System.Windows.Controls.DockPanel.GetDock%2A> 메서드. 마지막으로,이 예제에서는 추가 합니다 <xref:System.Windows.Controls.TextBlock> 부모 요소의 <xref:System.Windows.Controls.DockPanel>, `dp1`합니다.  
  
 [!code-csharp[DockPanelSetDock#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DockPanelSetDock/CSharp/DockPanel_SetDock.cs#1)]
 [!code-vb[DockPanelSetDock#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelSetDock/VisualBasic/DockPanel_SetDock.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.DockPanel>
- <xref:System.Windows.Controls.DockPanel.GetDock%2A>
- <xref:System.Windows.Controls.DockPanel.SetDock%2A>
- [패널 개요](panels-overview.md)
