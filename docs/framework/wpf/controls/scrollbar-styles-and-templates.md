---
title: ScrollBar 스타일 및 템플릿
ms.date: 03/30/2017
helpviewer_keywords:
- styles [WPF], ScrollBar
- ControlTemplate [WPF], ScrollBar
- states [WPF], ScrollBar
- ScrollBar [WPF], styles and templates
- templates [WPF], ScrollBar
- parts [WPF], ScrollBar
ms.assetid: 066ea45a-e27d-43b0-adfe-cce6934c22f5
ms.openlocfilehash: 016556fb825ddf60af7dc572d6fda7323b9bb09d
ms.sourcegitcommit: 3eeea78f52ca771087a6736c23f74600cc662658
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2019
ms.locfileid: "68671978"
---
# <a name="scrollbar-styles-and-templates"></a>ScrollBar 스타일 및 템플릿
이 항목에서는 <xref:System.Windows.Controls.Primitives.ScrollBar> 컨트롤의 스타일 및 템플릿에 대해 설명 합니다. 기본값을 수정할 수 있습니다 <xref:System.Windows.Controls.ControlTemplate> 고유한 모양을 제어할 수 있습니다. 자세한 내용은 [ControlTemplate을 만들어 기존 컨트롤의 모양 사용자 지정](customizing-the-appearance-of-an-existing-control.md)을 참조하세요.  
  
## <a name="scrollbar-parts"></a>스크롤 막대 부분  
 다음 표에서는 <xref:System.Windows.Controls.Primitives.ScrollBar> 컨트롤의 명명 된 파트를 나열 합니다.  
  
|부분|형식|Description|  
|-|-|-|  
|PART_Track|<xref:System.Windows.Controls.Primitives.Track>|의 위치를 나타내는 요소에 대 한 컨테이너입니다 <xref:System.Windows.Controls.Primitives.ScrollBar>.|  
  
## <a name="scrollbar-states"></a>스크롤 막대 상태  
 다음 표에서는 <xref:System.Windows.Controls.Primitives.ScrollBar> 컨트롤의 시각적 상태를 보여 줍니다.  
  
|VisualState 이름|VisualStateGroup 이름|Description|  
|----------------------|---------------------------|-----------------|  
|일반|CommonStates|기본 상태입니다.|  
|MouseOver|CommonStates|마우스 포인터가 컨트롤 위에 있습니다.|  
|사용 안 함|CommonStates|컨트롤이 비활성화되었습니다.|  
|유효|ValidationStates|컨트롤은 클래스를 <xref:System.Windows.Controls.Validation> 사용 하 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 고 연결 된 속성 `false`은입니다.|  
|InvalidFocused|ValidationStates|연결 된 속성이이 `true` 고 컨트롤에 포커스가 있습니다. <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>|  
|InvalidUnfocused|ValidationStates|연결 된 속성이이 `true` 고 컨트롤에 포커스가 없는 경우 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>|  
  
## <a name="scrollbar-controltemplate-example"></a>ScrollBar ControlTemplate 예제  
 다음 예제에서는 <xref:System.Windows.Controls.Primitives.ScrollBar> 컨트롤에 대 한을 <xref:System.Windows.Controls.ControlTemplate> 정의 하는 방법을 보여 줍니다.  
  
 [!code-xaml[ControlTemplateExamples#ScrollBar](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/scrollbar.xaml#scrollbar)]  
  
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
