---
title: '방법: (Visual Basic) 값을 반환 하는 프로시저 호출'
ms.date: 07/20/2015
helpviewer_keywords:
- procedure calls [Visual Basic], returning values
- Visual Basic code, procedures
- procedures [Visual Basic], calling
- procedures [Visual Basic], returning a value
ms.assetid: a445127b-0f5f-465a-98fb-3e514b93d115
ms.openlocfilehash: 6f45f01489ee84b6addb1f7c7c8dc584332f38dd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61864184"
---
# <a name="how-to-call-a-procedure-that-returns-a-value-visual-basic"></a>방법: (Visual Basic) 값을 반환 하는 프로시저 호출
`Function` 프로시저가 호출 코드에 값을 반환 합니다. 식 또는 대입문의 오른쪽에 있는 이름과 인수를 포함 하 여 프로시저를 호출 합니다.  
  
### <a name="to-call-a-function-procedure-within-an-expression"></a>식 내에서 함수 프로시저를 호출 하려면  
  
1. 사용 하 여는 `Function` 프로시저 변수를 사용할 때 동일한 방식으로 이름을 지정 합니다. 사용할 수는 `Function` 식에서 변수 또는 상수를 사용할 수 있습니다 원격 프로시저 호출 합니다.  
  
2. 괄호로 묶어 인수 목록에 프로시저 이름 뒤에. 인수가 없는 경우에 필요에 따라 괄호를 생략할 수 있습니다. 그러나 괄호를 사용 하 여 쉽게 코드 읽을 수 있습니다.  
  
3. 쉼표로 구분 하 여 괄호 안에 인수 목록의 인수를 배치 합니다. 같은 순서로 인수를 지정 해야 하는 `Function` 프로시저는 해당 매개 변수를 정의 합니다.  
  
     또는 이름으로 하나 이상의 인수를 전달할 수 있습니다. 자세한 내용은 [위치 및 이름별 인수 전달](./passing-arguments-by-position-and-by-name.md)합니다.  
  
4. 변수 값 처럼 식에 참여 하는 프로시저에서 반환 되는 값 또는 상수입니다.  
  
### <a name="to-call-a-function-procedure-in-an-assignment-statement"></a>대입문에서 함수 프로시저를 호출 합니다.  
  
1. 사용 된 `Function` 프로시저 이름 다음에 오는 (`=`) 대입문은 로그인 합니다.  
  
2. 괄호로 묶어 인수 목록에 프로시저 이름 뒤에. 인수가 없는 경우에 필요에 따라 괄호를 생략할 수 있습니다. 그러나 괄호를 사용 하 여 쉽게 코드 읽을 수 있습니다.  
  
3. 쉼표로 구분 하 여 괄호 안에 인수 목록의 인수를 배치 합니다. 같은 순서로 인수를 지정 해야 하는 `Function` 프로시저 이름으로 전달 하려는 경우가 아니면 해당 매개 변수를 정의 합니다.  
  
4. 프로시저에서 반환 되는 값은 변수 또는 대입문의 왼쪽에는 속성에 저장 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 Visual Basic <xref:Microsoft.VisualBasic.Interaction.Environ%2A> 운영 체제 환경 변수의 값을 검색 합니다. 첫 번째 줄에서는 `Environ` 내에서 식과 두 번째 줄에서에서 호출 대입문 합니다. `Environ` 변수 이름을 유일한 인수로 변수로 사용 합니다. 호출 코드에 변수 값을 반환합니다.  
  
 [!code-vb[VbVbcnProcedures#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#7)]  
  
## <a name="see-also"></a>참고자료

- [Function 프로시저](./function-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)
- [방법: 값을 반환 하는 프로시저 만들기](./how-to-create-a-procedure-that-returns-a-value.md)
- [방법: 프로시저에서 값을 반환 합니다.](./how-to-return-a-value-from-a-procedure.md)
- [방법: 값을 반환 하지 않는 프로시저 호출](./how-to-call-a-procedure-that-does-not-return-a-value.md)
