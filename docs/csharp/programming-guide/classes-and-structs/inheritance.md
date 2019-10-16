---
title: 상속 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- abstract methods [C#]
- abstract classes [C#]
- inheritance [C#]
- derived classes [C#]
- virtual methods [C#]
- C# language, inheritance
ms.assetid: 81d64ee4-50f9-4d6c-a8dc-257c348d2eea
ms.openlocfilehash: 3211a4741eb56ad9e138a848e52fabbc1d3daaeb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924467"
---
# <a name="inheritance-c-programming-guide"></a>상속(C# 프로그래밍 가이드)

캡슐화 및 다형성과 함께 상속은 개체 지향 프로그래밍의 세 가지 주요 특징 중 하나입니다. 상속을 사용하면 다른 클래스에 정의된 동작을 다시 사용, 확장 및 수정하는 새 클래스를 만들 수 있습니다. 멤버가 상속되는 클래스를 *기본 클래스*라고 하고 해당 멤버를 상속하는 클래스를 *파생 클래스*라고 합니다. 파생 클래스에는 직접적인 기본 클래스가 하나만 있을 수 있습니다. 그러나 상속은 전이됩니다. ClassC가 ClassB에서 파생되고 ClassB가 ClassA에서 파생되는 경우 ClassC는 ClassB 및 ClassA에 선언된 멤버를 상속합니다.  
  
> [!NOTE]
> 구조체는 상속을 지원하지 않지만 인터페이스를 구현할 수 있습니다. 자세한 내용은 [인터페이스](../interfaces/index.md)를 참조하세요.  
  
 파생 클래스는 개념적 측면에서 기본 클래스의 특수화입니다. 예를 들어 기본 클래스 `Animal`이 있는 경우 `Mammal`이라는 하나의 파생 클래스와 `Reptile`이라는 다른 파생 클래스가 있을 수 있습니다. `Mammal`은 `Animal`이고 `Reptile`은 `Animal`이지만 각 파생 클래스는 기본 클래스의 서로 다른 특수화를 나타냅니다.  
  
 다른 클래스에서 파생할 클래스를 정의하는 경우 파생 클래스는 해당 생성자와 종료자를 제외하고 기본 클래스의 모든 멤버를 암시적으로 얻게 됩니다. 따라서 파생 클래스는 다시 구현하지 않고도 기본 클래스의 코드를 다시 사용할 수 있습니다. 파생 클래스에서 더 많은 멤버를 추가할 수 있습니다. 이런 방식으로 파생 클래스는 기본 클래스의 기능을 확장합니다.  
  
 다음 그림은 일부 비즈니스 프로세스의 작업 항목을 나타내는 `WorkItem` 클래스를 보여 줍니다. 모든 클래스와 마찬가지로, <xref:System.Object?displayProperty=nameWithType>에서 파생되고 해당 메서드를 모두 상속합니다. `WorkItem`은 고유한 멤버 5개를 추가합니다. 생성자는 상속되지 않으므로 생성자도 여기에 포함됩니다. `ChangeRequest` 클래스는 `WorkItem`에서 상속되며 특정 종류의 작업 항목을 나타냅니다. `ChangeRequest`는 `WorkItem` 및 <xref:System.Object>에서 상속하는 멤버에 둘 이상의 멤버를 추가합니다. 고유한 생성자를 추가해야 하며, `originalItemID`도 추가합니다. `originalItemID` 속성을 사용하면 `ChangeRequest` 인스턴스를 변경 요청이 적용되는 원래 `WorkItem`에 연결할 수 있습니다.  
  
 ![클래스 상속을 보여 주는 다이어그램](./media/inheritance/class-inheritance-diagram.png)  
  
 다음 예제에서는 앞의 그림에서 보여 주는 클래스 관계가 C#에서 어떻게 표현되는지를 보여 줍니다. 또한 이 예제에서 `WorkItem`은 가상 메서드 <xref:System.Object.ToString%2A?displayProperty=nameWithType>을 재정의하는 방법과 `ChangeRequest` 클래스가 메서드의 `WorkItem` 구현을 상속하는 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideInheritance#49](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#49)]  
  
## <a name="abstract-and-virtual-methods"></a>추상 메서드 및 가상 메서드  
 기본 클래스가 메서드를 [virtual](../../language-reference/keywords/virtual.md)로 선언하는 경우 파생 클래스가 해당 구현으로 메서드를 [재정의](../../language-reference/keywords/override.md)할 수 있습니다. 기본 클래스가 멤버를 [abstract](../../language-reference/keywords/abstract.md)로 선언하는 경우 해당 클래스에서 직접 상속하는 모든 비추상 클래스에서 메서드를 재정의해야 합니다. 파생 클래스 자체가 abstract인 경우 직접 구현하지 않고 추상 멤버를 상속합니다. 추상 멤버 및 가상 멤버는 개체 지향 프로그래밍의 두 번째 주요 특징인 다형성의 기초가 됩니다. 자세한 내용은 [다형성](./polymorphism.md)을 참조하세요.  
  
## <a name="abstract-base-classes"></a>추상 기본 클래스  
 [new](../../language-reference/operators/new-operator.md) 연산자를 사용한 직접 인스턴스화를 방지하려는 경우 클래스를 [abstract](../../language-reference/keywords/abstract.md)로 선언할 수 있습니다. 이 작업을 수행하면 해당 클래스에서 새 클래스가 파생된 경우에만 클래스를 사용할 수 있습니다. 추상 클래스에는 그 자체가 abstract로 선언된 메서드 시그니처가 하나 이상 포함될 수 있습니다. 이러한 시그니처는 매개 변수와 반환 값을 지정하지만 구현(메서드 본문)이 없습니다. 추상 클래스는 추상 멤버를 포함하지 않아도 됩니다. 그러나 클래스에 추상 멤버가 포함되지 않은 경우 클래스 자체를 abstract로 선언해야 합니다. 그 자체가 추상이 아닌 파생 클래스는 추상 기본 클래스의 모든 추상 멤버에 대한 구현을 제공해야 합니다. 자세한 내용은 [Abstract 및 Sealed 클래스와 클래스 멤버](./abstract-and-sealed-classes-and-class-members.md)를 참조하세요.  
  
## <a name="interfaces"></a>인터페이스  
 *인터페이스*는 추상 멤버로만 구성된 추상 기본 클래스와 비슷한 참조 형식입니다. 클래스에서 인터페이스를 구현하는 경우 인터페이스의 모든 멤버에 대해 구현을 제공해야 합니다. 하나의 직접 기본 클래스에서만 파생할 수 있는 경우에도 클래스에서 여러 인터페이스를 구현할 수 있습니다.  
  
 인터페이스는 "is a" 관계가 없을 수도 있는 클래스에 대해 특정 기능을 정의하는 데 사용됩니다. 예를 들어 <xref:System.IEquatable%601?displayProperty=nameWithType> 인터페이스는 클라이언트 코드에서 형식의 두 개체가 같은지 여부를 확인할 수 있도록 해야 하는 모든 클래스 또는 구조체에 의해 구현될 수 있습니다(그러나 형식이 동등성을 정의함). <xref:System.IEquatable%601>은 기본 클래스와 파생 클래스 간에 존재하는 동일한 종류의 "is a" 관계를 암시하지 않습니다(예: `Mammal`은 `Animal`임). 자세한 내용은 [인터페이스](../interfaces/index.md)를 참조하세요.  
  
## <a name="preventing-further-derivation"></a>추가 파생 방지  
 클래스는 자신이나 멤버를 [sealed](../../language-reference/keywords/sealed.md)로 선언하여 다른 클래스가 해당 클래스나 멤버에서 상속할 수 없도록 차단할 수 있습니다. 자세한 내용은 [추상 및 봉인 클래스와 클래스 멤버](./abstract-and-sealed-classes-and-class-members.md)를 참조하세요.  
  
## <a name="derived-class-hiding-of-base-class-members"></a>파생 클래스의 기본 클래스 멤버 숨기기  
 파생 클래스는 동일한 이름과 시그니처로 멤버를 선언하여 기본 클래스 멤버를 숨길 수 있습니다. [new](../../language-reference/keywords/new-modifier.md) 한정자를 사용하여 멤버가 기본 멤버를 재정의하지 않음을 명시적으로 나타내는 데 사용할 수 있습니다. [new](../../language-reference/keywords/new-modifier.md) 사용은 필수가 아니지만 [new](../../language-reference/keywords/new-modifier.md)를 사용하지 않을 경우 컴파일러 경고가 생성됩니다. 자세한 내용은 [Override 및 New 키워드를 사용하여 버전 관리](./versioning-with-the-override-and-new-keywords.md) 및 [Override 및 New 키워드를 사용해야 하는 경우](./knowing-when-to-use-override-and-new-keywords.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [class](../../language-reference/keywords/class.md)
- [struct](../../language-reference/keywords/struct.md)
