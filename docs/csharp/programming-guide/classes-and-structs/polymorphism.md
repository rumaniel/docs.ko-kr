---
title: 다형성 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, polymorphism
- polymorphism [C#]
ms.assetid: 086af969-29a5-4ce8-a993-0b7d53839dab
ms.openlocfilehash: e98399ac49e70f9139281ab75947c4acaf2dee7c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922077"
---
# <a name="polymorphism-c-programming-guide"></a>다형성(C# 프로그래밍 가이드)
다형성은 흔히 캡슐화와 상속의 뒤를 이어 개체 지향 프로그래밍의 세 번째 특징으로 일컬어집니다. 다형성은 "여러 형태"를 의미하는 그리스어 단어이며 다음과 같은 두 가지 고유한 측면을 가집니다.  
  
- 런타임에 파생 클래스의 개체가 메서드 매개 변수 및 컬렉션 또는 배열과 같은 위치에서 기본 클래스의 개체로 처리될 수 있습니다. 이 경우 개체의 선언된 형식이 더 이상 해당 런타임 형식과 같지 않습니다.  
  
- 기본 클래스는 [가상](../../language-reference/keywords/virtual.md) *메서드*를 정의 및 구현할 수 있으며, 파생 클래스는 이러한 가상 메서드를 [재정의](../../language-reference/keywords/override.md)할 수 있습니다. 즉, 파생 클래스는 고유한 정의 및 구현을 제공합니다. 런타임에 클라이언트 코드에서 메서드를 호출하면 CLR은 개체의 런타임 형식을 조회하고 가상 메서드의 해당 재정의를 호출합니다. 따라서 소스 코드에서 기본 클래스에 대한 메서드를 호출하여 메서드의 파생 클래스 버전이 실행되도록 할 수 있습니다.  
  
 가상 메서드를 사용하면 동일한 방식으로 관련 개체 그룹에 대한 작업을 수행할 수 있습니다. 예를 들어, 사용자가 그리기 화면에서 다양한 종류의 도형을 만들 수 있는 그리기 애플리케이션이 있다고 가정합니다. 컴파일 타임에는 사용자가 어떤 특정 형식의 도형을 만들지 알 수 없습니다. 그러나 애플리케이션은 만들어지는 다양한 모든 형식의 도형을 추적해야 하며, 사용자의 마우스 작업에 따라 이러한 도형을 업데이트해야 합니다. 다음과 같은 기본 두 단계로 다형성을 사용하여 이 문제를 해결할 수 있습니다.  
  
1. 각 특정 도형 클래스가 공통 기본 클래스에서 파생되는 클래스 계층 구조를 만듭니다.  
  
2. 가상 메서드를 사용하여 기본 클래스 메서드에 대한 단일 호출을 통해 모든 파생 클래스에 대해 적절한 메서드를 호출합니다.  
  
 먼저, `Shape`라는 기본 클래스를 만들고 `Rectangle`, `Circle` 및 `Triangle`과 같은 파생 클래스를 만듭니다. `Shape` 클래스에 `Draw`라는 가상 메서드를 제공하고, 각 파생 클래스에서 이를 재정의하여 클래스가 나타내는 특정 도형을 그립니다. `List<Shape>` 개체를 만들고 이 개체에 Circle, Triangle 및 Rectangle을 추가합니다. 그리기 화면을 업데이트하려면 [foreach](../../language-reference/keywords/foreach-in.md) 루프를 사용하여 목록을 반복하고 목록의 각 `Shape` 개체에 대해 `Draw` 메서드를 호출합니다. 목록의 각 개체에 선언된 형식 `Shape`가 있더라도 이는 호출될 런타임 형식(각 파생 클래스에 있는 메서드의 재정의된 버전)입니다.  
  
 [!code-csharp[csProgGuideInheritance#50](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#50)]  
  
 C#에서 모든 형식은 사용자 정의 형식을 포함한 모든 형식이 <xref:System.Object>에서 파생되므로 다형 형식입니다.  
  
## <a name="polymorphism-overview"></a>다형성 개요  
  
### <a name="virtual-members"></a>가상 멤버  
 기본 클래스에서 파생 클래스가 상속되면 파생 클래스는 기본 클래스의 모든 메서드, 필드, 속성 및 이벤트를 얻습니다. 파생 클래스의 디자이너는 다음의 여부를 선택할 수 있습니다.  
  
- 기본 클래스의 가상 멤버 재정의  
  
- 가장 가까운 기본 클래스 메서드를 재정의하지 않고 상속  
  
- 기본 클래스 구현을 숨기는 해당 멤버의 새 비가상 구현 정의  
  
 파생 클래스는 기본 클래스 멤버가 [virtual](../../language-reference/keywords/virtual.md) 또는 [abstract](../../language-reference/keywords/abstract.md)로 선언된 경우에만 기본 클래스 멤버를 재정의할 수 있습니다. 파생 멤버는 [override](../../language-reference/keywords/override.md) 키워드를 사용하여 메서드가 가상 호출에 참여하도록 되어 있음을 명시적으로 나타내야 합니다. 다음 코드는 예제를 제공합니다.  
  
 [!code-csharp[csProgGuideInheritance#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#20)]  
  
 필드는 가상일 수 없습니다. 메서드, 속성, 이벤트 및 인덱서만 가상일 수 있습니다. 파생 클래스가 가상 멤버를 재정의하면 해당 멤버는 해당 클래스의 인스턴스가 기본 클래스의 인스턴스로 액세스되는 경우에도 호출됩니다. 다음 코드는 예제를 제공합니다.  
  
 [!code-csharp[csProgGuideInheritance#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#21)]  
  
 가상 메서드 및 속성을 통해 파생 클래스는 메서드의 기본 클래스 구현을 사용할 필요 없이 기본 클래스를 확장할 수 있습니다. 자세한 내용은 [Override 및 New 키워드를 사용하여 버전 관리](./versioning-with-the-override-and-new-keywords.md)를 참조하세요. 인터페이스는 구현이 파생 클래스에 남겨진 메서드 또는 메서드 집합을 정의하는 또 다른 방법을 제공합니다. 자세한 내용은 [인터페이스](../interfaces/index.md)를 참조하세요.  
  
### <a name="hiding-base-class-members-with-new-members"></a>새 멤버로 기본 클래스 멤버 숨기기  
 파생 멤버가 기본 클래스의 멤버와 동일한 이름을 갖되 가상 호출에는 참여하지 않도록 하려면 [new](../../language-reference/keywords/new-modifier.md) 키워드를 사용하면 됩니다. `new` 키워드는 바꿀 클래스 멤버의 반환 형식 앞에 배치됩니다. 다음 코드는 예제를 제공합니다.  
  
 [!code-csharp[csProgGuideInheritance#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#18)]  
  
 숨겨진 기본 클래스 멤버는 파생 클래스의 인스턴스를 기본 클래스의 인스턴스로 캐스팅하여 클라이언트 코드에서 계속 액세스할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#19)]  
  
### <a name="preventing-derived-classes-from-overriding-virtual-members"></a>파생 클래스가 가상 멤버를 재정의하지 못하도록 설정  
 가상 멤버는 가상 멤버와 원래 가상 멤버를 선언한 클래스 간에 선언된 클래스 수와 관계없이 무기한 가상으로 유지됩니다. 클래스 A가 가상 멤버를 선언하고, 클래스 B가 A에서 파생되며, 클래스 C가 B에서 파생되면 클래스 C는 클래스 B가 해당 멤버에 대한 재정의를 선언했는지 여부와 관계없이 가상 멤버를 상속하며, 가상 멤버를 재정의할 수 있습니다. 다음 코드는 예제를 제공합니다.  
  
 [!code-csharp[csProgGuideInheritance#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#22)]  
  
 파생 클래스는 재정의를 [sealed](../../language-reference/keywords/sealed.md)로 선언하여 가상 상속을 중지할 수 있습니다. 이렇게 하려면 클래스 멤버 선언에서 `sealed` 키워드 앞에 `override` 키워드를 배치해야 합니다. 다음 코드는 예제를 제공합니다.  
  
 [!code-csharp[csProgGuideInheritance#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#24)]  
  
 앞의 예제에서 `DoWork` 메서드는 C에서 파생된 모든 클래스에 대해 더 이상 가상이 아닙니다. 그러나 이 메서드는 C의 인스턴스가 형식 B 또는 형식 A로 캐스팅되더라도 여전히 C의 인스턴스에 대해서는 가상입니다. 다음 예제와 같이 `new` 키워드를 사용하여 sealed 메서드를 파생 클래스로 대체할 수 있습니다.  
  
 [!code-csharp[csProgGuideInheritance#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#25)]  
  
 이 경우 형식 D 변수를 사용하여 D에 대해 `DoWork`을 호출하면 새 `DoWork`가 호출됩니다. 형식 C, B 또는 A 변수를 사용하여 D의 인스턴스에 액세스하면 `DoWork`에 대한 호출에서 가상 상속의 규칙을 따라 해당 호출을 클래스 C에 대한 `DoWork`의 구현으로 라우팅합니다.  
  
### <a name="accessing-base-class-virtual-members-from-derived-classes"></a>파생 클래스에서 기본 클래스 가상 멤버 액세스  
 메서드 또는 속성을 바꾸었거나 재정의한 파생 클래스는 계속해서 `base` 키워드를 사용하여 기본 클래스에 대한 메서드 또는 속성에 액세스할 수 있습니다. 다음 코드는 예제를 제공합니다.  
  
 [!code-csharp[csProgGuideInheritance#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#26)]  
  
 자세한 내용은 [base](../../language-reference/keywords/base.md)를 참조하세요.  
  
> [!NOTE]
> 가상 멤버는 `base`를 사용하여 자체 구현에서 해당 멤버의 기본 클래스 구현을 호출하는 것이 좋습니다. 기본 클래스 동작이 발생하도록 하면 파생 클래스가 파생 클래스에 대한 동작 구현에 집중할 수 있습니다. 기본 클래스 구현이 호출되지 않는 경우 해당 동작이 기본 클래스의 동작과 호환되도록 하는 것은 파생 클래스의 책임입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
- [Override 및 New 키워드를 사용하여 버전 관리](./versioning-with-the-override-and-new-keywords.md)  
  
- [Override 및 New 키워드를 사용해야 하는 경우](./knowing-when-to-use-override-and-new-keywords.md)  
  
- [방법: ToString 메서드 재정의](./how-to-override-the-tostring-method.md)  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [상속](./inheritance.md)
- [추상/봉인된 클래스 및 클래스 멤버](./abstract-and-sealed-classes-and-class-members.md)
- [메서드](./methods.md)
- [이벤트](../events/index.md)
- [속성](./properties.md)
- [인덱서](../indexers/index.md)
- [유형](../types/index.md)
