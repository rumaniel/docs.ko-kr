---
title: 인터페이스(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, interfaces
- interfaces [Visual Basic], Visual Basic
- interfaces
- interfaces [Visual Basic]
ms.assetid: 61b06674-12c9-430b-be68-cc67ecee1f5b
ms.openlocfilehash: 968e5d9bb08f168e3c77b40ea42b16dc66e93e64
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956292"
---
# <a name="interfaces-visual-basic"></a>인터페이스(Visual Basic)
*인터페이스*는 클래스가 구현할 수 있는 속성, 메서드 및 이벤트를 정의합니다. 인터페이스를 사용하면 기능을 밀접한 관련이 있는 속성, 메서드, 이벤트 등의 작은 그룹으로 정의할 수 있습니다. 이렇게 하면 기존 코드를 그대로 사용하여 인터페이스에 대한 고급 구현을 개발할 수 있기 때문에 호환성 문제가 줄어듭니다. 추가적인 인터페이스와 구현을 개발하여 언제든지 새로운 기능을 추가할 수 있습니다.  
  
 클래스를 상속하는 대신 인터페이스를 사용해야 하는 몇 가지 다른 이유가 있습니다.  
  
- 인터페이스는 특정 기능을 제공하기 위해 무관할 수 있는 다수의 개체 형식이 애플리케이션에서 요구되는 경우에 더 적합합니다.  
  
- 인터페이스는 다중 인터페이스를 구현하는 단일 구현을 정의할 수 있기 때문에 기본 클래스보다 더 유연합니다.  
  
- 인터페이스는 기본 클래스로부터 구현을 상속할 필요가 없는 경우에 더 효율적입니다.  
  
- 인터페이스는 클래스 상속을 사용할 수 없는 경우에 유용합니다. 예를 들어 구조체는 클래스에서 상속할 수 없지만 인터페이스를 구현할 수는 있습니다.  
  
## <a name="declaring-interfaces"></a>인터페이스 선언  
 인터페이스 정의는 `Interface` 및 `End Interface` 문 내에 포함됩니다. `Interface` 문 다음에, 하나 이상의 상속된 인터페이스를 나열하는 `Inherits` 문을 선택적으로 추가할 수 있습니다. `Inherits` 문은 선언에서 주석을 제외하고는 다른 모든 문 앞에 와야 합니다. 인터페이스 정의에 나오는 나머지 문은 `Event`, `Sub`, `Function`, `Property`, `Interface`, `Class`, `Structure` 및 `Enum` 문입니다. 인터페이스는 구현 코드 또는 구현 코드와 관련된 문(예: `End Sub` 또는 `End Property`)을 포함할 수 없습니다.  
  
 네임스페이스에서 인터페이스 문은 기본적으로 `Friend`이지만 `Public` 또는 `Friend`로 명시적으로 선언할 수도 있습니다. 클래스, 모듈, 인터페이스 및 구조체 내에서 정의되는 인터페이스는 기본적으로 `Public`이지만 `Public`, `Friend`, `Protected` 또는 `Private`으로 명시적으로 선언할 수도 있습니다.  
  
> [!NOTE]
> `Shadows` 키워드는 모든 인터페이스 멤버에 적용할 수 있습니다. `Overloads` 키워드는 인터페이스 정의에서 정의되는 `Sub`, `Function` 및 `Property` 문에 적용할 수 있습니다. 또한 `Property` 문은 `Default`, `ReadOnly` 또는 `WriteOnly` 한정자를 가질 수 있습니다. `Public`, `Private`, `Friend`, `Protected`, `Shared`, `Overrides`, `MustOverride` 또는 `Overridable` 등의 다른 한정자는 허용되지 않습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 예를 들어 다음 코드는 하나의 함수, 하나의 속성, 하나의 이벤트가 있는 인터페이스를 정의합니다.  
  
 [!code-vb[VbVbalrOOP#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#17)]  
  
## <a name="implementing-interfaces"></a>인터페이스 구현  
 Visual Basic 예약어 `Implements` 는 두 가지 방법으로 사용 됩니다. `Implements` 문은 클래스 또는 구조체가 인터페이스를 구현한다는 것을 나타냅니다. `Implements` 키워드는 클래스 멤버 또는 구조체 멤버가 특정 인터페이스 멤버를 구현한다는 것을 나타냅니다.  
  
### <a name="implements-statement"></a>Implements 문  
 하나 이상의 인터페이스를 구현하는 클래스 또는 구조체에는 `Class` 또는 `Structure` 문 바로 다음에 `Implements`문이 나와야 합니다. `Implements` 문에는 클래스에 의해 구현될 인터페이스를 나열한, 쉼표로 구분된 목록이 필요합니다. 클래스 또는 구조체는 `Implements` 키워드를 사용하여 모든 인터페이스 멤버를 구현해야 합니다.  
  
### <a name="implements-keyword"></a>Implements 키워드  
 `Implements` 키워드에는 구현될 인터페이스 멤버를 나열한, 쉼표로 구분된 목록이 필요합니다. 일반적으로 단일 인터페이스 멤버만 지정되지만 여러 멤버를 지정할 수도 있습니다. 인터페이스 멤버의 사양은 인터페이스 이름(클래스 내의 implements 문에서 지정해야 함)과 기간 및 구현할 멤버 함수, 속성 또는 이벤트의 이름으로 구성됩니다. 인터페이스 멤버를 구현 하는 멤버의 이름에는 유효한 식별자를 사용할 수 있으며 이전 버전의 Visual Basic에 사용 `InterfaceName_MethodName` 되는 규칙으로 제한 되지 않습니다.  
  
 예를 들어 다음 코드에서는 인터페이스의 메서드를 구현하는 `Sub1`이라는 서브루틴을 선언하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrOOP#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#69)]  
  
 구현 멤버의 매개 변수 형식 및 반환 형식은 인터페이스의 인터페이스 속성 또는 멤버 선언과 일치해야 합니다. 인터페이스의 요소를 구현하는 가장 일반적인 방법은 이전 예제와 같이 인터페이스와 이름이 같은 멤버를 사용하는 것입니다.  
  
 인터페이스 메서드의 구현을 선언하려면 인스턴스 메서드 선언에 `Overloads`, `Overrides`, `Overridable`, `Public`, `Private`, `Protected`, `Friend`, `Protected Friend`, `MustOverride`, `Default`, `Static` 등의 유효한 특성을 사용할 수 있습니다. `Shared` 특성은 인스턴스 메서드가 아니라 클래스를 정의하므로 유효하지 않습니다.  
  
 `Implements`를 사용하여 다음 예제와 같이 인터페이스에서 정의된 여러 메서드를 구현하는 단일 메서드를 작성할 수도 있습니다.  
  
 [!code-vb[VbVbalrOOP#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#70)]  
  
 전용 멤버를 사용하여 인터페이스 멤버를 구현할 수 있습니다. 전용 멤버가 인터페이스의 멤버를 구현하는 경우 이 멤버는 클래스에 대한 개체 변수에 대해 직접 사용할 수 없더라도 인터페이스를 통해 사용할 수 있게 됩니다.  
  
### <a name="interface-implementation-examples"></a>인터페이스 구현 예제  
 인터페이스를 구현하는 클래스는 모든 속성, 메서드 및 이벤트를 구현해야 합니다.  
  
 다음 예제에서는 두 인터페이스를 정의합니다. 두 번째 인터페이스인 `Interface2`는 `Interface1`을 상속하며 추가 속성 및 메서드를 정의합니다.  
  
 [!code-vb[VbVbalrOOP#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#39)]  
  
 다음 예제에서는 이전 예제에서 정의된 인터페이스인 `Interface1`을 구현합니다.  
  
 [!code-vb[VbVbalrOOP#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#40)]  
  
 마지막 예제에서는 `Interface1`에서 상속된 메서드를 포함하여 `Interface2`를 구현합니다.  
  
 [!code-vb[VbVbalrOOP#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#41)]  
  
 읽기/쓰기 속성을 사용하여 읽기 전용 속성을 구현할 수 있습니다(즉, 구현 클래스에서 읽기 전용으로 선언할 필요가 없음).  인터페이스를 선언하면 최소한 이 인터페이스가 선언하는 멤버가 구현됩니다. 하지만 속성을 쓰기 가능하도록 허용하는 등, 더 많은 기능을 제공할 수 있습니다.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[연습: 인터페이스 만들기 및 구현](../../../../visual-basic/programming-guide/language-features/interfaces/walkthrough-creating-and-implementing-interfaces.md)|고유한 인터페이스를 정의하고 구현하는 프로세스를 안내하는 자세한 절차를 설명합니다.|  
|[제네릭 인터페이스의 가변성](../../concepts/covariance-contravariance/variance-in-generic-interfaces.md)|제네릭 인터페이스의 공분산 및 반공분산에 대해 설명하고 .NET Framework의 Variant 제네릭 인터페이스의 목록을 제공합니다.|
