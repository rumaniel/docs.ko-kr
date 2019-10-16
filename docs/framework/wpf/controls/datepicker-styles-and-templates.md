---
title: DatePicker 스타일 및 템플릿
ms.date: 03/30/2017
helpviewer_keywords:
- ControlTemplate [WPF], DatePicker
- DatePicker [WPF], styles and templates
- templates [WPF], DatePicker
- parts [WPF], DatePicker
- styles [WPF], DatePicker
- states [WPF], DatePicker
ms.assetid: c430a657-692f-44bd-a549-2341f92d6115
ms.openlocfilehash: 013076fdac8666b974fdf0ce9b09740197031c15
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170535"
---
# <a name="datepicker-styles-and-templates"></a>DatePicker 스타일 및 템플릿
이 항목에서는 스타일 및 템플릿에 대해 설명 합니다 <xref:System.Windows.Controls.DatePicker> 제어 합니다. 기본값을 수정할 수 있습니다 <xref:System.Windows.Controls.ControlTemplate> 고유한 모양을 제어할 수 있습니다. 자세한 내용은 [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)을 참조하세요.  
  
## <a name="datepicker-parts"></a>DatePicker 파트  
 다음 표에서 대 한 명명된 된 파트를 <xref:System.Windows.Controls.DatePicker> 제어 합니다.  
  
|파트|형식|설명|  
|-|-|-|  
|PART_Root|<xref:System.Windows.Controls.Grid>|루트 컨트롤입니다.|  
|PART_Button|<xref:System.Windows.Controls.Button>|열고 닫는 단추는 <xref:System.Windows.Controls.Calendar>합니다.|  
|PART_TextBox|<xref:System.Windows.Controls.Primitives.DatePickerTextBox>|날짜를 입력할 수 있는 텍스트 상자입니다.|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|에 대 한 팝업을 <xref:System.Windows.Controls.DatePicker> 제어 합니다.|  
  
## <a name="datepicker-states"></a>DatePicker 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.DatePicker> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|보통|CommonStates|기본 상태입니다.|  
|사용 안 함|CommonStates|<xref:System.Windows.Controls.DatePicker> 을 사용할 수 없습니다.|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 있습니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 가 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="datepickertextbox-parts"></a>DatePickerTextBox 파트  
 다음 표에서 대 한 명명된 된 파트를 <xref:System.Windows.Controls.Primitives.DatePickerTextBox> 제어 합니다.  
  
|파트|형식|설명|  
|-|-|-|  
|PART_Watermark|<xref:System.Windows.Controls.ContentControl>|초기 텍스트를 포함 하는 요소는 <xref:System.Windows.Controls.DatePicker>합니다.|  
|PART_ContentElement|<xref:System.Windows.FrameworkElement>|포함할 수 있는 시각적 요소를 <xref:System.Windows.FrameworkElement>입니다. 텍스트는 <xref:System.Windows.Controls.TextBox> 이 요소에 표시 됩니다.|  
  
## <a name="datepickertextbox-states"></a>DatePickerTextBox 상태  
 다음 표에서 대 한 시각적 상태를 <xref:System.Windows.Controls.Primitives.DatePickerTextBox> 제어 합니다.  
  
|VisualState 이름|VisualStateGroup 이름|설명|  
|-|-|-|  
|보통|CommonStates|기본 상태입니다.|  
|사용 안 함|CommonStates|<xref:System.Windows.Controls.Primitives.DatePickerTextBox> 을 사용할 수 없습니다.|  
|MouseOver|CommonStates|마우스 포인터가 위에 <xref:System.Windows.Controls.Primitives.DatePickerTextBox>합니다.|  
|ReadOnly|CommonStates|사용자의 텍스트를 변경할 수 없습니다는 <xref:System.Windows.Controls.Primitives.DatePickerTextBox>합니다.|  
|포커스 있음|FocusStates|컨트롤에 포커스가 있습니다.|  
|포커스 없음|FocusStates|컨트롤에 포커스가 없습니다.|  
|워터 마크 지정|WatermarkStates|컨트롤의 초기 텍스트를 표시합니다.  <xref:System.Windows.Controls.Primitives.DatePickerTextBox> 상태인 경우 사용자가 텍스트를 입력 하거나 날짜를 선택 하지 않습니다.|  
|Unwatermarked|WatermarkStates|사용자가 텍스트를 입력 합니다 <xref:System.Windows.Controls.Primitives.DatePickerTextBox> 에서 날짜를 선택 하거나를 <xref:System.Windows.Controls.DatePicker>입니다.|  
|유효|ValidationStates|컨트롤에서 사용 된 <xref:System.Windows.Controls.Validation> 클래스 및 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `false`합니다.|  
|InvalidFocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 컨트롤에 포커스가 있을 합니다.|  
|InvalidUnfocused|ValidationStates|합니다 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 연결 된 속성은 `true` 컨트롤에 포커스가 없는 합니다.|  
  
## <a name="datepicker-controltemplate-example"></a>DatePicker ControlTemplate 예제  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.DatePicker> 제어 합니다.  
  
 [!code-xaml[ControlTemplateExamples#DatePicker](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datepicker.xaml#datepicker)]  
  
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
