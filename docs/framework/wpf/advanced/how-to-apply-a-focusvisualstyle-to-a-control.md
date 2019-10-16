---
title: '방법: 컨트롤에 FocusVisualStyle 적용'
ms.date: 03/30/2017
helpviewer_keywords:
- properties [WPF], FocusVisualStyle
- FocusVisualStyle property [WPF]
ms.assetid: 363de99e-8ecc-438c-ac4a-f9147432ebd6
ms.openlocfilehash: 53d4984946143c15c4a2b71095529fb5ee7de4b1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051327"
---
# <a name="how-to-apply-a-focusvisualstyle-to-a-control"></a>방법: 컨트롤에 FocusVisualStyle 적용
이 예제에서는 리소스에서 포커스 비주얼 스타일을 만들고 컨트롤에 스타일을 적용 하는 방법을 보여 줍니다.를 사용 하 여 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> 속성입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 만드는 추가 컨트롤 합성 컨트롤에 키보드에 포커스가 있을 때만 적용 되는 스타일을 정의 합니다 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]합니다. 사용 하 여 스타일을 정의 하 여 이렇게를 <xref:System.Windows.Controls.ControlTemplate>를 설정 하는 경우 리소스로 해당 스타일을 참조 하는 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> 속성입니다.  
  
 테두리와 같은 외부 영역을 사각형 영역 외부에 배치 됩니다. 스타일의 크기 조정을 사용 하 여 수정이 고, 그렇지 않으면 합니다 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 및 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 포커스 비주얼 스타일이 적용 되는 사각형 컨트롤입니다. 에 대해 음수 값을 설정 하는이 예제는 <xref:System.Windows.FrameworkElement.Margin%2A> 약간 포커스가 있는 컨트롤 외부에 테두리를 확인 합니다.  
  
 [!code-xaml[FEFocusVisualStyle#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEFocusVisualStyle/CS/page1.xaml#xaml)]  
  
 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> 는 가산적 함께 제공 되는 모든 컨트롤 템플릿 스타일에 명시적 스타일 또는 테마 스타일;에서 컨트롤에 대 한 기본 스타일을 여전히 만들 수를 사용 하 여는 <xref:System.Windows.Controls.ControlTemplate> 스타일을 설정 하 고는 <xref:System.Windows.FrameworkElement.Style%2A> 속성.  
  
 포커스 비주얼 스타일 테마 또는 UI를 일관 되 게 사용 해야 각 포커스 가능 요소에 대해 다른 이름을 사용 하는 대신 합니다. 자세한 내용은 참조 하세요 [컨트롤에 FocusVisualStyle 포커스 스타일 지정](styling-for-focus-in-controls-and-focusvisualstyle.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>
- [스타일 지정 및 템플릿](../controls/styling-and-templating.md)
- [컨트롤의 포커스 스타일 지정 및 FocusVisualStyle](styling-for-focus-in-controls-and-focusvisualstyle.md)
