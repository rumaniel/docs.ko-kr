---
title: ListView 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], ListView
- ListView controls [WPF], about ListView control
ms.assetid: 989e12b0-260e-4570-95c6-489284003ce2
ms.openlocfilehash: 0148ded31f1c637f533f8e80427672a79ef05e02
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64621274"
---
# <a name="listview-overview"></a>ListView 개요
<xref:System.Windows.Controls.ListView> 컨트롤은 데이터 항목 집합을 다른 레이아웃 보기에 표시 하기 위한 인프라를 제공 합니다. 예를 들어 사용자가 데이터 항목을 표에 표시하고 해당 열을 정렬해야 할 수도 있습니다.  

<a name="WhatisaListView"></a>   
## <a name="what-is-a-listview"></a>ListView란?  
 합니다 <xref:System.Windows.Controls.ListView> 컨트롤은는 <xref:System.Windows.Controls.ItemsControl> 에서 파생 된 <xref:System.Windows.Controls.ListBox>합니다. 일반적으로 해당 데이터 컬렉션의 멤버인 항목과 표현 <xref:System.Windows.Controls.ListViewItem> 개체입니다. A <xref:System.Windows.Controls.ListViewItem> 되는 <xref:System.Windows.Controls.ContentControl> 단일 자식 요소만 포함 될 수 있습니다. 하지만 자식 요소는 모든 시각적 요소가 될 수 있습니다.  
  
<a name="DefiningaListViewView"></a>   
## <a name="defining-a-view-mode-for-a-listview"></a>ListView의 뷰 모드 정의  
 콘텐츠에 대 한 보기 모드를 지정 하는 <xref:System.Windows.Controls.ListView> 설정한 컨트롤은 <xref:System.Windows.Controls.ListView.View%2A> 속성. 뷰 모드 중 하나입니다 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 제공은 <xref:System.Windows.Controls.GridView>, 사용자 지정 가능한 열이 있는 테이블의 데이터 항목의 컬렉션을 표시 하는 합니다.  
  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.GridView> 에 대 한는 <xref:System.Windows.Controls.ListView> 직원 정보를 표시 하는 컨트롤입니다.  
  
 [!code-xaml[ListViewCode#ListViewEmployee](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 다음 그림에서는 이전 예제의 데이터가 표시되는 방법을 보여 줍니다.  
  
 ![GridView 출력이 있는 ListView를 보여주는 스크린샷.](./media/gridview-overview/listview-gridview-output.jpg)  
  
 상속 되는 클래스를 정의 하 여 사용자 지정 뷰 모드를 만들 수는 <xref:System.Windows.Controls.ViewBase> 클래스입니다. <xref:System.Windows.Controls.ViewBase> 클래스는 사용자 지정 보기를 생성 해야 하는 인프라를 제공 합니다. 사용자 지정 뷰를 만드는 방법에 대한 자세한 내용은 [ListView의 사용자 지정 뷰 모드 만들기](how-to-create-a-custom-view-mode-for-a-listview.md)를 참조하세요.  
  
<a name="BindingDatatoaListView"></a>   
## <a name="binding-data-to-a-listview"></a>ListView에 데이터 바인딩  
 사용 합니다 <xref:System.Windows.Controls.ItemsControl.Items%2A> 및 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 에 대 한 항목을 지정 하는 속성을 <xref:System.Windows.Controls.ListView> 제어 합니다. 다음 예제에서는 합니다 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 속성 이라고 하는 데이터 컬렉션을 `EmployeeInfoDataSource`입니다.  
  
 [!code-xaml[ListViewCode#ItemsSource](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#itemssource)]  
  
 에 <xref:System.Windows.Controls.GridView>, <xref:System.Windows.Controls.GridViewColumn> 개체는 지정 된 데이터 필드에 바인딩합니다. 다음 예제에서는 <xref:System.Windows.Controls.GridViewColumn> 개체를 지정 하 여 데이터 필드를 <xref:System.Windows.Data.Binding> 에 대 한는 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 속성입니다.  
  
 [!code-csharp[ListViewCode#GridViewColumnProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml.cs#gridviewcolumnproperties)]
 [!code-vb[ListViewCode#GridViewColumnProperties](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCode/visualbasic/window1.xaml.vb#gridviewcolumnproperties)]
 [!code-xaml[ListViewCode#GridViewColumnProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#gridviewcolumnproperties)]  
  
 지정할 수도 있습니다는 <xref:System.Windows.Data.Binding> 의 일부로 <xref:System.Windows.DataTemplate> 열의 셀 스타일을 사용 하는 정의 합니다. 다음 예에서 <xref:System.Windows.DataTemplate> 로 식별 되는 <xref:System.Windows.ResourceKey> 설정 합니다 <xref:System.Windows.Data.Binding> 에 대 한를 <xref:System.Windows.Controls.GridViewColumn>입니다. 이 예제에서는 정의 하지 않는 참고 합니다 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 수행 하므로 지정 된 바인딩 보다 우선 하므로 <xref:System.Windows.DataTemplate>합니다.  
  
 [!code-xaml[ListViewTemplate#GridViewCellTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 [!code-xaml[ListViewTemplate#CellTemplateProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
<a name="StylingaListView"></a>   
## <a name="styling-a-listview-that-implements-a-gridview"></a>GridView를 구현하는 ListView에 스타일 지정  
 합니다 <xref:System.Windows.Controls.ListView> 컨트롤에 <xref:System.Windows.Controls.ListViewItem> 표시 되는 데이터 항목을 나타내는 개체입니다. 다음 속성을 사용하여 데이터 항목의 콘텐츠 및 스타일을 정의할 수 있습니다.  
  
- 에 <xref:System.Windows.Controls.ListView> 컨트롤을 사용 하 여 합니다 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>, <xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A>, 및 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 속성입니다.  
  
- 에 <xref:System.Windows.Controls.ListViewItem> 컨트롤을 사용 합니다 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 및 <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A> 속성.  
  
 에 있는 셀 사이의 맞춤 문제를 방지 하려면를 <xref:System.Windows.Controls.GridView>를 사용 하지 마십시오는 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 에 있는 항목의 너비에 영향을 주는 콘텐츠를 추가 하거나 속성을 설정 하는 <xref:System.Windows.Controls.ListView>. 설정 하면 정렬 문제가 발생할 수 있습니다 예를 들어 합니다 <xref:System.Windows.FrameworkElement.Margin%2A> 속성에는 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>합니다. 항목 너비에 영향을 주는 콘텐츠를 정의 하거나 속성을 지정 하는 <xref:System.Windows.Controls.GridView>의 속성을 사용 합니다 <xref:System.Windows.Controls.GridView> 클래스 및 관련된 클래스를 같은 <xref:System.Windows.Controls.GridViewColumn>합니다.  
  
 사용 하는 방법에 대 한 자세한 내용은 <xref:System.Windows.Controls.GridView> 지원 클래스를 살펴보고 [GridView 개요](gridview-overview.md)합니다.  
  
 정의 하는 경우는 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 에 대 한를 <xref:System.Windows.Controls.ListView> 제어 하 고도 정의 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>를 포함 해야 합니다는 <xref:System.Windows.Controls.ContentPresenter> 되려면에서 스타일에서를 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 제대로 작동 하려면.  
  
 사용 하지 마십시오는 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 및 <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> 속성에 대 한 <xref:System.Windows.Controls.ListView> 사용 하 여 표시 되는 콘텐츠를 <xref:System.Windows.Controls.GridView>입니다. 열에서 콘텐츠의 맞춤을 지정 하는 <xref:System.Windows.Controls.GridView>, 정의 <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>합니다.  
  
<a name="UsingtheSameViewMoreThanOnce"></a>   
## <a name="sharing-the-same-view-mode"></a>같은 뷰 모드 공유  
 두 <xref:System.Windows.Controls.ListView> 컨트롤 동시에 같은 뷰 모드를 공유할 수 없습니다. 둘 이상의 같은 뷰 모드를 사용 하려는 경우 <xref:System.Windows.Controls.ListView> 제어, 예외가 발생 합니다.  
  
 둘 이상의 동시에 사용할 수 있는 뷰 모드를 지정 하려면 <xref:System.Windows.Controls.ListView>, 템플릿 또는 스타일을 사용 합니다.
  
<a name="CreatingaCustomView"></a>   
## <a name="creating-a-custom-view-mode"></a>사용자 지정 보기 모드 만들기  
 같은 뷰를 사용자 지정할 <xref:System.Windows.Controls.GridView> 에서 파생 되는 <xref:System.Windows.Controls.ViewBase> 표현 된 데이터 항목을 표시 하기 위한 도구를 제공 하는 클래스를 추상 <xref:System.Windows.Controls.ListViewItem> 개체입니다.    
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.GridView>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.ListViewItem>
- <xref:System.Windows.Data.Binding>
- [GridView 개요](gridview-overview.md)
- [방법 항목](listview-how-to-topics.md)
- [컨트롤](../advanced/optimizing-performance-controls.md)
