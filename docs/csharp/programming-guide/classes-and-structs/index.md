---
title: 클래스 및 구조체 - C# 프로그래밍 가이드
ms.custom: seodec18
description: C#의 클래스 및 구조(구조체) 사용에 대해 설명합니다.
ms.date: 01/17/2016
helpviewer_keywords:
- structs [C#], about structs
- classes [C#], overview
- C# language, structs
- C# language, objects
- objects [C#]
- C# language, classes
ms.assetid: cc39dbda-8754-423e-b5b1-16a1db0734c0
ms.openlocfilehash: c0b7e52cbbf0b49dee3598239f96e113ba929a80
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922265"
---
# <a name="classes-and-structs-c-programming-guide"></a>클래스 및 구조체(C# 프로그래밍 가이드)
클래스와 구조체는 .NET Framework의 공용 형식 시스템의 기본 구문 중 두 가지입니다. 각각은 기본적으로 하나의 논리 단위에 속하는 데이터 및 동작 집합을 캡슐화하는 데이터 구조입니다. 데이터 및 동작은 클래스 또는 구조체의 *멤버*로, 이 항목의 뒷부분에 나오는 것처럼 메서드, 속성 및 이벤트 등을 포함합니다.  
  
 클래스 또는 구조체 선언은 런타임에 인스턴스 또는 개체를 만드는 데 사용되는 청사진과도 같습니다. `Person`이라고 하는 클래스 또는 구조체를 정의하는 경우 `Person`이 형식의 이름입니다. 형식 `Person`의 변수 `p`를 선언하고 초기화하면 `p`는 `Person`의 개체 또는 인스턴스로 지칭됩니다. 같은 `Person` 형식의 여러 인스턴스를 만들 수 있으며 각 인스턴스는 속성 및 필드에 서로 다른 값을 가질 수 있습니다.  
  
 클래스는 참조 형식입니다. 클래스의 개체가 만들어지면 개체가 할당되는 변수는 해당 메모리에 대한 참조만 보유합니다. 개체 참조가 새 변수에 할당되면 새 변수는 원래 개체를 나타냅니다. 모두 동일한 데이터를 참조하므로 한 변수의 변경 내용이 다른 변수에도 반영됩니다.  
  
 구조체는 값 형식입니다. 구조체가 만들어지면 해당 구조체가 할당되는 변수에 구조체의 실제 데이터가 포함됩니다. 구조체를 새 변수에 할당하면 구조체가 복사됩니다. 따라서 새 변수와 원래 변수에 동일한 데이터의 두 가지 별도 복사본이 포함됩니다. 한 복사본의 변경 내용은 다른 복사본에 영향을 주지 않습니다.  
  
 일반적으로 클래스는 좀 더 복잡한 동작이나 클래스 개체를 만든 후 수정하려는 데이터를 모델링하는 데 사용됩니다. 구조체는 구조체를 만든 후에 수정하지 않으려는 데이터를 주로 포함하는 작은 데이터 구조에 가장 적합합니다.  
  
 자세한 내용은 [클래스](./classes.md), [개체](./objects.md) 및 [구조체](./structs.md)를 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제에서 `ProgrammingGuide` 네임스페이스의 `CustomClass`에는 세 개의 멤버, 즉 인스턴스 생성자, `Number`라는 속성 및 `Multiply`이라는 메서드가 있습니다. `Program` 클래스의 `Main` 메서드는 `CustomClass`의 인스턴스(개체)를 만들고 개체의 메서드 및 속성은 점 표기법을 사용하여 액세스됩니다.
  
 [!code-csharp[csProgGuideObjects#1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/class1.cs#1)]  
  
## <a name="encapsulation"></a>캡슐화  
 *캡슐화*는 경우에 따라 개체 지향 프로그래밍의 첫 번째 pillar 또는 원리로 인식됩니다. 캡슐화의 원리에 따라 클래스 또는 구조체는 클래스 또는 구조체 외부의 코드에 각 멤버가 액세스하는 방법을 지정할 수 있습니다. 코딩 오류 또는 악의적인 악용 가능성을 제한하려면 클래스 또는 어셈블리 외부에서 사용하지 않으려는 메서드 및 변수는 숨길 수 있습니다.  
  
 클래스에 대한 자세한 내용은 [클래스](./classes.md) 및 [개체](./objects.md)를 참조하세요.  
  
### <a name="members"></a>멤버  
 모든 메서드, 필드, 상수, 속성 및 이벤트는 형식 내에서 선언되어야 합니다. 이것을 형식의 *멤버*라고 합니다. 다른 언어에는 있지만 C#에는 전역 변수 또는 메서드가 없습니다. 프로그램의 진입점인 `Main` 메서드까지도 클래스 또는 구조체 내에서 선언되어야 합니다. 다음은 클래스 또는 구조체에서 선언될 수 있는 모든 다양한 종류의 멤버입니다.  
  
- [필드](./fields.md)  
  
- [상수](./constants.md)  
  
- [속성](./properties.md)  
  
- [메서드](./methods.md)  
  
- [생성자](./constructors.md)  
  
- [이벤트](../events/index.md)  
  
- [종료자](./destructors.md)  
  
- [인덱서](../indexers/index.md)  
  
- [연산자](../../language-reference/operators/index.md)  
  
- [중첩 형식](./nested-types.md)  
  
### <a name="accessibility"></a>액세스 가능성  
 일부 메서드 및 속성은 *클라이언트 코드*라고 하는 클래스 또는 구조체 외부의 코드에서 호출하거나 액세스할 수 있습니다. 다른 메서드 및 속성은 클래스 또는 구조체 자체에서만 사용할 수 있습니다. 의도된 클라이언트 코드에서만 연결될 수 있도록 코드의 액세스 가능성을 제한하는 것이 중요합니다. 형식 및 해당 멤버가 클라이언트 코드에 액세스하는 방법은 액세스 한정자 [public](../../language-reference/keywords/public.md), [protected](../../language-reference/keywords/protected.md), [internal](../../language-reference/keywords/internal.md), [protected internal](../../language-reference/keywords/protected-internal.md), [private](../../language-reference/keywords/private.md) 및 [private protected](../../language-reference/keywords/private-protected.md)를 사용하여 지정합니다. 기본 액세스 가능성은 `private`입니다. 자세한 내용은 [액세스 한정자](./access-modifiers.md)를 참조하세요.  
  
### <a name="inheritance"></a>상속  
 클래스(구조체는 아님)는 상속 개념을 지원합니다. 다른 클래스(*기본 클래스*)에서 파생되는 클래스는 생성자와 종료자를 제외하고 기본 클래스의 모든 public, protected 및 internal 멤버를 자동으로 포함합니다. 자세한 내용은 [상속](./inheritance.md) 및 [다형성](./polymorphism.md)을 참조하세요.  
  
 클래스를 [abstract](../../language-reference/keywords/abstract.md)로 선언할 수도 있습니다. 즉, 하나 이상의 해당 메서드에 구현이 없는 상태를 의미합니다. 추상 클래스는 직접 인스턴스화할 수 없지만 누락된 구현을 제공하는 다른 클래스에 대한 기본 클래스로 사용될 수 있습니다. 다른 클래스가 이 클래스에서 상속 받지 못하게 하려면 클래스를 [sealed](../../language-reference/keywords/sealed.md)로 선언할 수도 있습니다. 자세한 내용은 [Abstract 및 Sealed 클래스와 클래스 멤버](./abstract-and-sealed-classes-and-class-members.md)를 참조하세요.  
  
### <a name="interfaces"></a>인터페이스  
 클래스 및 구조체는 여러 인터페이스에서 상속할 수 있습니다. 인터페이스에서 상속하는 것은 형식이 해당 인터페이스에 정의된 모든 메서드를 구현한다는 것입니다. 자세한 내용은 [인터페이스](../interfaces/index.md)를 참조하세요.  
  
### <a name="generic-types"></a>제네릭 형식  
 하나 이상의 형식 매개 변수를 사용하여 클래스 및 구조체를 정의할 수 있습니다. 클라이언트 코드는 형식의 인스턴스를 만들 때 형식을 제공합니다. 예를 들어 <xref:System.Collections.Generic> 네임스페이스의 <xref:System.Collections.Generic.List%601> 클래스는 하나의 형식 매개 변수로 정의됩니다. 클라이언트 코드는 `List<string>` 또는 `List<int>`의 인스턴스를 만들어 목록에 포함될 형식을 지정합니다. 자세한 내용은 [제네릭](../generics/index.md)을 참조하세요.  
  
### <a name="static-types"></a>정적 형식  
 클래스(구조체는 아님)를 [static](../../language-reference/keywords/static.md)으로 선언할 수 있습니다. static 클래스는 static 멤버만 포함할 수 있고 new 키워드로 인스턴스화할 수 없습니다. 프로그램이 로드될 때 클래스의 단일 복사본만 메모리에 로드되고 해당 멤버는 클래스 이름을 통해 액세스됩니다. 클래스와 구조체 둘 다 정적 멤버를 포함할 수 있습니다. 자세한 내용은 [static 클래스 및 static 클래스 멤버](./static-classes-and-static-class-members.md)를 참조하세요.  
  
### <a name="nested-types"></a>중첩 형식  
 클래스 또는 구조체는 다른 클래스 또는 구조체 내에 중첩될 수 있습니다. 자세한 내용은 [중첩 형식](./nested-types.md)을 참조하세요.  
  
### <a name="partial-types"></a>부분 형식(Partial Type)  
 하나의 코드 파일 및 별도 코드 파일의 다른 부분에서 클래스, 구조체 또는 메서드의 부분을 정의할 수 있습니다. 자세한 내용은 [Partial 클래스 및 메서드](./partial-classes-and-methods.md)를 참조하세요.  
  
### <a name="object-initializers"></a>개체 이니셜라이저  
 해당 생성자를 명시적으로 호출하지 않고 클래스 또는 구조체 개체, 개체 컬렉션을 인스턴스화하고 초기화할 수 있습니다. 자세한 내용은 [개체 및 컬렉션 이니셜라이저](./object-and-collection-initializers.md)를 참조하세요.  
  
### <a name="anonymous-types"></a>익명 형식  
 유지하거나 다른 메서드에 전달할 필요가 없는 데이터 구조로 목록을 채우는 경우처럼 명명된 클래스를 만드는 것이 불편하거나 필요하지 않은 상황에서는 무명 형식을 사용합니다. 자세한 내용은 [무명 형식](./anonymous-types.md)을 참조하세요.  
  
### <a name="extension-methods"></a>확장명 메서드  
 마치 원래 형식에 속하는 것처럼 해당 메서드를 호출할 수 있는 별도 형식을 만들면 파생 클래스를 만들지 않고도 클래스를 “확장”할 수 있습니다. 자세한 내용은 [확장 메서드](./extension-methods.md)를 참조하세요.  
  
### <a name="implicitly-typed-local-variables"></a>암시적으로 형식화한 지역 변수  
 클래스 또는 구조체 메서드 내에서 암시적 형식 지정을 사용하여 컴파일러가 컴파일 타임에 올바른 형식을 결정하도록 할 수 있습니다. 자세한 내용은 [암시적으로 형식화된 지역 변수](./implicitly-typed-local-variables.md)를 참조하세요.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
