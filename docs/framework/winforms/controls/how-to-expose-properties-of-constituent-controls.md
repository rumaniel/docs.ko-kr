---
title: '방법: Constituent 컨트롤의 속성 공개'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- user controls [Windows Forms], exposing constituent controls
- controls [Windows Forms], constituent
- custom controls [Windows Forms], exposing properties
- constituent controls
ms.assetid: 5c1ec98b-aa48-4823-986e-4712551cfdf1
ms.openlocfilehash: f006e42771a5ecc71f6a508fd78d0e2dd8f2d2f2
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015860"
---
# <a name="how-to-expose-properties-of-constituent-controls"></a>방법: Constituent 컨트롤의 속성 공개
복합 컨트롤을 구성 하는 컨트롤을 *구성 요소 컨트롤*이라고 합니다. 이러한 컨트롤은 일반적으로 private으로 선언 되므로 개발자가 액세스할 수 없습니다. 이러한 컨트롤의 속성을 이후 사용자가 사용할 수 있게 하려면 사용자에 게 노출 해야 합니다. 구성 컨트롤의 속성은 사용자 정의 컨트롤에서 속성을 만들고 해당 속성의 `get` 및 `set` 접근자를 사용 하 여 구성 요소 컨트롤의 private 속성에 변경 내용을 적용 하 여 노출 됩니다.

 이라는 `MyButton`구성 단추가 있는 가상의 사용자 정의 컨트롤을 사용 하는 것이 좋습니다. 이 예제에서 사용자가 `ConstituentButtonBackColor` 속성을 요청 하면의 <xref:System.Windows.Forms.Control.BackColor%2A> `MyButton` 속성에 저장 된 값이 전달 됩니다. 사용자가이 속성에 값을 할당 하면 <xref:System.Windows.Forms.Control.BackColor%2A> 해당 값이의 `MyButton` 속성에 자동으로 전달 되 고 `set` `MyButton`코드가 실행 되어 색이 변경 됩니다.

 다음 예제에서는 구성 단추의 <xref:System.Windows.Forms.Control.BackColor%2A> 속성을 노출 하는 방법을 보여 줍니다.

```vb
Public Property ButtonColor() as System.Drawing.Color
   Get
      Return MyButton.BackColor
   End Get
   Set(Value as System.Drawing.Color)
      MyButton.BackColor = Value
   End Set
End Property
```

```csharp
public Color ButtonColor
{
   get
   {
      return(myButton.BackColor);
   }
   set
   {
      myButton.BackColor = value;
   }
}
```

### <a name="to-expose-a-property-of-a-constituent-control"></a>구성 컨트롤의 속성을 노출 하려면

1. 사용자 정의 컨트롤에 대 한 공용 속성을 만듭니다.

2. 속성의 `get` 섹션에서 노출 하려는 속성의 값을 검색 하는 코드를 작성 합니다.

3. 속성의 `set` 섹션에서 속성의 값을 구성 요소 컨트롤의 노출 된 속성에 전달 하는 코드를 작성 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.UserControl>
- [Windows Forms 컨트롤의 속성](properties-in-windows-forms-controls.md)
- [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)
