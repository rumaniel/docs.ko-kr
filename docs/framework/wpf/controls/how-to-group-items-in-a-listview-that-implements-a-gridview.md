---
title: '방법: GridView를 구현하는 ListView의 항목 그룹화'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], grouping items with GridViews
- grouping items in ListViews implementing GridViews [WPF]
- GridView controls [WPF], grouping items
ms.assetid: eebef25b-ddc6-424e-a66d-ea228d1bf33d
ms.openlocfilehash: b3dd6891976a942b299c87fca25e430e9ee59a51
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910275"
---
# <a name="how-to-group-items-in-a-listview-that-implements-a-gridview"></a>방법: GridView를 구현하는 ListView의 항목 그룹화
항목 그룹을 표시 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.GridView> 의 보기 모드를 <xref:System.Windows.Controls.ListView> 제어 합니다.  
  
## <a name="example"></a>예제  
 항목 그룹을 표시 하는 <xref:System.Windows.Controls.ListView>, 정의 <xref:System.Windows.Data.CollectionViewSource>합니다. 에서는 다음 예제는 <xref:System.Windows.Data.CollectionViewSource> 값에 따라 데이터 항목을 그룹화 하는 `Catalog` 데이터 필드입니다.  
  
 [!code-xaml[GridViewWithGroups#GroupingCollectionViewSource](~/samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#groupingcollectionviewsource)]  
  
 다음 예제에서는 합니다 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 에 대 한는 <xref:System.Windows.Controls.ListView> 에 <xref:System.Windows.Data.CollectionViewSource> 앞의 예제를 정의 하는 합니다. 이 예제에서는 또한 정의 <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> 구현 하는 <xref:System.Windows.Controls.Expander> 컨트롤입니다.  
  
 [!code-xaml[GridViewWithGroups#ListViewGroups](~/samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewgroups)]  
[!code-xaml[GridViewWithGroups#ListViewEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewend)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [방법 항목](listview-how-to-topics.md)
- [ListView 개요](listview-overview.md)
- [GridView 개요](gridview-overview.md)
