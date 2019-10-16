---
title: Windows Forms 컨트롤 렌더링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], rendering
- OnPaintBackground method [Windows Forms], invoking in Windows Forms custom controls
- custom controls [Windows Forms], graphics resources
- custom controls [Windows Forms], invalidation and painting
ms.assetid: aae8e1e6-4786-432b-a15e-f4c44760d302
ms.openlocfilehash: b24fbefac0dcfb666e25ad1d1726ef2cf8a5d84e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968271"
---
# <a name="rendering-a-windows-forms-control"></a>Windows Forms 컨트롤 렌더링
렌더링은 사용자 화면에서 시각적 표시를 만드는 프로세스를 나타냅니다. Windows Forms는 GDI (새 Windows graphics library)를 사용 하 여 렌더링 합니다. GDI에 대 한 액세스를 제공 하는 관리 되 <xref:System.Drawing?displayProperty=nameWithType> 는 클래스는 네임 스페이스 및 네임 스페이스에 있습니다.  
  
 컨트롤 렌더링에는 다음 요소가 포함 됩니다.  
  
- 기본 클래스 <xref:System.Windows.Forms.Control?displayProperty=nameWithType>에서 제공 하는 그리기 기능입니다.  
  
- GDI 그래픽 라이브러리의 필수 요소입니다.  
  
- 그리기 영역의 기 하 도형입니다.  
  
- 그래픽 리소스를 해제 하기 위한 절차입니다.  
  
## <a name="drawing-functionality-provided-by-control"></a>컨트롤에서 제공 하는 그리기 기능  
 기본 클래스 <xref:System.Windows.Forms.Control> 는 <xref:System.Windows.Forms.Control.Paint> 이벤트를 통해 그리기 기능을 제공 합니다. 컨트롤은 표시를 <xref:System.Windows.Forms.Control.Paint> 업데이트 해야 할 때마다 이벤트를 발생 시킵니다. .NET Framework 이벤트에 대 한 자세한 내용은 [이벤트 처리 및 발생](../../../standard/events/index.md)을 참조 하세요.  
  
 <xref:System.Windows.Forms.Control.Paint> 이벤트에 대 한 이벤트 데이터 클래스는 컨트롤을 그리는 데 필요한 데이터, 즉 그래픽 개체에 대 한 핸들과 그릴 영역을 나타내는 사각형 개체를 보유 합니다. <xref:System.Windows.Forms.PaintEventArgs> 이러한 개체는 다음 코드 조각에서 굵게 표시 됩니다.  
  
```vb  
Public Class PaintEventArgs  
   Inherits EventArgs  
   Implements IDisposable  
  
   Public ReadOnly Property ClipRectangle() As System.Drawing.Rectangle  
      ...  
   End Property  
  
   Public ReadOnly Property Graphics() As System.Drawing.Graphics  
      ...  
   End Property  
   ' Other properties and methods.  
   ...  
End Class  
```  
  
```csharp  
public class PaintEventArgs : EventArgs, IDisposable {  
public System.Drawing.Rectangle ClipRectangle {get;}  
public System.Drawing.Graphics Graphics {get;}  
// Other properties and methods.  
...  
}  
```  
  
 <xref:System.Drawing.Graphics>는이 항목의 뒷부분에 나오는 GDI의 설명에 설명 된 대로 그리기 기능을 캡슐화 하는 관리 되는 클래스입니다. 는 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 구조체<xref:System.Drawing.Rectangle> 의 인스턴스이고 컨트롤에서 그릴 수 있는 사용 가능한 영역을 정의 합니다. 컨트롤 개발자는이 항목의 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 뒷부분에 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 있는 geometry의 설명에 설명 된 대로 컨트롤의 속성을 사용 하 여를 계산할 수 있습니다.  
  
 <xref:System.Windows.Forms.Control.OnPaint%2A> 컨트롤이<xref:System.Windows.Forms.Control>상속 하는 메서드를 재정의 하 여 렌더링 논리를 제공 해야 합니다. <xref:System.Windows.Forms.Control.OnPaint%2A>및에 전달 된 <xref:System.Windows.Forms.PaintEventArgs> 인스턴스의 속성을통해그릴사각형및그래픽개체에대한액세스를가져옵니다.<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> <xref:System.Drawing.Design.PaintValueEventArgs.Graphics%2A>  
  
```vb  
Protected Overridable Sub OnPaint(pe As PaintEventArgs)  
```  
  
```csharp  
protected virtual void OnPaint(PaintEventArgs pe);  
```  
  
 기본 <xref:System.Windows.Forms.Control.OnPaint%2A> <xref:System.Windows.Forms.Control.Paint> 클래스의 메서드는 그리기 기능을 구현 하지 않지만 단순히 이벤트에 등록 된 이벤트 대리자를 호출 합니다. <xref:System.Windows.Forms.Control> 을 재정의 <xref:System.Windows.Forms.Control.OnPaint%2A>하는 경우 일반적으로 등록 된 <xref:System.Windows.Forms.Control.OnPaint%2A> 대리자가 이벤트를 <xref:System.Windows.Forms.Control.Paint> 받도록 기본 클래스의 메서드를 호출 해야 합니다. 그러나이로 인해 깜박임이 도입 되므로 전체 화면을 그리는 컨트롤은 기본 클래스 <xref:System.Windows.Forms.Control.OnPaint%2A>의를 호출 하면 안 됩니다. <xref:System.Windows.Forms.Control.OnPaint%2A> 이벤트를 재정의 하는 예제를 [보려면 방법: 진행률](how-to-create-a-windows-forms-control-that-shows-progress.md)을 표시 하는 Windows Forms 컨트롤을 만듭니다.  
  
> [!NOTE]
> 컨트롤에서 직접 <xref:System.Windows.Forms.Control.OnPaint%2A> 호출 하지 말고 대신 <xref:System.Windows.Forms.Control.Invalidate%2A> 메서드 (에서 <xref:System.Windows.Forms.Control>상속) 또는를 호출 <xref:System.Windows.Forms.Control.Invalidate%2A>하는 다른 메서드를 호출 합니다. 그런 <xref:System.Windows.Forms.Control.Invalidate%2A> 다음 메서드는를 <xref:System.Windows.Forms.Control.OnPaint%2A>호출 합니다. 메서드가 오버 로드 되 고에 <xref:System.Windows.Forms.Control.Invalidate%2A> `e`제공 된 인수에 따라 컨트롤이 화면 영역의 일부 또는 전체를 다시 그립니다. <xref:System.Windows.Forms.Control.Invalidate%2A>  
  
 기본 <xref:System.Windows.Forms.Control> 클래스는 메서드를 그리는 데 유용한 다른 메서드를 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 정의 합니다.  
  
```vb  
Protected Overridable Sub OnPaintBackground(pevent As PaintEventArgs)  
```  
  
```csharp  
protected virtual void OnPaintBackground(PaintEventArgs pevent);  
```  
  
 <xref:System.Windows.Forms.Control.OnPaintBackground%2A>는 창의 배경 (그리고 그에 따라 셰이프)을 칠하고,는 <xref:System.Windows.Forms.Control.OnPaint%2A> 빠른 것으로 확인 되 고, 개별 페인트 요청은 모든 영역을 포함 하는 하나의 <xref:System.Windows.Forms.Control.Paint> 이벤트로 결합 되기 때문에 속도가 느릴 수 있습니다. 그려야. 예를 들어 컨트롤의 그라데이션 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 색 배경을 그리려면를 호출 하는 것이 좋습니다.  
  
 에는 이벤트와 유사한 명명법이 있고 `OnPaint` 메서드와 동일한 인수를 사용 하지만 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 는 진정한 이벤트 메서드가 아닙니다. <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 이벤트는 없으며 `PaintBackground`이벤트대리자 를호출하지않습니다.<xref:System.Windows.Forms.Control.OnPaintBackground%2A> <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 메서드를 재정의 하는 경우 파생 클래스는 기본 클래스의 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 메서드를 호출 하는 데 필요 하지 않습니다.  
  
## <a name="gdi-basics"></a>GDI + 기본 사항  
 이 <xref:System.Drawing.Graphics> 클래스는 텍스트를 표시 하는 메서드 뿐만 아니라 원, 삼각형, 원호 및 타원과 같은 다양 한 모양을 그리기 위한 메서드를 제공 합니다. 네임 <xref:System.Drawing?displayProperty=nameWithType> 스페이스 및 네임 스페이스에는 도형 (원, 사각형, 원호 등), 색, 글꼴, 브러시 등의 그래픽 요소를 캡슐화 하는 클래스가 포함 되어 있습니다. GDI에 대 한 자세한 내용은 [관리 되는 그래픽 클래스 사용](../advanced/using-managed-graphics-classes.md)을 참조 하세요. 또한 GDI의 essentials는 [방법: 진행률](how-to-create-a-windows-forms-control-that-shows-progress.md)을 표시 하는 Windows Forms 컨트롤을 만듭니다.  
  
## <a name="geometry-of-the-drawing-region"></a>그리기 영역의 기 하 도형  
 컨트롤 <xref:System.Windows.Forms.Control.ClientRectangle%2A> 의 속성은 사용자 화면에서 컨트롤에 사용할 수 있는 사각형 영역을 지정 하는 반면의 <xref:System.Windows.Forms.PaintEventArgs> 속성 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 은 실제로 그려지는 영역을 지정 합니다. 인스턴스를 <xref:System.Windows.Forms.Control.Paint> <xref:System.Windows.Forms.PaintEventArgs> 인수로 사용 하는 이벤트 메서드에서 그리기가 수행 됩니다. 컨트롤 표시의 작은 섹션이 변경 되는 경우 처럼 컨트롤은 사용 가능한 영역의 일부만 그려야 할 수 있습니다. 이러한 상황에서 컨트롤 개발자는에 그릴 실제 사각형을 계산 하 고이를에 <xref:System.Windows.Forms.Control.Invalidate%2A>전달 해야 합니다. <xref:System.Windows.Forms.Control.Invalidate%2A> 또는 <xref:System.Drawing.Rectangle> <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 를 인수로 사용 하는의 오버 로드 된 버전은 해당 인수를 사용 하 여의 속성을 생성 합니다. <xref:System.Drawing.Region>  
  
 다음 코드 조각에서는 `FlashTrackBar` 사용자 지정 컨트롤이 그릴 사각형 영역을 계산 하는 방법을 보여 줍니다. 변수 `client` 는 속성을 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 나타냅니다. 전체 샘플을 보려면 [방법: 진행률](how-to-create-a-windows-forms-control-that-shows-progress.md)을 표시 하는 Windows Forms 컨트롤을 만듭니다.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#6)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#6)]  
  
## <a name="freeing-graphics-resources"></a>그래픽 리소스 해제  
 그래픽 개체는 시스템 리소스를 사용 하기 때문에 비용이 많이 듭니다. 이러한 개체에는 <xref:System.Drawing.Graphics?displayProperty=nameWithType> 클래스 <xref:System.Drawing.Brush?displayProperty=nameWithType>인스턴스 뿐 아니라, <xref:System.Drawing.Pen?displayProperty=nameWithType>및 기타 그래픽 클래스 인스턴스도 포함 됩니다. 필요한 경우에만 그래픽 리소스를 만들고 사용을 마친 후에 바로 릴리스 하는 것이 중요 합니다. 인터페이스를 <xref:System.IDisposable> 구현 하는 형식을 만드는 경우 리소스를 해제 하기 <xref:System.IDisposable.Dispose%2A> 위해 작업이 완료 되 면 메서드를 호출 합니다.  
  
 다음 코드 조각에서는 사용자 지정 컨트롤 `FlashTrackBar` 에서 리소스를 <xref:System.Drawing.Brush> 만들고 해제 하는 방법을 보여 줍니다. 전체 소스 코드를 보려면 [방법: 진행률](how-to-create-a-windows-forms-control-that-shows-progress.md)을 표시 하는 Windows Forms 컨트롤을 만듭니다.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#5)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#5)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#4)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#4)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#3)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#3)]  
  
## <a name="see-also"></a>참고자료

- [방법: 진행률을 표시 하는 Windows Forms 컨트롤 만들기](how-to-create-a-windows-forms-control-that-shows-progress.md)
