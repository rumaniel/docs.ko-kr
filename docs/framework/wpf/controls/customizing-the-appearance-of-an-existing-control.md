---
title: ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control contract [WPF]
- controls [WPF], visual structure changes
- ControlTemplate [WPF], customizing for existing controls
- skinning controls [WPF]
- controls [WPF], appearance specified by state
- templates [WPF], custom for existing controls
ms.assetid: 678dd116-43a2-4b8c-82b5-6b826f126e31
ms.openlocfilehash: 63a0b724b71c4a4901c2dedcf502045a75ec405c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69933725"
---
# <a name="customizing-the-appearance-of-an-existing-control-by-creating-a-controltemplate"></a>ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정
<a name="introduction"></a>는 <xref:System.Windows.Controls.ControlTemplate> 컨트롤의 시각적 구조와 시각적 동작을 지정 합니다. 새 <xref:System.Windows.Controls.ControlTemplate>를 제공 하 여 컨트롤의 모양을 사용자 지정할 수 있습니다. 를 만들 <xref:System.Windows.Controls.ControlTemplate>때 해당 기능을 변경 하지 않고 기존 컨트롤의 모양을 바꿉니다. 예를 들어 응용 프로그램의 단추를 기본 정사각형 셰이프 대신 round로 만들 수 있지만 단추는 이벤트를 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 계속 발생 시킵니다.  
  
 이 항목에서는의 <xref:System.Windows.Controls.ControlTemplate>다양 한 부분에 대해 설명 하 고, 간단한 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.Button>을 만드는 방법을 보여 주고, 컨트롤의 모양을 사용자 지정할 수 있도록 컨트롤의 컨트롤 계약을 이해 하는 방법을 설명 합니다. <xref:System.Windows.Controls.ControlTemplate> 에서[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]를 만들기 때문에 코드를 작성 하지 않고도 컨트롤의 모양을 변경할 수 있습니다. Microsoft Expression Blend와 같은 디자이너를 사용하여 사용자 지정 컨트롤 템플릿을 만들 수도 있습니다. 이 항목에서는의 모양을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] <xref:System.Windows.Controls.Button> 사용자 지정 하 고 항목의 끝에 있는 전체 예제를 나열 하는의 예제를 보여 줍니다. Expression Blend 사용에 대한 자세한 내용은 [템플릿을 지원하는 컨트롤의 스타일 지정](https://go.microsoft.com/fwlink/?LinkId=161153)을 참조하세요.  
  
 다음 그림에서는이 항목 <xref:System.Windows.Controls.Button> 에서 만든를 <xref:System.Windows.Controls.ControlTemplate> 사용 하는을 보여 줍니다.  
  
 ![사용자 지정 컨트롤 템플릿을 사용 하는 단추입니다.](./media/ndp-buttonnormal.png "NDP_ButtonNormal")  
사용자 지정 컨트롤 템플릿을 사용하는 단추  
  
 ![빨간색 테두리가 있는 단추입니다.](./media/ndp-buttonmouseover.png "NDP_ButtonMouseOver")  
사용자 지정 컨트롤 템플릿을 사용하고 마우스 포인터가 위에 놓여 있는 단추  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>필수 구성 요소  
 이 항목에서는 [컨트롤](index.md)에 설명된 대로 컨트롤과 스타일을 만들고 사용하는 방법을 알고 있다고 가정합니다. 이 항목에서 설명 하는 개념은를 제외 <xref:System.Windows.Controls.Control> <xref:System.Windows.Controls.UserControl>하 고 클래스에서 상속 되는 요소에 적용 됩니다. 에를 적용할 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.UserControl>수 없습니다.  
  
<a name="when_you_should_create_a_controltemplate"></a>   
## <a name="when-you-should-create-a-controltemplate"></a>ControlTemplate을 만들어야 하는 경우  
 컨트롤에는, <xref:System.Windows.Controls.Border.Background%2A> <xref:System.Windows.Controls.Control.Foreground%2A>및 <xref:System.Windows.Controls.Control.FontFamily%2A>와 같이 컨트롤의 모양에 대 한 다양 한 측면을 지정 하기 위해 설정할 수 있는 여러 속성이 있지만 이러한 속성을 설정 하 여 변경할 수 있는 내용은 제한 됩니다. 예를 들어에서 <xref:System.Windows.Controls.Control.Foreground%2A> <xref:System.Windows.Controls.Control.FontStyle%2A> 속성을 blue로 설정 하 고을 기울임꼴로 설정할 수 있습니다. <xref:System.Windows.Controls.CheckBox>  
  
 컨트롤에 대해 새 <xref:System.Windows.Controls.ControlTemplate> 을 만들 수 없는 기능을 사용 하는 경우 모든 기반 응용 프로그램 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 모든 컨트롤에 동일한 일반 모양이 지정 되어 사용자 지정 모양과 느낌을 가진 응용 프로그램을 만드는 기능이 제한 됩니다. 기본적으로 모든 <xref:System.Windows.Controls.CheckBox> 특성은 비슷한 특성을 가집니다. 예를 들어의 <xref:System.Windows.Controls.CheckBox> 콘텐츠는 항상 선택 표시기의 오른쪽에 있고 확인 표시는 <xref:System.Windows.Controls.CheckBox> 가 선택 되었음을 나타내는 데 항상 사용 됩니다.  
  
 컨트롤의 다른 <xref:System.Windows.Controls.ControlTemplate> 속성이 수행 하는 설정에 따라 컨트롤의 모양을 사용자 지정 하려는 경우을 만듭니다. 의 <xref:System.Windows.Controls.CheckBox>예제에서 확인란의 내용이 선택 표시기 위에 표시 <xref:System.Windows.Controls.CheckBox> 되도록 하 고 X를 선택 하 여가 선택 되어 있다고 가정 합니다. 이러한 변경 내용은 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.CheckBox>의에서 지정 합니다.  
  
 다음 그림에서는 기본값 <xref:System.Windows.Controls.CheckBox> <xref:System.Windows.Controls.ControlTemplate>을 사용 하는을 보여 줍니다.  
  
 ![기본 컨트롤 템플릿이 있는 확인란입니다.](./media/ndp-checkboxdefault.png "NDP_CheckBoxDefault")  
기본 컨트롤 템플릿을 사용하는 확인란  
  
 다음 그림에서는 사용자 지정 <xref:System.Windows.Controls.CheckBox> <xref:System.Windows.Controls.ControlTemplate> 를 사용 하 여 <xref:System.Windows.Controls.CheckBox> 선택 표시기 <xref:System.Windows.Controls.CheckBox> 위에의 내용을 삽입 하 고이 선택 될 때 X를 표시 하는를 보여 줍니다.  
  
 ![사용자 지정 컨트롤 템플릿이 있는 확인란입니다.](./media/ndp-checkboxcustom.png "NDP_CheckBoxCustom")  
사용자 지정 컨트롤 템플릿을 사용하는 확인란  
  
 이 샘플 <xref:System.Windows.Controls.CheckBox> 의에 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.Button>대 한는 비교적 복잡 하므로이 항목에서는에 대 한를 만드는 간단한 예제를 사용 합니다. <xref:System.Windows.Controls.ControlTemplate>  
  
<a name="changing_the_visual_structure_of_a_control"></a>   
## <a name="changing-the-visual-structure-of-a-control"></a>컨트롤의 시각적 구조 변경  
 에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]컨트롤은 종종 복합 <xref:System.Windows.FrameworkElement> 개체입니다. 를 만들 <xref:System.Windows.Controls.ControlTemplate>때 개체를 결합 <xref:System.Windows.FrameworkElement> 하 여 단일 컨트롤을 빌드합니다. 에 <xref:System.Windows.Controls.ControlTemplate> 는 루트 요소로 된 <xref:System.Windows.FrameworkElement> 가 하나만 있어야 합니다. 루트 요소는 일반적으로 다른 <xref:System.Windows.FrameworkElement> 개체를 포함 합니다. 개체가 조합되면 컨트롤의 시각적 구조가 만들어집니다.  
  
 다음 예에서는 <xref:System.Windows.Controls.Button>에 대 한 <xref:System.Windows.Controls.ControlTemplate> 사용자 지정을 만듭니다. <xref:System.Windows.Controls.ControlTemplate> 는<xref:System.Windows.Controls.Button>의 시각적 구조를 만듭니다. 이 예제에서는 마우스 포인트를 단추 위로 이동하거나 단추를 클릭할 때 단추의 모양이 변경되지 않습니다. 단추가 다른 상태에 있을 때 단추의 모양을 변경하는 방법에 대해서는 이 항목의 뒷부분에서 설명합니다.  
  
 이 예제에서 시각적 구조는 다음 부분으로 구성되어 있습니다.  
  
- 템플릿의 루트 `RootElement` <xref:System.Windows.Controls.Border> 역할<xref:System.Windows.FrameworkElement>을 하는 명명 된입니다.  
  
- <xref:System.Windows.Controls.Grid> 의`RootElement`자식인입니다.  
  
- 단추의 콘텐츠를 표시 하는입니다.<xref:System.Windows.Controls.ContentPresenter> 에서는 <xref:System.Windows.Controls.ContentPresenter> 모든 형식의 개체를 표시할 수 있습니다.  
  
 [!code-xaml[VSMButtonTemplate#BasicTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#basictemplate)]  
  
### <a name="preserving-the-functionality-of-a-controls-properties-by-using-templatebinding"></a>TemplateBinding을 사용하여 컨트롤의 속성 기능 유지  
 새 <xref:System.Windows.Controls.ControlTemplate>를 만들 때에도 공용 속성을 사용 하 여 컨트롤의 모양을 변경 하는 것이 좋습니다. [TemplateBinding](../advanced/templatebinding-markup-extension.md) 태그 확장은에 <xref:System.Windows.Controls.ControlTemplate> 있는 요소의 속성을 컨트롤에 정의 된 공용 속성에 바인딩합니다. [TemplateBinding](../advanced/templatebinding-markup-extension.md)을 사용하면 컨트롤의 속성이 템플릿의 매개 변수로 작동됩니다. 즉, 컨트롤의 속성을 설정하면 해당 값은 [TemplateBinding](../advanced/templatebinding-markup-extension.md)이 있는 요소로 전달됩니다.  
  
 다음 예제에서는 [TemplateBinding](../advanced/templatebinding-markup-extension.md) 태그 확장을 사용 하 여에 있는 요소의 <xref:System.Windows.Controls.ControlTemplate> 속성을 단추에 정의 된 공용 속성에 바인딩하는 위의 예제 부분을 반복 합니다.  
  
 [!code-xaml[VSMButtonTemplate#TemplateBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#templatebinding)]  
  
 이 예제에서는 <xref:System.Windows.Controls.Grid> <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType> 속성 템플릿이에 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType>바인딩되어 있습니다. 는 <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType> 템플릿 바인딩 이므로 동일한 <xref:System.Windows.Controls.ControlTemplate> 를 사용 하는 단추를 여러 개 만들고 각 단추에 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType> 대해를 다른 값으로 설정할 수 있습니다. 가 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType> 의 요소 <xref:System.Windows.Controls.ControlTemplate>속성에 매핑되지 않은 경우 단추를 설정 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType> 하면 단추의 모양에 영향을 주지 않습니다.  
  
 두 속성의 이름이 같지 않아도 됩니다. 앞의 예제 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=nameWithType> 에서의 속성 <xref:System.Windows.Controls.Button> 은의 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=nameWithType> 속성 <xref:System.Windows.Controls.ContentPresenter>에 바인딩된 템플릿입니다. 이를 통해 단추 콘텐츠의 가로 위치를 지정할 수 있습니다. <xref:System.Windows.Controls.ContentPresenter>에는 라는 `HorizontalContentAlignment`속성이 없지만 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=nameWithType> 에 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=nameWithType>바인딩할 수 있습니다. 속성을 템플릿 바인딩할 경우 대상 속성과 소스 속성의 형식이 동일해야 합니다.  
  
 클래스 <xref:System.Windows.Controls.Control> 는 컨트롤이 설정 될 때 컨트롤에 영향을 주지 않도록 컨트롤 템플릿에서 사용 해야 하는 여러 속성을 정의 합니다. 에서 <xref:System.Windows.Controls.ControlTemplate> 속성을 사용 하는 방법은 속성에 따라 달라 집니다. 는 <xref:System.Windows.Controls.ControlTemplate> 다음 방법 중 하나를 사용 하 여 속성을 사용 해야 합니다.  
  
- <xref:System.Windows.Controls.ControlTemplate> 템플릿의 요소가 속성에 바인딩됩니다.  
  
- 의 요소 <xref:System.Windows.Controls.ControlTemplate> 는 부모의 <xref:System.Windows.FrameworkElement>속성을 상속 합니다.  
  
 다음 표에서는 <xref:System.Windows.Controls.Control> 클래스의 컨트롤에서 상속 된 시각적 속성을 보여 줍니다. 또한 컨트롤의 기본 컨트롤 템플릿이 상속받은 속성 값을 사용하는지 또는 템플릿 바인딩되어야 하는지를 나타냅니다.  
  
|속성|사용 방법|  
|--------------|------------------|  
|<xref:System.Windows.Controls.Control.Background%2A>|템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.BorderThickness%2A>|템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.BorderBrush%2A>|템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.FontFamily%2A>|속성 상속 또는 템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.FontSize%2A>|속성 상속 또는 템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.FontStretch%2A>|속성 상속 또는 템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.FontWeight%2A>|속성 상속 또는 템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.Foreground%2A>|속성 상속 또는 템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>|템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.Padding%2A>|템플릿 바인딩|  
|<xref:System.Windows.Controls.Control.VerticalContentAlignment%2A>|템플릿 바인딩|  
  
 이 표에서는 <xref:System.Windows.Controls.Control> 클래스에서 상속 된 시각적 속성만 나열 합니다. 테이블에 나열 된 속성 외에도 컨트롤은 부모 프레임 워크 요소에서 <xref:System.Windows.FrameworkElement.DataContext%2A>, <xref:System.Windows.FrameworkElement.Language%2A>및 <xref:System.Windows.Controls.TextBlock.TextDecorations%2A> 속성을 상속할 수 있습니다.  
  
 또한 <xref:System.Windows.Controls.ContentPresenter> 이 <xref:System.Windows.Controls.ControlTemplate> 의 <xref:System.Windows.Controls.ContentControl> 에있는<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 경우가 및<xref:System.Windows.Controls.ContentControl.Content%2A> 속성에 자동으로 바인딩됩니다. <xref:System.Windows.Controls.ContentPresenter> <xref:System.Windows.Controls.ItemsPresenter> <xref:System.Windows.Controls.ItemsControl.Items%2A> 마찬가지로의 에있는<xref:System.Windows.Controls.ItemsPresenter> 는 및 속성에 자동으로 바인딩됩니다. <xref:System.Windows.Controls.ItemsControl> <xref:System.Windows.Controls.ControlTemplate>  
  
 다음 예제에서는 앞의 예제에서 정의 된 <xref:System.Windows.Controls.ControlTemplate> 를 사용 하는 두 개의 단추를 만듭니다. <xref:System.Windows.Controls.Control.Background%2A>이 예에서는 각 단추 <xref:System.Windows.Controls.Control.Foreground%2A>에, <xref:System.Windows.Controls.Control.FontSize%2A> 및 속성을 설정 합니다. 속성을 <xref:System.Windows.Controls.Control.Background%2A> 설정 하는 것은에 템플릿이 바인딩되어 <xref:System.Windows.Controls.ControlTemplate>있으므로 효과가 있습니다. <xref:System.Windows.Controls.Control.Foreground%2A> 및<xref:System.Windows.Controls.Control.FontSize%2A> 속성이 템플릿 바운드가 아닌 경우에도 해당 값이 상속 되므로 값을 설정 하면 효과가 있습니다.  
  
 [!code-xaml[VSMButtonTemplate#ButtonDeclaration](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#buttondeclaration)]  
  
 앞의 예제에서는 다음 그림과 유사한 출력을 생성합니다.  
  
 ![단추 두 개, 파란색 1 개 및 자주색 단추](./media/ndp-buttontwo.png "NDP_ButtonTwo")  
배경색이 서로 다른 두 개의 단추  
  
<a name="changing_the_appearance_of_a_control_depending_on_its_state"></a>   
## <a name="changing-the-appearance-of-a-control-depending-on-its-state"></a>상태에 따라 컨트롤의 모양 변경  
 기본 모양을 가진 단추와 앞의 예제에서 사용된 단추의 차이점은 기본 단추가 다른 상태에 있을 때 약간 변경된다는 것입니다. 예를 들어 단추를 누르거나 마우스 포인터가 단추 위에 있으면 기본 단추의 모양이 변경됩니다. 는 <xref:System.Windows.Controls.ControlTemplate> 컨트롤의 기능을 변경 하지 않지만 컨트롤의 시각적 동작을 변경 합니다. 시각적 동작은 컨트롤이 특정 상태에 있을 때의 컨트롤 모양을 설명합니다. 컨트롤의 기능과 시각적 동작의 차이점을 파악하려면 단추 예제를 참조하세요. 단추의 기능은 클릭 될 때 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트를 발생 시키는 것 이지만 단추의 시각적 동작은 포인터가 가리키거나 눌린 상태에서 모양을 변경 하는 것입니다.  
  
 개체를 <xref:System.Windows.VisualState> 사용 하 여 특정 상태에 있을 때 컨트롤의 모양을 지정할 수 있습니다. 에는에 <xref:System.Windows.Media.Animation.Storyboard> 있는 <xref:System.Windows.Controls.ControlTemplate>요소의 모양을 변경 하는가 <xref:System.Windows.VisualState> 포함 되어 있습니다. 컨트롤의 논리는를 <xref:System.Windows.VisualStateManager>사용 하 여 상태를 변경 하기 때문에이 작업을 수행 하기 위해 코드를 작성할 필요가 없습니다. 컨트롤에 지정 된 상태로 전환 하는 경우는 <xref:System.Windows.VisualState.Name%2A?displayProperty=nameWithType> 속성을 <xref:System.Windows.Media.Animation.Storyboard> 시작 합니다. 컨트롤 상태를 종료 하는 경우는 <xref:System.Windows.Media.Animation.Storyboard> 중지 합니다.  
  
 다음 예제에서는 마우스 포인터가 <xref:System.Windows.VisualState> 위에 <xref:System.Windows.Controls.Button> 있을 때의 모양을 변경 하는을 보여 줍니다. <xref:System.Windows.Media.Animation.Storyboard> 는`BorderBrush`의 색을 변경 하 여 단추의 테두리 색을 변경 합니다. 이 항목의 시작 부분 <xref:System.Windows.Controls.ControlTemplate> 에 있는 예제를 참조 하는 경우에는의에 `BorderBrush` 할당 <xref:System.Windows.Controls.Border.Background%2A> <xref:System.Windows.Controls.Border>된의 <xref:System.Windows.Media.SolidColorBrush> 이름이 표시 됩니다.  
  
 [!code-xaml[VSMButtonTemplate#4](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#4)]  
  
 이 컨트롤을 통해 해당 컨트롤 계약의 일부로 상태를 정의합니다. 컨트롤 계약에 대해서는 이 항목의 뒷부분에 있는 [컨트롤 계약을 이해하여 다른 컨트롤 사용자 지정](#customizing_other_controls_by_understanding_the_control_contract)에서 자세히 설명합니다. 다음 표에서는 <xref:System.Windows.Controls.Button>에 대해 지정 된 상태를 보여 줍니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|----------------------|---------------------------|-----------------|  
|일반|CommonStates|기본 상태입니다.|  
|MouseOver|CommonStates|마우스 포인터가 컨트롤 위에 있습니다.|  
|누름|CommonStates|컨트롤을 눌렀습니다.|  
|사용 안 함|CommonStates|컨트롤이 비활성화되었습니다.|  
|포커스 있음|FocusStates|컨트롤에 포커스가 있습니다.|  
|포커스 없음|FocusStates|컨트롤에 포커스가 없습니다.|  
  
 는 <xref:System.Windows.Controls.Button> 두 개의 상태 그룹 `Normal`을 정의 `CommonStates` 합니다. `Pressed`그룹에 `MouseOver`는,, `Disabled` 및 상태가 포함 됩니다. `FocusStates` 그룹에는 `Focused` 및 `Unfocused` 상태가 포함됩니다. 같은 상태 그룹에 있는 상태는 함께 사용할 수 없습니다. 컨트롤은 항상 그룹마다 한 개의 상태에 있습니다. 예를 들어, <xref:System.Windows.Controls.Button> 는 마우스 포인터가 위에 있지 않아도 포커스를 가질 수 있으므로 `Focused` 상태의 <xref:System.Windows.Controls.Button> 는 `MouseOver`, `Pressed`또는 `Normal` 상태일 수 있습니다.  
  
 개체에 <xref:System.Windows.VisualState> 개체를 <xref:System.Windows.VisualStateGroup> 추가 합니다. <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> 연결 된 <xref:System.Windows.VisualStateGroup> 속성에 개체를 추가 합니다. <xref:System.Windows.VisualState> 다음 예제에서는 `Normal`, `MouseOver` 및`Pressed`상태 에 대 한 개체를 정의 합니다 .이 개체는 모두 그룹에있습니다.`CommonStates` <xref:System.Windows.VisualState.Name%2A> 각<xref:System.Windows.VisualState> 의는 위의 테이블에 있는 이름과 일치 합니다. 간단한 예제를 제공하기 위해 `Disabled` 상태와 `FocusStates` 그룹의 상태는 생략되었지만 이 항목의 끝에 있는 전체 예제에는 포함되어 있습니다.  
  
> [!NOTE]
> 의 <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> 루트<xref:System.Windows.FrameworkElement>에 연결 된 속성을 설정 해야 합니다. <xref:System.Windows.Controls.ControlTemplate>  
  
 [!code-xaml[VSMButtonTemplate#VisualStates](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualstates)]  
  
 앞의 예제에서는 다음 그림과 유사한 출력을 생성합니다.  
  
 ![사용자 지정 컨트롤 템플릿을 사용 하는 단추입니다.](./media/ndp-buttonnormal.png "NDP_ButtonNormal")  
정상 상태에서 사용자 지정 컨트롤 템플릿을 사용하는 단추  
  
 ![빨간색 테두리가 있는 단추입니다.](./media/ndp-buttonmouseover.png "NDP_ButtonMouseOver")  
마우스가 위에 있는 상태에서 사용자 지정 컨트롤 템플릿을 사용하는 단추  
  
 ![누른 단추의 테두리는 투명 합니다.](./media/ndp-buttonpressed.png "NDP_ButtonPressed")  
누름 상태에서 사용자 지정 컨트롤 템플릿을 사용하는 단추  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]와 함께 제공된 컨트롤의 시각적 상태를 찾으려면 [Control 스타일 및 템플릿](control-styles-and-templates.md)을 참조하세요.  
  
<a name="specifying_the_behavior_of_a_control_when_it_transitions_between_states"></a>   
## <a name="specifying-the-behavior-of-a-control-when-it-transitions-between-states"></a>상태 간 전환 시 컨트롤의 동작 지정  
 위의 예제에서 단추를 클릭하면 모양도 변경되지만 단추를 1초 동안 누르고 있지 않으면 효과가 표시되지 않습니다. 기본적으로 애니메이션은 적용되려면 1초가 걸립니다. 사용자가 단추를 클릭 하 여 더 짧은 시간 안에 놓을 가능성이 있기 때문에를 <xref:System.Windows.Controls.ControlTemplate> 기본 상태로 유지 하는 경우 시각적 피드백은 효과적이 지 않습니다.  
  
 에 개체를 추가 <xref:System.Windows.VisualTransition> 하 여 컨트롤을 한 상태에서 다른 상태로 원활 하 게 전환 하기 위해 애니메이션이 발생 하는 시간을 지정할 수 있습니다. <xref:System.Windows.Controls.ControlTemplate> 만들 때는 <xref:System.Windows.VisualTransition>, 다음 중 하나 이상을 지정:  
  
- 적용할 상태 간에 전환되는 데 소요되는 시간  
  
- 컨트롤의 모양에 전환 시 적용되는 추가 변경 내용  
  
- <xref:System.Windows.VisualTransition> 이 적용 되는 상태입니다.  
  
### <a name="specifying-the-duration-of-a-transition"></a>전환 기간 지정  
 전환 하는 걸리는 시간을 설정 하 여 지정할 수 있습니다는 <xref:System.Windows.VisualTransition.GeneratedDuration%2A> 속성입니다. 앞의 예제에는 <xref:System.Windows.VisualState> 단추를 누를 때 단추의 테두리가 투명해 지는 것을 지정 하는가 포함 되어 있지만 단추를 빠르게 누르고 놓았을 경우 애니메이션을 눈에 띄게 유지 하는 데 너무 오래 걸립니다. 을 <xref:System.Windows.VisualTransition> 사용 하 여 컨트롤을 눌린 상태로 전환 하는 데 걸리는 시간을 지정할 수 있습니다. 다음 예제에서는 컨트롤이 누른 상태로 전환되는 데 1/100초가 걸리도록 지정합니다.  
  
 [!code-xaml[VSMButtonTemplate#PressedTransition](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#pressedtransition)]  
  
### <a name="specifying-changes-to-the-controls-appearance-during-a-transition"></a>전환 중 컨트롤의 모양 변경 지정  
 는 <xref:System.Windows.VisualTransition> 컨트롤이 상태 <xref:System.Windows.Media.Animation.Storyboard> 간에 전환 될 때 시작 하는를 포함 합니다. 예를 들어 컨트롤이 `MouseOver` 상태에서 `Normal` 상태로 전환될 때 특정 애니메이션이 적용되도록 지정할 수 있습니다. 다음 예제에서는 사용자가 <xref:System.Windows.VisualTransition> 마우스 포인터를 단추 밖으로 이동 하 고, 단추의 테두리가 파란색으로 바뀌고, 노란색으로 바뀌고, 1.5 초 안에 검정색으로 변경 되도록 지정 하는을 만듭니다.  
  
 [!code-xaml[VSMButtonTemplate#8](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#8)]  
  
### <a name="specifying-when-a-visualtransition-is-applied"></a>VisualTransition 적용 시기 지정  
 는 <xref:System.Windows.VisualTransition> 특정 상태에만 적용 되도록 제한 하거나 컨트롤이 상태 간에 전환 될 때마다 적용할 수 있습니다. 앞 <xref:System.Windows.VisualTransition> 의 예제에서는 컨트롤이 상태 `MouseOver` 에서 `Normal` 상태로 전환 될 때 적용 됩니다 <xref:System.Windows.VisualTransition> . 앞의 예제에서는 컨트롤이 `Pressed` 상태로 전환 될 때가 적용 됩니다. 시간을 제한할 수는 <xref:System.Windows.VisualTransition> 설정 하 여 적용 되는 <xref:System.Windows.VisualTransition.To%2A> 및 <xref:System.Windows.VisualTransition.From%2A> 속성. 다음 표에서는 최대한의 제한에서 최소한의 제한까지 제한 수준에 대해 설명합니다.  
  
|제한 유형|From 값|To 값|  
|-------------------------|-------------------|-----------------|  
|지정된 상태에서 지정된 다른 상태로 전환|이름을 <xref:System.Windows.VisualState>|이름을 <xref:System.Windows.VisualState>|  
|임의의 상태에서 지정된 상태로 전환|설정 안 함|이름을 <xref:System.Windows.VisualState>|  
|지정된 상태에서 임의의 상태로 전환|이름을 <xref:System.Windows.VisualState>|설정 안 함|  
|임의의 상태에서 임의의 다른 상태로 전환|설정 안 함|설정 안 함|  
  
 여러 개 있을 수 있습니다 <xref:System.Windows.VisualTransition> 개체는 <xref:System.Windows.VisualStateGroup> 동일한 상태를 참조 하는 있지만 이러한 이전 표에 지정 된 순서 대로 사용 됩니다. 다음 예제에는 두 개의 <xref:System.Windows.VisualTransition> 개체가 있습니다. 컨트롤에서 전환 하는 경우는 `Pressed` 상태는 `MouseOver` 상태를 <xref:System.Windows.VisualTransition> 둘 다를 포함 하는 <xref:System.Windows.VisualTransition.From%2A> 및 <xref:System.Windows.VisualTransition.To%2A> 집합이 사용 됩니다. 컨트롤이 `Pressed`가 아닌 상태에서 `MouseOver` 상태로 전환될 때는 다른 상태가 사용됩니다.  
  
 [!code-xaml[VSMButtonTemplate#7](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#7)]  
  
 <xref:System.Windows.VisualStateGroup> 에는<xref:System.Windows.VisualState> 의 개체에 적용 되 <xref:System.Windows.VisualTransition> 는 <xref:System.Windows.VisualStateGroup>개체를 포함 하는 속성이 있습니다. <xref:System.Windows.VisualStateGroup.Transitions%2A> 작성자는 <xref:System.Windows.Controls.ControlTemplate> 원하는 것을 자유롭게 <xref:System.Windows.VisualTransition> 포함할 수 있습니다. 그러나 <xref:System.Windows.VisualTransition.To%2A> 및 <xref:System.Windows.VisualTransition.From%2A> 속성이 <xref:System.Windows.VisualStateGroup> 에<xref:System.Windows.VisualTransition> 없는 상태 이름으로 설정 된 경우는 무시 됩니다.  
  
 다음 예제에서는에 <xref:System.Windows.VisualStateGroup> `CommonStates`대 한을 보여 줍니다. 이 예제에서는 각 <xref:System.Windows.VisualTransition> 단추의 다음 전환에 대해를 정의 합니다.  
  
- `Pressed` 상태로 전환  
  
- `MouseOver` 상태로 전환  
  
- `Pressed` 상태에서 `MouseOver` 상태로 전환  
  
- `MouseOver` 상태에서 `Normal` 상태로 전환  
  
 [!code-xaml[VSMButtonTemplate#VisualTransitions](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualtransitions)]  
  
<a name="customizing_other_controls_by_understanding_the_control_contract"></a>   
## <a name="customizing-other-controls-by-understanding-the-control-contract"></a>컨트롤 계약을 이해하여 다른 컨트롤 사용자 지정  
 개체를 사용 하 여 <xref:System.Windows.Controls.ControlTemplate> 시각적 구조 <xref:System.Windows.VisualState> 를 지정 하 고 개체를 사용 하 여 시각적 동작을 지정 하기 위해를 사용 하는 컨트롤은 파트 컨트롤 모델을 사용 합니다. <xref:System.Windows.FrameworkElement> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 4와 함께 제공되는 많은 컨트롤이 이 모델을 사용합니다. <xref:System.Windows.Controls.ControlTemplate> 작성자가 알고 있어야 하는 파트는 컨트롤 계약을 통해 전달 됩니다. 컨트롤 계약의 파트를 이해하면 파트 컨트롤 모델을 사용하는 모든 컨트롤의 모양을 사용자 지정할 수 있습니다.  
  
 컨트롤 계약에는 세 가지 요소가 있습니다.  
  
- 컨트롤 논리가 사용하는 시각적 요소  
  
- 컨트롤의 상태 및 각 상태가 속해 있는 그룹  
  
- 컨트롤에 시각적으로 영향을 미치는 공용 속성  
  
### <a name="visual-elements-in-the-control-contract"></a>컨트롤 계약의 시각적 요소  
 컨트롤의 논리가에 있는와 <xref:System.Windows.FrameworkElement> <xref:System.Windows.Controls.ControlTemplate>상호 작용 하는 경우가 있습니다. 예를 들어 컨트롤에서 해당 요소 중 하나의 이벤트를 처리할 수 있습니다. 컨트롤 <xref:System.Windows.FrameworkElement> <xref:System.Windows.Controls.ControlTemplate> 에서의 특정를 찾아야 하는 경우 해당 정보를 작성자에 게 전달 해야 합니다. <xref:System.Windows.Controls.ControlTemplate> 컨트롤은를 사용 <xref:System.Windows.TemplatePartAttribute> 하 여 예상 되는 요소의 형식과 요소의 이름을 전달 합니다. 의 컨트롤 계약에는 <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.ComboBox> 파트가없지만와같은다른컨트롤은<xref:System.Windows.FrameworkElement> 를 수행 합니다.  
  
 다음 예제에서는 <xref:System.Windows.Controls.ComboBox> 클래스에 <xref:System.Windows.TemplatePartAttribute> 지정 된 개체를 보여 줍니다. <xref:System.Windows.Controls.ComboBox> 의 논리는 `PART_EditableTextBox` <xref:System.Windows.Controls.Primitives.Popup> <xref:System.Windows.Controls.TextBox> 에서`PART_Popup` 명명된및<xref:System.Windows.Controls.ControlTemplate>를 찾아야 합니다.  
  
 [!code-csharp[VSMButtonTemplate#ComboBoxContract](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#comboboxcontract)]
 [!code-vb[VSMButtonTemplate#ComboBoxContract](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#comboboxcontract)]  
  
 다음 예제에서는 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.ComboBox> 클래스의 <xref:System.Windows.TemplatePartAttribute> 개체에 의해 <xref:System.Windows.Controls.ComboBox> 지정 된 요소를 포함 하는에 대 한 단순화 된을 보여 줍니다.  
  
 [!code-xaml[VSMButtonTemplate#ComboBoxTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/window1.xaml#comboboxtemplate)]  
  
### <a name="states-in-the-control-contract"></a>컨트롤 계약의 상태  
 컨트롤의 상태도 컨트롤 계약의 파트입니다. 에 <xref:System.Windows.Controls.ControlTemplate> 대해를<xref:System.Windows.Controls.Button> 만드는 예제에서는 상태에 따라의 모양을 지정 하는 방법을 보여줍니다.<xref:System.Windows.Controls.Button> 이 항목의 <xref:System.Windows.VisualState> 앞부분에 나오는 [상태에 따라 컨트롤의 모양 변경](#changing_the_appearance_of_a_control_depending_on_its_state) 에 <xref:System.Windows.TemplateVisualStateAttribute.GroupName%2A> 설명 된 <xref:System.Windows.VisualStateGroup>대로, 지정 된 각 상태에 대 한를 만들고을 공유 하는 모든 <xref:System.Windows.VisualState> 개체를에 배치 합니다. 타사 컨트롤은 <xref:System.Windows.TemplateVisualStateAttribute>를 사용 하 여 상태를 지정 해야 합니다 .이를 통해 식 Blend와 같은 디자이너 도구를 사용 하 여 컨트롤 템플릿 제작을 위한 컨트롤의 상태를 노출할 수 있습니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]와 함께 제공되는 컨트롤의 컨트롤 계약을 찾으려면 [Control 스타일 및 템플릿](control-styles-and-templates.md)을 참조하세요.  
  
### <a name="properties-in-the-control-contract"></a>컨트롤 계약의 속성  
 시각적으로 컨트롤에 영향을 주는 공용 속성도 컨트롤 계약에 포함됩니다. 이러한 속성을 설정 하 여 새 <xref:System.Windows.Controls.ControlTemplate>를 만들지 않고도 컨트롤의 모양을 변경할 수 있습니다. [TemplateBinding](../advanced/templatebinding-markup-extension.md) 태그 확장을 사용 하 여에 있는 요소의 <xref:System.Windows.Controls.ControlTemplate> 속성을에 정의 <xref:System.Windows.Controls.Button>된 공용 속성에 바인딩할 수도 있습니다.  
  
 다음 예제에서는 단추의 컨트롤 계약을 보여 줍니다.  
  
 [!code-csharp[VSMButtonTemplate#ButtonContract](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#buttoncontract)]
 [!code-vb[VSMButtonTemplate#ButtonContract](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#buttoncontract)]  
  
 를 만들 <xref:System.Windows.Controls.ControlTemplate>때 기존 <xref:System.Windows.Controls.ControlTemplate> 으로 시작 하 고 변경 하는 것이 가장 쉬운 경우가 많습니다. 다음 중 하나를 수행 하 여 기존 <xref:System.Windows.Controls.ControlTemplate>를 변경할 수 있습니다.  
  
- 컨트롤 템플릿을 만들기 위한 그래픽 사용자 인터페이스를 제공하는 Expression Blend 등의 디자이너를 사용합니다. 자세한 내용은 [템플릿을 지원하는 컨트롤의 스타일 지정](https://go.microsoft.com/fwlink/?LinkId=161153)을 참조하세요.  
  
- 기본값 <xref:System.Windows.Controls.ControlTemplate> 을 가져오고 편집 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]와 함께 제공되는 기본 컨트롤 템플릿을 찾으려면 [기본 WPF 테마](https://go.microsoft.com/fwlink/?LinkID=158252)를 참조하세요.  
  
<a name="complete_example"></a>   
## <a name="complete-example"></a>완성된 예제  
 다음 예제에서는이 항목에서 <xref:System.Windows.Controls.Button> 설명 하는 전체 <xref:System.Windows.Controls.ControlTemplate> 를 보여 줍니다.  
  
 [!code-xaml[VSMButtonTemplate#3](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#3)]  
  
## <a name="see-also"></a>참고자료

- [스타일 지정 및 템플릿](styling-and-templating.md)
