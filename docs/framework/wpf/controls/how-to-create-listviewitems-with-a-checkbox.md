---
title: '방법: CheckBox를 사용하여 ListViewItems 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], ListView
- controls [WPF], CheckBox
- ListView controls [WPF], CheckBox controls
- CheckBox control [WPF], ListView control
ms.assetid: f6d66c7f-906c-4f65-a55a-0ede9d00e26a
ms.openlocfilehash: b09d5ad11b0961febf524cec1e19cb1e59832e44
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910782"
---
# <a name="how-to-create-listviewitems-with-a-checkbox"></a>방법: CheckBox를 사용하여 ListViewItems 만들기
이 예제에서는 열을 표시 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.CheckBox> 컨트롤을 <xref:System.Windows.Controls.ListView> 사용 하는 컨트롤을 <xref:System.Windows.Controls.GridView>입니다.  
  
## <a name="example"></a>예제  
 포함 된 열을 만들려면 <xref:System.Windows.Controls.CheckBox> 컨트롤을 <xref:System.Windows.Controls.ListView>, 만들기를 <xref:System.Windows.DataTemplate> 포함 하는 <xref:System.Windows.Controls.CheckBox>합니다. 설정한 합니다 <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> 의 <xref:System.Windows.Controls.GridViewColumn> 에 <xref:System.Windows.DataTemplate>합니다.  
  
 다음 예제와 <xref:System.Windows.DataTemplate> 를 포함 하는 <xref:System.Windows.Controls.CheckBox>합니다. 예제를 <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> 의 속성을 <xref:System.Windows.Controls.CheckBox> 에 <xref:System.Windows.Controls.ListBoxItem.IsSelected%2A> 속성 값을 <xref:System.Windows.Controls.ListViewItem> 포함 된. 따라서 경우는 <xref:System.Windows.Controls.ListViewItem> 포함 하는 합니다 <xref:System.Windows.Controls.CheckBox> 을 선택 하면를 <xref:System.Windows.Controls.CheckBox> 확인란이 선택 되어 합니다.  
  
 [!code-xaml[ListViewChkBox#CheckBoxDataTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#checkboxdatatemplate)]  
  
 다음 예제에는 열을 만드는 방법을 보여 줍니다 <xref:System.Windows.Controls.CheckBox> 컨트롤입니다. 예제에서는 열 수 있도록를 <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> 의 속성을 <xref:System.Windows.Controls.GridViewColumn> 에 <xref:System.Windows.DataTemplate>.  
  
 [!code-xaml[ListViewChkBox#GridViewColumnCheckBox](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#gridviewcolumncheckbox)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Control>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [ListView 개요](listview-overview.md)
- [방법 항목](listview-how-to-topics.md)
- [GridView 개요](gridview-overview.md)
