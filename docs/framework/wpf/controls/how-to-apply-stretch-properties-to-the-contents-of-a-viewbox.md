---
title: '방법: Viewbox의 콘텐츠에 Stretch 속성 적용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- StretchDirection properties [WPF]
- Stretch properties [WPF]
- controls [WPF], Viewbox
- Viewbox control [WPF]
ms.assetid: b9c22ef4-bce4-4300-9e0c-8260b7db83cc
ms.openlocfilehash: 08358ea07e0c41e3b7cdf52251a3ed4296035e2d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62019037"
---
# <a name="how-to-apply-stretch-properties-to-the-contents-of-a-viewbox"></a>방법: Viewbox의 콘텐츠에 Stretch 속성 적용
## <a name="example"></a>예제  
 값을 변경 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Viewbox.StretchDirection%2A> 하 고 <xref:System.Windows.Controls.Viewbox.Stretch%2A> 의 속성을 <xref:System.Windows.Controls.Viewbox>.  
  
 첫 번째 예제에서는 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 정의 하는 <xref:System.Windows.Controls.Viewbox> 요소입니다. 할당 된 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 고 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 400입니다. 예제에서는 중첩을 <xref:System.Windows.Controls.Image> 내의 요소는 <xref:System.Windows.Controls.Viewbox>합니다. <xref:System.Windows.Controls.Button> 속성 값에 해당 하는 요소는 <xref:System.Windows.Controls.Viewbox.Stretch%2A> 하 고 <xref:System.Windows.Controls.StretchDirection> 중첩 된 확장 동작을 조작 하는 열거형 <xref:System.Windows.Controls.Image>.  
  
 [!code-xaml[viewboxStretchLayoutSamp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml#1)]  
  
 다음 코드 숨김 파일 핸들은 <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트는 이전 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 예제에서는 정의 합니다.  
  
 [!code-csharp[viewboxStretchLayoutSamp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml.cs#2)]
 [!code-vb[viewboxStretchLayoutSamp#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/viewboxStretchLayoutSamp/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Viewbox>
- <xref:System.Windows.Media.Stretch>
- <xref:System.Windows.Controls.StretchDirection>
