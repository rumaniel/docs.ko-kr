---
title: Protected(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Protected
helpviewer_keywords:
- Protected Friend keyword combination
- Protected keyword [Visual Basic], and Friend
- Protected keyword [Visual Basic], syntax
- Protected access modifier
- Protected keyword [Visual Basic]
ms.assetid: 74ad3d56-309f-49d2-b60c-1d0157d010e8
ms.openlocfilehash: a80e504cc8e88dfc8968f70fee2c17991b28aff5
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929465"
---
# <a name="protected-visual-basic"></a>Protected(Visual Basic)
하나 이상의 선언 된 프로그래밍 요소가 자체 클래스 또는 파생 된 클래스 내 에서만 액세스할 수 있도록 지정 하는 멤버 액세스 한정자입니다.  
  
## <a name="remarks"></a>설명  
 클래스에 선언 된 프로그래밍 요소가 중요 한 데이터 또는 제한 된 코드를 포함 하 고 있고 요소에 대 한 액세스를 제한 하려는 경우가 있습니다. 그러나 클래스가 상속 가능 하 고 파생 클래스의 계층 구조가 필요한 경우 이러한 파생 클래스에서 데이터 또는 코드에 액세스 해야 할 수 있습니다. 이 경우 기본 클래스와 모든 파생 클래스에서 요소에 액세스할 수 있도록 합니다. 이러한 방식으로 요소에 대 한 액세스를 제한 하려면로 `Protected`선언할 수 있습니다.  

> [!NOTE]
> 액세스 `Protected` 한정자는 다음과 같은 두 가지 한정자와 함께 사용할 수 있습니다.
>
> - [Protected Friend](protected-friend.md) 한정자는 클래스, 파생 클래스 및 클래스가 정의 된 동일한 어셈블리에서 클래스 멤버를 액세스할 수 있도록 합니다. 
> - [Private Protected](private-protected.md) 한정자를 사용 하면 파생 형식에서 클래스 멤버에 액세스할 수 있지만 포함 하는 어셈블리 내 에서만 클래스 멤버에 액세스할 수 있습니다.
  
## <a name="rules"></a>규칙  
  
- **선언 컨텍스트입니다.** 는 클래스 수준 `Protected` 에서만 사용할 수 있습니다. 즉, `Protected` 요소에 대 한 선언 컨텍스트는 클래스 여야 하며 소스 파일, 네임 스페이스, 인터페이스, 모듈, 구조체 또는 프로시저일 수 없습니다.  

## <a name="behavior"></a>동작  
  
- **액세스 수준입니다.** 클래스의 모든 코드는 해당 요소에 액세스할 수 있습니다. 기본 클래스에서 파생 되는 모든 클래스의 코드는 기본 클래스의 `Protected` 모든 요소에 액세스할 수 있습니다. 이는 모든 파생 세대에 적용 됩니다. 즉, 클래스가 기본 클래스의 기본 `Protected` 클래스 요소에 액세스할 수 있습니다.  
  
     보호 된 액세스는 friend 액세스의 상위 집합이 나 하위 집합이 아닙니다.  
  
- **액세스 한정자입니다.** 액세스 수준을 지정 하는 키워드를 *액세스 한정자*라고 합니다. 액세스 한정자의 비교는 [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조 하세요.  
  
 `Protected` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.  
  
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

- [공개](../../../visual-basic/language-reference/modifiers/public.md)
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)
- [전용](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](private-protected.md)
- [Protected Friend](protected-friend.md)
- [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [절차](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
