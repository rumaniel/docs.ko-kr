---
title: Overridable(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Overridable
- vb.Overridable
helpviewer_keywords:
- elements [Visual Basic], concrete
- properties [Visual Basic], redefining
- overriding, Overridable keyword
- elements [Visual Basic], virtual
- virtual [elements VB]
- procedures [Visual Basic], overriding
- concrete [elements VB]
- procedures [Visual Basic], redefining
- Overridable keyword [Visual Basic]
- properties [Visual Basic], overriding
ms.assetid: 612581e7-8a4c-4a5d-beff-3402fffa6f35
ms.openlocfilehash: 91a1cedc66fd66e336b6e7976ad87ad638cb43c3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053901"
---
# <a name="overridable-visual-basic"></a>Overridable(Visual Basic)
속성 또는 프로시저를 동일 하 게 명명 된 속성 또는 프로시저가 파생된 클래스에서 재정의할 수 있음을 지정 합니다.  
  
## <a name="remarks"></a>설명  
 `Overridable` 한정자 파생된 클래스에서 재정의 될 수 클래스에서 속성 또는 메서드를 허용 합니다. 합니다 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md) 파생된 클래스에서 재정의 되는 속성 또는 메서드를 방지 하는 한정자입니다.  자세한 내용은 [상속 기본 사항](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)을 참조하세요.  
  
 경우는 `Overridable` 또는 `NotOverridable` 한정자를 지정 하지 않으면 기본 설정 속성 또는 메서드의 기본 클래스 속성 또는 메서드를 재정의 하는 여부에 따라 달라 집니다. 속성 또는 메서드의 기본 클래스 속성 또는 메서드를 재정의 하는 경우 기본 설정은입니다 `Overridable`이 고, 그렇지 않으면 것 `NotOverridable`입니다.  
  
 섀도 하거나 상속된 된 요소를 다시 정의 하기 위해 재정의할 수 있지만 두 가지 방법 간에 중요 한 차이가 있습니다. 자세한 내용은 [Visual Basic의 숨김 기능](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)합니다.  
  
 재정의할 수 있는 요소는 때때로 이라고 하는 *가상* 요소입니다. 수도 라고를 재정의할 수 있습니다 수 없는 경우에 *구체적인* 요소입니다.  
  
 속성 또는 프로시저 선언문에서만 `Overridable`를 사용할 수 있습니다.  
  
## <a name="combined-modifiers"></a>결합 된 한정자  
 지정할 수 없습니다 `Overridable` 나 `NotOverridable` 에 대 한는 `Private` 메서드.  
  
 지정할 수 없습니다 `Overridable` 와 함께 `MustOverride`를 `NotOverridable`, 또는 `Shared` 같은 선언에 있습니다.  
  
 재정의 요소는 암시적으로 재정의할 수 있으므로 `Overridable`과 `Overrides`를 결합할 수 없습니다.  
  
## <a name="usage"></a>사용  
 `Overridable` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.  
  
 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>참고자료

- [한정자](../../../visual-basic/language-reference/modifiers/index.md)
- [상속 기본 사항](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)
- [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)
- [재정의](../../../visual-basic/language-reference/modifiers/overrides.md)
- [C++ 키워드](../../../visual-basic/language-reference/keywords/index.md)
- [Visual Basic의 숨김 기능](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
