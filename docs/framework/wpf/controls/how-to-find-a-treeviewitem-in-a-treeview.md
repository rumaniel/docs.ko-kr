---
title: '방법: TreeView에서 TreeViewItem 찾기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TreeView control [WPF], finding a TreeViewItem
- TreeViewItem [WPF], finding
ms.assetid: 72ecd40c-3939-4e01-b617-5e9daa6074d9
ms.openlocfilehash: ad72c7a7fb11dfe605db4119dde831b47dd7c5a4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962091"
---
# <a name="how-to-find-a-treeviewitem-in-a-treeview"></a>방법: TreeView에서 TreeViewItem 찾기
컨트롤 <xref:System.Windows.Controls.TreeView> 은 계층적 데이터를 표시 하는 편리한 방법을 제공 합니다. 이 데이터 소스 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 에 바인딩되어 있으면 속성을 통해 선택 된 데이터 개체를 신속 하 게 검색할 수 있습니다. <xref:System.Windows.Controls.TreeView> 일반적으로 기본 데이터 개체를 사용 하는 것이 좋지만, 경우에 따라 포함 <xref:System.Windows.Controls.TreeViewItem>된 데이터를 프로그래밍 방식으로 조작 해야 할 수도 있습니다. 예를 들어를 프로그래밍 방식으로 확장 <xref:System.Windows.Controls.TreeViewItem>하거나 <xref:System.Windows.Controls.TreeView>에서 다른 항목을 선택 해야 할 수 있습니다.  
  
 특정 데이터 개체가 <xref:System.Windows.Controls.TreeViewItem> 포함 된를 찾으려면 <xref:System.Windows.Controls.TreeView>의 각 수준을 트래버스 해야 합니다. 의 항목을 가상화 <xref:System.Windows.Controls.TreeView> 하 여 성능을 향상 시킬 수도 있습니다. 항목이 가상화 될 수 있는 경우에도에서 데이터 개체가 포함 되어 있는지 <xref:System.Windows.Controls.TreeViewItem> 여부를 확인 해야 합니다.  
  
## <a name="example"></a>예제  
  
## <a name="description"></a>Description  
 다음 예에서는에서 <xref:System.Windows.Controls.TreeView> 특정 개체를 검색 하 고 포함 하 <xref:System.Windows.Controls.TreeViewItem>는 개체를 반환 합니다. 이 예제에서는 자식 항목 <xref:System.Windows.Controls.TreeViewItem> 을 검색할 수 있도록 각가 인스턴스화되기를 확인 합니다. 이 예제는에서 가상화 된 <xref:System.Windows.Controls.TreeView> 항목을 사용 하지 않는 경우에도 작동 합니다.  
  
> [!NOTE]
> 다음 예에서는 기본 데이터 모델 <xref:System.Windows.Controls.TreeView>에 관계 없이 모든에 대해 작업을 수행 하 고 <xref:System.Windows.Controls.TreeViewItem> 개체가 검색 될 때까지 검색 합니다. 성능을 향상 시키는 또 다른 방법은 지정 된 개체에 대 한 데이터 모델을 검색 하 고 데이터 계층 내에서 해당 위치를 추적 한 다음 <xref:System.Windows.Controls.TreeViewItem> <xref:System.Windows.Controls.TreeView>에서 해당의 해당 위치를 확인 하는 것입니다. 그러나 성능을 향상 시키는 기술은 데이터 모델에 대 한 지식이 필요 하며 지정 <xref:System.Windows.Controls.TreeView>된에 대해 일반화 될 수 없습니다.  
  
## <a name="code"></a>코드  
 [!code-csharp[TreeViewFindTVI#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[TreeViewFindTVI#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#1)]  
  
 이전 코드는 라는 <xref:System.Windows.Controls.VirtualizingStackPanel> `BringIntoView`메서드를 노출 하는 사용자 지정를 사용 합니다. 다음 코드에서는 사용자 지정 <xref:System.Windows.Controls.VirtualizingStackPanel>를 정의 합니다.  
  
 [!code-csharp[TreeViewFindTVI#2](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#2)]
 [!code-vb[TreeViewFindTVI#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#2)]  
  
 다음 XAML에서는 사용자 지정 <xref:System.Windows.Controls.TreeView> <xref:System.Windows.Controls.VirtualizingStackPanel>를 사용 하는를 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[TreeViewFindTVI#3](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml#3)]  
  
## <a name="see-also"></a>참고자료

- [TreeView의 성능 개선](how-to-improve-the-performance-of-a-treeview.md)
