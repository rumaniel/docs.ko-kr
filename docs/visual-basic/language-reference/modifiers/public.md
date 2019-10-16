---
title: Public(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Public
helpviewer_keywords:
- Public keyword [Visual Basic]
- Public keyword [Visual Basic], syntax
- Public access modifier
ms.assetid: 284c9e1b-ed23-499b-9bc9-ad87c11485a5
ms.openlocfilehash: 0b8c31facc3605ff5a77aecf7b11456b33fbab72
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647742"
---
# <a name="public-visual-basic"></a>Public(Visual Basic)
선언 된 프로그래밍 요소를 하나 이상의 액세스 제한이 있는지를 지정 합니다.  
  
## <a name="remarks"></a>설명  
 구성 요소 또는 클래스 라이브러리 등의 구성 요소 집합을 게시 하는 경우 어셈블리를 사용 하 여 상호 운용 하는 모든 코드에서 액세스할 수 있도록 프로그래밍 요소를 일반적으로 합니다. 요소에 대 한 이러한 무제한 액세스를 부여 하 여 선언할 수 있습니다 `Public`합니다.  
  
 공용 액세스는 프로그래밍 요소에 대 한 보통 수준에 대 한 액세스를 제한 해야 하는 경우. 인터페이스, 모듈, 클래스 또는 구조체 내에 선언 된 액세스 수준 요소에는 기본적으로 `Public` 따로 선언 하지 마십시오.  
  
## <a name="rules"></a>규칙  
  
- **선언 컨텍스트입니다.** 사용할 수 있습니다 `Public` 모듈, 인터페이스 또는 네임 스페이스 수준 에서만. 즉, 선언 컨텍스트는 `Public` 요소 소스 파일, 네임 스페이스, 인터페이스, 모듈, 클래스 또는 구조 여야 하며 프로시저일 수는 없습니다.  
  
## <a name="behavior"></a>동작  
  
- **액세스 수준입니다.** 모듈, 클래스 또는 구조체에 액세스할 수 있는 모든 코드에 액세스할 수는 `Public` 요소입니다.  
  
- **기본 액세스 합니다.** 공용 액세스에 프로시저 기본값 내의 지역 변수 에서도 모든 액세스 한정자를 사용할 수 없습니다.  
  
- **액세스 한정자입니다.** 액세스 수준을 지정 하는 키워드 라고 *액세스 한정자*합니다. 액세스 한정자와 비교 [액세스 수준을 Visual Basic의](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)합니다.  
  
 `Public` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.  
  
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
  
 [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>참고자료

- [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)
- [전용](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](private-protected.md)
- [Protected Friend](protected-friend.md)
- [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [절차](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
