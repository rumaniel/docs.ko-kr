---
title: Calendar 스타일 및 템플릿
ms.date: 03/30/2017
helpviewer_keywords:
- styles [WPF], Calendar
- templates [WPF], Calendar
- states [WPF], Calendar
- parts [WPF], Calendar
- Calendar [WPF], styles and templates
- ControlTemplate [WPF], Calendar
ms.assetid: f4fcf046-7a8f-41b8-b5a8-534b64e0345c
ms.openlocfilehash: 18bef548b11f1a680c1361027b86f6952bedaad0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61912446"
---
# <a name="calendar-styles-and-templates"></a>Calendar 스타일 및 템플릿
이 항목에서는 스타일 및 템플릿에 대해 설명 합니다 <xref:System.Windows.Controls.Calendar> 제어 합니다. 기본값을 수정할 수 있습니다 <xref:System.Windows.Controls.ControlTemplate> 고유한 모양을 제어할 수 있습니다. 자세한 내용은 [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)을 참조하세요.  
  
## <a name="calendar-parts"></a>일정 부분  
 다음 표에서 대 한 명명된 된 파트를 <xref:System.Windows.Controls.Calendar> 제어 합니다.  
  
|파트|형식|설명|  
|-|-|-|  
|PART_CalendarItem|<xref:System.Windows.Controls.Primitives.CalendarItem>|현재 표시 된 달 또는 연도 <xref:System.Windows.Controls.Calendar>입니다.|  
|PART_Root|<xref:System.Windows.Controls.Panel>|포함 된 패널을 <xref:System.Windows.Controls.Primitives.CalendarItem>입니다.|  
  
## <a name="calendar-states"></a>일정 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.Calendar> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|----------------------|---------------------------|-----------------|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="calendaritem-parts"></a>CalendarItem 파트  
 다음 표에서 대 한 명명된 된 파트를 <xref:System.Windows.Controls.Primitives.CalendarItem> 제어 합니다.  
  
|파트|형식|설명|  
|-|-|-|  
|PART_Root|<xref:System.Windows.FrameworkElement>|루트 컨트롤입니다.|  
|PART_PreviousButton|<xref:System.Windows.Controls.Button>|클릭할 때 달력의 이전 페이지를 표시 하는 단추입니다.|  
|PART_NextButton|<xref:System.Windows.Controls.Button>|클릭할 때 달력의 다음 페이지를 표시 하는 단추입니다.|  
|PART_HeaderButton|<xref:System.Windows.Controls.Button>|월 모드, 연도 모드 및 10 년 모드를 전환할 수 있는 단추입니다.|  
|PART_MonthView|<xref:System.Windows.Controls.Grid>|월 모드에 있을 때 콘텐츠를 호스팅합니다.|  
|PART_YearView|<xref:System.Windows.Controls.Grid>|또는 10 년 모드에 있을 때 콘텐츠를 호스팅합니다.|  
|PART_DisabledVisual|<xref:System.Windows.FrameworkElement>|사용 안 함된 상태에 대 한 오버레이 합니다.|  
|DayTitleTemplate|<xref:System.Windows.DataTemplate>|<xref:System.Windows.DataTemplate> 시각적 구조를 설명 하는 합니다.|  
  
## <a name="calendaritem-states"></a>CalendarItem 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.Primitives.CalendarItem> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|정상 상태|CommonStates|기본 상태입니다.|  
|사용 안 함 상태|CommonStates|일정의 상태는 경우는 <xref:System.Windows.UIElement.IsEnabled%2A> 속성은 `false`합니다.|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="calendardaybutton-parts"></a>CalendarDayButton 파트  
 <xref:System.Windows.Controls.Primitives.CalendarDayButton> 컨트롤에 명명된 된 파트가 없습니다.  
  
## <a name="calendardaybutton-states"></a>CalendarDayButton 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.Primitives.CalendarDayButton> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|보통|CommonStates|기본 상태입니다.|  
|사용 안 함|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> 을 사용할 수 없습니다.|  
|MouseOver|CommonStates|마우스 포인터가 위에 <xref:System.Windows.Controls.Primitives.CalendarDayButton>합니다.|  
|누름|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> 눌러져 있습니다.|  
|선택함|SelectionStates|단추가 선택 됩니다.|  
|선택 취소|SelectionStates|단추를 선택 하지 않았습니다.|  
|CalendarButtonFocused|CalendarButtonFocusStates|단추에 포커스가 있습니다.|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|단추에 포커스가 없습니다.|  
|포커스 있음|FocusStates|단추에 포커스가 있습니다.|  
|포커스 없음|FocusStates|단추에 포커스가 없습니다.|  
|활성|ActiveStates|단추가 활성화 됩니다.|  
|비활성|ActiveStates|단추를 활성 상태가 아닙니다.|  
|RegularDay|DayStates|단추를 나타내지 않는 <xref:System.DateTime.Today%2A?displayProperty=nameWithType>합니다.|  
|오늘|DayStates|단추를 나타내는 <xref:System.DateTime.Today%2A?displayProperty=nameWithType>합니다.|  
|NormalDay|BlackoutDayStates|단추를 선택할 수 있는 일을 나타냅니다.|  
|BlackoutDay|BlackoutDayStates|단추를 선택할 수 없는 일을 나타냅니다.|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="calendarbutton-parts"></a>CalendarButton 파트  
 <xref:System.Windows.Controls.Primitives.CalendarButton> 컨트롤에 명명된 된 파트가 없습니다.  
  
## <a name="calendarbutton-states"></a>CalendarButton 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.Primitives.CalendarButton> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|보통|CommonStates|기본 상태입니다.|  
|사용 안 함|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> 을 사용할 수 없습니다.|  
|MouseOver|CommonStates|마우스 포인터가 위에 <xref:System.Windows.Controls.Primitives.CalendarButton>합니다.|  
|누름|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> 눌러져 있습니다.|  
|선택함|SelectionStates|단추가 선택 됩니다.|  
|선택 취소|SelectionStates|단추를 선택 하지 않았습니다.|  
|CalendarButtonFocused|CalendarButtonFocusStates|단추에 포커스가 있습니다.|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|단추에 포커스가 없습니다.|  
|포커스 있음|FocusStates|단추에 포커스가 있습니다.|  
|포커스 없음|FocusStates|단추에 포커스가 없습니다.|  
|활성|ActiveStates|단추가 활성화 됩니다.|  
|비활성|ActiveStates|단추를 활성 상태가 아닙니다.|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="calendar-controltemplate-example"></a>달력 ControlTemplate 예제  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.Calendar> 컨트롤과 연결 된 형식입니다.  
  
 [!code-xaml[ControlTemplateExamples#Calendar](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/calendar.xaml#calendar)]  
  
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
