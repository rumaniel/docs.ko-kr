---
title: 스타일을 지정할 수 있는 컨트롤을 디자인하기 위한 지침
ms.date: 03/30/2017
helpviewer_keywords:
- style design for controls [WPF]
- controls [WPF], style design
ms.assetid: c52dde45-a311-4531-af4c-853371c4d5f4
ms.openlocfilehash: a5a91d6a1f046b31ff26e769e9fcc1c7516904c8
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67662596"
---
# <a name="guidelines-for-designing-stylable-controls"></a>스타일을 지정할 수 있는 컨트롤을 디자인하기 위한 지침

이 문서에서는 쉽게 스타일을 지정하고 템플릿을 지정할 수 있는 컨트롤을 디자인할 때 고려해야 하는 모범 사례 집합을 요약합니다. 기본 제공 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 집합의 테마 컨트롤 스타일에 대해 작업하는 동안 많은 시행착오를 거쳐 이 모범 사례 집합을 얻게 되었습니다. 성공적으로 스타일을 지정하려면 스타일 자체만큼이나 잘 설계된 개체 모델이 필요함을 알게 되었습니다. 이 문서의 독자는 스타일 작성자가 아니라 컨트롤 작성자입니다.

<a name="Terminology"></a>

## <a name="terminology"></a>용어

“스타일 지정 및 템플릿 지정”은 컨트롤 작성자가 컨트롤의 시각적 요소를 컨트롤의 스타일과 템플릿에 의존할 수 있는 기술 집합체를 나타냅니다. 이 기술 집합체에는 다음이 포함됩니다.

- 스타일(속성 setter, 트리거 및 스토리보드 포함).

- 리소스.

- 컨트롤 템플릿.

- 데이터 템플릿.

스타일 지정과 템플릿 지정에 대한 소개는 [스타일 지정 및 템플릿 지정](styling-and-templating.md)을 참조하세요.

<a name="Before_You_Start__Understanding_Your_Control"></a>

## <a name="before-you-start-understanding-your-control"></a>시작 하기 전에: 컨트롤 이해

이 지침으로 이동하기 전에 컨트롤의 일반 용도를 이해하고 정의하는 것이 중요합니다. 스타일 지정에서는 다루기 힘든 상황이 많이 발생합니다. 여러 애플리케이션에서 많은 개발자가 광범위하게 사용하도록 작성된 컨트롤에서는 스타일 지정을 통해 컨트롤의 시각적 모양을 광범위하게 변경할 수 있다는 문제가 발생합니다. 스타일 지정된 컨트롤이 실제로는 작성자가 의도한 컨트롤과 전혀 비슷하지 않을 수 있습니다. 기본적으로 스타일 지정에서 제공하는 유연성은 무한하므로 일반적인 용도라는 개념을 사용하여 한정된 범위에서 결정을 내릴 수 있습니다.

컨트롤의 일반 용도를 이해하려면 컨트롤의 가치 제안에 대해 생각해 보는 것이 좋습니다. 테이블에 사용자의 컨트롤은 제공할 수 있지만, 다른 컨트롤에서는 제공할 수 없는 기능은 무엇인가요? 일반적인 용도란 시각적인 특정 모양을 의미하는 것이 아니라 용도와 관련된 합리적인 기대치 집합과 컨트롤의 원리를 의미합니다. 이 의미를 파악하면 일반적인 용도에서 스타일 정의된 컨트롤 동작과 컴퍼지션 모델을 가정할 수 있습니다. 경우 <xref:System.Windows.Controls.ComboBox>, 예를 들어, 일반 용도 이해을 제공 하지 않습니다 모든 정보에 대 한 특정 여부를 <xref:System.Windows.Controls.ComboBox> 둥근된 모서리 되었지만 팩트에 대 한 정보 제공 하는 <xref:System.Windows.Controls.ComboBox> 필요할 팝업 창 및 가 열려 있는지 여부를 설정/해제의 몇 가지 방법입니다.

<a name="General_Guidelines"></a>

## <a name="general-guidelines"></a>일반 지침

- **템플릿 계약을 엄격하게 적용하지 마세요.** 컨트롤의 템플릿 계약은 컨트롤이 제대로 작동하는 데 필요한 요소, 명령, 바인딩, 트리거 또는 속성 설정으로 구성될 수 있습니다.

  - 계약을 가능한 최소화합니다.

  - 디자인 시(즉, 디자인 도구를 사용할 때) 일반적으로 컨트롤 템플릿이 미완성 상태에 있도록 기대치를 디자인합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 “작성” 상태 인프라를 제공하지 않으므로, 해당 상태가 올바른 것으로 기대치를 설정하여 컨트롤을 빌드해야 합니다.

  - 템플릿 계약의 요소를 이행하지 않을 때 예외 처리하지 않습니다. 이러한 선을 따라 하위가 너무 많거나 너무 적을 경우 패널에서 예외 처리하지 않아야 합니다.

- **주변 기능을 템플릿 도우미 요소로 포함시킵니다.** 각 컨트롤은 핵심 기능과 참 값 제안에 집중해야 하며 컨트롤의 일반적 사용으로 정의해야 합니다. 이를 위해 템플릿 내의 컴퍼지션 및 도우미 요소를 사용하여 주변 동작과 시각화(즉, 컨트롤의 핵심 기능에 기여하지 않는 동작 및 시각화)를 사용으로 설정합니다. 도우미 요소는 다음 세 가지 범주로 구분됩니다.

  - **독립 실행형** 도움말 형식은 공용이며, 템플릿에서 “무명”으로 사용되는 재사용 가능 컨트롤 또는 기본 유형입니다. 즉, 도움말 요소와 스타일 지정된 컨트롤에서 서로를 인식하지 못합니다. 기술적으로 요소는 무명 형식일 수 있지만, 이 컨텍스트에서 이 용어는 대상 지정된 시나리오를 사용하도록 특수화된 기능을 캡슐화하는 형식을 설명합니다.

  - **형식 기반** 도우미 요소는 특수화된 기능을 캡슐화하는 새 형식입니다. 일반적으로 이러한 요소는 공용 컨트롤 또는 기본 요소보다 범위를 한정하여 설계합니다. 독립 실행형 도우미 요소와 달리, 형식 기반 도우미 요소는 자신이 사용되는 컨텍스트를 인식하며 일반적으로 속해 있는 템플릿의 컨트롤과 데이터를 공유해야 합니다.

  - **명명됨** 도우미 요소는 컨트롤이 템플릿에서 이름으로 찾을 수 있어야 하는 공용 컨트롤 또는 기본 요소입니다. 이러한 요소에는 템플릿에서 잘 알려진 이름이 제공되므로, 컨트롤에서 요소를 찾아 프로그래밍 방식으로 상호 작용할 수 있습니다. 모든 템플릿에서 지정된 이름의 요소는 하나뿐이어야 합니다.

  다음 테이블에서는 오늘 컨트롤 스타일별로 사용된 도우미 요소를 보여줍니다(이 목록은 전체 목록이 아님).

  |요소|형식|사용 주체|
  |-------------|----------|-------------|
  |<xref:System.Windows.Controls.ContentPresenter>|형식 기반|<xref:System.Windows.Controls.Button>를 <xref:System.Windows.Controls.CheckBox>, <xref:System.Windows.Controls.RadioButton>를 <xref:System.Windows.Controls.Frame>등 (모든 <xref:System.Windows.Controls.ContentControl> 형식)|
  |<xref:System.Windows.Controls.ItemsPresenter>|형식 기반|<xref:System.Windows.Controls.ListBox>를 <xref:System.Windows.Controls.ComboBox>하십시오 <xref:System.Windows.Controls.Menu>등 (모든 <xref:System.Windows.Controls.ItemsControl> 형식)|
  |<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|명명됨|<xref:System.Windows.Controls.ToolBar>|
  |<xref:System.Windows.Controls.Primitives.Popup>|독립 실행형|<xref:System.Windows.Controls.ComboBox>를 <xref:System.Windows.Controls.ToolBar>하십시오 <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.ToolTip>등|
  |<xref:System.Windows.Controls.Primitives.RepeatButton>|명명됨|<xref:System.Windows.Controls.Slider>를 <xref:System.Windows.Controls.Primitives.ScrollBar>등|
  |<xref:System.Windows.Controls.Primitives.ScrollBar>|명명됨|<xref:System.Windows.Controls.ScrollViewer>|
  |<xref:System.Windows.Controls.ScrollViewer>|독립 실행형|<xref:System.Windows.Controls.ListBox>를 <xref:System.Windows.Controls.ComboBox>하십시오 <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.Frame>등|
  |<xref:System.Windows.Controls.Primitives.TabPanel>|독립 실행형|<xref:System.Windows.Controls.TabControl>|
  |<xref:System.Windows.Controls.TextBox>|명명됨|<xref:System.Windows.Controls.ComboBox>|
  |<xref:System.Windows.Controls.Primitives.TickBar>|형식 기반|<xref:System.Windows.Controls.Slider>|

- **도우미 요소에서 필수 사용자 지정 바인딩 또는 속성 설정을 최소화**. 일반적으로 도우미 요소가 컨트롤 템플릿에서 적절하게 작동하려면 특정 바인딩 또는 속성 설정이 필요합니다. 도우미 요소와 템플릿 지정된 컨트롤은 최대한 이러한 설정을 지정해야 합니다. 속성을 설정하거나 바인딩을 설정할 때 사용자가 설정한 값을 재정의하지 않도록 주의해야 합니다. 구체적인 모범 사례는 다음과 같습니다.

  - 명명된 도우미 요소는 부모가 식별해야 하며, 부모가 도우미 요소에서 필요한 설정을 지정해야 합니다.

  - 형식 기반 도우미 요소는 모든 필수 설정을 직접 설정해야 합니다. 이 작업을 수행하려면 도우미 요소가 `TemplatedParent`(현재 자신이 사용되고 있는 템플릿의 컨트롤 형식)를 포함하여 현재 사용되고 있는 정보 컨텍스트를 쿼리해야 할 수도 있습니다. 예를 들어 <xref:System.Windows.Controls.ContentPresenter> 자동으로 바인딩합니다를 `Content` 속성을 해당 `TemplatedParent` 에 해당 <xref:System.Windows.Controls.ContentPresenter.Content%2A> 속성에 사용 되는 경우를 <xref:System.Windows.Controls.ContentControl> 파생 형식.

  - 도우미 요소와 상위가 서로를 알지 못하도록 정의되어 있으므로 독립 실행형 도우미 요소는 이 방식으로 최적화할 수 없습니다.

- **이름 속성을 사용하여 템플릿에서 요소에 플래그 지정**. 프로그래밍 방식으로 액세스하기 위해 스타일에서 요소를 찾아야 하는 컨트롤은 `Name` 속성과 `FindName` 패러다임을 사용하여 수행해야 합니다. 요소를 찾지 못해도 컨트롤에서 예외 처리를 하지 않아야 하며, 해당 요소가 필요한 기능을 자동으로 적절하게 사용 안 함으로 설정해야 합니다.

- **스타일에서 컨트롤 상태와 동작을 표시하기 위한 모범 사례 사용.** 다음은 스타일에서 컨트롤 상태 변경과 동작을 표시하기 위한 모범 사례가 순서대로 정렬된 목록입니다. 시나리오를 사용하게 설정하는 목록의 첫 번째 항목을 사용해야 합니다.

  1. 속성 바인딩. 예: 바인딩 간의 <xref:System.Windows.Controls.ComboBox.IsDropDownOpen%2A?displayProperty=nameWithType> 고 <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A?displayProperty=nameWithType>입니다.

  2. 트리거된 속성 변경 또는 속성 애니메이션. 예:의 가리키기 상태를 <xref:System.Windows.Controls.Button>입니다.

  3. 명령. 예: <xref:System.Windows.Controls.Primitives.ScrollBar.LineUpCommand>  /  <xref:System.Windows.Controls.Primitives.ScrollBar.LineDownCommand> 에서 <xref:System.Windows.Controls.Primitives.ScrollBar>합니다.

  4. 독립 실행형 도우미 요소. 예: <xref:System.Windows.Controls.Primitives.TabPanel> 에서 <xref:System.Windows.Controls.TabControl>합니다.

  5. 형식 기반 도우미 형식. 예: <xref:System.Windows.Controls.ContentPresenter> 에 <xref:System.Windows.Controls.Button>를 <xref:System.Windows.Controls.Primitives.TickBar> 에서 <xref:System.Windows.Controls.Slider>합니다.

  6. 명명됨 도우미 요소. 예: <xref:System.Windows.Controls.TextBox> 에서 <xref:System.Windows.Controls.ComboBox>합니다.

  7. 명명됨 도우미 유형의 거품형 이벤트. 스타일 요소에서 거품형 이벤트를 수신 대기하려면 해당 이벤트를 생성하는 요소를 고유하게 식별할 수 있어야 합니다. 예: <xref:System.Windows.Controls.Primitives.Thumb> 에서 <xref:System.Windows.Controls.ToolBar>합니다.

  8. 사용자 지정 `OnRender` 동작. 예: <xref:Microsoft.Windows.Themes.ButtonChrome> 에서 <xref:System.Windows.Controls.Button>합니다.

- **드물게 스타일 트리거 사용(템플릿 트리거와 반대)** . 템플릿에서 요소의 속성에 영향을 미치는 트리거를 템플릿에 선언해야 합니다. 템플릿을 변경하면 트리거도 손상되는 경우가 아닌 경우 컨트롤의 속성에 영향을 미치는 트리거(`TargetName`이 없음)는 스타일에 선언할 수 있습니다.

- **기존 스타일링 패턴과 일치.** 문제를 해결하는 방법이 여러 가지인 경우가 많습니다. 기존 컨트롤 스타일 지정 패턴을 인식하고 가능한 경우 이 패턴과 일치시킵니다. 이 동일한 기본 형식에서 파생 되는 컨트롤에 대 한 특히 중요 (예를 들어 <xref:System.Windows.Controls.ContentControl>, <xref:System.Windows.Controls.ItemsControl>, <xref:System.Windows.Controls.Primitives.RangeBase>등).

- **다시 템플릿을 지정하지 않고 공용 사용자 지정 시나리오를 사용하도록 속성 노출**. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 플러그형/사용자 지정 가능 파트를 지원하지 않으므로, 컨트롤 사용자는 속성을 직접 설정하거나 스타일을 사용하여 속성을 설정하는 식의 두 가지 방법으로만 사용자 지정할 수 있습니다. 이 점을 염두에 두고 매우 일반적이며 우선 순위가 높은 사용자 지정 시나리오에서 대상으로 지정된 제한된 수의 속성을 공개하는 것이 적절합니다. 그렇지 않으면 다시 템플릿을 지정해야 합니다. 다음은 사용자 지정 시나리오를 사용하도록 설정하는 시기와 방법에 관한 모범 사례입니다.

  - 매우 일반적인 사용자 지정을 컨트롤의 속성으로 노출하여 템플릿에서 사용해야 합니다.

  - 덜 일반적인(드물지는 않음) 사용자 지정은 연결된 속성으로 노출하여 템플릿에서 사용해야 합니다.

  - 알려져 있지만 드문 사용자 지정은 다시 템플릿을 지정해야 합니다.

<a name="Theme_Considerations"></a>

## <a name="theme-considerations"></a>테마 고려 사항

- **테마 스타일은 모든 테마에서 일관된 속성 의미 체계를 유지하려고 시도하지만 보장되지는 않습니다**. 컨트롤에는 설명서의 일부로 컨트롤의 속성 의미 체계, 즉 컨트롤의 속성 “의미”를 설명하는 문서가 있어야 합니다. 예를 들어 합니다 <xref:System.Windows.Controls.ComboBox> 컨트롤의 의미를 정의 해야 합니다 <xref:System.Windows.Controls.Control.Background%2A> 내에서 속성 <xref:System.Windows.Controls.ComboBox>합니다. 컨트롤의 기본 스타일은 모든 테마에서 해당 문서에 정의된 의미 체계를 따라야 합니다. 한편 컨트롤 사용자는 해당 속성 의미 체계가 테마 간에 변경될 수 있음을 알아야 합니다. 경우에 따라 특정 테마에 필요한 시각적 제약 조건때문에 지정된 속성이 표시되지 못할 수 있습니다. (예를 들어, 클래식 테마에는 여러 컨트롤에 대해 `Thickness`를 적용할 수 있는 단일 테두리가 없습니다.)

- **모든 테마에서 테마 스타일의 트리거 의미 체계는 일관되지 않아도 됩니다**. 트리거 또는 애니메이션을 통해 컨트롤 스타일이 노출한 동작은 테마마다 달라질 수 있습니다. 컨트롤 사용자는 모든 테마에서 특정 동작을 수행하기 위해 컨트롤에서 동일한 메커니즘을 채택하지 않아도 된다는 점을 알아야 합니다. 예를 들어, 한 테마에서는 애니메이션을 사용하여 가리키기 동작을 표현하며, 다른 테마에서는 트리거를 사용합니다. 그러면 사용자 지정된 컨트롤에서 동작이 일관되지 않게 유지될 수 있습니다. (예를 들어, 트리거를 사용하여 해당 상태를 표현하는 경우 배경 속성을 변경해도 컨트롤의 가리키기 상태에 영향을 미치지 않습니다. 그러나 애니메이션을 사용하여 가리키기 상태를 구현하는 경우 배경을 중단하면 애니메이션이 복구할 수 없게 손상될 수 있으므로 상태가 전환됩니다.)

- **모든 테마에서 테마 스타일의 “레이아웃”의미 체계는 일관되지 않아도 됩니다**. 예를 들어, 기본 스타일에서는 모든 테마에서 컨트롤이 반드시 동일한 크기를 차지하거나 컨트롤이 모든 테마에서 반드시 동일한 콘텐츠 여백 / 안쪽 여백을 유지하지 않아도 됩니다.

## <a name="see-also"></a>참고자료

- [스타일 지정 및 템플릿](styling-and-templating.md)
- [컨트롤 제작 개요](control-authoring-overview.md)
