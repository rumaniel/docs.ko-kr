---
title: 개체 지향 프로그래밍(C#)
ms.date: 07/20/2015
ms.assetid: 89574786-65ef-4335-88bc-fbacd094f183
ms.openlocfilehash: 50b38833582ebe46836ccfab4e1ebeb98b53a96e
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659873"
---
# <a name="object-oriented-programming-c"></a>개체 지향 프로그래밍(C#)

C#은 캡슐화, 상속, 다형성 등 개체 지향 프로그래밍에 대한 모든 지원을 제공합니다.

*캡슐화*는 서로 관련된 속성, 메서드 및 기타 멤버의 그룹을 하나의 단위나 개체로 취급하는 것을 말합니다.

*상속*은 기존 클래스를 기반으로 새로운 클래스를 만들 수 있는 능력을 나타냅니다.

*다형성*은 동일한 속성 또는 메서드를 각각 다른 방식으로 구현하는 여러 클래스를 서로 교체하여 사용할 수 있음을 의미합니다.

이 단원에서는 다음과 같은 개념에 대해 설명합니다.

- [클래스 및 개체](#Classes)

  - [클래스 멤버](#Members)

    - [속성 및 필드](#Properties)

    - [메서드](#Methods)

    - [생성자](#Constructors)

    - [종료자](#Finalizers)

    - [이벤트](#Events)

    - [중첩 클래스](#NestedClasses)

  - [액세스 한정자 및 액세스 수준](#AccessModifiers)

  - [클래스 인스턴스화](#InstantiatingClasses)

  - [정적 클래스 및 멤버](#Static)

  - [익명 형식](#AnonymousTypes)

- [상속](#Inheritance)

  - [멤버 재정의](#Overriding)

- [인터페이스](#Interfaces)

- [제네릭](#Generics)

- [대리자](#Delegates)

## <a name="Classes"></a> 클래스 및 개체

*클래스*와 *개체*를 혼용하는 경우가 있지만 클래스는 개체의 *형식*을 나타내고 개체는 사용 가능한 클래스의 *인스턴스*를 나타냅니다. 따라서 개체를 만드는 작업을 *인스턴스화*라고 합니다. 청사진에 비유한다면 클래스는 청사진이고 개체는 해당 청사진을 사용하여 만든 빌딩입니다.

클래스를 정의하려면

```csharp
class SampleClass
{
}
```

C#에서는 큰 개체 배열을 만들어야 하는데 메모리는 많이 사용하지 않으려는 경우에 유용한 라이브 버전의 클래스를 제공합니다. 이를 *구조체*라고 합니다.

구조체를 정의하려면

```csharp
struct SampleStruct
{
}
```

자세한 내용은 다음을 참조하세요.

- [class](../../language-reference/keywords/class.md)

- [struct](../../language-reference/keywords/struct.md)

### <a name="Members"></a> 클래스 멤버

각 클래스에는 클래스 데이터를 설명하는 속성, 클래스 동작을 정의하는 메서드 및 서로 다른 클래스와 개체 간의 통신을 제공하는 이벤트가 포함된 다양한 *클래스 멤버*가 있을 수 있습니다.

#### <a name="Properties"></a> 속성 및 필드

필드 및 속성은 개체가 포함하는 정보를 나타냅니다. 필드는 직접 읽거나 설정할 수 있기 때문에 변수와 비슷합니다.

필드를 정의하려면

```csharp
class SampleClass
{
    public string sampleField;
}
```

속성에는 값을 설정하고 가져오는 방법을 보다 세밀하게 제어할 수 있는 get 및 set 프로시저가 있습니다.

C#에서는 속성 값을 저장하기 위한 전용 필드를 만들거나 이 필드를 내부적으로 자동으로 만들고 속성 프로시저에 대한 기본 논리를 제공하는 자동 구현 속성을 사용할 수 있습니다.

자동 구현 속성을 정의하려면

```csharp
class SampleClass
{
    public int SampleProperty { get; set; }
}
```

속성 값을 읽고 쓰기 위해 몇 가지 추가 작업을 수행해야 하는 경우 다음과 같이 속성 값을 저장하기 위한 필드를 정의하고, 속성 값을 저장 및 검색하기 위한 기본 논리를 제공합니다.

```csharp
class SampleClass
{
    private int _sample;
    public int Sample
    {
        // Return the value stored in a field.
        get { return _sample; }
        // Store the value in the field.
        set { _sample = value; }
    }
}
```

대부분의 속성에는 속성 값을 설정하고 가져오는 메서드나 프로시저가 있습니다. 그러나 읽기 전용 또는 쓰기 전용 속성을 만들어 속성을 수정하거나 읽지 못하도록 제한할 수도 있습니다. C#에서는 `get` 또는 `set` 속성 메서드를 생략하면 됩니다. 하지만 자동 구현 속성은 읽기 전용 또는 쓰기 전용일 수 없습니다.

자세한 내용은 다음을 참조하세요.

- [get](../../language-reference/keywords/get.md)

- [set](../../language-reference/keywords/set.md)

#### <a name="Methods"></a> 메서드

*메서드*는 개체에서 수행할 수 있는 작업입니다.

클래스의 메서드를 정의하려면

```csharp
class SampleClass
{
    public int sampleMethod(string sampleParam)
    {
        // Insert code here
    }
}
```

클래스에는 매개 변수 개수나 매개 변수 형식이 다른 동일한 메서드의 구현 또는 *오버로드*가 여러 개 있을 수 있습니다.

메서드를 오버로드하려면

```csharp
public int sampleMethod(string sampleParam) {};
public int sampleMethod(int sampleParam) {}
```

대부분의 경우 클래스 정의 내에서 메서드를 선언하지만 C#에서는 클래스의 실제 정의 밖에 있는 기존 클래스에 메서드를 추가할 수 있는 *확장 메서드*도 지원합니다.

자세한 내용은 다음을 참조하세요.

- [메서드](../classes-and-structs/methods.md)

- [확장명 메서드](../classes-and-structs/extension-methods.md)

#### <a name="Constructors"></a> 생성자

생성자는 지정된 형식의 개체를 만들 때 자동으로 실행되는 클래스 메서드로, 일반적으로 새 개체의 데이터 멤버를 초기화합니다. 생성자는 클래스를 만들 때 한 번만 실행할 수 있습니다. 또한 생성자의 코드는 항상 클래스의 다른 코드보다 먼저 실행됩니다. 그러나 다른 메서드를 만들 때와 동일한 방법으로 여러 생성자 오버로드를 만들 수 있습니다.

클래스의 생성자를 정의하려면

```csharp
public class SampleClass
{
    public SampleClass()
    {
        // Add code here
    }
}
```

자세한 내용은 다음을 참조하세요.

[생성자](../classes-and-structs/constructors.md).

#### <a name="Finalizers"></a> 종료자

종료자는 클래스의 인스턴스를 소멸하는 데 사용됩니다. .NET Framework에서는 애플리케이션의 관리되는 개체에 대해 가비지 수집기가 자동으로 메모리를 할당하고 해제하지만 애플리케이션이 만드는 관리되지 않는 리소스를 정리하려면 여전히 종료자가 필요할 수 있습니다. 각 클래스에는 종료자가 하나씩만 있을 수 있습니다.

.NET Framework의 종료자 및 가비지 수집에 대한 자세한 내용은 [가비지 수집](../../../standard/garbage-collection/index.md)을 참조하세요.

#### <a name="Events"></a> 이벤트

클래스나 개체에서는 특정 상황이 발생할 때 이벤트를 통해 다른 클래스나 개체에 이를 알려 줄 수 있습니다. 이벤트를 보내거나 발생시키는 클래스를 *게시자*라고 하며 이벤트를 받거나 처리하는 클래스를 *구독자*라고 합니다. 이벤트를 발생시키고 처리하는 방법에 대한 자세한 내용은 [이벤트](../../../standard/events/index.md)를 참조하세요.

- 클래스에서 이벤트를 선언하려면 [event](../../language-reference/keywords/event.md) 키워드를 사용합니다.

- 이벤트를 발생시키려면 이벤트 대리자를 호출합니다.

- 이벤트를 구독하려면 `+=` 연산자를 사용하고 이벤트를 구독 취소하려면 `-=` 연산자를 사용합니다.

#### <a name="NestedClasses"></a> 중첩 클래스

다른 클래스 내에 정의된 클래스를 *중첩 클래스*라고 합니다. 기본적으로 중첩 클래스는 전용입니다.

```csharp
class Container
{
    class Nested
    {
        // Add code here.
    }
}
```

중첩 클래스의 인스턴스를 만들려면 다음과 같이 컨테이너 클래스의 이름, 점, 중첩 클래스의 이름을 차례로 입력합니다.

```csharp
Container.Nested nestedInstance = new Container.Nested()
```

### <a name="AccessModifiers"></a> 액세스 한정자 및 액세스 수준

모든 클래스 및 클래스 멤버는 *액세스 한정자*를 사용하여 다른 클래스에 제공할 액세스 수준을 지정할 수 있습니다.

다음과 같은 액세스 한정자를 사용할 수 있습니다.

|C# 한정자|정의|
|------------------|----------------|
|[public](../../language-reference/keywords/public.md)|동일한 어셈블리의 다른 코드나 해당 어셈블리를 참조하는 다른 어셈블리의 코드에서 형식이나 멤버에 액세스할 수 있습니다.|
|[private](../../language-reference/keywords/private.md)|동일한 클래스의 코드에서만 형식이나 멤버에 액세스할 수 있습니다.|
|[protected](../../language-reference/keywords/protected.md)|동일한 클래스의 코드나 파생 클래스의 코드에서만 형식이나 멤버에 액세스할 수 있습니다.|
|[internal](../../language-reference/keywords/internal.md)|동일한 어셈블리의 코드에서는 형식이나 멤버에 액세스할 수 있지만 다른 어셈블리의 코드에서는 액세스할 수 없습니다.|
|[protected internal](../../language-reference/keywords/protected-internal.md)|동일한 어셈블리의 코드 또는 다른 어셈블리의 파생 클래스에서 형식이나 멤버에 액세스할 수 있습니다.|
|[private protected](../../language-reference/keywords/private-protected.md)|기본 클래스 어셈블리 내 동일한 클래스 또는 파생 클래스의 코드에서 형식이나 멤버에 액세스할 수 있습니다.|

자세한 내용은 [액세스 한정자](../classes-and-structs/access-modifiers.md)를 참조하세요.

### <a name="InstantiatingClasses"></a> 클래스 인스턴스화

개체를 만들려면 클래스를 인스턴스화하거나 클래스 인스턴스를 만들어야 합니다.

```csharp
SampleClass sampleObject = new SampleClass();
```

클래스를 인스턴스화한 후에는 인스턴스의 속성과 필드에 값을 할당하고 클래스 메서드를 호출할 수 있습니다.

```csharp
// Set a property value.
sampleObject.sampleProperty = "Sample String";
// Call a method.
sampleObject.sampleMethod();
```

클래스를 인스턴스화하는 동안 속성에 값을 할당하려면 다음과 같이 개체 이니셜라이저를 사용합니다.

```csharp
// Set a property value.
SampleClass sampleObject = new SampleClass
    { FirstProperty = "A", SecondProperty = "B" };
```

자세한 내용은 다음을 참조하세요.

- [new 연산자](../../language-reference/operators/new-operator.md)

- [개체 이니셜라이저 및 컬렉션 이니셜라이저](../classes-and-structs/object-and-collection-initializers.md)

### <a name="Static"></a> 정적 클래스 및 멤버

클래스의 정적 멤버는 클래스의 모든 인스턴스에서 공유하는 속성, 프로시저 또는 필드입니다.

정적 멤버를 정의하려면

```csharp
static class SampleClass
{
    public static string SampleString = "Sample String";
}
```

정적 멤버에 액세스하려면 다음과 같이 이 클래스의 개체를 만들지 않고 클래스 이름을 사용합니다.

```csharp
Console.WriteLine(SampleClass.SampleString);
```

C#의 정적 클래스는 정적 멤버만 포함하며 인스턴스화할 수 없습니다. 또한 정적 멤버는 비정적 속성, 필드 또는 메서드에 액세스할 수 없습니다.

자세한 내용은 [static](../../language-reference/keywords/static.md)을 참조하세요.

### <a name="AnonymousTypes"></a> 무명 형식

익명 형식을 사용하면 데이터 형식에 대한 클래스 정의를 작성하지 않고 개체를 만들 수 있습니다. 대신 컴파일러가 클래스를 생성합니다. 이 클래스는 사용할 수 있는 이름이 없고 개체를 선언할 때 지정하는 속성을 포함합니다.

익명 형식의 인스턴스를 만들려면

```csharp
// sampleObject is an instance of a simple anonymous type.
var sampleObject =
    new { FirstProperty = "A", SecondProperty = "B" };
```

자세한 내용은 다음을 참조하세요. [익명 형식](../classes-and-structs/anonymous-types.md)을 참조하세요.

## <a name="Inheritance"></a> 상속

상속을 사용하면 다른 클래스에 정의된 동작을 다시 사용, 확장 및 수정하는 새 클래스를 만들 수 있습니다. 멤버가 상속되는 클래스를 *기본 클래스*라고 하고 해당 멤버를 상속하는 클래스를 *파생 클래스*라고 합니다. 그러나 C#의 모든 클래스는 .NET 클래스 계층 구조를 지원하고 모든 클래스에 하위 수준 서비스를 제공하는 <xref:System.Object> 클래스에서 암시적으로 상속됩니다.

> [!NOTE]
> C#은 다중 상속을 지원하지 않습니다. 즉, 파생된 클래스에 대해 하나의 기본 클래스만 지정할 수 있습니다.

기본 클래스에서 상속하려면

```csharp
class DerivedClass:BaseClass {}
```

기본적으로 모든 클래스는 상속될 수 있지만 클래스가 기본 클래스로 사용되지 않아야 하는지 여부를 지정하거나 기본 클래스로만 사용될 수 있는 클래스를 만들 수도 있습니다.

클래스가 기본 클래스로 사용될 수 없도록 지정하려면

```csharp
public sealed class A { }
```

클래스가 기본 클래스로만 사용되고 인스턴스화되지 않도록 지정하려면

```csharp
public abstract class B { }
```

자세한 내용은 다음을 참조하세요.

- [sealed](../../language-reference/keywords/sealed.md)

- [abstract](../../language-reference/keywords/abstract.md)

### <a name="Overriding"></a> 멤버 재정의

기본적으로 파생 클래스는 해당 기본 클래스에서 모든 멤버를 상속합니다. 상속된 멤버의 동작을 변경하려면 해당 멤버를 재정의해야 합니다. 즉, 파생 클래스에 해당 메서드, 속성 또는 이벤트의 새로운 구현을 정의할 수 있습니다.

다음 한정자는 속성 및 메서드가 재정의되는 방식을 제어하는 데 사용됩니다.

|C# 한정자|정의|
|------------------|----------------|
|[virtual](../../language-reference/keywords/virtual.md)|파생 클래스에서 클래스 멤버를 재정의할 수 있도록 합니다.|
|[override](../../language-reference/keywords/override.md)|기본 클래스에 정의된 가상(재정의 가능) 멤버를 재정의합니다.|
|[abstract](../../language-reference/keywords/abstract.md)|파생 클래스에서 클래스 멤버가 재정의되도록 합니다.|
|[new 한정자](../../language-reference/keywords/new-modifier.md)|기본 클래스에서 상속된 멤버를 숨깁니다.|

## <a name="Interfaces"></a> 인터페이스

인터페이스는 클래스와 마찬가지로 속성, 메서드 및 이벤트를 정의하지만 클래스와는 달리 구현을 제공하지 않습니다. 인터페이스는 클래스에 의해 구현되며 클래스와는 별개의 엔터티로 정의됩니다. 인터페이스는 계약을 나타내므로 인터페이스를 구현하는 클래스에서는 해당 인터페이스의 모든 부분을 정의된 그대로 정확하게 구현해야 합니다.

인터페이스를 정의하려면

```csharp
interface ISampleInterface
{
    void doSomething();
}
```

클래스에서 인터페이스를 구현하려면

```csharp
class SampleClass : ISampleInterface
{
    void ISampleInterface.doSomething()
    {
        // Method implementation.
    }
}
```

자세한 내용은 다음을 참조하세요.

[인터페이스](../interfaces/index.md)

[interface](../../language-reference/keywords/interface.md)

## <a name="Generics"></a> 제네릭

.NET Framework의 클래스, 구조체, 인터페이스 및 메서드는 저장하거나 사용할 수 있는 개체의 형식을 정의하는 *형식 매개 변수*를 포함할 수 있습니다. 제네릭의 가장 일반적인 예는 컬렉션에 저장할 개체의 형식을 지정할 수 있는 컬렉션입니다.

제네릭 클래스를 정의하려면

```csharp
public class SampleGeneric<T>
{
    public T Field;
}
```

제네릭 클래스의 인스턴스를 만들려면

```csharp
SampleGeneric<string> sampleObject = new SampleGeneric<string>();
sampleObject.Field = "Sample string";
```

자세한 내용은 다음을 참조하세요.

- [제네릭](../../../standard/generics/index.md)

- [제네릭](../generics/index.md)

## <a name="Delegates"></a> 대리자

*대리자*는 메서드 시그니처를 정의하는 형식으로, 호환되는 시그니처가 있는 모든 메서드에 대한 참조를 제공할 수 있습니다. 대리자를 통해 메서드를 호출할 수 있습니다. 대리자는 메서드를 다른 메서드에 인수로 전달하는 데 사용됩니다.

> [!NOTE]
> 이벤트 처리기는 대리자를 통해 호출되는 메서드라고 할 수 있습니다. 이벤트를 처리할 때 대리자를 사용하는 방법에 대한 자세한 내용은 [이벤트](../../../standard/events/index.md)를 참조하세요.

대리자를 만들려면

```csharp
public delegate void SampleDelegate(string str);
```

대리자가 지정한 시그니처와 일치하는 메서드에 대한 참조를 만들려면

```csharp
class SampleClass
{
    // Method that matches the SampleDelegate signature.
    public static void sampleMethod(string message)
    {
        // Add code here.
    }
    // Method that instantiates the delegate.
    void SampleDelegate()
    {
        SampleDelegate sd = sampleMethod;
        sd("Sample string");
    }
}
```

자세한 내용은 다음을 참조하세요.

- [대리자](../delegates/index.md)

- [delegate](../../language-reference/keywords/delegate.md)

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
