---
title: 접근자 액세스 가능성 제한 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- read-only properties [C#]
- read-only indexers [C#]
- accessors [C#]
- properties [C#], read-only
- asymmetric accessor accessibility [C#]
- indexers [C#], read-only
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
ms.openlocfilehash: ca990693d29f8c8abd2e4ba2488a429a797afaec
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596178"
---
# <a name="restricting-accessor-accessibility-c-programming-guide"></a>접근자 액세스 가능성 제한(C# 프로그래밍 가이드)
속성 또는 인덱서의 [get](../../language-reference/keywords/get.md) 및 [set](../../language-reference/keywords/set.md) 부분을 *접근자*라고 합니다. 기본적으로 이러한 접근자는 속하는 속성 또는 인덱서와 동일한 표시 유형 또는 액세스 수준을 갖습니다. 자세한 내용은 [접근성 수준](../../language-reference/keywords/accessibility-levels.md)을 참조하세요. 그러나 이러한 접근자 중 하나에 대한 액세스를 제한하는 것이 유용한 경우도 있습니다. 이렇게 하려면 일반적으로 `set` 접근자의 접근성을 제한하는 동시에 `get` 접근자를 공개적으로 액세스할 수 있도록 유지해야 합니다. 예:  
  
 [!code-csharp[csProgGuideIndexers#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#6)]  
  
 이 예제에서는 `Name` 속성이 `get` 및 `set` 접근자를 정의합니다. `get` 접근자는 속성 자체의 접근성 수준(이 경우 `public`)을 받는 반면, `set` 접근자는 접근자 자체에 [protected](../../language-reference/keywords/protected.md) 액세스 한정자를 적용하여 명시적으로 제한됩니다.  
  
## <a name="restrictions-on-access-modifiers-on-accessors"></a>접근자의 액세스 한정자에 대한 제한 사항  
 속성 또는 인덱서의 접근자 한정자 사용에는 다음과 같은 조건이 적용됩니다.  
  
- 인터페이스 또는 명시적 [interface](../../language-reference/keywords/interface.md) 멤버 구현에는 접근자 한정자를 사용할 수 없습니다.  
  
- 속성 또는 인덱서에 `set` 및 `get` 접근자가 모두 포함된 경우에만 접근자 한정자를 사용할 수 있습니다. 이 경우 두 접근자 중 하나에서만 한정자가 허용됩니다.  
  
- 속성 또는 인덱서에 [override](../../language-reference/keywords/override.md) 한정자가 있는 경우 접근자 한정자가 재정의된 접근자의 한정자와 일치해야 합니다(있는 경우).  
  
- 접근자의 접근성 수준은 속성 또는 인덱서 자체의 접근성 수준보다 더 제한적이어야 합니다.  
  
## <a name="access-modifiers-on-overriding-accessors"></a>재정의 접근자의 액세스 한정자  
 속성 또는 인덱서를 재정의하는 경우 재정의 코드에서 재정의된 접근자에 액세스할 수 있어야 합니다. 또한 속성/인덱서 및 접근자의 접근성이 재정의된 속성/인덱서 및 해당 접근자와 일치해야 합니다. 예:  
  
 [!code-csharp[csProgGuideIndexers#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#7)]  
  
## <a name="implementing-interfaces"></a>인터페이스 구현  
 접근자를 사용하여 인터페이스를 구현하는 경우 접근자에 액세스 한정자가 있을 수 없습니다. 그러나 `get` 등의 한 접근자를 사용하여 인터페이스를 구현하는 경우 다음 예제와 같이 다른 접근자에 액세스 한정자를 사용할 수 있습니다.  
  
 [!code-csharp[csProgGuideIndexers#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#8)]  
  
## <a name="accessor-accessibility-domain"></a>접근자 접근성 도메인  
 접근자의 액세스 한정자를 사용하는 경우 접근자의 [접근성 도메인](../../language-reference/keywords/accessibility-domain.md)은 이 한정자에 의해 결정됩니다.  
  
 접근자의 액세스 한정자를 사용하지 않은 경우 접근자의 접근성 도메인은 속성 또는 인덱서의 접근성 수준에 의해 결정됩니다.  
  
## <a name="example"></a>예  
 다음 예제에는 세 가지 클래스 `BaseClass`, `DerivedClass`, `MainClass`가 포함되어 있습니다. `BaseClass`에는 두 클래스의 `Name` 및 `Id`인 두 가지 속성이 있습니다. 예제에서는 [protected](../../language-reference/keywords/protected.md), [private](../../language-reference/keywords/private.md) 등의 제한적인 액세스 한정자를 사용할 때 `DerivedClass`의 `Id` 속성을 `BaseClass`의 `Id` 속성으로 숨길 수 있는 방법을 보여 줍니다. 따라서 이 속성에 값을 할당하면 `BaseClass` 클래스의 속성이 대신 호출됩니다. 액세스 한정자를 [public](../../language-reference/keywords/public.md)으로 바꾸면 속성에 액세스할 수 있습니다.  
  
 또한 예제에서는 `DerivedClass`, `Name` 속성의 `set` 접근자에 있는 `private`, `protected` 등의 제한적인 액세스 한정자가 접근자에 대한 액세스를 차단하고 할당을 시도할 때 오류를 생성함을 보여 줍니다.  
  
 [!code-csharp[csProgGuideIndexers#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#5)]  
  
## <a name="comments"></a>설명  
 `new private string Id` 선언을 `new public string Id`로 바꿀 경우 다음과 같이 출력됩니다.  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [속성](./properties.md)
- [인덱서](../indexers/index.md)
- [액세스 한정자](./access-modifiers.md)
