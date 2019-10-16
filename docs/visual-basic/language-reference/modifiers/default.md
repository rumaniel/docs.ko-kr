---
title: Default(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Default
helpviewer_keywords:
- defaults, properties
- properties [Visual Basic], default
- default properties, in Visual Basic
- Default keyword [Visual Basic]
- default properties
ms.assetid: 45fce9b9-d212-4b2d-ab86-6e359b8b57af
ms.openlocfilehash: f78ffe42a9d618d44da2a50c0de831396576430c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61800934"
---
# <a name="default-visual-basic"></a>Default(Visual Basic)
해당 클래스, 구조체 또는 인터페이스의 기본 속성으로 속성을 식별합니다.  
  
## <a name="remarks"></a>설명  
 클래스, 구조체 또는 인터페이스와 해당 속성 중 하나만 지정할 수는 *속성의 기본값을*속성은 하나 이상의 매개 변수가 있는 경우. 코드 멤버를 지정 하지 않고 클래스 또는 구조체에 대 한 참조를 만드는 경우 Visual Basic의 기본 속성에 대 한 해당 참조를 확인 합니다.  
  
 기본 속성 소스 코드의 문자를 약간 저하 될 수 있습니다 하지만 코드를 더 읽기 어렵다고 만들 수 있습니다. 클래스 또는 구조체 이름으로 참조 하는 경우 호출 코드에서 클래스 또는 구조체에 익숙하지 않은 경우 수 없습니다 특정 클래스 또는 구조체 자체를 기본 속성을 참조 하는 액세스 하는 여부. 이 경우 미묘한 런타임 논리 오류나 컴파일러 오류가 발생할 수 있습니다.  
  
 항상 사용 하 여 기본 속성 오류 가능성을 다소 줄일 수 있습니다 합니다 [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md) 컴파일러 형식 검사를 설정 하려면 `On`합니다.  
  
 사용 하 여 미리 정의 된 클래스 또는 구조체 코드에서 결정 해야 기본 속성이 있는지 여부와 하려는 경우 해당 이름 이란 합니다.  
  
 이러한 단점 때문에 기본 속성을 정의 하지 않는 고려해 야 합니다. 코드의 가독성을 높이기 위해 항상 모든 속성에 명시적으로 참조할 수도도 기본 속성 해야 있습니다.  
  
 `Default` 한정자는이 컨텍스트에서 사용할 수 있습니다.  
  
 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## <a name="see-also"></a>참고자료

- [방법: 선언 및 Visual Basic의 기본 속성을 호출](../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)
- [C++ 키워드](../../../visual-basic/language-reference/keywords/index.md)
