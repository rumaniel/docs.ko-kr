---
title: 익명 형식이 다른 필드를 초기화하는 데 사용되는 필드를 포함하고 있으므로 식 트리로 변환할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- bc36548
- vbc36548
helpviewer_keywords:
- BC36548
ms.assetid: 27de068f-080e-4160-86bf-1ec23fd1925a
ms.openlocfilehash: ba14c0cd8781b8771ac8b746e3efec29a457294a
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701185"
---
# <a name="cannot-convert-anonymous-type-to-expression-tree-because-it-contains-a-field-that-is-used-in-the-initialization-of-another-field"></a>익명 형식이 다른 필드를 초기화하는 데 사용되는 필드를 포함하고 있으므로 식 트리로 변환할 수 없습니다.
익명 형식의 속성 하나를 사용 하 여 익명 형식의 다른 속성을 초기화 하는 경우 컴파일러는 익명의 식 트리로의 변환을 허용 하지 않습니다. 예를 들어 다음 코드에서 `Prop1`은 초기화 목록에 선언 된 다음 `Prop2`의 초기 값으로 사용 됩니다.  
  
```vb  
Module M2  
  
    Sub ExpressionExample(Of T)(ByVal x As Expressions.Expression(Of Func(Of T)))  
    End Sub  
  
    Sub Main()  
        ' The following line causes the error.  
        ' ExpressionExample(Function() New With {.Prop1 = 2, .Prop2 = .Prop1})  
  
    End Sub  
End Module  
```  
  
 **오류 ID:** BC36548  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- @No__t-0에 대 한 초기 값을 지역 변수에 할당 합니다. 다음 코드와 같이 `Prop1` 및 `Prop2` 모두에 해당 변수를 할당 합니다.  
  
    ```vb  
    Sub Main()  
  
        Dim temp = 2  
        ExpressionExample(Function() New With {.Prop1 = temp, .Prop2 = temp})  
  
    End Sub  
    ```  
  
## <a name="see-also"></a>참조

- [익명 형식 (Visual Basic)](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [식 트리(Visual Basic)](../../programming-guide/concepts/expression-trees/index.md)
- [방법: 식 트리를 사용 하 여 동적 쿼리 (Visual Basic) @no__t 빌드-0
