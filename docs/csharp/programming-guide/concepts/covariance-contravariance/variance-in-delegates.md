---
title: 대리자의 가변성(C#)
ms.date: 07/20/2015
ms.assetid: 19de89d2-8224-4406-8964-2965b732b890
ms.openlocfilehash: 3dabac4e532198871cf05d639aa692751ab17ae1
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48027574"
---
# <a name="variance-in-delegates-c"></a>대리자의 가변성(C#)
.NET Framework 3.5에는 메서드 시그니처를 C#에 있는 모든 대리자의 대리자 형식과 일치시키는 가변성 지원이 추가되었습니다. 즉, 일치하는 시그니처가 있는 메서드만이 아니라 더 많은 파생된 형식(공변성(covariance))을 반환하는 메서드 또는 대리자 형식에 지정된 것보다 더 적은 수의 파생된 형식(반공변성(contravariance))을 가지고 있는 매개 변수를 수락하는 메서드도 대리자에 할당할 수 있습니다. 여기에는 제네릭 및 비 제네릭 대리자가 모두 포함됩니다.  
  
 다음과 같이 두 개의 클래스 및 두 개의 대리자(제네릭 및 비 제네릭)를 가지고 있는 코드를 예로 들어보겠습니다.  
  
```csharp  
public class First { }  
public class Second : First { }  
public delegate First SampleDelegate(Second a);  
public delegate R SampleGenericDelegate<A, R>(A a);  
```  
  
 `SampleDelegate` 또는 `SampleGenericDelegate<A, R>` 형식의 대리자를 만들 때 다음 메서드 중 하나를 할당할 수 있습니다.  
  
```csharp  
// Matching signature.  
public static First ASecondRFirst(Second first)  
{ return new First(); }  
  
// The return type is more derived.  
public static Second ASecondRSecond(Second second)  
{ return new Second(); }  
  
// The argument type is less derived.  
public static First AFirstRFirst(First first)  
{ return new First(); }  
  
// The return type is more derived   
// and the argument type is less derived.  
public static Second AFirstRSecond(First first)  
{ return new Second(); }  
```  
  
 다음 코드 예제에서는 메서드 시그니처 및 대리자 형식 사이의 암시적 변환을 보여 줍니다.  
  
```csharp  
// Assigning a method with a matching signature   
// to a non-generic delegate. No conversion is necessary.  
SampleDelegate dNonGeneric = ASecondRFirst;  
// Assigning a method with a more derived return type   
// and less derived argument type to a non-generic delegate.  
// The implicit conversion is used.  
SampleDelegate dNonGenericConversion = AFirstRSecond;  
  
// Assigning a method with a matching signature to a generic delegate.  
// No conversion is necessary.  
SampleGenericDelegate<Second, First> dGeneric = ASecondRFirst;  
// Assigning a method with a more derived return type   
// and less derived argument type to a generic delegate.  
// The implicit conversion is used.  
SampleGenericDelegate<Second, First> dGenericConversion = AFirstRSecond;  
```  
  
 더 많은 예제는 [대리자에서 가변성 사용(C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md) 및 [Func 및 Action 제네릭 대리자에 가변성 사용(C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)을 참조하세요.  
  
## <a name="variance-in-generic-type-parameters"></a>제네릭 형식 매개 변수에서의 가변성  
 .NET Framework 4 이상에서는 가변성에 필요한 대로 형식이 서로 간에 상속된 경우 제네릭 형식 매개 변수로 지정한 서로 다른 형식을 가지고 있는 제네릭 대리자를 상호 간에 할당할 수 있도록, 대리자 간 암시적 변환을 사용하도록 설정할 수 있습니다.  
  
 암시적 변환을 사용하도록 설정하려면 `in` 및 `out` 키워드를 사용하여 대리자에서 제네릭 매개 변수를 공변(covariant) 또는 반공변(contravariant)으로 선언해야 합니다.  
  
 다음 코드 예제에서는 공변(covariant) 제네릭 형식 매개 변수가 있는 대리자를 만드는 방법을 보여 줍니다.  
  
```csharp  
// Type T is declared covariant by using the out keyword.  
public delegate T SampleGenericDelegate <out T>();  
  
public static void Test()  
{  
    SampleGenericDelegate <String> dString = () => " ";  
  
    // You can assign delegates to each other,  
    // because the type T is declared covariant.  
    SampleGenericDelegate <Object> dObject = dString;             
}  
```  
  
 메서드 시그니처를 대리자 형식과 일치시키는 용도로만 가변성 지원을 사용하고 `in` 및 `out` 키워드를 사용하지 않는 경우, 대리자를 동일한 람다 식 또는 메서드로 인스턴스화할 수는 있지만 한 대리자를 다른 대리자에 할당할 수는 없는 경우가 더러 있습니다.  
  
 다음 코드 예제에서, `String`은 `Object`를 상속하지만 `SampleGenericDelegate<String>`을 `SampleGenericDelegate<Object>`로 명시적으로 변환할 수 없습니다. `T` 제네릭 매개 변수를 `out` 키워드로 표시하면 이 문제를 수정할 수 있습니다.  
  
```csharp  
public delegate T SampleGenericDelegate<T>();  
  
public static void Test()  
{  
    SampleGenericDelegate<String> dString = () => " ";  
  
    // You can assign the dObject delegate  
    // to the same lambda expression as dString delegate  
    // because of the variance support for   
    // matching method signatures with delegate types.  
    SampleGenericDelegate<Object> dObject = () => " ";  
  
    // The following statement generates a compiler error  
    // because the generic type T is not marked as covariant.  
    // SampleGenericDelegate <Object> dObject = dString;  
  
}  
```  
  
### <a name="generic-delegates-that-have-variant-type-parameters-in-the-net-framework"></a>.NET Framework에 Variant 형식 매개 변수를 가지고 있는 제네릭 대리자  
 .NET Framework 4에는 기존의 몇몇 제네릭 대리자에서 제네릭 형식 매개 변수에 대한 가변성 지원이 추가되었습니다.  
  
-   <xref:System> 네임스페이스의 `Action` 대리자(예: <xref:System.Action%601> 및 <xref:System.Action%602>)  
  
-   <xref:System> 네임스페이스의 `Func` 대리자(예: <xref:System.Func%601> 및 <xref:System.Func%602>)  
  
-   <xref:System.Predicate%601> 대리자  
  
-   <xref:System.Comparison%601> 대리자  
  
-   <xref:System.Converter%602> 대리자  
  
 자세한 정보 및 예제는 [Func 및 Action 제네릭 대리자에 가변성 사용(C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)을 참조하세요.  
  
### <a name="declaring-variant-type-parameters-in-generic-delegates"></a>제네릭 대리자에서 Variant 형식 매개 변수 선언  
 제네릭 대리자가 공변(covariant) 또는 반공변(contravariant) 제네릭 형식 매개 변수를 가지고 있는 경우 이를 *variant 제네릭 대리자*라고 할 수 있습니다.  
  
 `out` 키워드를 사용하여 제네릭 대리자에서 제네릭 형식 매개 변수를 공변(covariant)으로 선언할 수 있습니다. 공변(covariant) 형식은 메서드 반환 형식으로만 사용할 수 있으며 메서드 인수의 형식으로는 사용할 수 없습니다. 다음 코드 예제에서는 공변(covariant) 제네릭 대리자를 선언하는 방법을 보여 줍니다.  
  
```csharp  
public delegate R DCovariant<out R>();  
```  
  
 `in` 키워드를 사용하여 제네릭 대리자에서 제네릭 형식 매개 변수를 반공변(contravariant)으로 선언할 수 있습니다. 반공변(contravariant) 형식은 메서드 인수의 형식으로서만 사용할 수 있으며 메서드 반환 형식으로는 사용할 수 없습니다. 다음 코드 예제에서는 반공변(contravariant) 제네릭 대리자를 선언하는 방법을 보여 줍니다.  
  
```csharp  
public delegate void DContravariant<in A>(A a);  
```  
  
> [!IMPORTANT]
>  C#의 `ref`, `in` 및 `out` 매개 변수는 variant로 표시할 수 없습니다.  
  
 동일한 대리자에서, 그러나 서로 다른 형식 매개 변수에 대해 분산 및 공변성(covariance)을 모두 지원하는 것도 가능합니다. 다음 예제에서 이를 확인할 수 있습니다.  
  
```csharp  
public delegate R DVariant<in A, out R>(A a);  
```  
  
### <a name="instantiating-and-invoking-variant-generic-delegates"></a>Variant 제네릭 대리자 인스턴스화 및 호출  
 비 variant 대리자를 인스턴스화 및 호출하듯 variant 대리자를 인스턴스화 및 호출할 수 있습니다. 다음 예제에서는 람다 식을 사용하여 대리자가 인스턴스화됩니다.  
  
```csharp  
DVariant<String, String> dvariant = (String str) => str + " ";  
dvariant("test");  
```  
  
### <a name="combining-variant-generic-delegates"></a>Variant 제네릭 대리자 결합  
 Variant 대리자는 결합할 수 없습니다. <xref:System.Delegate.Combine%2A> 메서드는 variant 대리자 변환을 지원하지 않으며 대리자가 정확히 동일한 형식일 것으로 예상합니다. 따라서 다음 코드 예제와 같이 <xref:System.Delegate.Combine%2A> 메서드를 사용하거나 `+` 연산자를 사용하여 대리자를 결합하면 런타임 예외가 발생할 수 있습니다.  
  
```csharp  
Action<object> actObj = x => Console.WriteLine("object: {0}", x);  
Action<string> actStr = x => Console.WriteLine("string: {0}", x);  
// All of the following statements throw exceptions at run time.  
// Action<string> actCombine = actStr + actObj;  
// actStr += actObj;  
// Delegate.Combine(actStr, actObj);  
```  
  
## <a name="variance-in-generic-type-parameters-for-value-and-reference-types"></a>값 및 참조 형식에 대한 제네릭 형식 매개 변수에서의 가변성  
 제네릭 형식 매개 변수에 대한 가변성은 참조 형식에 대해서만 지원됩니다. 정수는 값 형식이므로, 예를 들어 `DVariant<int>`를 명시적으로 `DVariant<Object>` 또는 `DVariant<long>`으로 변환할 수 없습니다.  
  
 다음 예제에서는 제네릭 형식 매개 변수에서의 가변성이 값 형식에 대해 지원되지 않음을 보여 줍니다.  
  
```csharp  
// The type T is covariant.  
public delegate T DVariant<out T>();  
  
// The type T is invariant.  
public delegate T DInvariant<T>();  
  
public static void Test()  
{  
    int i = 0;  
    DInvariant<int> dInt = () => i;  
    DVariant<int> dVariantInt = () => i;  
  
    // All of the following statements generate a compiler error  
    // because type variance in generic parameters is not supported  
    // for value types, even if generic type parameters are declared variant.  
    // DInvariant<Object> dObject = dInt;  
    // DInvariant<long> dLong = dInt;  
    // DVariant<Object> dVariantObject = dVariantInt;  
    // DVariant<long> dVariantLong = dVariantInt;              
}  
```  
  
## <a name="see-also"></a>참고 항목

- [제네릭](~/docs/standard/generics/index.md)  
- [Func 및 Action 제네릭 대리자에 가변성 사용(C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)  
- [방법: 대리자 조합(멀티캐스트 대리자)](../../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)
