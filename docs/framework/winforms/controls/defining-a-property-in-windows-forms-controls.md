---
title: Windows Forms 컨트롤에서 속성 정의
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties [Windows Forms], defining in code
- custom controls [Windows Forms], defining properties in code
ms.assetid: c2eb8277-a842-4d99-89a9-647b901a0434
ms.openlocfilehash: a641b1e7565842a1edf6aeec88bdc37ee0786ab4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969125"
---
# <a name="defining-a-property-in-windows-forms-controls"></a>Windows Forms 컨트롤에서 속성 정의
속성의 개요는 [속성 개요](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120))를 참조하세요. 속성을 정의할 때 다음과 같은 몇 가지 주요 고려 사항이 있습니다.  
  
- 정의한 속성에 특성을 적용해야 합니다. 특성은 디자이너가 속성을 표시하는 방법을 지정합니다. 자세한 내용은 [구성 요소의 디자인 타임 특성](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/tk67c2t8(v=vs.120))을 참조하세요.  
  
- 속성을 변경 하 여 컨트롤의 시각적 표시에 영향을 주는 경우 <xref:System.Windows.Forms.Control.Invalidate%2A> `set` 접근자에서 컨트롤이 <xref:System.Windows.Forms.Control>상속 하는 메서드를 호출 합니다. <xref:System.Windows.Forms.Control.Invalidate%2A>그런 다음는 컨트롤 <xref:System.Windows.Forms.Control.OnPaint%2A> 을 다시 그리는 메서드를 호출 합니다. 를 <xref:System.Windows.Forms.Control.Invalidate%2A> 여러 번 호출 하면 효율성을 위해에 <xref:System.Windows.Forms.Control.OnPaint%2A> 대 한 단일 호출이 발생 합니다.  
  
- .NET Framework 클래스 라이브러리는 정수, 10진수 숫자, 부울 값 등과 같은 일반적인 데이터 형식에 대해 형식 변환기를 제공합니다. 형식 변환기의 목적은 일반적으로 문자열을 값으로 변환하도록 제공합니다(문자열 데이터에서 다른 데이터 형식으로). 일반적인 데이터 형식은 값을 문자열로 변환하고 문자열을 적절한 데이터 형식으로 변환하는 기본 형식 변환기와 연결됩니다. 사용자 지정(즉, 비표준) 데이터 형식인 속성을 정의하는 경우 형식 변환기를 지정하는 특성을 적용하여 해당 속성과 연결해야 합니다. 특성을 사용하여 사용자 지정 UI 형식 편집기를 속성과 연결할 수 있습니다. UI 형식 편집기는 속성이나 데이터 형식을 편집하는 사용자 인터페이스를 제공합니다. 색 선택은 UI 형식 편집기의 예입니다. 이 항목의 끝에 특성의 예가 제공됩니다.  
  
    > [!NOTE]
    > 사용자 지정 속성에 형식 변환기 또는 UI 형식 편집기를 사용할 수 없는 경우 [디자인 타임 지원 확장](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))에 설명된 대로 구현할 수 있습니다.  
  
 다음 코드 조각은 사용자 지정 컨트롤 `FlashTrackBar`에 대해 `EndColor`이라는 사용자 지정 속성을 정의합니다.  
  
```vb  
Public Class FlashTrackBar  
   Inherits Control  
   ...  
   ' Private data member that backs the EndColor property.  
   Private _endColor As Color = Color.LimeGreen  
  
   ' The Category attribute tells the designer to display  
   ' it in the Flash grouping.   
   ' The Description attribute provides a description of  
   ' the property.   
   <Category("Flash"), _  
   Description("The ending color of the bar.")>  _  
   Public Property EndColor() As Color  
      ' The public property EndColor accesses _endColor.  
      Get  
         Return _endColor  
      End Get  
      Set  
         _endColor = value  
         If Not (baseBackground Is Nothing) And showGradient Then  
            baseBackground.Dispose()  
            baseBackground = Nothing  
         End If  
         ' The Invalidate method calls the OnPaint method, which redraws    
         ' the control.  
         Invalidate()  
      End Set  
   End Property  
   ...  
End Class  
```  
  
```csharp  
public class FlashTrackBar : Control {  
   ...  
   // Private data member that backs the EndColor property.  
   private Color endColor = Color.LimeGreen;  
   // The Category attribute tells the designer to display  
   // it in the Flash grouping.   
   // The Description attribute provides a description of  
   // the property.   
   [  
   Category("Flash"),  
   Description("The ending color of the bar.")  
   ]  
   // The public property EndColor accesses endColor.  
   public Color EndColor {  
      get {  
         return endColor;  
      }  
      set {  
         endColor = value;  
         if (baseBackground != null && showGradient) {  
            baseBackground.Dispose();  
            baseBackground = null;  
         }  
         // The Invalidate method calls the OnPaint method, which redraws   
         // the control.  
         Invalidate();  
      }  
   }  
   ...  
}  
```  
  
 다음 코드 조각은 형식 변환기 및 UI 형식 편집기를 속성 `Value`과 연결합니다. 이 경우 `Value` 에는 정수 이며 기본 형식 변환기가 있지만이 특성은 디자이너에서이를 백분율로 표시할 수 있도록`FlashTrackBarValueConverter`하는 사용자 지정 형식 변환기 ()를 적용 합니다 <xref:System.ComponentModel.TypeConverterAttribute> . UI 형식 편집기인 `FlashTrackBarValueEditor`은 백분율을 시각적으로 표시할 수 있습니다. 이 예제에서는 <xref:System.ComponentModel.TypeConverterAttribute> 또는 <xref:System.ComponentModel.EditorAttribute> 특성으로 지정 된 형식 변환기 또는 편집기가 기본 변환기를 재정의 하는 방법도 보여 줍니다.  
  
```vb  
<Category("Flash"), _  
TypeConverter(GetType(FlashTrackBarValueConverter)), _  
Editor(GetType(FlashTrackBarValueEditor), _  
GetType(UITypeEditor)), _  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")>  _  
Public ReadOnly Property Value() As Integer  
...  
End Property  
```  
  
```csharp  
[  
Category("Flash"),   
TypeConverter(typeof(FlashTrackBarValueConverter)),  
Editor(typeof(FlashTrackBarValueEditor), typeof(UITypeEditor)),  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")  
]  
public int Value {  
...  
}  
```  
  
## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤의 속성](properties-in-windows-forms-controls.md)
- [ShouldSerialize 및 Reset 메서드를 사용하여 기본값 정의](defining-default-values-with-the-shouldserialize-and-reset-methods.md)
- [속성 변경 이벤트](property-changed-events.md)
- [Windows Forms 컨트롤의 특성](attributes-in-windows-forms-controls.md)
