---
title: class 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/18/2017
f1_keywords:
- class_CSharpKeyword
- class
helpviewer_keywords:
- class keyword [C#]
ms.assetid: b95d8815-de18-4c3f-a8cc-a0a53bdf8690
ms.openlocfilehash: 0c4fc9645e43f23e340804b46bbe8a5faa19525d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922394"
---
# <a name="class-c-reference"></a>class(C# 참조)

클래스는 다음 예제와 같이 `class` 키워드를 사용하여 선언됩니다.

```csharp
class TestClass
{
    // Methods, properties, fields, events, delegates
    // and nested classes go here.
}
```

## <a name="remarks"></a>설명

C#에서는 단일 상속만 허용됩니다. 즉, 한 클래스는 하나의 기본 클래스에서만 구현을 상속할 수 있습니다. 그러나 한 클래스는 두 개 이상의 인터페이스를 구현할 수 있습니다. 다음 표에는 클래스 상속 및 인터페이스 구현에 대한 예제가 나와 있습니다.

|상속|예|
|-----------------|-------------|
|없음|`class ClassA { }`|
|Single|`class DerivedClass: BaseClass { }`|
|없음. 두 개의 인터페이스 구현|`class ImplClass: IFace1, IFace2 { }`|
|단일. 하나의 인터페이스 구현|`class ImplDerivedClass: BaseClass, IFace1 { }`|

다른 클래스 내에 중첩되는 것이 아니라 네임스페이스 내에서 직접 선언되는 클래스는 [public](./public.md) 또는 [internal](./internal.md)일 수 있습니다. 기본적으로 클래스는 `internal`입니다.

중첩 클래스를 포함한 클래스 멤버는 [public](public.md), [protected internal](protected-internal.md), [protected](protected.md), [internal](internal.md), [private](private.md) 또는 [private protected](private-protected.md)일 수 있습니다. 기본적으로 멤버는 `private`입니다.

자세한 내용은 [액세스 한정자](../../programming-guide/classes-and-structs/access-modifiers.md)를 참조하세요.

형식 매개 변수가 포함된 제네릭 클래스를 선언할 수 있습니다. 자세한 내용은 [제네릭 클래스](../../programming-guide/generics/generic-classes.md)를 참조하세요.

클래스에는 다음 멤버의 선언이 포함될 수 있습니다.

- [생성자](../../programming-guide/classes-and-structs/constructors.md)

- [상수](../../programming-guide/classes-and-structs/constants.md)

- [필드](../../programming-guide/classes-and-structs/fields.md)

- [종료자](../../programming-guide/classes-and-structs/destructors.md)

- [메서드](../../programming-guide/classes-and-structs/methods.md)

- [속성](../../programming-guide/classes-and-structs/properties.md)

- [인덱서](../../programming-guide/indexers/index.md)

- [연산자](../operators/index.md)

- [이벤트](../../programming-guide/events/index.md)

- [대리자](../../programming-guide/delegates/index.md)

- [클래스](../../programming-guide/classes-and-structs/classes.md)

- [인터페이스](../../programming-guide/interfaces/index.md)

- [구조체](../../programming-guide/classes-and-structs/structs.md)

- [열거형](../../programming-guide/enumeration-types.md)

## <a name="example"></a>예

다음 예제에서는 클래스 필드, 생성자 및 메서드를 선언하는 방법을 보여 줍니다. 또한 개체 인스턴스화 및 인스턴스 데이터 출력을 보여 줍니다. 이 예제에서는 두 개의 클래스가 선언됩니다. 첫 번째 클래스인 `Child`는 private 필드 2개(`name` 및 `age`), public 생성자 2개, public 메서드 1개를 포함합니다. 두 번째 클래스인 `StringTest`는 `Main`을 포함하는 데 사용됩니다.

[!code-csharp[csrefKeywordsTypes#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#5)]

## <a name="comments"></a>설명

이전 예제에서 private 필드(`name` 및 `age`)는 `Child` 클래스의 public 메서드를 통해서만 액세스할 수 있습니다. 예를 들어 다음과 같은 문을 사용하여 `Main` 메서드에서 자식의 이름을 출력할 수 없습니다.

```csharp
Console.Write(child1.name);   // Error
```

`Main`이 클래스의 멤버인 경우에만 `Main`에서 `Child`의 private 멤버에 액세스할 수 있습니다.

액세스 한정자 없이 클래스 내부에 선언된 형식은 기본적으로 `private`로 설정되므로 키워드가 제거된 경우 이 예제의 데이터 멤버는 `private`입니다.

마지막으로 매개 변수 없는 생성자(`child3`)를 사용하여 만들어진 개체의 경우 `age` 필드는 기본적으로 0으로 초기화되었습니다.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](./index.md)
- [참조 형식](./reference-types.md)
