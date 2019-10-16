---
title: 클래스 - C# 프로그래밍 가이드
ms.custom: seodec18
description: 클래스 형식 및 이를 만드는 방법을 자세히 알아봅니다.
ms.date: 08/21/2018
helpviewer_keywords:
- classes [C#]
- C# language, classes
ms.assetid: e8848524-7273-429f-8aba-c658d5eff5ad
ms.openlocfilehash: 193446ff98edce3b7c078c6eeba07cf9acdadaf0
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597182"
---
# <a name="classes-c-programming-guide"></a>클래스(C# 프로그래밍 가이드)

## <a name="reference-types"></a>참조 형식  
[클래스](../../language-reference/keywords/class.md)로 정의된 형식은 *참조 형식*입니다. 런타임에 참조 형식의 변수를 선언하면 [new](../../language-reference/operators/new-operator.md) 연산자를 사용하여 클래스의 인스턴스를 명시적으로 만들거나 다음 예제와 같이 다른 곳에서 만들어진 호환성 있는 형식의 개체를 할당할 때까지 변수에는 [null](../../language-reference/keywords/null.md) 값이 포함됩니다.

```csharp
//Declaring an object of type MyClass.
MyClass mc = new MyClass();

//Declaring another object of the same type, assigning it the value of the first object.
MyClass mc2 = mc;
```

개체가 만들어지면 해당 특정 개체에 대해 관리되는 힙에 충분한 메모리가 할당되고 변수에는 개체 위치에 대한 참조만 포함됩니다. 관리되는 힙의 형식은 할당될 때, 그리고 *가비지 수집*이라는 CLR의 자동 메모리 관리 기능에 의해 회수될 때 오버헤드가 필요합니다. 그러나 가비지 수집은 고도로 최적화되고 대부분 시나리오에서 성능 문제를 일으키지 않습니다. 가비지 수집에 대한 자세한 내용은 [자동 메모리 관리 및 가비지 수집](../../../standard/garbage-collection/gc.md)을 참조하세요.  
  
## <a name="declaring-classes"></a>클래스 선언

 클래스는 다음 예제와 같이 [class](../../language-reference/keywords/class.md) 키워드 다음에 고유 식별자를 사용하여 선언됩니다.

 ```csharp
//[access modifier] - [class] - [identifier]
 public class Customer
 {
    // Fields, properties, methods and events go here...
 }
```

 `class` 키워드는 액세스 수준 뒤에 옵니다. 이 경우 [public](../../language-reference/keywords/public.md)이 사용되므로 누구나 이 클래스의 인스턴스를 만들 수 있습니다. 클래스 이름은 `class` 키워드 뒤에 옵니다. 클래스의 이름은 유효한 C# [식별자 이름](../inside-a-program/identifier-names.md)이어야 합니다. 정의의 나머지 부분은 동작과 데이터가 정의되는 클래스 본문입니다. 클래스의 필드, 속성, 메서드 및 이벤트를 모두 *클래스 멤버*라고 합니다.  
  
## <a name="creating-objects"></a>개체 만들기

클래스와 개체는 바꿔 사용되기도 하지만 서로 다른 항목입니다. 클래스는 개체의 형식을 정의하지만 개체 자체는 아닙니다. 개체는 클래스에 기반을 둔 구체적 엔터티이고 클래스의 인스턴스라고도 합니다.  
  
 개체를 만들려면 다음과 같이 [new](../../language-reference/operators/new-operator.md) 키워드 뒤에 개체의 기반이 되는 클래스의 이름을 사용합니다.  

 ```csharp
 Customer object1 = new Customer();
 ```

 클래스 인스턴스가 만들어질 때 개체에 대한 참조가 다시 프로그래머에게 전달됩니다. 이전 예제에서 `object1`은 `Customer`에 기반을 둔 개체에 대한 참조입니다. 이 참조는 새 개체를 참조하지만 개체 데이터 자체를 포함하지 않습니다. 실제로 개체를 만들지 않고도 개체 참조를 만들 수 있습니다.  
 
```csharp
 Customer object2;
```
 
 런타임에는 참조를 통한 개체 액세스 시도에 실패하므로 개체를 참조하지 않는 이와 같은 개체 참조는 만들지 않는 것이 좋습니다. 그러나 새 개체를 만들거나 다음과 같이 기존 개체에 개체를 할당하여 개체를 참조하는 참조를 만들 수 있습니다.  

 ```csharp
 Customer object3 = new Customer();
 Customer object4 = object3;
```
  
 이 코드에서는 같은 개체를 참조하는 두 개의 개체 참조를 만듭니다. 따라서 `object3`을 통해 이루어진 모든 개체 변경 내용은 이후 `object4` 사용 시 반영됩니다. 클래스에 기반을 둔 개체는 참조를 통해 참조되므로 클래스를 참조 형식이라고 합니다.  
  
## <a name="class-inheritance"></a>클래스 상속  

클래스는 개체 지향 프로그래밍의 기본적인 특성인 ‘상속’을 완전히 지원합니다.  클래스를 만들 때 [sealed](../../language-reference/keywords/sealed.md)로 정의되지 않은 기타 인터페이스 또는 클래스에서 상속될 수 있고 기타 클래스는 직접 만든 클래스에서 상속되고 클래스 가상 메서드를 재정의할 수 있습니다.

상속은 *파생*을 통해 수행합니다. 즉, 클래스는 데이터와 동작을 상속하는 소스 *기본 클래스*를 사용하여 선언됩니다. 다음과 같이 파생 클래스 이름 뒤에 콜론 및 기본 클래스 이름을 추가하여 기본 클래스를 지정합니다.  

 ```csharp
 public class Manager : Employee
 {
     // Employee fields, properties, methods and events are inherited
     // New Manager fields, properties, methods and events go here...
 }
 ```

기본 클래스를 선언하는 클래스는 생성자를 제외하고 기본 클래스의 모든 멤버를 상속합니다. 자세한 내용은 [상속](inheritance.md)을 참조하세요.
  
C++와 달리 C#의 클래스는 하나의 기본 클래스에서만 직접 상속될 수 있습니다. 그러나 기본 클래스 자체는 다른 클래스에서 상속될 수 있으므로 클래스는 여러 기본 클래스를 간접적으로 상속할 수 있습니다. 게다가 클래스는 두 개 이상의 인터페이스를 직접 구현할 수 있습니다. 자세한 내용은 [인터페이스](../interfaces/index.md)를 참조하세요.  
  
클래스는 [abstract](../../language-reference/keywords/abstract.md)로 선언될 수 있습니다. 추상 클래스에는 시그니처 정의가 있지만 구현이 없는 추상 메서드가 포함됩니다. 추상 클래스는 인스턴스화할 수 없습니다. 추상 클래스는 추상 메서드를 구현하는 파생 클래스를 통해서만 사용할 수 있습니다. 이와 달리 [sealed](../../language-reference/keywords/sealed.md) 클래스에서는 다른 클래스가 파생될 수 없습니다. 자세한 내용은 [Abstract 및 Sealed 클래스와 클래스 멤버](abstract-and-sealed-classes-and-class-members.md)를 참조하세요.  
  
클래스 정의는 여러 소스 파일로 분할될 수 있습니다. 자세한 내용은 참조 [Partial 클래스 및 메서드](partial-classes-and-methods.md)합니다.  
  
## <a name="example"></a>예제

다음 예제에서는 [자동 구현 속성](auto-implemented-properties.md), 메서드 및 생성자라는 특수 메서드를 포함하는 공용 클래스를 정의합니다. 자세한 내용은 [속성](properties.md), [메서드](methods.md) 및 [생성자](constructors.md) 항목을 참조하세요. 그런 다음, 클래스의 인스턴스는 `new` 키워드를 사용하여 인스턴스화됩니다.  
  
[!code-csharp[Class Example](~/samples/snippets/csharp/programming-guide/classes-and-structs/class-example.cs)] 
  
## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [개체 지향 프로그래밍](../concepts/object-oriented-programming.md)
- [다형성](polymorphism.md)
- [식별자 이름](../inside-a-program/identifier-names.md)
- [멤버](members.md)
- [메서드](methods.md)
- [생성자](constructors.md)
- [종료자](destructors.md)
- [개체](objects.md)
