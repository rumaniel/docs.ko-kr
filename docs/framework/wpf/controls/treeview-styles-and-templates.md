---
title: TreeView 스타일 및 템플릿
ms.date: 03/30/2017
helpviewer_keywords:
- ControlTemplate [WPF], TreeView
- templates [WPF], TreeView
- parts [WPF], TreeView
- states [WPF], TreeView
- styles [WPF], TreeView
- TreeView [WPF], styles and templates
ms.assetid: a49adb77-0202-4caa-b94a-8bb110d7fa9a
ms.openlocfilehash: 01841bb828594dd4cac0c179d70495fe392c8de5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61761301"
---
# <a name="treeview-styles-and-templates"></a>TreeView 스타일 및 템플릿
이 항목에서는 스타일 및 템플릿에 대해 설명 합니다 <xref:System.Windows.Controls.TreeView> 제어 합니다. 기본값을 수정할 수 있습니다 <xref:System.Windows.Controls.ControlTemplate> 고유한 모양을 제어할 수 있습니다. 자세한 내용은 [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)을 참조하세요.  
  
## <a name="treeview-parts"></a>TreeView 파트  
 <xref:System.Windows.Controls.TreeView> 컨트롤에 명명된 된 파트가 없습니다.  
  
 만들 때를 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.TreeView>, 템플릿에 포함 될 수 있습니다는 <xref:System.Windows.Controls.ItemsPresenter> 내는 <xref:System.Windows.Controls.ScrollViewer>합니다. (합니다 <xref:System.Windows.Controls.ItemsPresenter> 에 각 항목을 표시 합니다 <xref:System.Windows.Controls.TreeView>, <xref:System.Windows.Controls.ScrollViewer> 컨트롤 내에서 스크롤을 사용할 수)입니다.  경우는 <xref:System.Windows.Controls.ItemsPresenter> 의 직접 자식이 아닌 합니다 <xref:System.Windows.Controls.ScrollViewer>, 부여 해야 합니다는 <xref:System.Windows.Controls.ItemsPresenter> 이름 `ItemsPresenter`합니다.  
  
## <a name="treeview-states"></a>TreeView 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.TreeView> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="treeviewitem-parts"></a>TreeViewItem 파트  
 다음 표에서 대 한 명명된 된 파트를 <xref:System.Windows.Controls.TreeViewItem> 제어 합니다.  
  
|파트|형식|설명|  
|----------|----------|-----------------|  
|PART_Header|<xref:System.Windows.FrameworkElement>|해당 헤더의 콘텐츠를 포함 하는 시각적 요소를 <xref:System.Windows.Controls.TreeView> 제어 합니다.|  
  
## <a name="treeviewitem-states"></a>TreeViewItem 상태  
 다음 표에서 대 한 시각적 상태 <xref:System.Windows.Controls.TreeViewItem> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|----------------------|---------------------------|-----------------|  
|보통|CommonStates|기본 상태입니다.|  
|MouseOver|CommonStates|마우스 포인터가 위에 <xref:System.Windows.Controls.TreeViewItem>합니다.|  
|사용 안 함|CommonStates|<xref:System.Windows.Controls.TreeViewItem> 을 사용할 수 없습니다.|  
|포커스 있음|FocusStates|<xref:System.Windows.Controls.TreeViewItem> 포커스가 있습니다.|  
|포커스 없음|FocusStates|<xref:System.Windows.Controls.TreeViewItem> 포커스가 없습니다.|  
|넓게|ExpansionStates|<xref:System.Windows.Controls.TreeViewItem> 컨트롤을 확장 합니다.|  
|Collapsed|ExpansionStates|<xref:System.Windows.Controls.TreeViewItem> 컨트롤은 축소 합니다.|  
|HasItems|HasItemsStates|<xref:System.Windows.Controls.TreeViewItem> 항목을 했습니다.|  
|NoItems|HasItemsStates|<xref:System.Windows.Controls.TreeViewItem> 항목에 포함 되지 않습니다.|  
|선택함|SelectionStates|<xref:System.Windows.Controls.TreeViewItem> 을 선택 합니다.|  
|SelectedInactive|SelectionStates|<xref:System.Windows.Controls.TreeViewItem> 은 선택 되어 있지만 활성 상태가 아닙니다.|  
|선택 취소|SelectionStates|<xref:System.Windows.Controls.TreeViewItem> 선택 하지 않으면.|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="treeview-controltemplate-example"></a>TreeView ControlTemplate 예제  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.TreeView> 컨트롤과 연결 된 해당 형식입니다.  
  
 [!code-xaml[ControlTemplateExamples#TreeView](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/treeview.xaml#treeview)]  
  
 앞의 예제에서는 다음 리소스를 하나 이상 사용합니다.  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 전체 샘플을 보려면 [Styling with ControlTemplates Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)(ControlTemplate으로 스타일 지정 샘플)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [Control 스타일 및 템플릿](control-styles-and-templates.md)
- [컨트롤 사용자 지정](control-customization.md)
- [스타일 지정 및 템플릿](styling-and-templating.md)
- [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)
