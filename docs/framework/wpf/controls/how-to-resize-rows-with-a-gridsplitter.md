---
title: '방법: GridSplitter로 행 크기 조정'
ms.date: 03/30/2017
helpviewer_keywords:
- resizing grid rows [WPF]
- grid rows [WPF], resizing
- GridSplitter control [WPF], resizing grid rows
ms.assetid: 2413a9f2-1d81-46ed-95cb-95ec8233eea2
ms.openlocfilehash: 6760a7a691af4f666294556cae3bc95a4299730a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770710"
---
# <a name="how-to-resize-rows-with-a-gridsplitter"></a>방법: GridSplitter로 행 크기 조정
이 예제에서는 가로 사용 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.GridSplitter> 에 있는 두 행 사이의 간격을 재배포 하는 <xref:System.Windows.Controls.Grid> 의 크기를 변경 하지 않고는 <xref:System.Windows.Controls.Grid>.  
  
## <a name="example"></a>예제  
 **행의 가장자리를 오버레이하는 GridSplitter를 만드는 방법**  
  
 지정 하는 <xref:System.Windows.Controls.GridSplitter> 인접 행 크기를 조정 하는 <xref:System.Windows.Controls.Grid>설정는 <xref:System.Windows.Controls.Grid.Row%2A> 크기를 조정할 행 중 하나에 연결 된 속성입니다. 경우에 <xref:System.Windows.Controls.Grid> 둘 이상의 열이 있는 설정의 <xref:System.Windows.Controls.Grid.ColumnSpan%2A> 연결 된 속성을 열 수를 지정 합니다. 설정한 합니다 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 하 <xref:System.Windows.VerticalAlignment.Top> 또는 <xref:System.Windows.VerticalAlignment.Bottom> (설정 하는 맞춤의 크기를 조정 하려는 두 개의 행에 따라 다름). 마지막으로 설정 합니다 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 속성을 <xref:System.Windows.HorizontalAlignment.Stretch>입니다.  
  
 다음 예제에서는 가로 정의 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.GridSplitter> 인접 한 행의 크기를 조정 하 합니다.  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterRowOverlay](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterrowoverlay)]  
  
 A <xref:System.Windows.Controls.GridSplitter> 자체 행을 차지 하지 않습니다 다른 컨트롤에 의해 가려질 수 있습니다는 <xref:System.Windows.Controls.Grid>합니다. 이 문제를 방지하는 방법에 대한 자세한 내용은 [Make Sure That a GridSplitter Is Visible](how-to-make-sure-that-a-gridsplitter-is-visible.md)(GridSplitter가 표시되는지 확인)을 참조하세요.  
  
 **행을 차지하는 GridSplitter를 만드는 방법**  
  
 지정 하는 <xref:System.Windows.Controls.GridSplitter> 에서 행을 차지 하는 <xref:System.Windows.Controls.Grid>설정는 <xref:System.Windows.Controls.Grid.Row%2A> 크기를 조정할 행 중 하나에 연결 된 속성입니다. 경우에 <xref:System.Windows.Controls.Grid> 둘 이상의 열이 있는 설정의 <xref:System.Windows.Controls.Grid.ColumnSpan%2A> 연결 된 속성을 열 수 있습니다. 설정한를 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 를 <xref:System.Windows.VerticalAlignment.Center>설정 합니다 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 속성을 <xref:System.Windows.HorizontalAlignment.Stretch>, 설정 및를 <xref:System.Windows.Controls.RowDefinition.Height%2A> 포함 된 행의를 <xref:System.Windows.Controls.GridSplitter> 를 <xref:System.Windows.GridLength.Auto%2A>.  
  
 다음 예제에서는 가로 정의 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.GridSplitter> 행을 차지 하 고 양쪽에서 행의 크기를 조정 합니다.  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterEntireRowPart1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart1)]  
[!code-xaml[GridSplitterRowColumn#GridSplitterEntireRowPart2](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.GridSplitter>
- [방법 항목](gridsplitter-how-to-topics.md)
