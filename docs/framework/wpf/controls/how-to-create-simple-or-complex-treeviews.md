---
title: '방법: 간단하거나 복잡한 TreeView 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- TreeView control [WPF], creating
- Control class [WPF], TreeView [WPF], creating
ms.assetid: 1defbb78-b8e7-4c0e-b650-576453ac828d
ms.openlocfilehash: 7edb4933ebcc0f0d2cb02754238c2342ee9dd4a2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62031917"
---
# <a name="how-to-create-simple-or-complex-treeviews"></a>방법: 간단하거나 복잡한 TreeView 만들기
이 예제에는 간단 하거나 복잡 한를 만드는 방법을 보여 줍니다 <xref:System.Windows.Controls.TreeView> 컨트롤입니다.  
  
 A <xref:System.Windows.Controls.TreeView> 계층으로 구성 됩니다 <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 포함할 수 있는 간단한 텍스트 문자열과 더 복잡 한 콘텐츠를 같은 <xref:System.Windows.Controls.Button> 컨트롤 또는 <xref:System.Windows.Controls.StackPanel> 포함 된 콘텐츠를 사용 하 여 합니다. 명시적으로 정의할 수는 <xref:System.Windows.Controls.TreeView> 콘텐츠 또는 데이터 원본에서 콘텐츠를 제공할 수 있습니다. 이 항목에서는 이러한 개념의 예제를 제공합니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 의 속성을 <xref:System.Windows.Controls.TreeViewItem> 콘텐츠를 포함 하는 <xref:System.Windows.Controls.TreeView> 해당 항목에 대해 표시 됩니다. A <xref:System.Windows.Controls.TreeViewItem> 수도 있습니다 <xref:System.Windows.Controls.TreeViewItem> 자식 요소와 컨트롤 사용 하 여 이러한 하위 요소를 정의할 수는 <xref:System.Windows.Controls.ItemsControl.Items%2A> 속성입니다.  
  
 다음 예제에서는 명시적으로 정의 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.TreeViewItem> 설정 하 여 콘텐츠를 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 속성을 텍스트 문자열입니다.  
  
 [!code-xaml[TreeViewSimple#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#1)]  
  
 다음 예제에서는 자식 요소를 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.TreeViewItem> 정의한 <xref:System.Windows.Controls.ItemsControl.Items%2A> 된 <xref:System.Windows.Controls.Button> 컨트롤입니다.  
  
 [!code-xaml[TreeViewSimple#3](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#3)]  
  
 다음 예제에서는 만드는 방법을 보여 줍니다.는 <xref:System.Windows.Controls.TreeView> 여기서는 <xref:System.Windows.Data.XmlDataProvider> 제공 <xref:System.Windows.Controls.TreeViewItem> 콘텐츠 및 <xref:System.Windows.HierarchicalDataTemplate> 콘텐츠의 모양을 정의 합니다.  
  
 [!code-xaml[TreeViewSimple#6](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#6)]  
  
 [!code-xaml[TreeViewSimple#7](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#7)]  
  
 [!code-xaml[TreeViewSimple#5](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#5)]  
  
 다음 예제에서는 만드는 방법을 보여 줍니다.는 <xref:System.Windows.Controls.TreeView> 여기서는 <xref:System.Windows.Controls.TreeViewItem> 콘텐츠에 포함 된 <xref:System.Windows.Controls.DockPanel> 콘텐츠를 포함 하는 컨트롤입니다.  
  
 [!code-xaml[TreeViewSimple#9](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#9)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.TreeView>
- <xref:System.Windows.Controls.TreeViewItem>
- [TreeView 개요](treeview-overview.md)
- [방법 항목](treeview-how-to-topics.md)
