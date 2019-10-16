---
title: '방법: 템플릿을 사용하여 GridView를 사용하는 ListView의 스타일 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], styling
ms.assetid: 94bf964b-96c8-4bdf-a0c3-f5271b7cb565
ms.openlocfilehash: 1caa652c4a2a3a7d0a8d40fe703df7a3e8038c9b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699125"
---
# <a name="how-to-use-templates-to-style-a-listview-that-uses-gridview"></a>방법: 템플릿을 사용하여 GridView를 사용하는 ListView의 스타일 지정
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.DataTemplate> 및 <xref:System.Windows.Style> 의 모양을 지정 하는 개체를 <xref:System.Windows.Controls.ListView> 사용 하는 컨트롤을 <xref:System.Windows.Controls.GridView> 보기 모드입니다.  
  
## <a name="example"></a>예제  
 다음 예제에 나온 <xref:System.Windows.Style> 하 고 <xref:System.Windows.DataTemplate> 에 대 한 열 머리글의 모양을 사용자 지정 하는 개체는 <xref:System.Windows.Controls.GridViewColumn>합니다.  
  
 [!code-xaml[ListViewTemplate#GridViewHeaderStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheaderstyle)]  
  
 [!code-xaml[ListViewTemplate#GridViewHeaderTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheadertemplate)]  
  
 다음 예제에서는이 방법을 사용 하는 방법을 보여 줍니다 <xref:System.Windows.Style> 하 고 <xref:System.Windows.DataTemplate> 설정할 개체를 <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> 및 <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> 의 속성을 <xref:System.Windows.Controls.GridViewColumn>합니다. <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 속성 열 셀의 내용을 정의 합니다.  
  
 [!code-xaml[ListViewTemplate#GridViewColumnTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcolumntemplate)]  
  
 <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> 하 고 <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> 에 대 한 열 헤더 모양을 사용자 지정 하는 데 사용할 수 있는 여러 속성 중 두는 <xref:System.Windows.Controls.GridView> 컨트롤입니다. 자세한 내용은 [GridView 열 헤더 스타일 및 템플릿 개요](gridview-column-header-styles-and-templates-overview.md)를 참조하세요.  
  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.DataTemplate> 셀의 모양을 사용자 지정 하는 <xref:System.Windows.Controls.GridViewColumn>합니다.  
  
 [!code-xaml[ListViewTemplate#GridViewCellTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 다음 예제에서는이 사용 하는 방법을 보여 줍니다 <xref:System.Windows.DataTemplate> 의 콘텐츠를 정의 하는 <xref:System.Windows.Controls.GridViewColumn> 셀입니다. 이 템플릿을 대신 사용 합니다 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 이전에 표시 되는 속성 <xref:System.Windows.Controls.GridViewColumn> 예제입니다.  
  
 [!code-xaml[ListViewTemplate#CellTemplateProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [GridView 개요](gridview-overview.md)
- [방법 항목](listview-how-to-topics.md)
- [ListView 개요](listview-overview.md)
