---
title: OnPaint 메서드 재정의
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Paint event [Windows Forms], handling in Windows Forms custom control
- OnPaint method [Windows Forms], overriding in Windows Forms custom controls
ms.assetid: e9ca2723-0107-4540-bb21-4f5ffb4a9906
ms.openlocfilehash: e3c48aec830cdc3ccceb8683f93e3a99ee6364e2
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506190"
---
# <a name="overriding-the-onpaint-method"></a>OnPaint 메서드 재정의
.NET Framework에 정의 된 이벤트를 재정의 하기 위한 기본 단계는 동일 하며 다음 목록에 요약 되어 있습니다.  
  
#### <a name="to-override-an-inherited-event"></a>상속 된 이벤트를 재정의 하려면  
  
1. 보호 된 재정의 `On` *EventName* 메서드.  
  
2. 호출을 `On` *EventName* 기본 클래스에서 재정의 된 메서드의 `On` *EventName* 메서드를 등록 된 대리자가 이벤트를 받도록 합니다.  
  
 합니다 <xref:System.Windows.Forms.Control.Paint> 이벤트는 모든 Windows Forms 컨트롤 재정의 해야 하기 때문에 여기에서 자세히 설명 되어 합니다 <xref:System.Windows.Forms.Control.Paint> 에서 상속 하는 이벤트 <xref:System.Windows.Forms.Control>합니다. 기본 <xref:System.Windows.Forms.Control> 클래스에서 파생된 된 컨트롤을 그릴 수 있도록 요구 하는 방법을 알 수 없습니다 및의 모든 그리기 논리를 제공 하지 않습니다는 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드. 합니다 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드의 <xref:System.Windows.Forms.Control> 디스패치 하기만 합니다 <xref:System.Windows.Forms.Control.Paint> 이벤트 등록 된 이벤트 수신기를 합니다.  
  
 샘플을 수행한 경우 [방법: 간단한 Windows Forms 컨트롤 개발](how-to-develop-a-simple-windows-forms-control.md)를 재정의 하는 예를 살펴보았습니다는 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드. 다음 코드 조각은 샘플에서 가져온 것입니다.  
  
```vb  
Public Class FirstControl  
   Inherits Control  
  
   Public Sub New()  
   End Sub  
  
   Protected Overrides Sub OnPaint(e As PaintEventArgs)  
      ' Call the OnPaint method of the base class.  
      MyBase.OnPaint(e)  
      ' Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, New SolidBrush(ForeColor), RectangleF.op_Implicit(ClientRectangle))  
   End Sub  
End Class   
```  
  
```csharp  
public class FirstControl : Control {  
   public FirstControl() {}  
   protected override void OnPaint(PaintEventArgs e) {  
      // Call the OnPaint method of the base class.  
      base.OnPaint(e);  
      // Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, new SolidBrush(ForeColor), ClientRectangle);  
   }   
}   
```  
  
 <xref:System.Windows.Forms.PaintEventArgs> 클래스에 대 한 데이터가 포함 된 <xref:System.Windows.Forms.Control.Paint> 이벤트입니다. 다음 코드와 같이 두 개의 속성이 있습니다.  
  
```vb  
Public Class PaintEventArgs  
   Inherits EventArgs  
   ...  
   Public ReadOnly Property ClipRectangle() As System.Drawing.Rectangle  
      ...  
   End Property  
  
   Public ReadOnly Property Graphics() As System.Drawing.Graphics  
      ...  
   End Property   
   ...  
End Class  
```  
  
```csharp  
public class PaintEventArgs : EventArgs {  
...  
    public System.Drawing.Rectangle ClipRectangle {}  
    public System.Drawing.Graphics Graphics {}  
...  
}  
```  
  
 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 를 그릴 사각형 및 <xref:System.Windows.Forms.PaintEventArgs.Graphics%2A> 속성은 참조를 <xref:System.Drawing.Graphics> 개체입니다. 클래스는 <xref:System.Drawing?displayProperty=nameWithType> 네임 스페이스는 관리 되는 GDI +에서 새 Windows 그래픽 라이브러리의 기능에 대 한 액세스를 제공 하는 클래스입니다. <xref:System.Drawing.Graphics> 지점, 문자열, 선, 원호, 타원, 및 기타 많은 도형을 그릴 메서드가 개체입니다.  
  
 호출 하는 컨트롤을 해당 <xref:System.Windows.Forms.Control.OnPaint%2A> 해당 시각적 표시를 변경 해야 할 때마다 메서드. 이 메서드가 발생을 <xref:System.Windows.Forms.Control.Paint> 이벤트입니다.  
  
## <a name="see-also"></a>참고자료

- [이벤트](../../../standard/events/index.md)
- [Windows Forms 컨트롤 렌더링](rendering-a-windows-forms-control.md)
- [이벤트 정의](defining-an-event-in-windows-forms-controls.md)
