---
title: '방법: StackPanel 및 DockPanel 중에서 선택'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [WPF], DockPanel
- DockPanel control [WPF], StackPanel control compared to
- StackPanel control [WPF], DockPanel control compared to
- controls [WPF], StackPanel
ms.assetid: f9239086-451f-42e6-81f7-ef89ef349742
ms.openlocfilehash: 8338421dfb1bea856c15edf9d324cec955584f9f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911244"
---
# <a name="how-to-choose-between-stackpanel-and-dockpanel"></a>방법: StackPanel 및 DockPanel 중에서 선택
사용할지 선택 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.StackPanel> 또는 <xref:System.Windows.Controls.DockPanel> 의 콘텐츠를 스택 하는 경우는 <xref:System.Windows.Controls.Panel>합니다.  
  
## <a name="example"></a>예제  
 중 하나를 사용할 수 있지만 <xref:System.Windows.Controls.DockPanel> 또는 <xref:System.Windows.Controls.StackPanel> 스택은 자식 요소를 두 개의 컨트롤을 생성 하지 않을 동일한 결과 합니다. 자식 요소를 배치 하는 순서에 자식 요소의 크기 영향을 줄 수는 예를 들어, 한 <xref:System.Windows.Controls.DockPanel> 되지 않습니다는 <xref:System.Windows.Controls.StackPanel>합니다. 이 다른 문제가 발생 <xref:System.Windows.Controls.StackPanel> 에서 쌓는 방향으로 측정 <xref:System.Double>합니다.<xref:System.Double.PositiveInfinity>하지만 <xref:System.Windows.Controls.DockPanel> 사용 가능한 크기를 측정 합니다.  
  
 다음 예제에서는이 주요 차이점을 보여 줍니다 <xref:System.Windows.Controls.DockPanel> 고 <xref:System.Windows.Controls.StackPanel>입니다.  
  
 [!code-cpp[StackPanelOvw4#1](~/samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xaml[StackPanelOvw4#1](~/samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.StackPanel>
- <xref:System.Windows.Controls.DockPanel>
- [패널 개요](panels-overview.md)
