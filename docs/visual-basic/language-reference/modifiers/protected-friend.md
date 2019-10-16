---
title: Protected Friend (Visual Basic)
ms.date: 05/10/2018
helpviewer_keywords:
- Protected Friend keyword [Visual Basic]
- Protected Friend keyword [Visual Basic], syntax
ms.openlocfilehash: 331c63dc290d4096e8158f265ee869b47743a273
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053888"
---
# <a name="protected-friend-visual-basic"></a>Protected Friend (Visual Basic)

`Protected Friend` 키워드 조합은 멤버 액세스 한정자입니다. 둘 다를 부여 하 [Friend](friend.md) 액세스 하 고 [보호 된](protected.md) 자체 클래스 및 파생된 클래스에서 동일한 어셈블리에서 임의의 위치에서 액세스할 수 있도록 선언된 된 요소에 대 한 액세스. 지정할 수 있습니다 `Protected Friend` 클래스의 멤버에만 적용할 수 없습니다 `Protected Friend` 구조체의 멤버에 구조체를 상속할 수 없습니다 때문입니다.

> [!NOTE]
> Visual Studio에서에서 F1 도움말을 선택 하 `protected friend` 에 대 한 도움말을 제공 [보호](protected.md) 하거나 [friend](friend.md)합니다. IDE 복합 단어를 사용 하지 않고 커서 아래에 있는 단일 토큰을 선택 합니다.

## <a name="rules"></a>규칙

- **선언 컨텍스트입니다.** 사용할 수 있습니다 `Protected Friend` 클래스 수준에만 합니다. 즉, 선언 컨텍스트는 `Protected` 요소 클래스 여야 하며 소스 파일, 네임 스페이스, 인터페이스, 모듈, 구조체 또는 프로시저 일 수 없습니다. 

## <a name="see-also"></a>참고자료

- [공용](../../../visual-basic/language-reference/modifiers/public.md)
- [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](friend.md)
- [전용](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](./private-protected.md)
- [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [절차](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
