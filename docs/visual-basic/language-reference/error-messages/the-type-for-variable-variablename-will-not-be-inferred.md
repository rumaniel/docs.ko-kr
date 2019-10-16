---
title: "'<variablename>' 변수가 바깥쪽 범위의 필드에 바인딩되어 있으므로 변수의 형식을 유추할 수 없습니다."
ms.date: 07/20/2015
f1_keywords:
- vbc42110
- bc42110
helpviewer_keywords:
- BC42110
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
ms.openlocfilehash: e56529919945558df178e18a83a895a79bfe4919
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512718"
---
# <a name="the-type-for-variable-variablename-will-not-be-inferred-because-it-is-bound-to-a-field-in-an-enclosing-scope"></a>'\<Variablename > ' 변수의 형식은 바깥쪽 범위의 필드에 바인딩되어 있으므로 유추 되지 않습니다.

'\<Variablename > ' 변수의 형식은 바깥쪽 범위의 필드에 바인딩되어 있으므로 유추 되지 않습니다. '\<Variablename > '의 이름을 변경 하거나 정규화 된 이름 (예: ' variablename ' 또는 ' variablename ')을 사용 하십시오.

코드의 루프 제어 변수 이름이 클래스 또는 다른 바깥쪽 범위의 필드와 동일 합니다. 제어 변수는 `As` 절 없이 사용 되므로 바깥쪽 범위의 필드에 바인딩되고 컴파일러는 새 변수를 만들거나 해당 유형을 유추 하지 않습니다.

다음 예제 `Index`에서 `For` 문의 제어 변수는 `Customer` 클래스의 `Index` 필드에 바인딩됩니다. 컴파일러는 컨트롤 변수에 `Index` 대 한 새 변수를 만들거나 해당 형식을 유추 하지 않습니다.

```vb
Class Customer

    ' The class has a field named Index.
    Private Index As Integer

    Sub Main()

    ' The following line will raise this warning.
        For Index = 1 To 10
            ' ...
        Next

    End Sub
End Class
```

이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.

**오류 ID:** BC42110

### <a name="to-address-this-warning"></a>이 경고를 해결하려면

- 해당 이름을 클래스의 필드 이름이 아닌 식별자로 변경 하 여 루프 제어 변수를 로컬으로 만듭니다.

  ```vb
  For I = 1 To 10
  ```

- 변수 이름에 접두사로 `Me.` loop 제어 변수가 클래스 필드에 바인딩되도록 명시 합니다.

  ```vb
  For Me.Index = 1 To 10
  ```

- 지역 형식 유추를 사용 하는 대신 `As` 절을 사용 하 여 루프 제어 변수의 형식을 지정 합니다.

  ```vb
  For Index As Integer = 1 To 10
  ```

## <a name="example"></a>예제
 다음 코드에서는 첫 번째 수정이 적용 된 이전 예제를 보여 줍니다.

```vb
Class Customer

    ' The class has a field named Index.
    Private Index As Integer

    Sub Main()

        For I = 1 To 10
            ' ...
        Next

    End Sub
End Class
```

## <a name="see-also"></a>참고자료

- [Option Infer 문](../../../visual-basic/language-reference/statements/option-infer-statement.md)
- [For Each...Next 문](../../../visual-basic/language-reference/statements/for-each-next-statement.md)
- [For...Next 문](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [방법: 개체의 현재 인스턴스를 참조 하세요.](../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)
- [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Me, My, MyBase 및 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
