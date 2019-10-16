---
title: '방법: Thumb을 사용하여 캔버스 크기 조정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- resizing Canvas control [WPF]
- controls [WPF], Thumb
- controls [WPF], Canvas
- Thumb control [WPF]
- Canvas control [WPF]
ms.assetid: 7dc9f435-726c-4d4d-be41-eb24cfe17bef
ms.openlocfilehash: 14942157429b029147d47e2f88428c56e66523d1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770749"
---
# <a name="how-to-resize-a-canvas-by-using-a-thumb"></a>방법: Thumb을 사용하여 캔버스 크기 조정
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Primitives.Thumb> 컨트롤의 크기를 조정 하는 <xref:System.Windows.Controls.Canvas> 컨트롤입니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Controls.Primitives.Thumb> 컨트롤을 이동 하거나 모니터링 하 여 컨트롤을 크기 조정에 사용할 수 있는 끌기 기능을 제공 합니다 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>, <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 및 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> 의 이벤트는 <xref:System.Windows.Controls.Primitives.Thumb>합니다.  
  
 사용자가 마우스 포인터의 일시 중지 되 면 마우스 왼쪽된 단추를 눌러 끌기 작업을 시작 합니다 <xref:System.Windows.Controls.Primitives.Thumb> 제어 합니다. 끌기 작업에는 마우스 왼쪽된 단추를 누른 동안 계속 됩니다. 끌기 작업 중의 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 두 번 이상 발생할 수 있습니다. 발생할 때마다는 <xref:System.Windows.Controls.Primitives.DragDeltaEventArgs> 클래스는 해당 마우스 위치를 변경 하는 위치에 변경 내용을 제공 합니다. 마우스 왼쪽된 단추를 놓을 때 끌기 작업 완료 되었습니다. 끌기 작업만 새 좌표를 제공 합니다. 자동으로 위치를 유지 합니다 <xref:System.Windows.Controls.Primitives.Thumb>합니다.  
  
 에서는 다음 예제는 <xref:System.Windows.Controls.Primitives.Thumb> 컨트롤의 자식 요소인은 <xref:System.Windows.Controls.Canvas> 제어 합니다. 이벤트 처리기를 해당 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 이동할 논리를 제공 하는 이벤트를 <xref:System.Windows.Controls.Primitives.Thumb> 크기를 조정 하 고는 <xref:System.Windows.Controls.Canvas>합니다. 에 대 한 이벤트 처리기를 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted> 하 고 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> 의 색을 변경 하는 이벤트를 <xref:System.Windows.Controls.Primitives.Thumb> 끌기 작업 중입니다. 다음 예제에서는 정의 된 <xref:System.Windows.Controls.Primitives.Thumb>합니다.  
  
 [!code-xaml[Thumb#thumb](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml#thumb)]  
  
 다음 예제와 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 이동 하는 이벤트 처리기는 <xref:System.Windows.Controls.Primitives.Thumb> 크기를 조정 하 고는 <xref:System.Windows.Controls.Canvas> 마우스 이동에 대 한 응답에서 합니다.  
  
 [!code-csharp[Thumb#2](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#2)]  
  
 다음 예제는 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted> 이벤트 처리기입니다.  
  
 [!code-csharp[Thumb#DragStartedHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragstartedhandler)]
 [!code-vb[Thumb#DragStartedHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragstartedhandler)]  
  
 다음 예제는 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> 이벤트 처리기입니다.  
  
 [!code-csharp[Thumb#DragCompletedHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragcompletedhandler)]
 [!code-vb[Thumb#DragCompletedHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragcompletedhandler)]  
  
 전체 샘플을 참조 하세요 [Thumb 끌기 기능 샘플](https://go.microsoft.com/fwlink/?LinkID=160042)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Primitives.Thumb>
- <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>
- <xref:System.Windows.Controls.Primitives.Thumb.DragDelta>
- <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted>
