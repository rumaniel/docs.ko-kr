---
title: 수정할 수 있는 인수와 수정할 수 없는 인수 사이의 차이점(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedure arguments
- arguments [Visual Basic], nonmodifiable
- Visual Basic code, procedures
- arguments [Visual Basic], modifiable
ms.assetid: 87b2df69-e1f7-4657-9caf-b3f48d693428
ms.openlocfilehash: a880ae8c13eebd5d9d325468098e058f58d3fa71
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61665951"
---
# <a name="differences-between-modifiable-and-nonmodifiable-arguments-visual-basic"></a>수정할 수 있는 인수와 수정할 수 없는 인수 사이의 차이점(Visual Basic)
프로시저를 호출 하는 경우 일반적으로에 하나 이상의 인수를 전달 합니다. 각 인수는 기본 프로그래밍 요소에 해당합니다. 인수 자체와 내부 요소에 모두 수정할 수 또는 수정할 수 없는 일 수 있습니다.  
  
## <a name="modifiable-and-nonmodifiable-elements"></a>수정할 수 있는 인수와 수정할 수 없는 요소  
 프로그래밍 요소를 수 있습니다는 *수정할 수 있는 요소*, 변경 하 고, 해당 값을 사용할 수 있는 또는 *수정할 수 없는 요소*, 만들어진 후 있는 고정된 값.  
  
 다음 표에서 수정할 수 있는 인수와 수정할 수 없는 프로그래밍 요소를 나열합니다.  
  
|수정할 수 있는 요소|수정할 수 없는 요소|  
|-------------------------|----------------------------|  
|지역 변수 (프로시저 내에서 선언 됨), 읽기 전용으로 제외 하 고 개체 변수를 포함 하 여|읽기 전용 변수, 필드 및 속성|  
|읽기 전용으로 제외 하 고 필드 (모듈, 클래스 및 구조체의 멤버 변수)|상수 및 리터럴|  
|읽기 전용으로 제외 하 고 속성|열거형 멤버|  
|배열 요소|식 (해당 요소는 수정할 수 있는 경우에)|  
  
## <a name="modifiable-and-nonmodifiable-arguments"></a>수정할 수 있는 인수와 수정할 수 없는 인수  
 A *수정할 수 있는 인수* 수정할 수 있는 기본 요소를 사용 하는 합니다. 호출 코드에서 언제 든 지 새 값을 저장할 수 있습니다 및 인수를 전달 하는 경우 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), 프로시저의 코드 호출 코드의 내부 요소를 수정할 수도 있습니다.  
  
 A *수정할 수 없는 인수* 는 내부 요소를 수정할 수 없는 또는 전달 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)합니다. 요소를 수정할 수 있는 경우에 프로시저에서 호출 코드의 내부 요소를 수정할 수 없습니다. 요소를 수정할 수 없는 경우 자체 호출 코드를 수정할 수 없습니다.  
  
 호출된 프로시저 수정 호출 코드의 내부 요소에 영향을 주지 않습니다 하지만 자체 로컬 복사본을 수정할 수 없는 인수를 수정할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [인수를 값으로 전달할 때와 참조로 전달할 때의 차이점](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [방법: 프로시저 인수의 값 변경](./how-to-change-the-value-of-a-procedure-argument.md)
- [방법: 값 변경에 대해 프로시저 인수 보호](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [방법: 인수가 값으로 전달 되도록 설정](./how-to-force-an-argument-to-be-passed-by-value.md)
- [위치 및 이름으로 인수 전달](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
