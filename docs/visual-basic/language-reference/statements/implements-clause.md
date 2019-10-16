---
title: Implements 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.ImplementsClause
helpviewer_keywords:
- interface implementation [Visual Basic], reimplementation
- interface members [Visual Basic], reimplementation
- interface members [Visual Basic], Implements keyword
- interface members
- members [Visual Basic], reimplementation
- interface implementation [Visual Basic], Implements keyword
- interface members [Visual Basic], implementing
- Implements keyword [Visual Basic]
- Implements statement [Visual Basic], about Implements
- members [Visual Basic], implementing
- members [Visual Basic], Implements keyword
- reimplementation
ms.assetid: 5252cdf9-964d-4fc6-af0f-0449b7126b5a
ms.openlocfilehash: dcd20f21a989c327dcfcf27d5638d500b6e4b6da
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929313"
---
# <a name="implements-clause-visual-basic"></a>Implements 절(Visual Basic)
클래스 또는 구조체 멤버가 인터페이스에 정의 된 멤버에 대 한 구현을 제공 함을 나타냅니다.  
  
## <a name="remarks"></a>설명  
키워드는 [Implements 문과 다릅니다.](../../../visual-basic/language-reference/statements/implements-statement.md) `Implements` `Implements` 문을 사용 하 여 하나 이상의 인터페이스를 구현 하는 클래스 또는 구조체를 지정 하 고 각 멤버에 대해 `Implements` 키워드를 사용 하 여 인터페이스 및 인터페이스를 구현 하는 멤버를 지정 합니다.

클래스 또는 구조체에서 인터페이스를 구현 하는 경우 [클래스 문](../../../visual-basic/language-reference/statements/class-statement.md) 또는 `Implements` [구조체 문](../../../visual-basic/language-reference/statements/structure-statement.md)바로 뒤에 문을 포함 해야 하며, 인터페이스에서 정의 된 모든 멤버를 구현 해야 합니다.

## <a name="reimplementation"></a>재구현  
파생 클래스에서 기본 클래스가 이미 구현 된 인터페이스 멤버를 다시 구현할 수 있습니다. 이는 다음과 같은 측면에서 기본 클래스 멤버를 재정의 하는 것과는 다릅니다.

- 기본 클래스 멤버는 다시 구현 수 있도록 [재정의할](../../../visual-basic/language-reference/modifiers/overridable.md) 필요가 없습니다.
- 다른 이름을 사용 하 여 멤버를 다시 구현할 수 있습니다.

키워드 `Implements` 는 다음 컨텍스트에서 사용할 수 있습니다.

- [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>참고자료

- [Implements 문](../../../visual-basic/language-reference/statements/implements-statement.md)
- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
