---
title: Of 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Of
- vb.Of
- vb.of
helpviewer_keywords:
- Of keyword [Visual Basic]
- arguments [Visual Basic], data types
- constraints, Visual Basic generic types
- generic parameters
- generics [Visual Basic], constraints
- parameters [Visual Basic], type
- types [Visual Basic], generic
- parameters [Visual Basic], generic
- type parameters
- data type arguments
ms.assetid: 0db8f65c-65af-4089-ab7f-6fcfecb60444
ms.openlocfilehash: 880570c714292b0c11eef4e2cd4c4b410bb075f1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61784152"
---
# <a name="of-clause-visual-basic"></a>Of 절(Visual Basic)
소개는 `Of` 식별 하는 절을 *형식 매개 변수* 에 *제네릭* 클래스, 구조체, 인터페이스, 대리자 또는 프로시저. 제네릭 형식에 대 한 자세한 내용은 [Visual Basic의 제네릭 형식](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)합니다.  
  
## <a name="using-the-of-keyword"></a>사용 하는 키워드  
 다음 코드 예제에서는 `Of` 두 형식 매개 변수를 사용 하는 클래스의 윤곽선을 정의 하는 키워드입니다. 것 *제한* 는 `keyType` 매개 변수를 <xref:System.IComparable> 인터페이스를 사용 하는 코드를 구현 하는 형식 인수를 제공 해야 합니다 즉 <xref:System.IComparable>. 이 작업은 필요 있도록 합니다 `add` 프로시저를 호출할 수는 <xref:System.IComparable.CompareTo%2A?displayProperty=nameWithType> 메서드. 제약 조건에 대한 자세한 내용은 [Type List](../../../visual-basic/language-reference/statements/type-list.md)을 참조하세요.  
  
```  
Public Class Dictionary(Of entryType, keyType As IComparable)  
    Public Sub add(ByVal e As entryType, ByVal k As keyType)  
        Dim dk As keyType  
        If k.CompareTo(dk) = 0 Then  
        End If  
    End Sub  
    Public Function find(ByVal k As keyType) As entryType  
    End Function  
End Class  
```  
  
 위의 클래스 정의 완료 하는 경우에 다양 한을 생성할 수 있습니다 `dictionary` 에서 클래스입니다. 제공 하는 형식을 `entryType` 및 `keyType` 어떤 유형의 항목 클래스를 보유 하 고 각 항목에 연결 하는 키의 형식을 결정 합니다. 제공 해야는 제약 조건으로 인해 `keyType` 구현 하는 형식을 <xref:System.IComparable>합니다.  
  
 다음 코드 예제를 보유 하는 개체를 만듭니다 `String` 항목과 연결 된 `Integer` 각각 키입니다. `Integer` 구현 <xref:System.IComparable> 따라서에서 제약 조건을 만족 하 고 `keyType`입니다.  
  
```  
Dim d As New dictionary(Of String, Integer)  
```  
  
 `Of` 키워드는 다음 컨텍스트에서 사용할 수 있습니다.  
  
 [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Delegate 문](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>참고자료

- <xref:System.IComparable>
- [형식 목록](../../../visual-basic/language-reference/statements/type-list.md)
- [Visual Basic의 제네릭 형식](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)
- [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)
