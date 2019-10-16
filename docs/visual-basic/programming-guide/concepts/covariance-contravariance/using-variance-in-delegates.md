---
title: 대리자의 가변성 사용 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 7b5c20f1-6416-46a3-94b6-f109c31c842c
ms.openlocfilehash: ebba7e862e1b4677d9438aa301ef2b713fba3712
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169074"
---
# <a name="using-variance-in-delegates-visual-basic"></a>대리자의 가변성 사용 (Visual Basic)

메서드를 대리자에 할당하면 *공변성(covariance)* 및 *반공변성(Contravariance)* 은 대리자 형식과 메서드 시그니처의 일치를 확인하는 유연성을 제공합니다. 공변성(covariance)은 메서드가 대리자에 정의된 것보다 더 많은 수의 파생된 형식을 반환하도록 허용합니다. 반공변성(contravariance)은 메서드가 대리자 형식보다 더 적은 수의 파생된 매개 변수 형식을 갖도록 허용합니다.

## <a name="example-1-covariance"></a>예제 1: 공변성

### <a name="description"></a>Description

이 예제에서는 대리자를 대리자 시그니처의 반환 형식에서 파생된 반환 형식이 있는 메서드와 함께 사용하는 방법을 보여 줍니다. `DogsHandler`에서 반환된 데이터 형식은 `Dogs`이고, 이 형식은 대리자에 정의된 `Mammals` 형식에서 파생됩니다.

### <a name="code"></a>코드

```vb
Class Mammals
End Class

Class Dogs
    Inherits Mammals
End Class
Class Test
    Public Delegate Function HandlerMethod() As Mammals
    Public Shared Function MammalsHandler() As Mammals
        Return Nothing
    End Function
    Public Shared Function DogsHandler() As Dogs
        Return Nothing
    End Function
    Sub Test()
        Dim handlerMammals As HandlerMethod = AddressOf MammalsHandler
        ' Covariance enables this assignment.
        Dim handlerDogs As HandlerMethod = AddressOf DogsHandler
    End Sub
End Class
```

## <a name="example-2-contravariance"></a>예제 2: 반공변성(contravariance)

### <a name="description"></a>Description

이 예제에서는 대리자를 대리자 시그니처 매개 변수 형식의 기본 형식을 사용하는 매개 변수를 가지고 있는 메서드와 함께 사용하는 방법을 보여 줍니다. 반공변성(contravariance)에서는 별도의 여러 처리기 대신 하나의 이벤트 처리기를 사용할 수 있습니다. 다음 예제는 두 개의 대리자를 사용합니다.

- [Button.KeyDown](xref:System.Windows.Forms.Control.KeyDown) 이벤트의 시그니처를 정의하는 <xref:System.Windows.Forms.KeyEventHandler> 대리자. 해당 시그니처는 다음과 같습니다.

   ```vb
   Public Delegate Sub KeyEventHandler(sender As Object, e As KeyEventArgs)
   ```

- [Button.MouseClick](xref:System.Windows.Forms.Control.MouseDown) 이벤트의 시그니처를 정의하는 <xref:System.Windows.Forms.MouseEventHandler> 대리자. 해당 시그니처는 다음과 같습니다.

   ```vb
   Public Delegate Sub MouseEventHandler(sender As Object, e As MouseEventArgs)
   ```

예제에서는 <xref:System.EventArgs> 매개 변수를 사용하여 이벤트 처리기를 정의하고 이를 사용하여 `Button.KeyDown` 및 `Button.MouseClick` 이벤트를 모두 처리합니다. <xref:System.EventArgs>는 <xref:System.Windows.Forms.KeyEventArgs> 및 <xref:System.Windows.Forms.MouseEventArgs>의 기본 형식이므로 이 작업을 수행할 수 있습니다.

### <a name="code"></a>코드

```vb
' Event handler that accepts a parameter of the EventArgs type.
Private Sub MultiHandler(ByVal sender As Object,
                         ByVal e As System.EventArgs)
    Label1.Text = DateTime.Now
End Sub

Private Sub Form1_Load(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles MyBase.Load

    ' You can use a method that has an EventArgs parameter,
    ' although the event expects the KeyEventArgs parameter.
    AddHandler Button1.KeyDown, AddressOf MultiHandler

    ' You can use the same method
    ' for the event that expects the MouseEventArgs parameter.
    AddHandler Button1.MouseClick, AddressOf MultiHandler
End Sub
```

## <a name="see-also"></a>참고자료

- [대리자의 가변성(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
- [Func 및 Action 제네릭 대리자에 가변성 사용(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
