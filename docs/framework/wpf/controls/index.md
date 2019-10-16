---
title: 컨트롤
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], about WPF controls
ms.assetid: 3f255a8a-35a8-4712-9065-472ff7d75599
ms.openlocfilehash: faa1fbad85acf5788c10de7750c6a7c32b535bf5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957040"
---
# <a name="controls"></a>컨트롤
<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]<xref:System.Windows.Controls.Button>에는 <xref:System.Windows.Controls.Label> ,<xref:System.Windows.Controls.Menu>,, 및<xref:System.Windows.Controls.ListBox>와 같은 거의 모든 Windows 응용 프로그램에서 사용 되는 대부분의 공통 UI 구성 요소가 포함 되어 있습니다. <xref:System.Windows.Controls.TextBox> 지금까지 이러한 개체는 컨트롤이라고 불렀습니다. SDK는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 계속 해 서 "컨트롤" 이라는 용어를 사용 하 여 응용 프로그램에서 표시 되는 개체를 나타내는 모든 클래스를 사용 하는 반면, 클래스는 표시 되는 상태를 갖도록 <xref:System.Windows.Controls.Control> 클래스에서 상속 하지 않아도 된다는 점을 명심 해야 합니다. <xref:System.Windows.Controls.Control> 클래스에서 상속 되는 클래스에는 <xref:System.Windows.Controls.ControlTemplate>가 포함 되어 있습니다 .이를 통해 컨트롤의 소비자가 새 하위 클래스를 만들지 않고도 컨트롤의 모양을 크게 변경할 수 있습니다.  이 항목에서는 컨트롤 ( <xref:System.Windows.Controls.Control> 클래스에서 상속 되는 컨트롤과 그렇지 않은 컨트롤)이에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]일반적으로 사용 되는 방법에 대해 설명 합니다.  

<a name="creating_an_instance_of_a_control"></a>   
## <a name="creating-an-instance-of-a-control"></a>컨트롤의 인스턴스 만들기  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 또는 코드를 사용 하 여 응용 프로그램에 컨트롤을 추가할 수 있습니다.  다음 예제에서는 사용자에게 이름과 성을 묻는 간단한 애플리케이션을 만드는 방법을 보여 줍니다.  이 예제에서는 두 개의 레이블, 두 개의 텍스트 상자 및 두 개의 단추를 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]만듭니다. 모든 컨트롤을 유사하게 만들 수 있습니다.  
  
 [!code-xaml[ControlsOverview#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#1)]  
  
 다음 예제에서는 코드로 동일한 애플리케이션을 만듭니다. 간단히 하기 위해 샘플에서 <xref:System.Windows.Controls.Grid>, `grid1`의 만들기가 제외 되었습니다. `grid1`앞 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 의 예제에 표시 된 것과 같은 열 및 행 정의가 있습니다.  
  
 [!code-csharp[ControlsOverview#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#2)]
 [!code-vb[ControlsOverview#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#2)]  
  
<a name="changing_the_appearance_of_a_control"></a>   
## <a name="changing-the-appearance-of-a-control"></a>컨트롤의 모양 변경  
 일반적으로 애플리케이션의 모양과 느낌에 맞게 컨트롤의 모양을 변경합니다. 수행하려는 작업에 따라 다음 중 하나를 수행하여 컨트롤의 모양을 변경할 수 있습니다.  
  
- 컨트롤의 속성 값을 변경합니다.  
  
- 컨트롤에 <xref:System.Windows.Style> 대 한를 만듭니다.  
  
- 컨트롤에 대 <xref:System.Windows.Controls.ControlTemplate> 한 새를 만듭니다.  
  
### <a name="changing-a-controls-property-value"></a>컨트롤의 속성 값 변경  
 <xref:System.Windows.Controls.Control.Background%2A> 대부분<xref:System.Windows.Controls.Button>의 컨트롤에는의와 같이 컨트롤이 표시 되는 방식을 변경할 수 있는 속성이 있습니다. 및 코드 모두 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 에서 value 속성을 설정할 수 있습니다. <xref:System.Windows.Controls.Control.Background%2A>다음 예에서는 <xref:System.Windows.Controls.Button> 의 <xref:System.Windows.Controls.Control.FontWeight%2A> <xref:System.Windows.Controls.Control.FontSize%2A> 에서,및속성을설정합니다[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xaml[ControlsOverview#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#3)]  
  
 다음 예제에서는 코드로 동일한 속성을 설정합니다.  
  
 [!code-csharp[ControlsOverview#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#4)]
 [!code-vb[ControlsOverview#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#4)]  
  
### <a name="creating-a-style-for-a-control"></a>컨트롤에 대한 스타일 만들기  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 <xref:System.Windows.Style>만들어 응용 프로그램의 각 인스턴스에 대해 속성을 설정 하는 대신, 컨트롤의 모양을 지정 하는 기능을 제공 합니다. 다음 예제에서는 응용 프로그램 <xref:System.Windows.Style> 의 각 <xref:System.Windows.Controls.Button> 에 적용 되는를 만듭니다. <xref:System.Windows.Style>정의는 일반적으로의 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] <xref:System.Windows.FrameworkElement.Resources%2A> 속성과 <xref:System.Windows.ResourceDictionary> <xref:System.Windows.FrameworkElement>같은에 정의 됩니다.  
  
 [!code-xaml[ControlsOverview#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#5)]  
  
 스타일에 키를 할당 하 고 컨트롤의 `Style` 속성에 해당 키를 지정 하 여 특정 형식의 특정 컨트롤에만 스타일을 적용할 수도 있습니다.  스타일에 대 한 자세한 내용은 스타일 지정 [및 템플릿](styling-and-templating.md)을 참조 하세요.  
  
### <a name="creating-a-controltemplate"></a>ControlTemplate 만들기  
 를 <xref:System.Windows.Style> 사용 하면 한 번에 여러 컨트롤의 속성을 설정할 수 있지만, 경우에 <xref:System.Windows.Style>따라를 만들어 수행할 수 있는 작업 <xref:System.Windows.Controls.Control> 이상의 모양을 사용자 지정 하는 것이 좋습니다. <xref:System.Windows.Controls.Control> 클래스에서 상속 되는 클래스에는 <xref:System.Windows.Controls.ControlTemplate>의 <xref:System.Windows.Controls.Control>구조와 모양을 정의 하는가 있습니다. 의 속성은 public 이므로 기본값과 다른 <xref:System.Windows.Controls.Control> 를 <xref:System.Windows.Controls.ControlTemplate> 제공할 수 있습니다. <xref:System.Windows.Controls.Control.Template%2A> <xref:System.Windows.Controls.Control> 컨트롤에서 상속 하는 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.Control> 대신의 새를 지정 하 여의 모양을 <xref:System.Windows.Controls.Control>사용자 지정할 수 있습니다.  
  
 매우 일반적인 컨트롤인를 <xref:System.Windows.Controls.Button>살펴보겠습니다.  의 기본 동작은 사용자가 <xref:System.Windows.Controls.Button> 클릭할 때 응용 프로그램이 작업을 수행할 수 있도록 하는 것입니다.  기본적으로의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 는 <xref:System.Windows.Controls.Button> 볼록 사각형으로 나타납니다.  응용 프로그램을 개발 하는 동안 단추의 click 이벤트를 처리 하는 등의 <xref:System.Windows.Controls.Button>동작을 활용 하는 것이 좋습니다. 하지만 단추의 속성을 변경 하 여 수행할 수 있는 작업 이상으로 단추의 모양을 변경할 수도 있습니다.  이 경우 새 <xref:System.Windows.Controls.ControlTemplate>을 만들 수 있습니다.  
  
 다음 예제는 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.Button>합니다.  는 <xref:System.Windows.Controls.ControlTemplate> 모퉁이가 둥근 <xref:System.Windows.Controls.Button> 모퉁이와 그라데이션 배경을 사용 하 여을 만듭니다.  에 <xref:System.Windows.Controls.ControlTemplate> 는 두 <xref:System.Windows.Controls.Border> 개의 <xref:System.Windows.Controls.Border.Background%2A> 개체가있는<xref:System.Windows.Media.LinearGradientBrush> 가 있는가 포함 되어 있습니다. <xref:System.Windows.Media.GradientStop>  첫 번째 <xref:System.Windows.Media.GradientStop> 는 데이터 바인딩을 사용 하 여 <xref:System.Windows.Media.GradientStop.Color%2A> 의 <xref:System.Windows.Media.GradientStop> 속성을 단추의 배경 색에 바인딩합니다.  <xref:System.Windows.Controls.Control.Background%2A> 의 속성을 설정 하면 해당 값의 색이 첫 번째 <xref:System.Windows.Media.GradientStop>값으로 사용 됩니다. <xref:System.Windows.Controls.Button> 데이터 바인딩에 대한 자세한 내용은 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조하세요. 또한이 예제에서는가 <xref:System.Windows.Trigger> 인 <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> `true`경우의 모양을 변경 하는을 만듭니다.  
  
 [!code-xaml[ControlsOverview#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#6)]  
[!code-xaml[ControlsOverview#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#7)]  
  
> [!NOTE]
> 예제가 제대로 작동 하려면 <xref:System.Windows.Controls.Button> 의 <xref:System.Windows.Media.SolidColorBrush> 속성을로설정해야합니다.<xref:System.Windows.Controls.Control.Background%2A>  
  
<a name="subscribing_to_events"></a>   
## <a name="subscribing-to-events"></a>이벤트 구독  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 또는 코드를 사용 하 여 컨트롤의 이벤트를 구독할 수 있지만 이벤트를 코드 에서만 처리할 수 있습니다.  다음 예제에서는 `Click` <xref:System.Windows.Controls.Button>의 이벤트를 구독 하는 방법을 보여 줍니다.  
  
 [!code-xaml[ControlsOverview#10](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#10)]  
  
 [!code-csharp[ControlsOverview#8](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#8)]
 [!code-vb[ControlsOverview#8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#8)]  
  
 다음 예제에서는 <xref:System.Windows.Controls.Button>의 이벤트 `Click` 를 처리 합니다.  
  
 [!code-csharp[ControlsOverview#9](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#9)]
 [!code-vb[ControlsOverview#9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#9)]  
  
<a name="rich_content_in_controls"></a>   
## <a name="rich-content-in-controls"></a>컨트롤의 풍부한 콘텐츠  
 <xref:System.Windows.Controls.Control> 클래스에서 상속 되는 대부분의 클래스에는 다양 한 콘텐츠를 포함할 수 있는 용량이 있습니다. 예를 들어는 <xref:System.Windows.Controls.Label> 문자열 <xref:System.Windows.Controls.Image>, 또는 <xref:System.Windows.Controls.Panel>와 같은 모든 개체를 포함할 수 있습니다.  다음 클래스는 풍부한 콘텐츠를 지원 하며의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]대부분의 컨트롤에 대 한 기본 클래스로 작동 합니다.  
  
- <xref:System.Windows.Controls.ContentControl>-이 클래스에서 상속 되는 클래스의 예로는, <xref:System.Windows.Controls.Label> <xref:System.Windows.Controls.Button>및 <xref:System.Windows.Controls.ToolTip>가 있습니다.  
  
- <xref:System.Windows.Controls.ItemsControl>-이 클래스에서 상속 되는 클래스의 예로는, <xref:System.Windows.Controls.ListBox> <xref:System.Windows.Controls.Menu>및 <xref:System.Windows.Controls.Primitives.StatusBar>가 있습니다.  
  
- <xref:System.Windows.Controls.HeaderedContentControl>-이 클래스에서 상속 되는 클래스의 예로는, <xref:System.Windows.Controls.TabItem> <xref:System.Windows.Controls.GroupBox>및 <xref:System.Windows.Controls.Expander>가 있습니다.  
  
- <xref:System.Windows.Controls.HeaderedItemsControl>-이 클래스에서 상속 되는 클래스의 예로는, <xref:System.Windows.Controls.MenuItem> <xref:System.Windows.Controls.TreeViewItem>및 <xref:System.Windows.Controls.ToolBar>가 있습니다.  

 이러한 기본 클래스에 대 한 자세한 내용은 [WPF 콘텐츠 모델](wpf-content-model.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [스타일 지정 및 템플릿](styling-and-templating.md)
- [범주별 컨트롤](controls-by-category.md)
- [컨트롤 라이브러리](control-library.md)
- [데이터 템플릿 개요](../data/data-templating-overview.md)
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [입력](../advanced/input-wpf.md)
- [명령 사용](../advanced/how-to-enable-a-command.md)
- [연습: 사용자 지정 애니메이션 단추 만들기](walkthroughs-create-a-custom-animated-button.md)
- [컨트롤 사용자 지정](control-customization.md)
