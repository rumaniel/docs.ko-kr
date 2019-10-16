---
title: '방법: GridView를 구현하는 ListView 행의 스타일 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- GridView controls [WPF], styling rows
- styling rows in ListViews implementing GridViews [WPF]
- ListView controls [WPF], styling rows with GridViews
ms.assetid: 2e406ba2-70a0-4e62-841f-0934859de76e
ms.openlocfilehash: 9af8d10c7db2d3bbe8b9443402cbb1cfeaa7edb3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052016"
---
# <a name="how-to-style-a-row-in-a-listview-that-implements-a-gridview"></a>방법: GridView를 구현하는 ListView 행의 스타일 지정
행 스타일을 지정 하는 방법을 보여주는이 예제는 <xref:System.Windows.Controls.ListView> 구현 하는 컨트롤을 <xref:System.Windows.Controls.GridView> <xref:System.Windows.Controls.ListView.View%2A> 모드입니다.  
  
## <a name="example"></a>예제  
 행 스타일 지정할 수 있습니다는 <xref:System.Windows.Controls.ListView> 설정 하 여 컨트롤을 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 에 <xref:System.Windows.Controls.ListView> 컨트롤. 로 표현 되는 해당 항목에 대 한 스타일 설정 <xref:System.Windows.Controls.ListViewItem> 개체입니다. 합니다 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 참조는 <xref:System.Windows.Controls.ControlTemplate> 행 내용을 표시 하는 데 사용 되는 개체입니다.  
  
 다음 예제가 포함되어 있는 원래의 전체 샘플에서는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 데이터베이스에 저장된 곡 모음집 정보를 표시합니다. 데이터베이스의 각 곡에는 순위 필드가 있으며 이 필드의 값은 곡 정보 행의 표시 방법을 지정합니다.  
  
 다음 예제에서는 정의 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 에 대 한는 <xref:System.Windows.Controls.ListViewItem> 곡 모음집의 곡을 나타내는 개체입니다. 합니다 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 참조가 <xref:System.Windows.Controls.ControlTemplate> 곡 정보 행을 표시 하는 방법을 지정 하는 개체입니다.  
  
 [!code-xaml[ListViewItemStyleSnippet#ItemContainerStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#itemcontainerstyle)]  
  
 에서는 다음 예제는 <xref:System.Windows.Controls.ControlTemplate> 텍스트 문자열을 추가 하는 `"Strongly Recommended"` 행입니다. 이 서식 파일에서 참조 되는 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 곡의 5 (5)의 값이 표시 됩니다. <xref:System.Windows.Controls.ControlTemplate> 포함를 <xref:System.Windows.Controls.GridViewRowPresenter> 정의 된 대로 열에서 행의 내용을 배치 하는 개체는 <xref:System.Windows.Controls.GridView> 보기 모드입니다.  
  
 [!code-xaml[ListViewItemStyleSnippet#ControlTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#controltemplate)]  
  
 다음 예제에서는 정의 <xref:System.Windows.Controls.GridView>합니다.  
  
 [!code-xaml[ListViewItemStyleSnippet#GridView](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#gridview)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [방법 항목](listview-how-to-topics.md)
- [ListView 개요](listview-overview.md)
- [스타일 지정 및 템플릿](styling-and-templating.md)
