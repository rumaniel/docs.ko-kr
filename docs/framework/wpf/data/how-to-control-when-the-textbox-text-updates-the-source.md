---
title: '방법: TextBox 텍스트가 소스를 업데이트하는 시점 제어'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- source updates [WPF], timing of
- data binding [WPF], timing of source updates
- timing of source updates [WPF]
ms.assetid: ffb7b96a-351d-4c68-81e7-054033781c64
ms.openlocfilehash: d1d624d7550a1135431b7fffc7450e3a510855a7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966464"
---
# <a name="how-to-control-when-the-textbox-text-updates-the-source"></a>방법: TextBox 텍스트가 소스를 업데이트하는 시점 제어
이 항목에서는 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 속성을 사용 하 여 바인딩 소스 업데이트의 타이밍을 제어 하는 방법에 대해 설명 합니다. 이 항목에서는 컨트롤 <xref:System.Windows.Controls.TextBox> 을 예제로 사용 합니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Controls.TextBox>.<xref:System.Windows.Controls.TextBox.Text%2A> 속성의 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus>기본값은입니다. 이는 응용 프로그램에 데이터 바인딩된 <xref:System.Windows.Controls.TextBox> <xref:System.Windows.Controls.TextBox>가 있는 경우를 의미 합니다.<xref:System.Windows.Controls.TextBox.Text%2A> 속성에서에 입력 <xref:System.Windows.Controls.TextBox> 하는 텍스트는가 포커스를 <xref:System.Windows.Controls.TextBox> 잃을 때까지 원본을 업데이트 하지 않습니다 (예를 들어를 클릭 <xref:System.Windows.Controls.TextBox>한 경우).  
  
 입력할 때 원본을 업데이트 하려면 바인딩의를 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 로 <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>설정 합니다. 다음 예제에서 강조 표시 된 코드 줄은 `Text` <xref:System.Windows.Controls.TextBox> 및 <xref:System.Windows.Controls.TextBlock> 의 속성이 모두 동일한 소스 속성에 바인딩되어 있음을 보여 줍니다. 바인딩의 속성은 로<xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>설정 됩니다. <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> <xref:System.Windows.Controls.TextBox>  
  
 [!code-xaml[SimpleBinding#USTHowTo](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml?highlight=33-39,41-42)]  
  
 결과적으로,는 <xref:System.Windows.Controls.TextBlock> 샘플의 다음 스크린샷에 표시 된 것 처럼 사용자가에 <xref:System.Windows.Controls.TextBox>텍스트를 입력할 때 원본 변경 내용으로 인해 동일한 텍스트를 표시 합니다.  
  
 ![간단한 데이터 바인딩을 보여 주는 스크린샷](./media/how-to-control-when-the-textbox-text-updates-the-source/data-binding-simple-binding-sample.png)  
  
 대화 상자 또는 사용자가 편집할 수 있는 폼이 있고 사용자가 필드 편집을 마치고 "확인"을 클릭할 때까지 원본 업데이트를 지연 하려는 경우 다음 예제와 같이 바인딩의 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 값을로 <xref:System.Windows.Data.UpdateSourceTrigger.Explicit>설정할 수 있습니다.  
  
 [!code-xaml[UpdateSource#2](~/samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml#2)]  
  
 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 값을로 <xref:System.Windows.Data.UpdateSourceTrigger.Explicit>설정 하면 응용 프로그램에서 메서드를 <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> 호출 하는 경우에만 소스 값이 변경 됩니다. 다음 예제에서는에 대해 <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> `itemNameTextBox`를 호출 하는 방법을 보여 줍니다.  
  
 [!code-csharp[UpdateSource#1](~/samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml.cs#1)]
 [!code-vb[UpdateSource#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UpdateSource/VisualBasic/Window1.xaml.vb#1)]  
  
> [!NOTE]
> 다른 컨트롤의 속성에 동일한 기법을 사용할 수 있지만 대부분의 다른 속성에는 기본값이 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>있습니다. 자세한 내용은 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 속성 페이지를 참조 하세요.  
  
> [!NOTE]
> 속성 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 은 원본 업데이트를 처리 하므로 <xref:System.Windows.Data.BindingMode.TwoWay> 또는 <xref:System.Windows.Data.BindingMode.OneWayToSource> 바인딩과만 관련 됩니다. <xref:System.Windows.Data.BindingMode.TwoWay> 및<xref:System.Windows.Data.BindingMode.OneWayToSource> 바인딩이 작동 하려면 소스 개체가 속성 변경 알림을 제공 해야 합니다. 자세한 내용은 이 항목에 제시된 샘플을 참조하세요. 또한 [속성 변경 알림 구현](how-to-implement-property-change-notification.md)을 참조할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [방법 항목](data-binding-how-to-topics.md)
