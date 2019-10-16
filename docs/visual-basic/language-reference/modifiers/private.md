---
title: Private(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Private
helpviewer_keywords:
- Private keyword [Visual Basic]
- Private keyword [Visual Basic], syntax
ms.assetid: aba74a2e-5824-4613-bf63-b9ec7787f4e6
ms.openlocfilehash: ddb2d165de330758f58fbbcb5872e820e639808f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64642787"
---
# <a name="private-visual-basic"></a>Private(Visual Basic)
하나 이상의 선언 된 프로그래밍 요소를 포함 된 모든 형식을 포함 하 여 해당 선언 컨텍스트 내 에서만 액세스할 수 있도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
 프로그래밍 요소 소유권이 있는 기능 또는 기밀 데이터를 포함 하는 경우에 일반적으로 최대한 엄격 하 게 액세스를 제한 합니다. 모듈, 클래스 또는 구조체 정의에 액세스 하는 허용 하 여 최대 한계를 달성 합니다. 이러한 방식으로 요소에 대 한 액세스를 제한 하려면 사용 하 여 선언할 수 있습니다 `Private`합니다.  

> [!NOTE]
> 사용할 수도 있습니다는 [Private Protected](private-protected.md) 멤버를 해당 클래스 내에서 및 포함 된 어셈블리에 있는 파생 된 클래스에서 액세스할 수 있게 하는 액세스 한정자입니다.

## <a name="rules"></a>규칙  

- **선언 컨텍스트입니다.** `Private`는 모듈 수준에서만 사용할 수 있습니다. 즉, 선언 컨텍스트는 `Private` 요소 모듈, 클래스 또는 구조 여야 하며 소스 파일, 네임 스페이스, 인터페이스 또는 프로시저 일 수 없습니다.  
  
## <a name="behavior"></a>동작  
  
- **액세스 수준입니다.** 선언 컨텍스트 내에서 모든 코드에 액세스할 수는 `Private` 요소입니다. 이 중첩된 된 클래스 또는 열거형에 대입 식을 같은 포함 된 형식에 코드를 포함합니다. 액세스할 수 없는 코드 선언 컨텍스트 외부에서 해당 `Private` 요소입니다.  
  
- **액세스 한정자입니다.** 액세스 수준을 지정 하는 키워드 라고 *액세스 한정자*합니다. 액세스 한정자와 비교 [액세스 수준을 Visual Basic의](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)합니다.  
  
 `Private` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.  
  
 [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Const 문](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate 문](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum 문](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>참고자료

- [공용](../../../visual-basic/language-reference/modifiers/public.md)
- [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)
- [Private Protected](./private-protected.md)
- [Protected Friend](./protected-friend.md)[액세스 수준을 Visual basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [절차](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
