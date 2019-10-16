---
title: '방법: Windows Forms에서 깜빡임을 줄이기 위한 픽셀 복사'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- bitblt
- graphics [Windows Forms], copying
- flicker [Windows Forms], reducing in Windows Forms
- graphics [Windows Forms], reducing flicker
- pixels [Windows Forms], copying
- flicker
- bit-block transfer
ms.assetid: 33b76910-13a3-4521-be98-5c097341ae3b
ms.openlocfilehash: 5a18539153c64a5059d8079f6e245115b026bb91
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950142"
---
# <a name="how-to-copy-pixels-for-reducing-flicker-in-windows-forms"></a>방법: Windows Forms에서 깜빡임을 줄이기 위한 픽셀 복사
간단한 그래픽에 애니메이션 효과를 주는 경우 사용자는 때때로 깜박임 또는 기타 원치 않는 시각적 효과를 발생 시킬 수 있습니다. 이 문제를 제한 하는 한 가지 방법은 그래픽에서 "bitblt" 프로세스를 사용 하는 것입니다. Bitblt는 픽셀의 원본 사각형에서 대상 사각형 까지의 색 데이터의 "비트 블록 전송"입니다.  
  
 Windows Forms에서 bitblt는 <xref:System.Drawing.Graphics.CopyFromScreen%2A> <xref:System.Drawing.Graphics> 클래스의 메서드를 사용 하 여 수행 됩니다. 메서드의 매개 변수에서 원본 및 대상 (포인트로), 복사할 영역의 크기 및 새 셰이프를 그리는 데 사용 되는 그래픽 개체를 지정 합니다.  
  
 아래 예제에서는 셰이프를 해당 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 폼에 그립니다. 그런 다음 메서드를 사용 하 여 셰이프를 복제 합니다. <xref:System.Drawing.Graphics.CopyFromScreen%2A>  
  
> [!NOTE]
> 폼의 <xref:System.Windows.Forms.Control.DoubleBuffered%2A> 속성을로 `true` 설정 하면 <xref:System.Windows.Forms.Control.Paint> 이벤트의 그래픽 기반 코드를 이중 버퍼링 할 수 있습니다. 이는 아래 코드를 사용할 때 뚜렷한 성능이 향상 되지 않지만 보다 복잡 한 그래픽 조작 코드를 사용할 때 고려해 야 할 사항입니다.  
  
## <a name="example"></a>예제  
  
```vb  
Private Sub Form1_Paint(ByVal sender As Object, ByVal e As _  
    System.Windows.Forms.PaintEventArgs) Handles MyBase.Paint  
    ' Draw a circle with a bar on top.  
        e.Graphics.FillEllipse(Brushes.DarkBlue, New Rectangle _  
             (10, 10, 60, 60))  
        e.Graphics.FillRectangle(Brushes.Khaki, New Rectangle _  
             (20, 30, 60, 10))  
    ' Copy the graphic to a new location.  
        e.Graphics.CopyFromScreen(New Point(10, 10), New Point _  
             (100, 100), New Size(70, 70))  
End Sub  
```  
  
```csharp  
private void Form1_Paint(System.Object sender,  
    System.Windows.Forms.PaintEventArgs e)  
        {  
        e.Graphics.FillEllipse(Brushes.DarkBlue, new  
            Rectangle(10,10,60,60));  
        e.Graphics.FillRectangle(Brushes.Khaki, new  
            Rectangle(20,30,60,10));  
        e.Graphics.CopyFromScreen(new Point(10, 10), new Point(100, 100),   
            new Size(70, 70));  
}  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 위의 코드는 폼의 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기에서 실행 되므로 폼을 다시 그릴 때 그래픽이 유지 됩니다. 따라서 폼의 크기를 조정 하거나 다른 폼으로 숨기는 <xref:System.Windows.Forms.Form.Load> 경우에는 그려지는 콘텐츠가 다시 그려지지 않으므로 이벤트 처리기에서 그래픽 관련 메서드를 호출 하지 마십시오.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.CopyPixelOperation>
- <xref:System.Drawing.Graphics.FillRectangle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.OnPaint%2A?displayProperty=nameWithType>
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
