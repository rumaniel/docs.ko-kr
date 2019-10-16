---
title: 선언 컨텍스트 및 기본 액세스 수준(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- module level, defined
- declaration contexts, Visual Basic
- procedure level, defined
- namespace level, defined
- access levels, Visual Basic
- access levels, default levels
ms.assetid: bf63b96e-e825-4745-88c8-5dae222728db
ms.openlocfilehash: 05c2d6420526b660ead2f50eba7feb6b20524705
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623936"
---
# <a name="declaration-contexts-and-default-access-levels-visual-basic"></a>선언 컨텍스트 및 기본 액세스 수준(Visual Basic)
이 항목에는 Visual Basic 형식은 다른 형식 내에서 선언 될 수 있으며 어떤 액세스 수준을 기본적으로 지정 되지 않은 경우 설명 합니다.  
  
## <a name="declaration-context-levels"></a>선언 컨텍스트 수준  
 합니다 *선언 컨텍스트* 프로그래밍 요소의 선언 되는 코드의 영역입니다. 이 호출 되어 다른 프로그래밍 요소에 자주 발생 합니다 *요소가 포함 된*.  
  
 선언 컨텍스트의 수준은 다음과 같습니다.  
  
- *Namespace 수준* -클래스, 구조체, 모듈 또는 인터페이스를 제외한 소스 파일 또는 네임 스페이스 내  
  
- *모듈 수준* -클래스, 구조체, 모듈 또는 인터페이스 제외한 프로시저 또는 블록 내  
  
- *프로시저 수준* -프로시저 또는 블록 내에서 (같은 `If` 또는 `For`)  
  
 다음 표에서 해당 선언 컨텍스트에 따라 다양 한 선언 된 프로그래밍 요소에 대 한 기본 액세스 수준을 보여 줍니다.  
  
|선언 요소|Namespace 수준|모듈 수준|프로시저 수준|  
|----------------------|---------------------|------------------|---------------------|  
|변수 ([Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md))|허용되지 않음|`Private` (`Public` 에 `Structure`에서 허용 되지 않음, `Interface`)|`Public`|  
|상수 ([Const 문](../../../visual-basic/language-reference/statements/const-statement.md))|허용되지 않음|`Private` (`Public` 에 `Structure`에서 허용 되지 않음, `Interface`)|`Public`|  
|열거형 ([Enum 문](../../../visual-basic/language-reference/statements/enum-statement.md))|`Friend`|`Public`|허용되지 않음|  
|클래스 ([Class 문](../../../visual-basic/language-reference/statements/class-statement.md))|`Friend`|`Public`|허용되지 않음|  
|구조체 ([문을 구조체](../../../visual-basic/language-reference/statements/structure-statement.md))|`Friend`|`Public`|허용되지 않음|  
|모듈 ([Module 문](../../../visual-basic/language-reference/statements/module-statement.md))|`Friend`|허용되지 않음|허용되지 않음|  
|인터페이스 ([Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md))|`Friend`|`Public`|허용되지 않음|  
|프로시저 ([Function 문](../../../visual-basic/language-reference/statements/function-statement.md)하십시오 [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md))|허용되지 않음|`Public`|허용되지 않음|  
|외부 참조 ([Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md))|허용되지 않음|`Public` (사용할 수 없습니다 `Interface`)|허용되지 않음|  
|연산자 ([Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md))|허용되지 않음|`Public` (사용할 수 없습니다 `Interface` 또는 `Module`)|허용되지 않음|  
|속성 ([Property 문](../../../visual-basic/language-reference/statements/property-statement.md))|허용되지 않음|`Public`|허용되지 않음|  
|속성의 기본값 ([기본](../../../visual-basic/language-reference/modifiers/default.md))|허용되지 않음|`Public` (사용할 수 없습니다 `Module`)|허용되지 않음|  
|이벤트 ([이벤트 연결 문으로](../../../visual-basic/language-reference/statements/event-statement.md))|허용되지 않음|`Public`|허용되지 않음|  
|대리자 ([Delegate 문](../../../visual-basic/language-reference/statements/delegate-statement.md))|`Friend`|`Public`|허용되지 않음|  
  
 자세한 내용은 [액세스 수준을 Visual Basic의](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)
- [전용](../../../visual-basic/language-reference/modifiers/private.md)
- [공용](../../../visual-basic/language-reference/modifiers/public.md)
