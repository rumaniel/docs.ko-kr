---
title: '방법: 트리거를 사용하여 ListView에서 선택한 항목의 스타일 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], styling
ms.assetid: 1e2bdce0-afe8-4507-9b18-f33de43de25a
ms.openlocfilehash: ad64382b871bae9114a1e63257de3f8595376923
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61696200"
---
# <a name="how-to-use-triggers-to-style-selected-items-in-a-listview"></a>방법: 트리거를 사용하여 ListView에서 선택한 항목의 스타일 지정
정의 하는 방법을 보여 주는이 예제 <xref:System.Windows.Style.Triggers%2A> 에 대 한는 <xref:System.Windows.Controls.ListViewItem> 컨트롤 있도록 속성 값을 <xref:System.Windows.Controls.ListViewItem> 변경을 <xref:System.Windows.Style> 의 <xref:System.Windows.Controls.ListViewItem> 변경에 대 한 응답에서입니다.  
  
## <a name="example"></a>예제  
 원하는 경우는 <xref:System.Windows.Style> 의 <xref:System.Windows.Controls.ListViewItem> 속성 변경에 대 한 응답을 변경 하려면 정의 <xref:System.Windows.Style.Triggers%2A> 에 대 한를 <xref:System.Windows.Style> 변경 합니다.  
  
 다음 예제에서는 정의 <xref:System.Windows.Trigger> 설정 하는 <xref:System.Windows.Controls.Control.Foreground%2A> 속성을 <xref:System.Windows.Media.Brushes.Blue%2A> 변경 합니다 <xref:System.Windows.FrameworkElement.Cursor%2A> 표시할를 <xref:System.Windows.Input.CursorType.Hand> 때를 <xref:System.Windows.UIElement.IsMouseOver%2A> 속성 변경 `true`.  
  
 [!code-xaml[ListViewChkBox#ListViewItemTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersstart)]  
[!code-xaml[ListViewChkBox#Trigger](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#trigger)]  
[!code-xaml[ListViewChkBox#ListViewItemTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersend)]  
  
 다음 예제에서는 정의 <xref:System.Windows.MultiTrigger> 설정 하는 <xref:System.Windows.Controls.Control.Foreground%2A> 의 속성을 <xref:System.Windows.Controls.ListViewItem> 를 <xref:System.Windows.Media.Brushes.Yellow%2A> 경우는 <xref:System.Windows.Controls.ListViewItem> 선택한 항목 이며 키보드 포커스가.  
  
 [!code-xaml[ListViewChkBox#ListViewItemTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersstart)]  
[!code-xaml[ListViewChkBox#MultiTrigger](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#multitrigger)]  
[!code-xaml[ListViewChkBox#ListViewItemTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersend)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Control>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [방법 항목](listview-how-to-topics.md)
- [ListView 개요](listview-overview.md)
- [GridView 개요](gridview-overview.md)
