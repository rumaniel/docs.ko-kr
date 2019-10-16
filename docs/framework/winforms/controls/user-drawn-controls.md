---
title: 사용자가 그린 컨트롤
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], user-drawn
- OnPaint method [Windows Forms]
- user-drawn controls [Windows Forms]
ms.assetid: 034af4b5-457f-4160-a937-22891817faa8
ms.openlocfilehash: 50036f5bef323368b4970a080ca7a70cf94252d6
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966482"
---
# <a name="user-drawn-controls"></a>사용자가 그린 컨트롤
.NET Framework는 사용자 고유의 컨트롤을 쉽게 개발할 수 있는 기능을 제공 합니다. 코드를 사용 하 여 바인딩된 표준 컨트롤 집합인 사용자 정의 컨트롤을 만들거나 처음부터 직접 컨트롤을 디자인할 수 있습니다. 상속을 사용 하 여 기존 컨트롤에서 상속 하 고 해당 내재 된 기능에를 추가 하는 컨트롤을 만들 수도 있습니다. 사용 하는 방법에 관계 없이 .NET Framework는 사용자가 만드는 모든 컨트롤에 대 한 사용자 지정 그래픽 인터페이스를 그리는 기능을 제공 합니다.  
  
 컨트롤의 그리기는 컨트롤 <xref:System.Windows.Forms.Control.OnPaint%2A> 의 메서드에서 코드를 실행 하 여 수행 됩니다. <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드의 단일 인수는 컨트롤을 렌더링 하 <xref:System.Windows.Forms.PaintEventArgs> 는 데 필요한 모든 정보 및 기능을 제공 하는 개체입니다. 는 <xref:System.Windows.Forms.PaintEventArgs> 컨트롤의 렌더링에 사용 되는 두 개의 보안 주체 개체를 속성으로 제공 합니다.  
  
- <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>object-그릴 컨트롤의 부분을 나타내는 사각형입니다. 이는 컨트롤의 그리기 방법에 따라 전체 컨트롤 또는 컨트롤의 일부일 수 있습니다.  
  
- <xref:System.Drawing.Graphics>개체-컨트롤을 그리는 데 필요한 기능을 제공 하는 몇 가지 그래픽 지향 개체와 메서드를 캡슐화 합니다.  
  
 <xref:System.Drawing.Graphics> 개체 및 사용 [방법에 대 한 자세한 내용은 방법: 그리기](../advanced/how-to-create-graphics-objects-for-drawing.md)를 위한 그래픽 개체를 만듭니다.  
  
 이벤트 <xref:System.Windows.Forms.Control.OnPaint%2A> 는 화면에서 컨트롤을 그리거나 새로 고칠 때마다 발생 하 고, 개체는 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 그리기가 수행 되는 사각형을 나타냅니다. 전체 컨트롤을 새로 고쳐야 하는 경우은 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 전체 컨트롤의 크기를 나타냅니다. 그러나 컨트롤의 일부만 새로 고쳐야 하는 경우 개체는 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 다시 그려야 하는 영역만을 나타냅니다. 이러한 경우의 예는 컨트롤이 사용자 인터페이스의 다른 컨트롤이 나 폼에 의해 부분적으로 가려져 있는 경우입니다.  
  
 <xref:System.Windows.Forms.Control> 클래스에서 상속 하는 경우에는 메서드를 <xref:System.Windows.Forms.Control.OnPaint%2A> 재정의 하 고 내에서 그래픽 렌더링 코드를 제공 해야 합니다. 사용자 정의 컨트롤이 나 상속 된 컨트롤에 사용자 지정 그래픽 인터페이스를 제공 하려는 경우 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드를 재정의 하 여 수행할 수도 있습니다. 예제는 다음과 같습니다.  
  
```vb  
Protected Overrides Sub OnPaint(ByVal e As PaintEventArgs)  
   ' Call the OnPaint method of the base class.  
   MyBase.OnPaint(e)  
  
   ' Declare and instantiate a drawing pen.  
   Using myPen As System.Drawing.Pen = New System.Drawing.Pen(Color.Aqua)  
      ' Draw an aqua rectangle in the rectangle represented by the control.  
      e.Graphics.DrawRectangle(myPen, New Rectangle(Me.Location, Me.Size))  
   End Using
End Sub  
```  
  
```csharp  
protected override void OnPaint(PaintEventArgs e)  
{  
   // Call the OnPaint method of the base class.  
   base.OnPaint(e);  
  
   // Declare and instantiate a new pen.  
   using (System.Drawing.Pen myPen = new System.Drawing.Pen(Color.Aqua))  
   {
      // Draw an aqua rectangle in the rectangle represented by the control.  
      e.Graphics.DrawRectangle(myPen, new Rectangle(this.Location,   
         this.Size));  
   }
}  
```  
  
 앞의 예제에서는 매우 간단한 그래픽 표현으로 컨트롤을 렌더링 하는 방법을 보여 줍니다. 기본 클래스의 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드를 호출 하 고, 그릴 개체를 <xref:System.Drawing.Pen> 만든 다음, 마지막으로 컨트롤의 <xref:System.Windows.Forms.Control.Location%2A> 및 <xref:System.Windows.Forms.Control.Size%2A> 에 의해 결정 된 사각형에 타원을 그립니다. 대부분의 렌더링 코드는이 보다 훨씬 복잡 하지만이 예제에서는 <xref:System.Drawing.Graphics> <xref:System.Windows.Forms.PaintEventArgs> 개체에 포함 된 개체를 사용 하는 방법을 보여 줍니다. 또는 <xref:System.Windows.Forms.UserControl> <xref:System.Windows.Forms.Control.OnPaint%2A> 와 같이 그래픽 표현이 이미 있는 클래스에서 상속 하는 경우 해당 표현을 렌더링에 통합 하지 않으려는 경우 기본 클래스의를 호출 하면 안 됩니다. <xref:System.Windows.Forms.Button> 방법이.  
  
 컨트롤의 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드에 있는 코드는 컨트롤을 처음 그릴 때 그리고 새로 고쳐질 때마다 실행 됩니다. 크기를 조정할 때마다 컨트롤을 다시 그리도록 하려면 컨트롤의 생성자에 다음 줄을 추가 합니다.  
  
```vb  
SetStyle(ControlStyles.ResizeRedraw, True)  
```  
  
```csharp  
SetStyle(ControlStyles.ResizeRedraw, true);  
```  
  
> [!NOTE]
> 사각형이 아닌 컨트롤을 구현 하려면 속성을사용합니다.<xref:System.Windows.Forms.Control.Region%2A?displayProperty=nameWithType>  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.Region%2A>
- <xref:System.Windows.Forms.ControlStyles>
- <xref:System.Drawing.Graphics>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- <xref:System.Windows.Forms.PaintEventArgs>
- [방법: 그리기를 위한 그래픽 개체 만들기](../advanced/how-to-create-graphics-objects-for-drawing.md)
- [구성 요소 컨트롤](constituent-controls.md)
- [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)
