---
title: MustOverride(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.MustOverride
- MustOverride
helpviewer_keywords:
- virtual elements [Visual Basic], pure
- elements [Visual Basic], pure virtual
- properties [Visual Basic], redefining
- procedures [Visual Basic], overriding
- overriding, MustOverride keyword
- procedures [Visual Basic], redefining
- pure virtual elements [Visual Basic]
- MustOverride keyword [Visual Basic]
- properties [Visual Basic], overriding
ms.assetid: 6e9d9ad6-bb64-433f-b32b-3ef84293bf96
ms.openlocfilehash: f5932b28c4664dd59dad829228f2186e78108af5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64661250"
---
# <a name="mustoverride-visual-basic"></a>MustOverride(Visual Basic)
속성 또는 프로시저가이 클래스에서 구현 되지 않습니다 및 사용할 수 전에 파생된 클래스에서 재정의 해야 합니다를 지정 합니다.  
  
## <a name="remarks"></a>설명  
 속성 또는 프로시저 선언문에서만 `MustOverride`를 사용할 수 있습니다. 속성을 지정 하는 절차 `MustOverride` 클래스의 멤버 여야 합니다 클래스를 표시 해야 합니다 [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)합니다.  
  
## <a name="rules"></a>규칙  
  
- **완료 되지 않은 선언입니다.** 지정 하는 경우 `MustOverride`, 되지 모든 추가 속성 또는 프로시저에 대 한 코드 줄을 지정 하지 않으면 아무리 `End Function`, `End Property`, 또는 `End Sub` 문입니다.  
  
- **결합 된 한정자입니다.** 지정할 수 없습니다 `MustOverride` 와 함께 `NotOverridable`를 `Overridable`, 또는 `Shared` 같은 선언에 있습니다.  
  
- **숨기기와 재정의 합니다.** 숨김과 재정의는 둘 다 상속된 요소를 다시 정의하지만 두 방법에는 중요한 차이점이 있습니다. 자세한 내용은 [Visual Basic의 숨김 기능](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)합니다.  
  
- **대체 용어입니다.** 재정의에서 제외 하 고 사용할 수 없는 요소 라고도 함은 *순수 가상* 요소입니다.  
  
 `MustOverride` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.  
  
 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>참고자료

- [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)
- [재정의 가능](../../../visual-basic/language-reference/modifiers/overridable.md)
- [재정의](../../../visual-basic/language-reference/modifiers/overrides.md)
- [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)
- [C++ 키워드](../../../visual-basic/language-reference/keywords/index.md)
- [Visual Basic의 숨김 기능](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
