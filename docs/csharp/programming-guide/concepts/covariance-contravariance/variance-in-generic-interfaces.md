---
title: 제네릭 인터페이스의 가변성(C#)
ms.date: 06/06/2019
ms.assetid: 4828a8f9-48c0-4128-9749-7fcd6bf19a06
ms.openlocfilehash: 71225814a11074f52e4937dec88ca5e27114d6c7
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72179054"
---
# <a name="variance-in-generic-interfaces-c"></a>제네릭 인터페이스의 가변성(C#)

.NET Framework 4에서는 기존의 몇몇 제네릭 인터페이스에 대한 가변성 지원이 추가되었습니다. 가변성 지원은 이러한 인터페이스를 구현하는 클래스의 암시적 변환을 가능하게 합니다. 

.NET Framework 4부터 다음 인터페이스는 variant입니다.

- <xref:System.Collections.Generic.IEnumerable%601>(T는 공변(covariant)임)

- <xref:System.Collections.Generic.IEnumerator%601>(T는 공변(covariant)임)

- <xref:System.Linq.IQueryable%601>(T는 공변(covariant)임)

- <xref:System.Linq.IGrouping%602>(`TKey` 및 `TElement`는 공변(covariant)임)

- <xref:System.Collections.Generic.IComparer%601>(T는 반공변(contravariant)임)

- <xref:System.Collections.Generic.IEqualityComparer%601>(T는 반공변(contravariant)임)

- <xref:System.IComparable%601>(T는 반공변(contravariant)임)

.NET Framework 4.5부터 다음 인터페이스는 variant입니다.

- <xref:System.Collections.Generic.IReadOnlyList%601>(T는 공변(covariant)임)

- <xref:System.Collections.Generic.IReadOnlyCollection%601>(T는 공변(covariant)임)

공변성(covariance)은 메서드가 인터페이스의 제네릭 형식 매개 변수에 정의된 것보다 더 많은 수의 파생된 반환 형식을 갖도록 허용합니다. 공변성(covariance) 기능을 설명하려면 `IEnumerable<Object>` 및 `IEnumerable<String>`이라는 제네릭 인터페이스를 고려하세요. `IEnumerable<String>` 인터페이스는 `IEnumerable<Object>` 인터페이스를 상속하지 않습니다. 그러나 `String` 형식은 `Object` 형식을 상속하며, 경우에 따라 이러한 인터페이스의 개체를 서로 할당할 수 있습니다. 다음 코드 예제에서 이를 확인할 수 있습니다.

```csharp
IEnumerable<String> strings = new List<String>();
IEnumerable<Object> objects = strings;
```

.NET Framework의 이전 버전에서는 이 코드로 인해 C# 및 Visual Basic(`Option Strict`이 on인 경우)에서 컴파일 오류가 발생합니다. 그러나 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스는 공변(covariant) 이므로 이제 다음 예제와 같이 `objects` 대신 `strings`를 사용할 수 있습니다.

반공변성(Contravariance)은 메서드가 인터페이스의 제네릭 매개 변수에 지정된 것보다 더 적은 수의 파생된 형식의 인수 형식을 갖도록 허용합니다. 반공변성(contravariance)을 설명하기 위해, 사용자가 `BaseComparer` 클래스를 만들어 `BaseClass` 클래스의 인스턴스를 비교한다고 가정합니다. `BaseComparer` 클래스가 `IEqualityComparer<BaseClass>` 인터페이스를 구현합니다. <xref:System.Collections.Generic.IEqualityComparer%601> 인터페이스는 이제 반공변(contravariant)이므로 `BaseClass` 클래스를 상속하는 클래스의 인스턴스를 비교하는 데 `BaseComparer`를 사용할 수 있습니다. 다음 코드 예제에서 이를 확인할 수 있습니다.

```csharp
// Simple hierarchy of classes.
class BaseClass { }
class DerivedClass : BaseClass { }

// Comparer class.
class BaseComparer : IEqualityComparer<BaseClass>
{
    public int GetHashCode(BaseClass baseInstance)
    {
        return baseInstance.GetHashCode();
    }
    public bool Equals(BaseClass x, BaseClass y)
    {
        return x == y;
    }
}
class Program
{
    static void Test()
    {
        IEqualityComparer<BaseClass> baseComparer = new BaseComparer();

        // Implicit conversion of IEqualityComparer<BaseClass> to
        // IEqualityComparer<DerivedClass>.
        IEqualityComparer<DerivedClass> childComparer = baseComparer;
    }
}
```

추가 예제는 [제네릭 컬렉션용 인터페이스의 가변성 사용(C#)](./using-variance-in-interfaces-for-generic-collections.md)을 참조하세요.

제네릭 인터페이스의 가변성은 참조 형식에 대해서만 지원됩니다. 값 형식은 가변성을 지원하지 않습니다. 정수는 값 형식으로 표시되므로 예를 들어 `IEnumerable<int>`를 `IEnumerable<object>`로 암시적으로 변환할 수 없습니다.

```csharp
IEnumerable<int> integers = new List<int>();
// The following statement generates a compiler error,
// because int is a value type.
// IEnumerable<Object> objects = integers;
```

Variant 인터페이스를 구현하는 클래스는 여전히 비 variant라는 점에 유의해야 합니다. 예를 들어 <xref:System.Collections.Generic.List%601>는 공변(covariant) 인터페이스 <xref:System.Collections.Generic.IEnumerable%601>을 구현하지만 암시적으로 `List<String>`를 `List<Object>`으로 변환할 수 없습니다. 다음 코드 예제에서 이 내용을 보여 줍니다.

```csharp
// The following line generates a compiler error
// because classes are invariant.
// List<Object> list = new List<String>();

// You can use the interface object instead.
IEnumerable<Object> listObjects = new List<String>();
```

## <a name="see-also"></a>참고 항목

- [제네릭 컬렉션용 인터페이스의 가변성 사용(C#)](./using-variance-in-interfaces-for-generic-collections.md)
- [Variant 제네릭 인터페이스 만들기(C#)](./creating-variant-generic-interfaces.md)
- [제네릭 인터페이스](../../../../standard/generics/interfaces.md)
- [대리자의 가변성(C#)](./variance-in-delegates.md)
