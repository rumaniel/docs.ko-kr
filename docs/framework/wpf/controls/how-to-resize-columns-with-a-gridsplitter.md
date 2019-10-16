---
title: '방법: GridSplitter로 열 크기 조정'
ms.date: 03/30/2017
helpviewer_keywords:
- grid columns [WPF], resizing
- GridSplitter control [WPF], resizing grid columns
- resizing grid columns [WPF]
ms.assetid: 47b20fe6-7adc-4aa6-9693-b4e184eef74b
ms.openlocfilehash: f743e9ccf8a984a646a4b8f05ee99162e5bc73ad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770697"
---
# <a name="how-to-resize-columns-with-a-gridsplitter"></a>방법: GridSplitter로 열 크기 조정
이 예제에는 세로 만드는 방법을 보여 줍니다 <xref:System.Windows.Controls.GridSplitter> 의 두 열 사이의 간격을 재배포 하기 위해를 <xref:System.Windows.Controls.Grid> 의 크기를 변경 하지 않고는 <xref:System.Windows.Controls.Grid>합니다.  
  
## <a name="example"></a>예제  
 **열의 가장자리를 오버레이하는 GridSplitter를 만드는 방법**  
  
 지정 하는 <xref:System.Windows.Controls.GridSplitter> 에 인접 한 열 크기를 조정 하는 <xref:System.Windows.Controls.Grid>설정를 <xref:System.Windows.Controls.Grid.Column%2A> 크기를 조정할 열 중 하나에 연결 된 속성입니다. 경우에 <xref:System.Windows.Controls.Grid> 둘 이상의 행이 있고 설정의 <xref:System.Windows.Controls.Grid.RowSpan%2A> 연결 된 속성을 행 수입니다. 다음을 설정 합니다 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 속성을 <xref:System.Windows.HorizontalAlignment.Left> 또는 <xref:System.Windows.HorizontalAlignment.Right> (설정 하는 맞춤의 크기를 조정 하려는 두 개의 열에 따라 다름). 마지막으로 설정 합니다 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 속성을 <xref:System.Windows.VerticalAlignment.Stretch>입니다.  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterColumnOverlay](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplittercolumnoverlay)]  
  
 A <xref:System.Windows.Controls.GridSplitter> 고유한 열 없는 다른 컨트롤에 의해 가려질 수 있습니다는 <xref:System.Windows.Controls.Grid>합니다. 이 문제를 방지하는 방법에 대한 자세한 내용은 [Make Sure That a GridSplitter Is Visible](how-to-make-sure-that-a-gridsplitter-is-visible.md)(GridSplitter가 표시되는지 확인)을 참조하세요.  
  
 **열을 차지하는 GridSplitter를 만드는 방법**  
  
 지정 하는 <xref:System.Windows.Controls.GridSplitter> 에서 열을 차지 하는 <xref:System.Windows.Controls.Grid>설정를 <xref:System.Windows.Controls.Grid.Column%2A> 크기를 조정할 열 중 하나에 연결 된 속성. 그리드에 둘 이상의 행에 있는 경우 설정 된 <xref:System.Windows.Controls.Grid.RowSpan%2A> 연결 된 속성을 행 수입니다. 설정한를 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 를 <xref:System.Windows.HorizontalAlignment.Center>설정를 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 속성을 <xref:System.Windows.VerticalAlignment.Stretch>, 설정 및는 <xref:System.Windows.Controls.ColumnDefinition.Width%2A> 포함 된 열의 <xref:System.Windows.Controls.GridSplitter> 에 <xref:System.Windows.GridLength.Auto%2A>합니다.  
  
 다음 예제에서는 세로 정의 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.GridSplitter> 열을 차지 하 고 양쪽에서 열의 크기를 조정 합니다.  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterEntireColumnPart1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart1)]  
[!code-xaml[GridSplitterRowColumn#GridSplitterEntireColumnPart2](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.GridSplitter>
- [방법 항목](gridsplitter-how-to-topics.md)
