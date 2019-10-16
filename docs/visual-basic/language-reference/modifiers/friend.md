---
title: Friend(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Friend
helpviewer_keywords:
- Friend keyword [Visual Basic]
- Friend access modifier
- Friend keyword [Visual Basic], syntax
- Protected Friend keyword combination
- Friend keyword [Visual Basic], and Protected
ms.assetid: b664605e-1c79-4728-b996-aa59c50846bc
ms.openlocfilehash: 2a5a2d6b9d99693a551480fa047cedf42888fdf3
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969045"
---
# <a name="friend-visual-basic"></a>Friend(Visual Basic)
선언 된 프로그래밍 요소를 해당 선언이 포함 된 어셈블리 내 에서만 액세스할 수 있도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
 대부분의 경우 클래스 및 구조체와 같은 프로그래밍 요소를 선언 하는 구성 요소 뿐만 아니라 전체 어셈블리에서 사용 해야 합니다. 그러나 어셈블리 외부의 코드에서 액세스할 수 없도록 하는 것이 좋습니다 (예: 응용 프로그램이 소유 하는 경우). 이러한 방식으로 요소에 대 한 액세스를 제한 하려는 경우 `Friend` 한정자를 사용 하 여 해당 요소를 선언할 수 있습니다.  
  
 동일한 어셈블리로 컴파일되는 다른 클래스, 구조체 및 모듈의 코드는 해당 어셈블리의 모든 `Friend` 요소에 액세스할 수 있습니다.  
  
 `Friend`액세스는 응용 프로그램의 프로그래밍 요소에 대 한 기본 설정 수준 이며 `Friend` 인터페이스, 모듈, 클래스 또는 구조체의 기본 액세스 수준입니다.  
  
 는 모듈, `Friend` 인터페이스 또는 네임 스페이스 수준 에서만 사용할 수 있습니다. 따라서 `Friend` 요소의 선언 컨텍스트는 소스 파일, 네임 스페이스, 인터페이스, 모듈, 클래스 또는 구조체 여야 합니다 .이는 프로시저일 수 없습니다.  

> [!NOTE]
> [Protected Friend](protected-friend.md) 액세스 한정자를 사용 하 여 클래스, 파생 클래스 및 클래스가 정의 된 동일한 어셈블리에서 클래스 멤버에 액세스할 수 있게 할 수도 있습니다. 해당 클래스 내와 동일한 어셈블리의 파생 클래스에서 멤버에 대 한 액세스를 제한 하려면 [Private Protected](private-protected.md) 액세스 한정자를 사용 합니다.

 및 다른 액세스 한정자 `Friend` 의 비교는 [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조 하세요.  
  
> [!NOTE]
> 다른 어셈블리를 friend 어셈블리로 지정 하 여로 `Friend`표시 된 모든 형식 및 멤버에 액세스할 수 있도록 지정할 수 있습니다. 자세한 내용은 [Friend Assemblies](../../../standard/assembly/friend.md)(Friend 어셈블리)를 참조하세요.

## <a name="example"></a>예제  
 다음 클래스는 `Friend` 한정자를 사용 하 여 동일한 어셈블리 내의 다른 프로그래밍 요소가 특정 멤버에 액세스할 수 있도록 합니다.  
  
 [!code-vb[VbVbalrAccessModifiers#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalraccessmodifiers/vb/class1.vb#1)]  
  
## <a name="usage"></a>사용  
 한정자는 `Friend` 다음 컨텍스트에서 사용할 수 있습니다.  
  
 [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Const 문](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate 문](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum 문](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Module 문](../../../visual-basic/language-reference/statements/module-statement.md)  
  
 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [공용](../../../visual-basic/language-reference/modifiers/public.md)
- [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)
- [전용](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](./private-protected.md)
- [Protected Friend](./protected-friend.md)
- [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [절차](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
