---
title: "'System.Nullable(Of T)'의 메서드는 'AddressOf' 연산자의 피연산자로 사용할 수 없습니다."
ms.date: 07/20/2015
f1_keywords:
- vbc32126
- bc32126
helpviewer_keywords:
- BC32126
ms.assetid: 2325668b-e2ad-40ee-a1ec-30450236c20d
ms.openlocfilehash: e55e561fa20a3740d352537958681b0a66fc381e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592036"
---
# <a name="methods-of-systemnullableof-t-cannot-be-used-as-operands-of-the-addressof-operator"></a>'System.Nullable(Of T)'의 메서드는 'AddressOf' 연산자의 피연산자로 사용할 수 없습니다.
문을 사용 하는 `AddressOf` 의 프로시저를 나타내는 피연산자와 연산자를 <xref:System.Nullable%601> 구조입니다.  
  
 **오류 ID:** BC32126  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 프로시저 이름을 대체 합니다 `AddressOf` 소속 된 피연산자를 사용 하 여 절 <xref:System.Nullable%601>.  
  
- 메서드를 래핑하는 클래스를 작성 <xref:System.Nullable%601> 사용 하려는. 다음 예제에서는 `NullableWrapper` 라는 새 메서드를 정의 하는 클래스 `GetValueOrDefault`합니다. 이 새 메서드 멤버인 아니므로 <xref:System.Nullable%601>에 적용할 수 있습니다 `nullInstance`, nullable 형식에 대 한 인수에 인스턴스의 `AddressOf`합니다.  
  
```vb  
Module Module1  
  
    Delegate Function Deleg() As Integer  
  
    Sub Main()  
        Dim nullInstance As New Nullable(Of Integer)(1)  
  
        Dim del As Deleg  
  
        ' GetValueOrDefault is a method of the Nullable generic  
        ' type. It cannot be used as an operand of AddressOf.  
        ' del = AddressOf nullInstance.GetValueOrDefault  
  
        ' The following line uses the GetValueOrDefault method  
        ' defined in the NullableWrapper class.  
        del = AddressOf (New NullableWrapper(  
            Of Integer)(nullInstance)).GetValueOrDefault  
  
        Console.WriteLine(del.Invoke())  
    End Sub  
  
    Class NullableWrapper(Of T As Structure)  
        Private m_Value As Nullable(Of T)  
  
        Sub New(ByVal Value As Nullable(Of T))  
            m_Value = Value  
        End Sub  
  
        Public Function GetValueOrDefault() As T  
            Return m_Value.Value  
        End Function  
    End Class  
End Module  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Nullable%601>
- [AddressOf 연산자](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Nullable 값 형식](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
- [Visual Basic의 제네릭 형식](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
