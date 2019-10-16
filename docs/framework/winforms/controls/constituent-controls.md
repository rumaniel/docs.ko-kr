---
title: 구성 요소 컨트롤
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], constituent controls
- constituent controls [Windows Forms]
- user controls [Windows Forms], constituent controls
ms.assetid: 5565e720-198b-4bbd-a2bd-c447ba641798
ms.openlocfilehash: 522a1012fc7bdd54860b0538064ee073f7a761f7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918421"
---
# <a name="constituent-controls"></a>구성 요소 컨트롤
사용자 정의 컨트롤을 구성하는 컨트롤, 즉 *구성 요소컨트롤*은 사용자 지정 그래픽 렌더링을 수행할 때 사용 범위가 상대적으로 제한됩니다. 모든 Windows Forms 컨트롤은 자체 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드를 통해 자체 렌더링을 처리 합니다. 이 메서드는 protected로 선언되므로 개발자가 액세스할 수 없으며, 이에 따라 컨트롤을 그릴 때 실행되는 것을 막을 수 없습니다. 그러나 이러한 이유로 구성 요소 컨트롤의 모양에 적용되는 코드를 추가할 수 없는 것은 아닙니다. 이벤트 처리기를 추가하면 추가적 렌더링을 수행할 수 있습니다. 예를 들어 라는 <xref:System.Windows.Forms.UserControl> `MyButton`단추를 사용 하 여를 작성 한다고 가정 합니다. 에서 제공 <xref:System.Web.UI.WebControls.Button>하는 것 외에 추가로 렌더링 하려면 다음과 유사한 코드를 사용자 정의 컨트롤에 추가 합니다.  
  
```vb  
Public Sub MyPaint(ByVal sender as Object, e as PaintEventArgs) Handles _  
   MyButton.Paint  
   'Additional rendering code goes here  
End Sub  
```  
  
```csharp  
// Add the event handler to the button's Paint event.  
MyButton.Paint +=   
   new System.Windows.Forms.PaintEventHandler (this.MyPaint);  
// Create the custom painting method.  
protected void MyPaint (object sender,   
System.Windows.Forms.PaintEventArgs e)  
{  
   // Additional rendering code goes here.  
}  
```  
  
> [!NOTE]
> 과 <xref:System.Windows.Forms.TextBox>같은 일부 Windows Forms 컨트롤은 Windows에서 직접 그려집니다. 이러한 경우 메서드는 <xref:System.Windows.Forms.Control.OnPaint%2A> 호출 되지 않으므로 위의 예제는 호출 되지 않습니다.  
  
 이 경우 `MyButton.Paint` 이벤트가 실행될 때마다 실행되는 메서드를 만들어 사용자 정의 컨트롤에 추가적인 그래픽 표현을 추가합니다. 여기서는 `MyButton.OnPaint`가 실행되는 것을 막을 수 없으므로 사용자 지정 그리기뿐만 아니라 일반적으로 단추를 통해 수행되는 모든 그리기도 수행됩니다. GDI + 기술 및 사용자 지정 렌더링에 대한 자세한 내용은 [GDI+를 사용하여 그래픽 이미지 만들기](../advanced/how-to-create-graphics-objects-for-drawing.md)를 참조하세요. 고유한 컨트롤 표현을 제공하려면 상속된 컨트롤을 만들고 이 컨트롤에 필요한 사용자 지정 렌더링 코드를 작성하는 것이 가장 좋습니다. 자세한 내용은 [사용자가 그린 컨트롤](user-drawn-controls.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- [사용자가 그린 컨트롤](user-drawn-controls.md)
- [방법: 그리기를 위한 그래픽 개체 만들기](../advanced/how-to-create-graphics-objects-for-drawing.md)
- [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)
