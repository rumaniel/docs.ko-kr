---
title: 액세스 가능성 수준 - C# 참조
ms.custom: seodec18
ms.date: 12/06/2017
helpviewer_keywords:
- access modifiers [C#], accessibility levels
- accessibility levels
ms.assetid: dc083921-0073-413e-8936-a613e8bb7df4
ms.openlocfilehash: 2d6605a305e5003e19f4fe1dd260746302691215
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602394"
---
# <a name="accessibility-levels-c-reference"></a>액세스 가능성 수준(C# 참조)

액세스 한정자 `public`, `protected`, `internal` 또는 `private`을 사용하여 멤버에 대해 다음과 같이 선언된 접근성 수준 중 하나를 지정합니다.  
  
|선언된 액세스 가능성|의미|  
|----------------------------|-------------|  
|[`public`](public.md)|액세스가 제한되지 않습니다.|  
|[`protected`](protected.md)|액세스가 포함하는 클래스 또는 포함하는 클래스에서 파생된 형식으로 제한됩니다.|  
|[`internal`](internal.md)|액세스가 현재 어셈블리로 제한됩니다.|  
|[`protected internal`](protected-internal.md)|액세스가 현재 어셈블리 또는 포함하는 클래스에서 파생된 형식으로 제한됩니다.|  
|[`private`](private.md)|액세스가 포함하는 형식으로 제한됩니다.|  
|[`private protected`](private-protected.md)|액세스가 포함하는 클래스 또는 현재 어셈블리 내의 포함하는 클래스에서 파생된 형식으로 제한됩니다. C# 7.2부터 사용할 수 있습니다. |  
  
 `protected internal` 또는 `private protected` 조합을 사용할 경우를 제외하고 멤버 또는 형식에는 액세스 한정자가 하나만 허용됩니다.  
  
 네임스페이스에는 액세스 한정자가 허용되지 않습니다. 네임스페이스에는 액세스 제한이 없습니다.  
  
 멤버 선언이 발생한 컨텍스트에 따라 특정 선언된 액세스 가능성만 허용됩니다. 액세스 한정자가 멤버 선언에서 지정되지 않으면 기본 액세스 가능성이 사용됩니다.  
  
 다른 형식에 중첩되지 않은 최상위 형식에는 `internal` 또는 `public` 액세스 가능성만 포함될 수 있습니다. 이러한 형식에 대한 기본 액세스 가능성은 `internal`입니다.  
  
 다음 표에 나와 있는 대로 다른 형식의 멤버인 중첩 형식에는 선언된 액세스 가능성이 포함될 수 있습니다.  
  
|소속 그룹|기본 멤버 액세스 가능성|멤버의 허용된 선언된 액세스 가능성|  
|----------------|----------------------------------|--------------------------------------------------|  
|`enum`|`public`|없음|  
|`class`|`private`|`public`<br /><br /> `protected`<br /><br /> `internal`<br /><br /> `private`<br /><br /> `protected internal` <br /><br />`private protected`|  
|`interface`|`public`|없음|  
|`struct`|`private`|`public`<br /><br /> `internal`<br /><br /> `private`|  
  
 중첩된 형식의 액세스 가능성은 액세스 가능 도메인에 따라 다릅니다. [액세스 가능성 도메인](./accessibility-domain.md)은 멤버에 대해 선언된 액세스 가능성 및 한 수준 위 형식의 액세스 가능성 도메인에 의해 결정됩니다. 그러나 중첩 형식의 액세스 가능 도메인은 포함하는 형식의 액세스 가능 도메인을 벗어날 수는 없습니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](./index.md)
- [액세스 한정자](./access-modifiers.md)
- [접근성 도메인](./accessibility-domain.md)
- [접근성 수준 사용에 대한 제한](./restrictions-on-using-accessibility-levels.md)
- [액세스 한정자](../../programming-guide/classes-and-structs/access-modifiers.md)
- [public](./public.md)
- [private](./private.md)
- [protected](./protected.md)
- [internal](./internal.md)
