---
title: Imports '<qualifiedelementname>'에 지정된 네임스페이스 또는 형식에 public 멤버가 없거나 해당 네임스페이스 또는 형식을 찾을 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- bc40056
- vbc40056
helpviewer_keywords:
- BC40056
ms.assetid: b59f5754-444f-4378-9272-9678b437e84a
ms.openlocfilehash: 1873c0af7a251afd7754557f5dcb6aed13eb9f11
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61918322"
---
# <a name="namespace-or-type-specified-in-the-imports-qualifiedelementname-doesnt-contain-any-public-member-or-cannot-be-found"></a>Imports'에 지정 된 Namespace 또는 형식을\<qualifiedelementname >' public 멤버가 없거나 찾을 수 없습니다

Imports'에 지정 된 Namespace 또는 형식을\<qualifiedelementname >' public 멤버가 없거나 찾을 수 없습니다. 네임 스페이스 또는 형식 정의 되어 있고 하나 이상의 public 멤버를 포함 하는지 확인 합니다. 별칭 이름에는 다른 별칭 포함 되어 있지 않은지 확인 하십시오.

`Imports` 문에서 지정을 포함 하는 요소를 찾을 수 없습니다를 정의 하지 않습니다 `Public` 멤버입니다.

A *요소가 포함 된* 네임 스페이스, 클래스, 구조체, 모듈, 인터페이스 또는 열거형 일 수 있습니다. 요소를 포함 하는 변수, 프로시저 또는 다른 요소를 포함 하는 등의 멤버를 포함합니다.

가져오기의 목적은 이러한를 한정할 필요 없이 네임 스페이스 또는 형식 멤버에 액세스 하기 위해 코드를 허용 하도록 합니다. 프로젝트 네임 스페이스 또는 형식에 대 한 참조를 추가 해야 할 수 있습니다. 자세한 내용은 "를 포함 하는 요소 가져오기"를 참조 하세요 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)합니다.

컴파일러는 포함 하는 지정 된 요소를 찾을 수 없으면 사용 하는 참조를 확인할 수 없습니다. 요소를 찾습니다 있지만 요소는 노출 하지 않는 경우 `Public` 멤버 다음 참조가 없는 성공할 수 있습니다. 두 경우 모두에서 요소를 가져오는 의미가 없습니다.

포함 하는 요소를 가져오고 가져오기 별칭을 할당 하는 경우 다음 사용할 수 없다는 가져오기 별칭에는 다른 요소를 가져오는 것을 염두에 두십시오. 다음 코드는 컴파일러 오류를 생성 합니다.

```vb
Imports winfrm = System.Windows.Forms

' The following statement is INVALID  because it reuses an import alias.

Imports behave = winfrm.Design.Behavior`
```

**오류 ID:** BC40056

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

1. 포함 하는 요소를 프로젝트에서 액세스할 수 있는지 확인 합니다.

2. 사양의 요소를 포함 하는 다른 가져오기의 모든 가져오기 별칭에 포함 되지 않습니다 확인 합니다.

3. 포함 하는 요소가 하나 이상 노출 확인 `Public` 멤버입니다.

## <a name="see-also"></a>참고자료

- [Imports 문(.NET 네임스페이스 및 형식)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [Namespace 문](../../../visual-basic/language-reference/statements/namespace-statement.md)
- [공용](../../../visual-basic/language-reference/modifiers/public.md)
- [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [선언된 요소 참조](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
