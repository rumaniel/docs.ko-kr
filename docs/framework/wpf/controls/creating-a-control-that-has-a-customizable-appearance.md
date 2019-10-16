---
title: 사용자 지정 가능한 모양이 있는 컨트롤 만들기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], customizing
- VisualStateManager [WPF], managing the state of a control
- ControlTemplate [WPF], customizing appearance
- controls [WPF], defining the visual structure and behavior of
- customizing appearance [WPF], ControlTemplate
- managing control states [WPF], VisualStateManager
- VisualStateManager [WPF], best practice
ms.assetid: 9e356d3d-a3d0-4b01-a25f-2d43e4d53fe5
ms.openlocfilehash: e428939253065a5f66ca13f3d9f8a3321f3666ec
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67660324"
---
# <a name="creating-a-control-that-has-a-customizable-appearance"></a>사용자 지정 가능한 모양이 있는 컨트롤 만들기

<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 해당 모양을 사용자 지정할 수는 컨트롤을 만들 수가 있습니다. 예를 들어의 모양을 변경할 수 있습니다는 <xref:System.Windows.Controls.CheckBox> 어떤 설정을 제외 속성 작업을 수행 하려면 새 <xref:System.Windows.Controls.ControlTemplate>합니다. 다음 그림에 표시 된 <xref:System.Windows.Controls.CheckBox> 기본값을 사용 하는 <xref:System.Windows.Controls.ControlTemplate> 및 <xref:System.Windows.Controls.CheckBox> 사용자 지정을 사용 하는 <xref:System.Windows.Controls.ControlTemplate>합니다.

![기본 컨트롤 템플릿이 있는 확인란을 선택 합니다. ](./media/ndp-checkboxdefault.png "NDP_CheckBoxDefault") 기본 컨트롤 템플릿을 사용 하는 확인란

![사용자 지정 컨트롤 템플릿 사용 하 여 확인란을 선택 합니다. ](./media/ndp-checkboxcustom.png "NDP_CheckBoxCustom") 사용자 지정 컨트롤 템플릿을 사용 하는 확인란

컨트롤을 만들 때 일부 및 상태 모델을 따르는 경우 컨트롤의 모양을 사용자 지정할 수 있습니다. Microsoft Expression Blend와 같은 디자이너 도구 되도록이 모델을 수행할 때 컨트롤이 이러한 종류의 응용 프로그램에서 사용자 지정 가능한 파트 및 상태 모델을 지원 합니다.  이 항목에서는 파트 및 상태 모델 및 고유한 컨트롤을 만들 때 사용 하는 방법에 설명 합니다. 이 항목에서는 사용자 지정 컨트롤의 예로 `NumericUpDown`을이 모델의 원리를 보여 줍니다.  `NumericUpDown` 컨트롤 사용자 수 증가 또는 컨트롤의 단추를 클릭 하 여 감소 하는 숫자 값을 표시 합니다.  다음 그림에 표시 된 `NumericUpDown` 이 항목에서 설명 하는 컨트롤입니다.

![NumericUpDown 사용자 지정 컨트롤입니다. ](./media/ndp-numericupdown.png "NDP_NumericUPDown") 사용자 지정 NumericUpDown 컨트롤

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [필수 조건](#prerequisites)

- [파트 및 상태 모델](#parts_and_states_model)

- [ControlTemplate에서 시각적 구조 및 컨트롤의 시각적 동작 정의](#defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate)

- [코드에서 ControlTemplate의 부분을 사용 하 여](#using_parts_of_the_controltemplate_in_code)

- [컨트롤 계약을 제공합니다.](#providing_the_control_contract)

- [전체 예제](#complete_example)

<a name="prerequisites"></a>

## <a name="prerequisites"></a>전제 조건

이 항목에서는 새 하는 방법을 알고 있다고 가정 <xref:System.Windows.Controls.ControlTemplate> 기존 컨트롤의 경우 익숙한 컨트롤 계약의 요소를 무엇에 설명 된 개념을 이해 하 고 [하 여 기존 컨트롤의 모양 사용자 지정 ControlTemplate 만들기](customizing-the-appearance-of-an-existing-control.md)합니다.

> [!NOTE]
> 컨트롤에서 상속 되는 모양을 사용자 지정할 수 있는 컨트롤을 만들려면 만들어야 합니다 <xref:System.Windows.Controls.Control> 클래스 또는 해당 서브 클래스 이외의 중 하나 <xref:System.Windows.Controls.UserControl>합니다.  상속 되는 컨트롤 <xref:System.Windows.Controls.UserControl> 신속 하 게 만들 수 있는 컨트롤이 있지만 사용 하지 않습니다는 <xref:System.Windows.Controls.ControlTemplate> 고 모양을 사용자 지정할 수 없습니다.

<a name="parts_and_states_model"></a>

## <a name="parts-and-states-model"></a>파트 및 상태 모델

파트 및 상태 모델이 표시 구조 및 컨트롤의 시각적 동작을 정의 하는 방법을 지정 합니다. 파트 및 상태 모델을 수행 하려면 다음을 수행 해야 합니다.

- 표시 구조 및 시각적 동작을 정의 합니다 <xref:System.Windows.Controls.ControlTemplate> 컨트롤의 합니다.

- 컨트롤의 논리 컨트롤 템플릿의 구성 요소와 상호 작용 하는 경우 특정 모범 사례를 따릅니다.

- 컨트롤 계약에 포함 해야 하는 항목을 지정 하려면 제공 된 <xref:System.Windows.Controls.ControlTemplate>합니다.

표시 구조 및 시각적 동작을 정의 하는 경우는 <xref:System.Windows.Controls.ControlTemplate> 컨트롤의 응용 프로그램 작성자가 만들어 변경할 수 시각적 구조 및 컨트롤의 시각적 동작 새 <xref:System.Windows.Controls.ControlTemplate> 코드를 작성 하는 대신 합니다.   작성자에 게 응용 프로그램에 알려 주는 컨트롤 계약을 제공 해야 합니다 <xref:System.Windows.FrameworkElement> 개체 및 상태에 정의 되어야 합니다는 <xref:System.Windows.Controls.ControlTemplate>합니다. 파트를 사용 하 여 상호 작용할 때 몇 가지 모범 사례를 따라야 합니다 <xref:System.Windows.Controls.ControlTemplate> 컨트롤이 제대로 불완전 처리 되도록 <xref:System.Windows.Controls.ControlTemplate>합니다.  이러한 세 가지 원칙을 따르는 경우 응용 프로그램 작성자는 만들 수는 <xref:System.Windows.Controls.ControlTemplate> 만 컨트롤에 대 한 것 처럼 쉽게 컨트롤에 대 한는으로 제공할 수 있다는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다.  다음 섹션에서는 이러한 권장 사항 세부 정보에서 설명합니다.

<a name="defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate"></a>

## <a name="defining-the-visual-structure-and-visual-behavior-of-a-control-in-a-controltemplate"></a>ControlTemplate에서 시각적 구조 및 컨트롤의 시각적 동작 정의

컨트롤의 시각적 구조와 시각적 동작에서 정의 파트 및 상태 모델을 사용 하 여 사용자 지정 컨트롤을 만들면 해당 <xref:System.Windows.Controls.ControlTemplate> 대신 해당 논리에서입니다.  컨트롤의 시각적 구조가의 복합 <xref:System.Windows.FrameworkElement> 컨트롤을 구성 하는 개체입니다.  시각적 동작은 컨트롤이 특정 상태에 있을 때 표시 되는 방식을 보여 줍니다.   만들기에 대 한 자세한 내용은 <xref:System.Windows.Controls.ControlTemplate> 시각적 구조 및 컨트롤의 시각적 동작을 지정 하는 내용은 [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)합니다.

예제에서는 `NumericUpDown` 컨트롤을 시각적 구조에 두 개의 <xref:System.Windows.Controls.Primitives.RepeatButton> 컨트롤 및 <xref:System.Windows.Controls.TextBlock>합니다.  코드에서 이러한 컨트롤을 추가 하는 경우는 `NumericUpDown` 생성자를 통해 예를 들어-컨트롤-컨트롤의 위치를 변경할 수 없습니다.  코드에서 컨트롤의 시각적 구조와 시각적 동작을 정의 하는 대신에 정의 해야 하는 <xref:System.Windows.Controls.ControlTemplate>합니다.  단추 위치를 사용자 지정 하려면 다음 응용 프로그램 개발자 및 <xref:System.Windows.Controls.TextBlock> 발생 하는 동작을 지정 하 고 때 `Value` 음수인 때문에 <xref:System.Windows.Controls.ControlTemplate> 바꿀 수 있습니다.

다음 예제에서는 시각적 구조를 보여 줍니다.는 `NumericUpDown` 포함 된 컨트롤을 <xref:System.Windows.Controls.Primitives.RepeatButton> 늘리려면 `Value`, <xref:System.Windows.Controls.Primitives.RepeatButton> 감소 `Value`, 및 <xref:System.Windows.Controls.TextBlock> 표시할 `Value`합니다.

[!code-xaml[VSMCustomControl#VisualStructure](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#visualstructure)]

시각적 동작을 `NumericUpDown` 컨트롤은 음수 이면 값을 빨간색 글꼴로입니다.  변경 하는 경우는 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 의 <xref:System.Windows.Controls.TextBlock> 때 코드에서 합니다 `Value` 음수인 경우는 `NumericUpDown` 빨간색 음수 값을 항상 표시 됩니다. 컨트롤의 시각적 동작을 지정 합니다 <xref:System.Windows.Controls.ControlTemplate> 를 추가 하 여 <xref:System.Windows.VisualState> 개체를 <xref:System.Windows.Controls.ControlTemplate>합니다.  다음 예제와 합니다 <xref:System.Windows.VisualState> 에 대 한 개체를 `Positive` 및 `Negative` 상태입니다.  `Positive` 및 `Negative` (컨트롤은 항상 두 가지 중 하나)은 상호 배타적 이므로 예제에서는 배치 합니다 <xref:System.Windows.VisualState> 개체를 하나의 <xref:System.Windows.VisualStateGroup>합니다.  컨트롤을 이동 하는 경우는 `Negative` 상태는 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 의 <xref:System.Windows.Controls.TextBlock> 빨간색으로 변합니다.  컨트롤에는 `Positive` 상태는 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 원래 값으로 반환 합니다.  정의 <xref:System.Windows.VisualState> 개체를 <xref:System.Windows.Controls.ControlTemplate> 에 대해 자세히 설명 [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)합니다.

> [!NOTE]
> 설정 해야 합니다 <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> 루트에 연결 <xref:System.Windows.FrameworkElement> 의 <xref:System.Windows.Controls.ControlTemplate>합니다.

[!code-xaml[VSMCustomControl#ValueStates](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]

<a name="using_parts_of_the_controltemplate_in_code"></a>

## <a name="using-parts-of-the-controltemplate-in-code"></a>코드에서 ControlTemplate의 부분을 사용 하 여

A <xref:System.Windows.Controls.ControlTemplate> 작성자 생략할 수 있습니다 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.VisualState> 개체를 실수로 또는 의도적으로 컨트롤의 논리가 제대로 작동 하려면 이러한 부분이 필요할 수 있지만. 파트 및 상태 모델 컨트롤에도 잘 복원 되도록 지정 된 <xref:System.Windows.Controls.ControlTemplate> 없는 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.VisualState> 개체입니다.  컨트롤 해야 하지 예외를 throw 하거나 보고서 오류가 발생 하는 경우는 <xref:System.Windows.FrameworkElement>, <xref:System.Windows.VisualState>, 또는 <xref:System.Windows.VisualStateGroup> 없습니다를 <xref:System.Windows.Controls.ControlTemplate>입니다. 이 섹션에서는 상호 작용 하기 위한 권장된 사례를 설명 합니다. <xref:System.Windows.FrameworkElement> 개체 및 상태를 관리 합니다.

### <a name="anticipate-missing-frameworkelement-objects"></a>누락 된 FrameworkElement 개체 예상

정의 하는 경우 <xref:System.Windows.FrameworkElement> 개체는 <xref:System.Windows.Controls.ControlTemplate>, 컨트롤의 논리를 그 중 일부와 상호 작용 해야 할 수 있습니다.  예를 들어,를 `NumericUpDown` 제어 단추의 구독할 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 증가 또는 감소 하려면 이벤트 `Value` 설정 및를 <xref:System.Windows.Controls.TextBlock.Text%2A> 의 속성을 <xref:System.Windows.Controls.TextBlock> 를 `Value`. 사용자 지정 하는 경우 <xref:System.Windows.Controls.ControlTemplate> 생략는 <xref:System.Windows.Controls.TextBlock> 는 컨트롤이 해당 기능의 일부를 잃을 있지만 컨트롤 해도 오류가 발생 하지 않도록 해야 허용 되는 단추 또는 합니다. 예를 들어 경우는 <xref:System.Windows.Controls.ControlTemplate> 변경 하는 단추가 없습니다 `Value`의 `NumericUpDown` 는 기능만 사용 하는 응용 프로그램을 잃을 <xref:System.Windows.Controls.ControlTemplate> 계속 실행 됩니다.

다음 사례 컨트롤 누락 올바르게 응답 하면 <xref:System.Windows.FrameworkElement> 개체:

1. 설정 된 `x:Name` 각각에 대 한 특성 <xref:System.Windows.FrameworkElement> 코드에서 참조 해야 하는 합니다.

2. 각각에 대 한 개인 속성 정의 <xref:System.Windows.FrameworkElement> 상호 작용 해야 하는 합니다.

3. 구독 하 고 컨트롤에서 처리 하는 모든 이벤트를 구독 취소를 <xref:System.Windows.FrameworkElement> 속성의 set 접근자입니다.

4. 설정 된 <xref:System.Windows.FrameworkElement> 에 정의 된 속성 2 단계는 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> 메서드. 이 가능한 한 빨리는 <xref:System.Windows.FrameworkElement> 에 <xref:System.Windows.Controls.ControlTemplate> 컨트롤에 사용할 수입니다. 사용 하 여는 `x:Name` 의 <xref:System.Windows.FrameworkElement> 에서 가져오려는 <xref:System.Windows.Controls.ControlTemplate>합니다.

5. 있는지 여부를 확인 합니다 <xref:System.Windows.FrameworkElement> 아닙니다 `null` 해당 멤버에 액세스 하기 전에 합니다.  있으면 `null`, 오류를 보고 하지 않습니다.

다음 예제에 나온 방법을 `NumericUpDown` 컨트롤이와 상호 작용 <xref:System.Windows.FrameworkElement> 앞의 목록에서 권장 사항에 따라 개체입니다.

시각적 구조를 정의 하는 예제는 `NumericUpDown` 에서 제어를 <xref:System.Windows.Controls.ControlTemplate>의 <xref:System.Windows.Controls.Primitives.RepeatButton> 증가 시키는 `Value` 에 해당 `x:Name` 특성이로 설정 `UpButton`.  다음 예제에서는 라는 속성을 선언 `UpButtonElement` 나타내는 합니다 <xref:System.Windows.Controls.Primitives.RepeatButton> 에 선언 된는 <xref:System.Windows.Controls.ControlTemplate>합니다. `set` 접근자 먼저 구독을 취소 단추를 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트 경우 `UpDownElement` 아닙니다 `null`속성을 설정 하 고를 구독 합니다 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트입니다. 정의 되었지만 다른 여기에 표시 되지 않는 속성 이기도 <xref:System.Windows.Controls.Primitives.RepeatButton>라는 `DownButtonElement`합니다.

[!code-csharp[VSMCustomControl#UpButtonProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#upbuttonproperty)]
[!code-vb[VSMCustomControl#UpButtonProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#upbuttonproperty)]

다음 예제와 합니다 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> 에 대 한는 `NumericUpDown` 제어 합니다.  이 예제에서는 사용 합니다 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> 메서드를를 <xref:System.Windows.FrameworkElement> 에서 개체를 <xref:System.Windows.Controls.ControlTemplate>.  예제 으로부터 보호 하는 경우 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> 찾습니다는 <xref:System.Windows.FrameworkElement> 예상 된 유형이 아닌 지정 된 이름의 합니다. 지정된 된 요소를 무시 하는 것이 좋습니다 이기도 `x:Name` 하지만 형식이 잘못 되었습니다.

[!code-csharp[VSMCustomControl#ApplyTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
[!code-vb[VSMCustomControl#ApplyTemplate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]

앞의 예제에 표시 되는 사례를 따라 하는 컨트롤은 계속 실행 되도록 때 합니다 <xref:System.Windows.Controls.ControlTemplate> 없습니다를 <xref:System.Windows.FrameworkElement>입니다.

### <a name="use-the-visualstatemanager-to-manage-states"></a>상태를 관리 하는 VisualStateManager 사용

<xref:System.Windows.VisualStateManager> 컨트롤의 상태를 추적 하며 상태를 전환 하는 데 필요한 논리를 수행 합니다. 추가 하는 경우 <xref:System.Windows.VisualState> 개체를 <xref:System.Windows.Controls.ControlTemplate>, 추가할를 <xref:System.Windows.VisualStateGroup> 추가 <xref:System.Windows.VisualStateGroup> 에 <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> 연결 된 속성 있도록는 <xref:System.Windows.VisualStateManager> 에 대 한 액세스 권한이 합니다.

다음 예제에서는 이전 예제를 보여 주는 반복 합니다 <xref:System.Windows.VisualState> 에 해당 하는 개체를 `Positive` 및 `Negative` 컨트롤의 상태입니다. <xref:System.Windows.Media.Animation.Storyboard> 에 `Negative` <xref:System.Windows.VisualState> 설정 합니다 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 의 <xref:System.Windows.Controls.TextBlock> 빨간색.   경우는 `NumericUpDown` 컨트롤이 합니다 `Negative` 상태에서 스토리 보드를 `Negative` 상태가 시작.  그런 다음 <xref:System.Windows.Media.Animation.Storyboard> 에 `Negative` 컨트롤에 반환 될 때 중지 상태는 `Positive` 상태입니다.  `Positive` <xref:System.Windows.VisualState> 포함할 필요가 없습니다를 <xref:System.Windows.Media.Animation.Storyboard> 때문에 때를 <xref:System.Windows.Media.Animation.Storyboard> 에 대 한 합니다 `Negative` 중지 되 면는 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 원래 색을 반환 합니다.

[!code-xaml[VSMCustomControl#ValueStates](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]

<xref:System.Windows.Controls.TextBlock> 는 이름이 지정 됩니다 있지만 <xref:System.Windows.Controls.TextBlock> 에 대 한 컨트롤 계약에 없는 `NumericUpDown` 컨트롤의 논리 되지 참조 하기 때문에 <xref:System.Windows.Controls.TextBlock>합니다.  참조 되는 요소는 <xref:System.Windows.Controls.ControlTemplate> 이름을 갖지만 이므로 컨트롤 계약 포함 될 필요가 없습니다 새 <xref:System.Windows.Controls.ControlTemplate> 해당 요소를 참조 하는 컨트롤에 필요 하지 수에 대 한 합니다.  예를 들어, 사용자를 만듭니다 <xref:System.Windows.Controls.ControlTemplate> 에 대 한 `NumericUpDown` 나타내지 수도 `Value` 변경 하 여 음수인는 <xref:System.Windows.Controls.Control.Foreground%2A>합니다.  이런 경우, 모두 코드에서에서 또는 <xref:System.Windows.Controls.ControlTemplate> 참조는 <xref:System.Windows.Controls.TextBlock> 이름별 합니다.

컨트롤의 논리는 컨트롤의 상태를 변경 하는 일을 담당 합니다. 다음 예에서는 `NumericUpDown` 컨트롤을 호출 합니다 <xref:System.Windows.VisualStateManager.GoToState%2A> 로 이동 하는 방법을 `Positive` 상태의 `Value` 가 0 보다 크거나 및 `Negative` 상태의 `Value` 0 보다 작습니다.

[!code-csharp[VSMCustomControl#ValueStateChange](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#valuestatechange)]
[!code-vb[VSMCustomControl#ValueStateChange](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#valuestatechange)]

<xref:System.Windows.VisualStateManager.GoToState%2A> 메서드 시작 및 스토리 보드를 적절 하 게 중지 하는 데 필요한 논리를 수행 합니다. 컨트롤을 호출 하는 경우 <xref:System.Windows.VisualStateManager.GoToState%2A> 해당 상태를 변경 하는 <xref:System.Windows.VisualStateManager> 다음을 수행 합니다.

- 경우는 <xref:System.Windows.VisualState> 에 컨트롤 것임을 <xref:System.Windows.Media.Animation.Storyboard>, 스토리 보드를 시작 합니다. 그런 다음 경우는 <xref:System.Windows.VisualState> 가 컨트롤에서 제공 되는 <xref:System.Windows.Media.Animation.Storyboard>, 스토리 보드 끝입니다.

- 지정 된 상태의 컨트롤이 이미 있으면 <xref:System.Windows.VisualStateManager.GoToState%2A> 조치가 받아서 반환 `true`합니다.

- 지정 된 상태에 없는 경우는 <xref:System.Windows.Controls.ControlTemplate> 의 `control`, <xref:System.Windows.VisualStateManager.GoToState%2A> 아무 작업도 수행 하 고 반환 `false`합니다.

#### <a name="best-practices-for-working-with-the-visualstatemanager"></a>VisualStateManager를 사용 하기 위한 모범 사례

컨트롤의 상태를 유지 하기 위해 다음을 수행 하는 것이 좋습니다.

- 속성을 사용 하 여 해당 상태를 추적 합니다.

- 상태 간 전환 도우미 메서드를 만듭니다.

합니다 `NumericUpDown` 컨트롤이 사용 하 해당 `Value` 인지 여부를 추적 하는 속성을 `Positive` 또는 `Negative` 상태입니다.  `NumericUpDown` 컨트롤 정의 `Focused` 및 `UnFocused` 상태에 추적을 <xref:System.Windows.UIElement.IsFocused%2A> 속성. 컨트롤의 속성에 자연스럽 게 일치 하지 않는 상태를 사용 하는 경우에 상태를 추적 하는 개인 속성을 정의할 수 있습니다.

모든 상태를 업데이트 하는 단일 메서드 호출을 중앙 집중화 된 <xref:System.Windows.VisualStateManager> 하 고 관리 하기 쉬운 코드를 유지 합니다. 다음 예제는 `NumericUpDown` 컨트롤의 도우미 메서드를 `UpdateStates`입니다. 때 `Value` 가 0 보다 크거나 합니다 <xref:System.Windows.Controls.Control> 에 `Positive` 상태입니다.  때 `Value` 가 0 보다 작은 컨트롤에는 `Negative` 상태입니다.  때 <xref:System.Windows.UIElement.IsFocused%2A> 은 `true`, 컨트롤이 합니다 `Focused` 있는 상태이 고; 그렇지 않으면는 `Unfocused` 상태입니다.  컨트롤을 호출할 수 `UpdateStates` 때마다 상태 변경에 관계 없이 해당 상태를 변경 해야 합니다.

[!code-csharp[VSMCustomControl#UpdateStates](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#updatestates)]
[!code-vb[VSMCustomControl#UpdateStates](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#updatestates)]

상태 이름을 전달 하는 경우 <xref:System.Windows.VisualStateManager.GoToState%2A> 컨트롤이 있는 경우 이미 해당 상태를 <xref:System.Windows.VisualStateManager.GoToState%2A> 컨트롤의 현재 상태를 확인할 필요가 있으므로, 아무 작업도 수행 합니다.  예를 들어 경우 `Value` 음수가에서 다른 음수 이면에 대 한 스토리 보드로 변경 합니다 `Negative` 상태는 중단 되지 않습니다 및 사용자 컨트롤의 변경 표시 되지 것입니다.

합니다 <xref:System.Windows.VisualStateManager> 사용 하 여 <xref:System.Windows.VisualStateGroup> 개체를 호출할 때 종료 상태를 확인 하려면 <xref:System.Windows.VisualStateManager.GoToState%2A>합니다. 각각에 대 한 한 상태의 컨트롤은 항상 <xref:System.Windows.VisualStateGroup> 에 정의 된 해당 <xref:System.Windows.Controls.ControlTemplate> 와 같은 다른 상태로 전환 될 때 상태를 그대로 남겨 두기 <xref:System.Windows.VisualStateGroup>합니다. 예를 들어를 <xref:System.Windows.Controls.ControlTemplate> 의 `NumericUpDown` 컨트롤을 정의 합니다 `Positive` 및 `Negative` <xref:System.Windows.VisualState> 개체를 <xref:System.Windows.VisualStateGroup> 및 `Focused` 및 `Unfocused` <xref:System.Windows.VisualState> 다른 개체입니다. (볼 수 있습니다는 `Focused` 및 `Unfocused` <xref:System.Windows.VisualState> 에 정의 된를 [전체 예제](#complete_example) 컨트롤에서 이동 하는 경우이 항목의 섹션을 `Positive` 상태를 `Negative` 상태 또는 그 반대의 경우는 컨트롤에서 유지 합니다 `Focused` 또는 `Unfocused` 상태입니다.

세 가지 일반적인 위치는 컨트롤의 상태는 변경 될 수 있습니다.

- 경우는 <xref:System.Windows.Controls.ControlTemplate> 에 적용 되는 <xref:System.Windows.Controls.Control>합니다.

- 속성을 변경 하는 경우.

- 이벤트가 발생 합니다.

다음 예에서는 설명의 상태를 업데이트 합니다 `NumericUpDown` 이러한 경우에는 컨트롤입니다.

컨트롤의 상태를 업데이트 해야 합니다 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> 메서드 올바른에 컨트롤이 표시 되도록 상태의 <xref:System.Windows.Controls.ControlTemplate> 적용 됩니다. 다음 예제에서는 `UpdateStates` 에서 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> 적절 한 상태의 컨트롤 인지 확인 합니다.  예를 들어, 사용자가 만든를 `NumericUpDown` 컨트롤을 설정한 후 해당 <xref:System.Windows.Controls.Control.Foreground%2A> 녹색으로 및 `Value` -5입니다.  호출 하지 않으면 `UpdateStates` 때를 <xref:System.Windows.Controls.ControlTemplate> 에 적용 되는 `NumericUpDown` 컨트롤을 컨트롤에 없는 경우.는 `Negative` 상태 및 값은 녹색이 빨간색 대신 합니다.  호출 해야 합니다 `UpdateStates` 컨트롤에 삽입할는 `Negative` 상태입니다.

[!code-csharp[VSMCustomControl#ApplyTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
[!code-vb[VSMCustomControl#ApplyTemplate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]

속성이 변경 될 때 컨트롤의 상태를 업데이트 해야 합니다. 다음 예제에서는 전체 `ValueChangedCallback` 메서드. 때문에 `ValueChangedCallback` 될 때 호출 됩니다 `Value` 변경에 대 한 메서드 호출 `UpdateStates` 경우 `Value` 에서 양수 부정 하거나 반대로 변경 합니다. 호출 하는 것이 좋습니다 `UpdateStates` 때 `Value` 변경 되지만 경우 컨트롤 변경 되지 않으므로 상태 양수와 음수 모두 유지 됩니다.

[!code-csharp[VSMCustomControl#EntireValueChangedCallback](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#entirevaluechangedcallback)]
[!code-vb[VSMCustomControl#EntireValueChangedCallback](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#entirevaluechangedcallback)]

이벤트가 발생할 때 상태를 업데이트 해야 할 수 있습니다. 다음 예에서는 합니다 `NumericUpDown` 호출 `UpdateStates` 에 <xref:System.Windows.Controls.Control> 처리 하는 <xref:System.Windows.UIElement.GotFocus> 이벤트.

[!code-csharp[VSMCustomControl#OnGotFocus](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#ongotfocus)]
[!code-vb[VSMCustomControl#OnGotFocus](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#ongotfocus)]

<xref:System.Windows.VisualStateManager> 컨트롤의 상태를 관리할 수 있습니다. 사용 하 여는 <xref:System.Windows.VisualStateManager>는 컨트롤이 올바르게 전환 상태를 확인 합니다.  작업에 대 한이 섹션에 설명 된 권장 사항을 수행 하는 경우는 <xref:System.Windows.VisualStateManager>, 컨트롤의 코드는 읽기 쉽고 유지 됩니다.

<a name="providing_the_control_contract"></a>

## <a name="providing-the-control-contract"></a>컨트롤 계약을 제공합니다.

컨트롤 계약을 제공 하도록 <xref:System.Windows.Controls.ControlTemplate> 작성자 서식 파일에 배치 하 게 알 수 있습니다. 컨트롤 계약에는 세 가지 요소가 있습니다.

- 컨트롤 논리가 사용하는 시각적 요소

- 컨트롤의 상태 및 각 상태가 속해 있는 그룹

- 컨트롤에 시각적으로 영향을 미치는 공용 속성

새 사람 <xref:System.Windows.Controls.ControlTemplate> 알고 <xref:System.Windows.FrameworkElement> 개체를 사용 하 여 컨트롤의 논리를 각 개체 유형을 이며, 어떤 이름은. A <xref:System.Windows.Controls.ControlTemplate> 작성자는 또한 컨트롤의 가능한 가능한 각 상태와만 이름을 알고 해야 <xref:System.Windows.VisualStateGroup> 상태는 합니다.

반환 합니다 `NumericUpDown` 예제에서는 컨트롤이 예상 합니다 <xref:System.Windows.Controls.ControlTemplate> 다음 사항이 <xref:System.Windows.FrameworkElement> 개체:

- A <xref:System.Windows.Controls.Primitives.RepeatButton> 호출 `UpButton`합니다.

- <xref:System.Windows.Controls.Primitives.RepeatButton> 호출 `DownButton.`

 컨트롤 상태에서 수 있습니다.

- 안에 `ValueStates`<xref:System.Windows.VisualStateGroup>

  - `Positive`

  - `Negative`

- 안에 `FocusStates`<xref:System.Windows.VisualStateGroup>

  - `Focused`

  - `Unfocused`

동작을 지정 하 <xref:System.Windows.FrameworkElement> 개체 컨트롤, 사용를 <xref:System.Windows.TemplatePartAttribute>, 이름과 예상 되는 요소의 형식을 지정 합니다.  컨트롤의 가능한 상태를 지정 하려면 사용 합니다 <xref:System.Windows.TemplateVisualStateAttribute>, 및 상태의 이름을 지정 하는 <xref:System.Windows.VisualStateGroup> 에 속합니다.  배치 된 <xref:System.Windows.TemplatePartAttribute> 및 <xref:System.Windows.TemplateVisualStateAttribute> 컨트롤의 클래스 정의에 있습니다.

컨트롤의 모양에 영향을 주는 모든 공용 속성 컨트롤 계약의 일부 이기도 합니다.

다음 예제에서는 지정 된 <xref:System.Windows.FrameworkElement> 개체 및 상태에 대 한는 `NumericUpDown` 컨트롤입니다.

[!code-csharp[VSMCustomControl#ControlContract](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controlcontract)]
[!code-vb[VSMCustomControl#ControlContract](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controlcontract)]

<a name="complete_example"></a>

## <a name="complete-example"></a>완성된 예제

다음 예제는 전체 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 `NumericUpDown` 제어 합니다.

[!code-xaml[VSMCustomControl#NUDTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/themes/generic.xaml#nudtemplate)]

다음 예제에 대 한 논리는 `NumericUpDown`합니다.

[!code-csharp[VSMCustomControl#ControlLogic](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controllogic)]
[!code-vb[VSMCustomControl#ControlLogic](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controllogic)]

## <a name="see-also"></a>참고자료

- [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)
- [컨트롤 사용자 지정](control-customization.md)
