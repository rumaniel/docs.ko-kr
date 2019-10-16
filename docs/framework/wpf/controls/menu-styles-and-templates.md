---
title: Menu 스타일 및 템플릿
ms.date: 03/30/2017
helpviewer_keywords:
- styles [WPF], Menu
- ControlTemplate [WPF], Menu
- Menu [WPF], styles and templates
- states [WPF], Menu
- templates [WPF], Menu
- parts [WPF], Menu
ms.assetid: b89da183-9b87-42c6-ac53-731a42c7b09e
ms.openlocfilehash: 6818be4ac92dbdd7de0c6c6fa65109e21eadc2f5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942105"
---
# <a name="menu-styles-and-templates"></a>Menu 스타일 및 템플릿
이 항목에서는 스타일 및 템플릿에 대해 설명 합니다 <xref:System.Windows.Controls.Menu> 제어 합니다. 기본값을 수정할 수 있습니다 <xref:System.Windows.Controls.ControlTemplate> 고유한 모양을 제어할 수 있습니다. 자세한 내용은 [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)을 참조하세요.  
  
## <a name="menu-parts"></a>메뉴 파트  
 <xref:System.Windows.Controls.Menu> 컨트롤에 명명된 된 파트가 없습니다.  
  
 만들 때를 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.Menu>, 템플릿에 포함 될 수 있습니다는 <xref:System.Windows.Controls.ItemsPresenter> 내는 <xref:System.Windows.Controls.ScrollViewer>합니다. (합니다 <xref:System.Windows.Controls.ItemsPresenter> 에 각 항목을 표시 합니다 <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.ScrollViewer> 컨트롤 내에서 스크롤을 사용할 수)입니다.  경우는 <xref:System.Windows.Controls.ItemsPresenter> 의 직접 자식이 아닌 합니다 <xref:System.Windows.Controls.ScrollViewer>, 부여 해야 합니다는 <xref:System.Windows.Controls.ItemsPresenter> 이름 `ItemsPresenter`합니다.  
  
## <a name="menu-states"></a>메뉴 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.Menu> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="menuitem-parts"></a>MenuItem 파트  
 다음 표에서 대 한 명명된 된 파트를 <xref:System.Windows.Controls.Menu> 제어 합니다.  
  
|파트|형식|설명|  
|-|-|-|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|하위 메뉴에 대 한 영역입니다.|  
  
 만들 때를 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.MenuItem>, 템플릿에 포함 될 수 있습니다는 <xref:System.Windows.Controls.ItemsPresenter> 내는 <xref:System.Windows.Controls.ScrollViewer>합니다. (합니다 <xref:System.Windows.Controls.ItemsPresenter> 에 각 항목을 표시 합니다 <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Controls.ScrollViewer> 컨트롤 내에서 스크롤을 사용할 수)입니다.  경우는 <xref:System.Windows.Controls.ItemsPresenter> 의 직접 자식이 아닌 합니다 <xref:System.Windows.Controls.ScrollViewer>, 부여 해야 합니다는 <xref:System.Windows.Controls.ItemsPresenter> 이름 `ItemsPresenter`합니다.  
  
## <a name="menuitem-states"></a>MenuItem 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.MenuItem> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="menu-and-menuitem-controltemplate-example"></a>메뉴 및 MenuItem ControlTemplate 예제  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.Menu> 제어 합니다.  
  
 [!code-xaml[ControlTemplateExamples#Menu](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menu)]  
  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.MenuItem> 제어 합니다.  
  
 [!code-xaml[ControlTemplateExamples#MenuItem](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menuitem)]  
  
 다음 예제에서는 정의 된 `MenuScrollViewer`, 이전 예제에서 사용 됩니다.  
  
 [!code-xaml[ControlTemplateExamples#MenuScrollViewer](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menuscrollviewer)]  
  
 <xref:System.Windows.Controls.ControlTemplate> 예제에서는 다음 리소스 중 하나 이상을 사용 합니다.  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 전체 샘플을 보려면 [Styling with ControlTemplates Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)(ControlTemplate으로 스타일 지정 샘플)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [Control 스타일 및 템플릿](control-styles-and-templates.md)
- [컨트롤 사용자 지정](control-customization.md)
- [스타일 지정 및 템플릿](styling-and-templating.md)
- [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)
