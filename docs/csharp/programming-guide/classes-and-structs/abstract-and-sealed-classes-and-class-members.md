---
title: 추상 및 봉인 클래스와 클래스 멤버 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- abstract classes [C#]
- sealed classes [C#]
- C# language, abstract classes
- C# language, sealed
ms.assetid: 99aa52f7-b435-43f9-936e-2470af734c4e
ms.openlocfilehash: 1c98e2979ee96d4bcc885b8cc797eaac28c8d2ed
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597300"
---
# <a name="abstract-and-sealed-classes-and-class-members-c-programming-guide"></a>추상 및 봉인 클래스와 클래스 멤버(C# 프로그래밍 가이드)
[abstract](../../language-reference/keywords/abstract.md) 키워드를 사용하면, 불완전하여 파생 클래스에서 구현해야 하는 클래스 및 [클래스](../../language-reference/keywords/class.md) 멤버를 만들 수 있습니다.  
  
 [sealed](../../language-reference/keywords/sealed.md) 키워드를 사용하면, 이전에 [virtual](../../language-reference/keywords/virtual.md)로 표시되었던 클래스나 특정 클래스 멤버의 상속을 방지할 수 있습니다.  
  
## <a name="abstract-classes-and-class-members"></a>추상 클래스 및 클래스 멤버  
 클래스 정의 앞에 `abstract` 키워드를 배치하여 클래스를 추상으로 선언할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#13)]  
  
 추상 클래스는 인스턴스화할 수 없습니다. 추상 클래스의 목적은 여러 파생 클래스에서 공유할 수 있는 기본 클래스의 공통적인 정의를 제공하는 것입니다. 예를 들어 클래스 라이브러리에서 여러 자체 함수에 매개 변수로 사용되는 추상 클래스를 정의한 다음 해당 라이브러리를 사용하는 프로그래머가 파생 클래스를 만들어 클래스의 고유 구현을 제공하도록 할 수 있습니다.  
  
 추상 클래스에서는 추상 메서드도 정의할 수 있습니다. 메서드의 반환 형식 앞에 `abstract` 키워드를 추가하면 추상 메서드가 정의됩니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#14)]  
  
 추상 메서드에는 구현이 없으므로 메서드 정의 다음에는 일반적인 메서드 블록 대신 세미콜론이 옵니다. 추상 클래스의 파생 클래스에서는 모든 추상 메서드를 구현해야 합니다. 추상 클래스에서 기본 클래스의 가상 메서드를 상속하는 경우 추상 클래스에서는 추상 메서드를 사용하여 가상 메서드를 재정의할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#15)]  
  
 `virtual` 메서드는 `abstract`로 선언되어도 추상 클래스에서 상속된 모든 클래스에 대해 여전히 가상입니다. 추상 메서드를 상속하는 클래스에서는 메서드의 원본 구현에 액세스할 수 없습니다. 앞의 예제에서 F 클래스의 `DoWork`에서는 D 클래스의 `DoWork`를 호출할 수 없습니다. 따라서 추상 클래스는 파생 클래스에서 가상 메서드에 대한 새 메서드 구현을 반드시 제공하도록 제한할 수 있습니다.  
  
## <a name="sealed-classes-and-class-members"></a>봉인 클래스 및 클래스 멤버  
 클래스 정의 앞에 `sealed` 키워드를 배치하여 클래스를 [sealed](../../language-reference/keywords/sealed.md)로 선언할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#16)]  
  
 봉인 클래스는 기본 클래스로 사용할 수 없습니다. 그러므로 추상 클래스가 될 수도 없습니다. 봉인 클래스는 상속할 수 없습니다. 봉인 클래스는 기본 클래스로 사용될 수 없으므로 일부 런타임 최적화에서는 봉인 클래스 멤버 호출이 약간 더 빨라집니다.  
  
 기본 클래스의 가상 멤버를 재정의하는 파생 클래스의 메서드, 인덱서, 속성 또는 이벤트는 해당 멤버를 봉인으로 선언할 수 있습니다. 이렇게 하면 이후에 파생되는 클래스에서는 해당 멤버가 가상이 아니게 됩니다. 클래스 멤버 선언에서 [override](../../language-reference/keywords/override.md) 키워드 앞에 `sealed` 키워드를 배치하면 됩니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#17)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [상속](./inheritance.md)
- [메서드](./methods.md)
- [필드](./fields.md)
- [방법: 추상 속성 정의](./how-to-define-abstract-properties.md)
