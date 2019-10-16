---
title: Variant 제네릭 인터페이스 만들기(C#)
ms.date: 07/20/2015
ms.assetid: 30330ec4-9df2-4838-a535-6c406d0ed4df
ms.openlocfilehash: 4ba72f28cd2ddd800f169387cc2c742159d4cb1b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595314"
---
# <a name="creating-variant-generic-interfaces-c"></a>Variant 제네릭 인터페이스 만들기(C#)

인터페이스에서 제네릭 형식 매개 변수를 공변(covariant) 또는 반공변(contravariant)으로 선언할 수 있습니다. *공변성(covariance)* 은 인터페이스 메서드가 제네릭 형식 매개 변수에 정의된 것보다 더 많은 수의 파생된 반환 형식을 갖도록 허용합니다. *반공변성(contravariance)* 은 인터페이스 메서드가 제네릭 매개 변수에 지정된 것보다 더 적은 수의 파생된 형식의 인수 형식을 갖도록 허용합니다. 공변(covariant) 또는 반공변(contravariant) 제네릭 형식 매개 변수가 포함된 제네릭 인터페이스를 *variant*라고 합니다.

> [!NOTE]
> .NET Framework 4에서는 기존의 몇몇 제네릭 인터페이스에 대한 가변성 지원이 추가되었습니다. .NET Framework의 variant 인터페이스 목록은 [제네릭 인터페이스의 가변성(C#)](./variance-in-generic-interfaces.md)을 참조하세요.

## <a name="declaring-variant-generic-interfaces"></a>Variant 제네릭 인터페이스 선언

제네릭 형식 매개 변수에 `in` 및 `out` 키워드를 사용하여 Variant 제네릭 인터페이스를 선언할 수 있습니다.

> [!IMPORTANT]
> C#에서 `ref`, `in` 및 `out` 매개 변수는 variant일 수 없습니다. 또한 값 형식은 가변성을 지원하지 않습니다.

`out` 키워드를 사용하여 제네릭 형식 매개 변수를 공변(covariant)으로 선언할 수 있습니다. 공변(covariant) 형식은 다음 조건을 충족해야 합니다.

- 형식은 인터페이스 메서드의 반환 형식으로만 사용되고 메서드 인수의 형식으로 사용되지 않습니다. 이 내용은 `R` 형식이 공변(covariant)으로 선언된 다음 예제에서 설명합니다.

    ```csharp
    interface ICovariant<out R>
    {
        R GetSomething();
        // The following statement generates a compiler error.
        // void SetSomething(R sampleArg);

    }
    ```

    그러나 이 규칙에는 한 가지 예외가 있습니다. 반공변(contravariant) 제네릭 대리자가 메서드 매개 변수로 있는 경우 형식을 이 대리자에 대한 제네릭 형식 매개 변수로 사용할 수 있습니다. 다음 예제에서 `R` 형식을 통해 이를 확인할 수 있습니다. 자세한 내용은 [대리자에서 가변성 사용(C#)](./variance-in-delegates.md) 및 [Func 및 Action 제네릭 대리자에 가변성 사용(C#)](./using-variance-for-func-and-action-generic-delegates.md)을 참조하세요.

    ```csharp
    interface ICovariant<out R>
    {
        void DoSomething(Action<R> callback);
    }
    ```

- 형식은 인터페이스 메서드에 대한 제네릭 제약 조건으로 사용되지 않습니다. 이는 다음 코드에 설명되어 있습니다.

    ```csharp
    interface ICovariant<out R>
    {
        // The following statement generates a compiler error
        // because you can use only contravariant or invariant types
        // in generic constraints.
        // void DoSomething<T>() where T : R;
    }
    ```

`in` 키워드를 사용하여 제네릭 형식 매개 변수를 반공변(contravariant)으로 선언할 수 있습니다. 반공변(contravariant) 형식은 메서드 인수의 형식으로서만 사용할 수 있으며 인터페이스 메서드의 반환 형식으로는 사용할 수 없습니다. 반공변(contravariant) 형식은 제네릭 제약 조건에 사용될 수도 있습니다. 다음 코드에서는 반공변(contravariant) 인터페이스를 선언하고 해당 메서드 중 하나에 제네릭 제약 조건을 사용하는 방법을 보여 줍니다.

```csharp
interface IContravariant<in A>
{
    void SetSomething(A sampleArg);
    void DoSomething<T>() where T : A;
    // The following statement generates a compiler error.
    // A GetSomething();
}
```

같은 인터페이스에서 그러나 서로 다른 형식 매개 변수에 대해 공변성(covariance) 및 반공변성(contravariance)을 모두 지원하는 것도 가능합니다.

```csharp
interface IVariant<out R, in A>
{
    R GetSomething();
    void SetSomething(A sampleArg);
    R GetSetSomethings(A sampleArg);
}
```

## <a name="implementing-variant-generic-interfaces"></a>Variant 제네릭 인터페이스 구현

고정(invariant) 인터페이스에 사용되는 같은 구문을 사용하여 클래스에서 Variant 제네릭 인터페이스를 구현합니다. 다음 코드 예제에서는 제네릭 클래스에서 공변(covariant) 인터페이스를 구현하는 방법을 보여 줍니다.

```csharp
interface ICovariant<out R>
{
    R GetSomething();
}
class SampleImplementation<R> : ICovariant<R>
{
    public R GetSomething()
    {
        // Some code.
        return default(R);
    }
}
```

Variant 인터페이스를 구현하는 클래스는 고정입니다. 예를 들어, 다음과 같은 코드를 생각해 볼 수 있습니다.

```csharp
// The interface is covariant.
ICovariant<Button> ibutton = new SampleImplementation<Button>();
ICovariant<Object> iobj = ibutton;

// The class is invariant.
SampleImplementation<Button> button = new SampleImplementation<Button>();
// The following statement generates a compiler error
// because classes are invariant.
// SampleImplementation<Object> obj = button;
```

## <a name="extending-variant-generic-interfaces"></a>Variant 제네릭 인터페이스 확장

Variant 제네릭 인터페이스를 확장할 경우 `in` 및 `out` 키워드를 사용하여 파생 인터페이스가 가변성을 지원하는지 명시적으로 지정해야 합니다. 컴파일러에서는 확장되고 있는 인터페이스에서 가변성을 유추하지 않습니다. 예를 들어 다음 인터페이스를 살펴봅니다.

```csharp
interface ICovariant<out T> { }
interface IInvariant<T> : ICovariant<T> { }
interface IExtCovariant<out T> : ICovariant<T> { }
```

두 인터페이스가 모두 같은 인터페이스를 확장하더라도 `IInvariant<T>` 인터페이스에서 제네릭 형식 매개 변수 `T`는 고정이지만, `IExtCovariant<out T>`에서 형식 매개 변수는 공변(covariant)입니다. 반공변(contravariant) 제네릭 형식 매개 변수에는 같은 규칙이 적용됩니다.

제네릭 형식 매개 변수 `T`가 공변(covariant)인 인터페이스 및 확장 인터페이스에서 제네릭 형식 매개 변수 `T`가 고정인 경우 반공변(contravariant)인 인터페이스를 둘 다 확장하는 인터페이스를 만들 수 있습니다. 다음 코드 예제에서 이 내용을 보여 줍니다.

```csharp
interface ICovariant<out T> { }
interface IContravariant<in T> { }
interface IInvariant<T> : ICovariant<T>, IContravariant<T> { }
```

그러나 한 인터페이스에서 제네릭 형식 매개 변수 `T`가 공변(covariant)으로 선언되면 확장 인터페이스에서는 이 매개 변수를 반공변(contravariant)으로 선언할 수 없고, 반대의 경우도 마찬가지입니다. 다음 코드 예제에서 이 내용을 보여 줍니다.

```csharp
interface ICovariant<out T> { }
// The following statement generates a compiler error.
// interface ICoContraVariant<in T> : ICovariant<T> { }
```

### <a name="avoiding-ambiguity"></a>모호성 방지

Variant 제네릭 인터페이스를 구현할 경우 가변성으로 인해 모호성이 나타나는 경우가 있습니다. 이러한 경우가 발생해서는 안 됩니다.

예를 들어 서로 다른 제네릭 형식 매개 변수가 포함된 같은 Variant 제네릭 인터페이스를 한 클래스에서 명시적으로 구현하면 모호성이 발생할 수 있습니다. 컴파일러에서는 이 경우 오류를 생성하지 않지만 런타임에 선택될 인터페이스 구현이 지정되지 않습니다. 이로 인해 코드에서 미묘한 버그가 발생할 수 있습니다. 다음 코드 예제를 살펴봅니다.

```csharp
// Simple class hierarchy.
class Animal { }
class Cat : Animal { }
class Dog : Animal { }

// This class introduces ambiguity
// because IEnumerable<out T> is covariant.
class Pets : IEnumerable<Cat>, IEnumerable<Dog>
{
    IEnumerator<Cat> IEnumerable<Cat>.GetEnumerator()
    {
        Console.WriteLine("Cat");
        // Some code.
        return null;
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        // Some code.
        return null;
    }

    IEnumerator<Dog> IEnumerable<Dog>.GetEnumerator()
    {
        Console.WriteLine("Dog");
        // Some code.
        return null;
    }
}
class Program
{
    public static void Test()
    {
        IEnumerable<Animal> pets = new Pets();
        pets.GetEnumerator();
    }
}
```

이 예제에서는 `pets.GetEnumerator` 메서드가 `Cat` 및 `Dog` 중에 선택하는 방법이 지정되어 있지 않습니다. 이로 인해 코드에서 문제가 발생할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [제네릭 인터페이스의 가변성(C#)](./variance-in-generic-interfaces.md)
- [Func 및 Action 제네릭 대리자에 가변성 사용(C#)](./using-variance-for-func-and-action-generic-delegates.md)
