---
title: 대리자의 가변성 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 38e9353f-74f8-4211-a8f0-7a495414df4a
ms.openlocfilehash: 0c52fd3fb36162de16a91a85088018f4f579611c
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69664346"
---
# <a name="variance-in-delegates-visual-basic"></a>대리자의 가변성 (Visual Basic)

.NET Framework 3.5에는 및 Visual Basic의 C# 모든 대리자에서 메서드 시그니처와 일치 하는 대리자 형식을 사용 하기 위한 가변성 지원이 도입 되었습니다. 즉, 일치하는 시그니처가 있는 메서드만이 아니라 더 많은 파생된 형식(공변성(covariance))을 반환하는 메서드 또는 대리자 형식에 지정된 것보다 더 적은 수의 파생된 형식(반공변성(contravariance))을 가지고 있는 매개 변수를 수락하는 메서드도 대리자에 할당할 수 있습니다. 여기에는 제네릭 및 비 제네릭 대리자가 모두 포함됩니다.

다음과 같이 두 개의 클래스 및 두 개의 대리자(제네릭 및 비 제네릭)를 가지고 있는 코드를 예로 들어보겠습니다.

```vb
Public Class First
End Class

Public Class Second
    Inherits First
End Class

Public Delegate Function SampleDelegate(ByVal a As Second) As First
Public Delegate Function SampleGenericDelegate(Of A, R)(ByVal a As A) As R
```

`SampleDelegate` 또는 `SampleDelegate(Of A, R)` 형식의 대리자를 만들 때 다음 메서드 중 하나를 할당할 수 있습니다.

```vb
' Matching signature.
Public Shared Function ASecondRFirst(
    ByVal second As Second) As First
    Return New First()
End Function

' The return type is more derived.
Public Shared Function ASecondRSecond(
    ByVal second As Second) As Second
    Return New Second()
End Function

' The argument type is less derived.
Public Shared Function AFirstRFirst(
    ByVal first As First) As First
    Return New First()
End Function

' The return type is more derived
' and the argument type is less derived.
Public Shared Function AFirstRSecond(
    ByVal first As First) As Second
    Return New Second()
End Function
```

다음 코드 예제에서는 메서드 시그니처 및 대리자 형식 사이의 암시적 변환을 보여 줍니다.

```vb
' Assigning a method with a matching signature
' to a non-generic delegate. No conversion is necessary.
Dim dNonGeneric As SampleDelegate = AddressOf ASecondRFirst
' Assigning a method with a more derived return type
' and less derived argument type to a non-generic delegate.
' The implicit conversion is used.
Dim dNonGenericConversion As SampleDelegate = AddressOf AFirstRSecond

' Assigning a method with a matching signature to a generic delegate.
' No conversion is necessary.
Dim dGeneric As SampleGenericDelegate(Of Second, First) = AddressOf ASecondRFirst
' Assigning a method with a more derived return type
' and less derived argument type to a generic delegate.
' The implicit conversion is used.
Dim dGenericConversion As SampleGenericDelegate(Of Second, First) = AddressOf AFirstRSecond
```

더 많은 예제는 [대리자에서 가변성 사용 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md) 및 [Func 및 Action 제네릭 대리자에 가변성 사용 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)을 참조 하세요.

## <a name="variance-in-generic-type-parameters"></a>제네릭 형식 매개 변수에서의 가변성

.NET Framework 4 이상에서, 형식이에서 요구 하는 대로 서로 상속 되는 경우 제네릭 형식 매개 변수로 지정 된 다른 형식의 제네릭 대리자를 서로 할당할 수 있도록 대리자 간의 암시적 변환을 사용 하도록 설정할 수 있습니다. 반대로.

암시적 변환을 사용하도록 설정하려면 `in` 및 `out` 키워드를 사용하여 대리자에서 제네릭 매개 변수를 공변(covariant) 또는 반공변(contravariant)으로 선언해야 합니다.

다음 코드 예제에서는 공변(covariant) 제네릭 형식 매개 변수가 있는 대리자를 만드는 방법을 보여 줍니다.

```vb
' Type T is declared covariant by using the out keyword.
Public Delegate Function SampleGenericDelegate(Of Out T)() As T
Sub Test()
    Dim dString As SampleGenericDelegate(Of String) = Function() " "
    ' You can assign delegates to each other,
    ' because the type T is declared covariant.
    Dim dObject As SampleGenericDelegate(Of Object) = dString
End Sub
```

메서드 시그니처를 대리자 형식과 일치시키는 용도로만 가변성 지원을 사용하고 `in` 및 `out` 키워드를 사용하지 않는 경우, 대리자를 동일한 람다 식 또는 메서드로 인스턴스화할 수는 있지만 한 대리자를 다른 대리자에 할당할 수는 없는 경우가 더러 있습니다.

다음 코드 예제 `SampleGenericDelegate(Of String)` 에서는를 상속 `Object`하지만 `String` 는로 `SampleGenericDelegate(Of Object)`명시적으로 변환할 수 없습니다. `T` 제네릭 매개 변수를 `out` 키워드로 표시하면 이 문제를 수정할 수 있습니다.

```vb
Public Delegate Function SampleGenericDelegate(Of T)() As T
Sub Test()
    Dim dString As SampleGenericDelegate(Of String) = Function() " "

    ' You can assign the dObject delegate
    ' to the same lambda expression as dString delegate
    ' because of the variance support for
    ' matching method signatures with delegate types.
    Dim dObject As SampleGenericDelegate(Of Object) = Function() " "

    ' The following statement generates a compiler error
    ' because the generic type T is not marked as covariant.
    ' Dim dObject As SampleGenericDelegate(Of Object) = dString

End Sub
```

### <a name="generic-delegates-that-have-variant-type-parameters-in-the-net-framework"></a>.NET Framework에 Variant 형식 매개 변수를 가지고 있는 제네릭 대리자

.NET Framework 4에는 기존의 몇몇 제네릭 대리자에서 제네릭 형식 매개 변수에 대한 가변성 지원이 추가되었습니다.

- <xref:System> 네임스페이스의 `Action` 대리자(예: <xref:System.Action%601> 및 <xref:System.Action%602>)

- <xref:System> 네임스페이스의 `Func` 대리자(예: <xref:System.Func%601> 및 <xref:System.Func%602>)

- <xref:System.Predicate%601> 대리자

- <xref:System.Comparison%601> 대리자

- <xref:System.Converter%602> 대리자

자세한 내용 및 예제는 [Func 및 Action 제네릭 대리자에 가변성 사용 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)을 참조 하세요.

### <a name="declaring-variant-type-parameters-in-generic-delegates"></a>제네릭 대리자에서 Variant 형식 매개 변수 선언

제네릭 대리자가 공변(covariant) 또는 반공변(contravariant) 제네릭 형식 매개 변수를 가지고 있는 경우 이를 *variant 제네릭 대리자*라고 할 수 있습니다.

`out` 키워드를 사용하여 제네릭 대리자에서 제네릭 형식 매개 변수를 공변(covariant)으로 선언할 수 있습니다. 공변(covariant) 형식은 메서드 반환 형식으로만 사용할 수 있으며 메서드 인수의 형식으로는 사용할 수 없습니다. 다음 코드 예제에서는 공변(covariant) 제네릭 대리자를 선언하는 방법을 보여 줍니다.

```vb
Public Delegate Function DCovariant(Of Out R)() As R
```

`in` 키워드를 사용하여 제네릭 대리자에서 제네릭 형식 매개 변수를 반공변(contravariant)으로 선언할 수 있습니다. 반공변(contravariant) 형식은 메서드 인수의 형식으로서만 사용할 수 있으며 메서드 반환 형식으로는 사용할 수 없습니다. 다음 코드 예제에서는 반공변(contravariant) 제네릭 대리자를 선언하는 방법을 보여 줍니다.

```vb
Public Delegate Sub DContravariant(Of In A)(ByVal a As A)
```

> [!IMPORTANT]
> `ByRef`Visual Basic의 매개 변수는 variant로 표시할 수 없습니다.

동일한 대리자에서, 그러나 서로 다른 형식 매개 변수에 대해 분산 및 공변성(covariance)을 모두 지원하는 것도 가능합니다. 이는 다음 예에서 확인할 수 있습니다.

```vb
Public Delegate Function DVariant(Of In A, Out R)(ByVal a As A) As R
```

### <a name="instantiating-and-invoking-variant-generic-delegates"></a>Variant 제네릭 대리자 인스턴스화 및 호출

비 variant 대리자를 인스턴스화 및 호출하듯 variant 대리자를 인스턴스화 및 호출할 수 있습니다. 다음 예제에서는 람다 식을 사용하여 대리자가 인스턴스화됩니다.

```vb
Dim dvariant As DVariant(Of String, String) = Function(str) str + " "
dvariant("test")
```

### <a name="combining-variant-generic-delegates"></a>Variant 제네릭 대리자 결합

Variant 대리자는 결합할 수 없습니다. <xref:System.Delegate.Combine%2A> 메서드는 variant 대리자 변환을 지원하지 않으며 대리자가 정확히 동일한 형식일 것으로 예상합니다. 이 경우 다음 <xref:System.Delegate.Combine%2A> 코드 예제와 같이 메서드를 사용 C# `+` 하거나 (에서 및 Visual Basic) 연산자 (에서 C#)를 사용 하 여 대리자를 결합 하면 런타임 예외가 발생할 수 있습니다.

```vb
Dim actObj As Action(Of Object) = Sub(x) Console.WriteLine("object: {0}", x)
Dim actStr As Action(Of String) = Sub(x) Console.WriteLine("string: {0}", x)

' The following statement throws an exception at run time.
' Dim actCombine = [Delegate].Combine(actStr, actObj)
```

## <a name="variance-in-generic-type-parameters-for-value-and-reference-types"></a>값 및 참조 형식에 대한 제네릭 형식 매개 변수에서의 가변성

제네릭 형식 매개 변수에 대한 가변성은 참조 형식에 대해서만 지원됩니다. 예를 들어 `DVariant(Of Int)`정수는 값 형식 이므로 `DVariant(Of Object)` 는 `DVariant(Of Long)`를 또는로 암시적으로 변환할 수 없습니다.

다음 예제에서는 제네릭 형식 매개 변수에서의 가변성이 값 형식에 대해 지원되지 않음을 보여 줍니다.

```vb
' The type T is covariant.
Public Delegate Function DVariant(Of Out T)() As T
' The type T is invariant.
Public Delegate Function DInvariant(Of T)() As T
Sub Test()
    Dim i As Integer = 0
    Dim dInt As DInvariant(Of Integer) = Function() i
    Dim dVariantInt As DVariant(Of Integer) = Function() i

    ' All of the following statements generate a compiler error
    ' because type variance in generic parameters is not supported
    ' for value types, even if generic type parameters are declared variant.
    ' Dim dObject As DInvariant(Of Object) = dInt
    ' Dim dLong As DInvariant(Of Long) = dInt
    ' Dim dVariantObject As DInvariant(Of Object) = dInt
    ' Dim dVariantLong As DInvariant(Of Long) = dInt
End Sub
```

## <a name="relaxed-delegate-conversion-in-visual-basic"></a>Visual Basic의 완화 대리자 변환

완화 된 대리자 변환을 사용 하면 메서드 시그니처를 대리자 형식과 보다 유연 하 게 일치 시킬 수 있습니다. 예를 들어, 대리자에 메서드를 할당할 때 매개 변수 사양을 생략 하 고 함수 반환 값을 생략할 수 있습니다. 자세한 내용은 [완화 대리자 변환](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [제네릭](../../../../standard/generics/index.md)
- [Func 및 Action 제네릭 대리자에 가변성 사용(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
