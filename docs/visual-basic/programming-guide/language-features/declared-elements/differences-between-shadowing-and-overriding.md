---
title: 숨기기와 재정의의 차이점(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- shadowing, vs. overriding
- overriding, vs. shadowing
ms.assetid: 2d014a0b-7630-407d-8f4e-24bd87987923
ms.openlocfilehash: 8fcf43040e9cbbcb2a59b1e1cf8c1f58951d5d87
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64610471"
---
# <a name="differences-between-shadowing-and-overriding-visual-basic"></a>숨기기와 재정의의 차이점(Visual Basic)
기본 클래스에서 상속 되는 클래스를 정의 하는 경우 하나 이상의 파생된 클래스에서 기본 클래스 요소를 다시 정의 하려는 경우가 있습니다. 숨기기와 재정의이 목적을 위해는 둘 다 사용할 수 있습니다.  
  
## <a name="comparison"></a>비교  
 숨기기와 재정의는 파생된 클래스는 기본 클래스에서 상속 하 고 다른 하나의 선언 된 요소를 다시 정의 둘 다 사용 둘 다. 하지만 둘 사이 중요 한 차이가 있습니다.  
  
 다음 표에서 비교 숨김과 재정의 합니다.  
  
||||  
|---|---|---|  
|비교의 지점|섀도잉|재정의|  
|용도|파생된 클래스에서 이미 정의 된 멤버를 소개 하는 후속 기본 클래스 수정 으로부터 보호|프로시저 또는 속성이 호출 순서를 사용 하 여의 다른 구현을 정의 하 여 다형성을 달성<sup>1</sup>|  
|재정의 되는 요소|선언 된 요소 형식|프로시저에만 (`Function`하십시오 `Sub`, 또는 `Operator`) 또는 속성|  
|재정의 요소|선언 된 요소 형식|프로시저 또는 속성과 같은 호출 시퀀스<sup>1</sup>|  
|재정의 요소 액세스 수준|다른 액세스 수준|재정의 된 요소의 액세스 수준을 변경할 수 없습니다.|  
|읽기 및 쓰기 가능성 재정의 요소|조합|또는 재정의 된 속성의 쓰기 가능성을 변경할 수 없습니다.|  
|재정의 제어|기본 클래스 요소 적용 없거나 섀도잉 금지|기본 클래스 요소를 지정할 수 있습니다 `MustOverride`, `NotOverridable`, 또는 `Overridable`|  
|키워드 사용|`Shadows` 파생된 클래스에서 권장 `Shadows` 둘 다 하는 경우를 가정 `Shadows` 도 `Overrides` 지정<sup>2</sup>|`Overridable` 또는 `MustOverride` 기본 클래스에 필요 `Overrides` 파생된 클래스에서 필요 합니다.|  
|파생된 클래스에서 파생 된 클래스에서 재정의 되는 요소 상속|요소 숨기기 상속한 추가로 파생 되는 클래스입니다. 숨겨진된 요소는 여전히 숨겨져<sup>3</sup>|요소를 재정의 하 여 상속 된 추가 클래스 파생 재정의 된 요소는 여전히 재정의|  
  
 <sup>1</sup> 는 *호출 시퀀스* 요소 형식으로 구성 됩니다 (`Function`를 `Sub`를 `Operator`, 또는 `Property`), 이름, 매개 변수 목록 및 반환 형식입니다. 속성 또는 그 반대로 사용 하 여 프로시저를 재정의할 수 없습니다. 일종의 프로시저를 재정의할 수 없습니다 (`Function`, `Sub`, 또는 `Operator`) 다른 종류입니다.  
  
 <sup>2</sup> 지정 하지 않는 경우 `Shadows` 또는 `Overrides`, 컴파일러가 경고 메시지를 사용 하려는 재정의 유형을 확인할 수 있도록 합니다. 이 경고를 무시 하는 경우에 섀도잉 메커니즘이 사용 됩니다.  
  
 <sup>3</sup> 섀도잉 요소 추가 파생된 클래스에서 액세스할 수 없는 경우 섀도잉 상속 되지 않습니다. 예를 들어, 숨기는 요소를 선언 하는 경우 `Private`, 파생된 클래스에서 파생 된 클래스는 섀도잉 요소 대신 원래 요소를 상속 합니다.  
  
## <a name="guidelines"></a>지침  
 일반적으로 다음과 같은 경우 재정의 사용 합니다.  
  
- 파생된 클래스 다형 정의 됩니다.  
  
- 안전을 컴파일러는 동일한 요소 형식 및 호출 시퀀스를 적용 해야 합니다.  
  
 일반적으로 다음과 같은 경우 숨기기를 사용 합니다.  
  
- 기본 클래스 수정 될 수 있으며이 사용자와 동일한 이름을 사용 하는 요소를 정의 하는 예상 합니다.  
  
- 요소 형식을 변경 하거나 호출 시퀀스의 자유를 원하고 있습니다.  
  
## <a name="see-also"></a>참고자료

- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Visual Basic의 숨김 기능](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
- [방법: 변수 이름이 같은 변수 숨기기](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)
- [방법: 상속된 된 변수 숨기기](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)
- [방법: 파생된 클래스에 의해 숨겨진 변수에 액세스](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)
- [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
- [재정의](../../../../visual-basic/language-reference/modifiers/overrides.md)
