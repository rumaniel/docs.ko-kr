---
title: 컨트롤 제작 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], authoring overview
- authoring overview for controls [WPF]
ms.assetid: 3d864748-cff0-4e63-9b23-d8e5a635b28f
ms.openlocfilehash: 61cd7b61a586afa2addd55acff7cac6d16d92a1f
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70374534"
---
# <a name="control-authoring-overview"></a>컨트롤 제작 개요

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 컨트롤 모델의 확장성 덕분에 새 컨트롤을 만들 필요성이 상당히 줄어들었습니다. 그러나 어떤 경우에는 여전히 사용자 지정 컨트롤을 만들어야 할 수 있습니다. 이 항목에서는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 사용자 지정 컨트롤과 다양한 컨트롤 제작 모델을 만들 필요성을 최소화시키는 기능에 대해 설명합니다. 또한 새 컨트롤을 만드는 방법을 설명합니다.

<a name="when_to_write_a_new_control"></a>

## <a name="alternatives-to-writing-a-new-control"></a>새 컨트롤 작성에 대한 대안

지금까지 기존 컨트롤에서 사용자 지정 환경을 구현하려고 하면 배경색, 테두리 너비 및 글꼴 크기와 같은 컨트롤의 표준 속성을 변경하는 것으로 제한되어 있었습니다. 미리 정의된 이러한 매개 변수 이상으로 컨트롤의 모양이나 동작을 확장하려면 일반적으로 기존 컨트롤에서 상속받게 하고 컨트롤 그리기를 담당하는 메서드를 재정의하여 새 컨트롤을 만들어야 했습니다.  여전히 옵션이기는 하지만 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용하면 풍부한 콘텐츠 모델, 스타일, 템플릿 및 트리거를 사용하여 기존 컨트롤을 사용자 지정할 수 있습니다. 다음 목록에는 새 컨트롤을 만들지 않고 이러한 기능을 사용하여 사용자 지정 및 일관된 환경을 만드는 예제가 나와 있습니다.

- **풍부한 콘텐츠.** 많은 표준 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤이 풍부한 콘텐츠를 지원합니다. 예를 들어의 <xref:System.Windows.Controls.Button> content 속성은 형식이 <xref:System.Object>이므로 이론적으로 모든 항목을에 표시할 <xref:System.Windows.Controls.Button>수 있습니다.  단추에 이미지와 텍스트 <xref:System.Windows.Controls.TextBlock> 를 표시 하려면 이미지 <xref:System.Windows.Controls.StackPanel> 와를에 추가 하 <xref:System.Windows.Controls.ContentControl.Content%2A> 고를 속성 <xref:System.Windows.Controls.StackPanel> 에 할당 하면 됩니다. 이러한 컨트롤은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시각적 요소와 임의의 데이터를 표시할 수 있기 때문에 복잡한 시각화를 지원하기 위해 새 컨트롤을 만들거나 기존 컨트롤을 수정할 필요성이 적습니다. <xref:System.Windows.Controls.Button> 의[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]콘텐츠 모델과 기타 콘텐츠 모델에 대 한 자세한 내용은 [WPF 콘텐츠 모델](wpf-content-model.md)을 참조 하세요.

- **스타일.** 는 <xref:System.Windows.Style> 컨트롤의 속성을 나타내는 값의 컬렉션입니다. 스타일을 사용하면 새 컨트롤을 작성하지 않고도 원하는 컨트롤 모양과 동작을 재사용 가능한 표현으로 만들 수 있습니다. 예를 들어, 모든 <xref:System.Windows.Controls.TextBlock> 컨트롤의 글꼴 크기가 14 인 빨강 굴림 글꼴을 사용 하려는 경우를 가정해 보겠습니다. 스타일을 리소스로 만들고 이에 따라 적절한 속성을 설정할 수 있습니다. 그러면 응용 <xref:System.Windows.Controls.TextBlock> 프로그램에 추가 하는 모든 것이 같은 모양입니다.

- **데이터 템플릿.** 를 <xref:System.Windows.DataTemplate> 사용 하면 컨트롤에 데이터가 표시 되는 방식을 사용자 지정할 수 있습니다. 예를 들어, <xref:System.Windows.DataTemplate> 를 사용 하 여 <xref:System.Windows.Controls.ListBox>에 데이터를 표시 하는 방법을 지정할 수 있습니다.  이에 대한 예제는 [데이터 템플릿 개요](../data/data-templating-overview.md)를 참조하세요.  데이터의 모양을 사용자 지정 하는 것 외에 <xref:System.Windows.DataTemplate> 도에는 사용자 지정 ui에서 많은 유연성을 제공 하는 UI 요소가 포함 될 수 있습니다.  예를 들어를 사용 하 <xref:System.Windows.DataTemplate>여 각 항목에 확인란 <xref:System.Windows.Controls.ComboBox> 을 포함 하는을 만들 수 있습니다.

- **컨트롤 템플릿.** 의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 많은 컨트롤은를 <xref:System.Windows.Controls.ControlTemplate> 사용 하 여 컨트롤의 모양과 모양을 정의 합니다 .이 컨트롤의 모양은 컨트롤의 기능과 구분 됩니다. 를 재정의 <xref:System.Windows.Controls.ControlTemplate>하 여 컨트롤의 모양을 크게 변경할 수 있습니다.  예를 들어 신호등 모양의 컨트롤이 필요하다고 가정해 보겠습니다. 이 컨트롤에는 간단한 사용자 인터페이스 및 기능이 있습니다.  컨트롤은 세 개의 원으로, 한 번에 하나씩만 불을 켤 수 있습니다. 일부 리플렉션 후에는가 <xref:System.Windows.Controls.RadioButton> 한 번에 하나만 선택 하는 기능을 제공 하는 것을 알 수 있지만의 기본 모양은 <xref:System.Windows.Controls.RadioButton> 신호등의 조명 처럼 보입니다.  는 <xref:System.Windows.Controls.RadioButton> 컨트롤 템플릿을 사용 하 여 모양을 정의 하기 때문에 컨트롤의 요구 사항에 맞게 <xref:System.Windows.Controls.ControlTemplate> 를 다시 정의 하 고 라디오 단추를 사용 하 여 신호등을 만듭니다.

  > [!NOTE]
  > 는 <xref:System.Windows.Controls.RadioButton> 를 <xref:System.Windows.DataTemplate> 사용할<xref:System.Windows.DataTemplate> 수 있지만이 예제에서는이 충분 하지 않습니다.  는 <xref:System.Windows.DataTemplate> 컨트롤 내용의 모양을 정의 합니다. 의 <xref:System.Windows.Controls.RadioButton>경우 콘텐츠는 <xref:System.Windows.Controls.RadioButton> 가 선택 되었는지 여부를 나타내는 원의 오른쪽에 표시 됩니다.  신호등의 예제에서 라디오 버튼은 "불을 켤 수 있는" 원이어야 합니다. 신호등의 모양 요구 사항은의 기본 모양과 <xref:System.Windows.Controls.RadioButton>다르기 때문에를 다시 <xref:System.Windows.Controls.ControlTemplate>정의 해야 합니다.  일반적 <xref:System.Windows.DataTemplate> 으로는 컨트롤의 콘텐츠 (또는 데이터)를 정의 하는 데 사용 되 <xref:System.Windows.Controls.ControlTemplate> 고는 컨트롤의 구성 방법을 정의 하는 데 사용 됩니다.

- **트리거.** 를 <xref:System.Windows.Trigger> 사용 하면 새 컨트롤을 만들지 않고도 컨트롤의 모양과 동작을 동적으로 변경할 수 있습니다. 예를 들어 응용 프로그램에 여러 <xref:System.Windows.Controls.ListBox> 컨트롤이 있고 각 <xref:System.Windows.Controls.ListBox> 컨트롤이 선택 된 경우 굵게 표시 되 고 빨간색으로 표시 되도록 하려는 경우를 가정해 보겠습니다. 첫 번째 이러한은에서 <xref:System.Windows.Controls.ListBox> 상속 하는 클래스를 만들고 메서드를 <xref:System.Windows.Controls.Primitives.Selector.OnSelectionChanged%2A> 재정의 하 여 선택한 항목의 모양을 변경 하는 것이 아니라,의 모양을 변경 <xref:System.Windows.Controls.ListBoxItem> 하는의 스타일에 트리거를 추가 하는 것이 더 나은 방법입니다. 선택한 항목입니다. 트리거를 사용하면 속성 값을 변경하거나 속성 값을 기반으로 작업을 수행할 수 있습니다. 를 <xref:System.Windows.EventTrigger> 사용 하면 이벤트가 발생할 때 작업을 수행할 수 있습니다.

스타일, 템플릿 및 트리거에 대한 자세한 내용은 [스타일 지정 및 템플릿](styling-and-templating.md)을 참조하세요.

일반적으로 컨트롤이 기존 컨트롤의 기능을 반영하지만 컨트롤이 다르게 보이게 하려면 이 섹션에서 설명하는 메서드 중 하나를 사용하여 기존 컨트롤의 모양을 변경할 수 있는지 여부를 먼저 고려해야 합니다.

<a name="models_for_control_authoring"></a>

## <a name="models-for-control-authoring"></a>컨트롤 제작 모델

풍부한 콘텐츠 모델, 스타일, 템플릿 및 트리거를 사용하면 새 컨트롤을 만들어야 하는 필요성이 최소화됩니다. 그러나 새 컨트롤을 만들어야 한다면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 다양한 컨트롤 제작 모델을 이해하는 것이 중요합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 컨트롤을 만들기 위해 세 가지 일반적인 모델을 제공하며 각 모델은 서로 다른 일련의 기능과 유연성 수준을 제공합니다. 세 모델 <xref:System.Windows.Controls.UserControl>의 기본 클래스는, <xref:System.Windows.Controls.Control>및 <xref:System.Windows.FrameworkElement>입니다.

### <a name="deriving-from-usercontrol"></a>UserControl에서 파생

에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤을 만드는 가장 간단한 방법은에서 <xref:System.Windows.Controls.UserControl>파생 하는 것입니다. 에서 <xref:System.Windows.Controls.UserControl>상속 되는 컨트롤을 빌드하는 경우 기존 구성 요소 <xref:System.Windows.Controls.UserControl>를에 추가 하 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]고, 구성 요소의 이름을로 표시 하 고, 이벤트 처리기를 참조 합니다. 그런 다음 코드에서 명명된 요소를 참조하고 이벤트 처리기를 정의할 수 있습니다. 이 개발 모델은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 애플리케이션 개발에 사용된 모델과 매우 유사합니다.

올바르게 빌드된 경우는 <xref:System.Windows.Controls.UserControl> 풍부한 콘텐츠, 스타일 및 트리거의 이점을 활용할 수 있습니다. 그러나 컨트롤을에서 <xref:System.Windows.Controls.UserControl>상속 하는 경우에는 <xref:System.Windows.DataTemplate> 컨트롤을 사용 하는 사용자가 또는 <xref:System.Windows.Controls.ControlTemplate> 를 사용 하 여 모양을 사용자 지정할 수 없습니다.  템플릿을 지 원하는 사용자 지정 컨트롤을 <xref:System.Windows.Controls.Control> 만들려면 클래스 또는 해당 파생 클래스 중 하나 ( <xref:System.Windows.Controls.UserControl>이외의)에서 파생 해야 합니다.

#### <a name="benefits-of-deriving-from-usercontrol"></a>UserControl에서 파생하는 이점

다음 모두가 적용 <xref:System.Windows.Controls.UserControl> 되는 경우에서 파생 하는 것이 좋습니다.

- 애플리케이션을 빌드하는 방법과 유사하게 컨트롤을 빌드하려고 합니다.

- 컨트롤이 기존 구성 요소로만 구성됩니다.

- 복잡한 사용자 지정을 지원하지 않아도 됩니다.

### <a name="deriving-from-control"></a>Control에서 파생

<xref:System.Windows.Controls.Control> 클래스에서 파생 하는 것은 대부분의 기존 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에서 사용 하는 모델입니다. <xref:System.Windows.Controls.Control> 클래스에서 상속 되는 컨트롤을 만들 때 템플릿을 사용 하 여 해당 컨트롤의 모양을 정의 합니다. 그렇게 함으로써 작동 논리를 시각적 표현과 분리합니다. 이벤트 대신 명령 및 바인딩을 사용 하 고 가능 하면 <xref:System.Windows.Controls.ControlTemplate> 에서 요소를 참조 하지 않도록 UI와 논리의 분리를 보장할 수도 있습니다.  컨트롤의 UI와 논리가 적절히 분리 된 경우 컨트롤의 사용자는 컨트롤 <xref:System.Windows.Controls.ControlTemplate> 의 모양을 다시 정의 하 여 모양을 사용자 지정할 수 있습니다. 사용자 지정 <xref:System.Windows.Controls.Control> 을 빌드하는 것 만큼 <xref:System.Windows.Controls.UserControl>간단 하지는 않지만 사용자 지정 <xref:System.Windows.Controls.Control> 은 가장 뛰어난 유연성을 제공 합니다.

#### <a name="benefits-of-deriving-from-control"></a>Control에서 파생하는 이점

다음 중 하나가 <xref:System.Windows.Controls.Control> 적용 되는 경우 <xref:System.Windows.Controls.UserControl> 클래스를 사용 하는 대신에서 파생 하는 것이 좋습니다.

- 를 <xref:System.Windows.Controls.ControlTemplate>통해 컨트롤의 모양을 사용자 지정할 수 있습니다.

- 컨트롤이 다른 테마를 지원하게 하려고 합니다.

### <a name="deriving-from-frameworkelement"></a>FrameworkElement에서 파생

에서 <xref:System.Windows.Controls.UserControl> 파생 되거나 <xref:System.Windows.Controls.Control> 기존 요소 작성에 의존 하는 컨트롤입니다. 대부분의 시나리오에서는에서 <xref:System.Windows.FrameworkElement> 상속 되는 모든 개체가에 있을 <xref:System.Windows.Controls.ControlTemplate>수 있으므로이는 적합 한 솔루션입니다. 그러나 컨트롤의 모양이 단순한 요소 컴퍼지션 이상의 기능을 필요로 하는 경우가 있습니다. 이러한 시나리오에서는에 <xref:System.Windows.FrameworkElement> 구성 요소를 기반으로 하는 것이 적합 합니다.

빌드 <xref:System.Windows.FrameworkElement>기반 구성 요소에는 직접 렌더링과 사용자 지정 요소 컴퍼지션 이라는 두 가지 표준 방법이 있습니다. 직접 렌더링은의 <xref:System.Windows.UIElement.OnRender%2A> <xref:System.Windows.FrameworkElement> 메서드를 재정의 하 고 <xref:System.Windows.Media.DrawingContext> 구성 요소 시각적 개체를 명시적으로 정의 하는 작업을 제공 합니다. 이는 및 <xref:System.Windows.Controls.Image> <xref:System.Windows.Controls.Border>에서 사용 되는 방법입니다. 사용자 지정 요소 컴퍼지션에는 형식의 <xref:System.Windows.Media.Visual> 개체를 사용 하 여 구성 요소의 모양을 구성 하는 작업이 포함 됩니다. 예제는 [DrawingVisual 개체 사용](../graphics-multimedia/using-drawingvisual-objects.md)을 참조하세요. <xref:System.Windows.Controls.Primitives.Track>는 사용자 지정 요소 컴퍼지션을 사용 하 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 는의 컨트롤 예제입니다. 직접 렌더링과 사용자 지정 요소 컴퍼지션을 같은 컨트롤에서 혼합하여 사용할 수도 있습니다.

#### <a name="benefits-of-deriving-from-frameworkelement"></a>FrameworkElement에서 파생하는 이점

다음 중 하나가 <xref:System.Windows.FrameworkElement> 적용 되는 경우에서 파생 하는 것이 좋습니다.

- 단순한 요소 컴퍼지션에서 제공하는 기능 이상으로 컨트롤의 모양을 정확하게 제어하려고 합니다.

- 자체 렌더링 논리를 정의하여 컨트롤의 모양을 정의하려고 합니다.

- <xref:System.Windows.Controls.UserControl> 및<xref:System.Windows.Controls.Control>를 사용 하는 것 보다 novel 방법으로 기존 요소를 구성 하려고 합니다.

<a name="control_authoring_basics"></a>

## <a name="control-authoring-basics"></a>컨트롤 제작 기본 사항

앞에서 설명한 것처럼 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 가장 강력한 기능 중 하나는 컨트롤의 기본 속성 설정 이상으로 모양 및 동작을 변경하면서 사용자 지정 컨트롤을 만들지 않아도 되는 것입니다. 스타일 지정, 데이터 바인딩 및 트리거 기능은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 속성 시스템 및 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이벤트 시스템에 의해 가능합니다. 다음 섹션에서는 사용자 지정 컨트롤을 만드는 데 사용하는 모델에 관계없이 따라야 하는 몇 가지 방법을 설명합니다. 이에 따라 사용자 지정 컨트롤의 사용자는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에 포함된 컨트롤의 경우처럼 이러한 기능을 사용할 수 있습니다.

### <a name="use-dependency-properties"></a>종속성 속성 사용

속성이 종속성 속성인 경우 다음을 수행할 수 있습니다.

- 스타일에서 속성을 설정합니다.

- 속성을 데이터 소스에 바인딩합니다.

- 속성의 값으로 동적 리소스를 사용합니다.

- 속성에 애니메이션 효과를 줍니다.

컨트롤의 속성이 이 기능을 지원하도록 하려면 종속성 속성으로 구현해야 합니다. 다음 예제에서는 다음을 수행하여 `Value`라는 종속성 속성을 정의합니다.

- 라는 <xref:System.Windows.DependencyProperty> 식별자를`ValueProperty`필드로정의합니다 .`readonly` `public` `static`

- 을 호출 <xref:System.Windows.DependencyProperty.Register%2A?displayProperty=nameWithType>하 여 속성 시스템에 속성 이름을 등록 하 고 다음을 지정 합니다.

  - 속성의 이름입니다.

  - 속성의 형식입니다.

  - 속성을 소유하는 형식입니다.

  - 속성의 메타데이터입니다. 메타 데이터에는 속성의 기본값인 <xref:System.Windows.CoerceValueCallback> 및가 <xref:System.Windows.PropertyChangedCallback>포함 됩니다.

- 속성의 `Value` `get` 및 접근자를구현하여종속성속성을등록하는데사용되는것과동일한이름인라는CLR래퍼속성을정의합니다.`set` 및 `get` <xref:System.Windows.DependencyObject.GetValue%2A> <xref:System.Windows.DependencyObject.SetValue%2A> 접근자 는각각및를호출합니다.`set` 클라이언트와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 가 접근자를 무시 하 고를 <xref:System.Windows.DependencyObject.SetValue%2A> 직접 호출할 <xref:System.Windows.DependencyObject.GetValue%2A> 수 있으므로 종속성 속성의 접근자에 추가 논리를 포함 하지 않는 것이 좋습니다. 예를 들어 속성이 데이터 소스에 바인딩되면 해당 속성의 `set` 접근자가 호출되지 않습니다.  Get 및 set 접근자에 추가 논리를 추가 하는 대신 <xref:System.Windows.ValidateValueCallback>, <xref:System.Windows.CoerceValueCallback>및 <xref:System.Windows.PropertyChangedCallback> 대리자를 사용 하 여에 응답 하거나 값이 변경 될 때 값을 확인 합니다.  이 콜백에 대한 자세한 내용은 [종속성 속성 콜백 및 유효성 검사](../advanced/dependency-property-callbacks-and-validation.md)를 참조하세요.

- <xref:System.Windows.CoerceValueCallback> 명명`CoerceValue`된에 대 한 메서드를 정의 합니다. `CoerceValue`는 `Value`가 `MinValue`보다 크거나 같고 `MaxValue`보다 작거나 같도록 합니다.

- <xref:System.Windows.PropertyChangedCallback> 라는`OnValueChanged`에 대 한 메서드를 정의 합니다. `OnValueChanged`개체를 <xref:System.Windows.RoutedPropertyChangedEventArgs%601> 만들고 `ValueChanged` 라우트된 이벤트를 발생 시 키도 록 준비 합니다. 라우트된 이벤트는 다음 섹션에서 설명합니다.

[!code-csharp[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#dependencyproperty)]
[!code-vb[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#dependencyproperty)]

자세한 내용은 [사용자 지정 종속성 속성](../advanced/custom-dependency-properties.md)을 참조하세요.

### <a name="use-routed-events"></a>라우트된 이벤트 사용

종속성 속성이 추가 기능을 사용 하 여 CLR 속성의 개념을 확장 하는 것 처럼 라우트된 이벤트는 표준 CLR 이벤트의 개념을 확장 합니다. 라우트된 이벤트는 다음 동작을 지원하기 때문에 새로운 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤을 만들 때 이벤트를 라우트된 이벤트로 구현하는 것도 좋습니다.

- 이벤트는 여러 컨트롤의 부모에서 처리될 수 ​​있습니다. 이벤트가 버블링 이벤트인 경우 요소 트리의 단일 부모가 이벤트를 구독할 수 있습니다. 그런 다음 애플리케이션 작성자는 하나의 처리기를 사용하여 여러 컨트롤의 이벤트에 응답할 수 있습니다. 예를 들어 컨트롤이에 포함 <xref:System.Windows.Controls.ListBox> <xref:System.Windows.DataTemplate>되어 있기 때문에에 있는 각 항목의 일부인 경우 응용 프로그램 개발자는에서 <xref:System.Windows.Controls.ListBox>컨트롤의 이벤트에 대 한 이벤트 처리기를 정의할 수 있습니다. 이벤트가 컨트롤 중 하나에서 발생할 때마다 이벤트 처리기가 호출됩니다.

- 라우트된 이벤트는에서 <xref:System.Windows.EventSetter>사용할 수 있으며,이를 통해 응용 프로그램 개발자는 스타일 내에서 이벤트 처리기를 지정할 수 있습니다.

- 라우트된 이벤트는에서 <xref:System.Windows.EventTrigger>사용할 수 있습니다 .이는를 사용 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]하 여 속성에 애니메이션 효과를 주는 데 유용 합니다. 자세한 내용은 [애니메이션 개요](../graphics-multimedia/animation-overview.md)를 참조하세요.

다음 예제는 다음을 수행하여 라우트된 이벤트를 정의합니다.

- 라는 <xref:System.Windows.RoutedEvent> 식별자를`ValueChangedEvent`필드로정의합니다 .`readonly` `public` `static`

- 메서드를 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A?displayProperty=nameWithType> 호출 하 여 라우트된 이벤트를 등록 합니다. 이 예에서는를 호출할 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A>때 다음 정보를 지정 합니다.

  - 이벤트의 이름은 `ValueChanged`입니다.

  - 라우팅 전략 <xref:System.Windows.RoutingStrategy.Bubble>은 원본 (이벤트를 발생 시키는 개체)에 대 한 이벤트 처리기가 먼저 호출 된 다음, 소스의 부모 요소에 대 한 이벤트 처리기가 가장 가까운 이벤트 처리기부터 시작 하 여 연속적으로 호출 되는 것을 의미 합니다. 부모 요소입니다.

  - 이벤트 처리기의 형식은 <xref:System.Windows.RoutedPropertyChangedEventHandler%601> <xref:System.Decimal> 형식으로 생성 된입니다.

  - 이벤트의 소유 형식은 `NumericUpDown`입니다.

- `ValueChanged`라는 공용 이벤트를 선언하고 이벤트 접근자 선언을 포함합니다. 이 예제에서는 <xref:System.Windows.UIElement.AddHandler%2A> <xref:System.Windows.UIElement.RemoveHandler%2A> `remove` `add` 이벤트[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 서비스를 사용 하기 위해 접근자 선언 및 접근자 선언에서를 호출 합니다.

- `ValueChanged` 이벤트를 발생시키는 `OnValueChanged`라는 보호된 가상 메서드를 만듭니다.

[!code-csharp[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#routedevent)]
[!code-vb[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#routedevent)]

자세한 내용은 [라우트된 이벤트 개요](../advanced/routed-events-overview.md) 및 [사용자 지정 라우트된 이벤트 만들기](../advanced/how-to-create-a-custom-routed-event.md)를 참조하세요.

### <a name="use-binding"></a>바인딩 사용

해당 논리에서 컨트롤의 UI를 분리하려면 데이터 바인딩 사용을 고려합니다. 이는를 <xref:System.Windows.Controls.ControlTemplate>사용 하 여 컨트롤의 모양을 정의 하는 경우에 특히 중요 합니다. 데이터 바인딩을 사용하면 코드에서 UI의 특정 부분을 참조하지 않아도 될 수 있습니다. <xref:System.Windows.Controls.ControlTemplate> 코드에서 <xref:System.Windows.Controls.ControlTemplate> 및 <xref:System.Windows.Controls.ControlTemplate>에 있는 요소를 참조 하는 경우 참조 된 요소를 새에 포함 해야 하기 때문에에 있는 요소를 참조 하지 않는 것이 좋습니다. <xref:System.Windows.Controls.ControlTemplate>

다음 예제에서는 <xref:System.Windows.Controls.TextBlock> `NumericUpDown` 컨트롤의을 업데이트 하 고 이름을 할당 하 고 코드에서 이름을 기준으로 텍스트 상자를 참조 합니다.

[!code-xaml[UserControlNumericUpDownSimple#UIRefMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml#uirefmarkup)]

[!code-csharp[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml.cs#uirefcode)]
[!code-vb[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDownSimple/VisualBasic/NumericUpDown.xaml.vb#uirefcode)]

다음 예제에서는 바인딩을 사용하여 동일한 작업을 수행합니다.

[!code-xaml[UserControlNumericUpDown#Binding](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml#binding)]

데이터 바인딩에 대한 자세한 내용은 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조하세요.

### <a name="design-for-designers"></a>디자이너를 위한 디자인

[!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]에서 사용자 지정 WPF 컨트롤에 대한 지원을 받으려면(예:속성 창에서 속성 편집) 다음 지침을 따릅니다.  용 개발에 대 한 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]자세한 내용은 [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)을 참조 하세요.

#### <a name="dependency-properties"></a>종속성 속성

앞의 "종속성 속성 `get` 사용 `set` "에서 설명한 대로 CLR 및 접근자를 구현 해야 합니다. 디자이너는 래퍼를 사용하여 종속성 속성의 존재를 감지할 수 있지만 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 컨트롤의 클라이언트와 마찬가지로 속성을 가져오거나 설정할 때 접근자를 호출할 필요가 없습니다.

#### <a name="attached-properties"></a>연결된 속성

다음 지침을 사용하여 사용자 지정 컨트롤에서 연결된 속성을 구현해야 합니다.

- 메서드를 `public` `static` `readonly` <xref:System.Windows.DependencyProperty> 사용 하 여 만든 형식PropertyName`Property`의가있습니다. <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 에 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 전달 되는 속성 이름은 *PropertyName*과 일치 해야 합니다.

- `Set`*PropertyName* 및 `Get`*PropertyName*이라는 `public` `static` CLR 메서드 쌍을 구현합니다. 두 메서드는에서 <xref:System.Windows.DependencyProperty> 파생 된 클래스를 첫 번째 인수로 수락 해야 합니다. `Set`*PropertyName* 메서드는 그 형식이 속성의 등록된 데이터 형식과 일치하는 인수도 수락합니다. `Get`*PropertyName* 메서드는 동일한 형식의 값을 반환해야 합니다. `Set`*PropertyName* 메서드가 누락된 경우 속성이 읽기 전용으로 표시됩니다.

- `Set`*Propertyname* 및 `Get` *propertyname* 은 각각 대상 종속성 개체 <xref:System.Windows.DependencyObject.GetValue%2A> 의 <xref:System.Windows.DependencyObject.SetValue%2A> 및 메서드로 직접 라우팅합니다. 디자이너는 메서드 래퍼를 통해 호출하거나 대상 종속성 개체를 직접 호출하여 연결된 속성에 액세스할 수 있습니다.

연결된 속성에 대한 자세한 내용은 [연결된 속성 개요](../advanced/attached-properties-overview.md)를 참조하세요.

### <a name="define-and-use-shared-resources"></a>공유 리소스 정의 및 사용

애플리케이션과 동일한 어셈블리에 컨트롤을 포함하거나 여러 애플리케이션에서 사용할 수 있는 별도의 어셈블리에 컨트롤을 패키지화할 수 있습니다. 대부분, 이 항목에서 설명하는 정보는 사용하는 메서드에 관계없이 적용됩니다.  그러나 주목할 만한 차이점이 하나 있습니다.  애플리케이션과 동일한 어셈블리에 컨트롤을 배치하면 App.xaml 파일에 전역 리소스를 자유롭게 추가할 수 있습니다. 그러나 컨트롤만 <xref:System.Windows.Application> 포함 하는 어셈블리에는 연결 된 개체가 없으므로 app.xaml 파일을 사용할 수 없습니다.

애플리케이션이 리소스를 찾을 때 다음 순서로 세 가지 수준을 조사합니다.

1. 요소 수준

   시스템이 리소스를 참조하는 요소로 시작한 다음 루트 요소에 도달할 때까지 논리 부모 등의 리소스를 검색합니다.

2. 애플리케이션 수준

   개체에서 정의 되 <xref:System.Windows.Application> 는 리소스입니다.

3. 테마 수준

   테마 수준 사전은 Themes라는 하위 폴더에 저장됩니다.  Themes 폴더의 파일은 테마에 해당합니다.  예를 들어 Aero.NormalColor.xaml, Luna.NormalColor.xaml, Royale.NormalColor.xaml 등이 있을 수 있습니다.  generic.xaml이라는 파일이 있을 수도 있습니다.  시스템이 테마 수준에서 리소스를 찾으면 먼저 테마별 파일에서 찾은 다음 generic.xaml에서 찾습니다.

컨트롤이 애플리케이션과 별도의 어셈블리에 있을 때는 전역 리소스를 요소 수준이나 테마 수준에 배치해야 합니다. 두 가지 방법 모두 장점이 있습니다.

#### <a name="defining-resources-at-the-element-level"></a>요소 수준에서 리소스 정의

사용자 지정 리소스 사전을 만들어 컨트롤 리소스 사전과 병합하면 요소 수준에서 공유 리소스를 정의할 수 있습니다.  이 메서드를 사용하면 리소스 파일의 이름을 원하는 대로 지정할 수 있으며 컨트롤과 동일한 폴더에 배치할 수 있습니다. 요소 수준의 리소스는 간단한 문자열을 키로 사용할 수도 있습니다. 다음 예제에서는 Dictionary1 라는 <xref:System.Windows.Media.LinearGradientBrush> 리소스 파일을 만듭니다.

[!code-xaml[SharedResources#1](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/Dictionary1.xaml#1)]

사전을 정의한 후에는 컨트롤의 리소스 사전과 병합해야 합니다.  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 또는 코드를 사용하여 이 작업을 수행할 수 있습니다.

다음 예제는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 사용하여 리소스 사전을 병합합니다.

[!code-xaml[SharedResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml#2)]

이 방법의 단점은 참조할 때마다 <xref:System.Windows.ResourceDictionary> 개체가 만들어지기 때문입니다.  예를 들어 라이브러리에 10 개의 사용자 지정 컨트롤이 있고 XAML을 사용 하 여 각 컨트롤에 대 한 공유 리소스 사전을 병합 하는 경우 10 <xref:System.Windows.ResourceDictionary> 개의 동일한 개체를 만듭니다.  코드의 리소스를 병합 하 고 결과 <xref:System.Windows.ResourceDictionary>를 반환 하는 정적 클래스를 만들어이를 방지할 수 있습니다.

다음 예제에서는 공유 <xref:System.Windows.ResourceDictionary>를 반환 하는 클래스를 만듭니다.

[!code-csharp[SharedResources#3](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/SharedDictionaryManager.cs#3)]

다음 예제에서는 공유 리소스를 `InitializeComponent`를 호출하기 전에 컨트롤의 생성자에 있는 사용자 지정 컨트롤의 리소스와 병합합니다.  는 `SharedDictionaryManager.SharedDictionary` 정적 속성 <xref:System.Windows.ResourceDictionary> 이므로은 한 번만 만들어집니다. `InitializeComponent`가 호출되기 전에 리소스 사전이 병합되었기 때문에 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일의 컨트롤에서 리소스를 사용할 수 있습니다.

[!code-csharp[SharedResources#4](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml.cs#4)]

#### <a name="defining-resources-at-the-theme-level"></a>테마 수준에서 리소스 정의

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용하면 다양한 Windows 테마를 위한 리소스를 만들 수 있습니다.  컨트롤 작성자는 특정 테마의 리소스를 정의하여 사용 중인 테마에 따라 컨트롤의 모양을 변경할 수 있습니다. 예를 들어 windows <xref:System.Windows.Controls.Button> 클래식 테마에 있는의 모양 (windows 2000의 기본 테마)은에서 다른 <xref:System.Windows.Controls.ControlTemplate> 를 <xref:System.Windows.Controls.Button> 사용 하기 <xref:System.Windows.Controls.Button> 때문에 windows Luna 테마 (windows XP의 기본 테마)의와 다릅니다. 각 테마에 대해

테마와 관련된 리소스는 특정 파일 이름의 리소스 사전에 보관됩니다. 이러한 파일은 컨트롤이 포함된 폴더의 하위 폴더인 `Themes`라는 폴더에 있어야 합니다. 다음 표에는 각 파일과 관련된 리소스 사전 파일과 테마가 나와 있습니다.

|리소스 사전 파일 이름|Windows 테마|
|-----------------------------------|-------------------|
|`Classic.xaml`|Windows XP의 고전 Windows 9x/2000 모양|
|`Luna.NormalColor.xaml`|Windows XP의 기본 파란색 테마|
|`Luna.Homestead.xaml`|Windows XP의 올리브색 테마|
|`Luna.Metallic.xaml`|Windows XP의 은색 테마|
|`Royale.NormalColor.xaml`|Windows XP Media Center Edition의 기본 테마|
|`Aero.NormalColor.xaml`|Windows Vista의 기본 테마|

모든 테마에 대해 리소스를 정의할 필요는 없습니다. 특정 테마에 대해 리소스가 정의되지 않은 경우 컨트롤이 리소스에 대해 `Classic.xaml`을 확인합니다. 현재 테마에 해당하는 파일 또는 `Classic.xaml`에 리소스가 정의되지 않은 경우 컨트롤이 `generic.xaml`이라는 리소스 사전 파일에 있는 제네릭 리소스를 사용합니다.  `generic.xaml` 파일은 테마별 리소스 사전 파일과 같은 폴더에 있습니다. `generic.xaml`은 특정 Windows 테마에 해당하지 않지만 여전히 테마 수준의 사전입니다.

테마 [C#](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp) 및 UI 자동화 지원 샘플을 포함 하는 또는 [Visual Basic](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic) NumericUpDown 사용자 지정 컨트롤에는 `NumericUpDown` 컨트롤에 대 한 두 개의 리소스 사전이 포함 되어 있습니다. 하나는 Luna입니다. 

을 <xref:System.Windows.Controls.ControlTemplate> 테마별 리소스 사전 파일에 배치 하는 경우 컨트롤에 대 한 정적 생성자를 만들고 다음 예제와 같이에서 메서드 <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A>를 <xref:System.Windows.DependencyProperty.OverrideMetadata%28System.Type%2CSystem.Windows.PropertyMetadata%29> 호출 해야 합니다.

[!code-csharp[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/CSharp/NumericUpDown.cs#staticconstructor)]
[!code-vb[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/visualbasic/numericupdown.vb#staticconstructor)]

##### <a name="defining-and-referencing-keys-for-theme-resources"></a>테마 리소스에 대한 키 정의 및 참조

요소 레벨에서 리소스를 정의할 때 문자열을 키로 지정하고 문자열을 통해 리소스에 액세스할 수 있습니다. 테마 수준에서 리소스를 정의 하는 경우를 <xref:System.Windows.ComponentResourceKey> 키로 사용 해야 합니다.  다음 예제에서는 generic.xaml에서 리소스를 정의합니다.

[!code-xaml[ThemeResourcesControlLibrary#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/Themes/generic.xaml#5)]

다음 예제에서는를 <xref:System.Windows.ComponentResourceKey> 키로 지정 하 여 리소스를 참조 합니다.

[!code-xaml[ThemeResourcesControlLibrary#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/NumericUpDown.xaml#6)]

##### <a name="specifying-the-location-of-theme-resources"></a>테마 리소스의 위치 지정

컨트롤에 대한 리소스를 찾으려면 호스팅 애플리케이션이 어셈블리에 컨트롤 관련 리소스가 있는지 알아야 합니다. 컨트롤을 포함 하는 어셈블리 <xref:System.Windows.ThemeInfoAttribute> 에를 추가 하 여이를 수행할 수 있습니다. 에 <xref:System.Windows.ThemeInfoAttribute> <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> 는<xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> 제네릭 리소스의 위치를 지정 하는 속성과 테마별 리소스의 위치를 지정 하는 속성이 있습니다.

다음 예제에서는 <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> 및 <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> 속성을로 <xref:System.Windows.ResourceDictionaryLocation.SourceAssembly>설정 하 여 제네릭 및 테마별 리소스가 컨트롤과 동일한 어셈블리에 있도록 지정 합니다.

[!code-csharp[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/Properties/AssemblyInfo.cs#themessection)]
[!code-vb[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/my project/assemblyinfo.vb#themessection)]

## <a name="see-also"></a>참고자료

- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
- [WPF의 Pack URI](../app-development/pack-uris-in-wpf.md)
- [컨트롤 사용자 지정](control-customization.md)
