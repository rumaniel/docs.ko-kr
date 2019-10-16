---
title: GridView 개요
ms.date: 03/30/2017
helpviewer_keywords:
- GridView view mode [WPF]
- ListView controls [WPF], GridView view mode
- controls [WPF], ListView
ms.assetid: b2d02267-32b3-40ce-8e9f-06972d8749d9
ms.openlocfilehash: 6da556296679de1161f609a7731c6fbf14e94730
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966476"
---
# <a name="gridview-overview"></a>GridView 개요
<xref:System.Windows.Controls.GridView>보기 모드는 <xref:System.Windows.Controls.ListView> 컨트롤에 대 한 보기 모드 중 하나입니다. <xref:System.Windows.Controls.GridView> 클래스와 지원 클래스를 사용 하면 일반적으로 단추를 대화형 열 헤더로 사용 하는 테이블에서 항목 컬렉션을 볼 수 있습니다. 이 항목에서는 <xref:System.Windows.Controls.GridView> 클래스를 소개 하 고 사용을 간략하게 설명 합니다.  

<a name="DefiningaListViewthatusesGridViewView"></a>   
## <a name="what-is-a-gridview-view"></a>GridView 보기란?  
 뷰 <xref:System.Windows.Controls.GridView> 모드는 데이터 필드를 열에 바인딩하고 필드를 식별 하는 열 머리글을 표시 하 여 데이터 항목 목록을 표시 합니다. 기본 <xref:System.Windows.Controls.GridView> 스타일은 단추를 열 머리글로 구현 합니다. 열 머리글에 대 한 단추를 사용 하 여 중요 한 사용자 상호 작용 기능을 구현할 수 있습니다. 예를 들어 사용자는 열 머리글을 클릭 하 여 <xref:System.Windows.Controls.GridView> 특정 열의 내용에 따라 데이터를 정렬할 수 있습니다.  
  
> [!NOTE]
> 열 머리글에를 <xref:System.Windows.Controls.GridView> 사용 하는 단추 컨트롤은에서 <xref:System.Windows.Controls.Primitives.ButtonBase>파생 됩니다.  
  
 다음 그림에서는 <xref:System.Windows.Controls.ListView> 콘텐츠 보기 <xref:System.Windows.Controls.GridView> 를 보여 줍니다.  
    
 ![ListView 콘텐츠의 GridView 보기를 보여 주는 스크린샷](./media/gridview-overview/styled-listview-content.png)  
  
 <xref:System.Windows.Controls.GridView>열은 <xref:System.Windows.Controls.GridViewColumn> 개체로 표시 되며 해당 내용에 맞게 자동으로 크기가 조정 될 수 있습니다. 필요에 따라를 특정 너비로 명시적 <xref:System.Windows.Controls.GridViewColumn> 으로 설정할 수 있습니다. 열 헤더 사이에 위치 조정 막대를 끌어와 열의 크기를 조정할 수 있습니다. 에서이 기능이 기본적으로 제공 <xref:System.Windows.Controls.GridView>되므로 열을 동적으로 추가, 제거, 바꾸기 및 다시 정렬할 수도 있습니다. 그러나는 표시 되는 데이터를 직접 업데이트할 수없습니다.<xref:System.Windows.Controls.GridView>  
  
 다음 예제에서는 직원 데이터를 표시 하 <xref:System.Windows.Controls.GridView> 는를 정의 하는 방법을 보여 줍니다. 이 예제 <xref:System.Windows.Controls.ListView> 에서는 `EmployeeInfoDataSource` 를로 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>정의 합니다. 데이터를 데이터 범주 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 에 <xref:System.Windows.Controls.GridViewColumn> 바인딩하기 위한 `EmployeeInfoDataSource` 속성 정의입니다.  
  
 [!code-xaml[ListViewCode#ListViewEmployee](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 다음 그림은 이전 예에서 만든 테이블을 보여줍니다. GridView 컨트롤은 System.windows.controls.itemscontrol.itemssource 개체의 데이터를 표시 합니다.
    
 ![GridView를 출력 하는 ListView를 보여 주는 스크린샷](./media/gridview-overview/listview-gridview-output.jpg)  
  
<a name="GridViewLayoutandStyle"></a>   
## <a name="gridview-layout-and-style"></a>GridView 레이아웃 및 스타일  
 의 <xref:System.Windows.Controls.GridViewColumn> 열 셀과 열 머리글의 너비가 같습니다. 기본적으로 각 열은 콘텐츠에 맞게 너비의 크기를 조정합니다. 선택적으로 열을 고정 너비로 설정할 수 있습니다.  
  
 관련 데이터 콘텐츠가 가로 행에 표시됩니다. 예를 들어, 이전 그림에서 각 직원의 성, 이름 및 ID 번호가 가로 행에 표시되므로 집합으로 표시됩니다.  
  
<a name="DefiningandStylingColumnsinaGridView"></a>   
### <a name="defining-and-styling-columns-in-a-gridview"></a>GridView에서 열 정의 및 스타일 지정  
 에 표시할 <xref:System.Windows.Controls.GridViewColumn>데이터 필드를 정의 하는 경우 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>, <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>또는 <xref:System.Windows.Controls.GridViewColumn.CellTemplateSelector%2A> 속성을 사용 합니다. 속성 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 은 템플릿 속성 중 하나 보다 우선 적용 됩니다.  
  
 열에서 콘텐츠의 맞춤을 지정 하는 <xref:System.Windows.Controls.GridView>, 정의 <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>합니다. 사용 하지 마십시오는 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 및 <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> 속성에 대 한 <xref:System.Windows.Controls.ListView> 사용 하 여 표시 되는 콘텐츠를 <xref:System.Windows.Controls.GridView>입니다.  
  
 열 머리글에 대 한 템플릿 및 스타일 속성을 지정 하려면 <xref:System.Windows.Controls.GridView>, <xref:System.Windows.Controls.GridViewColumn>및 <xref:System.Windows.Controls.GridViewColumnHeader> 클래스를 사용 합니다. 자세한 내용은 [GridView 열 헤더 스타일 및 템플릿 개요](gridview-column-header-styles-and-templates-overview.md)를 참조하세요.  
  
<a name="AddingVisualElementstoaGridViewView"></a>   
### <a name="adding-visual-elements-to-a-gridview"></a>GridView에 시각적 요소 추가  
 <xref:System.Windows.Controls.CheckBox> <xref:System.Windows.Controls.GridView> 및 컨트롤과같은시각적요소를뷰모드에추가하려면템플릿또는스타일을사용합니다.<xref:System.Windows.Controls.Button>  
  
 시각적 요소를 데이터 항목으로 명시적으로 정의 하는 경우에는 <xref:System.Windows.Controls.GridView>한 번만 표시 될 수 있습니다. 요소에는 부모가 하나뿐일 수 있기 때문에 이 제한사항이 존재하고, 시각적 트리에 한 번만 표시될 수 있습니다.  
  
<a name="StylingRowsinaGridViewView"></a>   
### <a name="styling-rows-in-a-gridview"></a>GridView의 행 스타일 지정  
 및 클래스를 사용 하 여의 행을 서식 지정 하 <xref:System.Windows.Controls.GridView>고 표시 합니다. <xref:System.Windows.Controls.GridViewHeaderRowPresenter> <xref:System.Windows.Controls.GridViewRowPresenter> <xref:System.Windows.Controls.GridView> 뷰 모드에서 행의 스타일을 만드는 방법에 대 한 예는 [GridView를 구현 하는 ListView의 행 스타일](how-to-style-a-row-in-a-listview-that-implements-a-gridview.md)표시를 참조 하세요.  
  
<a name="AlignmentIssuesWhenUsingItemContainerStyle"></a>   
### <a name="alignment-issues-when-you-use-itemcontainerstyle"></a>ItemContainerStyle을 사용할 때 맞춤 문제  
 열 머리글과 셀 간의 맞춤 문제를 방지 하려면 속성을 설정 하거나의 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>항목 너비에 영향을 주는 템플릿을 지정 하지 마십시오. 예를 들어 <xref:System.Windows.FrameworkElement.Margin%2A> , 속성을 설정 하거나 <xref:System.Windows.Controls.ListView> 컨트롤에 정의 <xref:System.Windows.Controls.ControlTemplate> 된에를 <xref:System.Windows.Controls.CheckBox> 추가 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 하는를 지정 하지 마십시오. 대신 뷰 모드를 <xref:System.Windows.Controls.GridView> 정의 하는 클래스에서 직접 열 너비에 영향을 주는 속성 및 템플릿을 지정 합니다.  
  
 <xref:System.Windows.Controls.CheckBox> 예를 들어 <xref:System.Windows.Controls.GridView> <xref:System.Windows.DataTemplate> <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> 뷰모드<xref:System.Windows.DataTemplate>의 행에를 추가 하려면를에 추가 하고속성을로설정합니다.<xref:System.Windows.Controls.CheckBox>  
  
<a name="InteractingwithaGridViewControl"></a>   
## <a name="user-interactions-with-a-gridview"></a>GridView와의 사용자 상호 작용  
 응용 프로그램에서를 <xref:System.Windows.Controls.GridView> 사용 하는 경우 사용자는와 상호 작용 하 고 <xref:System.Windows.Controls.GridView>의 서식을 수정할 수 있습니다. 예를 들어, 열을 다시 정렬하고, 열의 크기를 조정하며, 테이블에서 항목을 선택하고, 콘텐츠를 스크롤할 수 있습니다. 사용자가 열 헤더 단추를 클릭하면 응답하는 이벤트 처리기도 정의할 수 있습니다. 이벤트 처리기는 열 내용에 <xref:System.Windows.Controls.GridView> 따라에 표시 되는 데이터를 정렬 하는 등의 작업을 수행할 수 있습니다.  
  
 다음 목록에서는 사용자 상호 작용에를 사용 하 <xref:System.Windows.Controls.GridView> 는 기능에 대해 자세히 설명 합니다.  
  
- **끌어서 놓기 메서드를 사용하여 열을 다시 정렬.**  
  
     사용자는 열 머리글 위에 있는 <xref:System.Windows.Controls.GridView> 동안 마우스 왼쪽 단추를 누른 다음 해당 열을 새 위치로 끌어의 열 순서를 바꿀 수 있습니다. 사용자가 열 헤더를 끌어오는 동안 헤더의 부동 버전과 함께 열을 삽입할 위치를 표시하는 검은 실선이 표시됩니다.  
  
     헤더의 부동 버전에 대 한 기본 스타일을 <xref:System.Windows.Controls.ControlTemplate> 수정 하려면 <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> 속성이로 <xref:System.Windows.Controls.GridViewColumnHeaderRole.Floating>설정 될 때 트리거되는 <xref:System.Windows.Controls.GridViewColumnHeader> 형식에 대해를 지정 합니다. 자세한 내용은 [끌어 온 GridView 열 헤더의 스타일 만들기](how-to-create-a-style-for-a-dragged-gridview-column-header.md)를 참조하세요.  
  
- **콘텐츠에 맞게 열의 크기 조정.**  
  
     콘텐츠에 맞게 열의 크기를 조정하려면 열 헤더의 오른쪽에 있는 위치 조정 막대를 두 번 클릭할 수 있습니다.  
  
    > [!NOTE]
    > <xref:System.Windows.Controls.GridViewColumn.Width%2A> 속성을로 `Double.NaN` 설정 하 여 동일한 효과를 얻을 수 있습니다.  
  
- **행 항목 선택.**  
  
     사용자는에서 하나 이상의 항목을 <xref:System.Windows.Controls.GridView>선택할 수 있습니다.  
  
     선택한 항목 <xref:System.Windows.Style> 의를 변경 하려면 [ListView에서 트리거를 사용 하 여 선택한 항목의 스타일](how-to-use-triggers-to-style-selected-items-in-a-listview.md)을 지정할 수 있습니다.  
  
- **처음에 화면에 표시되지 않는 콘텐츠를 보려면 스크롤.**  
  
     의 <xref:System.Windows.Controls.GridView> 크기가 작아서 모든 항목을 표시할 수 없는 경우 사용자는 <xref:System.Windows.Controls.ScrollViewer> 컨트롤에서 제공 하는 스크롤 막대를 사용 하 여 가로 또는 세로로 스크롤할 수 있습니다. 모든 콘텐츠가 특정 방향으로 표시 되는 경우 이숨겨집니다.<xref:System.Windows.Controls.Primitives.ScrollBar> 열 표제는 세로 스크롤 막대로는 스크롤되지 않지만 가로로는 스크롤됩니다.  
  
- **열 표제 단추를 클릭하여 열과 상호 작용.**  
  
     열 헤더 단추를 클릭하면, 정렬 알고리즘을 제공한 경우 열에 표시되는 데이터를 정렬할 수 있습니다.  
  
     정렬 알고리즘과 같은 기능 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 을 제공 하기 위해 열 머리글 단추에 대 한 이벤트를 처리할 수 있습니다. 단일 열 머리글 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 에 대 한 이벤트를 처리 하려면 <xref:System.Windows.Controls.GridViewColumnHeader>에 대 한 이벤트 처리기를 설정 합니다. 모든 열 머리글에 대 한 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트를 처리 하는 이벤트 처리기를 설정 하려면 <xref:System.Windows.Controls.ListView> 컨트롤에 대 한 처리기를 설정 합니다.  
  
<a name="Obtaining_Other_Custom_Views"></a>   
## <a name="obtaining-other-custom-views"></a>다른 사용자 지정 보기 가져오기  
 추상 클래스에서 파생 되는 <xref:System.Windows.Controls.ListView> 클래스는클래스의가능한보기모드중하나일뿐입니다.<xref:System.Windows.Controls.GridView> <xref:System.Windows.Controls.ViewBase> 클래스에서 파생 하 여에 대 <xref:System.Windows.Controls.ListView> 한 다른 사용자 지정 뷰를 만들 수 있습니다. <xref:System.Windows.Controls.ViewBase> 사용자 지정 보기 모드의 예는 [ListView의 사용자 지정 뷰 모드 만들기](how-to-create-a-custom-view-mode-for-a-listview.md)를 참조하세요.  
  
<a name="GridViewSupportingClasses"></a>   
## <a name="gridview-supporting-classes"></a>GridView 지원 클래스  
 다음 클래스는 뷰 모드 <xref:System.Windows.Controls.GridView> 를 지원 합니다.  
  
- <xref:System.Windows.Controls.GridViewColumn>  
  
- <xref:System.Windows.Controls.GridViewColumnHeader>  
  
- <xref:System.Windows.Controls.GridViewRowPresenter>  
  
- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>  
  
- <xref:System.Windows.Controls.GridViewColumnCollection>  
  
- <xref:System.Windows.Controls.GridViewColumnHeaderRole>  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.ListViewItem>
- <xref:System.Windows.Controls.GridViewColumn>
- <xref:System.Windows.Controls.GridViewColumnHeader>
- <xref:System.Windows.Controls.GridViewRowPresenter>
- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>
- <xref:System.Windows.Controls.ViewBase>
- [ListView 개요](listview-overview.md)
- [헤더를 클릭하면 GridView 열 정렬](how-to-sort-a-gridview-column-when-a-header-is-clicked.md)
- [방법 항목](listview-how-to-topics.md)
