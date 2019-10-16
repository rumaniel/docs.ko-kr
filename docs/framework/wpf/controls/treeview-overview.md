---
title: TreeView 개요
ms.date: 03/30/2017
helpviewer_keywords:
- expanding node [WPF]
- TreeView control [WPF], about TreeView control
- Control class [WPF], TreeView
ms.assetid: 62212512-5a5c-4864-949e-b6a6a3a52c02
ms.openlocfilehash: c0967aa506b087120c776389c2891ec9e0b0b64d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61761405"
---
# <a name="treeview-overview"></a>TreeView 개요
<xref:System.Windows.Controls.TreeView> 컨트롤은 축소 가능한 노드를 사용 하 여 계층 구조에서 정보를 표시 하는 방법을 제공 합니다. 이 항목에서는 소개 합니다 <xref:System.Windows.Controls.TreeView> 고 <xref:System.Windows.Controls.TreeViewItem> 컨트롤 및 사용 하는 간단한 예제를 제공 합니다.  

<a name="Simple_TreeView_Control"></a>   
## <a name="what-is-a-treeview"></a>TreeView란?  
 <xref:System.Windows.Controls.TreeView> <xref:System.Windows.Controls.ItemsControl> 를 사용 하 여 항목을 중첩 하 <xref:System.Windows.Controls.TreeViewItem> 컨트롤입니다. 다음 예제에서는 <xref:System.Windows.Controls.TreeView>합니다.  
  
 [!code-xaml[TreeViewSnips#EmbeddedTVIs](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#embeddedtvis)]  
  
<a name="Creating_a_TreeView"></a>   
## <a name="creating-a-treeview"></a>TreeView 만들기  
 합니다 <xref:System.Windows.Controls.TreeView> 계층을 포함 하는 컨트롤 <xref:System.Windows.Controls.TreeViewItem> 컨트롤입니다. A <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 <xref:System.Windows.Controls.HeaderedItemsControl> 있는 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 및 <xref:System.Windows.Controls.ItemsControl.Items%2A> 컬렉션.  
  
 정의 하는 경우는 <xref:System.Windows.Controls.TreeView> 를 사용 하 여 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]를 명시적으로 정의할 수 있습니다는 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 의 콘텐츠를 <xref:System.Windows.Controls.TreeViewItem> 컨트롤 및 해당 컬렉션을 구성 하는 항목입니다. 위의 그림에서는 이 메서드를 보여 줍니다.  
  
 지정할 수도 있습니다는 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 데이터 원본 및 다음 지정을 <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> 및 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 정의 하는 <xref:System.Windows.Controls.TreeViewItem> 콘텐츠.  
  
 레이아웃을 정의 하는 <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 사용할 수도 있습니다 <xref:System.Windows.HierarchicalDataTemplate> 개체입니다. 자세한 내용 및 예제는 [SelectedValue, SelectedValuePath 및 SelectedItem 사용](how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)을 참조하세요.  
  
 항목이 없는 경우는 <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 자동으로 묶어야 하 여를 <xref:System.Windows.Controls.TreeViewItem> 제어를 <xref:System.Windows.Controls.TreeView> 컨트롤이 표시 됩니다.  
  
<a name="Expanding_and_Collapsing_a_TreeViewItem"></a>   
## <a name="expanding-and-collapsing-a-treeviewitem"></a>TreeViewItem 확장 및 축소  
 사용자를 확장 하는 경우는 <xref:System.Windows.Controls.TreeViewItem>의 <xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> 속성이 `true`합니다. 또한 확장 하거나 축소할 수는 <xref:System.Windows.Controls.TreeViewItem> 설정 하 여 직접 사용자 개입 없이 <xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> 속성을 `true` (확장) 또는 `false` (축소) 합니다. 이 속성을 변경 하는 경우는 <xref:System.Windows.Controls.TreeViewItem.Expanded> 또는 <xref:System.Windows.Controls.TreeViewItem.Collapsed> 이벤트가 발생 합니다.  
  
 경우는 <xref:System.Windows.FrameworkElement.BringIntoView%2A> 메서드를 호출는 <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 <xref:System.Windows.Controls.TreeViewItem> 와 해당 부모 <xref:System.Windows.Controls.TreeViewItem> 컨트롤 확장. 경우는 <xref:System.Windows.Controls.TreeViewItem> 전체 또는 일부가 표시 되지는 <xref:System.Windows.Controls.TreeView> 볼 수 있도록으로 스크롤합니다.  
  
<a name="TreeViewItem_Selection"></a>   
## <a name="treeviewitem-selection"></a>TreeViewItem 선택  
 클릭할 때를 <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 선택 합니다는 <xref:System.Windows.Controls.TreeViewItem.Selected> 이벤트가 발생 및 해당 <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> 속성이 `true`합니다. <xref:System.Windows.Controls.TreeViewItem> 될 수도 합니다 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 의 <xref:System.Windows.Controls.TreeView> 제어 합니다. 반대로 변경 되 면 선택 항목에서를 <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 해당 <xref:System.Windows.Controls.TreeViewItem.Unselected> 이벤트 발생 및 해당 <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> 속성이 `false`합니다.  
  
 합니다 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 속성에는 <xref:System.Windows.Controls.TreeView> 제어는 읽기 전용 속성은 명시적으로 설정할 수 없습니다 따라서 합니다. <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 클릭할 경우 속성이 설정 되어를 <xref:System.Windows.Controls.TreeViewItem> 컨트롤 때나를 <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> 속성이로 설정 되어 `true` 에 <xref:System.Windows.Controls.TreeViewItem> 컨트롤입니다.  
  
 사용 하 여는 <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> 지정 하는 속성을 <xref:System.Windows.Controls.TreeView.SelectedValue%2A> 의 <xref:System.Windows.Controls.TreeView.SelectedItem%2A>. 자세한 내용은 [SelectedValue, SelectedValuePath 및 SelectedItem 사용](how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)을 참조하세요.  
  
 이벤트 처리기를 등록할 수 있습니다 합니다 <xref:System.Windows.Controls.TreeView.SelectedItemChanged> 선택 된 시기를 확인 하려면 이벤트 <xref:System.Windows.Controls.TreeViewItem> 변경 합니다. 합니다 <xref:System.Windows.RoutedPropertyChangedEventArgs%601> 이벤트 처리기는 다음과 같이 지정 됩니다. 제공 되는 합니다 <xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A>, 이전 선택 항목인 및 <xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>, 현재 선택 항목인 합니다. 애플리케이션 또는 사용자가 이전 또는 현재에 선택한 항목이 없는 경우 두 값은 `null`이 될 수 있습니다.  
  
<a name="TreeView_Style"></a>   
## <a name="treeview-style"></a>TreeView 스타일  
 에 대 한 기본 스타일을 <xref:System.Windows.Controls.TreeView> 컨트롤이 배치 내에서 <xref:System.Windows.Controls.StackPanel> 포함 된 개체는 <xref:System.Windows.Controls.ScrollViewer> 컨트롤입니다. 설정한 경우는 <xref:System.Windows.FrameworkElement.Width%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A> 에 대 한 속성을 <xref:System.Windows.Controls.TreeView>, 이러한 값은 크기를 사용는 <xref:System.Windows.Controls.StackPanel> 표시 하는 개체를 <xref:System.Windows.Controls.TreeView>. 표시할 콘텐츠가 표시 영역 보다 큰 경우는 <xref:System.Windows.Controls.ScrollViewer> 사용자가 스크롤할 수 있도록 자동으로 표시 됩니다는 <xref:System.Windows.Controls.TreeView> 콘텐츠입니다.  
  
 모양을 사용자 지정 하는 <xref:System.Windows.Controls.TreeViewItem> 컨트롤을 <xref:System.Windows.FrameworkElement.Style%2A> 속성을 사용자 지정 <xref:System.Windows.Style>.  
  
 다음 예제에서는 설정 하는 방법을 보여 줍니다를 <xref:System.Windows.Controls.Control.Foreground%2A> 및 <xref:System.Windows.Controls.Control.FontSize%2A> 속성에 대 한 값을 <xref:System.Windows.Controls.TreeViewItem> 사용 하 여 컨트롤을 <xref:System.Windows.FrameworkElement.Style%2A>합니다.  
  
 [!code-xaml[TreeViewSimple#8](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#8)]  
  
<a name="Adding_Images_and_oOther_Content_to_TreeView_Items"></a>   
## <a name="adding-images-and-other-content-to-treeview-items"></a>TreeView 항목에 이미지 및 기타 콘텐츠 추가  
 둘 이상의 개체를 포함할 수 있습니다 합니다 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 의 콘텐츠는 <xref:System.Windows.Controls.TreeViewItem>합니다. 여러 개체를 포함 하도록 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 콘텐츠와 같은 레이아웃 컨트롤 내에서 개체를 포함 합니다는 <xref:System.Windows.Controls.Panel> 또는 <xref:System.Windows.Controls.StackPanel>합니다.  
  
 다음 예제에서는 정의 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 의 <xref:System.Windows.Controls.TreeViewItem> 으로 <xref:System.Windows.Controls.CheckBox> 및 <xref:System.Windows.Controls.TextBlock> 는에 포함 된를 <xref:System.Windows.Controls.DockPanel> 컨트롤입니다.  
  
 [!code-xaml[TreeViewSnips#TVIHeader](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#tviheader)]  
  
 다음 예제에서는 정의 하는 방법을 보여 줍니다를 <xref:System.Windows.DataTemplate> 를 포함 하는 <xref:System.Windows.Controls.Image> 및 <xref:System.Windows.Controls.TextBlock> 에 포함 된를 <xref:System.Windows.Controls.DockPanel> 컨트롤입니다. 사용할 수는 <xref:System.Windows.DataTemplate> 설정 하는 <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> 또는 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 에 대 한는 <xref:System.Windows.Controls.TreeViewItem>합니다.  
  
 [!code-xaml[TreeViewDataBinding#6](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewDataBinding/CSharp/Window1.xaml#6)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.TreeView>
- <xref:System.Windows.Controls.TreeViewItem>
- [방법 항목](treeview-how-to-topics.md)
- [WPF 콘텐츠 모델](wpf-content-model.md)
