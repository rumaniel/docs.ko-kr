---
title: '방법: (Visual Basic) 속성에서 값 가져오기'
ms.date: 07/20/2015
helpviewer_keywords:
- property values [Visual Basic]
- Visual Basic code, procedures
- values [Visual Basic], properties
- Visual Basic code, properties
- properties [Visual Basic], values
ms.assetid: 3954423e-6ab7-4a4c-b55c-a8d27be47891
ms.openlocfilehash: 5e2676a0880092a78405fe5dafa0469161b85610
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61863638"
---
# <a name="how-to-get-a-value-from-a-property-visual-basic"></a>방법: (Visual Basic) 속성에서 값 가져오기
식에서 속성 이름을 포함 하 여 속성의 값을 검색 합니다.  
  
 속성의 `Get` 프로시저는 값을 검색 하지만 명시적으로 호출 하지 해당 이름으로 합니다. 변수를 사용할 때 처럼 속성을 사용 합니다. Visual Basic에서는 속성의 프로시저를 호출 합니다.  
  
### <a name="to-retrieve-a-value-from-a-property"></a>속성에서 값을 검색 하려면  
  
1. 변수 이름을 사용 하는 동일한 방식으로 식에서 속성 이름을 사용 합니다. 속성을 사용 하 여 어디서 나 변수 또는 상수를 사용할 수 있습니다.  
  
     또는  
  
     다음에 오는 속성 이름 사용 (`=`) 대입문에 로그인 합니다.  
  
     다음 예제에서는 Visual Basic의 값을 읽습니다 `Now` 속성을 호출 하는 암시적으로 해당 `Get` 프로시저입니다.  
  
     [!code-vb[VbVbalrDateProperties#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDateProperties/VB/Module1.vb#4)]  
  
2. 속성 인수를 사용 하는 경우에 속성 이름을 괄호로 묶어 인수 목록에 따릅니다. 인수가 없는 경우에 필요에 따라 괄호를 생략할 수 있습니다.  
  
3. 쉼표로 구분 하 여 괄호 안에 인수 목록의 인수를 배치 합니다. 속성은 해당 매개 변수 정의 동일한 순서로 인수를 지정 해야 합니다.  
  
 변수 처럼 식에 참여 하는 속성의 값 또는 상수 또는 변수 또는 대입문의 왼쪽에는 속성에 저장 됩니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [속성 프로시저](./property-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Property 문](../../../../visual-basic/language-reference/statements/property-statement.md)
- [Visual Basic에서 속성과 변수의 차이점](./differences-between-properties-and-variables.md)
- [방법: 속성 만들기](./how-to-create-a-property.md)
- [방법: 액세스 수준이 혼합된 된 속성 선언](./how-to-declare-a-property-with-mixed-access-levels.md)
- [방법: 속성 프로시저 호출](./how-to-call-a-property-procedure.md)
- [방법: 선언 및 Visual Basic의 기본 속성을 호출](./how-to-declare-and-call-a-default-property.md)
- [방법: 속성 값 입력](./how-to-put-a-value-in-a-property.md)
