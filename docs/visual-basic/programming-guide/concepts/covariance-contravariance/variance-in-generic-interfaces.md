---
title: (Visual Basic) 제네릭 인터페이스의 가변성
ms.date: 07/20/2015
ms.assetid: cf4096d0-4bb3-45a9-9a6b-f01e29a60333
ms.openlocfilehash: 93e169f658a855e3b271e3e3affeadac5d7e5032
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64642390"
---
# <a name="variance-in-generic-interfaces-visual-basic"></a>(Visual Basic) 제네릭 인터페이스의 가변성
.NET Framework 4에서는 기존의 몇몇 제네릭 인터페이스에 대한 가변성 지원이 추가되었습니다. 가변성 지원은 이러한 인터페이스를 구현하는 클래스의 암시적 변환을 가능하게 합니다. 다음 인터페이스는 현재 variant입니다.  
  
- <xref:System.Collections.Generic.IEnumerable%601>(T는 공변(covariant)임)  
  
- <xref:System.Collections.Generic.IEnumerator%601>(T는 공변(covariant)임)  
  
- <xref:System.Linq.IQueryable%601>(T는 공변(covariant)임)  
  
- <xref:System.Linq.IGrouping%602>(`TKey` 및 `TElement`는 공변(covariant)임)  
  
- <xref:System.Collections.Generic.IComparer%601>(T는 반공변(contravariant)임)  
  
- <xref:System.Collections.Generic.IEqualityComparer%601>(T는 반공변(contravariant)임)  
  
- <xref:System.IComparable%601>(T는 반공변(contravariant)임)  
  
 공변성(covariance)은 메서드가 인터페이스의 제네릭 형식 매개 변수에 정의된 것보다 더 많은 수의 파생된 반환 형식을 갖도록 허용합니다. 공변성(covariance) 기능을 설명하려면 `IEnumerable(Of Object)` 및 `IEnumerable(Of String)`이라는 제네릭 인터페이스를 고려하세요. `IEnumerable(Of String)` 인터페이스는 `IEnumerable(Of Object)` 인터페이스를 상속하지 않습니다. 그러나 `String` 형식은 `Object` 형식을 상속하며, 경우에 따라 이러한 인터페이스의 개체를 서로 할당할 수 있습니다. 다음 코드 예제에서 이를 확인할 수 있습니다.  
  
```vb  
Dim strings As IEnumerable(Of String) = New List(Of String)  
Dim objects As IEnumerable(Of Object) = strings  
```  
  
 .NET Framework의 이전 버전에서는이 코드는 사용 하 여 Visual Basic에서 컴파일 오류가 발생 `Option Strict On`합니다. 그러나 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스는 공변(covariant) 이므로 이제 다음 예제와 같이 `objects` 대신 `strings`를 사용할 수 있습니다.  
  
 반공변성(Contravariance)은 메서드가 인터페이스의 제네릭 매개 변수에 지정된 것보다 더 적은 수의 파생된 형식의 인수 형식을 갖도록 허용합니다. 반공변성(contravariance)을 설명하기 위해, 사용자가 `BaseComparer` 클래스를 만들어 `BaseClass` 클래스의 인스턴스를 비교한다고 가정합니다. `BaseComparer` 클래스는 `IEqualityComparer(Of BaseClass)` 인터페이스를 구현합니다. <xref:System.Collections.Generic.IEqualityComparer%601> 인터페이스는 이제 반공변(contravariant)이므로 `BaseClass` 클래스를 상속하는 클래스의 인스턴스를 비교하는 데 `BaseComparer`를 사용할 수 있습니다. 다음 코드 예제에서 이를 확인할 수 있습니다.  
  
```vb  
' Simple hierarchy of classes.  
Class BaseClass  
End Class  
  
Class DerivedClass  
    Inherits BaseClass  
End Class  
  
' Comparer class.  
Class BaseComparer  
    Implements IEqualityComparer(Of BaseClass)  
  
    Public Function Equals1(ByVal x As BaseClass,  
                            ByVal y As BaseClass) As Boolean _  
                            Implements IEqualityComparer(Of BaseClass).Equals  
        Return (x.Equals(y))  
    End Function  
  
    Public Function GetHashCode1(ByVal obj As BaseClass) As Integer _  
        Implements IEqualityComparer(Of BaseClass).GetHashCode  
        Return obj.GetHashCode  
    End Function  
End Class  
Sub Test()  
    Dim baseComparer As IEqualityComparer(Of BaseClass) = New BaseComparer  
    ' Implicit conversion of IEqualityComparer(Of BaseClass) to   
    ' IEqualityComparer(Of DerivedClass).  
    Dim childComparer As IEqualityComparer(Of DerivedClass) = baseComparer  
End Sub  
```  
  
 더 많은 예제를 참조 하세요 [(Visual Basic)의 제네릭 컬렉션 용 인터페이스의 가변성 사용](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)합니다.  
  
 제네릭 인터페이스의 가변성은 참조 형식에 대해서만 지원됩니다. 값 형식은 가변성을 지원하지 않습니다. 정수는 값 형식으로 표시되므로 예를 들어 `IEnumerable(Of Integer)`를 `IEnumerable(Of Object)`로 암시적으로 변환할 수 없습니다.  
  
```vb  
Dim integers As IEnumerable(Of Integer) = New List(Of Integer)  
' The following statement generates a compiler error  
' with Option Strict On, because Integer is a value type.  
' Dim objects As IEnumerable(Of Object) = integers  
```  
  
 Variant 인터페이스를 구현하는 클래스는 여전히 비 variant라는 점에 유의해야 합니다. 예를 들어 <xref:System.Collections.Generic.List%601>는 공변(covariant) 인터페이스 <xref:System.Collections.Generic.IEnumerable%601>을 구현하지만 암시적으로 `List(Of Object)`를 `List(Of String)`으로 변환할 수 없습니다. 다음 코드 예제에서 이 내용을 보여 줍니다.  
  
```vb  
' The following statement generates a compiler error  
' because classes are invariant.  
' Dim list As List(Of Object) = New List(Of String)  
  
' You can use the interface object instead.  
Dim listObjects As IEnumerable(Of Object) = New List(Of String)  
```  
  
## <a name="see-also"></a>참고자료

- [제네릭 컬렉션용 인터페이스의 가변성 사용(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)
- [Variant 제네릭 인터페이스 만들기(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)
- [제네릭 인터페이스](../../../../standard/generics/interfaces.md)
- [대리자의 가변성(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
