---
title: Private Protected (Visual Basic)
ms.date: 05/10/2018
helpviewer_keywords:
- Private Protected keyword [Visual Basic]
- Private Protected keyword [Visual Basic], syntax
ms.openlocfilehash: fea43558ac0fe8181f2786b69f2621346d446b2e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61920499"
---
# <a name="private-protected-visual-basic"></a>Private Protected (Visual Basic)

`Private Protected` 키워드 조합은 멤버 액세스 한정자입니다. `Private Protected` 멤버를 포함 하는 어셈블리가 있는 경우만 포함 하는 클래스에서 파생 된 형식 뿐만 아니라 모든 멤버에 포함 하는 클래스를 통해 액세스할 수 있습니다.

지정할 수 있습니다 `Private Protected` 클래스의 멤버에만 적용할 수 없습니다 `Private Protected` 구조체의 멤버에 구조체를 상속할 수 없습니다 때문입니다.

`Private Protected` 액세스 한정자는 Visual Basic 15.5 이상에 지원 됩니다. 를 사용 하려면 Visual Basic 프로젝트에 다음 요소를 추가할 수 있습니다 (\*.vbproj) 파일입니다. Visual Basic 15.5 하기만 이상 시스템에 설치 되어, 최신 버전의 Visual Basic 컴파일러를 지 원하는 모든 언어 기능을 활용할 수 있습니다.

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

자세한 내용은 참조 [Visual Basic 언어 버전을 설정](../../language-reference/configure-language-version.md)합니다.

> [!NOTE]
> Visual Studio에서에서 F1 도움말을 선택 하 `private protected` 에 대 한 도움말을 제공 [사설](private.md) 하거나 [보호](protected.md). IDE 복합 단어를 사용 하지 않고 커서 아래에 있는 단일 토큰을 선택 합니다.

## <a name="rules"></a>규칙

- **선언 컨텍스트입니다.** 사용할 수 있습니다 `Private Protected` 클래스 수준에만 합니다. 즉, 선언 컨텍스트는 `Protected` 요소 클래스 여야 하며 소스 파일, 네임 스페이스, 인터페이스, 모듈, 구조체 또는 프로시저 일 수 없습니다.

## <a name="behavior"></a>동작

- **액세스 수준입니다.** 클래스의 모든 코드가 해당 요소에 액세스할 수 있습니다. 모든 기본 클래스에서 파생 되는 동일한 어셈블리에 포함 된 모든 클래스의 코드에 액세스할 수는 `Private Protected` 요소의 기본 클래스입니다. 그러나 기본 클래스에서 파생 되는 다른 어셈블리에 포함 된 모든 클래스의 코드는 기본 클래스에 액세스할 수 없습니다 `Private Protected` 요소입니다.

- **액세스 한정자입니다.** 액세스 수준을 지정 하는 키워드 라고 *액세스 한정자*합니다. 액세스 한정자와 비교 [액세스 수준을 Visual Basic의](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)합니다.

`Private Protected` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.

- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md) 중첩된 된 클래스의

- [Const 문](../../../visual-basic/language-reference/statements/const-statement.md)

- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)

- [Delegate 문](../../../visual-basic/language-reference/statements/delegate-statement.md) 클래스에서 중첩 된 대리자

- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)

- [Enum 문](../../../visual-basic/language-reference/statements/enum-statement.md) 클래스에서 중첩 된 열거형의

- [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)

- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)

- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md) 인터페이스의 클래스에서 중첩

- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)

- [문을 구조체](../../../visual-basic/language-reference/statements/structure-statement.md) 클래스에서 중첩 된 구조의

- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)

## <a name="see-also"></a>참고자료

- [공용](../../../visual-basic/language-reference/modifiers/public.md)
- [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](friend.md)
- [전용](../../../visual-basic/language-reference/modifiers/private.md)
- [Protected Friend](./protected-friend.md)
- [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [절차](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
