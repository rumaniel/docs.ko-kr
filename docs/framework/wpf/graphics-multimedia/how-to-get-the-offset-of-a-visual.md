---
title: '방법: 시각적 개체의 오프셋 가져오기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- getting offset values from visual objects [WPF]
- offset values [WPF], retrieving from visual objects [WPF]
- visual objects [WPF], retrieving offset values from
- retrieving offset values from visual objects [WPF]
ms.assetid: 889a1dd6-1b11-445a-b351-fbb04c53ee34
ms.openlocfilehash: 4787b771c7e59a8b033b9267079c068a5845a1e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947496"
---
# <a name="how-to-get-the-offset-of-a-visual"></a>방법: 시각적 개체의 오프셋 가져오기
이러한 예제에는 해당 부모 또는 상위 항목 또는 하위 항목을 기준으로 하는 시각적 개체의 오프셋된 값을 검색 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 태그 예제는 <xref:System.Windows.Controls.TextBlock> 로 정의 된 <xref:System.Windows.FrameworkElement.Margin%2A> 4의 값입니다.  
  
 [!code-xaml[VisualSnippets#VisualSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml#visualsnippet1)]  
  
 다음 코드 예제를 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.VisualTreeHelper.GetOffset%2A> 의 오프셋을 검색 하는 메서드는 <xref:System.Windows.Controls.TextBlock>합니다. 오프셋된 값이 포함 되어 반환 된 <xref:System.Windows.Vector> 값입니다.  
  
 [!code-csharp[VisualSnippets#VisualSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet2)]
 [!code-vb[VisualSnippets#VisualSnippet2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet2)]  
  
 오프셋을 고려 합니다 <xref:System.Windows.FrameworkElement.Margin%2A> 값입니다. 이 예에서 <xref:System.Windows.Vector.X%2A> 가 4 및 <xref:System.Windows.Vector.Y%2A> 은 4입니다.  
  
 부모에 상대적인 오프셋된 값이 반환된 됩니다는 <xref:System.Windows.Media.Visual>합니다. 부모에 상대적인 없는 오프셋된 값을 반환 하려는 경우는 <xref:System.Windows.Media.Visual>를 사용 하 여를 <xref:System.Windows.Media.Visual.TransformToAncestor%2A> 메서드.  
  
## <a name="getting-the-offset-relative-to-an-ancestor"></a>상위 요소에 상대적인 오프셋 가져오기  
 다음 태그 예제는 <xref:System.Windows.Controls.TextBlock> 안에 두 개의 중첩 된 <xref:System.Windows.Controls.StackPanel> 개체입니다.  
  
 [!code-xaml[VisualSnippets#VisualSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window2.xaml#visualsnippet7)]  
  
 다음 그림에서는 태그의 결과 보여 줍니다.  
  
 ![개체의 값을 오프셋](./media/visualoffset-01.png "VisualOffset_01")  
두 Stackpanel 내에 중첩 된 TextBlock  
  
 다음 코드 예제를 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.Visual.TransformToAncestor%2A> 의 오프셋을 검색 하는 메서드를 <xref:System.Windows.Controls.TextBlock> 포함 하는 기준으로 <xref:System.Windows.Window>입니다. 오프셋된 값이 포함 되어 반환 된 <xref:System.Windows.Media.GeneralTransform> 값입니다.  
  
 [!code-csharp[VisualSnippets#VisualSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet5)]
 [!code-vb[VisualSnippets#VisualSnippet5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet5)]  
  
 오프셋을 고려 합니다 <xref:System.Windows.FrameworkElement.Margin%2A> 내의 포함 하는 모든 개체에 대 한 값 <xref:System.Windows.Window>합니다. 이 예에서 <xref:System.Windows.Vector.X%2A> 는 28 (16 + 8 + 4) 및 <xref:System.Windows.Vector.Y%2A> 는 28입니다.  
  
 반환된 된 오프셋된 값의 상위 항목을 기준으로는 <xref:System.Windows.Media.Visual>합니다. 하위 항목에 상대적인 오프셋된 값을 반환 하려는 경우는 <xref:System.Windows.Media.Visual>를 사용 하 여를 <xref:System.Windows.Media.Visual.TransformToDescendant%2A> 메서드.  
  
## <a name="getting-the-offset-relative-to-a-descendant"></a>하위 요소에 상대적인 오프셋 가져오기  
 다음 태그 예제는 <xref:System.Windows.Controls.TextBlock> 에 포함 된를 <xref:System.Windows.Controls.StackPanel> 개체입니다.  
  
 [!code-xaml[VisualSnippets#VisualSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml#visualsnippet4)]  
  
 다음 코드 예제를 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.Visual.TransformToDescendant%2A> 의 오프셋을 검색 하는 메서드를 <xref:System.Windows.Controls.StackPanel> 해당 자식에 상대적인 <xref:System.Windows.Controls.TextBlock>합니다. 오프셋된 값이 포함 되어 반환 된 <xref:System.Windows.Media.GeneralTransform> 값입니다.  
  
 [!code-csharp[VisualSnippets#VisualSnippet9](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet9)]
 [!code-vb[VisualSnippets#VisualSnippet9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet9)]  
  
 오프셋을 고려 합니다 <xref:System.Windows.FrameworkElement.Margin%2A> 모든 개체에 대 한 값입니다. 이 예에서 <xref:System.Windows.Vector.X%2A> -4 이며, 및 <xref:System.Windows.Vector.Y%2A> -4 이며, 합니다. 부모 개체는 해당 자식 개체를 기준으로 오프셋 부정적인 되므로 오프셋된 값은 음수 값으로 지정 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.Media.VisualTreeHelper>
- [WPF 그래픽 렌더링 개요](wpf-graphics-rendering-overview.md)
