---
title: C#의 컬렉션 반복
ms.date: 08/14/2018
ms.assetid: c93f6dd4-e72a-4a06-be1c-a98b3255b734
ms.openlocfilehash: 2b358e8272820bf6fb5bcb45763bae980b91962f
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50191196"
---
# <a name="iterators-c"></a>반복기(C#)

*반복기*는 목록 및 배열과 같은 컬렉션을 단계별로 실행하는 데 사용할 수 있습니다.

반복기 메서드 또는 `get` 접근자는 컬렉션에 대해 사용자 지정 반복을 수행합니다. 반복기 메서드는 [yield return](../../../csharp/language-reference/keywords/yield.md) 문을 사용하여 각 요소를 한 번에 하나씩 반환합니다. `yield return` 문에 도달하면 코드의 현재 위치가 기억됩니다. 다음에 반복기 함수가 호출되면 해당 위치에서 실행이 다시 시작됩니다.

클라이언트 코드에서 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 문 또는 LINQ 쿼리를 사용하여 반복기를 이용합니다.

다음 예제에서 `foreach` 루프의 첫 번째 반복은 첫 번째 `yield return` 문에 도달할 때까지 `SomeNumbers` 반복기 메서드에서 실행이 계속되도록 합니다. 이 반복은 3 값을 반환하며 반복기 메서드에서 현재 위치는 유지됩니다. 루프의 다음 반복에서는 반복기 메서드의 실행이 중지되었던 위치에서 계속되고 `yield return` 문에 도달하면 다시 중지됩니다. 이 반복은 값 5를 반환하며 반복기 메서드에서 현재 위치는 다시 유지됩니다. 루프는 반복기 메서드의 끝에 도달하면 완료됩니다.

```csharp
static void Main()
{
    foreach (int number in SomeNumbers())
    {
        Console.Write(number.ToString() + " ");
    }
    // Output: 3 5 8
    Console.ReadKey();
}

public static System.Collections.IEnumerable SomeNumbers()
{
    yield return 3;
    yield return 5;
    yield return 8;
}
```

반복기 메서드 또는 `get` 접근자의 반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator> 또는 <xref:System.Collections.Generic.IEnumerator%601>일 수 있습니다.

`yield break` 문을 사용하여 반복기를 종료할 수 있습니다.

> [!NOTE]
> 단순 반복기 예제를 제외한 이 항목의 모든 예제에 대해 `System.Collections` 및 `System.Collections.Generic` 네임스페이스에 대한 [using](../../../csharp/language-reference/keywords/using-directive.md) 지시문을 포함하세요.

## <a name="simple-iterator"></a>단순 반복기

다음 예제에는 [for](../../../csharp/language-reference/keywords/for.md) 루프 내에 단일 `yield return` 문이 있습니다. `Main`에서 `foreach` 문 본문을 반복할 때마다 다음 `yield return` 문으로 진행하는 반복기 함수에 대한 호출이 생성됩니다.

```csharp
static void Main()
{
    foreach (int number in EvenSequence(5, 18))
    {
        Console.Write(number.ToString() + " ");
    }
    // Output: 6 8 10 12 14 16 18
    Console.ReadKey();
}

public static System.Collections.Generic.IEnumerable<int>
    EvenSequence(int firstNumber, int lastNumber)
{
    // Yield even numbers in the range.
    for (int number = firstNumber; number <= lastNumber; number++)
    {
        if (number % 2 == 0)
        {
            yield return number;
        }
    }
}
```

## <a name="creating-a-collection-class"></a>컬렉션 클래스 만들기

다음 예제에서 `DaysOfTheWeek` 클래스는 <xref:System.Collections.IEnumerable> 인터페이스를 구현하며, <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드가 필요합니다. 컴파일러는 `GetEnumerator` 메서드를 암시적으로 호출하며, <xref:System.Collections.IEnumerator>가 반환됩니다.

`GetEnumerator` 메서드는 `yield return` 문을 사용하여 각 문자열을 한 번에 하나씩 반환합니다.

```csharp
static void Main()
{
    DaysOfTheWeek days = new DaysOfTheWeek();

    foreach (string day in days)
    {
        Console.Write(day + " ");
    }
    // Output: Sun Mon Tue Wed Thu Fri Sat
    Console.ReadKey();
}

public class DaysOfTheWeek : IEnumerable
{
    private string[] days = { "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat" };

    public IEnumerator GetEnumerator()
    {
        for (int index = 0; index < days.Length; index++)
        {
            // Yield each day of the week.
            yield return days[index];
        }
    }
}
```

다음 예제에서는 동물 컬렉션을 포함하는 `Zoo` 클래스를 만듭니다.

클래스 인스턴스(`theZoo`)를 참조하는 `foreach` 문은 `GetEnumerator` 메서드를 암시적으로 호출합니다. `Birds` 및 `Mammals` 속성을 참조하는 `foreach` 문은 `AnimalsForType` 명명된 반복기 메서드를 사용합니다.

```csharp
static void Main()
{
    Zoo theZoo = new Zoo();

    theZoo.AddMammal("Whale");
    theZoo.AddMammal("Rhinoceros");
    theZoo.AddBird("Penguin");
    theZoo.AddBird("Warbler");

    foreach (string name in theZoo)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Whale Rhinoceros Penguin Warbler

    foreach (string name in theZoo.Birds)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Penguin Warbler

    foreach (string name in theZoo.Mammals)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Whale Rhinoceros

    Console.ReadKey();
}

public class Zoo : IEnumerable
{
    // Private members.
    private List<Animal> animals = new List<Animal>();

    // Public methods.
    public void AddMammal(string name)
    {
        animals.Add(new Animal { Name = name, Type = Animal.TypeEnum.Mammal });
    }

    public void AddBird(string name)
    {
        animals.Add(new Animal { Name = name, Type = Animal.TypeEnum.Bird });
    }

    public IEnumerator GetEnumerator()
    {
        foreach (Animal theAnimal in animals)
        {
            yield return theAnimal.Name;
        }
    }

    // Public members.
    public IEnumerable Mammals
    {
        get { return AnimalsForType(Animal.TypeEnum.Mammal); }
    }

    public IEnumerable Birds
    {
        get { return AnimalsForType(Animal.TypeEnum.Bird); }
    }

    // Private methods.
    private IEnumerable AnimalsForType(Animal.TypeEnum type)
    {
        foreach (Animal theAnimal in animals)
        {
            if (theAnimal.Type == type)
            {
                yield return theAnimal.Name;
            }
        }
    }

    // Private class.
    private class Animal
    {
        public enum TypeEnum { Bird, Mammal }

        public string Name { get; set; }
        public TypeEnum Type { get; set; }
    }
}
```

## <a name="using-iterators-with-a-generic-list"></a>제네릭 목록과 함께 반복기 사용

다음 예제에서 <xref:System.Collections.Generic.Stack%601> 제네릭 클래스는 <xref:System.Collections.Generic.IEnumerable%601> 제네릭 인터페이스를 구현합니다. <xref:System.Collections.Generic.Stack%601.Push%2A> 메서드는 `T` 형식의 배열에 값을 할당합니다. <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 메서드는 `yield return` 문을 사용하여 배열 값을 반환합니다.

제네릭 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 메서드뿐 아니라 제네릭이 아닌 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드도 구현해야 합니다. <xref:System.Collections.Generic.IEnumerable%601>이 <xref:System.Collections.IEnumerable>에서 상속하기 때문입니다. 제네릭이 아닌 구현은 제네릭 구현을 따릅니다.

예제에서는 명명된 반복기를 사용하여 동일한 데이터 컬렉션을 반복하는 다양한 방법을 지원합니다. 이러한 명명된 반복기는 `TopToBottom` 및 `BottomToTop` 속성과 `TopN` 메서드입니다.

`BottomToTop` 속성은 `get` 접근자에서 반복기를 사용합니다.

```csharp
static void Main()
{
    Stack<int> theStack = new Stack<int>();

    //  Add items to the stack.
    for (int number = 0; number <= 9; number++)
    {
        theStack.Push(number);
    }

    // Retrieve items from the stack.
    // foreach is allowed because theStack implements IEnumerable<int>.
    foreach (int number in theStack)
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3 2 1 0

    // foreach is allowed, because theStack.TopToBottom returns IEnumerable(Of Integer).
    foreach (int number in theStack.TopToBottom)
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3 2 1 0

    foreach (int number in theStack.BottomToTop)
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 0 1 2 3 4 5 6 7 8 9

    foreach (int number in theStack.TopN(7))
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3

    Console.ReadKey();
}

public class Stack<T> : IEnumerable<T>
{
    private T[] values = new T[100];
    private int top = 0;

    public void Push(T t)
    {
        values[top] = t;
        top++;
    }
    public T Pop()
    {
        top--;
        return values[top];
    }

    // This method implements the GetEnumerator method. It allows
    // an instance of the class to be used in a foreach statement.
    public IEnumerator<T> GetEnumerator()
    {
        for (int index = top - 1; index >= 0; index--)
        {
            yield return values[index];
        }
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }

    public IEnumerable<T> TopToBottom
    {
        get { return this; }
    }

    public IEnumerable<T> BottomToTop
    {
        get
        {
            for (int index = 0; index <= top - 1; index++)
            {
                yield return values[index];
            }
        }
    }

    public IEnumerable<T> TopN(int itemsFromTop)
    {
        // Return less than itemsFromTop if necessary.
        int startIndex = itemsFromTop >= top ? 0 : top - itemsFromTop;

        for (int index = top - 1; index >= startIndex; index--)
        {
            yield return values[index];
        }
    }

}
```

## <a name="syntax-information"></a>구문 정보

반복기는 메서드 또는 `get` 접근자로 발생할 수 있습니다. 이벤트, 인스턴스 생성자, 정적 생성자 또는 정적 종료자에서는 반복기가 발생할 수 없습니다.

반복기에서 반환된 `yield return`IEnumerable의 형식 인수에 대한 명령문<T>의 식 형식에서 암시적 변환이 있어야 합니다.

C#에서 반복기 메서드는 `in`, `ref` 또는 `out` 매개 변수를 사용할 수 없습니다.

C#에서 "yield"는 예약어가 아니며 `return` 또는 `break` 키워드 앞에서 사용되는 경우에만 특별한 의미가 있습니다.

## <a name="technical-implementation"></a>기술 구현

반복기를 메서드로 작성하는 경우에도 컴파일러는 실제로 상태 시스템인 중첩 클래스로 변환합니다. 이 클래스는 클라이언트 코드의 `foreach` 루프가 계속되는 한 반복기의 위치를 추적합니다.

컴파일러의 용도를 확인하려면 Ildasm.exe 도구를 사용하여 반복기 메서드에 대해 생성되는 Microsoft Intermediate Language 코드를 확인할 수 있습니다.

[class](../../../csharp/language-reference/keywords/class.md) 또는 [struct](../../../csharp/language-reference/keywords/struct.md)에 대해 반복기를 만드는 경우 전체 <xref:System.Collections.IEnumerator> 인터페이스를 구현할 필요가 없습니다. 컴파일러는 반복기를 검색할 경우 <xref:System.Collections.IEnumerator> 또는 <xref:System.Collections.Generic.IEnumerator%601> 인터페이스의 `Current`, `MoveNext` 및 `Dispose` 메서드를 자동으로 생성합니다.

`foreach` 루프를 연속 반복하거나 `IEnumerator.MoveNext`를 직접 호출하면 다음 반복기 코드 본문이 이전 `yield return` 문 다음에 다시 시작됩니다. 그런 후 반복기 본문의 끝에 도달하거나 `yield break` 문이 나타날 때까지 다음 `yield return` 문을 계속 실행합니다.

반복기는 <xref:System.Collections.IEnumerator.Reset%2A?displayProperty=nameWithType> 메서드를 지원하지 않습니다. 처음부터 다시 반복하려면 새 반복기를 가져와야 합니다. 반복기 메서드에 의해 반환된 반복기에서 <xref:System.Collections.IEnumerator.Reset%2A>를 호출하면 <xref:System.NotSupportedException>가 throw됩니다.

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/classes.md#iterators)을 참조하세요.

## <a name="use-of-iterators"></a>반복기 사용

반복기를 사용하면 복잡한 코드를 사용하여 목록 시퀀스를 채워야 하는 경우 `foreach` 루프의 단순성을 유지할 수 있습니다. 이 기능은 다음을 수행하려는 경우에 유용할 수 있습니다.

- 첫 번째 `foreach` 루프 반복 후 목록 시퀀스를 수정합니다.

- 첫 번째 `foreach` 루프 반복 전에 큰 목록이 완전히 로드되지 않도록 합니다. 한 가지 예로 테이블 행을 일괄 로드하는 페이징 페치가 있으며, 또 다른 예로 .NET Framework 내에서 반복기를 구현하는 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 메서드가 있습니다.

- 반복기에서 목록 작성을 캡슐화합니다. 반복기 메서드에서 목록을 빌드한 후 루프에서 각 결과를 생성할 수 있습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic>
- <xref:System.Collections.Generic.IEnumerable%601>
- [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)
- [yield](../../../csharp/language-reference/keywords/yield.md)
- [배열에 foreach 사용](../../../csharp/programming-guide/arrays/using-foreach-with-arrays.md)
- [제네릭](../../../csharp/programming-guide/generics/index.md)